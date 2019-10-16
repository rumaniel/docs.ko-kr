---
title: Windows Communication Foundation의 큐
ms.date: 03/30/2017
helpviewer_keywords:
- queues [WCF]
ms.assetid: 43008409-1bb4-4bd4-85d7-862c8f10ae20
ms.openlocfilehash: 6990d2b08f0ff729f0c0138c091c728a5ba59605
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64643549"
---
# <a name="queues-in-windows-communication-foundation"></a>Windows Communication Foundation의 큐
이 섹션의에서 항목에서는 큐에 대 한 Windows Communication Foundation (WCF) 지원을 설명합니다. WCF에서 활용 하 여 Microsoft Message Queuing (이전에 MSMQ 라고 함)를 전송으로 큐에 대 한 지원을 제공 하 고 다음 시나리오를 사용:  
  
- 느슨하게 결합된 애플리케이션. 송신 애플리케이션은 수신 애플리케이션이 메시지를 처리할 수 있는지 여부를 확인할 필요 없이 큐에 메시지를 보낼 수 있습니다. 큐는 수신 애플리케이션이 메시지를 처리할 수 있는 속도에 따라 변경되지 않는 일정한 속도로 송신 애플리케이션이 메시지를 큐에 보낼 수 있는 독립적인 프로세스를 제공합니다. 큐에 메시지를 보내는 작업이 메시지 처리 작업과 밀접하게 연결되지 않을 경우 전반적인 시스템 가용성이 증가합니다.  
  
- 실패 격리. 메시지를 큐에 보내거나 받는 애플리케이션이 서로 간에 영향을 주지 않고 실패할 수 있습니다. 예를 들어 수신 애플리케이션이 실패하더라도 송신 애플리케이션은 계속해서 큐에 메시지를 보낼 수 있습니다. 수신 응용 프로그램이 다시 활성화되면 큐에서 메시지를 처리할 수 있습니다. 실패 격리는 전체 시스템 안정성 및 가용성을 향상시킵니다.  
  
- 로드 조정. 송신 애플리케이션이 수신 애플리케이션을 메시지로 가득 채울 수 있습니다. 큐는 수신 응용 프로그램이 과부하가 걸리지 않도록 일치하지 않는 메시지 작성 및 사용률을 관리할 수 있습니다.  
  
- 연결이 끊긴 작업. 송신, 수신 및 처리 작업은 모바일 디바이스의 경우처럼 대기 시간이 긴 네트워크 또는 가용성이 제한된 네트워크에서 통신하는 경우 연결이 끊어질 수 있습니다. 큐를 사용하면 엔드포인트의 연결이 끊어지더라도 이러한 작업을 계속 수행할 수 있습니다. 다시 연결이 되면 큐가 메시지를 수신 애플리케이션으로 전달합니다.  
  
 WCF 응용 프로그램에서 큐 기능을 사용 하려면 표준 바인딩 중 하나를 사용 하거나 표준 바인딩 중 하나가 요구 사항을 충족 하지 않는 경우 사용자 지정 바인딩을 만들 수 있습니다. 관련 표준 바인딩과 하나를 선택 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: WCF 끝점을 사용 하 여 메시지를 교환 및 메시지 큐 응용](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)합니다. 사용자 지정 바인딩을 만드는 방법에 대한 자세한 내용은 [사용자 지정 바인딩](../../../../docs/framework/wcf/extending/custom-bindings.md)을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
 [큐 개요](../../../../docs/framework/wcf/feature-details/queues-overview.md)  
 메시지 큐 개념의 개요.  
  
 [WCF의 큐](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)  
 WCF 큐 지원의 개요입니다.  
  
 [방법: 대기 중인 메시지와 WCF 끝점 교환](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md)  
 사용 하는 방법에 설명 합니다 <xref:System.ServiceModel.NetMsmqBinding> WCF 클라이언트와 WCF 서비스 간에 통신 하는 클래스입니다.  
  
 [방법: 메시지와 WCF 끝점 및 응용 프로그램 큐 메시지를 교환 합니다.](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)  
 사용 하는 방법에 설명 합니다 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> WCF와 메시지 큐 응용 프로그램 간의 통신에 합니다.  
  
 [세션의 대기 중인 메시지 그룹화](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md)  
 단일 수신 애플리케이션으로 상호 관련된 메시지 처리를 용이하게 하기 위해 큐의 메시지를 그룹화하는 방법에 대해 설명합니다.  
  
 [트랜잭션에서 메시지 일괄 처리](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md)  
 메시지를 트랜잭션으로 일괄 처리하는 방법에 대해 설명합니다.  
  
 [배달 못 한 편지 큐를 사용하여 메시지 전송 오류 처리](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)  
 배달 못 한 편지 큐를 사용하여 메시지 전송 및 배달 실패를 처리하고 배달 못 한 편지 큐에서 메시지를 처리하는 방법에 대해 설명합니다.  
  
 [포이즌 메시지 처리](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)  
 포이즌 메시지(수신 애플리케이션에 전달하는 최대 배달 시도 횟수를 초과한 메시지)를 처리하는 방법에 대해 설명합니다.  
  
 [Windows Vista, Windows Server 2003 및 Windows XP의 큐 기능 차이점](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)  
 WCF 큐 기능 간의 차이점을 보여 줍니다 [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]합니다.  
  
 [전송 보안을 사용하여 메시지에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)  
 전송 보안을 사용하여 대기 중인 메시지의 보안을 유지하는 방법에 대해 설명합니다.  
  
 [메시지 보안을 사용하여 메시지에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-messages-using-message-security.md)  
 메시지 보안을 사용하여 대기 중인 메시지의 보안을 유지하는 방법에 대해 설명합니다.  
  
 [대기 중인 메시지 문제 해결](../../../../docs/framework/wcf/feature-details/troubleshooting-queued-messaging.md)  
 일반적인 큐 문제를 해결하는 방법에 대해 설명합니다.  
  
 [대기 중인 통신을 위한 최선의 방법](../../../../docs/framework/wcf/feature-details/best-practices-for-queued-communication.md)  
 WCF를 사용 하 여에 대 한 모범 사례 대기 통신에 설명 합니다.  
