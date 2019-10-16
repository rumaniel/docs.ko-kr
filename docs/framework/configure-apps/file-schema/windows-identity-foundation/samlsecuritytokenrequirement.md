---
title: <samlSecurityTokenRequirement>
ms.date: 03/30/2017
ms.assetid: 09202d12-88d3-49cc-953b-703bcc1690eb
author: BrucePerlerMS
ms.openlocfilehash: cab7572518a7a6dc26f8bbcf67cd424fa1c01085
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251897"
---
# <a name="samlsecuritytokenrequirement"></a>\<samlSecurityTokenRequirement>
<xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> 클래스<xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> , 클래스 또는 이러한 클래스 중 하나의 파생 클래스에 대 한 구성을 제공 합니다. <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> 클래스로 표현 됩니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlers >** ](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> 추가**](add.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<samlSecurityTokenRequirement >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add>  
        <samlSecurityTokenRequirement   
            issuerCertificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
            issuerCertificateRevocationMode="NoCheck||Offline||Online"  
            issuerCertificateTrustedStoreLocation="CurrentLocation||LocalMachine"  
            issuerCertificateValidator="Namespace.Class Assembly"  
            mapToWindows=xs:boolean  
          <nameClaimType value=xs:string />  
          <roleClaimType value=xs:string />  
        </samlSecurityTokenRequirement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|mapToWindows|토큰 처리기가 들어오는 UPN 클레임을 사용 하 여 유효성 검사 토큰을 Windows 계정에 매핑할지 여부를 지정 합니다. 기본값은 "false"입니다.|  
|issuerCertificateRevocationMode|X.509 인증서에 사용할 해지 모드를 지정 하는 값입니다.<xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 기본값은 "Online"입니다.|  
|issuerCertificateValidationMode|X.509 인증서에 사용할 유효성 검사 모드를 지정 하는 값입니다.<xref:System.ServiceModel.Security.X509CertificateValidationMode> 기본값은 "PeerOrChainTrust"입니다.|  
|issuerCertificateTrustedStoreLocation|X.509 인증서 저장소를 지정 하는 값입니다.<xref:System.Security.Cryptography.X509Certificates.StoreLocation> 기본값은 "LocalMachine"입니다.|  
|issuerCertificateValidator|에서 <xref:System.IdentityModel.Selectors.X509CertificateValidator>파생 되는 사용자 지정 형식입니다. `issuerCertificateValidationMode` 특성이 "Custom" 이면 발급자 인증서 유효성 검사에이 형식의 인스턴스가 사용 됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<nameClaimType>](nameclaimtype.md)|속성을 <xref:System.Security.Principal.IIdentity.Name%2A> 지정 하는 클레임 유형을 설정 합니다.|  
|[\<roleClaimType>](roleclaimtype.md)|토큰 처리기의 <xref:System.Security.Claims.ClaimsIdentity> <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A> 메서드에서 반환 하는 개체의 컬렉션에서 역할 유형 클레임을 정의 하는 클레임 유형을 지정 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<add>](add.md)|지정 된 보안 토큰 처리기를 토큰 처리기 컬렉션에 추가 합니다.|  
  
## <a name="remarks"></a>설명  
 요소 `<samlSecurityTokenRequirement>` 는 개체 모델에서 <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> 클래스로 표시 되며 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> 또는 <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>에서 `SamlSecurityTokenRequirement` 속성을 구성 하는 데 사용 됩니다.  
  
## <a name="example"></a>예제  
  
```xml  
<add type="System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel">  
    <samlSecurityTokenRequirement issuerCertificateValidationMode="PeerOrChainTrust"  
                                  issuerCertificateRevocationMode="Online"  
                                  issuerCertificateTrustedStoreLocation="LocalMachine"  
                                  mapToWindows="false">  
  
        <nameClaimType value="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" />  
        <roleClaimType value="schemas.microsoft.com/ws/2006/04/identity/claims/role" />  
    </samlSecurityTokenRequirement>  
</add>  
```
