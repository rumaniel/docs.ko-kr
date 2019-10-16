---
title: WPF XAML 브라우저 애플리케이션 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XBAP [WPF], XAML browser application
- WPF XAML browser applications (XBAP)
- XAML browser applications (XBAP)
- browser-hosted applications [WPF]
ms.assetid: 3a7a86a8-75d5-4898-96b9-73da151e5e16
ms.openlocfilehash: 230a25ad16c91f7812e5d92203ba204ca0abc099
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70037756"
---
# <a name="wpf-xaml-browser-applications-overview"></a>WPF XAML 브라우저 애플리케이션 개요
<a name="introduction"></a>
[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]는 웹 응용 프로그램과 리치 클라이언트 응용 프로그램의 기능을 결합 합니다. XBAP는 웹 애플리케이션처럼 웹 서버에 배포할 수 있으며 Internet Explorer 또는 Firefox에서 시작할 수 있습니다. 풍부한 클라이언트 응용 프로그램과 마찬가지로 Xbap는 WPF의 기능을 활용할 수 있습니다. XBAP를 개발하는 것은 리치 클라이언트 개발과도 비슷합니다. 이 항목에서는 XBAP 개발에 대한 간단하고 고급 수준의 소개를 제공하며 XBAP 개발이 표준 리치 클라이언트 개발과 다른 점을 설명합니다.  
  
 이 항목에는 다음과 같은 단원이 포함되어 있습니다.  
  
- [새 XBAP(XAML 브라우저 응용 프로그램) 만들기](#creating_a_new_xaml_browser_application_xbap)  
  
- [XBAP 배포](#deploying_a_xbap)  
  
- [호스트 웹 페이지와 통신](#communicating_with_the_host_web_page)  
  
- [XBAP 보안 고려 사항](#xbap_security_considerations)  
  
- [XBAP 시작 시간 성능 고려 사항](#xbap_start_time_performance_considerations)  
  
<a name="creating_a_new_xaml_browser_application_xbap"></a>   
## <a name="creating-a-new-xaml-browser-application-xbap"></a>새 XBAP(XAML 브라우저 애플리케이션) 만들기  
 새 XBAP 프로젝트를 만드는 가장 간단한 방법은 Microsoft Visual Studio를 사용 하는 것입니다. 새 프로젝트를 만들려면 템플릿 목록에서 **WPF 브라우저 애플리케이션**을 선택합니다. 자세한 내용은 [방법: 새 WPF 브라우저 응용 프로그램 프로젝트](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb628663(v=vs.100))를 만듭니다.  
  
 XBAP 프로젝트를 실행하면 독립 실행형 창이 아닌 브라우저 창에서 열립니다. Visual Studio에서 XBAP를 디버깅할 때 응용 프로그램은 인터넷 영역 권한으로 실행 되므로 이러한 사용 권한을 초과 하는 경우 보안 예외가 throw 됩니다. 자세한 내용은 [보안](../security-wpf.md) 및 [WPF 부분 신뢰 보안](../wpf-partial-trust-security.md)을 참조하세요.  
  
> [!NOTE]
> Visual Studio를 사용 하 여 개발 하지 않거나 프로젝트 파일에 대 한 자세한 내용을 보려면 [WPF 응용 프로그램 빌드](building-a-wpf-application-wpf.md)를 참조 하세요.  
  
<a name="deploying_a_xbap"></a>   
## <a name="deploying-an-xbap"></a>XBAP 배포  
 XBAP를 빌드하는 경우 출력에는 다음 세 가지 파일이 포함됩니다.  
  
|파일|설명|  
|----------|-----------------|  
|실행 파일(.exe)|컴파일된 코드가 포함되며 확장명이 .exe입니다.|  
|애플리케이션 매니페스트(.manifest)|애플리케이션과 연결된 메타데이터가 포함되며 확장명이 .manifest입니다.|  
|배포 매니페스트(.xbap)|이 파일은 ClickOnce에서 응용 프로그램을 배포 하는 데 사용 하는 정보를 포함 하며 확장명이입니다.|  
  
 웹 서버 (예: Microsoft 인터넷 정보 서비스 (IIS) 5.0 이상 버전)에 Xbap를 배포 합니다. 웹 서버에 .NET Framework을 설치할 필요는 없지만, mime ( [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 다목적 Internet Mail Extensions) 형식 및 파일 이름 확장명을 등록 해야 합니다. 자세한 내용은 [IIS 5.0 및 IIS 6.0을 구성하여 WPF 애플리케이션 배포](how-to-configure-iis-5-0-and-iis-6-0-to-deploy-wpf-applications.md)를 참조하세요.  
  
 배포를 위해 XBAP를 준비하려면 .exe 및 연결된 매니페스트를 웹 서버에 복사합니다. 확장명이 .xbap인 파일인 배포 매니페스트를 여는 하이퍼링크가 포함된 HTML 페이지를 만듭니다. 사용자가 xbap 파일에 대 한 링크를 클릭 하면 ClickOnce에서 응용 프로그램을 다운로드 하 고 시작 하는 메커니즘을 자동으로 처리 합니다. 다음 예제 코드는 XBAP를 가리키는 하이퍼링크가 포함된 HTML 페이지를 보여 줍니다.  
  
```html
<html>   
    <head></head>  
    <body>   
        <a href="XbapEx.xbap">Click this link to launch the application</a>  
    </body>   
</html>  
```  
  
 웹 페이지 프레임에서 XBAP를 호스트할 수도 있습니다. 하나 이상의 프레임이 있는 웹 페이지를 만듭니다. 프레임의 원본 속성을 배포 매니페스트 파일로 설정합니다. 호스팅 웹 페이지와 XBAP 간의 통신에 기본 제공 메커니즘을 사용하려면 프레임에 애플리케이션을 호스트해야 합니다. 다음 예제 코드는 두 프레임이 있는 HTML 페이지를 보여 주며 두 번째 프레임의 원본은 XBAP로 설정됩니다.  
  
```html
<html>   
    <head>
        <title>A page with frames</title>
    </head>  
    <frameset cols="50%,50%">   
        <frame src="introduction.htm">   
        <frame src="XbapEx.xbap">   
    </frameset>   
</html>  
```  
  
### <a name="clearing-cached-xbaps"></a>캐시된 XBAP 지우기  
 XBAP를 다시 빌드하여 시작한 후 일부 경우에 이전 버전의 XBAP가 열린 것을 알 수 있습니다. 예를 들어 XBAP 어셈블리 버전 번호가 정적이고 명령줄에서 XBAP를 시작하는 경우 이러한 동작이 발생할 수 있습니다. 이 경우 캐시된 버전(이전에 시작된 버전)과 새 버전 사이 버전 번호가 같게 유지되므로 XBAP의 새 버전이 다운로드되지 않습니다. 대신, 캐시된 버전이 로드됩니다.  
  
 이러한 경우 명령 프롬프트에서 **Mage** 명령 (Visual Studio 또는 Windows SDK와 함께 설치 됨)을 사용 하 여 캐시 된 버전을 제거할 수 있습니다. 다음 명령은 애플리케이션 캐시를 지웁니다.  
  
 ```console
 Mage.exe -cc
 ```
  
 이 명령은 최신 버전의 XBAP가 시작되도록 보장해 줍니다. Visual Studio에서 응용 프로그램을 디버깅 하는 경우 최신 버전의 XBAP를 시작 해야 합니다. 일반적으로 배포 시마다 배포 버전 번호를 업데이트합니다. Mage에 자세한 내용은 [Mage.exe(매니페스트 생성 및 편집 도구)](../../tools/mage-exe-manifest-generation-and-editing-tool.md)를 참조하세요.  
  
<a name="communicating_with_the_host_web_page"></a>   
## <a name="communicating-with-the-host-web-page"></a>호스트 웹 페이지와 통신  
 애플리케이션이 HTML 프레임에서 호스팅되는 경우 XBAP가 포함된 웹 페이지와 통신할 수 있습니다. 이렇게 하려면의 <xref:System.Windows.Interop.BrowserInteropHelper.HostScript%2A> <xref:System.Windows.Interop.BrowserInteropHelper>속성을 검색 합니다. 이 속성은 HTML 창을 나타내는 스크립트 개체를 반환합니다. 그런 다음 정규 점(dot) 구문을 사용하여 [창 개체](https://go.microsoft.com/fwlink/?LinkId=160274)에서 속성, 메서드 및 이벤트에 액세스할 수 있습니다. 또한 스크립트 메서드 및 전역 변수에도 액세스할 수 있습니다. 다음 예제에서는 스크립트 개체를 검색하고 브라우저를 닫는 방법을 보여 줍니다.  
  
 [!code-csharp[XbapBrowserInterop#10](~/samples/snippets/csharp/VS_Snippets_Wpf/xbapbrowserinterop/cs/page1.xaml.cs#10)]
 [!code-vb[XbapBrowserInterop#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/xbapbrowserinterop/vb/page1.xaml.vb#10)]  
  
### <a name="debugging-xbaps-that-use-hostscript"></a>HostScript를 사용하는 XBAP 디버깅  
 XBAP에서 <xref:System.Windows.Interop.BrowserInteropHelper.HostScript%2A> 개체를 사용 하 여 HTML 창과 통신 하는 경우 Visual Studio에서 응용 프로그램을 실행 하 고 디버깅 하기 위해 지정 해야 하는 두 가지 설정이 있습니다. 애플리케이션은 원본 사이트에 대한 액세스 권한이 있어야 하고 XBAP가 포함된 HTML 페이지로 애플리케이션을 시작해야 합니다. 다음 단계는 이러한 두 설정을 확인하는 방법을 설명합니다.  
  
1. Visual Studio에서 프로젝트 속성을 엽니다.  
  
2. **보안** 탭에서 **고급**을 클릭합니다.  
  
     고급 보안 설정 대화 상자가 나타납니다.  
  
3. **원본 사이트에 응용 프로그램 액세스 허용** 확인란을 선택했는지 확인한 후 **확인**을 클릭합니다.  
  
4. **디버그** 탭에서 **다음 URL로 브라우저 시작** 옵션을 선택하고 XBAP가 포함된 HTML 페이지의 URL을 지정합니다.  
  
5. Internet Explorer에서 **도구** 단추를 클릭하고 **인터넷 옵션**을 선택합니다.  
  
     인터넷 옵션 대화 상자가 나타납니다.  
  
6. **고급** 탭을 클릭합니다.  
  
7. **보안** 아래 **설정** 목록에서 **[내 컴퓨터]에 있는 파일에서 액티브 콘텐츠가 실행되는 것을 허용** 확인란을 선택합니다.  
  
8. **확인**을 클릭합니다.  
  
     변경 내용을 적용하려면 Internet Explorer를 다시 시작합니다.  
  
> [!CAUTION]
> Internet Explorer에서 액티브 콘텐츠가 실행되도록 하면 컴퓨터가 위험에 처할 수 있습니다. Internet Explorer 보안 설정을 변경 하지 않으려는 경우 서버에서 HTML 페이지를 시작 하 고이 프로세스에 Visual Studio 디버거를 연결할 수 있습니다.  
  
<a name="xbap_security_considerations"></a>   
## <a name="xbap-security-considerations"></a>XBAP 보안 고려 사항  
 일반적으로 XBAP는 인터넷 영역 권한 설정으로 제한된 부분 신뢰 보안 샌드박스에서 실행됩니다. 따라서 구현은 인터넷 영역에서 지원 되는 WPF 요소의 하위 집합을 지원 하거나 응용 프로그램의 권한을 높여야 합니다. 자세한 내용은 [보안](../security-wpf.md)을 참조하세요.  
  
 응용 프로그램에서 컨트롤 <xref:System.Windows.Controls.WebBrowser> 을 사용 하는 경우 WPF는 내부적으로 네이티브 WebBrowser ActiveX 컨트롤을 인스턴스화합니다. 애플리케이션이 Internet Explorer에서 실행되는 부분 신뢰 XBAP인 경우 ActiveX 컨트롤은 Internet Explorer 프로세스의 전용 스레드에서 실행됩니다. 따라서 다음 제한 사항이 적용됩니다.  
  
- 컨트롤 <xref:System.Windows.Controls.WebBrowser> 은 보안 제한 사항을 포함 하 여 호스트 브라우저와 유사한 동작을 제공 해야 합니다. 이러한 보안 제한 사항 중 일부는 Internet Explorer 보안 설정을 통해 제어할 수 있습니다. 자세한 내용은 [보안](../security-wpf.md)을 참조하세요.  
  
- XBAP가 HTML 페이지의 도메인 간에 로드되면 예외가 throw됩니다.  
  
- 입력은 WPF <xref:System.Windows.Controls.WebBrowser>와 별도의 스레드에 있으므로 키보드 입력을 가로챌 수 없으며 IME 상태가 공유 되지 않습니다.  
  
- 탐색 시간 또는 순서는 다른 스레드에서 실행 중인 ActiveX 컨트롤로 인해 달라질 수 있습니다. 예를 들어 페이지 탐색은 다른 탐색 요청을 시작할 때 항상 취소되는 것은 아닙니다.  
  
- WPF 애플리케이션은 별도의 스레드에서 실행되므로 사용자 지정 ActiveX 컨트롤이 통신하는 데 문제가 있을 수 있습니다.  
  
- <xref:System.Windows.Interop.HwndHost.MessageHook>는 다른 스레드나 프로세스에서 <xref:System.Windows.Interop.HwndHost> 실행 되는 창을 서브클래싱하 할 수 없기 때문에 발생 하지 않습니다.  
  
### <a name="creating-a-full-trust-xbap"></a>완전 신뢰 XBAP 만들기  
 XBAP에 완전 신뢰가 필요한 경우 이 권한을 사용하도록 프로젝트를 변경할 수 있습니다. 다음 단계는 완전 권한을 설정하는 방법을 설명합니다.  
  
1. Visual Studio에서 프로젝트 속성을 엽니다.  
  
2. **보안** 탭에서 **완전 신뢰 응용 프로그램** 옵션을 선택합니다.  
  
 이 설정으로 다음이 변경됩니다.  
  
- 프로젝트 파일에서 `<TargetZone>` 요소 값이 `Custom`으로 변경됩니다.  
  
- 응용 프로그램 매니페스트 (manifest.xml) `Unrestricted="true"` 에서 특성은 '<xref:System.Security.PermissionSet> 요소에 추가 됩니다.  
  
    ```xml
    <PermissionSet class="System.Security.PermissionSet"   
                   version="1"   
                   ID="Custom"   
                   SameSite="site"   
                   Unrestricted="true" />  
    ```  
  
### <a name="deploying-a-full-trust-xbap"></a>완전 신뢰 XBAP 배포  
 ClickOnce 신뢰 배포 모델을 따르지 않는 완전 신뢰 XBAP를 배포하면 사용자가 애플리케이션을 실행할 때의 동작이 보안 영역에 따라 달라집니다. 일부 경우에는 사용자가 설치를 시도할 때 경고를 받게 됩니다. 사용자는 설치를 계속하거나 취소하도록 선택할 수 있습니다. 다음 표에서 각 보안 영역의 동작 및 애플리케이션이 완전 신뢰를 받기 위해 수행해야 하는 작업을 설명합니다.  
  
|보안 영역|동작|완전 신뢰 얻기|  
|-------------------|--------------|------------------------|  
|로컬 컴퓨터|자동 완전 신뢰|아무 동작도 필요하지 않습니다.|  
|인트라넷 및 신뢰할 수 있는 사이트|완전 신뢰 확인|사용자가 프롬프트에서 소스를 볼 수 있도록 인증서로 XBAP에 로그인합니다.|  
|인터넷|"신뢰할 수 없음"과 함께 실패|인증서로 XBAP를 서명합니다.|  
  
> [!NOTE]
> 위의 표에 설명된 동작은 ClickOnce 신뢰 배포 모델을 따르지 않는 완전 신뢰 XBAP에 대한 것입니다.  
  
 완전 신뢰 XBAP를 배포하는 데 ClickOnce 신뢰 배포 모델을 사용하는 것이 좋습니다. 이 모델을 통해 보안 영역에 관계없이 XBAP에 완전 신뢰를 자동으로 부여할 수 있으므로 사용자에게 확인 메시지가 표시되지 않습니다. 이 모델의 일부로, 신뢰할 수 있는 게시자의 인증서로 애플리케이션을 서명해야 합니다. 자세한 내용은 [신뢰할 수 있는 애플리케이션 배포 개요](/visualstudio/deployment/trusted-application-deployment-overview) 및 [코드 서명 소개](https://go.microsoft.com/fwlink/?LinkId=166327)를 참조하세요.  
  
<a name="xbap_start_time_performance_considerations"></a>   
## <a name="xbap-start-time-performance-considerations"></a>XBAP 시작 시간 성능 고려 사항  
 XBAP 성능에서 중요한 측면은 시작 시간입니다. XBAP가 로드할 첫 번째 WPF 애플리케이션인 경우 *콜드 부팅* 시간은 10초 이상일 수 있습니다. 이는 진행률 페이지가 WPF에 의해 렌더링되고 애플리케이션을 표시하기 위해 CLR 및 WPF가 모두 콜드 부팅되어야 하기 때문입니다.  
  
 .NET Framework 3.5 s p 1 부터는 배포 주기의 초기에 관리 되지 않는 진행률 페이지를 표시 하 여 XBAP 콜드 시작 시간이 완화 됩니다. 진행률 페이지는 원시 호스팅 코드에 의해 표시되고 HTML로 렌더링되기 때문에 거의 애플리케이션이 시작된 직후에 표시됩니다.  
  
 또한 ClickOnce 다운로드 순서의 동시성이 향상 되어 시작 시간이 최대 10%까지 향상 되었습니다. ClickOnce에서 매니페스트를 다운로드 하 고 유효성을 검사 한 후에는 응용 프로그램 다운로드가 시작 되 고 진행률 표시줄이 업데이트 되기 시작 합니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Studio를 구성하여 웹 서비스를 호출하는 XAML 브라우저 응용 프로그램 디버깅](configure-vs-to-debug-a-xaml-browser-to-call-a-web-service.md)
- [WPF 응용 프로그램 배포](deploying-a-wpf-application-wpf.md)
