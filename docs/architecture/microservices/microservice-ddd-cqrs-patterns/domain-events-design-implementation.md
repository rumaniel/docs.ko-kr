---
title: 도메인 이벤트. 디자인 및 구현
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | 집계 간에 통신을 설정하는 주요 개념인 도메인 이벤트의 세부적인 보기를 가져옵니다.
ms.date: 10/08/2018
ms.openlocfilehash: 4fe0c1fa04bbecb64783e070838ab796de4f90d6
ms.sourcegitcommit: 10db6551ea3c971470cf5d2cc21ba1cbcefe5c55
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72031846"
---
# <a name="domain-events-design-and-implementation"></a>도메인 이벤트: 디자인 및 구현

도메인 이벤트를 사용하여 도메인 내 변경의 파생 작업을 명시적으로 구현합니다. 다시 말해, DDD 용어를 사용하여, 도메인 이벤트를 사용하여 여러 집합체 전반에 파생 작업을 명시적으로 구현합니다. 선택적으로, 데이터베이스 잠금의 확장성을 높이고 영향을 줄이려면 동일한 도메인 내의 집합체 간에 최종 일관성을 사용합니다.

## <a name="what-is-a-domain-event"></a>도메인 이벤트란?

이벤트는 과거에 발생한 것입니다. 도메인 이벤트란 동일한 도메인의 다른 부분(프로세스 중)을 인식하고자 하는 도메인에서 발생한 이벤트입니다. 알림된 부분은 일반적으로 어떤 식으로든 이벤트에 대응합니다.

도메인 이벤트의 중요한 이점은 부작용이 명시적으로 표현될 수 있다는 것입니다.

예를 들어, Entity Framework를 사용하고 있고 일부 이벤트에 대한 반응이 있어야만 하는 경우에 이벤트를 트리거하는 것과 가까운 곳에 코딩할 수 있습니다. 따라서 규칙은 암시적으로 코드에 결합되고, 다행히 코드를 조사해서 규칙을 구현할 수 있습니다.

반면에 `DomainEvent`와 적어도 하나 이상의 `DomainEventHandler`가 포함되어 있기 때문에 도메인 이벤트를 사용하면 개념을 명시적으로 만듭니다.

예를 들어 eShopOnContainers 애플리케이션에서 주문이 생성되면 사용자가 구매자가 되므로 `ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler`에서 `OrderStartedDomainEvent`가 발생하고 처리되므로 기본 개념이 명확해집니다.

즉, 도메인 이벤트를 통해 도메인 전문가가 제공하는 유비쿼터스 언어에 기반한 도메인 규칙을 명시적으로 표현할 수 있습니다. 또한 도메인 이벤트를 사용하면 동일한 도메인 내의 클래스 간에 문제를 더 효과적으로 분리할 수 있습니다.

데이터베이스 트랜잭션과 마찬가지로 도메인 이벤트와 관련된 모든 작업이 성공적으로 완료되거나 수행되지 않아야 합니다.

도메인 이벤트는 메시징 스타일 이벤트와 유사하지만 한 가지 중요한 차이점이 있습니다. 실제 메시지, 메시지 큐, 메시지 broker 또는 AMQP를 사용하는 서비스 버스에서, 메시지는 항상 비동기식으로 전송되고 프로세스와 머신에서 통신됩니다. 이것은 다수의 바인딩된 컨텍스트, 마이크로 서비스 또는 다른 애플리케이션을 통합하는 데 유용합니다. 하지만 도메인 이벤트의 경우 현재 실행 중인 도메인 작업에서 이벤트를 발생시키려고 하지만 파생 작업은 동일한 도메인 내에서 발생하기를 바랍니다.

도메인 이벤트와 그 파생 작업(이벤트 처리기가 관리하는 이후에 트리거되는 동작)은 거의 즉시, 일반적으로 프로세스 내에서 그리고 동일한 도메인 내에서 발생해야 합니다. 따라서 도메인 이벤트는 동기 또는 비동기일 수 있습니다. 단, 통합 이벤트는 항상 비동기여야 합니다.

## <a name="domain-events-versus-integration-events"></a>도메인 이벤트와 통합 이벤트

도메인 및 통합 이벤트는 의미상으로 동일합니다. 즉, 방금 발생한 일에 대한 알림입니다. 하지만 구현은 달라야 합니다. 도메인 이벤트는 IoC 컨테이너 또는 다른 메서드를 기반으로 메모리 내 중재자로 구현될 수 있는 도메인 이벤트 디스패처에 푸시되는 메시지입니다.

반면에 통합 이벤트의 목적은 커밋된 트랜잭션 및 업데이트를 다른 마이크로 서비스, 바인딩된 컨텍스트 또는 외부 애플리케이션과 같은 추가적인 하위 시스템에 전파하는 것입니다. 따라서 엔터티가 성공적으로 지속되고 있는 경우에만 발생해야 하며, 그렇지 않으면 전체 작업이 발생하지 않은 것처럼 처리됩니다.

앞서 언급했듯이 통합 이벤트는 여러 마이크로 서비스(기타 바인딩된 컨텍스트) 또는 외부 시스템/애플리케이션 간에도 비동기 통신을 기반으로 해야 합니다.

따라서 이벤트 버스 인터페이스에는 잠재적인 원격 서비스 간에 분산된 프로세스 간 통신을 허용하는 인프라가 필요합니다. 상용 서비스 버스, 큐, 사서함으로 사용되는 공유된 데이터베이스 또는 그 밖의 분산된 푸시 기반 메시지 시스템을 기반으로 할 수 있습니다.

## <a name="domain-events-as-a-preferred-way-to-trigger-side-effects-across-multiple-aggregates-within-the-same-domain"></a>동일한 도메인 내의 여러 집합체 전반에서 파생 작업을 트리거하는 기본 방법인 도메인 이벤트

하나의 집계 인스턴스와 관련된 명령을 실행하기 위해 하나 이상의 추가 집합체에서 추가 도메인 규칙을 실행해야 하는 경우에는 해당 파생 작업이 도메인 이벤트에 의해 트리거되도록 설계하고 구현해야 합니다. 그림 7-14와 같이 가장 중요한 사용 사례 중 하나인 도메인 이벤트를 사용하여 동일한 도메인 모델 내의 여러 집계에 상태 변경 사항을 전파해야 합니다.

![집계 간의 일관성은 도메인 이벤트에 의해 달성되고, 주문 집계에서는 구매자 집계 업데이트로 처리되는 OrderStarted 도메인 이벤트를 보냅니다. ](./media/image15.png)

**그림 7-14**. 동일한 도메인 내의 여러 집합체 간에 일관성을 유지하기 위한 도메인 이벤트

그림에서 사용자가 주문을 시작하면 OrderStarted 도메인 이벤트는 ID 마이크로 서비스의 원래 사용자 정보를 기반으로(CreateOrder 명령에 제공된 정보를 사용하여) Ordering(주문) 마이크로 서비스에서 Buyer 개체 생성을 트리거합니다. 도메인 이벤트는 주문 집계가 처음 생성될 때 주문 집계에 의해 생성됩니다.

또는 집계 루트를 집합체의 멤버(자식 엔터티)가 생성한 이벤트에 가입시킬 수 있습니다. 예를 들어 각 OrderItem 자식 엔터티는 항목 가격이 특정 금액보다 높거나 제품 항목 가격이 너무 많으면 이벤트를 발생시킬 수 있습니다. 그런 다음, 집계 루트가 해당 이벤트를 수신하여 전역 계산 또는 집계를 수행합니다.

이런 이벤트 기반 통신은 집합체 내에서 직접 수행되지 않는 다는 점을 이해하는 것이 중요합니다. 도메인 이벤트 처리기를 구현해야 합니다.

도메인 이벤트 처리는 애플리케이션 관련 문제입니다. 도메인 모델 계층은 도메인 논리(도메인 전문가가 이해하는 논리)에만 집중해야 하며 리포지토리를 이용한 파생 작업 지속 동작 및 처리기와 같은 애플리케이션 인프라는 신경 쓸 필요가 없습니다. 따라서 애플리케이션 계층 수준은 도메인 이벤트가 발생할 때 동작을 트리거하는 도메인 이벤트 처리기가 있어야 하는 곳입니다.

도메인 이벤트는 다수의 애플리케이션 동작을 트리거하는 데에도 사용할 수 있으며 이보다 중요한 점은 향우 분리된 방식으로 이 숫자를 늘리는 것이 가능해야 한다는 점입니다. 예를 들어 주문이 시작되면 도메인 이벤트를 게시하여 해당 정보를 다른 집합체에 전파하거나 알림과 같은 애플리케이션 동작을 발생시킬 수 있습니다.

여기서 요점은 도메인 이벤트가 발생할 때 실행되는 동작의 수가 변화할 수 있다는 점입니다. 궁극적으로 도메인과 애플리케이션의 작업 및 규칙 수는 증가합니다. 어떤 일이 일어날 때 발생하는 파생 작업의 복잡성과 수는 증가하지만, 코드가 "접착제"(즉, `new`를 사용하여 특정 개체를 만드는 것)와 결합된 경우 새 작업을 추가해야 할 때마다 작업 및 테스트 코드도 변경해야 합니다.

이 변경으로 인해 새 버그가 발생할 수 있으며, 이 방식은 [SOLID](https://en.wikipedia.org/wiki/SOLID)의 [개방/폐쇄 원칙](https://en.wikipedia.org/wiki/Open/closed_principle)에도 위배됩니다. 뿐만 아니라, 작업을 오케스트레이션하는 원래 클래스가 계속 증가하게 되는데, 이것은 SRP([단일 책임 원칙](https://en.wikipedia.org/wiki/Single_responsibility_principle))에 위배됩니다.

반면에 도메인 이벤트를 사용하면 다음 방법을 사용하여 책임을 분리하여 세밀하고 분리된 구현을 생성할 수 있습니다.

1. 명령 보내기(예: CreateOrder).
2. 명령 처리기에서 명령 수신하기
   - 단일 집계의 트랜잭션 실행
   - (선택 사항) 파생 작업에 대해 도메인 이벤트 발생시키기(예: OrderStartedDomainEvent)
3. 여러 집합체나 애플리케이션 동작에서 다수의 파생 작업을 실행하는 도메인 이벤트(현재 프로세스 내) 처리 예:
   - buyer(구매자) 및 payment(지불) 메서드를 검증 또는 생성합니다.
   - 관련 통합 이벤트를 생성하고 이벤트 버스에 보내서 마이크로 서비스에 상태를 전파하거나 외부 동작(예: 구매자에게 이메일 보내기)을 트리거합니다.
   - 다른 파생 작업을 처리합니다.

그림 7-15와 같이 동일한 도메인 이벤트에서 시작하여, 도메인의 다른 집계와 관련된 여러 작업 또는 통합 이벤트 및 이벤트 버스를 연결하는 마이크로 서비스 전반에 걸쳐 수행해야 하는 추가 애플리케이션 작업을 처리할 수 있습니다.

![애플리케이션 계층에서 동일한 도메인 이벤트에 대한 여러 처리기가 있을 수 있으며, 하나의 처리기는 집계 간의 일관성을 해결할 수 있으며, 다른 처리기는 통합 이벤트를 게시할 수 있으므로 다른 마이크로 서비스와 함께 처리할 수 있습니다.](./media/image16.png)

**그림 7-15**. 도메인당 여러 동작 처리

이벤트 처리기는 일반적으로 애플리케이션 계층에 있는데, 리포지토리나 애플리케이션 API와 같은 인프라 개체를 마이크로 서비스의 동작에 사용하기 때문입니다. 이런 의미에서 이벤트 처리기는 명령 처리기와 유사하기 때문에 두 가지 모두 애플리케이션 계층의 일부입니다. 중요한 차이점은 명령을 한 번만 처리해야 한다는 것입니다. 도메인 이벤트는 0번 또는 *n*번 처리될 수 있습니다. 각 처리기마다 다른 목적으로 여러 수신자 또는 이벤트 처리기에서 수신될 수 있기 때문입니다.

도메인 이벤트당 처리기의 개수가 공개되어 있으면, 현재 코드에 영향을 주지 않고 필요에 따라 도메인 규칙을 추가할 수 있습니다. 예를 들어 다음과 같은 비즈니스 규칙을 구현하는 것은 몇 가지 이벤트 처리기를 추가(또는 하나만 추가)하는 것만큼 쉬울 수 있습니다.

> 상점에서 고객이 구매한 총 금액(주문 수와 상관없이)이 6,000달러를 초과하는 경우, 모든 신규 주문에 10% 할인을 적용하고 향후 주문에 대한 할인을 고객에게 이메일로 알립니다.

## <a name="implement-domain-events"></a>도메인 이벤트 구현

C#에서 도메인 이벤트는 DTO와 같이 단지 데이터를 보유하는 구조체 또는 클래스이며, 도메인에서 방금 발생한 내용과 관련된 모든 정보가 다음 예제와 같이 포함됩니다.

```csharp
public class OrderStartedDomainEvent : INotification
{
    public string UserId { get; }
    public int CardTypeId { get; }
    public string CardNumber { get; }
    public string CardSecurityNumber { get; }
    public string CardHolderName { get; }
    public DateTime CardExpiration { get; }
    public Order Order { get; }

    public OrderStartedDomainEvent(Order order,
                                   int cardTypeId, string cardNumber,
                                   string cardSecurityNumber, string cardHolderName,
                                   DateTime cardExpiration)
    {
        Order = order;
        CardTypeId = cardTypeId;
        CardNumber = cardNumber;
        CardSecurityNumber = cardSecurityNumber;
        CardHolderName = cardHolderName;
        CardExpiration = cardExpiration;
    }
}
```

이것은 본질적으로 OrderStarted 이벤트와 관련된 모든 데이터를 보유하는 클래스입니다.

도메인의 유비쿼터스 언어 측면에서 볼 때, 이벤트는 과거에 발생한 것이기 때문에 이벤트의 클래스 이름은 OrderStartedDomainEvent 또는 OrderShippedDomainEvent와 같이 과거 시제 동사로 나타내야 합니다. 이는 eShopOnContainers의 주문 마이크로 서비스에서 도메인 이벤트가 구현되는 방법입니다.

이전에 언급했듯이 이벤트의 중요한 특징은 이벤트는 과거에 발생한 것이므로 변경되지 않는다는 점입니다. 따라서 변경할 수 없는 클래스여야 합니다. 이전 코드에서 속성이 읽기 전용임을 알 수 있습니다. 개체를 업데이트할 방법이 없으며, 개체를 만들 때만 값을 설정할 수 있습니다.

여기서 중요한 것은 이벤트 개체를 직렬화 및 역 직렬화해야 하는 큐를 사용하여 도메인 이벤트를 비동기적으로 처리해야 하는 경우, 속성은 읽기 전용 대신 "개인 설정" 이어야 하므로 deserializer는 큐에서 제거할 때 값을 할당할 수 있습니다. 이는 도메인 이벤트 pub/sub가 MediatR을 사용하여 동기적으로 구현되므로 주문 마이크로 서비스에서는 문제가 되지 않습니다.

### <a name="raise-domain-events"></a>도메인 이벤트 발생

다음 질문은 관련 이벤트 처리기에 도달하도록 도메인 이벤트를 발생시키는 방법입니다. 여러 가지 방법을 사용할 수 있습니다.

Udi Dahan은 이벤트를 관리하고 발생시키기 위해 정적 클래스를 사용하도록 원래 제안했습니다(예: [Domain Events – Take 2](http://udidahan.com/2008/08/25/domain-events-take-2/)(도메인 이벤트 – 테이크 2)와 같은 몇 가지 관련 게시물). 여기에는 `DomainEvents.Raise(Event myEvent)`와 같은 구문을 사용하여, 도메인 이벤트가 호출될 때 즉시 발생시키는 DomainEvents라는 정적 클래스가 포함될 수 있습니다. Jimmy Bogard는 유사한 방식을 권장하는 블로그 게시물인 [Strengthening your domain: Domain Events](https://lostechies.com/jimmybogard/2010/04/08/strengthening-your-domain-domain-events/)(도메인: 강화: 도메인 이벤트)를 썼습니다.

하지만 도메인 이벤트 클래스가 정적인 경우 처리기에 즉시 디스패치됩니다. 이로 인해 테스트와 디버깅이 더 어려워지며, 이것은 파생 작업 논리가 있는 이벤트 처리기가 이벤트가 발생한 직후에 실행되기 때문입니다. 테스트 및 디버깅을 수행하는 경우에는 현재 집계 클래스 및 여기서 벌어지는 일에만 집중하는 것이 좋습니다. 다른 집합체나 애플리케이션 논리와 관련된 파생 작업에 대한 다른 이벤트 처리기로 갑자기 리디렉션되는 것은 좋지 않습니다. 이런 이유 때문에 다른 방식이 진화하였으며 이 내용은 다음 섹션에 설명되어 있습니다.

#### <a name="the-deferred-approach-to-raise-and-dispatch-events"></a>발생 및 디스패치 이벤트에 대한 지연된 접근 방법

도메인 이벤트 처리기에 즉시 디스패치하는 것보다 좋은 방법은 도메인 이벤트를 컬렉션에 추가한 다음, 트랜잭션을 커밋하기 *직전*이나 *바로* *후*에 도메인 이벤트를 디스패치하는 것입니다(EF의 SaveChanges와 같이). (이 방식은 Jimmy Bogard의 게시물인 [A better domain events pattern](https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/)(더 나은 도메인 이벤트 패턴)에 설명되어 있습니다.)

도메인 이벤트를 트랜잭션을 커밋하기 직전에 보낼지 또는 직후에 보낼지를 결정하는 것은 중요합니다. 그에 따라 파생 작업을 동일한 이벤트의 일부로 포함시킬 지 또는 다른 트랙잭션에 포함시킬 지가 결정되기 때문입니다. 후자의 경우 여러 집합체 전반에서 최종 일관성을 처리해야 합니다. 이 토픽은 다음 섹션에 설명되어 있습니다.

지연된 방식은 eShopOnContainers에 사용되는 방식입니다. 우선 엔터티에서 발생하는 이벤트를 엔터티당 이벤트 목록 또는 컬렉션에 추가합니다. 이 목록은 다음 Entity 기준 클래스 예제와 같이 엔터티 개체의 일부이거나 더 좋게는 기준 엔터티 클래스의 일부여야 합니다.

```csharp
public abstract class Entity
{
     //... 
     private List<INotification> _domainEvents;
     public List<INotification> DomainEvents => _domainEvents; 

     public void AddDomainEvent(INotification eventItem)
     {
         _domainEvents = _domainEvents ?? new List<INotification>();
         _domainEvents.Add(eventItem);
     }

     public void RemoveDomainEvent(INotification eventItem)
     {
         _domainEvents?.Remove(eventItem);
     }
     //... Additional code
}
```

이벤트를 발생시키려면 aggregate-root 엔터티의 메서드에 있는 코드에서 이벤트 컬렉션에 이벤트를 추가하기만 하면 됩니다.

다음 코드는 [eShopOnContainers의 Order agregate-root](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/AggregatesModel/OrderAggregate/Order.cs)의 일부이며 예제를 보여줍니다.

```csharp
var orderStartedDomainEvent = new OrderStartedDomainEvent(this, //Order object
                                                          cardTypeId, cardNumber,
                                                          cardSecurityNumber,
                                                          cardHolderName,
                                                          cardExpiration);
this.AddDomainEvent(orderStartedDomainEvent);
```

AddDomainEvent 메서드가 수행하는 유일한 작업은 목록에 이벤트를 추가하는 것입니다. 아직 디스패치된 이벤트가 없고 호출된 이벤트 처리기도 아직 없습니다.

나중에 데이터베이스에 트랜잭션을 커밋할 때 이벤트를 디스패치하려고 합니다. Entity Framework Core를 사용하는 경우, 다음 코드와 같이 EF DbContext의 SaveChanges 메서드를 의미합니다.

```csharp
// EF Core DbContext
public class OrderingContext : DbContext, IUnitOfWork
{
    // ...
    public async Task<bool> SaveEntitiesAsync(CancellationToken cancellationToken = default(CancellationToken))
    {
        // Dispatch Domain Events collection.
        // Choices:
        // A) Right BEFORE committing data (EF SaveChanges) into the DB. This makes
        // a single transaction including side effects from the domain event
        // handlers that are using the same DbContext with Scope lifetime
        // B) Right AFTER committing data (EF SaveChanges) into the DB. This makes
        // multiple transactions. You will need to handle eventual consistency and
        // compensatory actions in case of failures.        
        await _mediator.DispatchDomainEventsAsync(this);

        // After this line runs, all the changes (from the Command Handler and Domain
        // event handlers) performed through the DbContext will be committed
        var result = await base.SaveChangesAsync();
    }
}
```

이 코드를 사용하여 엔터티 이벤트를 해당 이벤트 처리기에 디스패치합니다.

도메인 이벤트 발생시키기를(메모리 목록에 간단히 추가하기) 이벤트 처리기에 도메인 이벤트를 디스패치하기와 분리시킨 것이 전반적인 결과입니다. 또한 사용 중인 디스패처의 종류에 따라 이벤트를 동기적으로 또는 비동기적으로 디스패치할 수 있습니다.

여기서 트랜잭션 경계가 중요한 역할을 한다는 점에 유의해야 합니다. 작업 단위와 트랜잭션이 둘 이상의 집합체에 있을 수 있으면(EF Core와 관계형 데이터베이스를 사용할 때처럼), 잘 작동할 수 있습니다. 하지만 트랜잭션이 여러 집합체에 있을 수 없으면(예: Azure CosmosDB와 같은 NoSQL 데이터베이스를 사용하는 경우) 일관성을 달성하기 위해 추가 단계를 구현해야 합니다. 이것은 지속성 무시가 보편적이지 않은 또 다른 이유이며, 사용하는 스토리지 시스템에 따라 달라집니다. 

### <a name="single-transaction-across-aggregates-versus-eventual-consistency-across-aggregates"></a>집합체 전반의 단일 트랜잭션 및 집합체 전반의 최종 일관성

집합체 전반에서 단일 트랜잭션을 수행할지 또는 집합체 전반에서 최종 일관성에 의존할지에 대한 질문에는 논쟁의 여지가 있습니다. Eric Evans 및 Vaughn Vernon과 같은 많은 DDD 작성자는 하나의 트랜잭션이 하나의 집계라는 규칙을 옹호하기 때문에 집합체 전반의 최종 일관성을 주장합니다. 예를 들어 Eric Evans의 저서인 *Domain-Driven Design*(도메인 기반 디자인)에는 다음과 같은 내용이 있습니다.

> 집합체에 걸쳐있는 규칙은 항상 최신 상태가 유지될 것으로 예상되지 않습니다. 이벤트 처리, 일괄 처리 또는 기타 업데이트 메커니즘을 통해 다른 종속성이 특정 시간 내에 확인될 수 있습니다. (128페이지)

Vaughn Vernon은 [Effective Aggregate Design. Part II: Making Aggregates Work Together](https://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf)(효과적인 집계 설계 2부: 집합체가 함께 작동하도록 만들기)에서 다음과 같이 언급하고 있습니다.

> 따라서 하나의 집계 인스턴스에서 명령을 실행하는 경우 하나 이상의 집합체에서 추가적인 비즈니스 규칙을 실행해야 하며, 최종 일관성을 사용하여 \[...\] DDD 모델에서 최종 일관성을 지원하는 실용적인 방법이 있습니다. 집계 메서드는 하나 이상의 비동기 구독자에게 제 시간에 배달되는 도메인 이벤트를 게시합니다.

이러한 근거는 많은 집합체나 엔터티에 걸쳐 있는 트랜잭션 대신 세분화된 트랜잭션을 수용하는 데 기반합니다. 두 번째의 경우, 높은 확장성이 필요한 대규모 애플리케이션에는 데이터베이스 잠금 수가 상당할 것이라는 생각 때문입니다. 확장성이 높은 애플리케이션은 여러 집합체 간에 즉각적인 트랜잭션 일관성이 필요하지 않다는 팩트를 수용하면 최종 일관성 개념을 받아들이는 데 도움이 됩니다. 비즈니스에서 원자성 변경은 필요하지 않은 경우가 많으며 특정 작업에 원자성 트랜잭션이 필요한지 여부를 결정하는 것은 어떤 경우든 도메인 전문가의 책임입니다. 작업에 여러 집합체 사이의 원자성 트랜잭션이 항상 필요한 경우에는 집계가 더 커야 하는지 또는 제대로 설계되지 않은 것인지에 의문을 가져야 합니다.

하지만 Jimmy Bogard와 같은 설계자나 다른 개발자는 단일 트랜잭션이 여러 집합체에 걸쳐 있어도 괜찮다고 합니다. 단, 추가적인 집합체가 동일한 원래 명령의 파생 작업과 관련이 있는 경우에 한합니다. 예를 들어 Bogard는 [A better domain events pattern](https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/)(더 나은 도메인 이벤트 패턴)에서 다음과 같이 언급하고 있습니다.

> 일반적으로 도메인 이벤트의 파생 작업이 논리 트랜잭션 내에서 발생하기를 바라지만 도메인 이벤트를 발생시키는 범위와 동일해야 하는 것은 아닙니다. \[...\] 트랜잭션을 커밋하기 직전에 이벤트를 해당 처리기에 디스패치합니다.

원래 트랜잭션을 커밋하기 직*전*에 도메인 이벤트를 디스패치하는 것은 이러한 이벤트의 파생 작업을 동일한 트랜잭션에 포함시키기를 바라기 때문입니다. 예를 들어 EF DbContext SaveChanges 메서드가 실패하면 트랜잭션은 관련 도메인 이벤트 처리기가 수행한 파생 작업의 결과를 비롯한 모든 변경 내용을 롤백합니다. 이것은 DbContext 수명 범위가 기본적으로 "범위 지정됨(scoped)"으로 정의되어 있기 때문입니다. 따라서 DbContext 개체는 동일한 범위나 개체 그래프 내에서 인스턴스화되는 다수의 리포지터리 개체 간에 공유됩니다. 이것은 Web API 또는 MVC 앱을 개발할 때 HttpRequest 범위와 일치합니다.

실제로 두 가지 방식(단일 원자성 트랜잭션 및 최종 일관성)이 모두 맞을 수 있습니다. 도메인이나 비즈니스 요구 사항 및 도메인 전문가의 의견에 따라 달라질 수 있습니다. 또한 서비스의 확장성이 얼마나 필요한지에 따라서도 달라집니다. (보다 세분화된 트랜잭션은 데이터베이스 잠금과 관련된 영향이 적습니다.) 코드에 투자할 의향이 얼마나 되는지에 따라서도 달라집니다. 최종 일관성을 위해서는 집합체 전반에서 잠재적인 비일관성을 감지하고 보정 작업을 구현하기 위해 더 복잡한 코드가 필요하기 때문입니다. 원래 집합체에 변경 내용을 커밋한 후 이벤트가 디스패치될 때 문제가 발생하고 이벤트 처리기가 파생 작업을 커밋할 수 없는 경우 집합체 사이에 불일치가 발생합니다.

보정 작업을 허용하는 방법은 추가 데이터베이스 테이블에 도메인 이벤트를 저장하여 원래 트랜잭션의 일부가 될 수 있도록 하는 것입니다. 이후에 현재 집합체 상태와 이벤트 목록을 비교하여 불일치를 감지하고 보정 작업을 실행하는 일괄 처리 프로세스를 구현할 수 있습니다. 보정 작업은 사용자 쪽에서도 비즈니스 사용자 및 도메인 전문가와의 토론을 비롯하여 심층적인 분석이 필요한 복잡한 토픽에 속합니다.

어떤 경우든 필요한 방식을 선택할 수 있습니다. 하지만 EF Core와 관계형 데이터베이스를 사용하는 경우에는 초기 지연 방식(커밋하기 전에 이벤트를 발생시키기 때문에 단일 트랜잭션을 사용)이 가장 간단한 방식입니다. 구현하기 쉽고 많은 비즈니스 사례에 유효합니다. eShopOnContainers의 Ordering(주문) 마이크로 서비스에 사용된 방식이기도 합니다.

하지만 이러한 이벤트를 해당 이벤트 처리기에 실제로 어떻게 디스패치합니까? 이전 예제에서 볼 수 있는 `_mediator` 개체는 무엇인가요? 이벤트와 이벤트 처리기 간의 매핑에 사용하는 기술 및 아티팩트와 관련이 있습니다.

### <a name="the-domain-event-dispatcher-mapping-from-events-to-event-handlers"></a>도메인 이벤트 디스패처: 이벤트에서 이벤트 처리기로 매핑

이벤트를 디스패치하거나 게시하는 것이 가능해지면 이벤트를 푸시할 아티팩트가 필요합니다. 그래야 모든 관련 처리기가 이벤트를 받아서 이를 기반으로 파생 작업을 처리할 수 있습니다.

한 가지 방법은 실제 메시지 시스템 또는 메모리 내 이벤트와 대조적으로 서비스 버스를 기반으로 할 수 있는 이벤트 버스입니다. 하지만 첫 번째의 경우, 동일한 프로세스 내(즉, 동일한 도메인 및 애플리케이션 계층 내)에 있는 이벤트만 처리하면 되기 때문에 실제 메시지는 도메인 이벤트를 처리하기에 과도합니다.

이벤트를 여러 이벤트 처리기에 매핑하는 또 다른 방법은 IoC 컨테이너의 형식 등록을 사용하여 이벤트를 디스패치할 곳을 동적으로 추론하는 것입니다. 다시 말해, 특정 이벤트를 얻기 위해 이벤트 처리기에 무엇이 필요한지 알아야 합니다. 그림 7-16은 이 방식에 대한 간단한 방법을 보여줍니다.

![MediatR에서 사용하는 방법인 종속성 주입을 사용하여 이벤트를 이벤트 처리기와 연관시킬 수 있습니다.](./media/image17.png)

**그림 7-16**. IoC를 사용한 도메인 이벤트 디스패처

배관 및 아티팩트를 모두 구축하여 이런 방식을 직접 구현할 수 있습니다. 하지만 커버에서 IoC 컨테이너를 사용하는 [MediatR](https://github.com/jbogard/MediatR)와 같은 사용 가능한 라이브러리를 사용할 수도 있습니다. 그러면 미리 정의된 인터페이스 및 중재자 개체의 게시/디스패치 메서드를 직접 사용할 수 있습니다.

코드에서 먼저 IoC 컨테이너에 이벤트 처리기 형식을 등록해야 합니다. 다음은 [eShopOnContainers Ordering(주문) 마이크로 서비스](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Infrastructure/AutofacModules/MediatorModule.cs)의 예제입니다.

```csharp
public class MediatorModule : Autofac.Module
{
    protected override void Load(ContainerBuilder builder)
    {
        // Other registrations ...
        // Register the DomainEventHandler classes (they implement IAsyncNotificationHandler<>)
        // in assembly holding the Domain Events
        builder.RegisterAssemblyTypes(typeof(ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler)
                                       .GetTypeInfo().Assembly)
                                         .AsClosedTypesOf(typeof(IAsyncNotificationHandler<>));
        // Other registrations ...
    }
}
```

먼저 코드는 처리기가 있는 어셈블리를 찾아서 도메인 이벤트 처리기가 포함된 어셈블리를 식별하지만(typeof(ValidateOrAddBuyerAggregateWhenXxxx) 사용) 다른 이벤트 처리기를 선택하여 어셈블리를 찾을 수도 있습니다. 모든 이벤트 처리기가 IAsyncNotificationHandler 인터페이스를 구현하기 때문에 코드는 해당 형식을 검색하여 모든 이벤트 처리기를 등록합니다.

### <a name="how-to-subscribe-to-domain-events"></a>도메인 이벤트 구독 방법

MediatR을 사용하는 경우 각 이벤트 처리기는 INotificationHandler 인터페이스의 제네릭 매개 변수에 제공된 이벤트 형식을 사용해야 합니다. 다음 코드를 참조하세요.

```csharp
public class ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler
  : IAsyncNotificationHandler<OrderStartedDomainEvent>
```

구독이라고 간주할 수 있는 이벤트와 이벤트 처리기 사이의 관계를 기반으로 MediatR 아티팩트는 각 이벤트에 대한 모든 이벤트 처리기를 검색하고 해당되는 각각의 이벤트 처리기를 트리거할 수 있습니다.

### <a name="how-to-handle-domain-events"></a>도메인 이벤트 처리 방법

마지막으로 이벤트 처리기는 대개 인프라 리포지토리를 사용하여 필요한 추가 집합체를 확보하고 파생 작업 도메인 논리를 실행하는 애플리케이션 계층 코드를 구현합니다. 다음 [eShopOnContainers의 도메인 이벤트 처리기 코드](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/DomainEventHandlers/OrderStartedEvent/ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler.cs)에서 구현 예제를 참조하세요.

```csharp
public class ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler
                   : INotificationHandler<OrderStartedDomainEvent>
{
    private readonly ILoggerFactory _logger;
    private readonly IBuyerRepository<Buyer> _buyerRepository;
    private readonly IIdentityService _identityService;

    public ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler(
        ILoggerFactory logger,
        IBuyerRepository<Buyer> buyerRepository,
        IIdentityService identityService)
    {
        // ...Parameter validations...
    }

    public async Task Handle(OrderStartedDomainEvent orderStartedEvent)
    {
        var cardTypeId = (orderStartedEvent.CardTypeId != 0) ? orderStartedEvent.CardTypeId : 1;        
        var userGuid = _identityService.GetUserIdentity();
        var buyer = await _buyerRepository.FindAsync(userGuid);
        bool buyerOriginallyExisted = (buyer == null) ? false : true;

        if (!buyerOriginallyExisted)
        {
            buyer = new Buyer(userGuid);
        }

        buyer.VerifyOrAddPaymentMethod(cardTypeId,
                                       $"Payment Method on {DateTime.UtcNow}",
                                       orderStartedEvent.CardNumber,
                                       orderStartedEvent.CardSecurityNumber,
                                       orderStartedEvent.CardHolderName,
                                       orderStartedEvent.CardExpiration,
                                       orderStartedEvent.Order.Id);

        var buyerUpdated = buyerOriginallyExisted ? _buyerRepository.Update(buyer) 
                                                                      : _buyerRepository.Add(buyer);

        await _buyerRepository.UnitOfWork
                .SaveEntitiesAsync();

        // Logging code using buyerUpdated info, etc.
    }
}
```

이전 도메인 이벤트 처리기 코드는 인프라 리포지토리를 사용하기 때문에 애플리케이션 계층 코드로 간주되었습니다. 이 내용은 인프라 지속성 계층에 관한 다음 섹션에 설명되어 있습니다. 이벤트 처리기는 다른 인프라 구성 요소도 사용할 수 있습니다.

#### <a name="domain-events-can-generate-integration-events-to-be-published-outside-of-the-microservice-boundaries"></a>도메인 이벤트는 마이크로 서비스 경계 밖에 게시할 통합 이벤트를 생성할 수 있습니다.

마지막으로 여러 마이크로 서비스에 걸쳐 이벤트를 전파해야 하는 경우가 있을 수 있다는 것을 언급하는 것이 중요합니다. 이 전파는 통합 이벤트로서, 특정 도메인 이벤트 처리기의 이벤트 버스를 통해 게시될 수 있습니다.

## <a name="conclusions-on-domain-events"></a>도메인 이벤트에 대한 결론

언급했듯이, 도메인 이벤트를 사용하여 도메인 내 변경의 파생 작업을 명시적으로 구현합니다. DDD 용어를 사용하려면, 도메인 이벤트를 사용하여 하나 또는 여러 집합체 전반에 파생 작업을 명시적으로 구현합니다. 추가적으로, 데이터베이스 잠금의 확장성을 높이고 영향을 줄이려면 동일한 도메인 내의 집합체 간에 최종 일관성을 사용합니다.

## <a name="additional-resources"></a>추가 자료

- **Greg Young. 도메인 이벤트란?** \
  <https://cqrs.files.wordpress.com/2010/11/cqrs_documents.pdf#page=25>

- **Jan Stenberg. 도메인 이벤트 및 최종 일관성** \
  <https://www.infoq.com/news/2015/09/domain-events-consistency>

- **Jimmy Bogard. 더 나은 도메인 이벤트 패턴** \
  <https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/>

- **Vaughn Vernon. 효과적인 집계 설계 2부: 집합체가 함께 작동하도록 만들기)에서 다음과 같이 언급하고 있습니다.**  \
  [https://dddcommunity.org/wp-content/uploads/files/pdf\_articles/Vernon\_2011\_2.pdf](https://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf)

- **Jimmy Bogard. 도메인 강화: 도메인 이벤트** \
  <https://lostechies.com/jimmybogard/2010/04/08/strengthening-your-domain-domain-events/>

- **Tony Truong. 도메인 이벤트 패턴 예제** \
  <https://www.tonytruong.net/domain-events-pattern-example/>

- **Udi Dahan. 완벽하게 캡슐화된 도메인 모델을 만드는 방법** \
  <http://udidahan.com/2008/02/29/how-to-create-fully-encapsulated-domain-models/>

- **Udi Dahan. 도메인 이벤트 - 테이크 2** \
  <http://udidahan.com/2008/08/25/domain-events-take-2/>

- **Udi Dahan. 도메인 이벤트 - 구원** \
  <http://udidahan.com/2009/06/14/domain-events-salvation/>

- **Jan Kronquist. 도메인 이벤트를 게시하지 말고 반환하라!** \
  <https://blog.jayway.com/2013/06/20/dont-publish-domain-events-return-them/>

- **Cesar de la Torre. Domain Events vs. DDD 및 마이크로 서비스 아키텍처의 통합 이벤트** \
  <https://devblogs.microsoft.com/cesardelatorre/domain-events-vs-integration-events-in-domain-driven-design-and-microservices-architectures/>

>[!div class="step-by-step"]
>[이전](client-side-validation.md)
>[다음](infrastructure-persistence-layer-design.md)
