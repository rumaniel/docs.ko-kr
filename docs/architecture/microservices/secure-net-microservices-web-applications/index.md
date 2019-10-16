---
title: .NET 마이크로 서비스 및 웹 애플리케이션 보안
description: .NET 마이크로 서비스 및 웹 애플리케이션 보안 - ASP.NET Core 웹 애플리케이션의 인증 옵션을 살펴봅니다.
author: mjrousos
ms.author: wiwagn
ms.date: 10/19/2018
ms.openlocfilehash: 0894465858e3503e2eddb5299b404f7ba95fdd6a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295206"
---
# <a name="make-secure-net-microservices-and-web-applications"></a>.NET 마이크로 서비스 및 웹 애플리케이션 보안

항목에서는 이와 같은 여러 설명서를 쉽게 사용할 수 있는 마이크로 서비스 및 웹 애플리케이션의 보안에 대한 많은 측면이 있으므로 이 섹션에서는 인증, 권한 및 애플리케이션 비밀에 집중하도록 하겠습니다.

## <a name="implement-authentication-in-net-microservices-and-web-applications"></a>.NET 마이크로 서비스 및 웹 애플리케이션의 인증 구현

서비스에서 게시된 리소스 및 API는 종종 특정 신뢰할 수 있는 사용자 또는 클라이언트로 제한되어야 합니다. 이러한 API 수준 신뢰 결정을 만드는 첫 번째 단계는 인증입니다. 인증은 사용자의 ID를 안정적으로 확인하는 프로세스입니다.

마이크로 서비스 시나리오에서 일반적으로 인증은 중앙에서 처리됩니다. API 게이트웨이를 사용하는 경우 그림 9-1에 표시된 것처럼 게이트웨이는 인증에 적합한 위치입니다. 이 방법을 사용하는 경우 메시지를 인증하는 데 추가 보안을 사용하지 않는 한 (API 게이트웨이 없이) 개별 마이크로 서비스에 직접 연결할 수 없습니다. 인증하는 메시지의 출처는 반드시 게이트웨이가 아니어도 무방합니다.

![API 게이트웨이는 인증을 중앙 집중 방식으로 관리하는 경우 마이크로 서비스에 요청을 전달할 때 사용자 정보를 추가합니다.](./media/image1.png)

**그림 9-1**. API 게이트웨이를 통한 중앙 집중식 인증

서비스에 직접 액세스할 수 있는 경우 Azure Active Directory 또는 STS(보안 토큰 서비스)로 작동하는 전용 인증 마이크로 서비스와 같은 인증 서비스를 사용하여 사용자를 인증할 수 있습니다. 신뢰 결정은 보안 토큰 또는 쿠키를 통해 서비스 간에 공유됩니다. (필요한 경우 [쿠키 공유](/aspnet/core/security/cookie-sharing)를 구현하여 이러한 토큰을 ASP.NET Core 애플리케이션 간에 공유할 수 있습니다.) 그림 9-2에서는 이 패턴을 보여줍니다.

![마이크로 서비스에 직접 액세스하는 경우 인증 및 권한 부여를 포함하는 트러스트는 마이크로 서비스 간에 공유되고, 전용 마이크로 서비스에서 발급한 보안 토큰에서 처리됩니다.](./media/image2.png)

**그림9-2** ID 마이크로 서비스에 의한 인증. 인증 토큰을 사용하여 신뢰가 공유됨

### <a name="authenticate-with-aspnet-core-identity"></a>ASP.NET Core ID를 사용한 인증

애플리케이션의 사용자를 식별하기 위한 ASP.NET Core의 기본 메커니즘은 [ASP.NET Core ID](/aspnet/core/security/authentication/identity) 멤버 자격 시스템입니다. ASP.NET ID는 사용자 정보(로그인 정보, 역할 및 클레임 포함)를 개발자가 구성한 데이터 저장소에 저장합니다. 일반적으로 ASP.NET Core ID 데이터 저장소는 `Microsoft.AspNetCore.Identity.EntityFrameworkCore` 패키지에서 제공된 Entity Framework 저장소입니다. 그러나 사용자 지정 저장소 또는 타사 패키지를 사용하여 Azure Table Storage, CosmosDB 또는 다른 위치에 ID 정보를 저장할 수 있습니다.

다음은 선택된 개별 사용자 계정 인증을 사용하여 ASP.NET Core 웹 애플리케이션 프로젝트 템플릿에서 가져온 코드입니다. Startup.ConfigureServices 메서드에서 EntityFramework.Core를 사용하여 ASP.NET Core ID를 구성하는 방법을 보여 줍니다.

```csharp
services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();
```

ASP.NET Core ID가 구성되면 서비스의 `Startup.Configure` 메서드에서 app.UseIdentity를 호출하여 사용할 수 있습니다.

ASP.NET Core ID를 통해 다음과 같은 몇 가지 시나리오를 사용할 수 있습니다.

- UserManager 형식(userManager.CreateAsync)을 사용하여 새 사용자 정보를 만듭니다.

- SignInManager 형식을 사용하여 사용자를 인증합니다. 직접 로그인하려면 `signInManager.SignInAsync`를 사용하거나, 사용자의 암호가 올바른지 확인한 다음, 로그인하려면 `signInManager.PasswordSignInAsync`를 사용할 수 있습니다.

- 브라우저의 후속 요청에 로그인한 사용자의 ID와 클레임이 포함되도록 (ASP.NET Core ID 미들웨어에서 읽는) 쿠키에 저장된 정보를 기반으로 사용자를 식별합니다.

ASP.NET Core ID도 [2단계 인증](/aspnet/core/security/authentication/2fa)을 지원합니다.

ASP.NET Core ID는 로컬 사용자 데이터 저장소를 사용하며 (MVC 웹 애플리케이션에서는 전형적인 방식인) 쿠키를 사용하여 요청 사이의 ID를 유지하는 인증 시나리오를 위해 권장되는 솔루션입니다.

### <a name="authenticate-with-external-providers"></a>외부 공급자를 사용한 인증

ASP.NET Core는 [외부 인증 공급자](/aspnet/core/security/authentication/social/)를 사용하여 사용자가 [OAuth 2.0](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2) 흐름을 통해 로그인할 수 있도록 지원합니다. 즉, 사용자가 Microsoft, Google, Facebook 또는 Twitter와 같은 공급 기업의 기존 인증 프로세스를 사용하여 로그인하고 애플리케이션에서 ASP.NET Core ID와 해당 ID를 연결할 수 있습니다.

외부 인증을 사용하려면 애플리케이션의 HTTP 요청 처리 파이프라인에서 적절한 인증 미들웨어를 포함합니다. 이 미들웨어는 인증 공급자의 URI 경로 반환 요청 처리, ID 정보 캡처, SignInManager.GetExternalLoginInfo 메서드를 통해 사용 가능하도록 설정하는 작업을 담당합니다.

인기 있는 외부 인증 공급 기업 및 해당 공급 기업과 연결된 NuGet 패키지는 다음 표에 표시됩니다.

| **공급 기업**  | **패키지**                                          |
| ------------- | ---------------------------------------------------- |
| **Microsoft** | **Microsoft.AspNetCore.Authentication.MicrosoftAccount** |
| **Google**    | **Microsoft.AspNetCore.Authentication.Google**           |
| **Facebook**  | **Microsoft.AspNetCore.Authentication.Facebook**         |
| **Twitter**   | **Microsoft.AspNetCore.Authentication.Twitter**          |

모든 경우에 미들웨어는 `Startup.Configure`의 `app.Use{ExternalProvider}Authentication`과 유사한 등록 메서드에 대한 호출에 등록됩니다. 이러한 등록 메서드에서는 공급자의 필요에 따라 애플리케이션 ID 및 비밀 정보(예: 암호)가 포함된 옵션 개체를 사용합니다. 외부 인증 공급자는 사용자 ID에 액세스하는 데 필요한 애플리케이션을 사용자에게 안내하기 위해 ([ASP.NET Core 설명서](/aspnet/core/security/authentication/social/)에서 설명한 것처럼) 등록할 애플리케이션을 요청합니다.

미들웨어가 `Startup.Configure`에 등록되면 모든 컨트롤러 작업에서 사용자에게 로그인을 요청할 수 있습니다. 이 작업을 수행하려면 인증 공급 기업의 이름 및 리디렉션 URL을 포함하는 `AuthenticationProperties` 개체를 만듭니다. 그런 다음, `AuthenticationProperties` 개체를 전달하는 챌린지 응답을 반환합니다. 다음 코드에서는 예제를 보여 줍니다.

```csharp
var properties = _signInManager.ConfigureExternalAuthenticationProperties(provider,
    redirectUrl);
return Challenge(properties, provider);
```

redirectUrl 매개 변수는 사용자가 인증되면 외부 공급자가 리디렉션해야 하는 URL을 포함합니다. URL은 다음 단순화된 예제와 같이 외부 ID 정보를 기반으로 사용자가 로그인하는 작업을 나타내야 합니다.

```csharp
// Sign in the user with this external login provider if the user
// already has a login.
var result = await _signInManager.ExternalLoginSignInAsync(info.LoginProvider, info.ProviderKey, isPersistent: false);

if (result.Succeeded)
{
    return RedirectToLocal(returnUrl);
}
else
{
    ApplicationUser newUser = new ApplicationUser
    {
        // The user object can be constructed with claims from the
        // external authentication provider, combined with information
        // supplied by the user after they have authenticated with
        // the external provider.
        UserName = info.Principal.FindFirstValue(ClaimTypes.Name),
        Email = info.Principal.FindFirstValue(ClaimTypes.Email)
    };
    var identityResult = await _userManager.CreateAsync(newUser);
    if (identityResult.Succeeded)
    {
        identityResult = await _userManager.AddLoginAsync(newUser, info);
        if (identityResult.Succeeded)
        {
            await _signInManager.SignInAsync(newUser, isPersistent: false);
        }
        return RedirectToLocal(returnUrl);
    }
}
```

Visual Studio에서 ASP.NET Core 웹 애플리케이션 프로젝트를 만들 때 **개별 사용자 계정** 인증 옵션을 선택한 경우 그림 9-3에 표시된 것처럼 외부 공급 기업을 통해 로그인하는 데 필요한 모든 코드는 이미 프로젝트에 있습니다.

![인증을 변경하는 단추를 강조 표시하는 새 ASP.NET Core 웹 애플리케이션의 대화 상자입니다.](./media/image3.png)

**그림 9-3** 웹 애플리케이션 프로젝트를 만들 경우 외부 인증 사용 옵션 선택

이전에 나열된 외부 인증 공급자뿐만 아니라 더욱 많은 외부 인증 공급자 사용에 대한 미들웨어를 제공하는 타사 패키지도 사용할 수 있습니다. 자세한 목록은 GitHub에서 [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers/tree/dev/src) 리포지토리를 확인하세요.

또한, 몇 가지 특별한 요구를 해결하려면 사용자 고유의 외부 인증 미들웨어를 만들 수 있습니다.

### <a name="authenticate-with-bearer-tokens"></a>전달자 토큰을 사용한 인증

ASP.NET Core ID(또는 ID 및 외부 인증 공급자)를 사용한 인증은 사용자 정보를 쿠키에 저장하는 것이 적합한 다수의 웹 애플리케이션 시나리오에 대해 효과적으로 작동합니다. 그러나 다른 시나리오의 경우 쿠키는 데이터를 유지하고 전송하는 자연스러운 방법이 아닙니다.

예를 들어 SPA(단일 페이지 애플리케이션), 네이티브 클라이언트 또는 다른 웹 API에서 액세스할 수 있는 RESTful 엔드포인트를 노출하는 ASP.NET Core 웹 API에서는 쿠키 대신 일반적으로 전달자 토큰 인증을 사용하는 것이 좋습니다. 이러한 유형의 애플리케이션은 쿠키와는 작동하지 않지만 간편하게 전달자 토큰을 검색하여 후속 요청의 인증 헤더에 포함합니다. 토큰 인증을 사용하기 위해 ASP.NET Core는 [OAuth 2.0](https://oauth.net/2/) 및 [OpenID Connect](https://openid.net/connect/) 사용에 대한 몇 가지 옵션을 지원합니다.

### <a name="authenticate-with-an-openid-connect-or-oauth-20-identity-provider"></a>OpenID Connect 또는 OAuth 2.0 ID 공급 기업을 사용한 인증

사용자 정보가 Azure Active Directory 또는 OpenID Connect 또는 OAuth 2.0을 지원하는 다른 ID 솔루션에 저장되는 경우 **Microsoft.AspNetCore.Authentication.OpenIdConnect** 패키지를 사용하여 OpenID Connect 워크플로를 통해 인증할 수 있습니다. 예를 들어 eShopOnContainers의 Identity.Api 마이크로 서비스에 대해 인증하려면 ASP.NET Core 웹 애플리케이션에서는 `Startup.cs`의 다음 간단한 예제에 표시된 것처럼 해당 패키지의 미들웨어를 사용할 수 있습니다.

```csharp
// Startup.cs

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    //…
    // Configure the pipeline to use authentication
    app.UseAuthentication();
    //…
    app.UseMvc();
}

public void ConfigureServices(IServiceCollection services)
{
    var identityUrl = Configuration.GetValue<string>("IdentityUrl");
    var callBackUrl = Configuration.GetValue<string>("CallBackUrl");

    // Add Authentication services

    services.AddAuthentication(options =>
    {
        options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.DefaultChallengeScheme = OpenIdConnectDefaults.AuthenticationScheme;
    })
    .AddCookie()
    .AddOpenIdConnect(options =>
    {
        options.SignInScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.Authority = identityUrl;
        options.SignedOutRedirectUri = callBackUrl;
        options.ClientSecret = "secret";
        options.SaveTokens = true;
        options.GetClaimsFromUserInfoEndpoint = true;
        options.RequireHttpsMetadata = false;
        options.Scope.Add("openid");
        options.Scope.Add("profile");
        options.Scope.Add("orders");
        options.Scope.Add("basket");
        options.Scope.Add("marketing");
        options.Scope.Add("locations");
        options.Scope.Add("webshoppingagg");
        options.Scope.Add("orders.signalrhub");
    });
}
```

이 워크플로를 사용하면 모든 사용자 정보 스토리지 및 인증이 ID 서비스에서 처리되므로 ASP.NET Core ID 미들웨어가 필요하지 않습니다.

### <a name="issue-security-tokens-from-an-aspnet-core-service"></a>ASP.NET Core 서비스에서 보안 토큰 발급

로컬 ASP.NET Core ID 사용자를 위해 외부 ID 공급자를 사용하는 대신 보안 토큰 발급을 선호하는 경우 일부 훌륭한 타사 라이브러리를 적절하게 활용할 수 있습니다.

[IdentityServer4](https://github.com/IdentityServer/IdentityServer4) 및 [OpenIddict](https://github.com/openiddict/openiddict-core)는 ASP.NET Core ID와 쉽게 통합하여 ASP.NET Core 서비스에서 보안 토큰을 발급할 수 있도록 허용하는 OpenID Connect 공급자입니다. [IdentityServer4 설명서](https://identityserver4.readthedocs.io/en/latest/)에는 라이브러리 사용에 대한 자세한 지침이 있습니다. 그러나 IdentityServer4를 사용하여 토큰을 발급하는 기본 단계는 다음과 같습니다.

1. Startup.Configure 메서드에서 app.UseIdentityServer를 호출하여 IdentityServer4를 애플리케이션의 HTTP 요청 처리 파이프라인에 추가합니다. 이렇게 하면 라이브러리 서버에서 /connect/token과 같은 OpenID Connect 및 OAuth2 엔드포인트에 요청할 수 있습니다.

2. services.AddIdentityServer를 호출하여 Startup.ConfigureServices에서 IdentityServer4를 구성합니다.

3. 다음 데이터를 설정하여 ID 서버를 구성합니다.

   - 서명에 사용할 [자격 증명](https://identityserver4.readthedocs.io/en/latest/topics/crypto.html)

   - 액세스를 위해 사용자가 요청할 수 있는 [ID 및 API 리소스](https://identityserver4.readthedocs.io/en/latest/topics/resources.html)

      - API 리소스는 사용자가 액세스 토큰을 사용하여 액세스할 수 있는 보호된 데이터 또는 기능을 나타냅니다. 웹 API 리소스의 예로는 권한 부여가 필요한 웹 API(또는 API 집합)가 있습니다.

      - ID 리소스는 사용자를 식별하기 위해 클라이언트에게 제공되는 정보(클레임)를 나타냅니다. 클레임에는 사용자 이름, 전자 메일 주소 등이 포함될 수 있습니다.

   - 토큰을 요청하기 위해 [클라이언트](https://identityserver4.readthedocs.io/en/latest/topics/clients.html)가 연결됩니다.

   - [ASP.NET Core ID](https://identityserver4.readthedocs.io/en/latest/quickstarts/0_overview.html) 또는 대체 요소와 같은 사용자 정보에 대한 스토리지 메커니즘.

IdentityServer4가 사용할 클라이언트와 리소스를 지정할 때 적절한 형식의 <xref:System.Collections.Generic.IEnumerable%601> 컬렉션을 메모리 내 클라이언트 또는 리소스 저장소를 사용하는 메서드로 전달할 수 있습니다. 또는 더 복잡한 시나리오의 경우 종속성 주입을 통해 클라이언트 또는 리소스 공급자 형식을 제공할 수 있습니다.

사용자 지정 IClientStore 형식에서 제공한 메모리 내 리소스 및 클라이언트를 사용하는 IdentityServer4를 위한 샘플 구성은 다음 예제처럼 표시될 수 있습니다.

```csharp
// Add IdentityServer services
services.AddSingleton<IClientStore, CustomClientStore>();
services.AddIdentityServer()
    .AddSigningCredential("CN=sts")
    .AddInMemoryApiResources(MyApiResourceProvider.GetAllResources())
    .AddAspNetIdentity<ApplicationUser>();
```

### <a name="consume-security-tokens"></a>보안 토큰 사용

OpenID Connect 엔드포인트에 대해 인증하거나 고유 보안 토큰을 발행하는 방법은 일부 시나리오에서 사용할 수 있습니다. 그러나 다른 서비스에서 제공받은 유효한 보안 토큰이 있는 사용자의 액세스를 제한해야 하는 서비스에는 어떤 방법을 사용해야 할까요?

해당 시나리오의 경우 JWT 토큰을 처리하는 인증 미들웨어를 **Microsoft.AspNetCore.Authentication.JwtBearer** 패키지에서 사용할 수 있습니다. JWT는 “[JSON Web Token](https://tools.ietf.org/html/rfc7519)”을 의미하며 보안 클레임 통신을 위한 일반적인 보안 토큰 형식(RFC 7519에 의해 정의됨)입니다. 미들웨어를 통해 이러한 토큰을 사용하는 방법의 간단한 예제는 eShopOnContainers의 Ordering.Api 마이크로 서비스에서 가져온 이 코드 조각처럼 보일 수 있습니다.

```csharp
// Startup.cs

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    //…
    // Configure the pipeline to use authentication
    app.UseAuthentication();
    //…
    app.UseMvc();
}

public void ConfigureServices(IServiceCollection services)
{
    var identityUrl = Configuration.GetValue<string>("IdentityUrl");

    // Add Authentication services

    services.AddAuthentication(options =>
    {
        options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
        options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;

    }).AddJwtBearer(options =>
    {
        options.Authority = identityUrl;
        options.RequireHttpsMetadata = false;
        options.Audience = "orders";
    });
}
```

이 사용에 대한 매개 변수는 다음과 같습니다.

- `Audience`는 들어오는 토큰의 수신기 또는 토큰에서 액세스 권한을 부여하는 리소스를 나타냅니다. 이 매개 변수에서 지정한 값이 토큰의 매개 변수와 일치하지 않는 경우 토큰이 거부됩니다.

- `Authority`는 토큰 발행 인증 서버의 주소입니다. JWT 전달자 인증 미들웨어는 이 URI를 사용하여 토큰 시그니처의 유효성을 검사하는 데 사용되는 공개 키를 가져옵니다. 또한 미들웨어는 토큰의 `iss` 매개 변수가 이 URI와 일치하는지 확인합니다.

다른 매개 변수 `RequireHttpsMetadata`는 테스트 목적으로 사용하는 것이 적합합니다. 이 매개 변수를 false로 설정하여 인증서가 없는 환경에서 테스트할 수 있습니다. 실제 배포에서 JWT 전달자 토큰은 항상 HTTPS를 통해서만 전달되어야 합니다.

미들웨어가 준비되면 JWT 토큰은 인증 헤더에서 자동으로 추출됩니다. 그런 다음, 토큰은 deserialize되고 (`Audience` 및 `Authority` 매개 변수를 사용하여) 유효성 검사가 진행되며 나중에 MVC 작업 또는 인증 필터에서 참조하는 사용자 정보로 저장됩니다.

JWT 전달자 인증 미들웨어는 인증 기관을 사용할 수 없는 경우 로컬 인증서를 사용하여 토큰의 유효성을 검사하는 상황과 같은 고급 시나리오도 지원할 수 있습니다. 이 시나리오의 경우 `JwtBearerOptions` 개체에서 `TokenValidationParameters` 개체를 지정할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

- **애플리케이션 간 쿠키 공유하기** \
  [https://docs.microsoft.com/aspnet/core/security/cookie-sharing](/aspnet/core/security/cookie-sharing)

- **ID 소개** \
  [https://docs.microsoft.com/aspnet/core/security/authentication/identity](/aspnet/core/security/authentication/identity)

- **Rick Anderson. SMS를 사용한 2단계 인증** \
  [https://docs.microsoft.com/aspnet/core/security/authentication/2fa](/aspnet/core/security/authentication/2fa)

- **Facebook, Google 및 기타 외부 공급 기업을 통해 인증 사용** \
  [https://docs.microsoft.com/aspnet/core/security/authentication/social/](/aspnet/core/security/authentication/social/)

- **Michell Anicas. OAuth 2 소개** \
  <https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2>

- **AspNet.Security.OAuth.Providers**(ASP.NET OAuth 공급자를 위한 GitHub 리포지토리) \
  <https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers/tree/dev/src>

- **Danny Strockis. ASP.NET Core 웹앱에 Azure AD 통합** \
  <https://azure.microsoft.com/resources/samples/active-directory-dotnet-webapp-openidconnect-aspnetcore/>

- **IdentityServer4. 공식 설명서** \
  <https://identityserver4.readthedocs.io/en/latest/>

>[!div class="step-by-step"]
>[이전](../implement-resilient-applications/monitor-app-health.md)
>[다음](authorization-net-microservices-web-applications.md)
