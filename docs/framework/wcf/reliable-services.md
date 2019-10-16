---
title: 신뢰할 수 있는 서비스
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], reliable messaging
- Windows Communication Foundation [WCF], reliable messaging
- WCF [WCF], reliable sessions
- Windows Communication Foundation [WCF], reliable sessions
- service contracts [WCF], reliable services
ms.assetid: 07814ed0-0775-47f2-987b-d8134fdd5099
ms.openlocfilehash: 67da784646cd918d7ce4a269311eedb6abee5013
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651030"
---
# <a name="reliable-services"></a>신뢰할 수 있는 서비스
큐 및 신뢰할 수 있는 세션은 신뢰할 수 있는 메시징을 구현 하는 Windows Communication Foundation (WCF) 기능. 이 항목에서는 WCF의 신뢰할 수 있는 메시징 기능을 설명 합니다.  
  
 *신뢰할 수 있는 메시징* 어떻게 신뢰할 수 있는 메시징 소스는 (호출 합니다 *원본*) 신뢰할 수 있는 메시징 대상에 메시지를 안정적으로 전송 (호출를 *대상*).  
  
 신뢰할 수 있는 메시징에서는 다음 기능을 수행합니다.  
  
- 메시지 전송 또는 전송 실패와 상관없이 소스에서 대상으로 보낸 메시지에 대한 보증을 전송합니다.  
  
- 소스와 대상을 서로 분리합니다. 따라서 소스 및 대상의 실패와 복구를 따로 관리할 수 있으며 소스나 대상을 사용할 수 없는 경우라도 메시지를 안전하게 전송 및 전달할 수 있습니다.  
  
 하지만 신뢰할 수 있는 메시징에는 대기 시간이 길다는 단점이 있습니다. *대기 시간* 메시지가 소스에서 대상까지 도달 하는 데 걸리는 시간입니다. 따라서 WCF, 신뢰할 수 있는 메시징에 대 한 다음과 같은 유형의 제공 합니다.  
  
- [신뢰할 수 있는 세션](../../../docs/framework/wcf/feature-details/reliable-sessions.md), 대기 시간이 길다는 단점 없이 안전 하 게 전송 합니다.  
  
- [WCF의 큐](../../../docs/framework/wcf/feature-details/queues-in-wcf.md), 신뢰할 수 있는 전송 및 원본과 대상 간의 분리를 제공 합니다.  
  
## <a name="reliable-sessions"></a>신뢰할 수 있는 세션  
 신뢰할 수 있는 세션에서는 메시징 엔드포인트(소스와 대상)를 분리하는 매개자의 형식이나 개수에 상관없이, WS-Reliable Messaging 프로토콜을 사용하여 소스와 대상 간의 안전한 엔드투엔드 메시지 전송을 제공합니다. 여기에는 엔드포인트 간의 메시지 흐름에 필요한, SOAP를 사용하지 않는 전송 매개자(예: HTTP 프록시) 또는 SOAP를 사용하는 매개자(예: SOAP 기반 라우터나 브리지)가 포함됩니다. 전송에 실패한 경우 신뢰할 수 있는 세션은 메모리 내 전송 창을 사용하여 SOAP 메시지 수준 오류를 마스킹하고 다시 연결합니다.  
  
 신뢰할 수 있는 세션은 대기 시간이 짧은 안전한 메시지 전송을 제공하며, TCP가 IP 브리지를 통해 패킷을 지원하는 것과 같이, 프록시나 매개자를 통해 SOAP 메시지를 지원합니다. 신뢰할 수 있는 세션에 대 한 자세한 내용은 참조 하세요. [신뢰할 수 있는 세션](../../../docs/framework/wcf/feature-details/reliable-sessions.md)합니다.  
  
### <a name="queues"></a>큐  
 WCF에서에서 큐에 안전 하 게 전송할 메시지와 분리의 소스와 대상을 분리할 수 있지만 높은 대기 시간을 제공합니다. WCF 지연 통신을 기반으로 메시지 큐 (MSMQ) 빌드됩니다.  
  
 MSMQ는 Windows의 선택적 구성 요소로 제공되며 MSMQ 서비스는 Windows 서비스로 실행되고, 소스 대신 전송 큐에서 전송할 메시지를 캡처하여 대상 큐로 배달합니다. 대상 큐는 대상을 대신해 메시지를 수락하고 나중에 대상에서 메시지를 요청할 때 배달합니다. MSMQ 관리자는 전송 중에 메시지가 손실되지 않도록 안전한 메시지 전송 프로토콜을 구현합니다. 이러한 프로토콜에는 네이티브 프로토콜 또는 SRMP(SOAP Reliable Messaging Protocol)라고 하는 SOAP 기반 프로토콜이 해당됩니다.  
  
 큐 간의 안전한 메시지 전송과 결합된 분리를 통해, 느슨하게 결합된 애플리케이션이 안전하게 통신할 수 있습니다. 신뢰할 수 있는 세션과 달리 소스와 대상은 동시에 실행될 필요가 없습니다. 따라서 소스의 메시지 생산율과 대상의 메시지 소비율이 맞지 않을 경우, 큐가 부하 평준화 메커니즘으로 효과적으로 사용될 수 있습니다. 큐에 대 한 자세한 내용은 참조 하세요. [WCF의 큐](../../../docs/framework/wcf/feature-details/queues-in-wcf.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [신뢰할 수 있는 세션 개요](../../../docs/framework/wcf/feature-details/reliable-sessions-overview.md)
- [WCF의 큐](../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)
