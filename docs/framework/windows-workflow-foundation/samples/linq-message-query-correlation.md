---
title: LINQ 메시지 쿼리 상관 관계
ms.date: 03/30/2017
ms.assetid: b746872e-57b1-4514-b337-53398a0e0deb
ms.openlocfilehash: 202d65914d32245952f308d3115ec93231f95f15
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989332"
---
# <a name="linq-message-query-correlation"></a>LINQ 메시지 쿼리 상관 관계
이 샘플에서는 시스템에서 제공하는 <xref:System.ServiceModel.Dispatcher.MessageQuery> 대신 사용자 지정 <xref:System.ServiceModel.XPathMessageQuery> 구현을 사용하여 내용 기반 상관 관계를 만드는 방법을 보여 줍니다.  
  
## <a name="demonstrates"></a>세부 항목  
 사용자 지정 <xref:System.ServiceModel.Dispatcher.MessageQuery>, 내용 기반 상관 관계  
  
## <a name="discussion"></a>토론  
 이 샘플에서는 상관 관계를 만들기 위해 <xref:System.ServiceModel.Dispatcher.MessageQuery> 기본 클래스를 확장하는 방법을 보여 줍니다. 사용자 지정 `LinqMessageQuery`를 구현하면 XLinq를 사용하여 메시지 내에서 XName을 찾을 수 있습니다. 쿼리를 통해 검색한 데이터는 메시지를 적절한 워크플로 인스턴스로 디스패치하기 위한 상관 관계 키를 만드는 데 사용됩니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. 이 샘플에서는 HTTP 엔드포인트를 사용하여 워크플로 서비스를 노출합니다. 이 샘플을 실행 하려면 Visual Studio를 관리자 권한으로 실행 하거나 관리자 권한 프롬프트에서 다음 명령을 실행 하 여 적절 한 Acl을 추가 하 여 적절 한 URL Acl을 추가 해야 합니다 (자세한 내용은 [HTTP 및 HTTPS 구성](https://go.microsoft.com/fwlink/?LinkId=70353) 참조). 도메인과 사용자 이름이 대체되었는지 확인합니다.  
  
    ```console  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2. URL ACL이 추가되었으면 다음 단계를 사용합니다.  
  
    1. 솔루션을 빌드합니다.  
  
    2. 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트 설정**을 선택 하 여 여러 시작 프로젝트를 설정 합니다. **서비스** 와 **클라이언트** (해당 순서로)를 여러 시작 프로젝트로 추가 합니다.  
  
    3. 애플리케이션을 실행합니다. 주문서를 보내고 구매 주문서 ID를 받은 다음 주문을 확인하는 워크플로가 클라이언트 콘솔에 표시됩니다. 처리 중인 요청이 서비스 창에 표시됩니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\LinqMessageQueryCorrelation`
