---
title: <ws2007HttpBinding>의 <message>
ms.date: 03/30/2017
ms.assetid: 9ffd8db6-84a8-4b38-a9fe-2cb1a87a1c97
ms.openlocfilehash: 987c51f65f5c36a70724fd62fecaf737943c2d9a
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398029"
---
# <a name="message-of-ws2007httpbinding"></a>\<ws2007HttpBinding의 \<메시지 > >
Ws2007HttpBinding > 요소의 메시지 수준 보안 [ \<](ws2007httpbinding.md) 설정을 정의 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<ws2007HttpBinding >** ](ws2007httpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<보안 >** ](security-of-ws2007httpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<메시지 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<ws2007HttpBinding>
  <binding>
    <security>
      <message clientCredentialType="None/Windows/UserName/Certificate/IssuedToken"
               establishSecurityContext="Boolean"
               negotiateServiceCredential="Boolean"
               algorithmSuite="Enumeration. See algorithmSuite Attribute below."
               defaultProtectionLevel="None/Sign/EncryptionAndSign" />
    </security>
  </binding>
</ws2007HttpBinding>
```  
  
## <a name="type"></a>형식  
 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp>  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`algorithmSuite`|메시지 암호화 및 키 래핑 알고리즘을 설정합니다. 알고리즘과 키 크기는 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 클래스로 결정됩니다. 이러한 알고리즘은 보안 정책 언어(WS-SecurityPolicy) 사양에 지정된 알고리즘에 매핑됩니다.<br /><br /> 기본값은 Basic256입니다.|  
|`clientCredentialType`|선택 사항입니다. `Message` 또는 `TransportWithMessageCredentials` 보안 모드를 사용하여 클라이언트 인증을 수행할 때 사용되는 자격 증명의 형식을 지정합니다. 다음 표에서 열거형 값을 참조하세요. 기본값은 Windows입니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.MessageCredentialType> 형식입니다.|  
|`establishSecurityContext`|보안 채널이 보안 세션을 설정할지 여부를 결정하는 값입니다. 보안 세션은 애플리케이션 메시지를 교환하기 전에 SCT(보안 컨텍스트 토큰)를 설정합니다. SCT가 설정되면 보안 채널은 상위 채널에 대한 <xref:System.ServiceModel.Channels.ISession> 인터페이스를 제공합니다. 보안 세션을 [사용 하는 방법에 대 한 자세한 내용은 방법: 보안 세션](../../../wcf/feature-details/how-to-create-a-secure-session.md)을 만듭니다.<br /><br /> 기본값은 `true`입니다.|  
|`negotiateServiceCredential`|선택 사항입니다. 서비스 자격 증명이 클라이언트에서 out-of-band 방식으로 제공되는지 아니면 협상 프로세스를 통해 서비스에서 클라이언트로 전달되는지를 지정하는 값입니다. 그러한 협상은 일반적인 메시지 교환에 앞서 수행됩니다.<br /><br /> 특성이 None, Username 또는 Certificate 일 경우이 특성을로 `false` 설정 하면 클라이언트에서 대역 외로 서비스 인증서를 사용할 수 있고 클라이언트에서 서비스 인증서를 지정 해야 하는 것을 의미 합니다. `clientCredentialType` [ serviceCertificate\<>](servicecertificate-of-servicecredentials.md)) serviceCredentials > 서비스 동작에서 [ \<](servicecredentials.md) 이 모드는 WS-Trust 및 WS-SecureConversation을 구현하는 SOAP 스택과 상호 운용할 수 있습니다.<br /><br /> `ClientCredentialType` 특성이 `Windows`로 설정된 경우 이 특성을 `false`로 설정하면 Kerberos 기반 인증이 지정됩니다. 이것은 클라이언트와 서비스가 동일한 Kerberos 도메인에 속해야 함을 의미합니다. 이 모드는 Kerberos 토큰 프로필(OASIS WSS TC에서 정의) 그리고 WS-Trust 및 WS-SecureConversation을 구현하는 SOAP 스택과 상호 운용할 수 있습니다.<br /><br /> 이 특성이 `true`일 경우 SOAP 메시지를 통한 <xref:System.ServiceModel.Security.Tokens.ServiceModelSecurityTokenTypes.Spnego%2A> 교환을 터널링하는 .NET SOAP 협상이 수행됩니다.<br /><br /> 기본값은 `true`입니다.|  
  
## <a name="algorithmsuite-attribute"></a>algorithmSuite 특성  
  
|값|Description|  
|-----------|-----------------|  
|Basic128|Aes128 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic192|Aes192 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic256|Aes256 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic256Rsa15|메시지 암호화의 경우 Aes256, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa15를 사용합니다.|  
|Basic192Rsa15|메시지 암호화의 경우 Aes192, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa15를 사용합니다.|  
|TripleDes|TripleDes 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic128Rsa15|메시지 암호화의 경우 Aes128, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa15를 사용합니다.|  
|TripleDesRsa15|TripleDes 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa15를 사용합니다.|  
|Basic128Sha256|메시지 암호화의 경우 Aes256, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic192Sha256|메시지 암호화의 경우 Aes192, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic256Sha256|메시지 암호화의 경우 Aes256, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|TripleDesSha256|메시지 암호화의 경우 TripleDes, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic128Sha256Rsa15|메시지 암호화의 경우 Aes128, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa15를 사용합니다.|  
|Basic192Sha256Rsa15|메시지 암호화의 경우 Aes192, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa15를 사용합니다.|  
|Basic256Sha256Rsa15|메시지 암호화의 경우 Aes256, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa15를 사용합니다.|  
|TripleDesSha256Rsa15|메시지 암호화의 경우 TripleDes, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa15를 사용합니다.|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 특성  
  
|값|Description|  
|-----------|-----------------|  
|`None`|이를 통해 서비스와 익명 클라이언트가 상호 작용할 수 있습니다. 서비스 쪽에서는 서비스가 클라이언트 자격 증명을 요구하지 않음을 의미하고 클라이언트 쪽에서는 클라이언트가 클라이언트 자격 증명을 제공하지 않음을 의미합니다.|  
|`Certificate`|서비스에서 인증서를 사용하여 클라이언트를 인증하도록 요구할 수 있습니다. `message` 보안 모드가 사용되고 `negotiateServiceCredential` 특성이 `false`로 설정되면 서비스 인증서를 사용하여 클라이언트를 구축해야 합니다.|  
|`IssuedToken`|일반적으로 STS(보안 토큰 서비스)에서 발급하는 사용자 지정 토큰을 지정합니다.|  
|`UserName`|서비스에서 `UserName` 자격 증명을 사용하여 클라이언트를 인증하도록 요구할 수 있습니다. WCF에서는 암호 다이제스트를 보내거나 암호를 사용 하 고 메시지 보안에 이러한 키를 사용 하 여 키를 파생 없습니다. 따라서 WCF는 자격 증명을 사용할 `UserName` 때 전송에 보안을 적용 합니다. 이 자격 증명 모드에서는 상호 운용이 가능한 교환 또는 `negotiateServiceCredential` 특성을 기반으로 하는 상호 운용이 불가능한 협상이 수행됩니다.|  
|`Windows`|`Windows` 자격 증명의 인증된 컨텍스트에서 SOAP 교환을 수행할 수 있습니다. `negotiateServiceCredential` 특성이 `true`로 설정되면 SSPI 협상 또는 Kerberos(상호 운용 가능 표준)가 수행됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<security>](security-of-ws2007httpbinding.md)|Ws2007HttpBinding >에 대 한 [ \<](ws2007httpbinding.md)보안 설정을 정의 합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.NonDualMessageSecurityOverHttp>
- <xref:System.ServiceModel.Configuration.WSHttpSecurityElement.Message%2A>
- <xref:System.ServiceModel.WSHttpSecurity.Message%2A>
- <xref:System.ServiceModel.Configuration.NonDualMessageSecurityOverHttpElement>
- [서비스 및 클라이언트에 보안 설정](../../../wcf/feature-details/securing-services-and-clients.md)
- [바인딩](../../../wcf/bindings.md)
- [시스템 제공 바인딩 구성](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
