---
title: .NET Framework 4 마이그레이션 문제
ms.date: 05/02/2017
helpviewer_keywords:
- .NET Framework 4, migration
- application compatibility
ms.assetid: df478548-8c05-4de2-8ba7-adcdbe1c2a60
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cae4ce2e1d5cdef097f4095a7748f09b80d1acdb
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699074"
---
# <a name="net-framework-4-migration-issues"></a>.NET Framework 4 마이그레이션 문제

이 항목에서는 수정, 표준 준수 및 보안에 대한 변경 내용, 고객 피드백 기반의 변경 내용을 포함하여 .NET Framework 버전 3.5 서비스 팩 1과 .NET Framework 버전 4 간의 마이그레이션 문제에 대해 설명합니다. 이러한 변경 내용은 대부분 애플리케이션에서 프로그래밍을 수정할 필요가 없습니다. 수정이 필요한 경우 표의 권장 변경 내용 열을 참조하세요.

이 항목에서는 다음 영역의 중요한 변경 내용에 대해 설명합니다.

- [ASP.NET 및 웹](#aspnet-and-web)

- [코어](#core)

- [Data](#data)

- [WCF(Windows Communication Foundation)](#windows-communication-foundation-wcf)

- [WPF(Windows Presentation Foundation)](#windows-presentation-foundation-wpf)

- [XML](#xml)

이 항목의 문제에 대한 좀 더 간략한 개요는 [.NET Framework 4 마이그레이션 가이드](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ff657133%28v=vs.100%29)를 참조하세요.

새로운 기능에 대한 자세한 내용은 [.NET Framework 4의 새로운 기능](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms171868%28v=vs.100%29)을 참조하세요.

## <a name="aspnet-and-web"></a>ASP.NET 및 웹

네임스페이스: <xref:System.Web>, <xref:System.Web.Mobile>, <xref:System.Web.Security>, <xref:System.Web.UI.WebControls>; 어셈블리: System.Web(System.Web.dll의)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **브라우저 정의 파일** | 브라우저 정의 파일은 새롭고 업데이트된 브라우저 및 디바이스에 대한 정보를 포함하도록 업데이트되었습니다. Netscape Navigator와 같은 오래된 브라우저와 디바이스는 제거되었으며 Google Chrome 및 Apple iPhone과 같은 최신 브라우저와 디바이스가 추가되었습니다.<br><br>애플리케이션에 제거된 브라우저 정의 중 하나를 상속하는 사용자 지정 브라우저 정의가 포함되어 있으면 오류가 표시됩니다.<br><br><xref:System.Web.HttpBrowserCapabilities> 개체(페이지의 `Request.Browse` 속성에 의해 노출됨)는 브라우저 정의 파일에 의해 구동됩니다. 따라서 ASP.NET 4에서 이 개체의 속성에 액세스하여 반환되는 정보는 이전 버전의 ASP.NET에서 반환된 정보와 다를 수 있습니다. | 애플리케이션에서 이전 브라우저 정의 파일을 사용하는 경우 다음 폴더에서 해당 파일을 복사할 수 있습니다.<br><br>*Windows\\Microsoft.NET\\Framework\\v2.0.50727\\CONFIG\\Browsers*<br><br>ASP.NET 4의 해당 *\\CONFIG\\Browsers* 폴더에 파일을 복사합니다. 파일을 복사한 후 [Aspnet_regbrowsers.exe](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms229858(v=vs.90)) 명령줄 도구를 실행합니다. 자세한 내용은 [https://www.asp.net/mobile](/aspnet/mobile/overview) 웹 사이트를 참조하세요. |
| **혼합된 버전의 ASP.NET에서 실행 중인 자식 애플리케이션** | 이전 버전의 ASP.NET을 실행하는 애플리케이션의 자식으로서 구성된 ASP.NET 4 애플리케이션은 구성 또는 컴파일 오류로 인해 시작하지 못할 수 있습니다. 발생하는 특정 오류는 애플리케이션이 IIS 6.0에서 실행되는지 아니면 IIS 7 또는 IIS 7.5에서 실행되는지에 따라 다릅니다. | 구성 시스템이 ASP.NET 4 애플리케이션을 올바르게 인식할 수 있도록 영향을 받는 애플리케이션의 구성 파일을 변경할 수 있습니다. 반드시 수행해야 할 변경 내용에 대한 자세한 내용은 ASP.NET 웹 사이트에 있는 [ASP.NET 4 Breaking Changes](/aspnet/whitepapers/aspnet4/breaking-changes)(ASP.NET 4 주요 변경 내용) 문서의 “ASP.NET 4 Child Applications Fail to Start When Under ASP.NET 2.0 or ASP.NET 3.5 Applications”(ASP.NET 4 자식 애플리케이션이 ASP.NET 2.0 또는 ASP.NET 3.5 애플리케이션에서 시작되지 않음) 섹션을 참조하세요. |
| **ClientID 변경 내용** | ASP.NET 4의 새로운 `clientIDMode` 설정을 통해 ASP.NET이 HTML 요소에 대해 `id` 특성을 생성하는 방법을 지정할 수 있습니다. ASP.NET의 이전 버전에서는 기본 동작이 `clientIDMode`의 `AutoID` 설정과 동일합니다. 이제 기본 설정은 `Predictable`입니다. 자세한 내용은 [ASP.NET 웹 서버 컨트롤 식별](https://docs.microsoft.com/previous-versions/aspnet/1d04y8ss%28v=vs.100%29)을 참조하세요. | Visual Studio를 사용하여 ASP.NET 2.0 또는 ASP.NET 3.5에서 애플리케이션을 업그레이드하는 경우, .NET Framework 이전 버전의 동작을 유지하는 Web.config 파일에 설정이 자동으로 추가됩니다. 그러나 .NET Framework 4를 대상으로 하도록 IIS에서 애플리케이션 풀을 변경하여 애플리케이션을 업그레이드하는 경우 ASP.NET은 기본적으로 새 모드를 사용합니다. 새 클라이언트 ID 모드를 사용하지 않으려면 Web.config 파일에 다음 설정을 추가하세요.<br><br>`<pages clientIDMode="AutoID" />` |
| **CAS(코드 액세스 보안)** | ASP.NET 3.5에 추가된 ASP.NET 2.0 NET 기능은 .NET Framework 1.1 및 .NET Framework 2.0 CAS(코드 액세스 보안) 모델을 사용합니다. 그러나 ASP.NET 4의 CAS 구현은 크게 개선되었습니다. 따라서 전역 어셈블리 캐시에서 실행되는 신뢰할 수 있는 코드를 사용하는 부분 신뢰 ASP.NET 애플리케이션은 다양한 보안 예외와 함께 실패할 수 있습니다. 컴퓨터 CAS 정책에 대한 광범위한 수정에 의존하는 부분 신뢰 애플리케이션도 실패하고 보안 예외를 throw할 수 있습니다. | 다음 예제와 같이 `trust` 구성 요소에서 새 `legacyCasModel` 특성을 사용하여 부분 신뢰 ASP.NET 4 애플리케이션을 ASP.NET 1.1 및 2.0의 동작으로 되돌릴 수 있습니다.<br><br>`<trust level= "Medium" legacyCasModel="true" />`<br><br>중요: 이전 CAS 모델로 되돌리면 보안이 약화될 수 있습니다.<br><br>새로운 ASP.NET 4 코드 액세스 보안 모델에 대한 자세한 내용은 [ASP.NET 4 애플리케이션의 코드 액세스 보안](https://docs.microsoft.com/previous-versions/dd984947(v=vs.100))을 참조하세요. |
| **구성 파일** | .NET Framework 및 ASP.NET 4의 루트 구성 파일(machine.config 파일 및 루트 Web.config 파일)은 ASP.NET 3.5의 애플리케이션 Web.config 파일에 있는 대부분의 상용구 구성 정보를 포함하도록 업데이트되었습니다. 관리되는 IIS 7 및 IIS 7.5 구성 시스템의 복잡성 때문에 ASP.NET 4, IIS 7 및 IIS 7.5에서 ASP.NET 3.5 애플리케이션을 실행하면 ASP.NET 오류 또는 IIS 오류가 발생할 수 있습니다. | Visual Studio의 프로젝트 업그레이드 도구를 사용하여 ASP.NET 3.5 애플리케이션을 ASP.NET 4로 업그레이드하세요. Visual Studio 2010은 ASP.NET 3.5 애플리케이션의 Web.config 파일을 자동으로 수정하여 ASP.NET 4에 대한 적절한 설정을 포함합니다.<br><br>그러나 다시 컴파일하지 않고 .NET Framework 4를 사용하여 ASP.NET 3.5 애플리케이션을 실행할 수 있습니다. 이 경우 .NET Framework 4 및 IIS 7 또는 IIS 7.5에서 애플리케이션을 실행하기 전에 애플리케이션의 Web.config 파일을 수동으로 수정해야 할 수 있습니다. 반드시 변경해야 하는 구체적인 내용은 SP(서비스 팩) 릴리스를 비롯하여 작업 중인 소프트웨어의 조합에 따라 다릅니다. 이 변경으로 인해 영향을 받을 수 있는 소프트웨어 조합 및 특정 조합의 문제를 해결하는 방법에 대한 자세한 내용은 ASP.NET 웹 사이트에 있는 [ASP.NET 4 Breaking Changes](/aspnet/whitepapers/aspnet4/breaking-changes)(ASP.NET 4 주요 변경 내용) 문서의 “Configuration Errors Related to New ASP.NET 4 Root Configuration”(새 ASP.NET 4 루트 구성과 관련된 구성 오류) 섹션을 참조하세요. |
| **컨트롤 렌더링** | 이전 버전의 ASP.NET에서는 일부 컨트롤에서 비활성화할 수 없는 태그를 내보냈습니다. 기본적으로 이 형식의 태그는 ASP.NET 4에서 더 이상 생성되지 않습니다. 이러한 렌더링 변경은 다음 컨트롤에 영향을 줍니다.<br><br>* `Image` 및 `ImageButton` 컨트롤은 더 이상 `border="0"` 특성을 렌더링하지 않습니다.<br>* `BaseValidator` 클래스와 그로부터 파생된 유효성 검사 컨트롤은 더 이상 기본적으로 빨간색 텍스트를 렌더링하지 않습니다.<br>* `HtmlForm` 컨트롤은 `name` 특성을 렌더링하지 않습니다.<br>* `Table` 컨트롤이 더 이상 `border="0"` 특성을 렌더링하지 않습니다.<br><br>사용자 입력용으로 디자인되지 않은 컨트롤(예: `Label` 컨트롤)은 `Enabled` 속성이 `false`로 설정된 경우(또는 컨테이너 컨트롤에서 이 설정을 상속하는 경우) 더 이상 `disabled="disabled"` 특성을 렌더링하지 않습니다. | Visual Studio를 사용하여 ASP.NET 2.0 또는 ASP.NET 3.5에서 애플리케이션을 업그레이드하는 경우, 레거시 렌더링을 유지하는 Web.config 파일에 설정이 자동으로 추가됩니다. 그러나 .NET Framework 4를 대상으로 하도록 IIS에서 애플리케이션 풀을 변경하여 애플리케이션을 업그레이드하는 경우 ASP.NET은 기본적으로 새 렌더링 모드를 사용합니다. 새 렌더링 모드를 사용하지 않으려면 Web.config 파일에 다음 설정을 추가하세요.<br><br>`<pages controlRenderingCompatibilityVersion="3.5" />` |
| **기본 문서의 이벤트 처리기** | ASP.NET 4는 기본 문서가 매핑된 확장명 없는 URL에 대한 요청이 있을 때 HTML `form` 요소의 `action` 특성 값을 빈 문자열로 렌더링합니다. 이전 버전의 ASP.NET에서는 `http://contoso.com`에 대한 요청이 결국 Default.aspx에 대한 요청이 되었습니다. 이 문서에서 여는 `form` 태그는 다음 예제와 같이 렌더링됩니다.<br><br>`<form action="Default.aspx" />`<br><br>ASP.NET 4에서는 `http://contoso.com`에 대한 요청이 결국 Default.aspx에 대한 요청이 되지만, ASP.NET에서는 이제 다음 예제와 같이 HTML 열기 `form` 태그를 렌더링합니다.<br><br>`<form action="" />`<br><br>`action` 특성이 빈 문자열이면 IIS `DefaultDocumentModule` 개체가 Default.aspx에 대한 자식 요청을 만듭니다. 대부분의 상황에서 이 자식 요청은 애플리케이션 코드에 대해 투명하며, Default.aspx 페이지는 정상적으로 실행됩니다. 그러나 관리 코드와 IIS 7 또는 IIS 7.5 통합 모드 간의 잠재적 상호 작용으로 인해 관리되는 .aspx 페이지가 자식 요청 중에 제대로 작동하지 않을 수 있습니다. 다음 상황이 발생하면 기본 .aspx 문서에 대한 자식 요청으로 인해 오류가 발생하거나 예기치 않은 동작이 발생합니다.<br><br>* `form` 요소의 `action` 특성이 ""로 설정된 상태로 .aspx 페이지가 브라우저로 전송됩니다.<br>* 양식이 ASP.NET에 다시 게시됩니다.<br>* 관리되는 HTTP 모듈은 `Request.Form` 또는 `Request.Params` 등 엔터티 본문의 일부를 읽습니다. 이렇게 하면 POST 요청의 엔터티 본문이 관리되는 메모리로 읽힙니다. 결과적으로 IIS 7 또는 IIS 7.5 통합 모드에서 실행 중인 모든 네이티브 코드 모듈에서 더 이상 엔터티 본문을 사용할 수 없습니다.<br>* IIS `DefaultDocumentModule` 개체가 결국 실행되어 Default.aspx 문서에 대한 자식 요청을 만듭니다. 그러나 엔터티 본문은 이미 관리 코드에 의해 읽혔기 때문에 자식 요청에 보낼 수 있는 엔터티 본문이 없습니다.<br>* HTTP 파이프라인이 자식 요청에 대해 실행되면 .aspx 파일의 처리기가 처리기 실행 단계 중에 실행됩니다.<br><br>엔터티 본문이 없기 때문에 양식 변수 및 보기 상태가 없습니다. 따라서 .aspx 페이지 처리기가 발생해야 하는 이벤트(있는 경우)를 결정하는 데 사용할 수 있는 정보가 없습니다. 그 결과, 영향을 받는 .aspx 페이지의 포스트백 이벤트 처리기는 실행되지 않습니다. | 이 변경의 결과 발생할 수 있는 문제를 해결하는 방법에 대한 자세한 내용은 ASP.NET 웹 사이트에 있는 [ASP.NET 4 Breaking Changes](/aspnet/whitepapers/aspnet4/breaking-changes)(ASP.NET 4 주요 변경 내용) 문서의 “Event Handlers Might Not Be Not Raised in a Default Document in IIS 7 or IIS 7.5 Integrated Mode”(IIS 7 또는 IIS 7.5 통합 모드의 기본 문서에서 이벤트 처리기가 작동하지 않을 수 있음) 섹션을 참조하세요. |
| **해시 알고리즘** | ASP.NET은 암호화 및 해시 알고리즘을 모두 사용하여 양식 인증 쿠키 및 보기 상태와 같은 데이터를 보호합니다. 기본적으로 ASP.NET 4는 쿠키 및 보기 상태의 해시 작업에 <xref:System.Security.Cryptography.HMACSHA256> 알고리즘을 사용합니다. 이전 버전의 ASP.NET에서는 이전 <xref:System.Security.Cryptography.HMACSHA1> 알고리즘을 사용했습니다. | 양식 인증 쿠키와 같은 데이터가 .NET Framework 버전 전체에서 작동해야 하는, ASP.NET 2.0 및 ASP.NET 4가 혼합된 애플리케이션을 실행하는 경우, Web.config 파일에서 다음 설정을 추가하여 ASP.NET 4 웹 애플리케이션이 이전 <xref:System.Security.Cryptography.HMACSHA1> 알고리즘을 사용하도록 구성하세요.<br><br>`<machineKey validation="SHA1" />` |
| **Internet Explorer의 컨트롤 호스팅** | 웹에 컨트롤을 호스트하는 더 나은 솔루션이 있기 때문에 더 이상 Internet Explorer에서 Windows Forms 컨트롤을 호스트할 수 없습니다. 따라서 IEHost.dll 및 IEExec.exe 어셈블리는 .NET Framework에서 제거되었습니다. | 웹 애플리케이션에서 사용자 지정 컨트롤 개발을 위해 다음 기술을 사용할 수 있습니다.<br><br>* Silverlight 애플리케이션을 만들고 브라우저 외부에서 실행되도록 구성할 수 있습니다. 자세한 내용은 [브라우저 외부에서 실행 지원](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/dd550721%28v=vs.95%29)을 참조하세요.<br>* XBAP(XAML 브라우저 애플리케이션)를 빌드하여 WPF 기능을 활용할 수 있습니다(클라이언트 컴퓨터에 .NET Framework 필요). 자세한 내용은 [WPF XAML 브라우저 애플리케이션 개요](../wpf/app-development/wpf-xaml-browser-applications-overview.md)를 참조하세요. |
| **HtmlEncode 및 UrlEncode 메서드** | <xref:System.Web.HttpUtility> 및 <xref:System.Web.HttpServerUtility> 클래스의 `HtmlEncode` 및 `UrlEncode` 메서드가 다음과 같이 작은따옴표 문자(')를 인코딩하도록 업데이트되었습니다.<br><br>* `HtmlEncode` 메서드는 작은따옴표의 인스턴스를 `&#39;`으로 인코딩합니다.<br>* `UrlEncode` 메서드는 작은따옴표의 인스턴스를 `%27`로 인코딩합니다. | `HtmlEncode` 및 `UrlEncode` 메서드를 사용하는 장소에 대한 코드를 검사하고 인코딩의 변경으로 인해 애플리케이션에 영향을 주는 변경이 발생하지 않는지 확인하세요. |
| **ASP.NET 2.0 애플리케이션의 HttpException 오류** | IIS 6에서 ASP.NET 4를 사용하도록 설정한 경우 IIS 6(Windows Server 2003 또는 Windows Server 2003 R2)에서 실행되는 ASP.NET 2.0 애플리케이션에서 다음과 같은 오류가 발생할 수 있습니다. `System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.` | * 웹 사이트를 실행하기 위해 ASP.NET 4가 필요하지 않은 경우 대신 ASP.NET 2.0을 사용하도록 사이트를 다시 매핑합니다.<br><br>또는<br><br>* 웹 사이트를 실행하기 위해 ASP.NET 4가 필요한 경우 자식 ASP.NET 2.0 가상 디렉터리를 ASP.NET 2.0에 매핑된 다른 웹 사이트로 이동합니다.<br><br>또는<br><br>* 확장명 없는 URL을 사용하지 않도록 설정하세요. 자세한 내용은 ASP.NET 웹 사이트에 있는 [ASP.NET 4 Breaking Changes](/aspnet/whitepapers/aspnet4/breaking-changes)(ASP.NET 4 주요 변경 내용) 문서의 “ASP.NET 2.0 Applications Might Generate HttpException Errors That Reference eurl.axd”(ASP.NET 2.0 애플리케이션이 eurl.axd를 참조하는 HttpException 오류를 생성할 수 있음)를 참조하세요. |
| **멤버 자격 유형** | ASP.NET 멤버 자격에서 사용되는 일부 형식(예: <xref:System.Web.Security.MembershipProvider>)이 System.Web.dll에서 System.Web.ApplicationServices.dll 어셈블리로 이동했습니다. 클라이언트 형식 및 확장된 .NET Framework SKU 형식 간 아키텍처 계층화 종속성을 해결하기 위해 형식을 이동했습니다. | ASP.NET의 이전 버전에서 업그레이드되었고 이동된 멤버 자격 유형을 사용하는 클래스 라이브러리는 ASP.NET 4 프로젝트에서 사용될 때 컴파일되지 않을 수 있습니다. 이 경우 클래스 라이브러리 프로젝트의 참조를 System.Web.ApplicationServices.dll에 추가하세요. |
| **메뉴 컨트롤 변경** | <xref:System.Web.UI.WebControls.Menu> 컨트롤을 변경하면 다음과 같은 동작이 발생합니다.<br><br>* <xref:System.Web.UI.WebControls.MenuRenderingMode>가 `List`로 설정되거나 <xref:System.Web.UI.WebControls.MenuRenderingMode>가 `Default`로 설정되고 <xref:System.Web.Configuration.PagesSection.ControlRenderingCompatibilityVersion>이 `4.0` 이상으로 설정된 경우 <xref:System.Web.UI.WebControls.MenuItem.PopOutImageUrl> 속성은 아무런 효과도 없습니다.<br>* <xref:System.Web.UI.WebControls.Menu.StaticPopOutImageUrl%2A> 및 <xref:System.Web.UI.WebControls.Menu.DynamicPopOutImageUrl> 속성에 설정된 경로에 백슬래시(\\)가 포함되어 있으면 이미지가 렌더링되지 않습니다. (ASP.NET의 이전 버전에서는 경로에 백슬래시를 포함할 수 있었습니다.) | * 개별 메뉴 항목의 <xref:System.Web.UI.WebControls.MenuItem.PopOutImageUrl> 속성을 설정하는 대신 부모 <xref:System.Web.UI.WebControls.Menu> 컨트롤의 <xref:System.Web.UI.WebControls.Menu.StaticPopOutImageUrl%2A> 또는 <xref:System.Web.UI.WebControls.Menu.DynamicPopOutImageUrl>을 설정하세요.<br><br>또는<br><br><xref:System.Web.UI.WebControls.MenuRenderingMode>를 `Table`, <xref:System.Web.UI.WebControls.MenuRenderingMode>를 `Default`, <xref:System.Web.Configuration.PagesSection.ControlRenderingCompatibilityVersion>을 `3.5`로 설정하세요. 이렇게 설정하면 <xref:System.Web.UI.WebControls.Menu> 컨트롤이 이전 버전의 ASP.NET에서 사용한 HTML 테이블 기반 레이아웃을 사용하게 합니다.<br>* <xref:System.Web.UI.WebControls.Menu.StaticPopOutImageUrl%2A> 또는 <xref:System.Web.UI.WebControls.Menu.DynamicPopOutImageUrl> 속성의 경로에 백슬래시(\\)가 포함되어 있으면 슬래시 문자(/)를 대체하세요. |
| **Web.config 파일의 모바일 어셈블리** | ASP.NET의 이전 버전에서는 System.Web.Mobile.dll 어셈블리에 대한 참조가 `system.web`/`compilation`의 `assemblies` 섹션에 있는 루트 Web.config 파일에 포함되었습니다. 성능 향상을 위해 이 어셈블리에 대한 참조가 제거되었습니다.<br><br>참고: System.Web.Mobile.dll 어셈블리 및 ASP.NET 모바일 컨트롤은 ASP.NET 4에 포함되지만 사용되지는 않습니다. | 이 어셈블리의 형식을 사용하려면 루트 Web.config 파일 또는 애플리케이션 Web.config 파일의 어셈블리에 대한 참조를 추가하세요. |
| **출력 캐싱** | ASP.NET 1.0에서는 `Location="ServerAndClient"`를 출력 캐시 설정으로 지정한 캐시된 페이지가 응답에서 `Vary:*` HTTP 헤더를 내보내는 버그가 있었습니다. 이로 인해 클라이언트 브라우저가 페이지를 로컬에 캐시하지 못했습니다. ASP.NET 1.1에서는 `Vary:*` 헤더를 억제하기 위해 호출할 수 있는 <xref:System.Web.HttpCachePolicy.SetOmitVaryStar%2A> 메서드가 추가되었습니다. 그러나 버그 보고서에 따르면 개발자는 기존의 `SetOmitVaryStar` 동작을 인식하지 못합니다.<br><br>ASP.NET 4에서는 다음 지시문을 지정하는 응답에서 더 이상 `Vary:*` HTTP 헤더를 내보내지 않습니다.<br><br>`<%@ OutputCache Location="ServerAndClient" %>`<br><br>결과적으로 `Vary:*` 헤더를 억제하기 위해 <xref:System.Web.HttpCachePolicy.SetOmitVaryStar%2A> 메서드가 더 이상 필요하지 않습니다. `Location` 특성에 대해 “ServerAndClient”를 지정하는 애플리케이션에서는 <xref:System.Web.HttpCachePolicy.SetOmitVaryStar%2A>를 호출할 필요 없이 브라우저에서 페이지를 캐시할 수 있습니다. | 애플리케이션의 페이지가 `Vary:*`을 내보내야 하는 경우 다음 예제와 같이 <xref:System.Web.HttpResponse.AppendHeader%2A> 메서드를 호출합니다.<br><br>`System.Web.HttpResponse.AppendHeader("Vary","*");`<br><br>또는 출력 캐싱 `Location` 특성의 값을 “Server”로 변경할 수 있습니다. |
| **페이지 구문 분석** | ASP.NET 웹 페이지(.aspx 파일) 및 사용자 컨트롤(.ascx 파일)의 페이지 파서는 이전 버전의 ASP.NET보다 ASP.NET 4에서 더 엄격하며, 이전 버전보다 더 많은 태그를 잘못된 것으로 표시합니다. | 페이지가 실행될 때 생성되는 오류 메시지를 검사하고 잘못된 태그에서 발생하는 오류를 수정하세요. |
| **Passport 형식** | ASP.NET 2.0에 내장된 Passport 지원은 사용되지 않으며 Passport(이제 Live ID SDK)의 변경으로 인해 지원되지 않습니다. 그 결과 <xref:System.Web.Security>의 Passport와 관련된 형식이 이제 `ObsoleteAttribute` 특성으로 표시됩니다. | <xref:System.Web.Security> 네임스페이스(예: <xref:System.Web.Security.PassportIdentity>)에서 Passport 형식을 사용하는 코드를 [SDK](https://go.microsoft.com/fwlink/?LinkId=106346)를 사용하도록 변경하세요. |
| **FilePath 속성의 PathInfo 정보** | ASP.NET 4는 <xref:System.Web.HttpRequest.FilePath>, <xref:System.Web.HttpRequest.AppRelativeCurrentExecutionFilePath>, <xref:System.Web.HttpRequest.CurrentExecutionFilePath>와 같은 속성의 반환 값에 더 이상 `PathInfo` 값을 포함하지 않습니다. 대신, `PathInfo` 정보를 <xref:System.Web.HttpRequest.PathInfo>에서 사용할 수 있습니다. 예를 들어 다음과 같은 URL 조각을 가정해 보겠습니다.<br><br>`/testapp/Action.mvc/SomeAction`<br><br>이전 버전의 ASP.NET에서 <xref:System.Web.HttpRequest> 속성은 다음과 같은 값을 갖습니다.<br><br>* <xref:System.Web.HttpRequest.FilePath>: `/testapp/Action.mvc/SomeAction`<br>* <xref:System.Web.HttpRequest.PathInfo>: (empty)<br><br>ASP.NET 4에서 <xref:System.Web.HttpRequest> 속성은 대신 다음과 같은 값을 갖습니다.<br><br>* <xref:System.Web.HttpRequest.FilePath>: `/testapp/Action.mvc`<br>* <xref:System.Web.HttpRequest.PathInfo>: `SomeAction` | 경로 정보를 반환하기 위해 <xref:System.Web.HttpRequest> 클래스의 속성에 의존하는 위치에 대한 코드를 검사하세요. 경로 정보가 반환되는 방식의 변화를 반영하도록 코드를 변경하세요. |
| **요청 유효성 검사** | 요청 유효성 검사를 향상하기 위해, 요청 수명 주기의 초기에 ASP.NET 요청 유효성 검사가 호출됩니다. 따라서 웹 서비스 호출 및 사용자 지정 처리기 등 .aspx 파일 이외의 요청에 대해서는 요청 유효성 검사가 실행됩니다. 또한 요청 처리 파이프라인에서 사용자 지정 HTTP 모듈이 실행 중일 때 요청 유효성 검사가 활성화됩니다.<br><br>이러한 변경 결과로 .aspx 파일 이외의 리소스에 대한 요청은 요청 유효성 검사 오류를 throw할 수 있습니다. 요청 파이프라인(예: 사용자 지정 HTTP 모듈)에서 실행되는 사용자 지정 코드는 요청 유효성 검사 오류를 throw할 수 있습니다. | 필요한 경우 웹 구성 파일에서 다음 설정을 사용하여 요청 유효성 검사를 트리거하는 .aspx 페이지만 이전 동작으로 되돌릴 수 있습니다.<br><br>`<httpRuntime requestValidationMode="2.0" />`<br><br>경고: 이전 동작으로 되돌리는 경우 기존 처리기, 모듈 및 기타 사용자 지정 코드의 모든 코드가 XSS 공격 벡터일 수 있는, 잠재적으로 안전하지 않은 HTTP 입력에 대한 검사를 수행해야 합니다. |
| **라우팅** | Visual Studio 2010에서 파일 시스템 웹 사이트를 만든 경우 이름에 점(.)이 포함된 폴더에 웹 사이트가 있으면 URL 라우팅이 안정적으로 작동하지 않습니다. 일부 가상 경로에서 HTTP 404 오류가 반환됩니다. 이 오류는 Visual Studio 2010이 루트 가상 디렉터리의 잘못된 경로를 사용하여 Visual Studio 개발 서버를 시작하기 때문에 발생합니다. | * 파일 기반 웹 사이트의 **속성** 페이지에서 **가상 경로** 특성을 “/”로 변경하세요.<br><br>또는<br><br>* 웹 사이트 프로젝트를 대신 웹 애플리케이션 프로젝트를 만드세요. 웹 애플리케이션 프로젝트에는 이 문제가 없으며, 프로젝트 폴더의 이름에 점이 있는 경우에도 URL 라우팅이 작동합니다.<br><br>또는<br><br>* IIS에서 호스트되는 HTTP 기반 웹 사이트를 만드세요. IIS에서 호스트하는 웹 사이트는 가상 경로는 물론 프로젝트 파일 폴더에도 점을 포함할 수 있습니다. |
| **SharePoint 사이트** | `WSS_Minimal`이라는 사용자 지정 부분 신뢰 수준이 포함된 SharePoint 웹 사이트의 자식으로 배포된 ASP.NET 4 웹 사이트를 실행하려고 하면 다음 오류가 표시됩니다.<br><br>`Could not find permission set named 'ASP.Net'.` | 지금은 ASP.NET과 호환되는 SharePoint 버전이 없습니다. 따라서 ASP.NET 4 웹 사이트를 SharePoint 웹 사이트의 자식으로 실행해서는 안 됩니다. |
| **XHTML 1.1 표준** | 새로운 웹 사이트에 XHTML 1.1 규격을 사용하기 위해 .NET Framework 4의 ASP.NET 컨트롤은 XHTML 1.1 규격 HTML을 생성합니다. `<system.Web>` 요소 내부의 Web.config 파일에서 다음 옵션을 사용하여 이 렌더링을 사용하도록 설정할 수 있습니다.<br><br>`<pages controlRenderingCompatibilityVersion="4.0"/>`<br><br>이 옵션은 기본적으로 4.0으로 설정됩니다. Visual Studio 2008에서 업그레이드되는 웹 프로젝트는 호환성을 위해 3.5 설정을 사용합니다. | 없음 |

## <a name="core"></a>코어

### <a name="general-features"></a>일반 기능

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **CardSpace** | Windows CardSpace는 이제 .NET Framework에 포함되지 않으며 별도로 제공됩니다. | [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?LinkId=199868)에서 Windows CardSpace를 다운로드하세요. |
| **구성 파일** | .NET Framework가 애플리케이션 구성 파일에 액세스하는 방법이 수정되었습니다. | 애플리케이션 구성 파일의 이름이 *application-name.config*인 경우 이름을 *application-name.exe.config*로 바꾸세요. 예를 들어 *MyApp.config*를 *MyApp.exe.config*로 바꿉니다. |
| **C# 코드 컴파일러** | <xref:Microsoft.CSharp> 네임스페이스에 있던 `Compiler`, `CompilerError` 및 `ErrorLevel` 클래스는 더 이상 사용할 수 없으며 해당 어셈블리(cscompmgd.dll)는 .NET Framework에 더 이상 포함되지 않습니다. | <xref:System.CodeDom.Compiler.CodeDomProvider> 클래스 및 <xref:System.CodeDom.Compiler> 네임스페이스의 기타 클래스를 사용하세요. 자세한 내용은 [CodeDOM 사용](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/y2k85ax6%28v=vs.100%29)을 참조하세요. |
| **호스팅**(관리되지 않는 API) | 호스팅 기능의 향상을 위해 일부 호스팅 활성화 API가 사용되지 않습니다. In-Process Side-by-Side 실행 기능을 통해 애플리케이션은 동일한 프로세스에서 여러 버전의 .NET Framework를 로드하고 시작할 수 있습니다. 예를 들어 .NET Framework 2.0 SP1을 기반으로 하는 추가 기능(또는 구성 요소) 및 동일한 프로세스에서 .NET Framework 4를 기반으로 하는 추가 기능을 로드하는 애플리케이션을 실행할 수 있습니다. 이전 구성 요소는 이전 .NET Framework 버전을 계속 사용하고 새 구성 요소는 새 .NET Framework 버전을 사용합니다. | [In-Process Side-by-Side 실행](../deployment/in-process-side-by-side-execution.md)에 설명된 구성을 사용하세요. |
| **새 보안 모델** | [.NET Framework 4의 보안 변경 내용](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd233103%28v=vs.100%29)에 설명된 대로 CAS(코드 액세스 보안) 정책이 해제되어 단순화된 모델로 대체되었습니다. | 애플리케이션에서 CAS를 사용하는 경우 수정이 필요할 수 있습니다. 자세한 내용은 [코드 액세스 보안 정책 호환성 및 마이그레이션](../misc/code-access-security-policy-compatibility-and-migration.md)을 참조하세요. |

### <a name="date-and-time"></a>날짜 및 시간

네임스페이스: <xref:System>; 어셈블리: mscorlib(mscorlib.dll)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **일광 절약** | 시스템 시계와의 일관성을 위해, 시간 속성(예: <xref:System.TimeZoneInfo.Local> 및 <xref:System.DateTime.Now>)은 일광 절약 시간제 작업에 대해 다른 .NET Framework 데이터 대신 운영 체제 규칙을 사용합니다. | 없음 |
| **문자열 서식 지정** | 문화권에 민감한 서식을 지원하기 위해 새로운 `ParseExact` 및 `TryParseExact` 메서드 외에도 `ToString`, `Parse` 및 `TryParse` 메서드의 새로운 오버로드가 <xref:System.TimeSpan> 구조에 포함됩니다. | 없음 |

### <a name="globalization"></a>전역화

중립적인 새로운 특정 문화권 목록은 [세계화 및 지역화의 새로운 기능](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd997383%28v=vs.100%29)을 참조하세요.

네임스페이스: <xref:System.Globalization>; 어셈블리: mscorlib(mscorlib.dll)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **문화권 이름** | 다음과 같은 이름 변경은 독일, 디베히 및 아프리카 문화권에 영향을 미칩니다.<br><br>* <xref:System.Globalization.CultureAndRegionInfoBuilder.CurrencyEnglishName>: 독일어(스위스)(de-CH) 문화권의 통화 이름이 “sFr.”에서 “Fr.”로 변경되었습니다.<br>* <xref:System.Globalization.DateTimeFormatInfo.LongDatePattern>: 디베히어(몰디브)(dv-MV) 문화권의 긴 날짜 패턴이 “dd/MMMM/yyyy”에서 “dd/MM/yyyy”로 변경되었습니다.<br>* <xref:System.Globalization.DateTimeFormatInfo.PMDesignator>: 아프리카어(남아프리카)(af-ZA) 문화권의 P.M. 지정자가 “nm”에서 “PM”으로 변경되었습니다. | 문화권 이름이 변경됩니다. |
| **LCID 매개 변수** | 자동화 서버 설정에서 예상되는 동작과의 일관성을 위해, CLR은 더 이상 `LCID` 매개 변수에 대한 현재 문화권을 관리되지 않는 COM 기반 애플리케이션에 전달하지 않습니다. 대신, 문화권에 1033(en-us)을 전달합니다. | 특정 문화권을 요구하는 기본 애플리케이션을 제외하고는 수정이 필요하지 않습니다. |
| **사용되지 않는 문화권 형식** | <xref:System.Globalization.CultureTypes> 및 <xref:System.Globalization.CultureTypes> 문화권 형식은 이제 사용되지 않습니다.<br><br>이전 버전과의 호환성을 위해 이제 <xref:System.Globalization.CultureTypes>는 이전 .NET Framework에 포함되었던 중립적인 특정 문화권을 반환하고, <xref:System.Globalization.CultureTypes>는 빈 목록을 반환합니다. | <xref:System.Globalization.CultureTypes> 열거형의 다른 값을 사용하세요. |
| **문화권 검색** | Windows 7부터 .NET Framework 4는 데이터 자체를 저장하는 대신 운영 체제에서 문화권 정보를 검색합니다. 또한 .NET Framework는 데이터 정렬 및 대/소문자 처리를 위해 Windows와 동기화됩니다. | 없음 |
| **Unicode 5.1 표준** | 이제 .NET Framework는 모든 유니코드 5.1 문자(약 1,400자 추가)를 지원합니다. 추가 문자에는 새로운 기호, 화살표, 분음 부호, 구두점, 수학 기호, CJK 스트로크 및 표의 문자, 추가 말라얄람어 및 텔루구어 숫자 문자, 다양한 미얀마어, 라틴어, 아랍어, 그리스어, 몽골어 및 키릴 문자가 포함됩니다. 유니코드 5.1에서는 다음 새 스크립트가 지원됩니다. 순다어, 렙차어, 올치키어, 바이어(Vai), 사우라슈트라어, 카야리어(Kayah Li), 레장어, 구르무키어, 오리야어, 타밀어, 텔구루어, 말라얌람어 문자 및 참어(Cham)입니다. | 없음 |

### <a name="exceptions"></a>예외

네임스페이스: <xref:System>, <xref:System.Runtime.ExceptionServices>; 어셈블리: mscorlib(mscorlib.dll)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **손상된 프로세스 상태에 대한 예외** | CLR은 더 이상 손상된 프로세스 상태에 대한 예외를 관리 코드의 예외 처리기로 전달하지 않습니다. | 이러한 예외는 프로세스의 상태가 손상되었음을 나타냅니다. 이 상태에서는 애플리케이션을 실행하는 것이 좋지 않습니다.<br><br>자세한 내용은 CLR 자세히 보기 블로그의 <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> 및 [손상된 상태 예외 처리](https://go.microsoft.com/fwlink/?LinkID=179681) 항목을 참조하세요. |
| **실행 엔진 예외** | catchable 예외로 인해 불안정한 프로세스가 계속 실행될 수 있으므로 <xref:System.ExecutionEngineException>은 이제는 사용되지 않습니다. 이러한 변경 덕분에 예측 가능성 및 런타임 시 안정성이 향상됩니다. | <xref:System.InvalidOperationException>을 사용하여 조건을 알리세요. |

### <a name="reflection"></a>반사

네임스페이스: <xref:System.Reflection>; 어셈블리: mscorlib(mscorlib.dll)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **어셈블리 해시 알고리즘** | 어셈블리가 로드되지 않을 경우 런타임에서 참조된 어셈블리의 해시 알고리즘을 알지 못하기 때문에 <xref:System.Reflection.AssemblyName.HashAlgorithm> 속성은 이제 <xref:System.Configuration.Assemblies.AssemblyHashAlgorithm>을 반환합니다. 이는 <xref:System.Reflection.Assembly.GetReferencedAssemblies%2A> 메서드에 의해 반환된 것과 같이 참조된 어셈블리의 속성을 사용함을 의미합니다. | 없음 |
| **어셈블리 로딩** | 어셈블리의 중복 로드를 방지하고 가상 주소 공간을 절약하기 위해 이제 CLR은 Win32 `MapViewOfFile` 함수만 사용하여 어셈블리를 로드합니다. 또한 더 이상 `LoadLibrary` 함수를 호출하지 않습니다.<br><br>이러한 변경은 진단 애플리케이션에 다음과 같은 방식으로 영향을 줍니다.<br><br>* <xref:System.Diagnostics.ProcessModuleCollection>에는 `Process.GetCurrentProcess().Modules`에 대한 호출에서 가져온 클래스 라이브러리(.dll 파일)의 모듈이 더 이상 포함되지 않습니다.<br>`EnumProcessModules` 함수를 사용하는 Win32 애플리케이션은 나열된 관리되는 모듈을 모두 볼 수는 없습니다. | 없음 |
| **선언 형식** | 형식에 선언 형식이 없으면 이제 <xref:System.Type.DeclaringType> 속성이 올바르게 null을 반환합니다. | 없음 |
| **대리자** | 대리자의 생성자에 null 값이 전달되면 이제 대리자가 <xref:System.NullReferenceException> 대신 <xref:System.ArgumentNullException>을 throw합니다. | 예외 처리가 <xref:System.ArgumentNullException>을 catch하는지 확인하세요. |
| **전역 어셈블리 캐시 위치 변경** | .NET Framework 4 어셈블리의 경우 전역 어셈블리 캐시가 Windows 디렉터리(%WINDIR%)에서 Microsoft.Net 하위 디렉터리( *%WINDIR%\\Microsoft.Net*)로 이동했습니다. 이전 버전의 어셈블리는 이전 디렉터리에 남아 있습니다.<br><br>관리되지 않는 [ASM_CACHE_FLAGS](../unmanaged-api/fusion/asm-cache-flags-enumeration.md) 열거형에 새 `ASM_CACHE_ROOT_EX` 플래그가 포함됩니다. 이 플래그는 [GetCachePath](../unmanaged-api/fusion/getcachepath-function.md) 함수로 얻을 수 있는 .NET Framework 4 어셈블리의 캐시 위치를 가져옵니다. | 애플리케이션이 어셈블리에 대한 명시적 경로를 사용하지 않는다고 가정할 경우에는 이 방식이 권장되지 않습니다. |
| **전역 어셈블리 캐시 도구** | [Gacutil.exe(전역 어셈블리 캐시 도구)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ex0ss12c%28v=vs.100%29)는 더 이상 셸 플러그 인 뷰어를 지원하지 않습니다. | 없음 |

### <a name="interoperability"></a>상호 운용성

네임스페이스: <xref:System.Runtime.InteropServices>; 어셈블리: mscorlib(mscorlib.dll)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **버퍼 길이**(관리되지 않는 API) | 메모리를 절약하기 위해 [ICorProfilerInfo2::GetStringLayout](../unmanaged-api/profiling/icorprofilerinfo2-getstringlayout-method.md) 메서드에 대한 `pBufferLengthOffset` 매개 변수의 기능이 `pStringLengthOffset` 매개 변수와 일치하도록 변경되었습니다. 이제 두 매개 변수가 문자열 길이의 오프셋 위치를 가리킵니다. 문자열 클래스의 표시에서 버퍼 길이가 제거되었습니다. | 버퍼 길이에 대한 종속성을 제거하세요. |
| **JIT 디버깅** | JIT(Just-In-Time) 디버깅에 대한 등록을 단순화하기 위해 .NET Framework 디버거는 이제 네이티브 코드의 JIT 디버깅 동작을 제어하는 AeDebug 레지스트리 키만 사용합니다. 이 변경의 결과는 다음과 같습니다.<br><br>* 더 이상 관리되는 네이티브 코드에 대해 서로 다른 두 가지 디버거를 등록할 수 없습니다.<br>* 비대화형 프로세스에 대해 자동으로 디버거를 시작할 수는 없지만, 사용자에게 대화형 프로세스를 요구할 수 있습니다.<br>* 디버거가 시작되지 않거나 시작해야 하는 등록된 디버거가 없을 때 더 이상 알림이 표시되지 않습니다.<br>* 애플리케이션의 대화형 작업에 의존하는 자동 시작 정책이 더 이상 지원되지 않습니다. | 필요에 따라 디버깅 작업을 조정하세요. |
| **플랫폼 호출** | 비관리 코드와의 상호 운용성 성능을 향상하기 위해, 이제 플랫폼 호출에 잘못된 호출 규칙이 있으면 애플리케이션이 실패합니다. 이전 버전에서는 마샬링 계층이 스택 위에서 이러한 오류를 해결했습니다. | Microsoft Visual Studio에서 애플리케이션을 디버그하면 이러한 오류를 알려주므로 수정할 수 있습니다.<br><br>업데이트할 수 없는 이진 파일이 있는 경우 애플리케이션의 구성 파일에 [\<NetFx40_PInvokeStackResilience&gt;](../configure-apps/file-schema/runtime/netfx40-pinvokestackresilience-element.md) 요소를 포함하면 이전 버전과 마찬가지로 스택 위에서 호출 오류를 해결할 수 있습니다. 그러나 이 경우 애플리케이션의 성능에 영향을 줄 수 있습니다. |
| **제거된 인터페이스**(관리되지 않는 API) | 개발자에게 혼란을 주지 않도록 다음 인터페이스가 제거되었습니다. 이러한 인터페이스는 유용한 런타임 시나리오를 제공하지 않았고 CLR이 구현을 제공하거나 수락하지 않았기 때문입니다.<br><br>* **INativeImageINativeImageDependency**<br>* **INativeImageInstallInfo**<br>* **INativeImageEvaluate**<br>* **INativeImageConverter**<br>* **ICorModule**<br>* **IMetaDataConverter** | 없음 |

## <a name="data"></a>데이터

이 섹션에서는 데이터 집합 및 SQL 클라이언트, Entity Framework, LINQ to SQL, WCF Data Services(이전의 ADO.NET Data Services) 사용에 대한 마이그레이션 문제를 설명합니다.

### <a name="dataset-and-sql-client"></a>데이터 세트 및 SQL 클라이언트

다음 표에서는 이전에 제한 사항이었거나 기타 문제가 있던 기능의 개선 내용을 설명합니다.

네임스페이스: <xref:System.Data>, <xref:System.Data.Objects.DataClasses>, <xref:System.Data.SqlClient>; 어셈블리: System.Data(System.Data.dll의), System.Data.Entity(System.Data.Entity.dll의)

| 기능 | 3\.5 SP1과의 차이점 |
| ------- | ------------------------ |
| **POCO 시나리오** | <xref:System.Data.Objects.DataClasses.IRelatedEnd> 인터페이스에는 POCO(Plain Old CLR Object) 시나리오의 유용성을 개선하기 위한 새로운 방법이 있습니다. 이 새로운 메서드는 매개 변수로 <xref:System.Data.Objects.DataClasses.IEntityWithRelationships> 엔터티 대신 <xref:System.Object>를 사용합니다. |
| **행 편집** | <xref:System.Data.DataView> 클래스에 의해 구현된 <xref:System.Collections.IList.IndexOf%2A> 메서드는 이제 -1을 반환하는 대신 편집 중인 행의 값을 올바르게 반환합니다. |
| **이벤트** | 행이 수정된 상태이고 <xref:System.Data.DataRow.RejectChanges%2A> 메서드가 호출되면 이제 <xref:System.Data.DataRowView.PropertyChanged> 이벤트가 발생합니다. 이러한 변경을 통해 <xref:System.Data.DataSet> 개체의 내용을 노출하는 UI 컨트롤을 더 쉽게 만들 수 있습니다. |
| **예외** | 연결이 설정되어 있지 않거나 <xref:System.NullReferenceException> 대신 열려 있으면 이제 <xref:System.Data.SqlClient.SqlCommand.Prepare%2A> 메서드가 <xref:System.InvalidOperationException>을 throw합니다. |
| **매핑 보기** | 쿼리 뷰 매핑 오류가 이제 런타임에 <xref:System.NullReferenceException>을 throw하는 대신 디자인 타임에 catch됩니다.<br><br>이제 매핑 유효성 검사는 개념 스키마(CSDL)의 두 연결 집합이 동일한 열로 매핑되는 오류를 catch합니다. |
| **트랜잭션** | 트랜잭션이 완료된 후(중단되거나 롤백된 경우 포함) 애플리케이션이 연결에서 명령문을 실행하려고 하면 이제 <xref:System.InvalidOperationException>이 throw됩니다. 이전 버전에서는 예외가 throw되지 않았으므로 트랜잭션이 중단되더라도 추가 명령을 실행할 수 있었습니다. |

### <a name="entity-framework"></a>Entity Framework

다음 표에서는 이전에 제한 사항이었거나 기타 문제가 있던 기능의 개선 내용을 설명합니다.

네임스페이스: <xref:System.Data>, <xref:System.Data.Objects>, <xref:System.Data.Objects.DataClasses>; 어셈블리: System.Data.Entity(System.Data.Entity.dll의)

| 기능 | 3\.5 SP1과의 차이점 |
| ------- | ------------------------ |
| **엔터티 개체** | 이제 <xref:System.Data.Objects.ObjectContext.Detach%2A> 메서드와 <xref:System.Data.Objects.ObjectContext.SaveChanges%2A> 메서드가 호출될 때 엔터티 개체의 상태 간에 패리티가 있습니다. 이렇게 일관성이 향상되어 예기치 않은 예외가 throw되지 않습니다. |
| **Entity SQL** | Entity SQL에서 식별자 해결에 대한 규칙이 개선되었습니다.<br><br>Entity SQL 파서에서 다중 파트 식별자 확인에 대한 논리가 개선되었습니다. |
| **구조적 주석** | 이제 Entity Framework가 구조적 주석을 인식합니다. |
| **쿼리** | 쿼리는 다음과 같이 향상되었습니다.<br><br>* 빈 컬렉션에 대해 null 키를 사용하는 `GroupBy` 쿼리는 쿼리에 추가 선택 항목이 있는지에 관계없이 행을 반환하지 않습니다.<br>* LINQ 및 Entity-SQL 쿼리에서 생성된 SQL은 기본적으로 문자열 매개 변수를 유니코드가 아닌 값으로 처리합니다. |

### <a name="linq-to-sql"></a>LINQ to SQL

다음 표에서는 이전에 제한 사항이었거나 기타 문제가 있던 기능의 개선 내용을 설명합니다.

네임스페이스: <xref:System.Data.Linq>; 어셈블리: System.Data.Linq(System.Data.Linq.dll의)

| 기능 | 3\.5 SP1과의 차이점 |
| ------- | ------------------------ |
| **이벤트** | 컬렉션이 로드될 때 이벤트를 일으키는 것 외에도, <xref:System.Data.Linq.EntitySet%601>가 언로드될 때 <xref:System.Data.Linq.EntitySet%601> 컬렉션은 이제 추가 및 제거 작업에 대해 <xref:System.Data.Linq.EntitySet%601.ListChanged> 이벤트를 발생시킵니다. |
| **쿼리** | `Skip(0)`은 LINQ to SQL 쿼리에서 더 이상 무시되지 않습니다. 따라서 이 메서드가 있는 쿼리가 다르게 동작할 수 있습니다. 예를 들면 경우에 따라 `Skip(0)`에 `OrderBy` 절이 필요하며, `OrderBy` 절이 포함되지 않은 경우 이제 쿼리에서 <xref:System.NotSupportedException> 예외를 throw합니다. |

### <a name="wcf-data-services"></a>WCF Data Services

다음 표에서는 이전에 제한 사항이었거나 기타 문제가 있던 기능의 개선 내용을 설명합니다.

네임스페이스: <xref:System.Data.Services>, <xref:System.Data.Services.Client>, <xref:System.Data.Services.Common>, <xref:System.Data.Services.Providers>; 어셈블리: System.Data.Services(System.Data.Services.dll의), System.Data.Services.Client(System.Data.Services.Client.dll의)

| 기능 | 3\.5 SP1과의 차이점 |
| ------- | ------------------------ |
| **일괄 처리된 이진 콘텐츠** | 이제 WCF 데이터 서비스는 요청 및 응답에서 일괄 처리된 이진 콘텐츠를 지원합니다. |
| **변경 인터셉터** | 이제 삭제 요청에 대해 변경 인터셉터가 실행됩니다.<br><br>변경 인터셉터는 엔터티 집합의 엔터티를 수정하기 위해 서버에서 요청을 수신할 때마다 실행되는 메서드로서, 들어오는 요청이 실행되기 전에 실행됩니다. 또한 변경되고 있는 엔터티 및 여기에서 수행되는 작업에 대한 액세스를 제공합니다. |
| **예외** | 다음 조건은 이제 <xref:System.NullReferenceException> 대신 좀 더 유용한 예외를 throw합니다.<br><br>* 데이터 서비스 호출이 시간 초과될 때 <xref:System.ServiceProcess.TimeoutException>.<br>* 데이터 서비스에 대한 잘못된 요청이 있을 때 <xref:System.Data.Services.Client.DataServiceRequestException>.<br><br>애플리케이션에서 새 예외를 catch하려면 예외 처리를 변경해야 합니다. |
| **헤더** | 헤더는 다음과 같이 향상되었습니다.<br><br>* WCF Data Services는 이제 지정되지 않은 값을 가지고 있는 `eTag` 헤더를 올바르게 거부합니다.<br>* WCF Data Services는 이제 오류를 반환하고, 요청에 `if-*` 헤더가 있을 때 링크에 대한 삭제 요청을 실행하지 않습니다.<br>* WCF Data Services는 이제 클라이언트가 Accept 헤더에 지정한 형식(Atom, JSON)으로 클라이언트에 오류를 반환합니다. |
| **JSON 판독기** | JSON(JavaScript Object Notation) 판독기는 이제 WCF 데이터 서비스로 전송된 JSON 페이로드를 처리할 때 단일 백 슬래시(“\\”) 이스케이프 문자를 읽을 경우 올바르게 오류를 반환합니다. |
| **병합** | <xref:System.Data.Services.Client.MergeOption> 열거형은 다음과 같이 향상되었습니다.<br><br>* <xref:System.Data.Services.Client.MergeOption> 병합 옵션은 더 이상 데이터 서비스에서 오는 후속 응답의 결과로 클라이언트의 엔터티를 수정하지 않습니다.<br>* <xref:System.Data.Services.Client.MergeOption> 옵션은 이제 동적 SQL과 저장 프로시저 기반 업데이트 간에 일치합니다. |
| **요청** | <xref:System.Data.Services.DataService%601.OnStartProcessingRequest%2A> 메서드는 이제 데이터 서비스에 대한 요청이 처리되기 전에 호출됩니다. 따라서 <xref:System.Data.Services.Providers.ServiceOperation> 서비스에 대한 요청이 올바르게 작동할 수 있습니다. |
| **스트림** | WCF Data Services는 더 이상 읽기 및 쓰기 작업에 대한 기본 스트림을 닫지 않습니다. |
| **URI** | WCF Data Services 클라이언트에서 URI의 이스케이프가 수정되었습니다. |

## <a name="windows-communication-foundation-wcf"></a>WCF(Windows Communication Foundation)

다음 표에서는 이전에 제한 사항이었거나 기타 문제가 있던 기능의 개선 내용을 설명합니다.

| 기능 | 3\.5 SP1과의 차이점 |
| ------- | ------------------------ |
| **구성 파일** | 구성 파일 계층 구조를 통해 동작을 상속할 수 있도록 WCF는 이제 구성 파일 간 병합을 지원합니다.<br><br>이제 구성 상속 모델이 확장되어 컴퓨터에서 실행 중인 모든 서비스에 적용될 동작을 사용자가 정의할 수 있습니다.<br><br>계층 구조의 서로 다른 수준에 같은 이름의 동작이 있는 경우 동작 변경이 발생할 수 있습니다. |
| **서비스 호스팅** | 요소 정의에 `allowDefinition="MachineToApplication"` 특성을 추가하여 서비스 수준에서 더 이상 `<serviceHostingEnvironment>` 구성 요소를 지정할 수 없습니다.<br><br>서비스 수준에서 `<serviceHostingEnvironment>` 요소를 지정하는 것은 기술적으로 올바르지 않으며, 이로 인해 일관성 없는 동작이 발생합니다. |

## <a name="windows-presentation-foundation-wpf"></a>WPF(Windows Presentation Foundation)

### <a name="applications"></a>애플리케이션

네임스페이스: <xref:System.Windows>, <xref:System.Windows.Controls>; 어셈블리: PresentationFramework(PresentationFramework.dll의)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **예외 처리** | 오류를 더 일찍 검색할 수 있도록 WPF는 <xref:System.Reflection.TargetInvocationException>을 throw하고 원래 예외를 catch하는 대신 <xref:System.Exception.InnerException> 속성을 <xref:System.NullReferenceException>, <xref:System.OutOfMemoryException>, <xref:System.StackOverflowException> 및 <xref:System.Security.SecurityException>과 같은 심각한 예외로 설정합니다. | 없음 |
| **연결된 리소스** | 좀 더 쉬운 연결을 위해, 프로젝트의 폴더 구조가 아닌 다른 위치에 있는 리소스 파일(예: 이미지)은 애플리케이션을 빌드할 때 파일 이름 대신 리소스 파일의 전체 경로를 리소스 ID로 사용합니다. 애플리케이션은 런타임 시 파일을 찾을 수 있습니다. | 없음 |
| **부분 신뢰 애플리케이션** | 보안상의 이유로, 부분 신뢰로 실행되고 HTML이 포함된 <xref:System.Windows.Controls.WebBrowser> 컨트롤 또는 <xref:System.Windows.Controls.Frame> 컨트롤을 포함하는 Windows 기반 애플리케이션은 컨트롤이 생성될 때 <xref:System.Security.SecurityException>을 throw합니다.<br><br>브라우저 애플리케이션은 예외를 throw하고 다음 조건이 모두 충족될 경우 메시지를 표시합니다.<br><br>* 애플리케이션이 Firefox에서 실행되고 있습니다.<br>* 애플리케이션이 신뢰할 수 없는 사이트의 인터넷 영역에서 부분 신뢰로 실행되고 있습니다.<br>* 애플리케이션에 HTML이 포함된 <xref:System.Windows.Controls.WebBrowser> 컨트롤 또는 <xref:System.Windows.Controls.Frame> 컨트롤이 있습니다.<br><br>신뢰할 수 있는 사이트 또는 인트라넷 영역에서 실행되는 애플리케이션은 영향을 받지 않습니다. | 브라우저 애플리케이션에서 다음 중 하나를 수행하여 이 변경의 영향을 완화할 수 있습니다.<br><br>* 완전 신뢰에서 브라우저 애플리케이션을 실행합니다.<br>* 고객이 애플리케이션의 사이트를 신뢰할 수 있는 사이트 영역에 추가하도록 합니다.<br>* 고객이 Internet Explorer에서 애플리케이션을 실행하도록 합니다. |
| **리소스 사전** | 테마 수준 리소스 사전을 개선하고, 변경하지 못하도록 리소스 사전에 정의되어 있고 테마 수준 사전에 병합된 고정 가능한 리소스는 항상 고정된 것으로 표시되며 변경되지 않습니다. 이것이 고정 가능한 리소스에 대해 예상되는 동작입니다. | 테마 수준에서 병합된 사전에 정의된 리소스를 수정하는 애플리케이션은 리소스를 복제하고 복제된 복사본을 수정해야 합니다. 또는 리소스를 쿼리할 때마다 <xref:System.Windows.ResourceDictionary>에서 새 복사본을 만들도록 리소스를 `x:Shared="false"`로 표시할 수 있습니다. |
| **Windows 7** | WPF 애플리케이션이 Windows 7에서 더 잘 작동할 수 있도록 다음과 같이 창 동작이 수정되었습니다.<br><br>* 도킹 및 제스처 상태가 이제 사용자 상호 작용을 기반으로 예상대로 작동합니다.<br>* 작업 표시줄 명령 **Cascade windows, Show windows stacked** 및 **Show windows side-by-side**가 이제 올바르게 작동하고 적절한 속성을 업데이트합니다.<br>* 이제 최대화 또는 최소화된 창의 `Top`, `Left`, `Width` 및 `Height` 속성에 모니터에 따라 다른 값 대신 창의 올바른 복원 위치가 포함됩니다. | 없음 |
| **창 스타일 및 투명도** | <xref:System.Windows.Window.AllowsTransparency>가 `true`이고 <xref:System.Windows.WindowState>가 <xref:System.Windows.WindowState>일 때 <xref:System.Windows.Window.WindowStyle>을 <xref:System.Windows.WindowStyle> 이외의 값으로 설정하려고 하면 <xref:System.InvalidOperationException>이 throw됩니다. | <xref:System.Windows.Window.AllowsTransparency>가 `true`일 때 <xref:System.Windows.Window.WindowStyle>을 변경해야 하는 경우 Win32 `SetWindowLongPtr` 기능을 호출할 수 있습니다. |
| **XPS 뷰어** | WPF에는 Microsoft XPSEP(XML Paper Specification Essentials Pack)가 포함되어 있지 않습니다. XPSEP는 Windows 7 및 Windows Vista에 포함되어 있습니다.<br><br>.NET Framework 3.5 SP1을 설치하지 않고 Windows XP를 실행하는 컴퓨터에서는 <xref:System.Windows.Controls.PrintDialog>에 있는 것 이외의 WPF API를 사용하여 인쇄할 때 WINSPOOL에 의존하게 됩니다. 일부 프린터 기능은 보고되지 않으며 일부 프린터 설정은 인쇄 중에 적용되지 않습니다. | 필요한 경우 [Microsoft XML Paper Specification Essentials Pack](https://go.microsoft.com/fwlink/?LinkId=178895)을 설치하세요. |

### <a name="controls"></a>컨트롤

네임스페이스: <xref:System.Windows>, <xref:System.Windows.Controls>, <xref:System.Windows.Data>, <xref:System.Windows.Input>; 어셈블리: PresentationFramework(PresentationFramework.dll의), PresentationCore(PresentationCore.dll의), WindowsBase(WindowsBase.dll의)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **대화 상자** | 안정성을 높이기 위해 <xref:Microsoft.Win32.CommonDialog.ShowDialog%2A> 메서드는 <xref:Microsoft.Win32.FileDialog> 컨트롤을 만든 동일한 스레드에서 호출됩니다. | 반드시 <xref:Microsoft.Win32.FileDialog> 컨트롤을 만들고 동일한 스레드에서 <xref:Microsoft.Win32.CommonDialog.ShowDialog%2A> 메서드를 호출해야 합니다. |
| **부동 창** | 부동 창을 올바르지 않게 계속해서 다시 활성화하여 모달 대화 상자처럼 표시되게 하는 포커스 복원 논리를 수정하기 위해, 이제 후보가 창의 자식이 아닌 경우 포커스 복원이 방지됩니다. | 없음 |
| **컬렉션의 항목** | 항목을 기본 컬렉션으로 이동하거나 추가할 경우, <xref:System.Windows.Data.CollectionView>가 정렬되지 않으면 동일한 상대 위치의 <xref:System.Windows.Data.CollectionView>에 항목이 나타납니다. 이렇게 하면 컬렉션의 항목 위치 및 연관된 <xref:System.Windows.Data.CollectionView>의 항목 위치 간에 일관성이 유지됩니다. | 항목의 고정된 위치에 의존하는 대신 <xref:System.Windows.Data.CollectionView>에서 항목의 위치를 찾으려면 <xref:System.Windows.Controls.ItemContainerGenerator.ContainerFromItem%2A> 또는 <xref:System.Windows.Data.CollectionView.IndexOf%2A> 메서드를 사용하세요. |
| **레이아웃** | 불필요한 레이아웃 재작업을 제거하기 위해 <xref:System.Windows.Controls.Page.ShowsNavigationUI>를 변경하면 더 이상 레이아웃이 무효화되지 않거나 다른 레이아웃이 전달됩니다. | <xref:System.Windows.Controls.Page.ShowsNavigationUI>를 변경하면 다른 레이아웃이 전달될 것으로 예상하는 경우, 속성을 설정한 후에 <xref:System.Windows.UIElement.InvalidateVisual%2A>을 호출하세요. |
| **메뉴** | 메뉴 팝업에서 ClearType 텍스트를 사용할 수 있도록 <xref:System.Windows.Controls.ControlTemplate> 클래스와 <xref:System.Windows.Controls.MenuItem> 컨트롤 및 기타 컨트롤이 수정되었습니다. | 애플리케이션은 컨트롤 템플릿의 시각적 구조에 의존해서는 안 됩니다. <xref:System.Windows.Controls.ControlTemplate>의 명명된 부분만 공용 계약의 일부입니다. 애플리케이션이 <xref:System.Windows.Controls.ControlTemplate>에서 특정 개체를 찾아야 하는 경우, 트리에서 개체의 고정된 위치에 의존하는 대신 시각적 트리에서 특정 형식을 검색하세요. |
| **탐색** | <xref:System.Windows.Controls.Frame>이 특정 위치로 직접 이동하면 초기 탐색 후 <xref:System.Windows.Navigation.NavigatingCancelEventArgs.IsNavigationInitiator> 속성은 `true`입니다. 이러한 변경 덕분에 시작 시나리오 중에 추가 이벤트가 발생하지 않습니다. | 없음 |
| **팝업** | 레이아웃 전달 중에 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> 대리자를 한 번만 호출하는 대신 여러 번 호출할 수 있습니다. | <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> 대리자가 이전 위치를 기반으로 <xref:System.Windows.Controls.Primitives.Popup>의 위치를 계산할 때 `popupSize`, `targetSize` 또는 `offset` 매개 변수의 값이 변경되는 경우에만 위치를 다시 계산하세요. |
| **속성 값** | <xref:System.Windows.DependencyObject.SetCurrentValue%2A> 메서드를 사용할 경우 속성에 영향을 미치는 모든 바인딩, 스타일 또는 트리거는 계속 준수되지만, 속성을 유효한 값으로 설정할 수 있습니다. | 컨트롤 작성자는 사용자 조작을 포함하여 다른 동작의 부작용으로 속성 값이 변경될 때마다 <xref:System.Windows.DependencyObject.SetCurrentValue%2A>를 사용해야 합니다. |
| **텍스트 상자** | 보안상의 이유로, <xref:System.Windows.Forms.TextBoxBase.Copy%2A> 및 <xref:System.Windows.Forms.TextBoxBase.Cut%2A> 메서드는 부분 신뢰로 호출될 때 자동으로 실패합니다.<br><br>또한 <xref:System.Windows.Controls.Primitives.TextBoxBase>에서 상속한 컨트롤의 <xref:System.Windows.Input.ApplicationCommands.Copy> 또는 <xref:System.Windows.Input.ApplicationCommands.Cut> 속성을 프로그래밍 방식으로 실행하면 부분 신뢰에서 차단됩니다. 그러나 <xref:System.Windows.Controls.Primitives.ButtonBase.Command> 속성이 이러한 명령 중 하나에 바인딩된 단추를 클릭하는 등 사용자가 시작한 복사 및 잘라내기 명령은 작동합니다. 바로 가기 키를 통한 표준 복사 및 잘라내기와 상황에 맞는 메뉴는 이전과 마찬가지로 부분 신뢰로 작동합니다. | 단추 클릭 등 사용자가 시작한 작업에 <xref:System.Windows.Input.ApplicationCommands.Copy> 또는 <xref:System.Windows.Input.ApplicationCommands.Cut> 명령을 바인딩하세요. |

### <a name="graphics"></a>그래픽

네임스페이스: <xref:System.Windows>, <xref:System.Windows.Controls>, <xref:System.Windows.Data>, <xref:System.Windows.Input>, <xref:System.Windows.Media.Effects>; 어셈블리: PresentationFramework(PresentationFramework.dll의), PresentationCore(PresentationCore.dll의), WindowsBase(WindowsBase.dll의)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **비트맵 효과** | 성능 향상을 위해, <xref:System.Windows.Media.Effects.BitmapEffect> 클래스 및 <xref:System.Windows.Media.Effects.BitmapEffect> 클래스에서 상속한 클래스는 여전히 존재하지만 비활성화되어 있습니다. 다음 조건이 참인 경우 하드웨어 가속 렌더링 파이프라인을 사용하여 효과가 렌더링됩니다.<br><br>* 애플리케이션은 반경 속성이 100DIU 미만인 <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> 또는 <xref:System.Windows.Media.Effects.BlurBitmapEffect>를 사용합니다.<br>* 애플리케이션을 실행하는 컴퓨터의 비디오 카드는 픽셀 셰이더 2.0을 지원합니다.<br><br>이러한 조건이 충족되지 않으면 <xref:System.Windows.Media.Effects.BitmapEffect> 개체는 아무 효과도 없습니다.<br><br>또한 Visual Studio는 <xref:System.Windows.Media.Effects.BitmapEffect> 개체 또는 하위 클래스를 발견하면 컴파일러 경고를 생성합니다.<br><br><xref:System.Windows.Media.DrawingContext.PushEffect%2A> 메서드는 사용되지 않는 것으로 표시됩니다. | 기존의 <xref:System.Windows.Media.Effects.BitmapEffect> 및 파생 클래스 사용을 중단하고 대신 <xref:System.Windows.Media.Effects.Effect>에서 파생된 새 클래스(<xref:System.Windows.Media.Effects.BlurEffect>, <xref:System.Windows.Media.Effects.DropShadowEffect> 및 <xref:System.Windows.Media.Effects.ShaderEffect>)를 사용하세요.<br><br><xref:System.Windows.Media.Effects.ShaderEffect> 클래스로부터 상속받아 자신의 고유한 효과를 만들 수도 있습니다. |
| **비트맵 프레임** | 복제된 <xref:System.Windows.Media.Imaging.BitmapFrame> 개체는 이제 <xref:System.Windows.Media.Imaging.BitmapSource.DownloadProgress>, <xref:System.Windows.Media.Imaging.BitmapSource.DownloadCompleted> 및 <xref:System.Windows.Media.Imaging.BitmapSource.DownloadFailed> 이벤트를 수신합니다. 이렇게 하면, 웹에서 다운로드되어 <xref:System.Windows.Controls.Image> 컨트롤에 적용된 이미지가 <xref:System.Windows.Style>을 통해 올바르게 작동합니다.<br><br>다음이 모두 참인 경우에만 동작이 변경됩니다.<br><br>* <xref:System.Windows.Media.Imaging.BitmapSource.DownloadProgress>, <xref:System.Windows.Media.Imaging.BitmapSource.DownloadCompleted> 또는 <xref:System.Windows.Media.Imaging.BitmapSource.DownloadFailed> 이벤트를 구독합니다.<br>* <xref:System.Windows.Media.Imaging.BitmapFrame>의 소스가 웹에서 온 것입니다.<br>* 다운로드가 진행되는 동안 <xref:System.Windows.Media.Imaging.BitmapFrame>이 복제됩니다. | 이벤트 처리기에서 전송자를 확인하고 전송자가 원래 <xref:System.Windows.Media.Imaging.BitmapFrame>인 경우에만 조치를 취하세요. |
| **이미지 디코딩** | 이미지가 디코딩되지 않을 때 <xref:System.IO.IOException>이 처리되지 않도록 <xref:System.Windows.Media.Imaging.BitmapSource> 클래스는 이미지를 디코딩하지 않을 때 <xref:System.Windows.Media.Imaging.BitmapSource.DecodeFailed> 이벤트를 일으킵니다. | <xref:System.IO.IOException>에 대한 예외 처리를 제거하고 <xref:System.Windows.Media.Imaging.BitmapSource.DecodeFailed> 이벤트를 사용하여 디코딩 실패를 확인하세요. |

### <a name="input"></a>입력

네임스페이스: <xref:System.Windows>, <xref:System.Windows.Controls>, <xref:System.Windows.Data>, <xref:System.Windows.Input>; 어셈블리: PresentationFramework(PresentationFramework.dll의), PresentationCore(PresentationCore.dll의), WindowsBase(WindowsBase.dll의)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **명령 인스턴스 바인딩** | 보기-모델 기반 명령 인스턴스를 보기 기반 입력 제스처에 바인딩하는 메커니즘을 제공하기 위해 <xref:System.Windows.Input.InputBinding> 클래스는 이제 <xref:System.Windows.DependencyObject> 대신 <xref:System.Windows.Freezable>에서 상속받습니다. 이제 다음 속성이 종속성 속성이 됩니다.<br><br>* <xref:System.Windows.Input.InputBinding.Command><br>* <xref:System.Windows.Input.InputBinding.CommandParameter><br>* <xref:System.Windows.Input.InputBinding.CommandTarget><br><br>이 변경의 결과는 다음과 같습니다.<br><br>* 이제 <xref:System.Windows.Input.InputBinding> 개체는 변경 가능한 상태로 유지되는 대신 등록 시 고정됩니다.<br>* <xref:System.Windows.DependencyObject> 클래스의 제한 때문에 다중 스레드에서 인스턴스 수준 <xref:System.Windows.Input.InputBinding> 개체에 액세스할 수 없습니다.<br>* <xref:System.Windows.Freezable> 클래스의 제한 때문에 등록 이후에 클래스 수준 입력 바인딩을 변경할 수 없습니다.<br>* 보기-모델에서 작성된 명령 인스턴스에는 입력 바인딩을 지정할 수 없습니다. | 바인딩이 변경될 수 있는 경우 개별 스레드에 <xref:System.Windows.Input.InputBinding> 클래스의 개별 인스턴스를 작성하거나 아니면 고정하세요. 등록된 후에는 클래스 수준의 정적 <xref:System.Windows.Input.InputBinding>을 변경하지 마세요. |
| **브라우저 애플리케이션** | WPF 브라우저 애플리케이션(.XBAP)은 이제 개체가 올바른 순서로 라우팅된 키 이벤트를 수신할 수 있도록 독립 실행형 WPF 애플리케이션과 마찬가지로 키 이벤트를 처리합니다. | 없음 |
| **데드 키 조합** | WPF는 눈에 보이는 문자를 생성하지 않는 데드 키를 난독 처리하지만, 대신 키가 다음 문자 키와 결합되어 한 문자를 생성함을 나타냅니다. <xref:System.Windows.Input.Keyboard.KeyDownEvent> 이벤트와 같은 키 입력 이벤트는 <xref:System.Windows.Input.KeyEventArgs.Key> 속성을 <xref:System.Windows.Input.Key> 값으로 설정하여 키가 데드 키일 때 보고합니다. 애플리케이션은 일반적으로 결합된 문자를 만드는 키보드 입력에 응답하지 않으므로, 이는 일반적으로 예상되는 동작입니다. | 결합된 문자의 일부였던 키를 읽어야 하는 애플리케이션은 <xref:System.Windows.Input.KeyEventArgs.DeadCharProcessedKey> 속성을 사용하여 현재 모호한 키를 얻을 수 있습니다. |
| **포커스 관리자** | `true`로 설정된 [IsFocusScope](xref:System.Windows.Input.FocusManager.IsFocusScope%2A) 연결 속성이 있는 요소가 <xref:System.Windows.Input.FocusManager.GetFocusedElement(System.Windows.DependencyObject)?displayProperty=nameWithType> 메서드에 전달되면, 이 메서드는 해당 포커스 영역 내에서 마지막 키보드 포커스 요소인 요소를 반환합니다. 단, 반환된 요소가 메서드에 전달된 요소와 동일한 <xref:System.Windows.PresentationSource> 개체여야 합니다. | 없음 |

### <a name="ui-automation"></a>UI 자동화

네임스페이스: <xref:System.Windows>, <xref:System.Windows.Automation.Peers>, <xref:System.Windows.Automation.Provider>, <xref:System.Windows.Controls>, <xref:System.Windows.Data>, <xref:System.Windows.Input>; 어셈블리: PresentationFramework(PresentationFramework.dll의), PresentationCore(PresentationCore.dll의), UIAutomationProvider(UIAutomationProvider.dll의), WindowsBase(WindowsBase.dll의)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **보기의 클래스 계층 구조** | <xref:System.Windows.Automation.Peers.TreeViewAutomationPeer> 및 <xref:System.Windows.Automation.Peers.TreeViewItemAutomationPeer> 클래스는 <xref:System.Windows.Automation.Peers.FrameworkElementAutomationPeer> 대신 <xref:System.Windows.Automation.Peers.ItemsControlAutomationPeer>에서 상속합니다. | <xref:System.Windows.Automation.Peers.TreeViewItemAutomationPeer> 클래스에서 상속하고 <xref:System.Windows.Automation.Peers.TreeViewItemAutomationPeer.GetChildrenCore%2A> 메서드를 재정의하는 경우 새 <xref:System.Windows.Automation.Peers.TreeViewDataItemAutomationPeer> 클래스에서 상속하는 개체의 반환을 고려해 보세요. |
| **화면 밖 컨테이너** | 잘못된 반환 값을 수정하기 위해 <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.IsOffscreenCore%2A> 메서드는 보기에서 벗어나 스크롤된 항목 컨테이너에 대해 이제 `false`를 올바르게 반환합니다. 또한 메서드의 값은 다른 창에 의해 가려지는지 또는 요소가 특정 모니터에 표시되는지 여부에 의해 영향을 받지 않습니다. | 없음 |
| **메뉴 및 자식 개체** | <xref:System.Windows.Controls.MenuItem> 개체가 아닌 자식이 포함된 메뉴의 UI 자동화를 사용할 수 있도록, <xref:System.Windows.Automation.Peers.MenuItemAutomationPeer.GetChildrenCore%2A> 메서드는 <xref:System.Windows.Automation.Peers.MenuItemAutomationPeer> 개체 대신 자식 <xref:System.Windows.UIElement> 개체의 <xref:System.Windows.Automation.Peers.AutomationPeer> 개체를 반환합니다. | 없음 |
| **새 인터페이스 및 어셈블리** | UI 자동화에 대한 새로운 기능을 사용할 수 있도록 다음 인터페이스가 추가되었습니다.<br><br>* <xref:System.Windows.Automation.Provider.IItemContainerProvider><br>* <xref:System.Windows.Automation.Provider.ISynchronizedInputProvider><br>* <xref:System.Windows.Automation.Provider.IVirtualizedItemProvider> | WPF 자동화 피어를 빌드하는 프로젝트는 UIAutomationProvider.dll에 대한 명시적 참조를 추가해야 합니다. |
| **Thumb** | <xref:System.Windows.Automation.Peers.ThumbAutomationPeer.GetClassNameCore%2A> 메서드는 null 대신 값을 반환합니다. 따라서 <xref:System.Windows.Controls.Primitives.Thumb> 클래스에서 상속하는 <xref:System.Windows.Controls.GridSplitter> 등의 컨트롤은 이름을 UI 자동화에 보고합니다. | 없음 |
| **가상화된 요소** | 성능 향상을 위해 <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetChildrenCore%2A> 메서드는 가상화 여부와 관계없이 모든 자식 개체 대신 시각적 트리에 실제로 있는 자식 개체만 반환합니다. | <xref:System.Windows.Automation.Peers.ItemsControlAutomationPeer>의 모든 항목을 반복하려면 <xref:System.Windows.Automation.ItemContainerPattern>을 사용하세요. |

### <a name="xaml"></a>XAML

네임스페이스: <xref:System.Windows>, <xref:System.Windows.Controls>, <xref:System.Windows.Data>, <xref:System.Windows.Input>, <xref:System.Windows.Markup>; 어셈블리: PresentationFramework(PresentationFramework.dll의), PresentationCore(PresentationCore.dll의), WindowsBase(WindowsBase.dll의)

| 기능 | 3\.5 SP1과의 차이점 | 권장 변경 내용 |
| ------- | ------------------------ | ------------------- |
| **태그 확장** | WPF는 이제 속성을 설정하거나 컬렉션에 항목을 만들기 위해 태그 확장을 사용할 때 경우에 따라 <xref:System.Windows.Markup.MarkupExtension> 개체를 반환하는 대신 항상 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A> 메서드의 값을 올바르게 사용합니다. 경우에 따라 태그 확장은 자체를 반환할 수 있습니다. | 애플리케이션이 이전 버전에서 <xref:System.Windows.Markup.MarkupExtension> 개체를 반환한 리소스에 액세스하는 경우 <xref:System.Windows.Markup.MarkupExtension> 개체 대신 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>에서 반환된 개체를 참조하세요. |
| **특성 구문 분석** | 이제 XAML의 특성에는 마침표를 하나만 포함할 수 있습니다. 예를 들어, 다음은 유효합니다.<br><br>`<Button Background="Red"/>`(마침표 없음)<br><br>`<Button Button.Background = "Red"/>`(마침표 1개)<br><br>다음은 유효하지 않습니다.<br><br>`<Button Control.Button.Background = "Red"/>`(마침표 2개 이상) | 마침표가 2개 이상인 XAML 특성을 수정하세요. |

## <a name="xml"></a>XML

다음 표의 각 행에서는 이전에 제한 사항이었거나 기타 문제가 있던 기능의 개선 내용을 설명합니다.

### <a name="schema-and-transforms"></a>스키마 및 변환

네임스페이스: <xref:System.Xml.Linq>, <xref:System.Xml.Schema>, <xref:System.Xml.XPath>; 어셈블리: System.Xml(System.Xml.dll의), System.Xml.Linq(System.Xml.Linq.dll의)

| 기능 | 3\.5 SP1과의 차이점 |
| ------- | ------------------------ |
| **카멜레온 스키마** | 데이터 손상을 방지하기 위해 이제 카멜레온 스키마는 여러 스키마에 포함될 때 올바르게 복제됩니다.<br><br>카멜레온 스키마는 대상 네임스페이스가 없는 스키마이며, 다른 XSD에 포함될 때 가져오기 스키마의 대상 네임스페이스를 사용합니다. 카멜레온 스키마는 스키마에 공통 형식을 포함하는 데 종종 사용됩니다. |
| **ID 함수** | <xref:System.Xml.XmlReader> 개체가 XLST에 전달될 때 이제 XSLT [id 함수](/sql/xquery/functions-on-sequences-id)가 null 대신 올바른 값을 반환합니다.<br><br>사용자가 <xref:System.Xml.Linq.XNode.CreateReader%2A> 메서드를 사용하여 LINQ to XML 클래스에서 <xref:System.Xml.XmlReader> 개체를 만들었고 이 <xref:System.Xml.XmlReader> 개체가 XSLT로 전달된 경우, XSLT의 `id` 함수 인스턴스가 전에는 null을 반환했습니다. 이것은 `id` 함수에 대해 허용된 반환 값이 아닙니다. |
| **네임스페이스 특성** | 데이터 손상을 방지하기 위해 이제 <xref:System.Xml.XPath.XPathNavigator> 개체가 `x:xmlns` 특성의 로컬 이름을 올바르게 반환합니다. |
| **네임스페이스 선언** | 하위 트리의 <xref:System.Xml.XmlReader> 개체는 더 이상 하나의 XML 요소 내에 중복된 네임스페이스 선언을 만들지 않습니다. |
| **스키마 유효성 검사** | 잘못된 스키마 유효성 검사를 방지하기 위해, <xref:System.Xml.Schema.XmlSchemaSet> 클래스는 XSD 스키마가 일관성 있고 정확하게 컴파일되도록 합니다. 이러한 스키마는 다른 스키마를 포함할 수 있습니다. 예를 들어 `A.xsd`는 `C.xsd`를 포함할 수 있는 `B.xsd`를 포함할 수 있습니다. 이들 중 하나를 컴파일하면 이 의존성 그래프가 트래버스됩니다. |
| **스크립트 함수** | 함수가 실제로 사용 가능할 때 [function-available 함수](https://msdn.microsoft.com/library/ms256124(v=vs.110).aspx)는 더 이상 올바르지 않게 `false`를 반환하지 않습니다. |
| **URI** | <xref:System.Xml.Linq.XElement.Load%2A> 메서드는 이제 LINQ 쿼리에서 올바른 BaseURI를 반환합니다. |

### <a name="validation"></a>유효성 검사

네임스페이스: <xref:System.Xml.Linq>, <xref:System.Xml.Schema>, <xref:System.Xml.XPath>; 어셈블리: System.Xml(System.Xml.dll의), System.Xml.Linq(System.Xml.Linq.dll의)

| 기능 | 3\.5 SP1과의 차이점 |
| ------- | ------------------------ |
| **네임스페이스 확인자** | <xref:System.Xml.XmlReader.ReadContentAs%2A> 메서드는 더 이상 전달된 <xref:System.Xml.IXmlNamespaceResolver> 확인자를 무시하지 않습니다.<br><br>이전 버전에서는 지정된 네임스페이스 확인자가 무시되고 대신 <xref:System.Xml.XmlReader>가 사용되었습니다. |
| **공백** | 판독기를 만들 때 데이터 손실을 방지하기 위해 <xref:System.Xml.XmlReader.Create%2A> 메서드는 더 이상 유효한 공백을 삭제하지 않습니다.<br><br>XML 유효성 검사는 텍스트가 XML 태그와 혼합될 수 있는 혼합 콘텐츠 모드를 인식합니다. 혼합 모드에서는 모든 공백이 유효하므로 보고되어야 합니다. |

### <a name="writing"></a>쓰기

네임스페이스: <xref:System.Xml.Linq>, <xref:System.Xml.Schema>, <xref:System.Xml.XPath>; 어셈블리: System.Xml(System.Xml.dll의), System.Xml.Linq(System.Xml.Linq.dll의)

| 기능 | 3\.5 SP1과의 차이점 |
| ------- | ------------------------ |
| **엔터티 참조** | 데이터 손상을 방지하기 위해, 엔터티 참조가 더 이상 XML 특성에서 두 번 엔터티화되지 않습니다.<br><br>사용자가 엔터티를 `xmlns` 특성에 쓰려고 하거나 <xref:System.Xml.XmlWriter.WriteEntityRef%2A> 메서드를 사용하여 `xml:lang` 또는 `xml:space` 특성에 쓰려고 하면, 엔터티가 출력에서 두 번 엔터티화되어 데이터가 손상됩니다. |
| **줄 바꿈 처리** | 데이터 손상을 방지하기 위해 <xref:System.Xml.XmlWriter> 개체가 <xref:System.Xml.NewLineHandling> 옵션을 존중합니다. |

## <a name="see-also"></a>참고 항목

- [.NET Framework 4의 새 형식 및 멤버](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ff641764%28v=vs.100%29)
- [.NET Framework 4 마이그레이션 가이드](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ff657133%28v=vs.100%29)
- [.NET Framework 4의 새로운 기능](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms171868%28v=vs.100%29)
- [.NET Framework의 버전 호환성](version-compatibility.md)
- [.NET Framework 4로 Office 솔루션 마이그레이션](/visualstudio/vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later)
- [.NET Framework 클래스 라이브러리의 사용되지 않는 기능](../whats-new/whats-obsolete.md)
