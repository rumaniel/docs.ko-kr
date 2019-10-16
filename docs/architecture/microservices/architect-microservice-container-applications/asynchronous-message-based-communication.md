---
title: 비동기 메시지 기반 통신
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | 비동기 메시지 기반 통신은 마이크로 서비스 아키텍처에서 필수 개념입니다. 마이크로 서비스를 서로 독립적인 상태로 유지하는 동시에, 결국은 동기화된 상태로 유지하는 가장 좋은 방법이기 때문입니다.
ms.date: 09/20/2018
ms.openlocfilehash: 109737a04eac8cfc30c746d283ca71c697f5b29d
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834478"
---
# <a name="asynchronous-message-based-communication"></a>비동기 메시지 기반 통신

비동기 메시징 및 이벤트 기반 통신은 다양한 마이크로 서비스 및 해당 관련 도메인 모델에 걸쳐 변경 내용을 전파할 때 중요합니다. 앞서 마이크로 서비스 및 바운딩된 컨텍스트(BC) 논의에서 언급한 것처럼 모델(사용자, 고객, 제품, 계정 등)은 다른 마이크로 서비스 또는 BC에 대한 다른 것을 의미할 수 있습니다. 이는 곧 변경이 발생할 때 다른 모델 간의 변화를 조정할 어떤 방법이 필요하다는 의미입니다. 비동기 메시징에 기반한 이벤트 기반 통신 및 최종 일관성이 솔루션입니다.

메시징를 사용할 경우 프로세스는 비동기적으로 메시지를 교환하여 통신합니다. 클라이언트는 메시지를 전송해 서비스에 대한 명령이나 요청을 합니다. 해당 서비스는 응답할 필요가 있는 경우 클라이언트에 다른 메시지를 전송합니다. 이는 메시지 기반 통신이므로 클라이언트는 응답이 즉시 수신되지 않고 전혀 응답이 없을 수도 있음을 가정합니다.

메시지는 헤더(식별 또는 보안 정보 같은 메타데이터)와 본문으로 구성됩니다. 메시지는 일반적으로 AMQP 같은 비동기 프로토콜을 통해 전송됩니다.

마이크로 서비스 커뮤니티에서의 이러한 유형의 통신을 위해 선호하는 인프라는 SOA에 사용되는 오케스트레이터 및 대형 브로커와는 다른 간단한 메시지 브로커입니다. 간단한 메시지 브로커의 인프라를 일반적으로 "단순," RabbitMQ 또는 Azure Service Bus와 같은 클라우드에서 확장 가능한 서비스 버스와 같은 간단한 구현과 함께 메시지 브로커 역할만으로 작동합니다. 이 시나리오에서 대부분의 "스마트"한 생각은 메시지를 생성하고 소모하는 엔드포인트, 즉 마이크로 서비스에 여전히 존재합니다.

가능한 한 준수하려고 노력해야 하는 또 다른 규칙은 내부 서비스 간에 비동기 메시징만을 사용하고 또한 클라이언트 앱에서 프런트 엔드 서비스(API 게이트웨이 + 첫 번째 수준의 마이크로 서비스)까지만 동기 통신(HTTP 같은)을 사용하는 것입니다.

비동기 메시징 통신에는 단일 수신자 메시지 기반 통신 및 다중 수신자 메시지 기반 통신 등 두 가지가 있습니다. 다음 섹션에서는 이에 대한 세부 정보를 제공합니다.

## <a name="single-receiver-message-based-communication"></a>단일 수신자 메시지 기반 통신

단일 수신자와의 메시지 기반 비동기 통신은 채널을 통해 메시지를 읽고 해당 메시지를 단 한 번 처리하는 소비자에게 정확히 메시지가 전달되는 지점 간 통신이 있음을 의미합니다. 그러나 특별한 경우도 있습니다. 예를 들어, 오류에서 자동으로 복구되는 클라우드 시스템에서는 동일한 메시지를 여러 번 보낼 수 있습니다. 네트워크 또는 기타 오류로 인해 해당 클라이언트는 메시지 보내기를 재시도할 수 있어야 하며, 해당 서버는 특정 메시지를 한 번만 처리하기 위해 idempotent 되게 작업을 구현해야 합니다.

단일 수신자 메시지 기반 통신은 이 방법을 보여주는 그림 4-18과 같이 비동기 명령을 한 마이크로 서비스에서 다른 마이크로 서비스로 전송하기에 아주 적합합니다.

메시지 전송 기반 통신(명령 또는 이벤트를 통해)을 시작 하면 메시지 기반 통신을 동기 HTTP 통신과 혼합하지 마십시오.

![비동기 메시지를 수신하는 단일 마이크로 서비스](./media/asynchronous-message-based-communication/single-receiver-message-based-communication.png)

**그림 4-18**. 비동기 메시지를 수신하는 단일 마이크로 서비스

명령이 클라이언트 애플리케이션에서 오는 경우 HTTP 동기 명령처럼 구현될 수 있는지 유의하십시오. 보다 큰 확장성이 필요하거나 메시지 기반 비즈니스 프로세스가 이미 실행 중인 경우 메시지 기반 명령을 사용해야 합니다.

## <a name="multiple-receivers-message-based-communication"></a>다중 수신자 메시지 기반 통신

게시/구독 메커니즘을 보다 유연하게 사용할 수 있게 돼 발신자의 통신이 추가 구독자 마이크로 서비스나 외부 애플리케이션에 사용될 수 있습니다. 따라서 발송 서비스에서 [개방/폐쇄 원칙](https://en.wikipedia.org/wiki/Open/closed_principle)을 준수하도록 도와줍니다. 이렇게 추가 구독자는 발송자 서비스를 수정할 필요 없이 나중에 추가될 수 있습니다.

게시/구독 통신을 사용하는 경우 이벤트 버스 인터페이스를 사용하여 모든 구독자에게 이벤트를 게시할 수 있습니다.

## <a name="asynchronous-event-driven-communication"></a>비동기 이벤트 기반 통신

비동기 이벤트 기반 통신을 사용하는 경우 마이크로 서비스는 도메인 내에서 무언가 발생할 때 통합 이벤트를 게시하고, 다른 마이크로 서비스는 제품 카탈로그 마이크로 서비스에서의 가격 변동처럼 이를 인식해야 합니다. 추가 마이크로 서비스는 이벤트를 비동기적으로 수신할 수 있도록 해당 이벤트를 구독합니다. 이 경우, 수신자는 자체 도메인 엔터티를 업데이트할 수 있어 더 많은 통합 이벤트를 게시하게 할 수 있습니다. 해당 게시/구독 시스템은 일반적으로 이벤트 버스의 구현을 통해 수행됩니다. 이벤트 버스는 이벤트를 구독하거나 구독 취소하고 또한 이벤트를 게시하는 데 필요한 API를 갖춘 추상화 또는 인터페이스로 설계할 수 있습니다. 이벤트 버스는 비동기 통신 및 게시/구독 모델을 지원하는 메시징 큐 또는 서비스 같은 프로세스 간 브로커 또는 메시징 브로커에 기반한 하나 이상의 구현이 가능합니다.

시스템이 통합 이벤트 기반 최종 일관성을 사용할 경우 이 방법이 최종 사용자에게 완전히 명확해지는 것이 좋습니다. 해당 시스템은 클라이언트에서의 폴링 시스템 또는 SignalR 같이 통합 이벤트를 모방하는 방법을 사용해서는 안 됩니다. 최종 사용자와 비즈니스 소유자는 명시적으로 시스템에서 최종 일관성을 포용하고 대부분의 경우 명시적으로 밝히는 한 해당 비즈니스가 이 방법과 아무 문제가 없음을 인식해야 합니다. 이는 사용자가 몇 가지 결과를 즉시 볼 것으로 예상할 수 있고, 이는 최종 일관성에서는 발생하지 않을 수 있기 때문에 중요합니다.

앞서 [분산 데이터 관리의 문제 및 솔루션](distributed-data-management.md) 섹션에서 설명한 것 처럼 여러 마이크로 서비스에 걸쳐 있는 비즈니스 작업을 구현하기 위해 통합 이벤트를 사용할 수 있습니다. 따라서 해당 서비스 간의 최종 일관성을 유지해야 합니다. 결국 일관된 트랜잭션은 분산된 작업의 컬렉션으로 구성돼 있습니다. 각 작업에서 관련 마이크로 서비스는 도메인 엔터티를 업데이트 하고, 같은 엔드투엔드 비즈니스 작업 내에서 다음 작업을 발생시키는 또 다른 통합 이벤트를 게시합니다.

중요한 점은 동일한 이벤트를 구독하는 다양한 마이크로 서비스와 통신하고자 하는 것입니다. 이렇게 하기 위해 그림 4-19에 보이는 것처럼 이벤트 기반 통신에 기초해 메시지를 게시/구독할 수 있습니다. 이 게시/구독 메커니즘은 마이크로 서비스 아키텍처에만 적용되지 않습니다. 이는 DDD에서 [바운딩된 컨텍스트](https://martinfowler.com/bliki/BoundedContext.html)가 통신하는 방식이나 [명령 및 쿼리 역할 구분(CQRS)](https://martinfowler.com/bliki/CQRS.html) 아키텍처 패턴에서 쓰기 데이터베이스에서 읽기 데이터베이스로 업데이트하는 방식과 유사합니다. 목표는 분산된 시스템에 걸쳐 여러 데이터 원본 간의 최종 일관성을 유지하는 것입니다.

![비동기 이벤트 기반 통신을 보여 주는 다이어그램입니다.](./media/asynchronous-message-based-communication/asynchronous-event-driven-communication.png)

**그림 4-19**. 비동기 이벤트 기반 메시지 통신

비동기 이벤트 기반 통신에서 하나의 마이크로 서비스는 이벤트 버스에 이벤트를 게시하고 여러 마이크로 서비스가 이를 구독하여 알림을 받고 이에 대한 조치를 취할 수 있습니다. 해당 구현은 이벤트 기반 및 메시지 기반 통신을 위해 어떤 프로토콜을 사용할지 결정하게 됩니다. [AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol)는 신뢰할 수 있는 대기 중인 통신을 완수할 수 있게 합니다.

이벤트 버스를 사용할 경우 [RabbitMQ](https://www.rabbitmq.com/) 같은 메시지 브로커 또는 [Azure Service Bus with Topics](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions) 같은 서비스 버스로부터 API를 사용하는 코드를 통해 클래스에서 관련 구현에 기반한 추상적 개념 수준(이벤트 버스 인터페이스 같은)을 사용할 수 있습니다. 또는 이벤트 버스와 게시/구독 시스템을 활용하기 위해 NServiceBus, MassTransit, Brighter 같은 더 높은 수준의 서비스 버스를 사용할 수도 있습니다.

## <a name="a-note-about-messaging-technologies-for-production-systems"></a>생산 시스템용 메시징 기술에 대한 유의사항

추상적 이벤트 버스 구현을 위해 사용할 수 있는 메시징 기술은 다양한 수준입니다. 예를 들어, RabbitMQ(메시징 브로커 전송)과 Azure Service Bus 같은 제품은 RabbitMQ와 Azure Service Bus 위에서 작동할 수 있는 NServiceBus, MassTransit, Brighter 같은 제품보다 낮은 수준에 있습니다. 선택 기준은 애플리케이션에 얼마나 많은 기본 확장성과 얼마나 많은 기능이 필요한지에 달려 있습니다. 개발 환경을 위한 이벤트 버스 개념 증명을 구현하기 위해서는 eShopOnContainers 샘플에서와 같이 Docker 컨테이너에서 실행되는 RabbitMQ에서의 간단한 구현만으로 충분할 수 있습니다.

높은 확장성이 필요한 중요 업무용 생산 시스템을 위해 Azure Service Bus를 평가할 수 있습니다. 분산 애플리케이션 개발을 더 쉽게 해주는 상위 수준의 추상적 개념 및 기능을 위해서는 NServiceBus, MassTransit, Brighter 같은 다른 상용 및 오픈 소스 서비스 버스를 평가 하는 것이 좋습니다. 물론, RabbitMQ 및 Docker 같은 하위 수준의 기술을 기반으로 서비스 버스 기능을 직접 빌드할 수 있습니다. 그러나 배관 작업은 사용자 지정 엔터프라이즈 애플리케이션의 경우 너무 많은 비용이 들어갑니다.

## <a name="resiliently-publishing-to-the-event-bus"></a>이벤트 버스에 탄력적으로 게시

다중 마이크로 서비스에서 이벤트 기반 아키텍처를 구현하는 경우 문제는 트랜잭션에 기반을 둔 이벤트 버스로 관련 통합 이벤트를 탄력적으로 게시하는 동시에 원래 마이크로 서비스의 상태를 원자 단위로 업그레이드하는 방법입니다. 다음은 추가적으로 방법이 있을 수 있지만 이 방법을 완수하는 몇 가지 방법입니다.

- MSMQ와 같은 트랜잭션(DTC 기반) 큐를 사용합니다. (다만, 이는 레거시 방식입니다.)

- [트랜잭션 로그 마이닝](https://www.scoop.it/t/sql-server-transaction-log-mining)을 사용합니다.

- 전체 [이벤트 소싱](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing) 패턴을 사용합니다.

- [보낼 메일함 패턴](http://gistlabs.com/2014/05/the-outbox/) 사용: 이벤트를 만들고 게시하는 이벤트 생성자 구성 요소의 기본이 되는 메시지 큐로서의 트랜잭션 데이터베이스 테이블입니다.

비동기 통신을 사용할 때 고려해야 할 추가 토픽은 메시지 idempotence 및 메시지 중복입니다. 이들 토픽은 이 가이드의 뒷부분에 나오는 [마이크로 서비스(통합 이벤트) 간 이벤트 기반 통신 구현](../multi-container-microservice-net-applications/integration-event-based-microservice-communications.md) 섹션에서 다룹니다.

## <a name="additional-resources"></a>추가 자료

- **이벤트 기반 메시징** \
  <http://soapatterns.org/design_patterns/event_driven_messaging>

- **게시/구독 채널** \
  <https://www.enterpriseintegrationpatterns.com/patterns/messaging/PublishSubscribeChannel.html>

- **Udi Dahan. 명확한 CQRS** \
  <http://udidahan.com/2009/12/09/clarified-cqrs/>

- **CQRS(명령과 쿼리의 역할 구분)**  \
  <https://docs.microsoft.com/azure/architecture/patterns/cqrs>

- **바인딩된 컨텍스트 간 통신** \
  <https://docs.microsoft.com/previous-versions/msp-n-p/jj591572(v=pandp.10)>

- **최종 일관성** \
  <https://en.wikipedia.org/wiki/Eventual_consistency>

- **Jimmy Bogard. 복원력에 대한 리팩터링: 결합 평가** \
  <https://jimmybogard.com/refactoring-towards-resilience-evaluating-coupling/>

> [!div class="step-by-step"]
> [이전](communication-in-microservice-architecture.md)
> [다음](maintain-microservice-apis.md)
