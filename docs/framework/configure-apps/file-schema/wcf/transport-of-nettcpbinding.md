---
title: <netTcpBinding>의 <transport>
ms.date: 03/30/2017
ms.assetid: 49462e0a-66e1-463f-b3e1-c83a441673c6
ms.openlocfilehash: 41f11be9b4ae8f7a7535c9766965de8575cff784
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399304"
---
# <a name="transport-of-nettcpbinding"></a>\<netTcpBinding>의 \<transport>
[ \<NetTcpBinding >](nettcpbinding.md)로 구성 된 끝점의 메시지 수준 보안 요구 사항 형식을 정의 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<netTcpBinding >** ](nettcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<보안 >** ](security-of-nettcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<전송 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<netTcpBinding>
  <binding>
    <security mode="None|Transport|Message|TransportWithMessageCredential">
      <transport clientCredentialType="None|Windows|Certificate"
                 protectionLevel="None|Sign|EncryptAndSign"
                 sslProtocols="Tls|Tls11|Tls12">
        <extendedProtectionPolicy policyEnforcement="Never|WhenSupported|Always"
                                  protectionScenario="TransportSelected|TrustedProxy">
          <customServiceNames>
          </customServiceNames>
        </extendedProtectionPolicy>
      </transport>
    </security>
  </binding>
</netTcpBinding>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|clientCredentialType|선택 사항입니다. 전송 보안을 사용하여 클라이언트 인증을 수행할 때 사용되는 자격 증명의 형식을 지정합니다.<br /><br /> -기본값 `Windows`은입니다.<br />-이 특성은 형식 <xref:System.ServiceModel.TcpClientCredentialType>입니다.|  
|protectionLevel|선택 사항입니다. TCP 전송의 수준에 보안을 정의합니다. 메시지에 서명하면 전송 중인 메시지를 제3자가 손상할 위험을 줄일 수 있습니다. 암호화는 전송 중에 데이터 수준에서 개인 정보를 보호합니다.<br /><br /> 기본값은 `EncryptAndSign`입니다.|  
|sslProtocols|지원되는 SslProtocols를 지정하는 SslProtocols 열거형 플래그 값입니다. 기본값은 Tls&#124;Tls11&#124;Tls12입니다.|  
|policyEnforcement|이 열거형은 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy>가 적용되는 경우를 지정합니다.<br /><br /> 1.  Never - 정책이 적용되지 않습니다(확장 보호가 사용되지 않음).<br />2.  WhenSupported – 클라이언트에서 확장 보호를 지원하는 경우에만 정책이 적용됩니다.<br />3.  Always – 정책이 항상 적용됩니다. 확장 보호를 지원하지 않는 클라이언트는 인증되지 않습니다.|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 특성  
  
|값|설명|  
|-----------|-----------------|  
|없음|클라이언트는 익명입니다. 여기에는 서비스 인증서가 필요합니다.|  
|Windows|SP 협상(Kerberos 협상)을 사용하는 클라이언트의 Windows 인증을 지정합니다.|  
|Certificate|클라이언트는 인증서를 사용하여 인증됩니다. 클라이언트에서는 SSL 협상을 사용하며 서비스 인증서가 필요합니다.|  
  
## <a name="protectionlevel-attribute"></a>protectionLevel 특성  
  
|값|설명|  
|-----------|-----------------|  
|없음|보호되지 않습니다.|  
|Sign|메시지가 서명됩니다.|  
|EncryptAndSign|-메시지가 암호화 되 고 서명 됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<security>](security-of-nettcpbinding.md)|[ \<NetTcpBinding >](nettcpbinding.md)의 보안 기능을 지정 합니다.|  
  
## <a name="remarks"></a>설명  
 SOAP 메시지의 무결성 및 기밀성과 상호 인증을 위해 전송 보안을 사용합니다. 바인딩에서 이 보안 모드를 선택하면 보안 전송을 사용하여 채널 스택이 구성되고 Windows(협상) 또는 SSL over TCP 같은 전송 보안을 사용하여 SOAP 메시지가 보안됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.TcpTransportSecurity>
- <xref:System.ServiceModel.Configuration.NetTcpSecurityElement.Transport%2A>
- <xref:System.ServiceModel.NetTcpSecurity.Transport%2A>
- <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>
- [서비스 및 클라이언트에 보안 설정](../../../wcf/feature-details/securing-services-and-clients.md)
- [바인딩](../../../wcf/bindings.md)
- [시스템 제공 바인딩 구성](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
