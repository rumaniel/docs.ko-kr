---
title: <netTcpBinding>의 <security>
ms.date: 03/30/2017
ms.assetid: 286cd191-4fd5-4c4e-a223-9c71cf7fdead
ms.openlocfilehash: 971b1ea979877f631766e438cc41bc0bdabfd346
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399795"
---
# <a name="security-of-nettcpbinding"></a>\<netTcpBinding >의 \<보안 >
바인딩에 대한 보안 설정을 정의합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<netTcpBinding >** ](nettcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<보안 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<security mode="Message/None/Transport/TransportWithCredential">
  <transport clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"
             protectionLevel="None/Sign/EncryptAndSign" />
  <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
           clientCredentialType="Certificate/IssuedToken/None/UserName/Windows" />
</security>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|모드|선택 사항입니다. 적용되는 보안 형식을 지정합니다. 유효한 값이 아래에 나와 있습니다. 기본값은 `Transport`입니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.SecurityMode> 형식입니다.|  
  
## <a name="mode-attribute"></a>mode 특성  
  
|값|설명|  
|-----------|-----------------|  
|없음|보안이 해제되어 있습니다.|  
|전송|전송 보안은 TCP를 통한 TLS 또는 SPNego를 사용하여 제공됩니다. 서비스는 SSL 인증서로 구성해야 할 수도 있습니다. 이 모드에서는 보호 수준을 제어할 수 있습니다.|  
|메시지|SOAP 메시지 보안을 사용하여 보안이 제공됩니다. 기본적으로 SOAP 본문은 암호화되고 서명됩니다. 이 모드는 서비스 자격 증명을 클라이언트에서 밴드 외 방식으로 사용할 수 있는지 여부, 사용할 알고리즘 모음, 메시지 본문에 적용될 보호 수준과 같은 다양한 기능을 제공합니다. 클라이언트 인증은 세션당 한 번씩 수행되며 세션 기간 동안 인증 결과가 캐시에 저장됩니다.|  
|TransportWithMessageCredential|전송 보안이 메시지 보안과 결합되어 있습니다. 전송 보안은 TCP를 통한 TLS 또는 SPNego를 사용하여 제공되며 무결성, 기밀성 및 서버 인증을 보장합니다. SOAP 메시지 보안에서는 클라이언트 인증이 제공됩니다. 기본적으로 클라이언트 인증은 세션당 한 번씩 수행되며 세션 기간 동안 인증 결과가 캐시에 저장됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<transport>](transport-of-nettcpbinding.md)|전송의 보안 설정을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.TcpTransportSecurityElement> 형식입니다.|  
|[\<message>](message-element-of-nettcpbinding.md)|메시지에 대한 보안 설정을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.MessageSecurityOverTcpElement> 형식입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|바인딩(binding)|[ \<NetTcpBinding >](nettcpbinding.md)의 바인딩 요소입니다.|  
  
## <a name="remarks"></a>설명  
 각 표준 바인딩은 전송 보안 요구 사항을 제어하는 매개 변수를 제공합니다. 일반적으로 이러한 매개 변수에는 메시지 수준 보안이 사용되는지 또는 전송 수준 보안이 사용되는지 지정한 보안 모드 및 선택한 클라이언트 자격 증명 형식이 포함됩니다. 이러한 매개 변수가 나타내는 선택 옵션에 따라 채널 스택이 해당 보안을 사용하여 생성됩니다.  
  
 WCF(Windows Communication Foundation)에서 제공하는 시스템 제공 바인딩은 가장 일반적인 일부 시나리오의 요구 사항을 충족하기 위한 집합입니다 이러한 각 바인딩을 사용하면 일부 특정 대상 시나리오의 보안 요구 사항을 지정할 수 있습니다.  
  
 이 구성 요소는 `netTcpBinding`의 보안 사양을 제공합니다. 이것은 시스템 간 통신에 적합한 안전하고, 신뢰할 수 있으며, 최적화된 바인딩입니다. 기본적으로 메시지 배달을 위한 TCP, 메시지 보안 및 인증을 위한 Windows 보안, 안정성을 위한 WS-Reliable Messaging 및 이진 메시지 인코딩을 지원하는 런타임 통신 스택을 생성합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.NetTcpSecurity>
- <xref:System.ServiceModel.NetTcpBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.NetTcpBindingElement.Security%2A>
- <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>
- [서비스 및 클라이언트에 보안 설정](../../../wcf/feature-details/securing-services-and-clients.md)
- [바인딩](../../../wcf/bindings.md)
- [시스템 제공 바인딩 구성](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
