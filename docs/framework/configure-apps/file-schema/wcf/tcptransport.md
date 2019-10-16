---
title: <tcpTransport>
ms.date: 03/30/2017
ms.assetid: 8fcd18c1-9958-42e7-b442-7903f7bdb563
ms.openlocfilehash: 409d2e47b411c0bfaa2b0fe46fc242bd8453a042
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399484"
---
# <a name="tcptransport"></a>\<tcpTransport>
사용자 지정 바인딩에 대한 메시지를 전송하기 위해 채널이 사용할 수 있는 TCP 전송을 정의합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<tcpTransport >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<tcpTransport channelInitializationTimeout="TimeSpan"
              connectionBufferSize="Integer"
              hostNameComparisonMode="StrongWildcard/Exact/WeakWildcard"
              listenBacklog="Integer"
              manualAddressing="Boolean"
              maxBufferPoolSize="Integer"
              maxBufferSize="Integer"
              maxOutputDelay="TimeSpan"
              maxPendingAccepts="Integer"
              maxPendingConnections="Integer"
              maxReceivedMessageSize="Integer"
              portSharingEnabled="Boolean"
              teredoEnabled="Boolean"
              transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse" >
  <connectionPoolSettings groupName="String"
                          idleTimeout="TimeSpan"
                          leaseTimeout="TimeSpan"
                          maxOutboundConnectionsPerEndpoint="Integer" />
</tcpTransport>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|channelInitializationTimeout|수락할 채널을 초기화하기 위한 시간 제한을 가져오거나 설정합니다.  연결이 끊어지기 전에 채널이 초기화 상태를 유지할 수 있는 최대 시간(초)입니다. 이 할당량에는 TCP 연결이 .NET 메시지 프레이밍 프로토콜을 사용 하 여 자신을 인증 하는 데 사용할 수 있는 시간이 포함 됩니다. 서버가 인증을 수행하는 데 충분한 정보를 가지려면 클라이언트가 몇 가지 초기 데이터를 보내야 합니다. 기본값은 30초입니다.|  
|connectionBufferSize|통신 중에 클라이언트나 서비스로부터 serialize된 메시지 청크를 전송할 때 사용되는 버퍼의 크기를 가져오거나 설정합니다.|  
|hostNameComparisonMode|URI 비교 시 서비스에 액세스하는 데 호스트 이름이 사용되는지 여부를 나타내는 값을 가져오거나 설정합니다.|  
|listenBacklog|웹 서비스에 대해 보류할 수 있는 최대 대기 중인 연결 요청 수입니다. `connectionLeaseTimeout` 특성은 연결 예외가 throw되기 전에 클라이언트가 연결을 대기하는 시간을 제한합니다. 웹 서비스에 대해 보류할 수 있는 최대 대기 중인 연결 요청 수를 제어하는 소켓 수준 속성입니다. ListenBacklog이 너무 낮으면 WCF는 요청 수락을 중지 하므로 서버에서 대기 중인 기존 연결 중 일부를 승인할 때까지 새 연결을 삭제 합니다. 기본값은 16 * 프로세서 수입니다.|  
|manualAddressing|메시지의 주소를 수동으로 지정해야 하는지 여부를 나타내는 값을 가져오거나 설정합니다.|  
|maxBufferPoolSize|전송에 사용되는 최대 버퍼 풀 크기를 가져오거나 설정합니다.|  
|maxBufferSize|사용할 버퍼의 최대 크기를 가져오거나 설정합니다. 스트리밍된 메시지의 경우 이 값은 버퍼링된 모드에서 읽어오는 메시지 헤더의 최대 예상 크기 이상이어야 합니다.|  
|maxOutputDelay|메시지 청크 또는 전체 메시지를 보내기 전에 메모리에 버퍼링된 상태로 유지할 수 있는 최대 시간 간격을 가져오거나 설정합니다.|  
|maxPendingAccepts|서비스에 들어오는 연결을 처리하는 데 사용할 수 있는 보류 중인 최대 비동기 수락 작업 수를 가져오거나 설정합니다.|  
|maxPendingConnections|서비스에서 디스패치를 대기하는 최대 연결 수를 가져오거나 설정합니다.|  
|maxReceivedMessageSize|받을 수 있는 최대 메시지 크기를 가져오거나 설정합니다.|  
|portSharingEnabled|이 연결에서 TCP 포트 공유를 사용하는지를 지정하는 부울 값입니다. 이 값이 `false`이면 바인딩마다 자체 단독 포트가 사용됩니다. 기본값은 `false`입니다.<br /><br /> 이 설정은 서비스에만 적용되며, 클라이언트는 영향을 받지 않습니다.<br /><br /> 이 설정을 사용하려면 WCF(Windows Communication Foundation) TCP 포트 공유 서비스의 시작 유형을 수동 또는 자동으로 변경하여 서비스를 사용하도록 설정해야 합니다|  
|teredoEnabled|Teredo(방화벽으로 보호되는 클라이언트의 주소를 지정하는 기술)의 사용 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 이 속성은 내부 TCP 소켓에 대해 Teredo를 활성화합니다. 자세한 내용은 [Teredo 개요](https://go.microsoft.com/fwlink/?LinkId=95339)합니다.<br /><br /> 이 속성은 [!INCLUDE[wxpsp2](../../../../../includes/wxpsp2-md.md)] 및 [!INCLUDE[ws2003](../../../../../includes/ws2003-md.md)]에만 적용됩니다. [!INCLUDE[wv](../../../../../includes/wv-md.md)]에는 시스템 수준의 Teredo 구성 옵션이 있으므로 Vista를 실행할 경우 이 속성이 무시됩니다. Teredo를 사용할 경우 클라이언트와 서비스 시스템 모두에 Microsoft IPv6 스택을 설치하고 Teredo 사용에 적합하도록 구성해야 합니다. Teredo 구성에 대 한 자세한 내용은 참조 하세요. [Teredo 개요](https://go.microsoft.com/fwlink/?LinkId=95339)합니다. 자세한 내용은 [Windows Server 2003 기술 센터](https://go.microsoft.com/fwlink/?LinkId=49888)합니다.|  
|transferMode|메시지가 연결 지향 전송을 사용하여 버퍼링되는지 아니면 스트리밍되는지를 나타내는 값을 가져오거나 설정합니다.|  
|connectionPoolSettings|명명된 파이프 바인딩의 추가 연결 풀 설정을 지정합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|사용자 지정 바인딩의 모든 바인딩 기능을 정의합니다.|  
  
## <a name="remarks"></a>설명  
 이 전송은 "net.tcp://hostname:port/path" 형식의 URI를 사용합니다. 다른 URI 구성 요소는 선택적입니다.  
  
 `tcpTransport` 요소는 TCP 전송 프로토콜을 구현하는 사용자 지정 바인딩을 만들기 위한 시작점입니다. 이 전송은 WCF와 WCF 사이의 통신을 위해 최적화됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.TcpTransportElement>
- <xref:System.ServiceModel.Channels.TcpTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [전송](../../../wcf/feature-details/transports.md)
- [전송 선택](../../../wcf/feature-details/choosing-a-transport.md)
- [바인딩](../../../wcf/bindings.md)
- [바인딩 확장](../../../wcf/extending/extending-bindings.md)
- [사용자 지정 바인딩](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
