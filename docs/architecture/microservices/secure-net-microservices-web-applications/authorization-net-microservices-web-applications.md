---
title: .NET 마이크로 서비스 및 웹 애플리케이션의 권한 부여 정보
description: .NET 마이크로 서비스 및 웹 애플리케이션의 보안 - ASP.NET Core 애플리케이션의 기본 권한 부여 옵션인 역할 기반 및 정책 기반의 개요를 살펴볼 수 있습니다.
author: mjrousos
ms.author: wiwagn
ms.date: 10/19/2018
ms.openlocfilehash: 36cd8eaf7ffe78a29762398044dc1803adc1b200
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68675660"
---
# <a name="about-authorization-in-net-microservices-and-web-applications"></a>.NET 마이크로 서비스 및 웹 애플리케이션의 권한 부여 정보

인증 후에는 ASP.NET Core Web API에서 액세스 권한을 부여해야 합니다. 이 프로세스를 사용하면 서비스에서 일부 인증된 사용자는 API를 사용할 수 있지만, 모든 사용자가 사용할 수는 없습니다. [권한 부여](/aspnet/core/security/authorization/introduction)는 사용자의 역할 또는 사용자 지정 정책에 따라 수행될 수 있습니다. 이 경우 클레임 또는 다른 추론 검사가 포함될 수 있습니다.

ASP.NET Core MVC 경로에 대한 액세스를 제한하는 것은 다음 예제와 같이 작업 메서드(또는 컨트롤러의 모든 작업에 권한 부여가 필요한 경우 컨트롤러의 클래스)에 Authorize 특성을 적용하는 것만큼 쉽습니다.

```csharp
public class AccountController : Controller
{
    public ActionResult Login()
    {
    }

    [Authorize]
    public ActionResult Logout()
    {
    }
}
```

기본적으로 매개 변수 없이 Authorize 특성을 추가하면 해당 컨트롤러 또는 작업에 대한 인증된 사용자의 액세스가 제한됩니다. 특정 사용자만 사용할 수 있도록 API를 추가로 제한하려면 사용자에게 적합한 필수 역할 또는 정책을 지정하도록 특성을 확장할 수 있습니다.

## <a name="implement-role-based-authorization"></a>역할 기반 권한 부여 구현

ASP.NET Core ID에는 기본 제공되는 역할에 대한 개념이 있습니다. ASP.NET Core ID는 사용자 외에도 애플리케이션에서 사용하는 여러 역할에 대한 정보를 저장하고, 해당 역할에 할당된 사용자를 추적합니다. 이러한 할당은 지속형 스토리지의 역할을 업데이트하는 `RoleManager` 유형과 사용자에게 역할을 부여하거나 철회할 수 있는 `UserManager` 유형을 사용하여 프로그래밍 방식으로 변경할 수 있습니다.

JWT 전달자 토큰으로 인증하는 경우 ASP.NET Core JWT 전달자 인증 미들웨어는 토큰에 있는 역할 클레임에 따라 사용자의 역할을 채웁니다. MVC 작업 또는 컨트롤러에 대한 액세스를 특정 역할의 사용자로 제한하려면 다음 코드 조각과 같이 Authorize 주석(특성)에 Roles 매개 변수를 포함하면 됩니다.

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [Authorize(Roles = "Administrator")]
    public ActionResult ShutDown()
    {
    }
}
```

이 예제에서는 Administrator 또는 PowerUser 역할의 사용자만 ControlPanel 컨트롤러의 API(예: SetTime 작업 실행)에 액세스할 수 있습니다. ShutDown API는 Administrator 역할의 사용자만 액세스할 수 있도록 추가로 제한됩니다.

사용자가 여러 역할을 수행하도록 하려면 다음 예제와 같이 여러 개의 Authorize 특성을 사용합니다.

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
[Authorize(Roles = "RemoteEmployee ")]
[Authorize(Policy = "CustomPolicy")]
public ActionResult API1 ()
{
}
```

이 예제에서 API1을 호출하려면 사용자가 다음을 충족해야 합니다.

- Adminstrator 또는 PowerUser 역할을 담당합니다. 그리고  

- RemoteEmployee 역할을 담당합니다. *그리고*

- CustomPolicy 권한 부여를 위한 사용자 지정 처리기를 충족시킵니다.

## <a name="implement-policy-based-authorization"></a>정책 기반 권한 부여 구현

사용자 지정 권한 부여 규칙은 [권한 부여 정책](https://docs.asp.net/en/latest/security/authorization/policies.html)을 사용하여 작성할 수도 있습니다. 이 섹션에서는 개요를 살펴봅니다. 자세한 내용은 [ASP.NET 권한 부여 워크샵](https://github.com/blowdart/AspNetAuthorizationWorkshop)을 참조하세요.

사용자 지정 권한 정책은 service.AddAuthorization 메서드를 사용하여 Startup.ConfigureServices 메서드에 등록됩니다. 이 메서드는 AuthorizationOptions 인수를 구성하는 대리자를 사용합니다.

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("AdministratorsOnly", policy =>
        policy.RequireRole("Administrator"));
    options.AddPolicy("EmployeesOnly", policy =>
        policy.RequireClaim("EmployeeNumber"));
    options.AddPolicy("Over21", policy =>
        policy.Requirements.Add(new MinimumAgeRequirement(21)));
});
```

이 예제와 같이 정책은 다양한 유형의 요구 사항과 연결할 수 있습니다. 정책이 등록되면 정책 이름을 Authorize 특성의 Policy 인수(예: `[Authorize(Policy="EmployeesOnly")]`)로 전달하여 작업 또는 컨트롤러에 적용할 수 있습니다. 정책에는 하나의 요구 사항만 아니라 이 예제처럼 여러 요구 사항이 있을 수 있습니다.

앞의 예제에서 첫 번째 AddPolicy 호출은 역할별로 권한을 부여하는 다른 방법일 뿐입니다. `[Authorize(Policy="AdministratorsOnly")]`가 API에 적용되면 Administrator 역할의 사용자만 API에 액세스할 수 있습니다.

두 번째 <xref:Microsoft.AspNetCore.Authorization.AuthorizationOptions.AddPolicy%2A> 호출은 사용자에게 특정 클레임이 있어야 한다고 요구하는 쉬운 방법을 보여 줍니다. <xref:Microsoft.AspNetCore.Authorization.AuthorizationPolicyBuilder.RequireClaim%2A> 메서드는 필요에 따라 클레임에 대한 예상 값도 사용합니다. 값이 지정되면 사용자가 올바른 유형의 클레임과 지정된 값 중 하나를 가지고 있는 경우에만 요구 사항이 충족됩니다. JWT 전달자 인증 미들웨어를 사용하는 경우 모든 JWT 속성을 사용자 클레임으로 사용할 수 있습니다.

여기서 보여 주는 가장 흥미로운 정책은 세 번째 `AddPolicy` 메서드에 있으며, 사용자 지정 권한 요구 사항을 사용합니다. 사용자 지정 권한 부여 요구 사항을 사용하면 권한 부여가 수행되는 방식을 크게 제어할 수 있습니다. 이렇게 하려면 다음 유형을 구현해야 합니다.

- <xref:Microsoft.AspNetCore.Authorization.IAuthorizationRequirement>에서 파생되고 요구 사항의 세부 정보를 지정하는 필드가 포함된 Requirements 유형. 예제에서는 샘플 `MinimumAgeRequirement` 유형의 연령 필드입니다.

- <xref:Microsoft.AspNetCore.Authorization.AuthorizationHandler%601>를 구현하는 처리기. 여기서 T는 처리기가 충족할 수 있는 <xref:Microsoft.AspNetCore.Authorization.IAuthorizationRequirement> 유형입니다. 처리기에서 <xref:Microsoft.AspNetCore.Authorization.AuthorizationHandler%601.HandleRequirementAsync%2A> 메서드를 구현해야 합니다. 이 메서드는 지정된 컨텍스트(사용자에 대한 정보가 포함되어 있음)에서 요구 사항이 충족되는지 여부를 확인합니다.

사용자가 요구 사항을 충족하는 경우 `context.Succeed`를 호출하면 사용자에게 권한이 있음을 알립니다. 사용자가 권한 부여 요구 사항을 충족시킬 수 있는 여러 가지 방법이 있는 경우 처리기를 여러 개 만들 수 있습니다.

`AddPolicy` 호출에 사용자 지정 정책 요구 사항을 등록하는 것 외에도, 종속성 삽입(`services.AddTransient<IAuthorizationHandler, MinimumAgeHandler>()`)을 통해 사용자 지정 요구 사항 처리기를 등록해야 합니다.

`DateOfBirth` 클레임에 따라 사용자의 연령을 확인하기 위한 사용자 지정 권한 부여 요구 사항 및 처리기의 예제는 ASP.NET Core [권한 부여 문서](https://docs.asp.net/en/latest/security/authorization/policies.html)에서 확인할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

- **ASP.NET Core 인증** \
  [https://docs.microsoft.com/aspnet/core/security/authentication/identity](/aspnet/core/security/authentication/identity)

- **ASP.NET Core 권한 부여** \
  [https://docs.microsoft.com/aspnet/core/security/authorization/introduction](/aspnet/core/security/authorization/introduction)

- **역할 기반 권한 부여** \
  [https://docs.microsoft.com/aspnet/core/security/authorization/roles](/aspnet/core/security/authorization/roles)

- **사용자 지정 정책 기반 권한 부여** \
  [https://docs.microsoft.com/aspnet/core/security/authorization/policies](/aspnet/core/security/authorization/policies)

>[!div class="step-by-step"]
>[이전](index.md)
>[다음](developer-app-secrets-storage.md)
