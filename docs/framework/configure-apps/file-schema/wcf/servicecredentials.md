---
title: <serviceCredentials>
ms.date: 03/30/2017
ms.assetid: 96db336c-4f7a-4193-81a5-910b8ffd804f
ms.openlocfilehash: 90a34a4a52b4c7a2e67d733fecba132818cac4fc
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399638"
---
# <a name="servicecredentials"></a>\<serviceCredentials>
서비스를 인증하는 데 사용되는 자격 증명 및 클라이언트 자격 증명 유효성 검사 관련 설정을 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceBehaviors >** ](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<serviceCredentials >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<serviceCredentials type="String">
  <clientCertificate>
  </clientCertificate>
  <issuedTokenAuthentication>
  </issuedTokenAuthentication>
  <peer>
  </peer>
  <secureConversationAuthentication>
  </secureConversationAuthentication>
  <serviceCertificate>
  </serviceCertificate>
  <userNameAuthentication>
  </userNameAuthentication>
  <windowsAuthentication>
  </windowsAuthentication>
</serviceCredentials>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|`type`|이 구성 요소의 형식을 지정하는 문자열입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<clientCertificate>](clientcertificate-of-servicecredentials.md)|클라이언트 인증서가 out-of-band 방식으로 제공될 때 사용할 인증서를 지정합니다. 이 요소는 클라이언트 인증서 유효성 검사 설정도 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement> 형식입니다.|  
|[\<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md)|이 서비스에 대해 현재 발급된 토큰을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement> 형식입니다.|  
|[\<peer>](peer-of-servicecredentials.md)|피어 노드에 대한 현재 자격 증명을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.PeerCredentialElement> 형식입니다.|  
|[\<secureConversationAuthentication>](secureconversationauthentication-of-servicecredential.md)|보안 대화에 대한 현재 자격 증명을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.SecureConversationServiceElement> 형식입니다.|  
|[\<serviceCertificate>](servicecertificate-of-servicecredentials.md)|자체 식별을 위해 서비스에서 사용되는 인증서를 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.X509RecipientCertificateServiceElement> 형식입니다.|  
|[\<userNameAuthentication>](usernameauthentication.md)|사용자 이름 암호 유효성 검사의 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.UserNameServiceElement> 형식입니다.|  
|[\<windowsAuthentication>](windowsauthentication-of-servicecredentials.md)|Windows 자격 증명 유효성 검사의 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.WindowsServiceElement> 형식입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|동작 요소를 지정합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement>
- <xref:System.ServiceModel.Description.ServiceCredentials>
- [보안 동작](../../../wcf/feature-details/security-behaviors-in-wcf.md)
