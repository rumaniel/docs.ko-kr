---
title: <webSocketSettings>
ms.date: 03/30/2017
ms.assetid: bbf97e02-8dd1-4922-acac-3cd33397b249
ms.openlocfilehash: 80784f40130e572ae374bd9b26e701360dbfcaa5
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399141"
---
# <a name="websocketsettings"></a>\<webSocketSettings>
WebSocket 설정을 지정하는 데 사용되는 구성 요소입니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<netHttpBinding >** ](nethttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<webSocketSettings >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<netHttpBinding>
  <binding>
    <webSocketSettings createNotificationOnConnection="Boolean"
                       disablePayloadMasking="Boolean"
                       keepAliveInterval="TimeSpan"
                       maxPendingConnections="Integer"
                       receiveBufferSize="Integer"
                       sendBufferSize="Integer"
                       subProtocol="String"
                       transportUsage="WhenDuplex/Always/Never" />
  </binding>
</netHttpBinding>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|createNotificationOnConnection|연결 시 알림이 보내지는지 여부를 지정합니다.|  
|disablePayloadMasking|WebSocket 마스킹을 사용하지 않도록 설정할지 여부를 지정합니다.|  
|keepAliveInterval|상태 유지 간격을 지정합니다.|  
|maxPendingConnections|서비스에서 디스패치를 대기하는 최대 연결 수를 지정합니다.|  
|receiveBufferSize|수신 버퍼의 크기를 지정합니다.|  
|sendBufferSize|전송 버퍼의 크기를 지정합니다.|  
|subProtocol|WebSocket 하위 프로토콜을 지정합니다.|  
|transportUsage|WebSocket을 사용할 시기를 지정합니다.|  
  
## <a name="transportusage-attribute"></a>transportUsage 특성  
  
|값|설명|  
|-----------|-----------------|  
|WhenDuplex|이중 계약인 경우 WebSocket 프로토콜을 사용합니다.|  
|항상|계약과 관계없이 항상 WebSocket 프로토콜을 사용합니다.|  
|Never|WebSocket 프로토콜을 사용하지 않습니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|\<netHttpBinding>|NetHttpBinding을 지정합니다.|  
  
## <a name="example"></a>예제  
 다음 예제에서는 \<webSocketSettings > 요소를 사용 하는 방법을 보여 줍니다.  
  
```xml  
<netHttpBinding>
  <binding>
    <webSocketSettings createNotificationOnConnection="true"
                       disablePayloadMasking="false"
                       keepAliveInterval="00:10:00"
                       maxPendingConnections="100"
                       receiveBufferSize="1000"
                       sendBufferSize="1000"
                       subProtocol="Soap"
                       transportUsage="WhenDuplex/Always/Never" />
  </binding>
</netHttpBinding>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.Binding>
- <xref:System.ServiceModel.Channels.BindingElement>
- <xref:System.ServiceModel.BasicHttpBinding>
- <xref:System.ServiceModel.Configuration.BasicHttpBindingElement>
- [바인딩](../../../wcf/bindings.md)
- [시스템 제공 바인딩 구성](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
