---
title: ASP.NET 캐싱 통합
ms.date: 03/30/2017
ms.assetid: f581923a-8a72-42fc-bd6a-46de2aaeecc1
ms.openlocfilehash: 56f686b83deb576f1245a9d4b9df2df433ea1e2f
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045787"
---
# <a name="aspnet-caching-integration"></a>ASP.NET 캐싱 통합

이 샘플에서는 WCF 웹 HTTP 프로그래밍 모델을 사용하여 ASP.NET 출력 캐시를 활용하는 방법을 보여 줍니다. 이 항목에서는 ASP.NET 출력 캐시 통합 기능을 중점적으로 설명합니다.

## <a name="demonstrates"></a>세부 항목

ASP.NET 출력 캐시와 통합

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\AspNetCachingIntegration`

## <a name="discussion"></a>토론

이 샘플에서는 Windows Communication Foundation <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> (WCF) 서비스에서를 사용 하 여 ASP.NET 출력 캐싱을 활용 합니다. <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>는 서비스 작업에 적용되며, 구성 파일에서 지정된 작업의 응답에 적용해야 하는 캐시 프로필의 이름을 제공합니다.

샘플 서비스 프로젝트의 Service.cs 파일에서 `GetCustomer` 및 `GetCustomers` <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>작업은 모두 캐시 프로필 이름 "CacheFor60Seconds"을 제공 하는로 표시 됩니다. Service 프로젝트의 web.config 파일에서 캐시 프로필 "CacheFor60Seconds"은 <`caching``system.web`>의 < > 요소 아래에 제공 됩니다. 이 캐시 프로필의 경우 `duration` 특성의 값은 "60" 이므로이 프로필과 연결 된 응답은 60 초 동안 ASP.NET 출력 캐시에 캐시 됩니다. 또한이 캐시 프로필 `varmByParam` 의 경우 특성은 "format"으로 설정 되므로 `format` 쿼리 문자열 매개 변수에 대 한 값이 서로 다른 요청에서는 응답이 별도로 캐시 됩니다. 마지막으로, 캐시 프로필의 `varyByHeader` 특성이 "accept"로 설정 되어 있으므로 accept 헤더 값이 서로 다른 요청에서 응답이 별도로 캐시 됩니다.

Client 프로젝트의 Program.cs에서는 <xref:System.Net.HttpWebRequest>를 사용하여 이러한 클라이언트를 작성하는 방법을 보여 줍니다. 이 방법은 WCF 서비스에 액세스하는 여러 방법 중 하나일 뿐입니다. 또한 WCF 채널 팩터리 및와 <xref:System.Net.WebClient>같은 다른 .NET Framework 클래스를 사용 하 여 서비스에 액세스할 수 있습니다. SDK의 다른 샘플 (예: [기본 HTTP 서비스](../../../../docs/framework/wcf/samples/basic-http-service.md) 예제)에서는 이러한 클래스를 사용 하 여 WCF 서비스와 통신 하는 방법을 보여 줍니다.

## <a name="to-run-the-sample"></a>이 샘플을 실행하려면

이 샘플은 다음의 세 프로젝트로 구성되어 있습니다.

- **서비스**: ASP.NET에서 호스트 되는 WCF HTTP 서비스가 포함 된 웹 응용 프로그램 프로젝트입니다.

- **클라이언트**: 서비스를 호출하는 콘솔 응용 프로그램 프로젝트입니다.

- **일반**: 클라이언트 및 서비스에서 사용 하는 고객 유형이 포함 된 공유 라이브러리입니다.

Client 콘솔 애플리케이션이 실행되면 클라이언트에서는 서비스로 요청을 보내고 응답의 관련 정보를 콘솔 창에 씁니다.

#### <a name="to-run-the-sample"></a>이 샘플을 실행하려면

1. ASP.NET Caching Integration 샘플의 솔루션을 엽니다.

2. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.

3. **솔루션 탐색기** 창이 아직 열려 있지 않은 경우 Ctrl + W + S를 누릅니다.

4. **솔루션 탐색기** 창에서 **서비스** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **새 인스턴스 시작**을 선택 합니다. 그러면 ASP.NET Development Server가 시작되어 서비스를 호스트합니다.

5. **솔루션 탐색기** 창에서 **클라이언트** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **새 인스턴스 시작**을 선택 합니다.

6. 클라이언트 콘솔 창이 나타나고 실행 중인 서비스의 URI와 실행 중인 서비스에 대한 HTML 도움말 페이지의 URI가 제공됩니다. 언제든지 브라우저에서 HTML 도움말 페이지의 URI를 입력하면 해당 도움말 페이지를 볼 수 있습니다.

7. 샘플이 실행되면 클라이언트에서는 현재 활동의 상태를 씁니다.

8. 아무 키나 눌러 클라이언트 콘솔 애플리케이션을 종료합니다.

9. Shift+F5를 눌러 서비스 디버깅을 중지합니다.

10. Windows 알림 영역에서 ASP.NET development 서버 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **중지**를 선택 합니다.
