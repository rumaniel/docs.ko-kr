---
title: 일시 중단된 인스턴스 관리
ms.date: 03/30/2017
ms.assetid: f5ca3faa-ba1f-4857-b92c-d927e4b29598
ms.openlocfilehash: 7a2f36ac2c127376eea56601f54aa5e571d66a55
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70037885"
---
# <a name="suspended-instance-management"></a>일시 중단된 인스턴스 관리
이 샘플에서는 일시 중단된 워크플로 인스턴스를 관리하는 방법을 보여 줍니다.  <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>의 기본 동작은 `AbandonAndSuspend`입니다. 즉, 기본적으로 <xref:System.ServiceModel.WorkflowServiceHost>에서 호스트되는 워크플로 인스턴스에서 처리되지 않은 예외가 throw될 경우 인스턴스가 메모리에서 삭제(중단)되고 영속/지속적 버전의 인스턴스는 일시 중단된 인스턴스로 표시됩니다. 일시 중단된 워크플로 인스턴스는 일시 중단이 해제될 때까지 실행할 수 없습니다.

 이 샘플에서는 일시 중단된 인스턴스를 쿼리하는 명령줄 유틸리티를 구현하는 방법과 사용자에게 해당 인스턴스를 다시 시작하거나 종료하는 옵션을 제공하는 방법을 보여 줍니다. 이 샘플에서는 워크플로 서비스가 의도적으로 예외를 throw하여 일시 중단 상태가 됩니다. 그런 다음 명령줄 유틸리티를 사용하여 인스턴스를 쿼리하고 이후에 인스턴스를 다시 시작하거나 종료할 수 있습니다.

## <a name="demonstrates"></a>세부 항목
 <xref:System.ServiceModel.WorkflowServiceHost>WF (Windows Workflow Foundation)를 사용 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> 합니다. <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>

## <a name="discussion"></a>토론
 이 샘플에서 구현하는 명령줄 유틸리티는 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]에서 제공되는 SQL 인스턴스 저장소 구현에 따라 다릅니다. 인스턴스 저장소의 사용자 지정 구현이 있는 경우 샘플의 `WorkflowInstanceCommand` 구현을 현재 인스턴스 저장소와 관련된 구현으로 바꿔 이 유틸리티를 적용할 수 있습니다.

 제공된 구현에서는 SQL 인스턴스 저장소에 대해 직접 SQL 명령을 실행하여 일시 중단된 인스턴스를 나열하고, 인스턴스를 다시 시작하거나 종료하기 위해 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>에 추가된 <xref:System.ServiceModel.WorkflowServiceHost>를 사용합니다.

#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 이 샘플에는 다음과 같은 Windows 구성 요소를 사용해야 합니다.

    1. MSMQ(Microsoft Message Queue) Server

    2. SQL Server Express

2. SQL Server 데이터베이스를 설정합니다.

    1. Visual Studio 2010 명령 프롬프트에서 다음을 수행 하는 SuspendedInstanceManagement 샘플 디렉터리에서 "setup.exe"를 실행 합니다.

        1. SQL Server Express를 사용하여 지속성 데이터베이스를 만듭니다. 지속성 데이터베이스가 이미 있으면 삭제된 다음 다시 만들어집니다.

        2. 지속성 데이터베이스를 설정합니다.

        3. 지속성 데이터베이스를 설정할 때 정의된 InstanceStoreUsers 역할에 IIS APPPOOL\DefaultAppPool 및 NT AUTHORITY\Network Service를 추가합니다.

3. 서비스 큐를 설정합니다.

    1. Visual Studio 2010에서 **SampleWorkflowApp** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트로 설정**을 클릭 합니다.

    2. **F5**키를 눌러 SampleWorkflowApp를 컴파일하고 실행 합니다. 이렇게 하면 필요한 큐가 만들어집니다.

    3. **Enter** 키를 눌러 SampleWorkflowApp을 중지 합니다.

    4. 명령 프롬프트에서 Compmgmt.msc를 실행하여 컴퓨터 관리 콘솔을 엽니다.

    5. **서비스 및 응용 프로그램**, **메시지 큐**, **개인 큐**를 차례로 확장 합니다.

    6. **ReceiveTx** 큐를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.

    7. **보안** 탭을 선택 하 고 **모든 사용자** 가 메시지를 **받고**, 메시지를 읽고, **메시지를 보낼**수 있는 권한을 갖도록 허용 합니다.

4. 이제 샘플을 실행합니다.

    1. Visual Studio 2010에서 **Ctrl + F5**를 눌러 디버깅 하지 않고 SampleWorkflowApp 프로젝트를 다시 실행 합니다. 두 엔드포인트 주소가 콘솔 창에 출력됩니다. 이 주소 중 하나를 애플리케이션 엔드포인트에 대한 주소이고, 다른 하나는 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>의 주소입니다. 그런 다음 워크플로 인스턴스가 만들어지고, 해당 인스턴스에 대한 추적 레코드가 콘솔 창에 나타납니다. 워크플로 인스턴스를 예외를 throw하며, 인스턴스가 일시 중단되고 중단됩니다.

    2. 명령줄 유틸리티를 사용하여 모든 인스턴스에 대해 추가 동작을 수행할 수 있습니다. 명령줄 인수에 대한 구문은 다음과 같습니다.

         `SuspendedInstanceManagement -Command:[CommandName] -Server:[ServerName] -Database:[DatabaseName] -InstanceId:[InstanceId]`

         지원되는 명령은 `Query`, `Resume` 및 `Terminate`이며,  InstanceId 스위치는 `Resume` 및 `Terminate` 작업에만 필요합니다.

#### <a name="to-cleanup-optional"></a>정리하려면(옵션)

1. `vs2010` 명령 프롬프트에서 Compmgmt.msc를 실행하여 컴퓨터 관리 콘솔을 엽니다.

2. **서비스 및 응용 프로그램**, **메시지 큐**, **개인 큐**를 차례로 확장 합니다.

3. **ReceiveTx** 큐를 삭제 합니다.

4. 지속성 데이터베이스를 제거하려면 cleanup.cmd를 실행합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\SuspendedInstanceManagement`
