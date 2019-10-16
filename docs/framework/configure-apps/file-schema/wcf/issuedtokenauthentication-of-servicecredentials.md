---
title: <serviceCredentials>의 <issuedTokenAuthentication>
ms.date: 03/30/2017
ms.assetid: 5c2e288f-f603-4d13-839a-0fd6d1981bec
ms.openlocfilehash: 6d468a27ee05fb4dd8cf087d10e5d170783d3454
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400353"
---
# <a name="issuedtokenauthentication-of-servicecredentials"></a>\<serviceCredentials의 \<issuedTokenAuthentication > >
서비스 자격 증명으로 발급된 사용자 지정 토큰을 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceBehaviors >** ](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceCredentials >** ](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<issuedTokenAuthentication >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<issuedTokenAuthentication allowUntrustedRsaIssuers="Boolean"
                           audienceUriMode="Always/BearerKeyOnly/Never"
                           customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"
                           certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"
                           revocationMode="NoCheck/Online/Offline"
                           samlSerializer="String"
                           trustedStoreLocation="CurrentUser/LocalMachine">
  <allowedAudienceUris>
    <add allowedAudienceUri="String" />
  </allowedAudienceUris>
  <knownCertificates>
    <add findValue="String"
         storeLocation="CurrentUser/LocalMachine"
         storeName=" CurrentUser/LocalMachine"
         x509FindType="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
  </knownCertificates>
</issuedTokenAuthentication>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`allowedAudienceUris`|<xref:System.IdentityModel.Tokens.SamlSecurityToken> 인스턴스에서 유효한 대상으로 지정할 수 있는 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> 보안 토큰의 대상 URI 집합을 가져옵니다. 이 특성 사용에 대한 자세한 내용은 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>를 참조하세요.|  
|`allowUntrustedRsaIssuers`|신뢰할 수 없는 RSA 인증서 발급자에 대한 허용 여부를 지정하는 부울 값입니다.<br /><br /> 인증서는 신뢰성 확인을 위해 CA(인증 기관)의 서명을 받습니다. 신뢰할 수 없는 발급자는 인증서 서명을 위한 신뢰성이 지정되지 않은 CA입니다.|  
|`audienceUriMode`|<xref:System.IdentityModel.Tokens.SamlSecurityToken> 보안 토큰의 <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition>에 대해 유효성을 검사해야 하는지 여부를 지정하는 값을 가져옵니다. 이 값은 <xref:System.IdentityModel.Selectors.AudienceUriMode> 형식입니다. 이 특성 사용에 대한 자세한 내용은 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>를 참조하세요.|  
|`certificateValidationMode`|인증서 유효성 검사 모드를 설정합니다. <xref:System.ServiceModel.Security.X509CertificateValidationMode>의 유효한 값 중 하나입니다. `Custom`으로 설정되면 `customCertificateValidator`도 지정해야 합니다. 기본값은 `ChainTrust`입니다.|  
|`customCertificateValidatorType`|선택적 문자열입니다. 사용자 지정 형식의 유효성을 검사하는 데 사용되는 형식 및 어셈블리입니다. 이 특성은 `certificateValidationMode`가 `Custom`으로 설정되어 있을 때 설정해야 합니다.|  
|`revocationMode`|해지 검사의 수행 여부 및 이를 온라인 또는 오프라인으로 수행할지를 지정하는 해지 모드를 설정합니다. 이 특성은 <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 형식입니다.|  
|`samlSerializer`|서비스 자격 증명에 사용되는 SamlSerializer의 형식을 지정하는 선택적 문자열 특성입니다. 기본값은 빈 문자열입니다.|  
|`trustedStoreLocation`|선택적 열거형입니다. 시스템 저장소 위치 `LocalMachine` 또는 `CurrentUser` 중 하나입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|`knownCertificates`|서비스 자격 증명에 대해 신뢰할 수 있는 발급자를 지정하는 <xref:System.ServiceModel.Configuration.X509CertificateTrustedIssuerElement> 요소의 컬렉션을 지정합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<serviceCredentials>](servicecredentials.md)|서비스를 인증하는 데 사용되는 자격 증명 및 클라이언트 자격 증명 유효성 검사 관련 설정을 지정합니다.|  
  
## <a name="remarks"></a>설명  
 발급된 토큰 시나리오에는 3단계가 있습니다. 첫 번째 단계에서는 서비스에 액세스 하려는 클라이언트를 *보안 토큰 서비스*라고 합니다. 보안 토큰 서비스는 클라이언트를 인증한 다음 일반적으로 SAML(Security Assertions Markup Language) 토큰이라는 클라이언트 토큰을 발급합니다. 클라이언트는 토큰을 통해 서비스에 반환됩니다. 서비스는 토큰 및 해당 클라이언트를 인증할 수 있는 데이터의 토큰을 검사합니다. 토큰을 인증하려면 보안 토큰 서비스가 사용하는 인증서를 서비스가 인식해야 합니다.  
  
 이 요소는 이러한 보안 토큰 서비스 인증서에 대한 리포지토리입니다. 인증서를 추가 하려면 [ \<> knowncertificates](knowncertificates.md)를 사용 합니다. 다음 예제와 같이 각 인증서에 대 한 [ 추가>를삽입합니다.\<](add-of-knowncertificates.md)  
  
```xml  
<issuedTokenAuthentication>
  <knownCertificates>
    <add findValue="www.contoso.com"
         storeLocation="LocalMachine"
         storeName="My"
         X509FindType="FindBySubjectName" />
  </knownCertificates>
</issuedTokenAuthentication>
```  
  
 기본적으로 인증서는 보안 토큰 서비스에서 가져와야 합니다. 이러한 "알려진" 인증서는 올바른 클라이언트만 서비스에 액세스할 수 있도록 합니다.  
  
 이 구성 요소를 [사용 하는 방법에 대 한 자세한 내용은 방법: 페더레이션 서비스](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)에 대 한 자격 증명을 구성 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>
- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.IssuedTokenAuthentication%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement>
- <xref:System.ServiceModel.Description.ServiceCredentials.IssuedTokenAuthentication%2A>
- <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>
- [서비스 및 클라이언트에 보안 설정](../../../wcf/feature-details/securing-services-and-clients.md)
- [방법: 페더레이션 서비스에 대 한 자격 증명 구성](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
