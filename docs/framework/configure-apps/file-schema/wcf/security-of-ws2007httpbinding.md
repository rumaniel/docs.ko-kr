---
title: '&lt;ws2007HttpBinding&gt;의 &lt;security&gt;'
ms.date: 03/30/2017
ms.assetid: fdda0ff7-b462-4e26-af52-e87ddab71945
ms.openlocfilehash: fb92e7549b86a2c4a4a8453d13f6c4f08d696348
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199385"
---
# <a name="ltsecuritygt-of-ltws2007httpbindinggt"></a>&lt;ws2007HttpBinding&gt;의 &lt;security&gt;
사용 하는 보안 설정을 나타냅니다 합니다 [ \<ws2007HttpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md) 요소입니다.  
  
 \<system.serviceModel>  
\<바인딩 >  
\<ws2007HttpBinding>  
\<바인딩 >  
\<security>  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.serviceModel>  
    <bindings>  
        <ws2007HttpBinding>  
            <binding name = "string">  
              <security mode="None/Message/Transport/TransportWithMessageCredential">  
                  <transport>  
                  </transport>  
                  <message>  
                  </message>  
              </security  
        </ws2007HttpBinding>  
    </bindings>  
</system.ServiceModel>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`mode`|-선택 사항입니다. 적용되는 보안 형식을 지정합니다. 기본값은 `Message`입니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.SecurityMode> 형식입니다.|  
  
## <a name="mode-attribute"></a>Mode 특성  
  
|값|설명|  
|-----------|-----------------|  
|`None`|보안이 해제되어 있습니다.|  
|`Transport`|HTTPS를 사용하여 보안이 제공됩니다. SSL(Secure Sockets Layer) 인증서를 사용하여 서비스를 구성해야 합니다. 메시지는 HTTPS를 사용하여 완전하게 보안 처리되며, 서비스는 서비스의 SSL 인증서를 사용하여 클라이언트에 의해 인증됩니다. 클라이언트 인증을 통해 제어 됩니다 합니다 `ClientCredentials` 특성을 [ \<전송 >](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-ws2007httpbinding.md) 요소입니다.|  
|`Message`|SOAP 메시지 보안을 사용하여 보안이 제공됩니다. 기본적으로 SOAP 본문은 암호화되고 서명됩니다. 이 모드는 서비스 자격 증명을 out-of-band 클라이언트에서 사용할 수 있는지 여부, 사용할 알고리즘 모음 및 <xref:System.ServiceModel.Security.SecurityMessageProperty>를 통해 메시지 본문에 적용할 보호 수준과 같은 다양한 기능을 제공합니다. 클라이언트 인증은 각 세션에 대해 한 번씩 수행되며 세션 기간 동안 인증 결과가 캐시됩니다.|  
|`TransportWithMessageCredential`|이 모드에서 HTTPS는 무결성, 기밀성 및 서버 인증을 제공하고 SOAP 메시지 보안은 클라이언트 인증을 제공합니다. 기본적으로 클라이언트 인증은 각 세션에 대해 한 번씩 수행되며 세션 기간 동안 인증 결과가 캐시됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<transport>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-ws2007httpbinding.md)|전송 보안 설정을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement> 형식에 해당합니다. 이 설정은 모드를 Transport로 설정한 경우에만 적용됩니다.|  
|[\<message>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-ws2007httpbinding.md)|메시지에 대한 보안 설정을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.MessageSecurityOverHttpElement> 형식에 해당합니다. 이 설정은 모드를 Transport로 설정한 경우에 적용되지 않습니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<ws2007HttpBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md)|HTTP 전송 응용 프로그램에 대한 보안 바인딩입니다.|  
  
## <a name="remarks"></a>설명  
 이 요소는 WS-* 사양을 구현하는 서비스와 상호 운용하도록 디자인되었습니다. 이 바인딩의 전송 보안은 HTTP 또는 SSL(Secure Sockets Layer) over HTTP입니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.WSHttpSecurity>  
 <xref:System.ServiceModel.WSHttpBinding.Security%2A>  
 <xref:System.ServiceModel.Configuration.WSHttpBindingElement.Security%2A>  
 <xref:System.ServiceModel.Configuration.WSHttpSecurityElement>  
 <xref:System.ServiceModel.BasicHttpSecurity>  
 [서비스 및 클라이언트에 보안 설정](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)  
 [바인딩](../../../../../docs/framework/wcf/bindings.md)  
 [시스템 제공 바인딩 구성](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)  
 [\<binding>](../../../../../docs/framework/misc/binding.md)
