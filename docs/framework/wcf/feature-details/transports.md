---
title: Windows Communication Foundation의 전송
ms.date: 03/30/2017
helpviewer_keywords:
- transports [WCF]
- WCF, transports
- Windows Communication Foundation, transports
ms.assetid: 005c894b-af70-48aa-a1c1-c99338083c27
ms.openlocfilehash: 6bb8e8b90c26533661684bd403b9ec439f1bb37e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61933733"
---
# <a name="transports-in-windows-communication-foundation"></a>Windows Communication Foundation의 전송
전송 계층은 채널 스택의 최하위 수준에 있습니다. Windows Communication Foundation (WCF)에서 사용 되는 기본 전송은 HTTP, HTTPS, TCP 및 명명 된 파이프 됩니다. 이 단원의 항목에서는 이러한 전송 중에서 특정 전송을 선택하여 구성하고 조정 속성을 설정하는 방법에 대해 설명합니다.  
  
 WCF에는 추가 전송을 포함합니다. 메시지 큐 (MSMQ 라고도 함) 전송에 대 한 정보를 참조 하세요 [Queues and Reliable Sessions](../../../../docs/framework/wcf/feature-details/queues-and-reliable-sessions.md)합니다. 피어-투-피어 전송에 대 한 정보를 참조 하세요 [피어-투-피어 네트워킹](../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [전송 선택](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)  
 세 가지 기본 전송과 그 중 하나를 선택하기 위해 고려해야 할 사항에 대해 설명합니다.  
  
 [메시지 인코더 선택](../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)  
 메시지 인코딩 바인딩 요소를 선택할 때 고려해야 할 사항에 대해 설명합니다.  
  
 [스트리밍 메시지 전송](../../../../docs/framework/wcf/feature-details/streaming-message-transfer.md)  
 스트리밍을 수행하도록 전송 계층을 구성하는 방법에 대해 설명합니다.  
  
 [HTTP 및 HTTPS 구성](../../../../docs/framework/wcf/feature-details/configuring-http-and-https.md)  
 HTTP 및 HTTPS 전송 바인딩 요소를 구성하는 방법에 대해 설명합니다.  
  
 [방법: WCF URL 예약을 제한 된 예약으로 바꿉니다.](../../../../docs/framework/wcf/feature-details/how-to-replace-the-wcf-url-reservation-with-a-restricted-reservation.md)  
 제한 된 WCFURL 예약을 사용 하는 방법을 설명 합니다.  
  
 [전송 할당량](../../../../docs/framework/wcf/feature-details/transport-quotas.md)  
 전송 계층에 사용할 수 있는 할당량을 설정할 때 고려해야 할 사항에 대해 설명합니다.  
  
 [NAT 및 방화벽 작업](../../../../docs/framework/wcf/feature-details/working-with-nats-and-firewalls.md)  
 방화벽을 사용하여 메시지를 주고 받을 경우 또는 NAT(Network Address Translation)를 사용할 경우 전송 계층을 구성하는 방법에 대해 설명합니다.  
  
 [Net.TCP 포트 공유](../../../../docs/framework/wcf/feature-details/net-tcp-port-sharing.md)  
 WCF의 Net.TCP 포트 공유 구성 요소를 사용 하는 방법에 설명 합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
  
 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
 <xref:System.ServiceModel.Channels.TcpTransportBindingElement>  
  
 <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>  
  
## <a name="related-sections"></a>관련 단원  
 [바인딩](../../../../docs/framework/wcf/feature-details/bindings.md)  
  
 [바인딩 확장](../../../../docs/framework/wcf/extending/extending-bindings.md)
