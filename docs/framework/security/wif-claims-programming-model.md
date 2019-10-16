---
title: WIF 클레임 프로그래밍 모델
ms.date: 03/30/2017
ms.assetid: 149cb875-9b1c-4695-b88a-fbf1725a02f9
author: BrucePerlerMS
ms.openlocfilehash: 19dbf5ed8852ea8d3ad9be078cb575c6e4dc06ed
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65631898"
---
# <a name="wif-claims-programming-model"></a>WIF 클레임 프로그래밍 모델
ASP.NET 및 WCF(Windows Communication Foundation) 개발자는 일반적으로 사용자의 ID 정보 작업에 IIdentity 및 IPrincipal 인터페이스를 사용합니다. .NET 4.5에서는 다음 다이어그램과 같이 이제 모든 보안 주체에 대한 클레임이 항상 표시되도록 WIF(Windows Identity Foundation)가 통합되었습니다.

 ![WIF 클레임 프로그래밍 모델을 보여 주는 다이어그램입니다.](./media/wif-claims-programming-model/wif-claims-programming-model.png)

 .NET 4.5에서는 System.Security.Claims에 새 ClaimsPrincipal 및 ClaimsIdentity 클래스가 포함됩니다(위 다이어그램 참조). .NET의 모든 보안 주체는 이제 ClaimsPrincipal에서 파생됩니다. ASP.NET용 FormsIdentity 및 WindowsIdentity 같은 모든 기본 제공 ID 클래스는 이제 ClaimsIdentity에서 파생됩니다. 마찬가지로, GenericPrincipal 및 WindowsPrincipal 같은 모든 기본 제공 보안 주체 클래스는 ClaimsPrincipal에서 파생됩니다.

 클레임은 <xref:System.Security.Claims.Claim> 클래스로 표현됩니다. 이 클래스에는 다음과 같은 중요한 속성이 있습니다.

- <xref:System.Security.Claims.Claim.Type%2A>은 클레임 형식을 나타내며 일반적으로 URI입니다. 예를 들어 전자 메일 주소 클레임은 라고 `http://schemas.microsoft.com/ws/2008/06/identity/claims/email`합니다.

- <xref:System.Security.Claims.Claim.Value%2A>에는 클레임 값이 포함되며 문자열로 표현됩니다. 으로 전자 메일 주소를 나타낼 수 예를 들어, "someone@contoso.com"입니다.

- <xref:System.Security.Claims.Claim.ValueType%2A>은 클레임 값 형식을 나타내며 일반적으로 URI입니다. 예를 들어 문자열 형식은 `http://www.w3.org/2001/XMLSchema#string`으로 표현됩니다. 값 형식은 XML 스키마에 따라 QName이어야 합니다. WIF에서 유효한 QName 값을 출력할 수 있게 하려면 값이 `namespace#format` 형식이어야 합니다. 네임스페이스가 잘 정의된 네임스페이스가 아닐 경우 해당 네임스페이스에 대해 게시된 XSD 파일이 없으므로 생성된 XML의 스키마 유효성이 검사되지 않을 수 있습니다. 기본값 형식은 `http://www.w3.org/2001/XMLSchema#string`입니다. 안전 하 게 사용할 수 있는 잘 알려진 값 형식에 대 한 자세한 내용은 참조는 [W3C XML 스키마](https://www.w3.org/2001/XMLSchema) 페이지입니다.

- <xref:System.Security.Claims.Claim.Issuer%2A>는 클레임을 발급한 STS(보안 토큰 서비스)의 식별자입니다. `https://sts1.contoso.com/sts` 같은 STS를 나타내는 이름 또는 STS의 URL로 나타낼 수 있습니다.

- <xref:System.Security.Claims.Claim.OriginalIssuer%2A>는 체인에 있는 STS 개수에 관계없이 원래 클레임을 발급한 STS의 식별자입니다. <xref:System.Security.Claims.Claim.Issuer%2A>와 같이 표현됩니다.

- <xref:System.Security.Claims.Claim.Subject%2A>는 ID가 검사되는 주체입니다. SOAP 메시지에 <xref:System.Security.Claims.ClaimsIdentity>이 있습니다.

- <xref:System.Security.Claims.Claim.Properties%2A>는 개발자가 다른 속성과 함께 통신 중에 전송될 응용 프로그램 관련 데이터를 제공할 수 있도록 하는 사전이며, 사용자 지정 유효성 검사에 사용될 수 있습니다.

## <a name="identity-delegation"></a>ID 위임
<xref:System.Security.Claims.ClaimsIdentity>의 중요한 속성은 <xref:System.Security.Claims.ClaimsIdentity.Actor%2A>입니다. 이 속성을 통해 중간 계층이 백 엔드 서비스에 요청을 수행하는 클라이언트 역할을 하는 다계층 시스템에서 자격 증명을 위임할 수 있습니다.

### <a name="accessing-claims-through-threadcurrentprincipal"></a>Thread.CurrentPrincipal을 통해 클레임 액세스
RP 애플리케이션에서 현재 사용자의 클레임 집합에 액세스하려면 `Thread.CurrentPrincipal`을 사용합니다.

다음 코드 샘플은 이 메서드를 사용하여 System.Security.Claims.ClaimsIdentity를 가져오는 방법을 보여 줍니다.

```csharp
ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;
```

자세한 내용은 <xref:System.Security.Claims>을 참조하세요.

### <a name="role-claim-type"></a>역할 클레임 형식
RP 애플리케이션을 구성하는 과정에서 역할 클레임 형식이 결정됩니다. 이 클레임 형식은 System.Security.Claims.ClaimsPrincipal.IsInRole(System.String)에서 사용됩니다. 기본 클레임 형식은 `http://schemas.microsoft.com/ws/2008/06/identity/claims/role`입니다.

### <a name="claims-extracted-by-windows-identity-foundation-from-different-token-types"></a>Windows Identity Foundation이 서로 다른 토큰 형식에서 추출한 클레임
WIF는 기본적으로 여러 가지 인증 메커니즘 조합을 지원합니다. 다음 표에는 WIF가 다양한 토큰 형식에서 추출하는 클레임이 나와 있습니다.

|토큰 형식|클레임 생성|Windows 액세스 토큰에 매핑|
|-|-|-|
|SAML 1.1|1.  System.IdentityModel.SecurityTokenService.GetOutputClaimsIdentity(System.Security.Claims.ClaimsPrincipal,System.IdentityModel.Protocols.WSTrust.RequestSecurityToken,System.IdentityModel.Scope)의 모든 클레임<br />2.  토큰에 증명 토큰이 포함된 경우 확인 키의 XML serialization을 포함하는 `http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey` 클레임<br />3.  Issuer 요소의 `http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername` 클레임<br />4.  토큰에 인증 문이 포함된 경우 AuthenticationMethod 및 AuthenticationInstant 클레임|“SAML 1.1”에 나열된 클레임뿐 아니라 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name` 형식의 클레임을 제외한 Windows 인증 관련 클레임이 추가되고 ID는 WindowsClaimsIdentity로 표현됩니다.|
|SAML 2.0|“SAML 1.1”과 같습니다.|“Windows 계정에 매핑된 SAML 1.1”과 같습니다.|
|X509|1.  X500 고유 이름, emailName, dnsName, SimpleName, UpnName, UrlName, 지문, RsaKey(X509Certificate2.PublicKey.Key 속성에서 RSACryptoServiceProvider.ExportParameters 메서드를 사용하여 추출할 수 있음), DsaKey(X509Certificate2.PublicKey.Key 속성에서 DSACryptoServiceProvider.ExportParameters 메서드를 사용하여 추출할 수 있음), X509 인증서의 SerialNumber 속성을 사용하는 클레임<br />2.  값이 `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509`인 AuthenticationMethod 클레임 XmlSchema DateTime 형식으로 인증서의 유효성을 검사한 시간 값을 가진 AuthenticationInstant 클레임.|1.  Windows 계정 정규화된 도메인 이름을 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name` 클레임 값으로 사용합니다. .<br />2.  Windows에 매핑되지 않은 X509 인증서의 클레임 및 인증서를 Windows에 매핑하여 얻은 Windows 계정의 클레임.|
|UPN|1.  클레임은 Windows 인증 섹션의 클레임과 유사합니다.<br />2.  값이 `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`인 AuthenticationMethod 클레임 XmlSchema DateTime 형식으로 암호의 유효성을 검사한 시간 값을 가진 AuthenticationInstant 클레임.||
|Windows(Kerberos 또는 NTLM)|1.  와 같은 액세스 토큰에서 생성 된 클레임: PrimarySID, DenyOnlyPrimarySID, PrimaryGroupSID, DenyOnlyPrimaryGroupSID, GroupSID, DenyOnlySID, 및 이름<br />2.  값이 `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows`인 AuthenticationMethod XMLSchema DateTime 형식으로 Windows 액세스 토큰이 생성된 시간 값을 가진 AuthenticationInstant||
|RSA 키 쌍|1.  값이 RSAKeyValue인 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/rsa` 클레임<br />2.  값이 `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/signature`인 AuthenticationMethod 클레임 XMLSchema DateTime 형식으로 RSA 키가 인증된(즉, 시그니처가 확인된) 시간 값을 가진 AuthenticationInstant 클레임||

|인증 형식|“AuthenticationMethod” 클레임으로 내보낸 URI|
|-|-|
|암호|`urn:oasis:names:tc:SAML:1.0:am:password`|
|Kerberos|`urn:ietf:rfc:1510`|
|SecureRemotePassword|`urn:ietf:rfc:2945`|
|TLSClient|`urn:ietf:rfc:2246`|
|X509|`urn:oasis:names:tc:SAML:1.0:am:X509-PKI`|
|PGP|`urn:oasis:names:tc:SAML:1.0:am:PGP`|
|Spki|`urn:oasis:names:tc:SAML:1.0:am:SPKI`|
|XmlDSig|`urn:ietf:rfc:3075`|
|지정되지 않음|`urn:oasis:names:tc:SAML:1.0:am:unspecified`|
