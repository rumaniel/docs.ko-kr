---
title: Windows Vista, Windows Server 2003 및 Windows XP의 큐 기능 차이점
ms.date: 03/30/2017
helpviewer_keywords:
- queues [WCF], differences in operating systems
ms.assetid: aa809d93-d0a3-4ae6-a726-d015cca37c04
ms.openlocfilehash: 694d7af8e6e869a7a21a3414be6c69cf9f5e7c8f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64626991"
---
# <a name="differences-in-queuing-features-in-windows-vista-windows-server-2003-and-windows-xp"></a>Windows Vista, Windows Server 2003 및 Windows XP의 큐 기능 차이점
이 항목에서는 Windows Communication Foundation (WCF) 큐 기능 간의 차이점을 보여 줍니다 [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]합니다.  
  
## <a name="application-specific-dead-letter-queue"></a>애플리케이션별 배달 못한 편지 큐  
 대기 중인 메시지는 수신 애플리케이션이 적절한 시간 내에 메시지를 읽지 못하는 경우 무기한 큐에 남을 수 있습니다. 시간이 중요한 메시지인 경우에는 이 동작이 별로 좋지 않습니다. 시간이 중요한 메시지는 대기 중인 바인딩에서 `TimeToLive` 속성이 설정되어 있습니다. 이 속성은 메시지가 만료될 때까지 큐에 머물 수 있는 기간을 나타냅니다. 만료된 메시지는 배달 못한 편지 큐라는 특수 큐로 보내집니다. 또한 큐 할당량 초과 또는 인증 오류 등 다른 이유로 메시지가 배달 못한 편지 큐에 놓일 수도 있습니다.  
  
 일반적으로 큐 관리자를 공유하는 모든 대기 중인 애플리케이션에 대해 시스템 전체 수준의 배달 못한 편지 큐 하나가 존재합니다. 각 애플리케이션에 대해 배달 못한 편지 큐를 사용하면 이러한 애플리케이션에서 해당 애플리케이션별 배달 못한 편지 큐를 직접 지정하여 큐 관리자를 공유하는 대기 중인 애플리케이션을 서로 격리할 수 있습니다. 다른 애플리케이션과 배달 못한 편지 큐를 공유하는 애플리케이션에서는 큐에서 해당되는 메시지를 찾아야 합니다. 애플리케이션별 배달 못한 편지 큐를 사용하면 애플리케이션에서는 배달 못한 편지 큐에 있는 모든 메시지가 자신에 해당되는 것임을 확신할 수 있습니다.  
  
 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서는 애플리케이션별 배달 못한 편지 큐를 사용할 수 있습니다. [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서는 애플리케이션별 배달 못한 편지 큐를 사용할 수 없고 시스템 수준의 배달 못한 편지 큐를 사용해야 합니다.  
  
## <a name="poison-message-handling"></a>포이즌 메시지 처리  
 포이즌 메시지는 받는 애플리케이션에 전달하는 최대 배달 시도 횟수를 초과한 메시지입니다. 이 상황은 트랜잭션 큐에서 메시지를 읽는 애플리케이션이 오류 때문에 메시지를 즉시 처리할 수 없는 경우에 발생합니다. 애플리케이션에서 대기 중인 메시지를 받은 트랜잭션이 중단되면 메시지가 큐에 반환됩니다. 그러면 애플리케이션에서 새 트랜잭션으로 메시지를 다시 검색하려고 시도합니다. 오류를 일으킨 문제가 해결되지 않은 경우 받는 애플리케이션은 최대 배달 시도 횟수를 초과할 때까지 같은 메시지를 받고 중단하는 루프에 갇힐 수 있으며, 포이즌 메시지가 발생합니다.  
  
 [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]의 MSMQ(Message Queuing) 사이에서 포이즌 처리와 관련된 주요 차이점은 다음과 같습니다.  
  
- [!INCLUDE[wv](../../../../includes/wv-md.md)]의 MSMQ는 하위 큐를 지원하지만 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서는 하위 큐를 지원하지 않습니다. 하위 큐는 포이즌 메시지 처리에 사용됩니다. 재시도 큐와 포이즌 큐는 포이즌 메시지 처리 설정에 따라 만들어지는 애플리케이션 큐의 하위 큐입니다. `MaxRetryCycles`는 만들 재시도 하위 큐의 수를 지정합니다. 따라서 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 또는 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 실행하는 경우 `MaxRetryCycles`는 무시되며 `ReceiveErrorHandling.Move`는 허용되지 않습니다.  
  
- MSMQ는 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 네거티브 승인을 지원하지만 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서는 지원하지 않습니다. 받는 큐 관리자에서 네거티브 승인을 사용하면 거부된 메시지가 보내는 큐 관리자의 배달 못한 편지 큐에 들어갑니다. 따라서 `ReceiveErrorHandling.Reject`는 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 허용되지 않습니다.  
  
- [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 MSMQ는 메시지 배달 시도 횟수를 보관하는 메시지 속성을 지원합니다. 이 중단 횟수 속성은 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 사용할 수 없습니다. WCF는이 속성 하지 않을 수도 정확한 값을 WCF 서비스가 웹 팜에서 둘 이상에서 같은 메시지를 읽으면 되므로 중단 횟수가 메모리에 유지 합니다.  
  
## <a name="remote-transactional-read"></a>원격 트랜잭션 읽기  
 [!INCLUDE[wv](../../../../includes/wv-md.md)]의 MSMQ에서는 원격 트랜잭션 읽기를 지원합니다. 이를 통해 큐에서 읽기를 수행하는 애플리케이션을 큐가 호스팅된 컴퓨터와 다른 컴퓨터에 호스팅할 수 있습니다. 이 기능을 사용하면 중앙의 큐에서 읽기를 수행하는 서비스 팜을 구성하여 시스템의 전체적인 처리량을 높일 수 있습니다. 또한 메시지를 읽거나 처리하는 동안 오류가 발생하면 트랜잭션을 롤백하여 나중에 처리할 수 있도록 메시지를 큐에 남길 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [배달 못 한 편지 큐를 사용하여 메시지 전송 오류 처리](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)
- [포이즌 메시지 처리](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)
