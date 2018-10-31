---
title: '&lt;netPeerBinding&gt;의 &lt;security&gt;'
ms.date: 03/30/2017
ms.assetid: 1ef40d8c-f903-4426-9b08-da81462766d8
ms.openlocfilehash: d32b6426009c403d74ca3a05d3c3ba7be9163cae
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197329"
---
# <a name="ltsecuritygt-of-ltnetpeerbindinggt"></a>&lt;netPeerBinding&gt;의 &lt;security&gt;
보안 설정을 정의 합니다 [ \<netPeerTcpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/netpeertcpbinding.md), 인증 유형 등 사용 및 보안 메시지 전송에 사용 합니다.  
  
 \<system.ServiceModel>  
\<바인딩 >  
\<netPeerBinding>  
\<바인딩 >  
\<security>  
  
## <a name="syntax"></a>구문  
  
```xml  
<netPeerBinding>  
    <binding>  
        <security mode="Message/None/Transport//TransportWithMessageCredential">  
            <transport credentialType="Certificate/Password" />  
        </security>  
    </binding>  
</netPeerBinding>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|모드|선택 사항입니다. 이 바인딩으로 구성된 피어에서 사용하는 보안 형식을 지정합니다. 기본값은 `Message`입니다. 이 특성은 <xref:System.ServiceModel.SecurityMode> 형식입니다.|  
  
## <a name="mode-attribute"></a>mode 특성  
  
|값|설명|  
|-----------|-----------------|  
|메시지|SOAP 전송은 무결성, 기밀성 및 인증을 제공합니다.|  
|없음|보안이 해제되어 있습니다.|  
|전송|HTTPS를 사용하여 보안이 제공됩니다.|  
|TransportWithMessageCredential|HTTPS는 인증 및 기밀성을 제공합니다. SOAP 메시지는 다양한 자격 증명 형식을 제공합니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<transport>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-netpeertcpbinding.md)|이 바인딩으로 구성된 피어에서 보낸 보안 메시지의 전송 형식을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.PeerTransportSecurityElement> 형식입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<binding>](../../../../../docs/framework/misc/binding.md)|모든 바인딩 기능을 정의 합니다 [ \<netPeerTcpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/netpeertcpbinding.md)합니다.|  
  
## <a name="remarks"></a>설명  
 보안은 메시지 또는 전송별로 고유할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Configuration.PeerSecurityElement>  
 <xref:System.ServiceModel.NetPeerTcpBinding.Security%2A>  
 <xref:System.ServiceModel.Configuration.NetPeerTcpBindingElement.Security%2A>  
 <xref:System.ServiceModel.PeerSecuritySettings>  
 [서비스 및 클라이언트에 보안 설정](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)  
 [자격 증명 형식 선택](../../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)  
 [바인딩](../../../../../docs/framework/wcf/bindings.md)  
 [시스템 제공 바인딩 구성](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)  
 [\<binding>](../../../../../docs/framework/misc/binding.md)
