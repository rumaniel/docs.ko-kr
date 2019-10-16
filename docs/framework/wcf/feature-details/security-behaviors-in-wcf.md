---
title: WCF의 보안 동작
ms.date: 03/30/2017
ms.assetid: 513232c0-39fd-4409-bda6-5ebd5e0ea7b0
ms.openlocfilehash: 378edb6ddd7a66249a0c7548a3d9465475f670a8
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487756"
---
# <a name="security-behaviors-in-wcf"></a>WCF의 보안 동작
Windows Communication Foundation (WCF), 동작 서비스 수준 또는 끝점 수준에서 런타임 동작을 수정합니다. (일반적으로 참조 동작에 대 한 자세한 내용은 [서비스 런타임 동작 지정](../../../../docs/framework/wcf/specifying-service-run-time-behavior.md).) *보안 동작* 감사 로그 및 자격 증명, 인증, 권한 부여에 대 한 제어를 허용 합니다. 프로그래밍 또는 구성을 통해 동작을 사용할 수 있습니다. 이 항목에서는 보안 기능과 관련된 다음 동작의 구성에 대해 중점적으로 설명합니다.  
  
- [\<serviceCredentials>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md).  
  
- [\<clientCredentials>](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md).  
  
- [\<serviceAuthorization>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md).  
  
- [\<serviceSecurityAudit>](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md).  
  
- [\<serviceMetadata >](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md), 또한 클라이언트가 메타 데이터에 액세스할 수 있는 보안 끝점을 지정할 수 있습니다.  
  
## <a name="setting-credentials-with-behaviors"></a>동작을 통한 자격 증명 설정  
 사용 된 [ \<serviceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md) 및 [ \<clientCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) 서비스 또는 클라이언트에 대 한 자격 증명 값을 설정 합니다. 기본 바인딩 구성은 자격 증명을 설정해야 할지 여부를 결정합니다. 예를 들어, 보안 모드가 `None`으로 설정된 경우 클라이언트 및 서비스 둘 다 서로 간에 인증되지 않으며 모든 형식의 자격 증명이 필요하지 않습니다.  
  
 반면에 서비스 바인딩의 경우 클라이언트 자격 증명 형식이 필요할 수 있습니다. 이러한 경우, 동작을 사용하여 자격 증명 값을 설정해야 합니다. (가능한 유형의 자격 증명에 대 한 자세한 내용은 참조 하세요. [자격 증명 유형을 선택 하면](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md).) Windows 자격 증명을 사용하여 인증하는 것과 같은 일부의 경우, 환경에서 자동으로 실제 자격 증명 값을 설정하기 때문에 다른 자격 증명 집합을 지정하려고 하지 않는 한 자격 증명 값을 명시적으로 설정할 필요가 없습니다.  
  
 모든 서비스 자격 증명의 자식 요소로 발견 되는 [ \<serviceBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)합니다. 다음 예제에서는 서비스 자격 증명으로 사용되는 인증서를 보여 줍니다.  
  
```xml  
<configuration>  
 <system.serviceModel>  
  <behaviors>  
   <serviceBehaviors>  
    <behavior name="ServiceBehavior1">  
     <serviceCredentials>  
      <serviceCertificate findValue="000000000000000000000000000"   
                          storeLocation="CurrentUser"  
      storeName="Root" x509FindType="FindByThumbprint" />  
     </serviceCredentials>  
    </behavior>  
   </serviceBehaviors>  
  </behaviors>  
 </system.serviceModel>  
</configuration>  
```  
  
## <a name="service-credentials"></a>서비스 자격 증명  
 합니다 [ \<serviceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md) 네 개의 자식 요소를 포함 합니다. 요소 및 사용법에 대해서는 다음 단원에서 설명합니다.  
  
### <a name="servicecertificate-element"></a>\<serviceCertificate > 요소  
 이 요소를 사용하여 메시지 보안 모드를 사용하는 클라이언트에 대한 서비스를 인증하는 데 사용할 X.509 인증서를 지정합니다. 주기적으로 갱신되는 인증서를 사용하는 경우 지문이 변경됩니다. 이러한 경우 인증서를 동일한 주체 이름으로 다시 발급할 수 있기 때문에 주체 이름으로 `X509FindType`을 사용합니다.  
  
 요소를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: 클라이언트 자격 증명 값 지정](../../../../docs/framework/wcf/how-to-specify-client-credential-values.md)합니다.  
  
### <a name="certificate-of-clientcertificate-element"></a>\<인증서 >의 \<clientCertificate > 요소  
 사용 된 [ \<인증서 >](../../../../docs/framework/configure-apps/file-schema/wcf/certificate-of-clientcertificate-element.md) 요소 서비스에 통신 하기 위해 안전 하 게 클라이언트를 사용 하 여 클라이언트의 인증서가 있어야 합니다. 이는 양방향 통신 패턴을 사용하는 경우 발생합니다. 대부분의 일반적인 요청-회신 패턴의 경우, 클라이언트는 요청 시 서비스가 클라이언트에게 해당 응답을 안전하게 보내기 위해 사용하는 인증서를 포함합니다. 그러나 양방향 통신 패턴에는 요청 및 회신이 없습니다. 서비스는 통신에서 클라이언트의 인증서를 유추할 수 없기 때문에 서비스는 클라이언트에 대해 메시지 보안을 유지하기 위해 클라이언트 인증서를 필요로 합니다. 클라이언트 인증서를 out-of-band 방식으로 가져와서 이 요소를 사용하여 인증서를 지정해야 합니다. 이중 서비스에 대 한 자세한 내용은 참조 하세요. [방법: 이중 계약 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)합니다.  
  
### <a name="authentication-of-clientcertificate-element"></a>\<인증 >의 \<clientCertificate > 요소  
 합니다 [ \<인증 >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md) 요소를 사용 하면 클라이언트를 인증 하는 방법을 사용자 지정할 수 있습니다. `CertificateValidationMode` 특성을 `None`, `ChainTrust`, `PeerOrChainTrust`, `PeerTrust` 또는 `Custom`으로 설정할 수 있습니다. 기본적으로 수준 설정 `ChainTrust`에서 종료 되는 인증서의 계층 구조에서 각 인증서를 찾을 수 해야를 지정 하는 *루트 기관* 체인의 맨 위에 있는 합니다. 이 모드가 가장 안전한 모드입니다. 또한 값을 `PeerOrChainTrust`로 설정할 수 있으며, 이는 자체 발급된 인증서(신뢰 피어)가 신뢰 체인에 있는 인증서와 함께 수락됨을 지정합니다. 자체 발급 인증서를 신뢰할 수 있는 기관에서 구입할 필요 없기 때문에 클라이언트 및 서비스를 개발 및 디버깅하는 경우 이 값이 사용됩니다. 클라이언트를 배포하는 경우 `ChainTrust` 값을 대신 사용합니다. 또한 값을 `Custom`으로 설정할 수도 있습니다. `Custom` 값으로 설정할 경우 `CustomCertificateValidatorType` 특성도 인증서 유효성을 검사하는 데 사용되는 어셈블리 및 형식으로 설정해야 합니다. 사용자 지정 유효성 검사기를 만들려면 추상 <xref:System.IdentityModel.Selectors.X509CertificateValidator> 클래스에서 상속해야 합니다.  
  
### <a name="issuedtokenauthentication-element"></a>\<issuedTokenAuthentication > 요소  
 발급된 토큰 시나리오에는 3단계가 있습니다. 첫 번째 단계에서는 서비스에 액세스 하려는 클라이언트 라고 한 *보안 토큰 서비스* (STS). STS는 클라이언트를 인증한 다음 일반적으로 SAML(Security Assertions Markup Language) 토큰이라는 클라이언트 토큰을 발급합니다. 클라이언트는 토큰을 통해 서비스에 반환됩니다. 서비스는 토큰 및 해당 클라이언트를 인증할 수 있는 데이터의 토큰을 검사합니다. 토큰을 인증하려면 보안 토큰 서비스가 사용하는 인증서를 서비스가 인식해야 합니다. 합니다 [ \<issuedTokenAuthentication >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md) 요소는 이러한 보안 토큰 서비스 인증서에 대 한 리포지토리입니다. 인증서를 추가 하려면 사용 합니다 [ \<knownCertificates >](../../../../docs/framework/configure-apps/file-schema/wcf/knowncertificates.md)합니다. 삽입 된 [ \<추가 >](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-knowncertificates.md) 다음 예와에서 같이 각 인증서에 대 한 합니다.  
  
```xml  
<issuedTokenAuthentication>  
   <knownCertificates>  
      <add findValue="www.contoso.com"   
           storeLocation="LocalMachine" storeName="My"   
           X509FindType="FindBySubjectName" />  
    </knownCertificates>  
</issuedTokenAuthentication>  
```  
  
 기본적으로 인증서는 보안 토큰 서비스에서 가져와야 합니다. 이러한 "알려진" 인증서는 올바른 클라이언트만 서비스에 액세스할 수 있도록 합니다.  
  
 사용 해야 합니다 [ \<allowedAudienceUris >](../../../../docs/framework/configure-apps/file-schema/wcf/allowedaudienceuris.md) 활용 하는 페더레이션된 응용 프로그램에서 컬렉션을 *보안 토큰 서비스* 발급 (STS) `SamlSecurityToken` 보안 토큰입니다. STS는 보안 토큰을 발급할 때 보안 토큰에 `SamlAudienceRestrictionCondition`을 추가하여 보안 토큰을 사용할 웹 서비스의 URI를 지정할 수 있습니다. 따라서 발급된 보안 토큰이 해당 웹 서비스용인지 검사하도록 지정하여 수신자 웹 서비스의 `SamlSecurityTokenAuthenticator`가 이를 확인하도록 할 수 있습니다. 이렇게 하려면 다음을 수행하세요.  
  
- 설정 합니다 `audienceUriMode` 의 특성 [ \<issuedTokenAuthentication >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md) 하 `Always` 또는 `BearerKeyOnly`합니다.  
  
- 이 컬렉션에 URI를 추가하여 유효한 URI 집합을 지정합니다. 이 작업을 수행 하려면 삽입는 [ \<추가 >](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-allowedaudienceuris.md) 각 URI에 대 한  
  
 자세한 내용은 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>을 참조하세요.  
  
 이 구성 요소를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: 페더레이션 서비스에서 자격 증명 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)합니다.  
  
#### <a name="allowing-anonymous-cardspace-users"></a>익명 CardSpace 사용자 허용  
 `AllowUntrustedRsaIssuers` 요소의 `<IssuedTokenAuthentication>` 특성을 `true`로 설정하면 명시적으로 클라이언트가 임의 RSA 키 쌍으로 서명된 자체 발급 토큰을 제공할 수 있습니다. 발급자 *신뢰할 수 없는* 키에 연결 된 발급자 데이터가 없습니다. CardSpace 사용자 id의 자체 제공된 클레임이 포함 된 자체 발급 된 카드를 만들 수 있습니다. 이 기능은 주의하여 사용하십시오. 이 기능을 사용하려면 사용자 이름과 함께 데이터베이스에 저장되어야 하는 보다 안전한 암호로 RSA 공개 키를 설정합니다. 클라이언트가 서비스에 액세스하도록 허용하기 전에 클라이언트에서 제공하는 RSA 공개 키를 제공된 사용자 이름에 대해 저장된 공개 키와 비교하여 확인합니다. 이것은 사용자가 사용자 이름을 등록하고 자체 발급된 RSA 공개 키와 연결할 수 있는 등록 프로세스를 설정한 것으로 간주합니다.  
  
## <a name="client-credentials"></a>클라이언트 자격 증명  
 클라이언트 자격 증명은 상호 인증이 필요한 경우 서비스에 대해 클라이언트를 인증하는 데 사용됩니다. 또한 클라이언트가 서비스 인증서를 사용하여 서비스에 대한 메시지 보안을 유지해야 하는 경우 서비스 인증서를 지정하는 데 사용할 수 있습니다.  
  
 보안 토큰 서비스 또는 토큰 로컬 발급자로부터 발급된 토큰을 사용하도록 클라이언트를 페더레이션 시나리오의 일부로 구성할 수 있습니다. 페더레이션된 시나리오에 대 한 자세한 내용은 참조 하세요. [페더레이션 및 발급 된 토큰](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)합니다. 아래에 나와 있는 모든 클라이언트 자격 증명을 [ \<endpointBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md)다음 코드에 표시 된 것 처럼 합니다.  
  
```xml  
<behaviors>  
 <endpointBehaviors>  
  <behavior name="EndpointBehavior1">  
   <clientCredentials>  
    <clientCertificate findValue="cn=www.contoso.com"     
        storeLocation="LocalMachine"  
        storeName="AuthRoot" x509FindType="FindBySubjectName" />  
    <serviceCertificate>  
     <defaultCertificate findValue="www.cohowinery.com"   
                    storeLocation="LocalMachine"  
                    storeName="Root" x509FindType="FindByIssuerName" />  
    <authentication revocationMode="Online"  
                    trustedStoreLocation="LocalMachine" />  
    </serviceCertificate>  
   </clientCredentials>  
  </behavior>  
 </endpointBehaviors>  
```  
  
#### <a name="clientcertificate-element"></a>\<clientCertificate > 요소  
 이 요소로 클라이언트를 인증하는 데 사용하는 인증서를 설정합니다. 자세한 내용은 [방법: 클라이언트 자격 증명 값 지정](../../../../docs/framework/wcf/how-to-specify-client-credential-values.md)합니다.  
  
#### <a name="httpdigest"></a>\<httpDigest>  
 이 기능은 Windows 및 IIS(인터넷 정보 서비스)의 Active Directory를 통해 사용해야 합니다. 자세한 내용은 [IIS 6.0의 다이제스트 인증](https://go.microsoft.com/fwlink/?LinkId=88443)합니다.  
  
#### <a name="issuedtoken-element"></a>\<issuedToken > 요소  
 합니다 [ \<issuedToken >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md) 토큰 또는 보안 토큰 서비스를 사용 하는 동작의 로컬 발급자를 구성 하는 데 필요한 요소를 포함 합니다. 로컬 발급자를 사용 하는 클라이언트를 구성 하는 방법에 지침을 참조 하세요. [방법: 로컬 발급자 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)합니다.  
  
#### <a name="localissueraddress"></a>\<localIssuerAddress>  
 기본 보안 토큰 서비스 주소를 지정합니다. 이 때를 <xref:System.ServiceModel.WSFederationHttpBinding> 페더레이션 바인딩의 발급자 주소가 때 또는 보안 토큰 서비스에 대 한 URL을 제공 하지 않습니다 `http://schemas.microsoft.com/2005/12/ServiceModel/Addressing/Anonymous` 또는 `null`합니다. 이러한 경우 로컬 발급자의 주소와 이 발급자와 통신하는 데 사용할 바인딩을 사용하여 <xref:System.ServiceModel.Description.ClientCredentials>를 구성해야 합니다.  
  
#### <a name="issuerchannelbehaviors"></a>\<issuerChannelBehaviors>  
 사용 합니다 [ \<issuerChannelBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/issuerchannelbehaviors-element.md) 보안 토큰 서비스와 통신할 때 사용 되는 WCF 클라이언트 동작을 추가 합니다. 클라이언트 동작을 정의 합니다 [ \<endpointBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md) 섹션입니다. 정의 된 동작을 사용 하려면 추가 <`add`> 요소는 `<issuerChannelBehaviors>` 두 특성을 가진 요소입니다. 다음 예제와 같이 `issuerAddress`를 보안 토큰 서비스의 URL로 설정하고 `behaviorConfiguration` 특성을 정의된 엔드포인트 동작 이름으로 설정합니다.  
  
```xml  
<clientCredentials>  
   <issuedToken>  
      <issuerChannelBehaviors>  
         <add issuerAddress="http://www.contoso.com"  
               behaviorConfiguration="clientBehavior1" />     
```  
  
#### <a name="servicecertificate-element"></a>\<serviceCertificate > 요소  
 이 요소를 사용하여 서비스 인증서의 인증을 제어합니다.  
  
 합니다 [ \<defaultCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/defaultcertificate-element.md) 요소는 서비스 인증서를 지정 하는 경우 사용 하는 단일 인증서를 저장할 수 있습니다.  
  
 사용 합니다 [ \<scopedCertificates >](../../../../docs/framework/configure-apps/file-schema/wcf/scopedcertificates-element.md) 및 [ \<추가 >](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-scopedcertificates-element.md) 특정 서비스와 연결 된 서비스 인증서를 설정 합니다. `<add>` 요소에는 인증서를 서비스와 연결하는 데 사용되는 `targetUri` 특성이 포함되어 있습니다.  
  
 합니다 [ \<인증 >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md) 요소는 인증서를 인증 하는 데 사용 되는 신뢰 수준을 지정 합니다. 기본적으로 수준은 "ChainTrust"로 설정되며 이는 각 인증서가 체인 맨 위의 신뢰할 수 있는 인증 기관에서 종료되는 인증서의 계층 구조에 있어야 함을 지정합니다. 이 모드가 가장 안전한 모드입니다. 또한 값을 "PeerOrChainTrust"로 설정할 수 있으며, 이는 자체 발급된 인증서(신뢰 피어)가 신뢰 체인에 있는 인증서와 함께 수락됨을 지정합니다. 자체 발급 인증서를 신뢰할 수 있는 기관에서 구입할 필요 없기 때문에 클라이언트 및 서비스를 개발 및 디버깅하는 경우 이 값이 사용됩니다. 클라이언트를 배포하는 경우 "ChainTrust" 값을 대신 사용합니다. 또한 값을 "Custom" 또는 "None"으로 설정할 수 있습니다. "Custom" 값을 사용하려면 `CustomCertificateValidatorType` 특성도 인증서 유효성을 검증하는 데 사용되는 어셈블리 및 형식으로 설정해야 합니다. 사용자 지정 유효성 검사기를 만들려면 추상 <xref:System.IdentityModel.Selectors.X509CertificateValidator> 클래스에서 상속해야 합니다. 자세한 내용은 [방법: 사용자 지정 인증서 유효성 검사기를 사용 하는 서비스 만들기](../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)합니다.  
  
 [ \<인증 >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md) 요소를 포함 한 `RevocationMode` 인증서 해지 확인 하는 방법을 지정 하는 특성입니다. 기본값은 "online"이며, 이는 인증서 해지 여부를 자동으로 검사함을 나타냅니다. 자세한 내용은 [Working with Certificates](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)합니다.  
  
## <a name="serviceauthorization"></a>ServiceAuthorization  
 합니다 [ \<serviceAuthorization >](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md) 요소 권한 부여, 사용자 지정 역할 공급자 및 가장에 영향을 주는 요소를 포함 합니다.  
  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 클래스는 서비스 메서드에 적용됩니다. 특성은 보호된 메서드의 사용 권한을 부여할 때 사용할 사용자 그룹을 지정합니다. 기본값은 "UseWindowsGroups"이며 리소스에 액세스하려는 ID에 대해 "Administrators" 또는 "Users"와 같은 Windows 그룹을 검색하도록 지정합니다. "하도록 UseAspNetRoles"를 지정할 수도 있습니다 아래에서 구성 된 사용자 지정 역할 공급자를 사용 하는 <`system.web` > 요소를 다음 코드와 같이 합니다.  
  
```xml  
<system.web>  
  <membership defaultProvider="SqlProvider"   
   userIsOnlineTimeWindow="15">  
     <providers>  
       <clear />  
       <add   
          name="SqlProvider"   
          type="System.Web.Security.SqlMembershipProvider"   
          connectionStringName="SqlConn"  
          applicationName="MembershipProvider"  
          enablePasswordRetrieval="false"  
          enablePasswordReset="false"  
          requiresQuestionAndAnswer="false"  
          requiresUniqueEmail="true"  
          passwordFormat="Hashed" />  
     </providers>  
   </membership>  
  <!-- Other configuration code not shown.-->  
</system.web>  
```  
  
 다음 코드에서는 `roleProviderName` 특성과 함께 사용되는 `principalPermissionMode`을 보여 줍니다.  
  
```xml  
<behaviors>  
 <behavior name="ServiceBehaviour">          
  <serviceAuthorization principalPermissionMode ="UseAspNetRoles"   
                        roleProviderName ="SqlProvider" />  
</behavior>   
   <!-- Other configuration code not shown. -->  
</behaviors>  
```  
  
## <a name="configuring-security-audits"></a>보안 감사 구성  
 사용 하 여는 [ \<serviceSecurityAudit >](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md) 쓸 로그 및 지정 유형의 로그온 이벤트입니다. 자세한 내용은 [감사](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)합니다.  
  
```xml  
<system.serviceModel>  
<serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceSecurityAudit auditLogLocation="Application"   
             suppressAuditFailure="true"  
             serviceAuthorizationAuditLevel="Success"   
             messageAuthenticationAuditLevel="Success" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
## <a name="secure-metadata-exchange"></a>보안 메타데이터 교환  
 메타데이터를 클라이언트로 내보내기는 구성 및 클라이언트 코드를 다운로드할 수 있기 때문에 서비스 및 클라이언트 개발자에게 편리한 기능입니다. 악의적인 사용자에 대한 서비스 노출을 줄이기 위해 HTTPS(HTTP를 통한 SSL) 메커니즘을 사용하여 전송 보안을 유지할 수 있습니다. 이렇게 하려면 먼저 적절한 X.509 인증서를 서비스를 호스트하는 컴퓨터의 특정 포트에 바인딩해야 합니다. (자세한 내용은 [Working with Certificates](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).) 둘째, 추가 [ \<serviceMetadata >](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md) 서비스 구성 및 설정 하는 `HttpsGetEnabled` 특성을 `true`입니다. 마지막으로 다음 예제와 같이 `HttpsGetUrl` 특성을 서비스 메타데이터 엔드포인트의 URL로 설정합니다.  
  
```xml  
<behaviors>  
 <serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceMetadata httpsGetEnabled="true"   
     httpsGetUrl="https://myComputerName/myEndpoint" />  
  </behavior>  
 </serviceBehaviors>  
</behaviors>  
```  
  
## <a name="see-also"></a>참고자료

- [감사](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)
- [Windows Server appfabric 보안 모델](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
