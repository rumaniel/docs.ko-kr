---
title: <udpAnnouncementEndpoint>의 <udpTransportSettings>
ms.date: 03/30/2017
ms.assetid: a7ddff1a-5eed-4bbc-8580-b95ef8890e1f
ms.openlocfilehash: b67bdf825948dffe18aabe91b0de236eb929bccc
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854853"
---
# <a name="udptransportsettings-of-udpannouncementendpoint"></a>\<udpTransportSettings> of \<udpAnnouncementEndpoint>
이 구성 요소는 [ \<udpannouncementendpoint >](udpannouncementendpoint.md)에 대 한 UDP 전송 설정을 노출 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<standardEndpoints >** ](standardendpoints.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<udpAnnouncementEndpoint >** ](udpannouncementendpoint.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<updTransportSettings >**  

## <a name="syntax"></a>구문  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
    <udpAnnouncementEndpoint>
      <standardEndpoint>
        <updTransportSettings duplicateMessageHistoryLength="Integer"
                              maxBufferPoolSize="Integer"
                              maxMulticastRetransmitCount="Integer"
                              maxPendingMessageCount="Integer"
                              maxReceivedMessageSize="Integer"
                              maxUnicastRetransmitCount="Integer"
                              multicastInterfaceId="String"
                              socketReceiveBufferSize="Integer"
                              timeToLive="Integer" />
      </standardEndpoint>
    </udpAnnouncementEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|duplicateMessageHistoryLength|중복 메시지를 식별하기 위해 전송에 사용되는 최대 메시지 해시 수를 지정합니다.  TransportManager 수준에서 중복 검색이 수행됩니다. 이 속성을 0으로 설정하면 중복 검색이 사용되지 않습니다.<br /><br /> 시스템 관리자나 개발자는 이 특성을 사용하여 중복 메시지 검색 알고리즘을 해제할 수 있습니다. 직접 작성한 중복 검색 알고리즘을 구현하려는 경우 유용할 수 있습니다.<br /><br /> 기본값은 4112입니다.|  
|maxBufferPoolSize|전송에 사용할 수 있는 버퍼 풀의 최대 크기를 지정하는 정수입니다.|  
|maxMulticastRetransmitCount|메시지를 처음 보낸 후 재전송해야 하는 최대 횟수를 지정하는 정수입니다.<br /><br /> 기본값은 2입니다.|  
|maxPendingMessageCount|수신되었으나 개별 채널 인스턴스의 InputQueue에서 아직 제거되지 않은 최대 메시지 수를 지정하는 정수입니다.  InputQueue가 보류 중인 메시지 수 제한에 도달하는 경우 메시지가 삭제됩니다.<br /><br /> 기본값은 32입니다.|  
|maxReceivedMessageSize|바인딩에서 처리할 수 있는 메시지의 최대 크기를 지정하는 정수입니다.<br /><br /> 기본값은 65507입니다.|  
|maxUnicastRetransmitCount|메시지를 처음 보낸 후 재전송해야 하는 최대 횟수를 지정하는 정수입니다.  메시지를 유니캐스트 주소로 보내고 응답 메시지가 해당 RelatesTo 헤더에서 수신되면 구성된 횟수만큼 재전송하기 하기 전에 재전송이 일찍 종료될 수 있습니다.<br /><br /> 기본값은 1입니다.|  
|multicastInterfaceId|멀티홈 컴퓨터에서 멀티캐스트 트래픽을 보내고 받을 때 사용해야 하는 네트워크 어댑터를 고유하게 식별하는 문자열입니다. 런타임에 전송에서 이 특성 값을 사용하여 인터페이스 인덱스를 조회합니다. 이 인덱스는 `IP_MULTICAST_IF` 및 `IPV6_MULTICAST_IF` 소켓 옵션을 설정하는 데 사용됩니다.  해당되는 경우 동일한 인터페이스 인덱스가 멀티캐스트 그룹을 조인할 때 사용됩니다.<br /><br /> 기본값은 `null`입니다.|  
|socketReceiveBufferSize|기본 WinSock 소켓의 수신 버퍼 크기를 지정하는 정수입니다.<br /><br /> 수신 채널의 사용자는 바인딩의 이 특성을 사용하여 데이터를 받을 때 시스템이 동작하는 방식을 제어할 수 있습니다.  예를 들어 최대 임계값으로 인바운드 WCF 메시지를 사용하는 특정 애플리케이션에서 이 특성에 더 큰 값을 사용하면 애플리케이션에서 메시지를 처리할 수 있을 때까지 대기하는 동안 메시지가 WinSock 버퍼에 쌓이게 됩니다.  같은 상황에서 더 작은 값을 사용하면 메시지가 삭제됩니다. 이 특성은 기본 WinSock `SO_RCVBUF` 소켓 옵션을 노출합니다. 이 특성의 값은 적어도 `maxReceivedMessageSize` 크기 이상이어야 합니다.   이 값을 `maxReceivedMessageSize`보다 작은 값으로 설정하며 런타임 예외가 발생합니다.<br /><br /> 기본값은 65536입니다.|  
|timeToLive|멀티캐스트 패킷이 이동할 수 있는 네트워크 세그먼트 홉의 수를 지정하는 정수입니다.  이 특성은 `IP_MULTICAST_TTL` 및 `IP_TTL` 소켓 옵션과 관련된 기능을 노출합니다.<br /><br /> 기본값은 1입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<udpAnnouncementEndpoint>](udpannouncementendpoint.md)|고정 알림 계약 및 UDP 전송 바인딩이 있는 표준 엔드포인트입니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Discovery.UdpTransportSettings>
