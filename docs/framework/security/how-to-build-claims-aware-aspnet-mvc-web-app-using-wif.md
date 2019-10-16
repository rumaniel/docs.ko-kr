---
title: '방법: WIF를 사용하여 클레임 인식 ASP.NET MVC 웹 애플리케이션 빌드'
ms.date: 03/30/2017
ms.assetid: 0efb76bc-9f7b-4afe-be1c-2a57c917010b
author: BrucePerlerMS
ms.openlocfilehash: 4d245288b04d8ed3d997bc5572b40c7f8a9334e5
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045444"
---
# <a name="how-to-build-claims-aware-aspnet-mvc-web-application-using-wif"></a>방법: WIF를 사용하여 클레임 인식 ASP.NET MVC 웹 애플리케이션 빌드
## <a name="applies-to"></a>적용 대상  
  
- Microsoft® Windows® Identity Foundation(WIF)  
  
- ASP.NET® MVC  
  
## <a name="summary"></a>요약  
 이 방법은 간단한 클레임 인식 ASP.NET MVC 웹 애플리케이션을 만들기 위한 자세한 단계별 프로시저를 제공합니다. 또한 클레임 기반 인증을 성공적으로 구현하기 위해 간단한 클레임 인식 ASP.NET MVC 웹 애플리케이션을 테스트하는 방법에 대한 지침을 제공합니다. 이 방법에 STS(보안 토큰 서비스)를 만들기 위한 자세한 지침은 없으며, STS를 이미 구성했다고 가정합니다.  
  
## <a name="contents"></a>목차  
  
- 목표  
  
- 단계 요약  
  
- 1단계 – 간단한 ASP.NET MVC 애플리케이션 만들기  
  
- 2단계 – 클레임 기반 인증에 대한 ASP.NET MVC 애플리케이션 구성  
  
- 3단계 - 솔루션 테스트  
  
- 관련 항목  
  
## <a name="objectives"></a>목표  
  
- 클레임 기반 인증에 대한 ASP.NET MVC 웹 애플리케이션 구성  
  
- 성공적인 클레임 인식 ASP.NET MVC 웹 애플리케이션 테스트  
  
## <a name="summary-of-steps"></a>단계 요약  
  
- 1단계 – 간단한 ASP.NET MVC 애플리케이션 만들기  
  
- 2단계 – 클레임 기반 인증에 대한 ASP.NET MVC 애플리케이션 구성  
  
- 3단계 - 솔루션 테스트  
  
## <a name="step-1--create-simple-aspnet-mvc-application"></a>1단계 – 간단한 ASP.NET MVC 애플리케이션 만들기  
 이 단계에서는 새로운 ASP.NET MVC 애플리케이션을 만듭니다.  
  
#### <a name="to-create-simple-aspnet-mvc-application"></a>간단한 ASP.NET MVC 애플리케이션을 만들려면  
  
1. Visual Studio를 시작하고 **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭합니다.  
  
2. **새 프로젝트** 창에서 **ASP.NET MVC 3 웹 응용 프로그램**을 클릭합니다.  
  
3. **이름**에서 `TestApp`을 입력하고 **확인**을 누릅니다.  
  
4. **새 ASP.NET MVC 3 프로젝트** 대화 상자에서 사용 가능한 템플릿 중에 **인터넷 응용 프로그램**을 선택하고, **뷰 엔진**이 **Razor**로 설정되어 있는지 확인하고 나서, **확인**을 클릭합니다.  
  
5. 새 프로젝트가 열리면 **솔루션 탐색기**에서 **TestApp**을 마우스 오른쪽 단추로 클릭하고 **속성** 옵션을 선택합니다.  
  
6. 프로젝트 속성 페이지에서 왼쪽에 있는 **웹** 탭을 클릭하고 **로컬 IIS 웹 서버 사용** 옵션이 선택되어 있는지 확인합니다.  
  
## <a name="step-2--configure-aspnet-mvc-application-for-claims-based-authentication"></a>2단계 – 클레임 기반 인증에 대한 ASP.NET MVC 애플리케이션 구성  
 이 단계에서는 ASP.NET MVC 웹 애플리케이션의 *Web.config* 구성 파일에 구성 항목을 추가하여 클레임을 인식하도록 설정합니다.  
  
#### <a name="to-configure-aspnet-mvc-application-for-claims-based-authentication"></a>클레임 기반 인증에 대한 ASP.NET MVC 애플리케이션을 구성하려면  
  
1. *Web.config* 구성 파일에 다음 구성 섹션 정의를 추가합니다. 이를 통해 Windows Identity Foundation에 필요한 구성 섹션을 정의합니다. **\<configuration>** 여는 요소 바로 뒤에 정의를 추가합니다.  
  
    ```xml  
    <configSections>  
        <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
        <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    </configSections>  
    ```  
  
2. 응용 프로그램의 페더레이션 메타데이터에 액세스할 수 있는 **\<location>** 요소를 추가합니다.  
  
    ```xml  
    <location path="FederationMetadata">  
        <system.web>  
            <authorization>  
                <allow users="*" />  
            </authorization>  
        </system.web>  
    </location>  
    ```  
  
3. **\<system.web>** 요소 내에 다음 구성 항목을 추가하여 사용자를 거부하고, 기본 인증을 사용하지 않도록 설정하고, WIF로 인증을 관리합니다.  
  
    ```xml  
    <authorization>  
        <deny users="?" />  
    </authorization>  
    <authentication mode="None" />  
    ```  
  
4. 다음 Windows Identity Foundation 관련 구성 항목을 추가하고 ASP.NET 응용 프로그램의 URL 및 포트 번호가 **\<audienceUris>** 항목, **\<wsFederation>** 요소의 **realm** 특성 및 **\<wsFederation>** 요소의 **reply** 특성 값과 일치하는지 확인합니다. 또한 **issuer** 값이 STS(보안 토큰 서비스) URL과 일치하는지 확인합니다.  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration>  
            <audienceUris>  
                <add value="http://localhost:28503/" />  
            </audienceUris>  
            <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
                <trustedIssuers>  
                    <add thumbprint="1234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ1234" name="YourSTSName" />  
                </trustedIssuers>   
            </issuerNameRegistry>  
            <certificateValidation certificateValidationMode="None" />  
        </identityConfiguration>  
    </system.identityModel>  
    <system.identityModel.services>  
        <federationConfiguration>  
            <cookieHandler requireSsl="false" />  
            <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:13922/wsFederationSTS/Issue" realm="http://localhost:28503/" reply="http://localhost:28503/" requireHttps="false" />  
        </federationConfiguration>  
    </system.identityModel.services>  
    ```  
  
5. <xref:System.IdentityModel> 어셈블리에 대한 참조를 추가합니다.  
  
6. 솔루션을 컴파일하여 오류가 있는지 확인합니다.  
  
## <a name="step-3--test-your-solution"></a>3단계 - 솔루션 테스트  
 이 단계에서는 클레임 기반 인증에 대해 구성된 ASP.NET MVC 웹 애플리케이션을 테스트합니다. 기본 테스트를 수행하려면 STS(보안 토큰 서비스)에서 발급된 토큰에 클레임을 표시하는 간단한 코드를 추가합니다.  
  
#### <a name="to-test-your-aspnet-mvc-application-for-claims-based-authentication"></a>클레임 기반 인증에 대한 ASP.NET MVC 애플리케이션을 테스트하려면  
  
1. **솔루션 탐색기**에서 **컨트롤러** 폴더를 확장하고 편집기에서 *HomeController.cs* 파일을 엽니다. **Index** 메서드에 다음 코드를 추가합니다.  
  
    ```csharp  
    public ActionResult Index()  
    {  
        ViewBag.ClaimsIdentity = Thread.CurrentPrincipal.Identity;  
  
        return View();  
    }  
    ```  
  
2. **솔루션 탐색기**에서 **뷰**, **홈** 폴더를 차례로 확장하고, 편집기에서 *Index.cshtml* 파일을 엽니다. 콘텐츠를 삭제하고 다음 태그를 추가합니다.  
  
    ```html  
    @{  
        ViewBag.Title = "Home Page";  
    }  
  
    <h2>Welcome: @ViewBag.ClaimsIdentity.Name</h2>  
    <h3>Values from Identity</h3>  
    <table>  
        <tr>  
            <th>  
                IsAuthenticated   
            </th>  
            <td>  
                @ViewBag.ClaimsIdentity.IsAuthenticated   
            </td>  
        </tr>  
        <tr>  
            <th>  
                Name   
            </th>          
            <td>  
                @ViewBag.ClaimsIdentity.Name  
            </td>          
        </tr>  
    </table>  
    <h3>Claims from ClaimsIdentity</h3>  
    <table>  
        <tr>  
            <th>  
                Claim Type  
            </th>  
            <th>  
                Claim Value  
            </th>  
            <th>  
                Value Type  
            </th>  
            <th>  
                Subject Name  
            </th>          
            <th>  
                Issuer Name  
            </th>          
        </tr>  
            @foreach (System.Security.Claims.Claim claim in ViewBag.ClaimsIdentity.Claims ) {  
        <tr>  
            <td>  
                @claim.Type  
            </td>  
            <td>  
                @claim.Value  
            </td>  
            <td>  
                @claim.ValueType  
            </td>  
            <td>  
                @claim.Subject.Name  
            </td>  
            <td>  
                @claim.Issuer  
            </td>  
        </tr>  
    }  
    </table>  
    ```  
  
3. **F5** 키를 눌러 솔루션을 실행합니다.  
  
4. STS(보안 토큰 서비스)에서 발급된 토큰에 클레임을 표시하는 페이지가 표시되어야 합니다.  
  
## <a name="related-items"></a>관련 항목  
  
- [방법: WIF를 사용 하 여 클레임 인식 ASP.NET Web Forms 응용 프로그램 빌드](how-to-build-claims-aware-aspnet-web-forms-app-using-wif.md)
