---
title: 대기 중인 통신을 위한 최선의 방법
ms.date: 03/30/2017
helpviewer_keywords:
- queues [WCF], best practices
- best practices [WCF], queued communication
ms.assetid: 446a6383-cae3-4338-b193-a33c14a49948
ms.openlocfilehash: b2f64faab6df678182fb39174c8a558b298a8748
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64584981"
---
# <a name="best-practices-for-queued-communication"></a>대기 중인 통신을 위한 최선의 방법
이 항목에서는 Windows Communication Foundation (WCF)에서 대기 중인된 통신에 대 한 모범 사례를 제공합니다. 다음 단원에서는 시나리오 측면에서 권장되는 방법에 대해 설명합니다.  
  
## <a name="fast-best-effort-queued-messaging"></a>신속하고 가장 효율적인 대기 중인 메시징  
 대기 중인 메시징이 제공하는 분리와 가장 효율적인 보증 작업을 통해 신속하고도 고성능인 메시징이 필요한 시나리오의 경우, 비트랜잭션 큐를 사용하여 <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A> 속성을 `false`로 설정합니다.  
  
 또한 <xref:System.ServiceModel.MsmqBindingBase.Durable%2A> 속성을 `false`로 설정하여 디스크 쓰기 비용이 발생하지 않도록 선택할 수 있습니다.  
  
 보안 작업은 성능에 영향을 줍니다. 자세한 내용은 [성능 고려 사항](../../../../docs/framework/wcf/feature-details/performance-considerations.md)합니다.  
  
## <a name="reliable-end-to-end-queued-messaging"></a>신뢰할 수 있는 엔드투엔드 대기 중인 메시징  
 다음 단원에서는 엔드투엔드 신뢰할 수 있는 메시징이 필요한 시나리오에 대해 권장되는 방법을 설명합니다.  
  
### <a name="basic-reliable-transfer"></a>기본적으로 신뢰할 수 있는 전송  
 엔드투엔드 안정성을 위해 <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A> 속성을 `true`로 설정하여 전송을 보장합니다. 요구 사항에 따라 <xref:System.ServiceModel.MsmqBindingBase.Durable%2A> 속성을 `true` 또는 `false`로 설정할 수 있습니다. 기본값은 `true`입니다. 엔드투엔드 안정성을 위한 작업 중 하나로, 보통 <xref:System.ServiceModel.MsmqBindingBase.Durable%2A> 속성은 `true`로 설정됩니다. 성능을 유지하는 데 많은 노력이 필요하더라도 해당 메시지를 지속적으로 만들어 큐 관리자가 손상된 경우에도 메시지가 손실되지 않도록 합니다.  
  
### <a name="use-of-transactions"></a>트랜잭션 사용  
 트랜잭션을 사용하여 엔드투엔드 신뢰성을 보장할 수 있습니다. `ExactlyOnce` 보증은 메시지가 대상 큐에 배달되었는지만 보장합니다. 메시지가 수신되는 것을 보장하려면 트랜잭션을 사용합니다. 트랜잭션을 사용하지 않고 서비스가 손상될 경우, 배달되는 메시지가 손실되지만 실제 애플리케이션에 배달됩니다.  
  
### <a name="use-of-dead-letter-queues"></a>배달 못 한 편지 큐 사용  
 배달 못 한 편지 큐는 메시지가 대상 큐에 배달되지 못하는 경우 사용자에게 이를 알리는지 확인합니다. 시스템 제공 배달 못 한 편지 큐 또는 사용자 지정 배달 못 한 편지 큐를 사용할 수 있습니다. 일반적으로 사용자 지정 배달 못 한 편지 큐를 사용하는 것이 가장 좋은 방법입니다. 이 큐를 사용하면 애플리케이션에서 단일 배달 못 한 편지 큐로 배달 못 한 메시지를 보낼 수 있기 때문입니다. 그렇지 않을 경우 시스템에서 실행 중인 모든 애플리케이션에 대해 발생하는 모든 배달 못 한 메시지가 단일 큐에 배달됩니다. 그러면 각 애플리케이션은 배달 못 한 편지 큐를 검색하여 해당 애플리케이션과 관련된 배달 못 한 메시지를 찾아야 합니다. 가끔 MSMQ 3.0을 사용하는 경우처럼 사용자 지정 배달 못 한 편지 큐를 사용할 수 없는 경우도 있습니다.  
  
 엔드투엔드 신뢰할 수 있는 통신에 대해 배달 못 한 편지 큐 기능을 끄지 않는 것이 좋습니다.  
  
 자세한 내용은 [배달 못 한 편지 큐 메시지 전송 오류 처리를 사용 하 여](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)입니다.  
  
### <a name="use-of-poison-message-handling"></a>포이즌 메시지 처리 사용  
 포이즌 메시지 처리는 오류를 복구하여 메시지를 처리하는 기능을 제공합니다.  
  
 포이즌 메시지 처리 기능을 사용하는 경우 <xref:System.ServiceModel.MsmqBindingBase.ReceiveErrorHandling%2A> 속성이 적절한 값으로 설정되어 있는지 확인합니다. <xref:System.ServiceModel.ReceiveErrorHandling.Drop>으로 설정할 경우 데이터가 손실됩니다. 반면에 <xref:System.ServiceModel.ReceiveErrorHandling.Fault>로 설정하면 포이즌 메시지를 감지할 때 서비스 호스트에 오류가 발생합니다. MSMQ 3.0을 사용하는 경우 <xref:System.ServiceModel.ReceiveErrorHandling.Fault>가 데이터 손실을 방지하고 포이즌 메시지를 제거하기 위한 최상의 옵션입니다. MSMQ 4.0을 사용하는 경우 <xref:System.ServiceModel.ReceiveErrorHandling.Move> 방식을 권장합니다. <xref:System.ServiceModel.ReceiveErrorHandling.Move>는 큐에서 포이즌 메시지를 제거하여 서비스가 계속해서 새 메시지를 처리할 수 있도록 합니다. 그러면 포이즌 메시지 서비스가 포이즌 메시지를 개별적으로 처리할 수 있습니다.  
  
 자세한 내용은 [포이즌 메시지 처리](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)합니다.  
  
## <a name="achieving-high-throughput"></a>높은 처리량 달성  
 단일 엔드포인트에서 높은 처리량을 달성하려면 다음을 사용합니다.  
  
- 트랜잭션된 일괄 처리. 트랜잭션된 일괄처리를 사용하면 많은 메시지를 단일 트랜잭션으로 읽을 수 있습니다. 이를 통해 트랜잭션 커밋이 최적화되어 전체 성능이 향상됩니다. 일괄 처리 비용은 일괄 처리 내의 단일 메시지에 오류가 발생하는 경우 발생하며 이러한 경우 전체 일괄 처리가 롤백되고, 일괄 처리가 다시 안전할 때까지 메시지를 한 번에 하나씩 처리해야 합니다. 대부분의 경우 포이즌 메시지가 발생하는 경우는 드물기 때문에 일괄 처리는 특히 트랜잭션에 참여하는 다른 리소스 관리자가 있는 경우 시스템 성능 향상을 위한 기본적인 방법입니다. 자세한 내용은 [트랜잭션에서 메시지 일괄 처리](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md)합니다.  
  
- 동시성. 동시성은 처리량을 증가시키지만 또한 공유 리소스를 사용하는 데 영향을 줍니다. 자세한 내용은 [동시성](../../../../docs/framework/wcf/samples/concurrency.md)합니다.  
  
- 스로틀. 최적의 성능을 위해 디스패처 파이프라인의 메시지 수를 조절합니다. 이 작업을 수행 하는 방법의 예제를 참조 하세요 [제한](../../../../docs/framework/wcf/samples/throttling.md)합니다.  
  
 일괄 처리를 사용하는 경우 동시성 및 스로틀이 동시 일괄 처리로 변환됩니다.  
  
 높은 처리량 및 가용성을 달성 하려면 큐에서 읽은 WCF 서비스의 팜을 사용 합니다. 이를 사용하려면 이러한 모든 서비스가 동일한 엔드포인트에서 동일한 계약을 노출해야 합니다. 팜 접근 방식은 많은 서비스를 동일한 큐에서 모두 읽을 수 있기 때문에 생산율이 높은 메시지가 있는 애플리케이션에 가장 적합합니다.  
  
 MSMQ 3.0에서 팜을 사용하는 경우 트랜잭션된 원격 읽기를 지원하지 않습니다. MSMQ 4.0은 트랜잭션된 원격 읽기를 지원합니다.  
  
 자세한 내용은 [트랜잭션에서 메시지 일괄 처리](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md) 하 고 [Windows Vista, Windows Server 2003 및 Windows XP의 큐 기능 차이점](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)합니다.  
  
## <a name="queuing-with-unit-of-work-semantics"></a>작업 단위 의미 체계를 사용한 큐  
 일부 시나리오의 경우 큐에서 메시지 그룹이 관련될 수 있기 때문에 이러한 메시지의 순서 지정이 중요합니다. 이러한 시나리오에서는 관련 메시지 그룹을 단일 단위로 함께 처리합니다. 즉, 모든 메시지가 성공적으로 처리되거나 모두 처리되지 않습니다. 이러한 동작을 구현하려면 큐가 있는 세션을 사용하십시오.  
  
 자세한 내용은 [세션에서 대기 중인 메시지 그룹화](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md)합니다.  
  
## <a name="correlating-request-reply-messages"></a>요청-회신 메시지 상호 연결  
 일반적으로 큐는 단방향이지만 일부 시나리오에서는 수신한 회신을 이전에 보낸 요청과 상호 연결해야 하는 경우가 있습니다. 이러한 상호 연결이 필요한 경우 메시지에 상호 연결 정보가 포함된 자체 SOAP 메시지 헤더를 적용하는 것이 좋습니다. 일반적으로 보낸 사람은 이 헤더를 메시지에 첨부하고 받는 사람은 메시지 처리 및 회신 큐에 새 메시지로 다시 회신할 때 상호 연결 정보가 포함된 보낸 사람의 메시지 헤더를 첨부하여 보낸 사람이 요청 메시지를 통해 회신 메시지를 식별할 수 있도록 합니다.  
  
## <a name="integrating-with-non-wcf-applications"></a>비WCF 애플리케이션과 통합  
 사용 하 여 `MsmqIntegrationBinding` 아닌 WCF 서비스 또는 클라이언트를 사용 하 여 WCF 서비스 또는 클라이언트를 통합 하는 경우. 비 WCF 응용 프로그램에는 System.Messaging, COM +, Visual Basic을 사용 하 여 작성 된 MSMQ 응용 프로그램 수 또는 C++입니다.  
  
 `MsmqIntegrationBinding`을 사용하는 경우 다음 사항에 주의하십시오.  
  
- WCF 메시지 본문은 MSMQ 메시지 본문과 같습니다. 대기 중인된 바인딩을 사용 하 여 WCF 메시지를 보낼 때 WCF 메시지 본문은 MSMQ 메시지 내부에 배치 됩니다. MSMQ 인프라는 이러한 추가 정보를 인식하지 못하고 MSMQ 메시지만 확인합니다.  
  
- `MsmqIntegrationBinding`은 가장 많이 사용하는 serialization 형식을 지원합니다. serialization 형식에 기반한 일반 메시지의 본문 형식인 <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>은 다른 형식의 매개 변수를 가져옵니다. 예를 들어 <xref:System.ServiceModel.MsmqIntegration.MsmqMessageSerializationFormat.ByteArray>는 `MsmqMessage\<byte[]>`가 필요하고 <xref:System.ServiceModel.MsmqIntegration.MsmqMessageSerializationFormat.Stream>은 `MsmqMessage<Stream>`이 필요합니다.  
  
- XML serialization을 통해 지정할 수 있습니다 사용 하 여 알려진된 형식을 합니다 `KnownTypes` 특성을 [ \<동작 >](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) XML 메시지를 deserialize 하는 방법을 결정 한 후 사용 되는 요소.  
  
## <a name="see-also"></a>참고자료

- [WCF의 큐](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)
- [방법: 대기 중인 메시지와 WCF 끝점 교환](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md)
- [방법: 메시지와 WCF 끝점 및 응용 프로그램 큐 메시지를 교환 합니다.](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)
- [세션의 대기 중인 메시지 그룹화](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md)
- [트랜잭션에서 메시지 일괄 처리](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md)
- [배달 못 한 편지 큐를 사용하여 메시지 전송 오류 처리](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)
- [포이즌 메시지 처리](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)
- [Windows Vista, Windows Server 2003 및 Windows XP의 큐 기능 차이점](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)
- [전송 보안을 사용하여 메시지에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)
- [메시지 보안을 사용하여 메시지에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-messages-using-message-security.md)
- [대기 중인 메시지 문제 해결](../../../../docs/framework/wcf/feature-details/troubleshooting-queued-messaging.md)
