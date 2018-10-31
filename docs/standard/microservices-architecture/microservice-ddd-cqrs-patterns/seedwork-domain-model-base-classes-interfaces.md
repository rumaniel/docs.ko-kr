---
title: Seedwork(도메인 모델에 대해 재사용이 가능한 기본 클래스 및 인터페이스)
description: 컨테이너 화 된.NET 응용 프로그램을 위한 .NET Microservices 아키텍처 | Seedwork(도메인 모델에 대해 재사용이 가능한 기본 클래스 및 인터페이스)
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 12/12/2017
ms.openlocfilehash: 7a38d90caab2232c17d8d58ca0c57d5bb56b3ce9
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198398"
---
# <a name="seedwork-reusable-base-classes-and-interfaces-for-your-domain-model"></a>Seedwork(도메인 모델에 대해 재사용이 가능한 기본 클래스 및 인터페이스)

솔루션 폴더에 *SeedWork* 폴더가 포함되어 있습니다. *SeedWork* 폴더 도메인 엔터티 및 값 개체에 대 한 기본으로 사용할 수 있는 사용자 지정 기본 클래스를 포함 합니다. 각 도메인의 개체 클래스에 중복 코드가 없으므로 이러한 기본 클래스를 사용합니다. 이러한 유형의 클래스의 폴더는 *SeedWork*라고 하며 *프레임 워크* 같은 것이 아닙니다. *SeedWork*라고 하는 이유는 이 폴더에는 실제로 프레임워크라고 할 수 없는 재사용이 가능한 클래스의 작은 하위 집합 포함하기 때문입니다. *Seedwork*는 [Michael Feathers](https://www.artima.com/forums/flat.jsp?forum=106&thread=8826)가 도입해 [Martin Fowler](https://martinfowler.com/bliki/Seedwork.html)에 의해 유명해진 용어지만 해당 폴더를 Common, SharedKernel 또는 비슷한 이름으로 부를 수도 있습니다.

그림 9-12는 정렬 마이크로 서비스에서 도메인 모델 의 시드워크를 구성하는 클래스를 보여줍니다. 시드워크에는 엔터티와 ValueObject, 열거형을 포함한 몇 가지 인터페이스처럼 사용자 지정 기본 클래스가 있습니다. 이러한 인터페이스(IRepository 및 IUnitOfWork)는 인프라 계층에게 구현되어야 할 사항에 대해 알려줍니다. 이러한 인터페이스는 또한 응용 프로그램 계층에서 종속성 주입을 통해 사용됩니다.

![](./media/image13.PNG)

**그림 9-12**. 도메인 모델인 "시드워크" 기본 클래스 및 인터페이스의 샘플 집합

이 집합은 대부분 개발자가 공식 프레임 워크가 아닌 프로젝트 간에 공유하는 재사용을 복사하기 및 붙여넣기하는 형식입니다. 모든 레이어 또는 라이브러리에 시드워크가 있을 수 있니다. 그러나 클래스 및 인터페이스 집합이 충분히 큰 경우 단일 클래스 라이브러리를 만드는 것이 좋습니다.

## <a name="the-custom-entity-base-class"></a>사용자 지정 엔터티 기본 클래스

다음 코드는 엔터티 ID, [같음 연산자](/cpp/cpp/equality-operators-equal-equal-and-exclpt-equal), 엔터티별 도메인 이벤트 목록 같은 모든 도메인 엔터티가 같은 방법으로 사용할 수 있는 코드를 배치할 수 있는 엔터티 기본 클래스의 예제입니다.

```csharp
// COMPATIBLE WITH ENTITY FRAMEWORK CORE (1.1 and later)
public abstract class Entity
{
    int? _requestedHashCode;
    int _Id;    
    private List<INotification> _domainEvents;
    public virtual int Id 
    {
        get
        {
            return _Id;
        }
        protected set
        {
            _Id = value;
        }
    }

    public List<INotification> DomainEvents => _domainEvents;        
    public void AddDomainEvent(INotification eventItem)
    {
        _domainEvents = _domainEvents ?? new List<INotification>();
        _domainEvents.Add(eventItem);
    }
    public void RemoveDomainEvent(INotification eventItem)
    {
        if (_domainEvents is null) return;
        _domainEvents.Remove(eventItem);
    }

    public bool IsTransient()
    {
        return this.Id == default(Int32);
    }

    public override bool Equals(object obj)
    {
        if (obj == null || !(obj is Entity))
            return false;
        if (Object.ReferenceEquals(this, obj))
            return true;
        if (this.GetType() != obj.GetType())
            return false;
        Entity item = (Entity)obj;
        if (item.IsTransient() || this.IsTransient())
            return false;
        else
            return item.Id == this.Id;
    }

    public override int GetHashCode()
    {
        if (!IsTransient())
        {
            if (!_requestedHashCode.HasValue)
                _requestedHashCode = this.Id.GetHashCode() ^ 31;
            // XOR for random distribution. See:
            // https://blogs.msdn.microsoft.com/ericlippert/2011/02/28/guidelines-and-rules-for-gethashcode/
            return _requestedHashCode.Value;
        }
        else
            return base.GetHashCode();
    }
    public static bool operator ==(Entity left, Entity right)
    {
        if (Object.Equals(left, null))
            return (Object.Equals(right, null));
        else
            return left.Equals(right);
    }
    public static bool operator !=(Entity left, Entity right)
    {
        return !(left == right);
    }
}
```

엔터티별 도메인 이벤트 목록을 사용하는 이전 코드는 도메인 이벤트에 중점인 다음 섹션에서 설명됩니다. 

## <a name="repository-contracts-interfaces-in-the-domain-model-layer"></a>도메인 모델 계층에서의 리포지토리 계약(인터페이스)

리포지토리 계약은 단순히 각 집계에 사용할 리포지토리의 계약 요구사항을 나타내는 .NET 인터페이스입니다. 

EF Core 코드 또는 기타 모든 인프라 종속성과 코드(Linq, SQL, 등)를 갖춘 리포지토리는 도메인 모델 내에서 구현되어서는 안 되며, 해당 리포지토리는 사용자가 정의하는 인터페이스만을 구현해야합니다. 

이 방법(리포지토리 인터페이스를 도메인 모델 계층에 배치하는 것)과 관련된 패턴은 분리된 인터페이스 패턴입니다. Martin Fowler가 [설명](https://www.martinfowler.com/eaaCatalog/separatedInterface.html)한 것처럼 “분리된 인터페이스를 사용해 한 패키지의 인터페이스를 정의하되 또 다른 패키지의 인터페이스는 구현하십시오. 이처럼 인터페이스에 종속되어 있는 클라이언트는 해당 구현을 전혀 인식할 수 없습니다.”

구분된 인터페이스 패턴을 따르면 응용 프로그램 계층(이 경우는 마이크로 서비스에 대한 Web API 프로젝트)이 도메인 모델에서 정의된 요구사항에 대 한 종속성을 가질 수 있지만 인프라/지속성 계층에 직접 종속되지는 않습니다. 또한 종속성 주입을 사용해 레포지토리를 사용해 인프라/지속성 계층에서 구현되는 해당 구현을 격리할 수 있습니다.

예를 들어 IOrderRepository 인터페이스를 사용하는 다음 예제에서는 인프라 계층에서의 구현을 위해 OrderRepository 클래스가 어떤 작업이 필요한지 규정합니다. 응용 프로그램의 현재 구현에서는 해당 코드가 데이터베이스에 순서를 추가하거나 업데이트해야 합니다. 쿼리가 간단한 CQRS 접근 방법에 따라 분할되기 때문입니다.

```csharp
// Defined at IOrderRepository.cs
public interface IOrderRepository : IRepository<Order>
{
    Order Add(Order order);
        
    void Update(Order order);

    Task<Order> GetAsync(int orderId);
}

// Defined at IRepository.cs (Part of the Domain Seedwork)
public interface IRepository<T> where T : IAggregateRoot
{
    IUnitOfWork UnitOfWork { get; }
}
```

## <a name="additional-resources"></a>추가 자료

-   **Martin Fowler. 분리된 인터페이스.**
    [*https://www.martinfowler.com/eaaCatalog/separatedInterface.html*](https://www.martinfowler.com/eaaCatalog/separatedInterface.html)


>[!div class="step-by-step"]
[이전](net-core-microservice-domain-model.md)
[다음](implement-value-objects.md)
