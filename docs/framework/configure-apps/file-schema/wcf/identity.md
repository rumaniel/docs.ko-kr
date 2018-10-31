---
title: '&lt;identity&gt;'
ms.date: 03/30/2017
ms.assetid: c1d2ae56-e231-4a07-9c3f-9f13381dc0d8
ms.openlocfilehash: 74c88df867efa82d48693a3df86b4c7813c40eba
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200048"
---
# <a name="ltidentitygt"></a>&lt;identity&gt;
ID 요소를 사용하면 클라이언트 개발자가 서비스에 필요한 ID를 디자인 타임에 지정할 수 있습니다. 클라이언트와 서비스 간의 핸드셰이크 프로세스에서 Windows Communication Foundation (WCF) 인프라는 되도록 예상 되는 서비스가이 요소의 값과 일치의 id 및 인증 될 수 있습니다. 자세한 내용은 [서비스 Id 및 인증](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)합니다.  
  
 \<system.ServiceModel>  
\<client>  
\<endpoint>  
  
## <a name="syntax"></a>구문  
  
```xml  
<identity>  
    <certificate encodedValue="String"/>  
    <certificateReference findValue="String"   
       isChainIncluded="Boolean"  
       storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"  
       storeLocation="LocalMachine/CurrentUser"  
       X509FindType= Enumeration./>  
    <dns value="String"/>  
    <rsa value="String"/>  
    <servicePrincipalName value="String"/>  
    <usePrincipalName value="String"/>  
</identity>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|certificate|X.509 인증서의 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.CertificateElement> 형식입니다. 이 요소에는 이 인증서로 인코딩된 값을 지정하는 문자열인 `encodedValue` 특성이 포함되어 있습니다.|  
|certificateReference|X.509 인증서 유효성 검사의 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.CertificateReferenceElement> 형식입니다.|  
|dns|서비스를 인증하는 데 사용되는 X.509 인증서의 DNS를 지정합니다. 이 요소에는 문자열인 `value` 특성이 포함되며 실제 ID가 포함됩니다.|  
|rsa|클라이언트에 서비스를 인증하는 데 사용되는 X.509 인증서의 RSA 필드 값을 지정합니다. 이 요소에는 문자열인 `value` 특성이 포함되며 실제 ID가 포함됩니다.|  
|servicePrincipalName|서비스의 인스턴스를 고유하게 식별하기 위해 클라이언트에서 사용하는 사용자 이름인 SPN(서버 사용자 이름) ID를 지정합니다. 이 요소에는 문자열인 `value` 특성이 포함되며 실제 사용자 이름이 포함됩니다. 이 요소는 <xref:System.ServiceModel.Configuration.ServicePrincipalNameElement> 형식입니다.|  
|userPrincipalName|네트워크 사용자의 로그온 이름 형식인 UPN(User Principal Name) ID를 지정합니다. 사용자 계정 이름 뒤에 Active Directory에서 사용 되는 사용자 개체 이름 이루어져는 at 기호 (\@) 그런 다음 일반적으로 부모 도메인 Domain Name System. 예를 들어, Fabrikam.com 도메인 트리에 있는 Jeff 사용자 계정 이름 있을 [ jeff@fabrikam.com ](mailto:jeffsmith@fabrikam.com)합니다.  이 요소에는 문자열인 `value` 특성이 포함되며 실제 사용자 이름이 포함됩니다. 이 요소는 <xref:System.ServiceModel.Configuration.UserPrincipalNameElement> 형식입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<custom>](../../../../../docs/framework/configure-apps/file-schema/wcf/custom.md)|netPeerTcpBinding에 대한 사용자 지정 피어 확인자를 지정합니다.|  
|[\<endpoint>](https://msdn.microsoft.com/library/13aa23b7-2f08-4add-8dbf-a99f8127c017)|다양한 형식의 엔드포인트를 구성합니다.|  
|[\<issuer>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuer.md)|페더레이션 서비스에 대한 STS(보안 토큰 서비스)를 지정합니다.|  
|[\<issuerMetadata>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuermetadata.md)|페더레이션 서비스의 STS(보안 토큰 서비스)에 대한 메타데이터 엔드포인트를 지정합니다.|  
|[\<issuedTokenParameters>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenparameters.md)|사용자 지정 바인딩에서 발급된 토큰에 대한 매개 변수를 정의합니다.|  
|[\<localIssuer>](../../../../../docs/framework/configure-apps/file-schema/wcf/localissuer.md)|로컬 STS(보안 토큰 서비스)를 지정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Configuration.IdentityElement>  
 <xref:System.ServiceModel.EndpointAddress>  
 <xref:System.ServiceModel.EndpointAddress.Identity%2A>  
 [서비스 ID 및 인증](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)  
 [엔드포인트: 주소, 바인딩 및 계약](../../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
