---
title: 클레임 및 토큰
ms.date: 03/30/2017
helpviewer_keywords:
- claims [WCF], and tokens
ms.assetid: eff167f3-33f8-483d-a950-aa3e9f97a189
ms.openlocfilehash: 6d148bca56cfa4e28c2d3e6c0d9fcb564861a7cd
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663456"
---
# <a name="claims-and-tokens"></a>클레임 및 토큰

이 항목에서는 Windows Communication Foundation (WCF) 지원 되는 기본 토큰 으로부터 만드는 다양 한 클레임 형식을 설명 합니다.

<xref:System.IdentityModel.Claims.ClaimSet> 및 <xref:System.IdentityModel.Claims.Claim> 클래스를 사용하여 클라이언트 자격 증명 클레임을 검사할 수 있습니다. `ClaimSet`에는 `Claim` 개체의 컬렉션이 포함됩니다. 각 `Claim`의 중요한 멤버는 다음과 같습니다.

- <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> 속성은 생성하는 클레임의 형식을 지정하는 URI(Uniform Resource Identifier)를 반환합니다. 예를 들어, 클레임 유형을 있는 경우 URI는 인증서의 지문의 않을 `http://schemas.microsoft.com/ws/20005/05/identity/claims/thumprint`합니다.

- <xref:System.IdentityModel.Claims.Claim.Right%2A> 속성은 클레임의 권한을 지정하는 URI를 반환합니다. 미리 정의된 권한은 <xref:System.IdentityModel.Claims.Rights> 클래스(<xref:System.IdentityModel.Claims.Rights.Identity%2A>,  <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>)에 있습니다.

- <xref:System.IdentityModel.Claims.Claim.Resource%2A> 속성은 클레임과 연결된 리소스를 반환합니다.

또한 각 <xref:System.IdentityModel.Claims.ClaimSet>에는 <xref:System.IdentityModel.Claims.ClaimSet.Issuer%2A> 속성이 있습니다. 이 속성은 <xref:System.IdentityModel.Claims.ClaimSet>의 `Issuer`를 나타냅니다.

## <a name="windows-accounts"></a>Windows 계정

클라이언트 자격 증명이 Windows 사용자 계정에 매핑되는 경우 결과 <xref:System.IdentityModel.Claims.ClaimSet>의 값은 다음과 같습니다.

- `Issuer`는 <xref:System.IdentityModel.Claims.ClaimSet> 클래스의 정적 Windows 속성에 의해 반환되는 값입니다.

- 컬렉션의 클레임은 다음과 같습니다.

  - <xref:System.IdentityModel.Claims.Claim> 값이 SID(보안 ID)이고, <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> 속성 값이 <xref:System.IdentityModel.Claims.Claim.Right%2A>이고, `Identity`가 실제 SID 값을 반환하는 <xref:System.IdentityModel.Claims.Claim.Resource%2A>. SID는 도메인 컨트롤러에서 모든 사용자에게 발급하는 고유한 값입니다. SID는 Windows 보안과 상호 작용하여 사용자를 식별하는 데 사용됩니다.

  - <xref:System.IdentityModel.Claims.Claim> 값이 SID이고, <xref:System.IdentityModel.Claims.Claim.ClaimType%2A>가 <xref:System.IdentityModel.Claims.Claim.Right%2A>이고, `PossessProperty`가 SID 값인 <xref:System.IdentityModel.Claims.Claim.Resource%2A>.

  - <xref:System.IdentityModel.Claims.Claim>이 <xref:System.IdentityModel.Claims.Claim.ClaimType%2A>이고, <xref:System.IdentityModel.Claims.ClaimTypes.Name%2A>가 <xref:System.IdentityModel.Claims.Claim.Right%2A>이고, `PossessProperty`가 사용자 이름을 포함하는 문자열(예: "MYMACHINE\Bob")인 <xref:System.IdentityModel.Claims.Claim.Resource%2A>.

  - 사용자가 속하는 다양한 그룹에 대한 <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>를 가진 추가 SID 클레임

## <a name="certificates"></a>인증서

클라이언트 자격 증명이 인증서이면 결과 <xref:System.IdentityModel.Claims.ClaimSet> 값은 다음과 같습니다.

- 자체 발급된 인증서의 경우 `Issuer`는 <xref:System.IdentityModel.Claims.ClaimSet> 자체입니다. <xref:System.IdentityModel.Claims.ClaimSet>는 <xref:System.IdentityModel.Claims.Claim.ClaimType%2A>의 <xref:System.IdentityModel.Claims.ClaimTypes.Thumbprint%2A>, <xref:System.IdentityModel.Claims.Claim.Right%2A>의 `Identity` 및 <xref:System.IdentityModel.Claims.Claim.Resource%2A> 값(인증서의 지문을 포함하는 <xref:System.Byte> 배열)을 반환합니다.

- 인증 기관에서 발급한 인증서의 경우 발급자는 인증 기관의 인증서를 나타내는 `ClaimSet`입니다.

- 컬렉션의 `Claims`는 다음과 같습니다.

  - `Claim`이 지문이고, `ClaimType`가 PossessProperty이고, `Right`가 인증서의 지문을 포함하는 바이트 배열인 `Resource`

  - X500DistinguishedName, Dns, Name, Upn 및 Rsa를 포함하여 다양한 형식의 추가 PossessProperty 클레임이 인증서의 다양한 속성을 나타냅니다. Rsa 클레임에 대 한 리소스에는 인증서에 연결 된 공용 키입니다. **참고** 클라이언트 자격 증명 형식이 인증서 서비스는 Windows에 매핑되는 계정에 두 개의 `ClaimSet` 개체가 생성 됩니다. 첫 번째 개체는 Windows 계정과 관련된 모든 클레임을 포함하고 두 번째 개체는 인증서와 관련된 모든 클레임을 포함합니다.

## <a name="user-namepassword"></a>사용자 이름/암호

클라이언트 자격 증명이 Windows 계정에 매핑되지 않는 사용자 이름/암호(또는 동등한 형식)인 경우 결과 `ClaimSet`는 <xref:System.IdentityModel.Claims.ClaimSet.System%2A> 클래스의 static `ClaimSet` 속성에 의해 발급됩니다. `ClaimSet` 포함는 `Identity` 형식의 클레임 <xref:System.IdentityModel.Claims.ClaimTypes.Name%2A> 해당 리소스는 사용자 이름 클라이언트를 제공 합니다. 해당 클레임에는 `Right`의 `PossessProperty`이 있습니다.

## <a name="rsa-keys"></a>RSA 키

인증서를 사용 하 여 연결 되지 않은 RSA 키를 사용 하는 결과 `ClaimSet` 는 자체 발급 되며 포함을 `Identity` 형식의 클레임 <xref:System.IdentityModel.Claims.ClaimTypes.Rsa%2A> 해당 리소스가 RSA 키인 합니다. 해당 클레임에는 `Right`의 `PossessProperty`이 있습니다.

## <a name="saml"></a>SAML

클라이언트가 SAML(Security Assertions Markup Language) 토큰으로 인증되는 경우 결과 `ClaimSet`는 SAML 토큰에 서명한 엔터티에 의해 발급되며, SAML 토큰에 서명한 STS(보안 토큰 서비스) 인증서에 의해 발급되는 경우도 있습니다. `ClaimSet`는 SAML 토큰에 있는 다양한 클레임을 포함합니다. SAML 토큰에 `SamlSubject`이 아닌 이름을 가진 `null`가 있는 경우 형식이 `Identity`이고 리소스 형식이 <xref:System.IdentityModel.Claims.ClaimTypes.NameIdentifier%2A>인 <xref:System.IdentityModel.Tokens.SamlNameIdentifierClaimResource> 클레임이 만들어집니다.

## <a name="identity-claims-and-servicesecuritycontextisanonymous"></a>ID 클레임 및 ServiceSecurityContext.IsAnonymous

없으면 합니다 `ClaimSet` 클라이언트 자격 증명에서 생성 하는 개체에 클레임을 포함을 `Right` 의 `Identity,` 그런 다음 <xref:System.ServiceModel.ServiceSecurityContext.IsAnonymous%2A> 속성에서 반환 `true`합니다. 그런 클레임이 하나 이상 있는 경우 `IsAnonymous` 속성은 `false`를 반환합니다.

## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Claims.ClaimSet>
- <xref:System.IdentityModel.Claims.Claim>
- <xref:System.IdentityModel.Claims.Rights>
- <xref:System.IdentityModel.Claims.ClaimTypes>
- [ID 모델을 사용하여 클레임 및 권한 부여 관리](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)
