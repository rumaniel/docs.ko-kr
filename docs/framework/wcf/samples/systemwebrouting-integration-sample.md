---
title: SystemWebRouting Integration 샘플
ms.date: 03/30/2017
ms.assetid: f1c94802-95c4-49e4-b1e2-ee9dd126ff93
ms.openlocfilehash: 032be700beaa38ed6c08ed1940aab558b2106591
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964489"
---
# <a name="systemwebrouting-integration-sample"></a>SystemWebRouting Integration 샘플
이 샘플에서는 호스팅 계층과 <xref:System.Web.Routing> 네임스페이스에 있는 클래스의 통합을 보여 줍니다. <xref:System.Web.Routing> 네임스페이스의 클래스를 사용하면 애플리케이션에서 실제 리소스에 직접적으로 해당하지 않는 URL을 사용할 수 있습니다. 개발자는 웹 라우팅을 사용 하 여 HTTP에 대 한 가상 주소를 만든 다음 실제 WCF 서비스에 다시 매핑할 수 있습니다. 이렇게 하면 실제 파일 또는 리소스 없이 WCF 서비스를 호스트해야 하거나 .html 또는 .aspx와 같은 파일 확장명이 포함되지 않은 URL을 사용하여 서비스에 액세스해야 하는 경우에 유용합니다. 이 샘플에서는 <xref:System.Web.Routing.RouteTable> 클래스를 사용하여 global.asax에 정의된 실행 중인 서비스에 매핑되는 가상 URI를 만드는 방법을 보여 줍니다. 

> [!NOTE]
> <xref:System.Web.Routing> 네임스페이스의 클래스는 HTTP를 통해 호스트되는 서비스에 대해서만 작동합니다.  
  
이 예제에서는 WCF를 사용 하 여 `movies` 피드 `channels` 및 피드의 두 RSS 피드를 만듭니다. 서비스를 활성화 하는 url은 확장을 포함 하지 않으며 `Application_Start` <xref:System.Web.HttpApplication> 클래스에서 파생 된 `Global` 클래스의 메서드에 등록 됩니다.  
  
> [!NOTE]
> IIS 6.0에서 확장 Url을 지원 하기 위해 다른 방법을 사용 하므로이 샘플은 인터넷 정보 서비스 (IIS) 7.0 이상 에서만 작동 합니다.  

#### <a name="to-download-this-sample"></a>이 샘플을 다운로드 하려면
  
이 샘플은 컴퓨터에 이미 설치 되어 있을 수 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
   
`<InstallDrive>:\WF_WCF_Samples`  
   
 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
   
`<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebRoutingIntegration`  
  
#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면  
  
1. Visual Studio를 사용 하 여 WebRoutingIntegration .sln 파일을 엽니다.  
  
2. F5 키를 눌러 솔루션을 실행하고 웹 개발 서버를 시작합니다.  
  
     샘플의 디렉터리 목록이 나타납니다. 파일 확장명이 .svc인 파일은 없습니다.  
  
3. 주소 표시줄에서 URL에를 `movies` 추가 하 여를 읽고 `http://localhost:[port]/movies` enter 키를 누릅니다.  
  
     movies 피드가 브라우저에 나타납니다.  
  
4. 주소 표시줄에서을 (를 `channels` ) 읽도록 `http://localhost:[port]/channels` URL에를 추가 하 고 enter 키를 누릅니다.  
  
     channels 피드가 브라우저에 나타납니다.  
  
5. Alt+F4를 눌러 웹 브라우저를 닫습니다.  
  
     개발 서버가 종료 되지 않은 경우 알림 영역 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **중지**를 선택 합니다.  
  
#### <a name="to-use-this-sample-when-hosted-in-iis"></a>IIS에서 호스트될 때 이 샘플을 사용하려면  
  
1. Visual Studio를 사용 하 여 WebRoutingIntegration .sln 파일을 엽니다.  
  
2. Ctrl+Shift+B를 눌러 프로젝트를 빌드합니다.  
  
3. IIS(인터넷 정보 서비스) 관리자에서 웹 애플리케이션을 만듭니다.  
  
    1. IIS 관리자에서 **기본 웹 사이트** 를 마우스 오른쪽 단추로 클릭 하 고 **응용 프로그램 추가**를 선택 합니다.  
  
    2. **별칭**에 대해를 입력 `WebRoutingIntegration`합니다.  
  
    3. **실제 경로**의 경우 프로젝트 내에서 서비스 폴더를 선택 합니다.  
  
    4. **확인**을 누릅니다.  
  
4. 웹 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 **응용 프로그램 관리** 를 선택한 다음 **찾아보기**를 선택 하 여 응용 프로그램을 시작 합니다.  
  
5. 주소 표시줄에서을 (를 `movies` ) 읽도록 `http://localhost:[port]/movies` URL에를 추가 하 고 enter 키를 누릅니다.  
  
     movies 피드가 브라우저에 나타납니다.  
  
6. 주소 표시줄에서을 (를 `channels` ) 읽도록 `http://localhost:[port]/channels` URL에를 추가 하 고 enter 키를 누릅니다.  
  
     channels 피드가 브라우저에 나타납니다.  
  
7. Alt+F4를 눌러 웹 브라우저를 닫습니다.  
  
 이 샘플에서는 HTTP를 통해 호스트되는 서비스의 요청을 라우트하기 위해 <xref:System.Web.Routing> 네임스페이스의 클래스를 사용하여 호스팅 계층을 작성할 수 있음을 보여 줍니다.  
  
> [!NOTE]
> 버전 2로 설정 된 경우 기본 응용 프로그램 [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] 풀 버전을로 업데이트 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [AppFabric 호스팅 및 지 속성 샘플](https://go.microsoft.com/fwlink/?LinkId=193961)
