---
title: <identity>
ms.date: 03/30/2017
ms.assetid: c1d2ae56-e231-4a07-9c3f-9f13381dc0d8
ms.openlocfilehash: 15c9e38a141fc294c47863b1a932711444ac079a
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855147"
---
# <a name="identity"></a>\<identity>
ID 요소를 사용하면 클라이언트 개발자가 서비스에 필요한 ID를 디자인 타임에 지정할 수 있습니다. 클라이언트와 서비스 간의 핸드셰이크 프로세스에서 WCF (Windows Communication Foundation) 인프라는 예상 되는 서비스의 id가이 요소의 값과 일치 하는지 확인 하므로 인증 될 수 있습니다. 자세한 내용은 [서비스 Id 및 인증](../../../wcf/feature-details/service-identity-and-authentication.md)합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<클라이언트 >** ](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<끝점 >** ](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<id >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<identity>
  <certificate encodedValue="String" />
  <certificateReference findValue="String"
                        isChainIncluded="Boolean"
                        storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                        storeLocation="LocalMachine/CurrentUser"
                        X509FindType="Enumeration" />
  <dns value="String" />
  <rsa value="String" />
  <servicePrincipalName value="String" />
  <userPrincipalName value="String" />
</identity>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|인증서(certificate)|X.509 인증서의 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.CertificateElement> 형식입니다. 이 요소에는 이 인증서로 인코딩된 값을 지정하는 문자열인 `encodedValue` 특성이 포함되어 있습니다.|  
|certificateReference|X.509 인증서 유효성 검사의 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.CertificateReferenceElement> 형식입니다.|  
|dns|서비스를 인증하는 데 사용되는 X.509 인증서의 DNS를 지정합니다. 이 요소에는 문자열인 `value` 특성이 포함되며 실제 ID가 포함됩니다.|  
|rsa|클라이언트에 서비스를 인증하는 데 사용되는 X.509 인증서의 RSA 필드 값을 지정합니다. 이 요소에는 문자열인 `value` 특성이 포함되며 실제 ID가 포함됩니다.|  
|servicePrincipalName|서비스의 인스턴스를 고유하게 식별하기 위해 클라이언트에서 사용하는 사용자 이름인 SPN(서버 사용자 이름) ID를 지정합니다. 이 요소에는 문자열인 `value` 특성이 포함되며 실제 사용자 이름이 포함됩니다. 이 요소는 <xref:System.ServiceModel.Configuration.ServicePrincipalNameElement> 형식입니다.|  
|userPrincipalName|네트워크 사용자의 로그온 이름 형식인 UPN(User Principal Name) ID를 지정합니다. 사용자 계정 이름은 Active Directory에 사용 되는 사용자 개체 이름, 기호 (\@), 일반적으로 도메인 이름 시스템 부모 도메인으로 구성 됩니다. 예를 들어, Fabrikam.com 도메인 트리에 있는 Jeff 사용자 계정 이름 있을 [ jeff@fabrikam.com ](mailto:jeffsmith@fabrikam.com)합니다.  이 요소에는 문자열인 `value` 특성이 포함되며 실제 사용자 이름이 포함됩니다. 이 요소는 <xref:System.ServiceModel.Configuration.UserPrincipalNameElement> 형식입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<custom>](custom.md)|netPeerTcpBinding에 대한 사용자 지정 피어 확인자를 지정합니다.|  
|[\<endpoint>](endpoint-element.md)|서비스 끝점을 구성 합니다.|  
|[\<클라이언트 >의 \<끝점 >](endpoint-of-client.md)|채널 끝점을 구성 합니다.|  
|[\<issuer>](issuer.md)|페더레이션 서비스에 대한 STS(보안 토큰 서비스)를 지정합니다.|  
|[\<issuerMetadata>](issuermetadata.md)|페더레이션 서비스의 STS(보안 토큰 서비스)에 대한 메타데이터 엔드포인트를 지정합니다.|  
|[\<issuedTokenParameters>](issuedtokenparameters.md)|사용자 지정 바인딩에서 발급된 토큰에 대한 매개 변수를 정의합니다.|  
|[\<localIssuer>](localissuer.md)|로컬 STS(보안 토큰 서비스)를 지정합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- [서비스 ID 및 인증](../../../wcf/feature-details/service-identity-and-authentication.md)
- [종점 주소, 바인딩 및 계약](../../../wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
