---
title: WIF 3.5와 WIF 4.5 간의 네임스페이스 매핑
ms.date: 03/30/2017
ms.assetid: a092d98c-444d-4336-a644-63c2e11e96c8
author: BrucePerlerMS
ms.openlocfilehash: d967ce931e81ca14645e7464943e1411264d6ca2
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045413"
---
# <a name="namespace-mapping-between-wif-35-and-wif-45"></a>WIF 3.5와 WIF 4.5 간의 네임스페이스 매핑

.NET 4.5부터 WIF(Windows Identity Foundation)는 완전히 .NET Framework에 통합되었습니다. 이와 같이 통합하면 이름이 변경되고 WIF 네임스페이스와 API 화면이 일부 통합됩니다. 이 항목에서는 WIF 3.5 네임스페이스와 WIF 4.5 네임스페이스 사이의 일반적인 매핑 및 지침을 제공합니다. 이 항목에서는 모든 정보를 제공하는 것이 아니라 WIF 4.5에서 익숙한 WIF 3.5 클래스가 있는 위치에 대한 일반적인 정보만 제공합니다. WIF 3.5와 WIF 4.5 간의 차이점에 대한 자세한 내용은 [Windows Identity Foundation 4.5의 새로운 기능](whats-new-in-wif.md)을 참조하세요. WIF 3.5를 사용하여 빌드된 애플리케이션을 WIF 4.5로 마이그레이션하는 방법에 대한 지침은 [WIF 3.5를 사용하여 빌드된 애플리케이션을 WIF 4.5로 마이그레이션하는 지침](guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)을 참조하세요.

## <a name="wif-35-to-wif-45-namespace-map"></a>WIF 3.5와 WIF 4.5 네임스페이스 맵

WIF 3.5의 `Microsoft.IdentityModel` 네임스페이스에서 수집된 WIF 클래스는 이제 WIF 4.5 `System.Security.Claims`, `System.ServiceModel.Security` 및 `System.IdentityModel` 네임스페이스 간에 분배됩니다. 또한 일부 WIF 3.5 네임스페이스는 WIF 4.5에서 완전히 삭제되거나 통합되었습니다.

> [!IMPORTANT]
> 다음 `System.IdentityModel` 네임스페이스에는 WCF 클레임 기반 ID 모델을 구현하는 클래스가 포함됩니다. <xref:System.IdentityModel.Claims?displayProperty=nameWithType>, <xref:System.IdentityModel.Policy?displayProperty=nameWithType> 및 <xref:System.IdentityModel.Selectors?displayProperty=nameWithType>. WCF 클레임 기반 ID 모델은 WIF로 대체됩니다. WIF를 기반으로 솔루션을 빌드할 때 이러한 세 개의 네임스페이스에서 클래스를 사용하면 안 됩니다.

다음 표에서는 WIF 4.5에서 WIF 3.5 클래스가 있는 위치에 대한 정보를 제공합니다.

|**WIF 3.5 네임스페이스**|**WIF 4.5 네임스페이스**|**설명**|
|-|-|-|
|`Microsoft.IdentityModel`|<xref:System.IdentityModel?displayProperty=nameWithType>|-   상수를 나타내는 대부분의 클래스는 구현되지 않습니다.<br />-   보안 토큰 서비스를 빌드하는 데 사용되는 클래스는 `Microsoft.IdentityModel.SecurityTokenService`에서 <xref:System.IdentityModel?displayProperty=nameWithType>으로 이동되었습니다.<br />-   `Microsoft.IdentityModel.Threading`의 클래스는 <xref:System.IdentityModel?displayProperty=nameWithType>으로 이동되었습니다.<br />-   `ExceptionMapper` 및 `MruSecurityTokenCache` 클래스는 구현되지 않습니다.|
|`Microsoft.IdentityModel.Claims`|<xref:System.Security.Claims?displayProperty=nameWithType>|-   `IClaimsPrincipal` 및 `IClaimsIdentity` 인터페이스는 WIF 4.5에서 구현되지 않습니다. 대신 <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType> 및 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=nameWithType>이 이제 대부분의 .NET 보안 주체와 ID 클래스가 파생사는 기본 클래스입니다. 즉, WIF 4.5에서 `Microsoft.IdentityModel.Claims.WindowsClaimsPrincipal` 및 `Microsoft.IdentityModel.Claims.WindowsClaimsIdentity` 등의 특수 클레임 보안 주체와 ID 클래스가 필요하지 않으며, 대신 <xref:System.Security.Principal.WindowsPrincipal?displayProperty=nameWithType> 및 <xref:System.Security.Principal.WindowsIdentity?displayProperty=nameWithType>을 사용합니다. WIF 3.5에 있는 다른 특수 클레임 보안 주체와 ID 클래스의 경우에도 마찬가지입니다.<br />-   `Microsoft.IdentityModel.Claims.ClaimsCollection` 클래스가 WIF 4.5에 구현되지 않았습니다. 대신, 클레임의 컬렉션은 <xref:System.Security.Claims.Claim?displayProperty=nameWithType> 유형의 열거형 컬렉션으로 공개됩니다.<br />-   <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType> 및 <xref:System.Security.Claims.ClaimsIdentity?displayProperty=nameWithType>에서는 이제 LINQ를 완전히 지원하는 메서드를 제공합니다.|
|`Microsoft.IdentityModel.Configuration`|<xref:System.IdentityModel.Configuration?displayProperty=nameWithType>|일부 요소와 클래스에서는 이름이 변경되었으며 일부는 WIF 4.5에서 제거되었습니다. 예를 들어 `Microsoft.IdentityModel.Configuration.ServiceConfiguration`은 이제 <xref:System.IdentityModel.Configuration.IdentityConfiguration?displayProperty=nameWithType>입니다.|
|`Microsoft.IdentityModel.Protocols`|<xref:System.IdentityModel.Services?displayProperty=nameWithType>|-|
|`Microsoft.IdentityModel.Protocols.WSFederation`|<xref:System.IdentityModel.Services?displayProperty=nameWithType>|-|
|`Microsoft.IdentityModel.Protocols.WSFederation.Metadata`|<xref:System.IdentityModel.Metadata?displayProperty=nameWithType>|-|
|`Microsoft.IdentityModel.Protocols.WSIdentity`|WIF 4.5에서 구현되지 않음|CardSpace를 지원하는 WIF 3.5에 포함된 클래스의 경우 WIF 4.5에는 구현되지 않음|
|`Microsoft.IdentityModel.Protocols.WSTrust`|<xref:System.IdentityModel.Protocols.WSTrust?displayProperty=nameWithType> 및 <xref:System.ServiceModel.Security?displayProperty=nameWithType> 네임스페이스를 분리합니다.|WS-Trust 아티팩트를 나타내는 클래스는 <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=nameWithType> 네임스페이스에 있습니다(예: <xref:System.IdentityModel.Protocols.WSTrust.RequestSecurityToken> 클래스). WCF 서비스 계약을 나타내는 클래스, 서비스 호스트 및 WCF 서비스를 통해 WS-Trust 프로토콜을 사용하여 통신할 수 있는 채널은 <xref:System.ServiceModel.Security?displayProperty=nameWithType> 네임스페이스에 있습니다(예: <xref:System.ServiceModel.Security.WSTrustServiceHost> 클래스).|
|`Microsoft.IdentityModel.Protocols.WSTrust.Bindings`|WIF 4.5에서 구현되지 않음|-|
|`Microsoft.IdentityModel.Protocols.XmlEncryption`|WIF 4.5에서 구현되지 않음|WIF 3.5의 XML 암호화 상수를 나타내는 포함된 클래스. 이러한 상수는 WIF 4.5에 구현되어 있지 않습니다.|
|`Microsoft.IdentityModel.Protocols.XmlSignature`|<xref:System.IdentityModel?displayProperty=nameWithType>|`EnvelopingSignature` 클래스와 상수를 나타내는 클래스는 구현되지 않았습니다.|
|`Microsoft.IdentityModel.SecurityTokenService`|<xref:System.IdentityModel?displayProperty=nameWithType>, <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=nameWithType> 및 <xref:System.IdentityModel.Tokens?displayProperty=nameWithType> 네임스페이스를 분리합니다.|-|
|`Microsoft.IdentityModel.Threading`|<xref:System.IdentityModel?displayProperty=nameWithType>|-|
|`Microsoft.IdentityModel.Tokens`|<xref:System.IdentityModel.Tokens?displayProperty=nameWithType>|-|
|`Microsoft.IdentityModel.Tokens.Saml11`|<xref:System.IdentityModel.Tokens?displayProperty=nameWithType>|-|
|`Microsoft.IdentityModel.Tokens.Saml2`|<xref:System.IdentityModel.Tokens?displayProperty=nameWithType>|-|
|`Microsoft.IdentityModel.Web`|<xref:System.IdentityModel.Services?displayProperty=nameWithType>|-|
|`Microsoft.IdentityModel.Web.Configuration`|<xref:System.IdentityModel.Services.Configuration?displayProperty=nameWithType>|수동(WS-Federation) 시나리오의 구성을 제공하는 클래스는 대부분 <xref:System.IdentityModel.Services.Configuration?displayProperty=nameWithType>으로 이동되었지만, 이러한 클래스 중 일부는 <xref:System.IdentityModel.Services?displayProperty=nameWithType>에 있습니다.|
|`Microsoft.IdentityModel.Web.Controls`|WIF 4.5에서 구현되지 않음|`Microsoft.IdentityModel.Web.Controls`의 클래스는 WIF 4.5에 없는 Federated Passive Sign-In Control을 구현했습니다.|
|`Microsoft.IdentityModel.WindowsTokenService`|WIF 4.5에서 구현되지 않음|-|

## <a name="see-also"></a>참고자료

- [Windows Identity Foundation 4.5의 새로운 기능](whats-new-in-wif.md)
- [WIF 3.5를 사용하여 빌드된 응용 프로그램을 WIF 4.5로 마이그레이션하는 지침](guidelines-for-migrating-an-application-built-using-wif-3-5-to-wif-4-5.md)
