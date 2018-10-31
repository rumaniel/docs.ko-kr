---
title: 마이크로 서비스(통합 이벤트) 간 이벤트 기반 통신 구현
description: 컨테이너 화 된.NET 응용 프로그램에 대한 .NET Microservices 아키텍처 | 마이크로 서비스(통합 이벤트) 간 이벤트 기반 통신 구현
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 12/11/2017
ms.openlocfilehash: 6a365c284d66ea24a9bb4caae51c63f22c79877b
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50194048"
---
# <a name="implementing-event-based-communication-between-microservices-integration-events"></a>마이크로 서비스(통합 이벤트) 간 이벤트 기반 통신 구현

앞서 설명한 대로 이벤트 기반 통신을 사용할 경우 마이크로 서비스는 비즈니스 엔터티를 업데이트할 때처럼 주목할 만한 무엇인가 발생할 때 이벤트를 게시합니다. 다른 마이크로 서비스는 해당 이벤트를 구독합니다. 마이크로 서비스가 이벤트를 수신하면 자체 비즈니스 엔터티를 업데이트할 수 있고 더 많은 이벤트가 게시되도록 할 수 있습니다. 해당 게시/구독 시스템은 일반적으로 이벤트 버스의 구현을 통해 수행됩니다. 이벤트 버스는 이벤트를 구독하고 취소하고 또 이벤트를 게시하기 위해 필요한 API를 갖춘 인터페이스로서 설계 가능합니다. 이벤트 버스는 비동기 통신을 지원하는 메시징 큐 또는 서비스 및 게시/구독 모델 같은 프로세스 간 통신 또는 메시징 서비스에 기반한 하나 이상의 구현이 가능합니다.

다양한 서비스로 확장하는 비즈니스 트랜잭션을 구현할 이벤트를 사용하여 해당 서비스 간의 최종 일관성을 제공합니다. 결국 일관된 트랜잭션은 일련의 배포된 작업으로 구성돼 있습니다. 각 작업에서 마이크로 서비스는 비즈니스 엔터티를 업데이트하고 다음 작업을 트리거하는 이벤트를 게시합니다.

![](./media/image19.PNG)

**그림 8-18**. 이벤트 버스에 기반한 이벤트 구동 통신

이 섹션에서는 그림 8-18에 보이는 것 같이 일반 이벤트 버스 인터페이스를 사용하여 .NET와의 통신을 구현할 수 있는 방법을 설명합니다. RabbitMQ, Azure Service Bus 또는 기타 다른 타사 오픈 소스나 상용 서비스 버스 같은 인프라 또는 다른 기술을 사용하는 다양한 잠재적인 구현이 있습니다.

## <a name="using-message-brokers-and-services-buses-for-production-systems"></a>생산 시스템을 위해 메시지 브로커나 서비스 버스 사용

아키텍처 섹션에서 설명한 대로, 추상적인 이벤트 버스를 구현하기 위한 여러 메시징 기술을 선택할 수 있습니다. 그러나 이러한 기술은 수준이 다양합니다. 예를 들어, 메시징 브로커 전송 기술인 RabbitMQ는 Azure Service Bus, NServiceBus, MassTransit, 또는 Brighter 같은 상업용 제품보다 수준이 낮습니다. 이런 제품 대부분은 RabbitMQ 또는 Azure Service Bus에 기반해 작업할 수 있습니다. 제품의 선택 기준은 응용 프로그램에 얼마나 많은 기본 확장성과 얼마나 많은 기능이 필요한지에 달려 있습니다.

개발 환경을 위한 이벤트 버스 개념 증명 구현하기 위해서는 eShopOnContainers 샘플에서와 같이 컨테이너로서 실행하는 RabbitMQ에서의 간단한 구현으로 충분할 수 있습니다. 높은 확장성이 필요한 중요 업무용 생산 시스템을 위해 Azure Service Bus를 평가하고 사용할 수 있습니다.

분산 개발을 더 쉽게 만드는 장기 운영 프로세스를 위한 [Sagas](https://docs.particular.net/nservicebus/sagas/) 같이 고수준의 추상적 개념과 더 풍성한 기능을 요구하는 경우, NServiceBus, MassTransit, Brighter 같은 기타 상업용 및 오픈소스 서비스 버스는 평가할 만한 가치가 있습니다. 이 경우 사용할 추상적 개념과 API는 일반적으로 사용자 자신의 추상적 개념([eShopOnContainers에 제공되는 단순 이벤트 버스 추상적 개념](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/BuildingBlocks/EventBus/EventBus/Abstractions/IEventBus.cs)과 같은)이 아닌 고수준의 서비스 버스에서 제공하는 추상적 개념이 됩니다. 이를 위해 [NServiceBus를 사용하여 포크된 eShopOnContainers](https://go.particular.net/eShopOnContainers)(특정 소프트웨어에 의해 구현된 추가 파생 샘플) 연구 가능

물론, RabbitMQ 및 Docker 같은 저수준의 기술을 기반으로 한 사용자 고유의 서비스 버스 기능은 항상 빌드할 수 있지만 "항목을 새로 개발하기 위해" 필요한 작업은 사용자 지정 엔터프라이즈 응용 프로그램에 지나치게 높은 비용이 들 수 있습니다.

## <a name="integration-events"></a>통합 이벤트

통합 이벤트는 여러 마이크로 서비스 또는 외부 시스템에 걸쳐 동기화된 도메인 상태 전환에 사용 됩니다. 이 작업은 마이크로 서비스 외부에 통합 이벤트를 게시함으로써 수행됩니다. 이벤트가 여러 수신기 마이크로 서비스(통합 이벤트를 구독하는 만큼 많은 마이크로 서비스)에 게시될 경우 각 수신기 마이크로 서비스에서의 적절한 이벤트 처리기가 해당 이벤트를 처리합니다.

통합 이벤트는 기본적으로 다음 예제와 같은 데이터 보유 클래스입니다.

```csharp
public class ProductPriceChangedIntegrationEvent : IntegrationEvent
{
    public int ProductId { get; private set; }
    public decimal NewPrice { get; private set; }
    public decimal OldPrice { get; private set; }

    public ProductPriceChangedIntegrationEvent(int productId, decimal newPrice,
        decimal oldPrice)
    {
        ProductId = productId;
        NewPrice = newPrice;
        OldPrice = oldPrice;
    }
}
```

통합 이벤트는 각 마이크로 서비스의 응용 프래그램 수준에서 정의될 수 있으므로 Viewmodel이 서버와 클라이언트에서 정의되는 방법과 유사한 방식으로 마이크로 서비스가 서로 분리됩니다. 여러 마이크로 서비스에 걸쳐 있는 일반적인 통합 이벤트 라이브러리의 공유는 권장되지 않습니다. 이렇게 하면 단일 이벤트 정의 데이터 라이브러리와 마이크로 서비스가 연결되게 됩니다. 여러 마이크로 서비스에 걸쳐 있는 공용 도메인 모델을 공유하고 싶지 않은 것과 동일한 이유로 이 작업을 수행하고 싶지 않습니다. 마이크로 서비스는 전적으로 자율적이어야 하기 때문입니다.

마이크로 서비스에 걸쳐 공유해야 할 몇 가지 유형의 라이브러리가 있습니다. 하나는 eShopOnContainers에서처럼 [이벤트 버스 클라이언트 API](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/BuildingBlocks/EventBus)와 같은 최종 응용 프로그램 블록으로서의 라이브러리입니다. 다른 하나는 JSON 직렬 변환기와 같은 NuGet 구성 요소로서 공유될 수 있는 도구를 구성하는 라이브러리입니다.

## <a name="the-event-bus"></a>이벤트 버스

이벤트 버스는 그림 8-19에 나와 있는 것 처럼 서로를 명확히 인식하기 위한 구성 요소를 요구 하지 않고 마이크로 서비스 간의 게시/구독-스타일 통신을 허용 합니다.

![](./media/image20.png)

**그림 8-19**. 이벤트 버스를 사용한 게시/구독 기본 사항

이벤트 버스는 관찰자 패턴 및 게시-구독 패턴과 관련이 있습니다.

### <a name="observer-pattern"></a>관찰자 패턴

[관찰자 패턴](https://en.wikipedia.org/wiki/Observer_pattern)에서, 기본 개체(관찰 가능한 객체라고도 함)가 관련 정보(이벤트)를 관심 있는 다른 개체(관찰자 라고도 함)에게 알려줍니다.

### <a name="publish-subscribe-pubsub-pattern"></a>게시-구독(Pub/Sub) 패턴 

[Pub/Sub 패턴](https://msdn.microsoft.com/library/ff649664.aspx)의 목적은 관찰자 패턴과 동일합니다. 특정 이벤트가 발생할 경우 다른 서비스에 알립니다. 하지만 관찰자 패턴과 Pub/Sub 패턴 간에는 중요한 차이가 있습니다. 관찰자 패턴에서는 관찰 가능 객체가 직접 관찰자에게 브로드캐스트를 수행함으로써 서로를 “알게”됩니다. 하지만 Pub/Sub 패턴을 사용할 경우 게시자 및 구독자 모두 알고 있는 브로커 또는 메시지 브로커 또는 이벤트 버스라는 세 번째 구성 요소가 있습니다. 따라서 Pub/Sub 패턴을 사용 하는 경우 게시자와 구독자는 앞서 언급한 이벤트 버스 또는 메시지 브로커 덕분에 정확하게 분리됩니다.

### <a name="the-middleman-or-event-bus"></a>매개자 또는 이벤트 버스 

게시자와 구독자 간에 익명성을 어떻게 달성합니까? 모든 통신을 매개자가 처리하게 하는 것이 간단한 방법입니다. 이벤트 버스는 이러한 매개자 중 하나입니다.

이벤트 버스는 일반적으로 두 부분으로 구성 됩니다.

-   추상적 개념 또는 인터페이스 및

-   하나 이상의 구현입니다.

그림 8-19에서는 응용 프로그램의 관점에서 이벤트 버스가 어떻게 Pub/Sub 채널에 불과한지 알 수 있습니다. 이 비동기 통신을 구현하는 방법은 달라질 수 있습니다. 환경 요구 사항에 따라 두 요구 사항(예를 들어, 생산 대 개발 환경)을 서로 교체할 수 있도록 다양한 구현 방법을 가질 수 있습니다.

그림 8-20에서는 RabbitMQ, Azure Service Bus 또는 다른 이벤트/메시지 브로커 같은 메시징 인프라 기술을 기반으로 다중 구현을 통해 이벤트 버스의 추상적 개념을 확인할 수 있습니다. 

![](./media/image21.png)

**그림 8- 20.** 이벤트 버스의 다중 구현

그러나 전에 언급 한 것 처럼 고유한 추상적 개념(이벤트 버스 인터페이스) 사용은 추상적 개념의 지원을 받는 기본 이벤트 버스 기능이 필요한 경우에만 유용합니다. 더 풍부한 서비스 버스 기능이 필요하면 고유한 추상적 개념 대신에 선호하는 상업용 서비스 버스가 제공하는 추상적 개념과 API를 사용해야 할지도 모릅니다. 

### <a name="defining-an-event-bus-interface"></a>이벤트 버스 인터페이스 정의

이벤트 버스 인터페이스에 대한 구현 코드 및 탐색 목적으로 가능한 구현부터 시작하도록 하겠습니다. 인터페이스는 다음 인터페이스에서와 같이 일반적이고 간단해야 합니다.

```csharp
public interface IEventBus
{
    void Publish(IntegrationEvent @event);

    void Subscribe<T, TH>()
        where T : IntegrationEvent
        where TH : IIntegrationEventHandler<T>;

    void SubscribeDynamic<TH>(string eventName)
        where TH : IDynamicIntegrationEventHandler;

    void UnsubscribeDynamic<TH>(string eventName)
        where TH : IDynamicIntegrationEventHandler;

    void Unsubscribe<T, TH>()
        where TH : IIntegrationEventHandler<T>
        where T : IntegrationEvent;
}
```

`Publish` 메서드는 간단합니다. 이벤트 버스는 모든 마이크로 서비스로 전달되는 통합 이벤트 또는 해당 이벤트를 구독하는 외부 응용 프로그램을 브로드캐스트합니다. 이 메서드 해당 이벤트를 게시하는 마이크로 서비스가 사용합니다.

`Subscribe` 메서드(인수에 따라 몇 가지 구현이 있을 수 있습니다)는 이벤트를 수신하려는 마이크로 서비스에서 사용됩니다. 이 메서드는 두 개의 인수를 갖습니다. 첫 번째는 (`IntegrationEvent`)을 구독할 통합 이벤트입니다. 두 번째 인수는 `IIntegrationEventHandler<T>`로 명명된 통합 이벤트 처리기(또는 콜백 메서드)로서, 수신기 마이크로 서비스가 해당 통합 이벤트 메시지를 수신할 때 실행됩니다.


>[!div class="step-by-step"]
[이전](database-server-container.md)
[다음](rabbitmq-event-bus-development-test-environment.md)
