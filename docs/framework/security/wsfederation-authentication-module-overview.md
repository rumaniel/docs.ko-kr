---
title: WSFederation 인증 모듈 개요
ms.date: 03/30/2017
ms.assetid: 02c4d5e8-f0a7-49ee-9cf5-3647578510ad
author: BrucePerlerMS
ms.openlocfilehash: 26cd022ded8dddcfcf695c89b3cf4b90d3ceb2ef
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044943"
---
# <a name="wsfederation-authentication-module-overview"></a>WSFederation 인증 모듈 개요
WIF(Windows Identity Foundation)에는 WS-FAM( WS-Federated Authentication Module)을 통한 ASP.NET 애플리케이션의 페더레이션된 인증 지원이 포함되어 있습니다. 이 항목은 페더레이션된 인증의 작동 방식과 사용 방법을 이해하는 데 도움이 됩니다.  
  
### <a name="overview-of-federated-authentication"></a>페더레이션된 인증 개요  
 페더레이션된 인증을 사용하면 두 도메인 간에 트러스트 관계가 있는 경우 한 트러스트 도메인의 STS(보안 토큰 서비스)에서 다른 트러스트 도메인의 STS에 인증 정보를 제공할 수 있습니다. 이에 대 한 예는 다음 그림에 나와 있습니다.  
  
 ![페더레이션된 인증 시나리오를 보여 주는 다이어그램](./media/wsfederation-authentication-module-overview/federated-authentication.gif)  
  
1. Fabrikam 트러스트 도메인의 클라이언트는 Contoso 트러스트 도메인의 RP(신뢰 당사자) 애플리케이션에 요청을 보냅니다.  
  
2. RP는 클라이언트를 Contoso 트러스트 도메인의 STS로 리디렉션합니다. 이 STS는 클라이언트를 알지 못합니다.  
  
3. Contoso STS는 Contoso 트러스트 도메인과 트러스트 관계가 있는 Fabrikam 트러스트 도메인의 STS에 클라이언트를 리디렉션합니다.  
  
4. Fabrikam STS는 클라이언트의 ID를 확인하고 Contoso STS에 보안 토큰을 발급합니다.  
  
5. Contoso STS는 Fabrikam 토큰을 사용하여 RP에서 사용할 수 있는 자체 토큰을 만들어 RP에 전송합니다.  
  
6. RP는 보안 토큰에서 클라이언트의 클레임을 추출하고 권한 부여를 결정합니다.  
  
### <a name="using-the-federated-authentication-module-with-aspnet"></a>ASP.NET과 함께 페더레이션된 인증 모듈 사용  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>(WS-FEDERATION)는 ASP.NET 응용 프로그램에 페더레이션된 인증을 추가할 수 있는 HTTP 모듈입니다. 페더레이션된 인증을 사용하면 STS를 통해 인증 논리를 처리하고 비즈니스 논리 작성에 집중할 수 있습니다.  
  
 인증되지 않은 요청을 리디렉션할 STS를 지정하려면 WS-FAM을 구성합니다. WIF에서는 다음 두 가지 방법으로 사용자를 인증할 수 있습니다.  
  
1. 수동 리디렉션: 인증 되지 않은 사용자가 보호 된 리소스에 액세스 하려고 시도 하는 경우 로그인 페이지가 없어도 STS로 리디렉션하는 것이 적절 한 방법입니다. STS는 사용자의 ID를 확인하고 해당 사용자에 대한 적절한 클레임을 포함하는 보안 토큰을 발급합니다. 이 옵션을 사용할 경우 HTTP 모듈 파이프라인에 WS-FAM을 추가해야 합니다. Visual Studio 2012용 ID 및 액세스 도구를 통해 WS-FAM을 사용하고 STS와 페더레이션하도록 애플리케이션의 구성 파일을 수정할 수 있습니다. 자세한 내용은 [Visual Studio 2012용 ID 및 액세스 도구](identity-and-access-tool-for-vs.md)를 참조하세요.  
  
2. RP 애플리케이션의 로그인 페이지에 대한 코드 숨김에서 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SignIn%2A?displayProperty=nameWithType> 메서드 또는 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectToIdentityProvider%2A> 메서드를 호출할 수 있습니다.  
  
 수동 리디렉션에서는 모든 통신이 클라이언트(일반적으로 브라우저)의 응답/리디렉션을 통해 수행됩니다. 애플리케이션의 HTTP 파이프라인에 WS-FAM을 추가할 수 있습니다. 여기서 인증되지 않은 사용자 요청을 감시하고 사용자를 지정한 STS로 리디렉션합니다.  
  
 또한 ASP.NET 응용 프로그램에서 해당 기능을 사용자 지정할 수 있는 여러 이벤트를 발생 시킵니다.  
  
### <a name="how-the-ws-fam-works"></a>WS-FAM의 작동 방식  
 WS-FAM은 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 클래스에서 구현됩니다. 일반적으로 ASP.NET RP 응용 프로그램의 HTTP 파이프라인에 WS FAM을 추가 합니다. 인증되지 않은 사용자가 보호된 리소스에 액세스하려고 하면 RP가 “401 인증이 거부되었습니다.”라는 HTTP 응답을 반환합니다. WS-FAM은 클라이언트의 수신을 허용하는 대신 이 응답을 가로챈 다음 사용자를 지정된 STS로 리디렉션합니다. STS가 보안 토큰을 발급하고, WS-FAM이 이 토큰을 다시 가로챕니다. Ws-atomictransaction은 토큰을 사용 하 여 인증 된 사용자에 대 한 <xref:System.Security.Claims.ClaimsPrincipal> 의 인스턴스를 만듭니다 .이를 통해 일반 .NET Framework 권한 부여 메커니즘이 작동할 수 있습니다.  
  
 HTTP는 상태 비저장이므로 사용자가 다른 보호된 리소스에 액세스를 시도할 때마다 이 전체 프로세스를 반복하지 않을 방법이 필요합니다. <xref:System.IdentityModel.Services.SessionAuthenticationModule>이 필요한 이유가 바로 여기에 있습니다. STS가 사용자에 대한 보안 토큰을 발급할 때 <xref:System.IdentityModel.Services.SessionAuthenticationModule>에서도 사용자에 대한 세션 보안 토큰을 만들어 쿠키에 저장합니다. 후속 요청 시 <xref:System.IdentityModel.Services.SessionAuthenticationModule>은 이 쿠키를 가로챈 다음 사용해서 사용자의 <xref:System.Security.Claims.ClaimsPrincipal>을 다시 구성합니다.  
  
 다음 다이어그램은 수동 리디렉션 사례에서 정보의 전반적인 흐름을 보여 줍니다. STS를 통해 요청이 자동으로 리디렉션되어 로그인 페이지 없이 자격 증명을 설정합니다.  
  
 ![수동 리디렉션을 사용한 로그인을 보여 주는 다이어그램입니다.](./media/wsfederation-authentication-module-overview/sign-in-using-passive-redirect.gif)  
  
 다음 다이어그램은 사용자가 STS에 인증했으며 해당 보안 토큰이 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>에 의해 처리될 때 발생하는 사항을 자세히 보여 줍니다.  
  
 ![수동 리디렉션을 사용한 토큰 처리 타이밍](./media/signinusingpassiveredirect-tokenprocessing.gif "SignInUsingPassiveRedirect_TokenProcessing")  
  
 다음 다이어그램은 사용자의 보안 토큰이 쿠키로 직렬화되었으며 <xref:System.IdentityModel.Services.SessionAuthenticationModule>에서 가로챌 때 발생하는 사항을 자세히 보여 줍니다.  
  
 ![컨트롤을 사용한 로그인을 보여 주는 SAM 타이밍 다이어그램](./media/signinusingconrols-sam.gif "SignInUsingConrols_SAM")  
  
### <a name="events"></a>이벤트  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule><xref:System.IdentityModel.Services.SessionAuthenticationModule> 및 해당 부모 클래스인 <xref:System.IdentityModel.Services.HttpModuleBase>는 HTTP 요청의 여러 처리 단계에서 이벤트를 발생시킵니다. ASP.NET 응용 프로그램의 `global.asax` 파일에서 이러한 이벤트를 처리할 수 있습니다.  
  
- ASP.NET 인프라는 모듈의 <xref:System.IdentityModel.Services.HttpModuleBase.Init%2A> 메서드를 호출하여 모듈을 초기화합니다.  
  
- ASP.NET 인프라가 <xref:System.IdentityModel.Services.HttpModuleBase>에서 파생되는 애플리케이션의 모듈 중 하나에서 <xref:System.IdentityModel.Services.HttpModuleBase.Init%2A> 메서드를 처음 호출할 때 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfigurationCreated?displayProperty=nameWithType> 이벤트가 발생합니다. 이 메서드는 정적 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType> 속성에 액세스하여 Web.config 파일에서 구성이 로드되도록 합니다. 이 이벤트는 이 속성에 처음 액세스할 때만 발생합니다. 구성에서 초기화된 <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> 개체는 이벤트 처리기의 <xref:System.IdentityModel.Services.Configuration.FederationConfigurationCreatedEventArgs.FederationConfiguration%2A?displayProperty=nameWithType> 속성을 통해 액세스할 수 있습니다. 이 이벤트를 사용하여 모듈에 적용되기 전에 구성을 수정할 수 있습니다. Application_Start 메서드에 이 이벤트에 대한 처리기를 추가할 수 있습니다.  
  
    ```csharp
    void Application_Start(object sender, EventArgs e)  
    {  
        FederatedAuthentication.FederationConfigurationCreated += new EventHandler<FederationConfigurationCreatedEventArgs>(FederatedAuthentication_FederationConfigurationCreated);  
    }  
    ```  
  
     각 모듈은 <xref:System.IdentityModel.Services.HttpModuleBase.InitializeModule%2A?displayProperty=nameWithType> 및 <xref:System.IdentityModel.Services.HttpModuleBase.InitializePropertiesFromConfiguration%2A?displayProperty=nameWithType> 추상 메서드를 재정의합니다. 첫 번째 메서드는 모듈에 관련된 ASP.NET 파이프라인 이벤트에 대한 처리기를 추가합니다. 대부분의 경우 모듈의 기본 구현만으로 충분합니다. 두 번째 메서드는 해당 <xref:System.IdentityModel.Services.HttpModuleBase.FederationConfiguration%2A?displayProperty=nameWithType> 속성에서 모듈의 속성을 초기화합니다. 이전에 로드된 구성의 복사본입니다. <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 또는 <xref:System.IdentityModel.Services.SessionAuthenticationModule>에서 파생하는 클래스의 구성에서 새 속성의 초기화를 지원하려는 경우 이 두 번째 메서드를 재정의해야 할 수도 있습니다. 이러한 경우 <xref:System.IdentityModel.Configuration.IdentityConfiguration>, <xref:System.IdentityModel.Services.Configuration.WsFederationConfiguration> 또는 <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> 등에서 추가된 구성 속성을 지원하기 위해 적절한 구성 개체에서 파생해야 합니다.  
  
- WS-FAM은 STS에서 발급된 보안 토큰을 가로챌 때 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SecurityTokenReceived> 이벤트를 발생시킵니다.  
  
- WS-FAM은 토큰의 유효성을 검사한 후 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SecurityTokenValidated> 이벤트를 발생시킵니다.  
  
- <xref:System.IdentityModel.Services.SessionAuthenticationModule> 모듈은 사용자에 대한 세션 보안 토큰을 만들 때 <xref:System.IdentityModel.Services.SessionAuthenticationModule.SessionSecurityTokenCreated> 이벤트를 발생시킵니다.  
  
- <xref:System.IdentityModel.Services.SessionAuthenticationModule>은 세션 보안 토큰을 포함하는 쿠키를 사용하여 후속 요청을 가로챌 때 <xref:System.IdentityModel.Services.SessionAuthenticationModule.SessionSecurityTokenReceived> 이벤트를 발생시킵니다.  
  
- WS-FAM은 사용자를 발급자로 리디렉션하기 전에 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider> 이벤트를 발생시킵니다. WS-Federation 로그인 요청은 이벤트에 전달된 <xref:System.IdentityModel.Services.RedirectingToIdentityProviderEventArgs>의 <xref:System.IdentityModel.Services.RedirectingToIdentityProviderEventArgs.SignInRequestMessage%2A> 속성을 통해 사용할 수 있습니다. 이 요청을 발급자에게 보내기 전에 수정할 수 있습니다.  
  
- 쿠키가 성공적으로 작성되고 사용자가 로그인하면 WS-FAM이 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SignedIn>을 발생시킵니다.  
  
- 각 사용자에 대해 세션이 닫히기 때문에 WS-FAM은 세션당 한 번 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SigningOut> 이벤트를 발생시킵니다. 클라이언트 쪽에서 세션이 닫힌 경우(예: 세션 쿠키 삭제)에는 이벤트가 발생하지 않습니다. SSO 환경에서는 IP-STS가 각 RP에 로그아웃하도록 요청할 수도 있습니다. 이 경우에도 <xref:System.IdentityModel.Services.SigningOutEventArgs.IsIPInitiated%2A>가 `true`로 설정되어 이 이벤트가 발생합니다.  
  
> [!NOTE]
> <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 또는 <xref:System.IdentityModel.Services.SessionAuthenticationModule>에서 발생하는 이벤트 중에는 <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=nameWithType> 속성을 사용하면 안 됩니다. 이는 인증 프로세스 중 이벤트가 발생하는 반면 <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=nameWithType>은 인증 프로세스 후에 설정되기 때문입니다.  
  
### <a name="configuration-of-federated-authentication"></a>페더레이션된 인증 구성  
 WS-FAM 및 SAM은 [\<federationConfiguration>](../configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) 요소를 통해 구성됩니다. [\<wsFederation>](../configure-apps/file-schema/windows-identity-foundation/wsfederation.md) 자식 요소는 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.Issuer%2A> 속성 및 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.Realm%2A> 속성 같은 WS-FAM 속성의 기본값을 구성합니다. 일부 WS-FAM 이벤트(예: <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider>)에 대한 처리기를 제공하여 요청별로 이러한 값을 변경할 수 있습니다. SAM에서 사용되는 쿠키 처리기는 [\<cookieHandler>](../configure-apps/file-schema/windows-identity-foundation/cookiehandler.md) 자식 요소를 통해 구성됩니다. WIF는 <xref:System.IdentityModel.Services.ChunkedCookieHandler> 클래스에 구현된 기본 쿠키 처리기를 제공하며, [\<chunkedCookieHandler>](../configure-apps/file-schema/windows-identity-foundation/chunkedcookiehandler.md) 요소를 통해 해당 청크 크기를 설정할 수 있습니다. `<federationConfiguration>` 요소는 <xref:System.Security.Claims.ClaimsAuthenticationManager>, <xref:System.Security.Claims.ClaimsAuthorizationManager> 등 응용 프로그램에서 사용되는 다른 WIF 구성 요소에 대한 구성을 제공하는 <xref:System.IdentityModel.Configuration.IdentityConfiguration>을 참조합니다. `<federationConfiguration>` 요소의 `identityConfigurationName` 특성에 명명된 [\<identityConfiguration>](../configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 요소를 지정하여 ID 구성을 명시적으로 참조할 수 있습니다. ID 구성이 명시적으로 참조되지 않은 경우 기본 ID 구성이 사용됩니다.  
  
 다음 XML에서는 ASP.NET RP(신뢰 당사자) 애플리케이션의 구성을 보여 줍니다. <xref:System.IdentityModel.Configuration.SystemIdentityModelSection> 및 <xref:System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection> 구성 섹션은 `<configSections>` 요소 아래에 추가됩니다. SAM 및 WS-FAM은 HTTP 모듈의 `<system.webServer>`/`<modules>` 요소 아래에 추가됩니다. 최종적으로, WIF 구성 요소는 `<system.identityModel>`/`<identityConfiguration>` 및 `<system.identityModel.services>`/`<federationConfiguration>` 요소 아래에 구성됩니다. 이 구성은 기본 쿠키 처리기이고 `<cookieHandler>` 요소에 지정된 쿠키 처리기 유형이 없기 때문에 청크 분할된 쿠키 처리기를 지정합니다.  
  
> [!WARNING]
> 다음 예제에서 `<wsFederation>` 요소의 `requireHttps` 특성과 `<cookieHandler>` 요소의 `requireSsl` 특성은 둘 다 `false`입니다. 이 경우 보안 위협이 발생할 수 있습니다. 프로덕션에서는 이러한 두 값을 모두 `true`로 설정해야 합니다.  
  
```xml  
<configuration>  
  <configSections>  
    <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
  </configSections>  
  
  ...  
  
  <system.webServer>  
    <modules>  
      <add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
      <add name="SessionAuthenticationModule" type="System.IdentityModel.Services.SessionAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
    </modules>  
  </system.webServer>  
  
  <system.identityModel>  
    <identityConfiguration>  
      <audienceUris>  
        <add value="http://localhost:50969/" />  
      </audienceUris>  
      <certificateValidation certificateValidationMode="None" />  
      <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
        <trustedIssuers>  
          <add thumbprint="9B74CB2F320F7AAFC156E1252270B1DC01EF40D0" name="LocalSTS" />  
        </trustedIssuers>  
      </issuerNameRegistry>  
    </identityConfiguration>  
  </system.identityModel>  
  <system.identityModel.services>  
    <federationConfiguration>  
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:15839/wsFederationSTS/Issue" realm="http://localhost:50969/" reply="http://localhost:50969/" requireHttps="false" />  
      <cookieHandler requireSsl="false" />  
    </federationConfiguration>  
  </system.identityModel.services>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Services.SessionAuthenticationModule>
- <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>
- [\<federationConfiguration>](../configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)
