---
title: 기업 구매 프로세스
ms.date: 03/30/2017
ms.assetid: a5e57336-4290-41ea-936d-435593d97055
ms.openlocfilehash: d019c1915e691fcba00fa8f1b0884a898ce02fab
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951520"
---
# <a name="corporate-purchase-process"></a>기업 구매 프로세스
이 샘플에서는 최상의 제안을 자동으로 선택하는 구매 프로세스를 기반으로 매우 기본적인 RFP(제안 요청서)를 만드는 방법을 보여 줍니다. 여기에서는 <xref:System.Activities.Statements.Parallel>, <xref:System.Activities.Statements.ParallelForEach%601> 및 <xref:System.Activities.Statements.ForEach%601>과 사용자 지정 활동을 결합하여 이 프로세스를 나타내는 워크플로를 만듭니다.

 이 샘플에는 다른 참여자 (원래 요청자 또는 특정 공급 업체)로 프로세스와 상호 작용할 수 있도록 하는 ASP.NET 클라이언트 응용 프로그램이 포함 되어 있습니다.

## <a name="requirements"></a>요구 사항

- Visual Studio 2012.

- [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].

## <a name="demonstrates"></a>세부 항목

- 사용자 지정 활동

- 활동의 컴퍼지션

- 책갈피

- 지속성

- 스키마화된 지속성

- 추적(Tracing)

- 추적(Tracking)

- 다른 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 클라이언트 (ASP.NET 웹 응용 프로그램 및 WinForms 응용 프로그램)에서 호스팅.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\PurchaseProcess`  
  
## <a name="description-of-the-process"></a>프로세스 설명  
 이 샘플에서는 일반 회사를 위한 공급 업체의 제안을 수집 하는 WF (Windows Workflow Foundation) 프로그램의 구현을 보여 줍니다.  
  
1. X라는 회사의 직원이 RFP(제안 요청서)를 만듭니다.  
  
    1. 이 직원이 RFP 제목과 설명을 입력합니다.  
  
    2. 제안서를 제출하도록 요청할 공급업체를 선택합니다.  
  
2. 직원이 제안서를 제출합니다.  
  
    1. 워크플로의 인스턴스가 만들어집니다.  
  
    2. 모든 공급업체에서 제안서를 제출할 때까지 워크플로가 대기 상태를 유지합니다.  
  
3. 제안서를 모두 받고 나면 접수된 모든 제안서를 하나씩 돌아가며 워크플로를 실행하고 최상의 제안서 하나를 선택합니다.  
  
    1. 각 공급업체에는 저마다의 평판이 있습니다. 이 샘플에서는 평판 목록을 VendorRepository.cs에 저장합니다.  
  
    2. 제안서의 최종 금액은 (공급업체가 제시한 금액) * (공급업체에 대해 기록된 평판) / 100으로 계산됩니다.  
  
4. 맨 처음 요청자는 제출된 제안서를 모두 볼 수 있습니다. 최상의 제안이 보고서의 특정 섹션에 표시됩니다.  
  
## <a name="process-definition"></a>프로세스 정의  
 이 샘플의 핵심 논리에는 <xref:System.Activities.Statements.ParallelForEach%601> 활동이 사용됩니다. 이 활동에서는 책갈피를 만드는 사용자 지정 활동을 사용하여 각 공급업체의 제안서를 기다린 다음 <xref:System.Activities.Statements.InvokeMethod> 활동을 사용하여 공급업체 제안서를 RFP로 등록합니다.  
  
 그런 다음 이 샘플에서는 접수 후 `RfpRepository`에 저장된 모든 제안서를 하나씩 돌아가며 <xref:System.Activities.Statements.Assign> 활동과 <xref:System.Activities.Expressions> 활동을 사용하여 조정 값을 계산합니다. 지금까지 나온 최상의 제안보다 더 나은 조정 값이 발견되면 <xref:System.Activities.Statements.If> 및 <xref:System.Activities.Statements.Assign> 활동을 사용하여 새 값을 최상의 제안으로 할당합니다.  
  
## <a name="projects-in-this-sample"></a>이 샘플의 프로젝트  
 이 샘플에는 다음 프로젝트가 포함되어 있습니다.  
  
|Project|Description|  
|-------------|-----------------|  
|공용|프로세스 내에 사용되는 엔터티 개체(제안 요청서, 공급업체 및 공급업체 제안서)입니다.|  
|WfDefinition|구매 프로세스 워크플로의 인스턴스를 만들고 사용하기 위해 클라이언트 애플리케이션에 사용되는 프로세스([!INCLUDE[wf1](../../../../includes/wf1-md.md)] 프로그램)와 호스트(`PurchaseProcessHost`)에 대한 정의입니다.|  
|WebClient|사용자가 구매 프로세스의 인스턴스를 만들고 참여할 수 있게 해 주는 ASP.NET client 응용 프로그램입니다. 이 응용 프로그램에서는 워크플로 엔진과 상호 작용하기 위해 사용자 지정하여 만든 호스트를 사용합니다.|  
|WinFormsClient|사용자가 구매 프로세스의 인스턴스를 만들고 여기에 참가할 수 있도록 하는 Windows Forms 클라이언트 애플리케이션입니다. 이 응용 프로그램에서는 워크플로 엔진과 상호 작용하기 위해 사용자 지정하여 만든 호스트를 사용합니다.|  
  
### <a name="wfdefinition"></a>WfDefinition  
 다음 표에는 WfDefinition 프로젝트의 주요 파일에 대한 설명이 나와 있습니다.  
  
|파일|Description|  
|----------|-----------------|  
|IPurchaseProcessHost.cs|워크플로의 호스트에 대한 인터페이스입니다.|  
|PurchaseProcessHost.cs|워크플로에 대한 호스트의 구현입니다. 이 호스트는 워크플로 런타임에 대한 세부 사항을 추상화하며, 모든 클라이언트 애플리케이션에서 `PurchaseProcess` 워크플로 인스턴스를 로드 및 실행하고 상호 작용하는 데 사용됩니다.|  
|PurchaseProcessWorkflow.cs|구매 프로세스 워크플로에 대한 정의가 포함된 활동이며, <xref:System.Activities.Activity>에서 파생됩니다.<br /><br /> <xref:System.Activities.Activity>에서 파생되는 활동은 기존의 사용자 지정 활동과 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 활동 라이브러리에서 가져온 활동을 어셈블하여 기능을 구성합니다. 이 활동을 어셈블하는 것은 사용자 지정 기능을 만드는 가장 기본적인 방법입니다.|  
|WaitForVendorProposal.cs|이 사용자 지정 활동은 <xref:System.Activities.NativeActivity>에서 파생되며, 명명된 책갈피를 만듭니다. 이 책갈피는 나중에 제안서를 제출하는 공급업체가 다시 시작해야 합니다.<br /><br /> <xref:System.Activities.NativeActivity>에서 파생되는 활동과 같이 <xref:System.Activities.CodeActivity>에서 파생되는 활동은 <xref:System.Activities.NativeActivity.Execute%2A>를 재정의하여 명령형 기능을 만들지만, <xref:System.Activities.ActivityContext> 메서드에 전달되는 `Execute`를 통해 워크플로 런타임의 모든 기능에 액세스할 수도 있습니다. 이 컨텍스트에서는 자식 활동 예약 및 취소, 비지속성 영역(원자성 트랜잭션 내에서와 같이 런타임에 워크플로의 데이터가 지속되지 않는 실행 블록) 설정 및 <xref:System.Activities.Bookmark> 개체(일시 중지된 워크플로를 다시 시작하기 위한 핸들)를 지원합니다.|  
|TrackingParticipant.cs|모든 추적 이벤트를 받아 텍스트 파일로 저장하는 <xref:System.Activities.Tracking.TrackingParticipant>입니다.<br /><br /> 추적 참가자가 워크플로 인스턴스에 확장으로 추가됩니다.|  
|XmlWorkflowInstanceStore.cs|워크플로 애플리케이션을 XML 파일에 저장하는 사용자 지정 <xref:System.Runtime.DurableInstancing.InstanceStore>입니다.|  
|XmlPersistenceParticipant.cs|제안 요청의 인스턴스를 XML 파일에 저장하는 사용자 지정 <xref:System.Activities.Persistence.PersistenceParticipant>입니다.|  
|AsyncResult.cs / CompletedAsyncResult.cs|지속성 구성 요소의 비동기 패턴을 구현하기 위한 도우미 클래스입니다.|  
  
### <a name="common"></a>공용  
 다음 표에는 Common 프로젝트의 주요 클래스에 대한 설명이 나와 있습니다.  
  
|클래스|설명|  
|-----------|-----------------|  
|Vendor|제안 요청서에 제안을 제출하는 공급업체입니다.|  
|RequestForProposal|RFP(제안 요청서)는 특정 상품이나 서비스에 대한 제안서를 제출하도록 공급업체에 요청하는 초대장입니다.|  
|VendorProposal|공급업체가 구체적인 RFP에 대해 제출한 제안서입니다.|  
|VendorRepository|공급업체의 리포지토리입니다. 이 구현에는 공급업체 인스턴스의 메모리 내 컬렉션과 해당 인스턴스를 노출하기 위한 메서드가 포함됩니다.|  
|RfpRepository|제안 요청서의 리포지토리입니다. 이 구현에는 스키마화된 지속성에 의해 생성된 제안 요청서의 XML 파일을 쿼리하기 위한 Linq to XML 사용이 포함됩니다. |  
|IOHelper|이 클래스는 모든 I/O 관련 문제(폴더, 경로 등)를 처리합니다.|  
  
### <a name="web-client"></a>웹 클라이언트  
 다음 표에는 WebClient 프로젝트의 주요 웹 페이지에 대한 설명이 나와 있습니다.  
  
|파일|Description|  
|-|-|  
|CreateRfp.aspx|새 제안 요청서를 만들고 제출합니다.|  
|Default.aspx|활성화된 제안 요청서와 완료된 제안 요청서를 모두 표시합니다.|  
|GetVendorProposal.aspx|구체적인 제안 요청서에 대해 공급업체의 제안서를 가져옵니다. 이 페이지는 공급업체에서만 사용합니다.|  
|ShowRfp.aspx|제안 요청서에 대한 모든 정보(접수된 제안서, 날짜, 금액 및 기타 정보)를 표시합니다. 이 페이지는 제안 요청서의 작성자만 사용합니다.|  
  
### <a name="winforms-client"></a>WinFormsClient  
 다음 표에는 WinFormsClient 프로젝트의 주요 폼에 대한 설명이 나와 있습니다.  
  
|Form|Description|  
|-|-|  
|NewRfp|새 제안 요청서를 만들고 제출합니다.|  
|ShowProposals|활성화된 제안 요청서와 완료된 제안 요청서를 모두 표시합니다. **참고:**  제안에 대 한 요청을 만들거나 수정한 후 해당 화면에 변경 내용을 표시 하려면 UI에서 **새로 고침** 단추를 클릭 해야 할 수도 있습니다.|  
|SubmitProposal|구체적인 제안 요청서에 대해 공급업체의 제안서를 가져옵니다. 이 창은 공급업체에서만 사용합니다.|  
|ViewRfp|제안 요청서에 대한 모든 정보(접수된 제안서, 날짜, 금액 및 기타 정보)를 표시합니다. 이 창은 제안 요청서의 작성자만 사용합니다.|  
  
### <a name="persistence-files"></a>지속성 파일  
 다음 표에는 지속성 공급자(`XmlPersistenceProvider`)가 생성하는 파일이 나와 있습니다. 이 파일은 <xref:System.IO.Path.GetTempPath%2A>를 사용하여 현재 시스템의 임시 폴더 경로에 저장됩니다. 추적 파일은 현재 실행 경로에 만들어집니다.  
  
|파일 이름|설명|경로|  
|-|-|-|  
|rfps.xml|활성화된 제안 요청서와 완료된 제안 요청서가 모두 포함된 XML 파일입니다.|<xref:System.IO.Path.GetTempPath%2A>|  
|[instanceid]|이 파일에는 워크플로 인스턴스에 대한 모든 정보가 포함됩니다.<br /><br /> 이 파일은 스키마화된 지속성 구현(XmlPersistenceProvider의 PersistenceParticipant)을 통해 생성됩니다.|<xref:System.IO.Path.GetTempPath%2A>|  
|[instanceId].tracking|구체적인 인스턴스 내에서 발생하는 모든 이벤트가 포함된 텍스트 파일입니다.<br /><br /> 이 파일은 TrackingParticipant에 의해 생성됩니다.|<xref:System.IO.Path.GetTempPath%2A>|  
|PurchaseProcess.Tracing.TraceLog.txt|App.config 또는 Web.config 파일의 구성 매개 변수를 기반으로 하여 워크플로를 통해 생성되는 추적 파일입니다.|현재 실행 경로|  
  
#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면  
  
1. Visual Studio 2010을 사용 하 여 PurchaseProcess 솔루션 파일을 엽니다.  
  
2. 웹 클라이언트 프로젝트를 실행 하려면 **솔루션 탐색기** 열고 **웹 클라이언트** 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. **시작 프로젝트로 설정을**선택 합니다.  
  
3. WinForms Client 프로젝트를 실행 하려면 **솔루션 탐색기** 을 열고 **WinForms client** 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. **시작 프로젝트로 설정을**선택 합니다.  
  
4. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.  
  
5. Ctrl+F5를 눌러 솔루션을 실행합니다.  
  
### <a name="web-client-options"></a>웹 클라이언트 옵션  
  
- **새 RFP을 만듭니다**. 제안 (RFP)에 대 한 새 요청을 만들고 구매 프로세스 워크플로를 시작 합니다.  
  
- **새로 고침**: 주 창에서 활성 및 완료 된 Rfp 목록을 새로 고칩니다.  
  
- **보기**: 기존 RFP의 콘텐츠를 표시 합니다. RFP가 완료되지 않았거나 공급업체가 요청을 받은 경우 공급업체에서 제안서를 제출할 수 있습니다.  
  
- 다음으로 보기: 사용자는 active Rfp 표의 **보기 형식** 콤보 상자에서 원하는 참가자를 선택 하 여 다른 id를 사용 하 여 RFP에 액세스할 수 있습니다.  
  
### <a name="winforms-client-options"></a>WinForms 클라이언트 옵션  
  
- **RFP 만들기**: 제안 (RFP)에 대 한 새 요청을 만들고 구매 프로세스 워크플로를 시작 합니다.  
  
- **새로 고침**: 주 창에서 활성 및 완료 된 Rfp 목록을 새로 고칩니다.  
  
- **RFP 보기**: 기존 RFP의 콘텐츠를 표시 합니다. RFP가 완료되지 않았거나 공급업체가 요청을 받은 경우 공급업체에서 제안서를 제출할 수 있습니다.  
  
- **연결 이름**: 사용자는 active Rfp 표의 **보기 형식** 콤보 상자에서 원하는 참가자를 선택 하 여 다른 id를 사용 하 여 RFP에 액세스할 수 있습니다.
