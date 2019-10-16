---
title: WIF 3.5를 사용하여 빌드된 애플리케이션을 WIF 4.5로 마이그레이션하는 지침
ms.date: 03/30/2017
ms.assetid: 7a32fe6e-5f68-4693-9371-19411fa8063c
author: BrucePerlerMS
ms.openlocfilehash: 645fd09de91d8190384faea9df2ef18511162c2f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834528"
---
# <a name="guidelines-for-migrating-an-application-built-using-wif-35-to-wif-45"></a>WIF 3.5를 사용하여 빌드된 애플리케이션을 WIF 4.5로 마이그레이션하는 지침

## <a name="applies-to"></a>적용 대상

- Microsoft® WIF(Windows® Identity Foundation) 3.5 및 4.5.

## <a name="overview"></a>개요

WIF(Windows Identity Foundation)는 원래 .NET 3.5 SP1 기간에 릴리스되었습니다. 해당 버전의 WIF를 WIF 3.5라고 합니다. 별도의 런타임 및 SDK로 릴리스되었습니다. 즉, WIF 지원 애플리케이션이 실행된 모든 컴퓨터에 WIF 런타임이 설치되어 있어야 하고, 개발자가 WIF 지원 애플리케이션을 개발할 수 있는 Visual Studio 템플릿과 도구를 얻기 위해 WIF SDK를 다운로드하여 설치해야 했습니다. .NET 4.5부터 WIF는 완전히 .NET Framework에 통합되었습니다. 더 이상 별도의 런타임이 필요하지 않고 WIF 도구는 Visual Studio 2012에서 Visual Studio 확장 관리자를 사용하여 설치할 수 있습니다. 이 버전의 WIF를 WIF 4.5라고 합니다.

WIF를 .NET에 통합하려면 WIF API 화면에서 여러 항목을 변경해야 했습니다. WIF 4.5에는 Visual Studio에 대한 새로운 네임스페이스, 몇 가지 구성 요소 변경 및 새로운 도구가 포함됩니다. 이 항목에서는 WIF 3.5를 사용하여 빌드된 애플리케이션을 WIF 4.5로 마이그레이션할 때 사용할 수 있는 지침을 제공합니다. Windows 8 또는 Windows Server 2012를 실행하는 컴퓨터에서 WIF 3.5를 사용하여 빌드된 레거시 애플리케이션을 실행해야 하는 경우가 있을 수 있습니다. 이 항목에서는 이러한 운영 체제에서 WIF 3.5를 사용하도록 설정하는 방법에 대한 지침을 제공합니다.

## <a name="changes-required-for-wif-45"></a>WIF 4.5에 필요한 변경 내용

이 섹션에서는 WIF 3.5 애플리케이션을 WIF 4.5로 마이그레이션하는 데 필요한 변경 내용을 설명합니다.

### <a name="assembly-and-namespace-changes"></a>어셈블리 및 네임스페이스 변경 내용

WIF 3.5에서 모든 WIF 클래스는 `Microsoft.IdentityModel` 어셈블리(microsoft.identitymicrosoft.identitymodel.dll)에 포함되었습니다. WIF 4.5에서 WIF 클래스는 `mscorlib`(mscorlib.dll), `System.IdentityModel`(System.IdentityModel.dll), `System.IdentityModel.Services`(System.IdentityModel.Services.dll) 및 `System.ServiceModel`(System.ServiceModel.dll) 어셈블리에 분할되었습니다.

WIF 3.5 클래스는 `Microsoft.IdentityModel` 네임스페이스(예: `Microsoft.IdentityModel`, `Microsoft.IdentityModel.Tokens`, `Microsoft.IdentityModel.Web` 등) 중 하나에 모두 포함되었습니다. WIF 4.5에서 WIF 클래스는 이제 [System.IdentityModel](https://go.microsoft.com/fwlink/?LinkId=272004) 네임스페이스, <xref:System.Security.Claims?displayProperty=nameWithType> 네임스페이스 및 <xref:System.ServiceModel.Security?displayProperty=nameWithType> 네임스페이스에 분산되어 있습니다. 이 재구성 이외에 일부 WIF 3.5 클래스는 WIF 4.5에서 삭제되었습니다.

다음 표에서는 일부 더 중요한 WIF 4.5 네임스페이스와 네임스페이스에 포함된 클래스 종류를 보여 줍니다. WIF 3.5와 WIF 4.5 간 네임스페이스 매핑 방법 및 WIF 4.5에서 삭제된 네임스페이스와 클래스에 대한 자세한 내용은 [WIF 3.5와 WIF 4.5 간의 네임스페이스 매핑](namespace-mapping-between-wif-3-5-and-wif-4-5.md)을 참조하세요.

|WIF 4.5 네임스페이스|설명|
|-----------------------|-----------------|
|<xref:System.IdentityModel?displayProperty=nameWithType>|쿠키 변환, 보안 토큰 서비스 및 특수 XML 사전 판독기를 나타내는 클래스를 포함합니다. WIF 3.5 네임스페이스 `Microsoft.IdentityModel`, `Microsoft.IdentityModel.SecurityTokenService` 및 `Microsoft.IdentityModel.Threading`의 클래스를 포함합니다.|
|<xref:System.Security.Claims?displayProperty=nameWithType>|클레임, 클레임 기반 ID, 클레임 기반 주체 및 기타 클레임 기반 ID 모델 아티팩트를 나타내는 클래스를 포함합니다. `Microsoft.IdentityModel.Claims` 네임스페이스의 클래스를 포함합니다.|
|<xref:System.IdentityModel.Tokens?displayProperty=nameWithType>|보안 토큰, 보안 토큰 처리기 및 기타 보안 토큰 아티팩트를 나타내는 클래스를 포함합니다. WIF 3.5 네임스페이스 `Microsoft.IdentityModel.Tokens`, `Microsoft.IdentityModel.Tokens.Saml11` 및 `Microsoft.IdentityModel.Tokens.Saml2`의 클래스를 포함합니다.|
|<xref:System.IdentityModel.Services?displayProperty=nameWithType>|수동(WS-Federation) 시나리오에서 사용되는 클래스를 포함합니다. `Microsoft.IdentityModel.Web` 네임스페이스의 클래스를 포함합니다.|
|<xref:System.ServiceModel.Security?displayProperty=nameWithType>|활성(WS-Trust) 시나리오에서 사용되는 WCF 계약, 채널, 서비스 호스트 및 기타 아티팩트를 나타내는 클래스는 이제 이 네임스페이스에 있습니다. WIF 3.5에서 이러한 클래스는 `Microsoft.IdentityModel.Protocols.WSTrust` 네임스페이스에 있었습니다.|

> [!IMPORTANT]
> 다음 `System.IdentityModel` 네임스페이스에는 WCF 클레임 기반 ID 모델을 구현하는 클래스가 포함됩니다. <xref:System.IdentityModel.Claims?displayProperty=nameWithType>, <xref:System.IdentityModel.Policy?displayProperty=nameWithType> 및 <xref:System.IdentityModel.Selectors?displayProperty=nameWithType>. WCF 클레임 기반 ID 모델은 WIF로 대체됩니다. WIF를 기반으로 솔루션을 빌드할 때 이러한 세 개의 네임스페이스에서 클래스를 사용하면 안 됩니다.

### <a name="changes-due-to-net-integration"></a>.NET 통합으로 인한 변경

WIF는 이제 .NET Framework에 통합되어 있습니다. 대부분의 .NET ID 및 주체 클래스는 이제 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=nameWithType> 및 <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType>에서 파생됩니다. 이에 따라 WIF 4.5에서 다음과 같이 변경됩니다.

- 클레임, ID 및 주체를 나타내는 WIF 클래스는 이제 <xref:System.Security.Claims?displayProperty=nameWithType> 네임스페이스에 있습니다.

    > [!IMPORTANT]
    > <xref:System.IdentityModel.Claims?displayProperty=nameWithType> 네임스페이스에는 WCF 클레임 기반 ID 모델의 아티팩트를 나타내는 클래스가 포함됩니다. 이러한 클래스는 대부분 WIF 클래스와 동일한 이름을 가집니다(예: `Claims`). WIF를 기반으로 솔루션을 빌드할 때 이러한 클래스를 사용하지 마세요.

- .NET ID 및 주체 클래스는 이제 클레임 기반 ID 및 보안 주체를 나타내는 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=nameWithType> 및 <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType>에서 직접 파생됩니다. 따라서 WIF 3.5 인터페이스 `IClaimsIdentity` 및 `IClaimsPrincipal`은 더 이상 필요하지 않고 WIF 4.5에서 사용할 수 없습니다.

- <xref:System.Security.Principal.WindowsIdentity?displayProperty=nameWithType> 및 <xref:System.Security.Principal.WindowsPrincipal?displayProperty=nameWithType>과 같은 .NET ID 및 주체 클래스는 이제 <xref:System.Security.Claims.ClaimsIdentity> 및 <xref:System.Security.Claims.ClaimsPrincipal>에서 파생되므로 클레임 기능이 기본 제공됩니다. 따라서 WIF 3.5에 있던 `WindowsClaimsIdentity` 및 `WindowsClaimsPrincipal`과 같은 클레임별 ID 및 주체 클래스는 더 이상 필요하지 않고 WIF 4.5에 없습니다.

### <a name="other-changes-to-wif-functionality"></a>WIF 기능의 기타 변경 내용

네임스페이스 변경 내용과 .NET 통합으로 인한 변경 내용 이외에 WIF 기능에 대한 다음과 같은 일반 변경이 WIF 4.5에서 이루어집니다.

- 특정 SOAP 오류에 예외를 매핑할 수 있는 기능을 제공한 `Microsoft.IdentityModel.ExceptionMapper` 클래스가 제거됩니다.

- 예외 화면이 크게 감소했습니다.

- 프로토콜 또는 WS-* 관련 상수를 정의한 대부분의 클래스가 제거되었습니다(예: WS-Addressing 1.0 관련 상수를 정의한 `Microsoft.IdentityModel.WSAddressing10Constants` 클래스).

- Windows 토큰 서비스에 대한 클레임(c2wts) 및 `Microsoft.IdentityModel.WindowsTokenService` 네임스페이스의 해당 연결된 클래스가 제거됩니다.

### <a name="wif-configuration-changes"></a>WIF 구성 변경

구성 파일의 대부분 변경 내용은 WIF 4.5의 네임스페이스 업데이트로 인해 발생했습니다. 예를 들어 WS-Federation 인증 관리자를 애플리케이션에 추가하려면 `<httpModules>` 섹션에서 다음 WIF 3.5 항목을 고려하세요.

```xml
<add name="WSFederationAuthenticationModule" type="Microsoft.IdentityModel.Web.WSFederationAuthenticationModule, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=abcd … 5678" />
```

이 항목은 새 네임스페이스와 어셈블리 버전을 포함하도록 WIF 4.5에서 업데이트되었습니다.

```xml
<add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=abcd … 5678"/>
```

다음 목록에는 WIF 4.5 구성 파일에 대한 주요 변경 내용이 열거됩니다.

- `<microsoft.identityModel>` 섹션은 이제 [\<system.identityModel>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) 섹션입니다.

- `<service>` 요소는 이제 [\<identityConfiguration>](../configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 요소입니다.

- 수동(WS-Federation) 시나리오에서 동작을 제어하는 설정을 지정하기 위해 새로운 섹션 [\<system.identityModel.services>](../configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md)가 추가되었습니다.

- [\<federationConfiguration>](../configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md) 요소와 해당 자식 요소가 WIF 3.5의 `<service>` 요소에서 새로운 `<system.identityModel.services>` 요소로 이동되었습니다.

- WIF 3.5의 `<service>` 요소 바로 아래의 서비스 수준에서 지정될 수 있는 여러 요소는 [\<securityTokenHandlerConfiguration>](../configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md) 요소 아래에 지정되도록 제한되었습니다. 이전 버전과의 호환성을 위해 WIF 4.5에서도 이러한 요소를 [\<identityConfiguration>](../configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 요소 아래에 지정할 수 있습니다.

WIF 4.5 구성 요소의 전체 목록을 보려면 [WIF 구성 스키마](../configure-apps/file-schema/windows-identity-foundation/index.md)를 참조하세요.

### <a name="visual-studio-tooling-changes"></a>Visual Studio 도구 변경

WIF 3.5 SDK에서는 WIF 사용 가능 애플리케이션의 ID 관리를 STS(보안 토큰 서비스)로 아웃소싱하는 데 사용할 수 있는 독립 실행형 페더레이션 유틸리티, FedUtil.exe(FedUtil)를 제공했습니다. 이 도구는 애플리케이션이 하나 이상의 STS에서 보안 토큰을 가져올 수 있도록 WIF 설정을 애플리케이션 구성 파일에 추가하고 **Add STS Service Reference**(STS 서비스 참조 추가) 단추를 통해 Visual Studio에 표시되었습니다. FedUtil은 WIF 4.5와 함께 제공되지 않습니다. 대신에 WIF 4.5는 ID 관리를 STS로 아웃소싱하는 데 필요한 WIF 설정을 통해 애플리케이션 구성 파일을 수정하는 데 사용할 수 있는 Visual Studio 2012용 ID 및 액세스 도구라는 새로운 Visual Studio 확장을 지원합니다. ID 및 액세스 도구는 WIF 사용 가능 애플리케이션을 테스트하는 데 사용할 수 있는 로컬 STS라는 STS도 구현합니다. 대부분의 경우 이 기능을 사용하면 개발 시에 솔루션을 테스트하기 위해 WIF 3.5에서 종종 필요했던 사용자 지정 STS를 빌드할 필요가 없습니다. 따라서 STS 템플릿은 Visual Studio 2012에서 더는 지원되지 않지만 STS 개발을 지원하는 클래스는 WIF 4.5에서 계속 사용할 수 있습니다.

Visual Studio의 확장 및 업데이트 관리자에서 Id 및 액세스 도구를 설치 하거나 코드 갤러리의 다음 페이지에서이 도구를 다운로드할 수 있습니다. [코드 갤러리의 Visual Studio 2012에 대 한 id 및 액세스 도구](https://go.microsoft.com/fwlink/?LinkID=245849)입니다. Visual Studio 도구 변경 내용은 다음 목록에 요약되어 있습니다.

- STS 서비스 참조 추가 기능이 제거됩니다. 대신에 ID 및 액세스 도구가 사용됩니다.

- Visual Studio STS 템플릿이 제거됩니다. ID 및 액세스 도구를 통해 사용할 수 있는 로컬 STS를 사용하여 WIF로 개발하는 ID 솔루션을 테스트할 수 있습니다. 로컬 STS 구성을 수정하여 구성이 사용되는 클레임을 사용자 지정할 수 있습니다.

- 독립 실행형 페더레이션 유틸리티(FedUtil)를 WIF 4.5에서 사용할 수 없습니다. ID 및 액세스 도구를 통해 구성 파일을 수정하여 ID 관리를 STS로 아웃소싱할 수 있습니다.

Id 및 액세스 도구에 대 한 자세한 내용은 [Visual Studio 2012에 대 한 id 및 액세스 도구](identity-and-access-tool-for-vs.md)를 참조 하세요.

<a name="BKMK_ToolingChanges"></a>

### <a name="passive-ws-federation-scenarios"></a>수동(WS-Federation) 시나리오:

- 수동 시나리오를 지원하는 클래스는 <xref:System.IdentityModel.Services?displayProperty=nameWithType> 네임스페이스로 이동되었습니다. WIF 3.5에서 이러한 클래스는 `Microsoft.IdentityModel.Web` 네임스페이스에 있었습니다.

- `Microsoft.IdentityModel.Web.Configuration` 네임스페이스의 클래스는 <xref:System.IdentityModel.Services.Configuration?displayProperty=nameWithType>으로 이동되었습니다. 이러한 클래스는 수동 시나리오에서 구성 관련 개체를 나타냅니다.

- `FederatedPassiveSignInControl`은 더 이상 지원되지 않고 `Microsoft.IdentityModel.Web.Controls` 네임스페이스의 모든 클래스가 WIF 4.5에서 제거되었습니다.

- WS-Federation 인증 모듈(<xref:System.IdentityModel.Services.WSFederationAuthenticationModule>) 로그아웃 기능은 WIF 3.5와 다릅니다. WIF 4.5의 로그아웃 작동 방식에 대한 자세한 내용은 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 클래스 항목을 참조하세요.

### <a name="active-wcfws-trust-scenarios"></a>활성(WCF/WS-Trust) 시나리오:

- `Microsoft.IdentityModel.Protocols.WSTrust` 네임스페이스는 WIF 4.5에서 주로 두 개의 네임스페이스로 분할되었습니다. WS-Trust 프로토콜에 관련된 아티팩트를 나타내는 클래스는 이제 <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=nameWithType>에 있습니다. 여기에는 <xref:System.IdentityModel.Protocols.WSTrust.RequestSecurityToken> 같은 클래스가 포함됩니다. WCF 애플리케이션에서 WS-Trust 사용에 포함된 서비스 계약, 채널, 서비스 호스트 및 기타 아티팩트를 나타내는 클래스는 <xref:System.ServiceModel.Security?displayProperty=nameWithType>(예: <xref:System.ServiceModel.Security.IWSTrust13AsyncContract> 인터페이스)로 이동되었습니다.

- WIF를 사용하도록 WCF 애플리케이션을 구성하는 작업이 크게 간소화되었습니다. 이전에 `Microsoft.IdentityModel.Configuration.ConfigureServiceHostBehaviorExtensionElement`는 동작 확장으로 추가되어야 했고 이 기능은 `<federatedServiceHostConfiguration>` 요소를 지정하여 WIF를 서비스 동작에 밀어 넣는 데 사용되었습니다. WIF 4.5는 WCF와 더 엄격하게 통합되었습니다. 이제 다음 XML과 같이 `<system.serviceModel>`/`<behaviors>`/`<serviceBehaviors>`/`<serviceCredentials>` 요소에서 `useIdentityConfiguration` 특성을 지정하여 WCF 서비스에서 WIF를 사용할 수 있습니다.

    ```xml
    <serviceCredentials useIdentityConfiguration="true">
        <!--Certificate added by Identity And Access VS Package.  Subject='CN=localhost', Issuer='CN=localhost'. Make sure you have this certificate installed. The Identity and Access tool does not install this certificate.-->
        <serviceCertificate findValue="CN=localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName" />
    </serviceCredentials>
    ```

- WIF 4.5의 경우 활성(WCF) 서비스에서 사용되는 서비스 인증서를 서비스 호스트에서 지정해야 합니다. 이전 예제와 같이 구성에서 `<system.serviceModel>`/`<behaviors>`/`<serviceBehaviors>`/`<serviceCredentials>`/`<serviceCertificate>` 요소를 통해 이 작업을 수행할 수 있습니다. WIF 3.5에서 서비스 인증서는 WIF `<service>` 요소의 `<serviceCertificate>` 자식 요소를 통해 지정할 수 있습니다. WIF 4.5에는 이 기능이 없습니다. 대신에 `<serviceCredentials>` 요소 아래에 `<serviceCertificate>` 요소를 지정합니다.

- WIF 3.5를 WCF로 밀어 넣는 데 사용되는 클래스가 더 이상 없습니다. 여기에는 `Microsoft.IdentityModel.Tokens` 네임스페이스의 `FederatedSecurityTokenManager`, `FederatedServiceCredentials` 및 `IdentityModelServiceAuthorizationManager` 클래스와 `Microsoft.IdentityModel.Configuration.ConfigureServiceHostBehaviorExtensionElement` 클래스가 포함됩니다.

## <a name="enabling-wif-35-in-windows-8"></a>Windows 8에서 WIF 3.5 사용

WIF 4.5는 .NET 4.5의 일부이므로 Windows 8 및 Windows Server 2012를 실행하는 컴퓨터에서 자동으로 사용하도록 설정되고 WIF 4.5를 사용하여 빌드된 애플리케이션은 기본적으로 Windows 8 또는 Windows Server 2012에서 실행됩니다. 그러나 Windows 8 또는 Windows Server 2012를 실행하는 컴퓨터에서 WIF 3.5를 사용하여 빌드된 애플리케이션을 실행해야 할 수 있습니다. 이 경우 대상 컴퓨터에서 WIF 3.5를 사용하도록 설정해야 합니다. Windows 8을 실행하는 컴퓨터에서는 DISM(배포 이미지 서비스 및 관리) 도구를 사용하여 이 작업을 수행할 수 있습니다. Windows Server 2012를 실행하는 컴퓨터에서 DISM 도구를 사용하거나 Windows PowerShell `Add-WindowsFeature` cmdlet을 사용할 수 있습니다. 두 경우에 모두 명령줄에서 또는 Windows PowerShell 환경 내에서 해당 명령을 호출할 수 있습니다.

다음 명령은 명령줄에서 또는 Windows PowerShell 환경 내에서 DISM 도구를 사용하는 방법을 보여 줍니다. 기본적으로 DISM PowerShell 모듈은 Windows 8 및 Windows Server 2012에 포함되어 있고 가져올 필요가 없습니다. Windows PowerShell에서 DISM을 사용하는 방법에 대한 자세한 내용은 [Windows PowerShell에서 DISM 사용](https://go.microsoft.com/fwlink/?LinkId=254419)을 참조하세요.

DISM으로 WIF 3.5를 사용하도록 설정하려면:

```console
dism /online /enable-feature:windows-identity-foundation
```

DISM으로 WIF 3.5를 사용하지 않도록 설정하려면:

```console
dism /online /disable-feature:windows-identity-foundation
```

DISM으로 사용하거나 사용하지 않도록 설정되는 기능을 확인하려면:

```console
dism /online /get-features
```

또는 Windows Server 2012를 실행하는 컴퓨터에서 Windows PowerShell `Add-WindowsFeature` cmdlet을 사용하여 WIF 3.5를 사용하도록 설정할 수 있습니다. 명령줄에서 이 작업을 수행하려면 다음 명령을 입력합니다.

```console
powershell "add-windowsfeature windows-identity-foundation"
```

 Windows PowerShell 환경 내에서 명령을 직접 입력할 수 있습니다.

```powershell
Add-WindowsFeature windows-identity-foundation
```

> [!NOTE]
> WIF 3.5 및 WIF 4.5의 대부분 클래스는 동일한 이름을 공유하므로 WIF 3.5 및 WIF 4.5를 함께 사용할 경우 정규화된 클래스 이름을 사용하거나 네임스페이스 별칭을 사용하여 WIF 3.5 및 WIF 4.5의 클래스를 구별해야 합니다.

## <a name="see-also"></a>참조

- [WIF 구성 스키마](../configure-apps/file-schema/windows-identity-foundation/index.md)
- [WIF 3.5와 WIF 4.5 간의 네임스페이스 매핑](namespace-mapping-between-wif-3-5-and-wif-4-5.md)
- [Windows Identity Foundation 4.5의 새로운 기능](whats-new-in-wif.md)
- [Visual Studio 2012용 ID 및 액세스 도구](identity-and-access-tool-for-vs.md)
