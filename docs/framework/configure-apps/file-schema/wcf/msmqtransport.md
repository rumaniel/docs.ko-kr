---
title: <msmqTransport>
ms.date: 03/30/2017
ms.assetid: 19d89f35-76ac-49dc-832b-e8bec2d5e33b
ms.openlocfilehash: 0948df37a97f51076747485d0b6074f14b3f9d58
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70397922"
---
# <a name="msmqtransport"></a>\<msmqTransport>
이 전송이 사용자 지정 바인딩에 포함되면 MSMQ 전송에서 채널이 메시지를 전송하도록 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<msmqTransport >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<msmqTransport customDeadLetterQueue="Uri"
               deadLetterQueue="Custom/None/System"
               durable="Boolean"
               exactlyOnce="Boolean"
               manualAddressing="Boolean"
               maxBufferPoolSize="Integer"
               maxImmediateRetries="Integer"
               maxPoolSize="Integer"
               maxReceivedMessageSize="Integer"
               maxRetryCycles="Integer"
               queueTransferProtocol="Native/Srmp/SrmpSecure"
               rejectAfterLastRetry="Boolean"
               retryCycleDelay="TimeSpan"
               timeToLive="TimeSpan"
               useActiveDirectory="Boolean"
               useSourceJournal="Boolean"
               useMsmqTracing="Boolean"
               ...>
  <msmqTransportSecurity>
  </msmqTransportSecurity>
</msmqTransport>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|customDeadLetterQueue|만료되었거나 응용 프로그램에 배달되지 못한 메시지가 전송되는 응용 프로그램별 배달 못 한 편지 큐의 위치를 나타내는 URI입니다.<br /><br /> ExactlyOnce 보증이 필요한 즉, `exactlyOnce`가 `true`로 설정된 메시지의 경우 이 특성의 기본값은 MSMQ에서 시스템 차원의 배달 못 한 트랜잭션 큐로 설정됩니다.<br /><br /> 보증이 필요하지 않은 즉, `exactlyOnce`가 `false`로 설정된 메시지의 경우 이 특성의 기본값은 `null`로 설정됩니다.<br /><br /> 값은 net.msmq 체계를 사용해야 합니다. 기본값은 `null`입니다.<br /><br /> `deadLetterQueue`가 `None` 또는 `System`으로 설정되면 이 특성이 `null`로 설정되어야 합니다. 이 특성이 `null`이 아니면 `deadLetterQueue`는 `Custom`으로 설정되어야 합니다.|  
|deadLetterQueue|사용할 배달 못 한 편지 큐의 형식을 지정합니다.<br /><br /> 유효한 값은 다음과 같습니다.<br /><br /> 재구성 사용자 지정 배달 못한 편지 큐입니다.<br />없음을 배달 못한 편지 큐를 사용할 수 없습니다.<br />컴퓨터 시스템 배달 못한 편지 큐를 사용 합니다.<br /><br /> 이 특성은 DeadLetterQueue 형식입니다.|  
|durable|이 바인딩이 처리하는 메시지가 지속적인지 또는 일시적인지를 지정하는 부울 값입니다. 기본값은 `true`입니다.<br /><br /> 지속적 메시지는 큐 관리자가 중단되더라도 남아 있지만, 일시적 메시지는 손실됩니다. 응용 프로그램에서 더 낮은 대기 시간을 요구하며 어느 정도의 메시지 손실을 허용할 수 있다면 일시적 메시지가 유용합니다.<br /><br /> `exactlyOnce`가 `true`로 설정되었다면 메시지가 지속적이어야 합니다.|  
|exactlyOnce|이 바인딩이 처리한 메시지를 정확히 한 번만 받을지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.<br /><br /> 메시지는 보증과 함께 또는 보증 없이 보낼 수 있습니다. 보증을 사용하면 응용 프로그램에서는 보낸 메시지가 수신 메시지 큐에 도착했는지 확인할 수 있으며, 메시지가 도착하지 않았을 경우에는 배달 못 한 편지 큐를 읽어 이를 확인할 수 있습니다.<br /><br /> `exactlyOnce`가 `true`로 설정된 경우 MSMQ는 보낸 메시지를 수신 메시지 큐에 단 한 번만 배달하고, 배달이 실패하면 배달 못 한 편지 큐로 보냅니다.<br /><br /> `exactlyOnce`를 `true`로 설정하여 보내는 메시지는 트랜잭션 큐로만 보내야 합니다.|  
|manualAddressing|사용자가 메시지 주소 지정을 제어할 수 있도록 하는 부울 값입니다. 이 속성은 여러 대상 중 어느 대상으로부터 메시지를 받을 것인지를 애플리케이션에서 결정하는 라우터 시나리오에서 주로 사용됩니다.<br /><br /> 이 속성이`true`로 설정되면 채널에서는 메시지에 이미 주소가 지정되었다고 가정하여 더 이상 정보를 추가하지 않습니다. 그러면 사용자는 모든 메시지의 주소를 개별적으로 지정할 수 있습니다.<br /><br /> `false`로 설정되면 기본 WCF(Windows Communication Foundation) 주소 지정 메커니즘이 모든 메시지에 대한 주소를 자동으로 만듭니다.<br /><br /> 기본값은 `false`입니다.|  
|maxBufferPoolSize|버퍼 풀의 최대 크기를 지정하는 양의 정수입니다. 기본값은 524288입니다.<br /><br /> WCF의 많은 부분에서 버퍼를 사용합니다. 버퍼를 사용할 때마다 만들고 삭제하면 비용이 많이 들며, 버퍼에 대한 가비지 수집 역시 비용이 많이 듭니다. 버퍼 풀이 있으면 이 풀로부터 버퍼를 가져와 사용한 다음 다시 풀로 반환할 수 있습니다. 따라서 버퍼를 만들고 삭제하는 데 오버헤드를 피할 수 있습니다.|  
|maxImmediateRetries|응용 프로그램 큐에서 읽은 메시지에 대 한 최대 즉시 재시도 횟수를 지정 하는 정수입니다. 기본값은 5입니다.<br /><br /> 메시지에 대한 최대 즉시 재시도 횟수만큼 시도했으나 응용 프로그램에서 메시지를 배달하지 못한 경우 그 메시지는 나중에 재시도하기 위해 재시도 큐로 보내집니다. 재시도 주기를 지정하지 않은 경우 해당 메시지가 포이즌 메시지 큐로 보내지거나 발신자에게 부정 승인이 다시 보내집니다.|  
|maxPoolSize|풀의 최대 크기를 지정하는 양의 정수입니다. 기본값은 524288입니다.|  
|maxReceivedMessageSize|헤더를 포함하는 최대 메시지 크기(바이트)를 지정하는 양의 정수입니다. 수신자에게 너무 큰 메시지를 보내면 메시지의 발신자에게 SOAP 오류가 발생합니다. 수신자는 메시지를 삭제하고 추적 로그에 이벤트 항목을 만듭니다. 기본값은 65536입니다.|  
|maxRetryCycles|수신 응용 프로그램으로 메시지를 배달하려는 최대 재시도 주기 수를 지정하는 정수입니다. 기본값은 <xref:System.Int32.MaxValue>입니다.<br /><br /> 단일 재시도 주기는 지정된 횟수만큼 애플리케이션으로 메시지 배달을 시도합니다. 시도 횟수는 `maxImmediateRetries` 특성으로 설정합니다. 배달 시도를 모두 수행했으나 애플리케이션에서 메시지를 배달하지 못한 경우 그 메시지는 재시도 큐로 보내집니다. 후속 재시도 주기는 `retryCycleDelay` 특성에서 지정한 지연 시간이 지나고 응용 프로그램에서 메시지 배달을 다시 시도하기 위해 재시도 큐에서 응용 프로그램 큐로 반환되는 메시지로 구성됩니다. `maxRetryCycles` 특성은 응용 프로그램에서 메시지 배달 시도에 사용할 재시도 주기 수를 지정합니다.|  
|queueTransferProtocol|이 바인딩에서 사용하는 대기 중인 통신 채널 전송을 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> 전용  네이티브 MSMQ 프로토콜을 사용합니다.<br />-   Srmp:  SRMP(SOAP Reliable Messaging Protocol)를 사용합니다.<br />-SrmpSecure: SRMPS(Soap Reliable Messaging Protocol Secure) 전송을 사용합니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.QueueTransferProtocol> 형식입니다.<br /><br /> MSMQ는 SOAP 신뢰할 수 있는 메시징 프로토콜을 사용 하는 경우 Active Directory 주소 지정을 지원 하지 않으므로가로 `useActiveDirectory` `true`설정 된 경우이 특성을 Srmp 또는 srmps로 설정 하면 안 됩니다.|  
|rejectAfterLastRetry|최대 재시도 횟수만큼 시도한 후에 배달하지 못한 메시지에 대해 수행할 작업을 지정하는 부울 값입니다.<br /><br /> `true`인 경우 부정 승인이 발신자에게 반환되고 메시지가 삭제되며, `false`인 경우 메시지가 포이즌 메시지 큐로 보내집니다. 기본값은 `false`입니다.<br /><br /> 값이 `false`이면 수신 응용 프로그램에서는 포이즌 메시지 큐를 읽어 포이즌 메시지(배달하지 못한 메시지)를 처리할 수 있습니다.<br /><br /> MSMQ 3.0에서는 부정 승인을 발신자에게 반환할 수 없으므로 이 특성이 무시됩니다.|  
|retryCycleDelay|즉시 배달할 수 없는 메시지를 배달하려고 할 때 재시도 주기 사이의 지연 시간을 지정하는 <xref:System.TimeSpan>입니다. 기본값은 00:10:00입니다.<br /><br /> 단일 재시도 주기는 지정된 횟수만큼 수신 애플리케이션으로 메시지 배달을 시도합니다. 시도 횟수는 `maxImmediateRetries` 특성으로 지정합니다. 지정된 횟수만큼 즉시 재시도가 수행되었으나 애플리케이션에서 메시지를 배달하지 못한 경우 그 메시지는 재시도 큐로 보내집니다. 후속 재시도 주기는 `retryCycleDelay` 특성에서 지정한 지연 시간이 지나고 응용 프로그램에서 메시지 배달을 다시 시도하기 위해 재시도 큐에서 응용 프로그램 큐로 반환되는 메시지로 구성됩니다. 재시도 주기 횟수는 `maxRetryCycles` 특성으로 지정합니다.|  
|timeToLive|메시지가 만료되어 배달 못 한 큐에 배치되기 전에 메시지가 유효한 기간을 지정하는 <xref:System.TimeSpan>입니다. 기본값은 1일을 의미하는 1.00:00:00입니다.<br /><br /> 이 특성은 시간을 다투는 메시지가 수신 응용 프로그램에서 처리되기 전에 무효화되지 않도록 하기 위해 설정됩니다. 지정된 시간 간격 내에 수신 애플리케이션에서 사용하지 않은 큐의 메시지는 만료된 것으로 간주됩니다. 만료된 메시지는 배달 못한 편지 큐라는 특수 큐로 보내집니다. 배달 못 한 편지 큐의 위치는 보증에 따라 `customDeadLetterQueue` 특성으로 설정되거나 해당 기본값으로 설정됩니다.|  
|UseActiveDirectory|Active Directory를 사용하여 큐 주소를 변환해야 하는지 여부를 지정하는 부울 값입니다.<br /><br /> MSMQ 큐 주소는 경로 이름이나 직접 형식 이름으로 구성될 수 있습니다. 직접 형식 이름을 사용할 경우 MSMQ는 DNS, NetBIOS 또는 IP를 사용하여 컴퓨터 이름을 확인합니다. 경로 이름을 사용할 경우 MSMQ는 Active Directory를 사용하여 컴퓨터 이름을 확인합니다. 기본적으로 WCF(Windows Communication Framework) 대기 중인 전송은 메시지 큐의 URI를 직접 형식 이름으로 변환합니다. 응용 프로그램에서는 이 특성을 `true`로 설정하여 대기 중인 전송이 DNS, NetBIOS 또는 IP가 아닌 Active Directory를 사용하여 컴퓨터의 이름을 확인하도록 지정할 수 있습니다.|  
|useMsmqTracing|이 바인딩이 처리하는 메시지를 추적할지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 추적 기능을 사용하면 메시지가 메시지 큐 컴퓨터에 들어가거나 나올 때마다 보고서 메시지가 만들어진 후 보고서 큐로 보내집니다.|  
|useSourceJournal|이 바인딩이 처리하는 메시지의 복사본을 소스 업무 일지 큐에 저장해야 하는지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 대기 중 응용 프로그램에서 컴퓨터의 나가는 큐를 떠난 메시지의 레코드를 보존해야 할 경우 메시지를 업무 일지 큐에 복사할 수 있습니다. 메시지가 보내는 큐를 떠난 후 대상 컴퓨터에 수신되었다는 승인을 받으면 해당 메시지의 복사본이 보낸 컴퓨터의 시스템 업무 일지 큐에 보관됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<msmqTransportSecurity>](msmqtransportsecurity.md)|이 바인딩의 전송 보안 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement> 형식입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|사용자 지정 바인딩의 모든 바인딩 기능을 정의합니다.|  
  
## <a name="remarks"></a>설명  
 `msmqTransport` 요소를 사용하여 대기 중 통신 채널 속성을 설정할 수 있습니다. 대기 중 통신 채널에서는 전송에 메시지 큐를 사용합니다.  
  
 이 바인딩 요소는 메시지 큐 표준 바인딩(`netMsmqBinding`)에 사용되는 기본 바인딩 요소입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.MsmqTransportElement>
- <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [WCF의 큐](../../../wcf/feature-details/queues-in-wcf.md)
- [전송](../../../wcf/feature-details/transports.md)
- [전송 선택](../../../wcf/feature-details/choosing-a-transport.md)
- [바인딩](../../../wcf/bindings.md)
- [바인딩 확장](../../../wcf/extending/extending-bindings.md)
- [사용자 지정 바인딩](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
