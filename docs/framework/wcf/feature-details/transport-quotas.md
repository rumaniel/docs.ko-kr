---
title: 전송 할당량
ms.date: 03/30/2017
helpviewer_keywords:
- transport quotas [WCF]
ms.assetid: 3e71dd3d-f981-4d9c-9c06-ff8abb61b717
ms.openlocfilehash: a40fa9beec1eabeb02c6ccc4e2ab8179aa49288c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64585780"
---
# <a name="transport-quotas"></a>전송 할당량
전송 할당량은 연결이 과도한 리소스를 사용하는 경우를 결정하는 정책 메커니즘입니다. 할당량은 할당량 값을 초과하면 추가 리소스를 사용하지 못하도록 설정된 절대 한계입니다. 전송 할당량은 악의적이거나 의도하지 않은 서비스 거부 공격을 방지합니다.  
  
 Windows Communication Foundation (WCF) 전송은 신중한 리소스 할당을 기반으로 하는 기본 할당량 값을 갖습니다. 이러한 기본값은 개발 환경 및 소규모 설치 시나리오에 적합합니다. 설치로 인해 리소스가 부족해지거나 추가 리소스를 사용할 수 있더라도 연결이 제한되는 경우 서비스 관리자는 전송 할당량을 검토하고 개별 할당량 값을 조정해야 합니다.  
  
## <a name="types-of-transport-quotas"></a>전송 할당량 유형  
 WCF 전송에는 세 가지 유형의 할당량이 있습니다.  
  
- *시간 제한* 오랜 시간에 대 한 리소스를 묶어 의존 하는 서비스 공격 거부를 완화 합니다.  
  
- *메모리 할당 제한* 단일 연결에서 시스템 메모리를 소진 하 고 다른 연결에 대 한 서비스 거부를 방지 합니다.  
  
- *컬렉션 크기 제한* 간접적으로 메모리를 할당 하거나 공급에 제한이 있는 리소스 사용을 바인딩합니다.  
  
## <a name="transport-quota-descriptions"></a>전송 할당량 설명  
 이 섹션에서는 표준 WCF 전송에 사용할 수 있는 전송 할당량을 설명합니다. HTTP (S), TCP/IP 및 명명 된 파이프 합니다. 사용자 지정 전송은 이 목록에 포함되지 않은 구성 가능한 할당량을 노출할 수 있습니다. 할당량에 대한 자세한 내용은 사용자 지정 전송 설명서를 참조하십시오.  
  
 각 할당량 설정에는 형식, 최소값 및 기본값이 있습니다. 할당량의 최대값은 형식에 의해 제한됩니다. 시스템 제한으로 인해 할당량을 최대값으로 설정할 수 없는 경우도 있습니다.  
  
|이름|형식|최소<br /><br /> 값|기본<br /><br /> 값|설명|  
|----------|----------|--------------------|-----------------------|-----------------|  
|`ChannelInitializationTimeout`|TimeSpan|1틱|5 초|처음에 읽는 동안 프리앰블을 보내기 위해 연결을 기다리는 최대 시간입니다. 이 데이터는 인증이 발생되기 전에 수신됩니다. 일반적으로 이 설정은 `ReceiveTimeout` 할당량 값보다 상당히 작습니다.|  
|`CloseTimeout`|TimeSpan|0|1분|전송에서 예외가 발생되기 전에 연결을 닫을 때까지 기다리는 최대 시간입니다.|  
|`ConnectionBufferSize`|정수|1|8KB|기본 전송의 전송 및 수신 버퍼 크기(바이트)입니다. 버퍼 크기를 늘리면 대용량 메시지 전송 시 처리량이 향상될 수 있습니다.|  
|`IdleTimeout`|TimeSpan|0|2분|풀 연결이 닫히기 전에 유휴 상태로 유지될 수 있는 최대 시간입니다.<br /><br /> 이 설정은 풀 연결에만 적용됩니다.|  
|`LeaseTimeout`|TimeSpan|0|5분|활성 풀 연결의 최대 수명입니다. 지정된 시간이 경과한 후 현재 요청이 서비스되면 연결이 닫힙니다.<br /><br /> 이 설정은 풀 연결에만 적용됩니다.|  
|`ListenBacklog`|정수|1|10|해당 엔드포인트에 대한 추가 연결이 거부되기 전에 수신기에서 지원할 수 없는 최대 연결 수입니다.|  
|`MaxBufferPoolSize`|Long|0|512KB|전송이 재사용 가능한 메시지 버퍼 풀링에 사용할 수 있는 최대 메모리(바이트)입니다. 풀이 메시지 버퍼를 제공할 수 없는 경우 임시로 새 버퍼를 할당하여 사용합니다.<br /><br /> 여러 채널 팩터리 또는 수신기를 만드는 설치에서 버퍼 풀에 대해 대용량 메모리를 할당할 수 있습니다. 이 시나리오에서 이 버퍼 크기를 줄이면 메모리 사용량을 상당히 줄일 수 있습니다.|  
|`MaxBufferSize`|정수|1|64KB|데이터 스트리밍에 사용되는 버퍼의 최대 크기(바이트)입니다. 이 전송 할당량을 설정하지 않았거나 전송이 스트리밍을 사용하지 않는 경우 할당량 값은 `MaxReceivedMessageSize` 할당량 값 및 <xref:System.Int32.MaxValue> 중 작은 값과 동일합니다.|  
|`MaxOutboundConnectionsPerEndpoint`|정수|1|10|특정 엔드포인트에 연결할 수 있는 나가는 연결의 최대 수입니다.<br /><br /> 이 설정은 풀 연결에만 적용됩니다.|  
|`MaxOutputDelay`|TimeSpan|0|200밀리초|단일 작업에서 추가 메시지를 일괄 처리하기 위한 전송 작업 후 기다리는 최대 시간입니다. 메시지는 기본 전송 버퍼가 가득 차기 전에 전송됩니다. 추가 메시지를 전송하더라도 지연 기간이 다시 설정되지 않습니다.|  
|`MaxPendingAccepts`|정수|1|1|수신기에서 수락될 때까지 대기할 수 있는 최대 채널 수입니다.<br /><br /> 수락 완료 및 새 수락 시작 사이에 시간 간격이 있습니다. 이 컬렉션 크기가 증가하면 이 간격 동안 연결된 클라이언트가 연결이 끊기지 않도록 할 수 있습니다.|  
|`MaxPendingConnections`|정수|1|10|애플리케이션에서 수락할 때까지 수신기에서 기다릴 수 있는 최대 연결 수입니다. 이 할당량 값을 초과하면 새 들어 오는 연결은 수락될 때까지 기다리지 않고 연결이 끊깁니다.<br /><br /> 메시지 보안과 같은 연결 기능을 통해 클라이언트가 둘 이상의 연결을 열 수 있습니다. 서비스 관리자는 이 할당량 값을 설정할 때 이러한 추가 연결을 고려해야 합니다.|  
|`MaxReceivedMessageSize`|Long|1|64KB|전송에서 예외가 발생하기 전에 헤더를 포함하여 받은 메시지의 최대 크기(바이트)입니다.|  
|`OpenTimeout`|TimeSpan|0|1분|전송에서 예외가 발생되기 전에 연결을 설정할 때까지 기다리는 최대 시간입니다.|  
|`ReceiveTimeout`|TimeSpan|0|10분|전송에서 예외가 발생되기 전에 읽기 작업이 완료될 때까지 기다리는 최대 시간입니다.|  
|`SendTimeout`|Timespan|0|1분|전송에서 예외가 발생되기 전에 쓰기 작업이 완료될 때까지 기다리는 최대 시간입니다.|  
  
 전송 할당량 `MaxPendingConnections` 및 `MaxOutboundConnectionsPerEndpoint`는 바인딩 또는 구성을 통해 설정될 때 `MaxConnections`라는 단일 전송 할당량에 결합됩니다. 바인딩 요소만 이러한 할당량 값을 개별적으로 설정할 수 있습니다. `MaxConnections` 전송 할당량의 최소값 및 기본값은 동일합니다.  
  
## <a name="setting-transport-quotas"></a>전송 할당량 설정  
 전송 할당량은 전송 바인딩 요소, 전송 바인딩, 애플리케이션 구성 또는 호스트 정책을 통해 설정됩니다. 이 문서에서는 호스트 정책을 통한 전송 설정에 대해서는 설명하지 않습니다. 호스트 정책 할당량에 대한 설정에 대해서는 기본 전송 설명서를 참조하십시오. 합니다 [HTTP 및 HTTPS 구성](../../../../docs/framework/wcf/feature-details/configuring-http-and-https.md) Http.sys 드라이버에 대 한 할당량 설정에 설명 합니다. HTTP, TCP/IP 및 명명된 파이프 연결과 관련하여 Windows 제한 구성에 대한 자세한 내용은 Microsoft 기술 자료를 검색하십시오.  
  
 기타 유형의 할당량은 전송에 간접적으로 적용됩니다. 메시지를 바이트로 변형하기 위해 전송에서 사용하는 메시지 인코더에서 자체 할당량 설정을 구성할 수 있습니다. 그러나 이러한 할당량은 사용하는 전송 형식에 독립적입니다.  
  
### <a name="controlling-transport-quotas-from-the-binding-element"></a>바인딩 요소에서 전송 할당량 제어  
 바인딩 요소를 통한 전송 할당량 설정은 전송 동작 제어 시 뛰어난 유연성을 제공합니다. Close, Open, Receive 및 Send 작업에 대한 기본 시간 제한은 채널 작성 시 바인딩에서 가져옵니다.  
  
|이름|HTTP|TCP/IP|명명된 파이프|  
|----------|----------|-------------|----------------|  
|`ChannelInitializationTimeout`||X|X|  
|`CloseTimeout`||||  
|`ConnectionBufferSize`||X|X|  
|`IdleTimeout`||X|X|  
|`LeaseTimeout`||X||  
|`ListenBacklog`||X||  
|`MaxBufferPoolSize`|X|X|X|  
|`MaxBufferSize`|X|X|X|  
|`MaxOutboundConnectionsPerEndpoint`||X|X|  
|`MaxOutputDelay`||X|X|  
|`MaxPendingAccepts`||X|X|  
|`MaxPendingConnections`||X|X|  
|`MaxReceivedMessageSize`|X|X|X|  
|`OpenTimeout`||||  
|`ReceiveTimeout`||||  
|`SendTimeout`||||  
  
### <a name="controlling-transport-quotas-from-the-binding"></a>바인딩에서 전송 할당량 제어  
 바인딩을 통한 전송 할당량 설정에서는 가장 일반적인 할당량 값에 대한 액세스를 제공하는 동시에 선택할 수 있는 간단한 할당량 집합을 제공합니다.  
  
|이름|HTTP|TCP/IP|명명된 파이프|  
|----------|----------|-------------|----------------|  
|`ChannelInitializationTimeout`||||  
|`CloseTimeout`|X|X|X|  
|`ConnectionBufferSize`||||  
|`IdleTimeout`||||  
|`LeaseTimeout`||||  
|`ListenBacklog`||X||  
|`MaxBufferPoolSize`|X|X|X|  
|`MaxBufferSize`|1|X|X|  
|`MaxOutboundConnectionsPerEndpoint`||2|2|  
|`MaxOutputDelay`||||  
|`MaxPendingAccepts`||||  
|`MaxPendingConnections`||2|2|  
|`MaxReceivedMessageSize`|X|X|X|  
|`OpenTimeout`|X|X|X|  
|`ReceiveTimeout`|X|X|X|  
|`SendTimeout`|X|X|X|  
  
1. `MaxBufferSize` 전송 할당량은 `BasicHttp` 바인딩에서만 사용할 수 있습니다. `WSHttp` 바인딩은 스트리밍된 전송 모드를 지원하지 않는 시나리오에 적용됩니다.  
  
2. 전송 할당량 `MaxPendingConnections` 및 `MaxOutboundConnectionsPerEndpoint`는 `MaxConnections`라는 단일 전송 할당량에 결합됩니다.  
  
### <a name="controlling-transport-quotas-from-configuration"></a>구성에서 전송 할당량 제어  
 애플리케이션 구성 시 바인딩의 속성에 직접 액세스할 때와 동일한 전송 할당량을 설정할 수 있습니다. 구성 파일에서 전송 할당량의 이름은 항상 소문자로 시작합니다. 예를 들어 바인딩의 `CloseTimeout` 속성은 구성에서 `closeTimeout` 설정에 해당하고 바인딩의 `MaxConnections` 속성은 구성의 `maxConnections` 설정에 해당합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
- <xref:System.ServiceModel.Channels.TcpTransportBindingElement>
- <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>
- <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
