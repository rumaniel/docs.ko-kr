---
title: 인프라 지속성 계층 디자인
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | 인프라 지속성 계층 디자인에서 리포지토리 패턴을 탐색합니다.
ms.date: 10/08/2018
ms.openlocfilehash: 76f545403a1b595ce7a541a96d212b9406d89c10
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674120"
---
# <a name="design-the-infrastructure-persistence-layer"></a>인프라 지속성 계층 디자인

데이터 지속성 구성 요소는 마이크로 서비스(즉, 마이크로 서비스의 데이터베이스)의 경계 내에서 호스팅된 데이터에 대한 액세스를 제공합니다. 이 구성 요소에는 사용자 지정 EF(Entity Framework) <xref:Microsoft.EntityFrameworkCore.DbContext> 개체와 같은 [작업 단위](https://martinfowler.com/eaaCatalog/unitOfWork.html) 클래스 및 리포지토리 등의 구성 요소의 실제 구현을 포함합니다. EF DbContext는 리포지토리와 작업 단위 패턴을 모두 구현합니다.

## <a name="the-repository-pattern"></a>리포지토리 패턴

리포지토리는 데이터 원본에 액세스하는 데 필요한 논리를 캡슐화하는 클래스 또는 구성 요소입니다. 리포지토리는 공통 데이터 액세스 기능에 집중해 더 나은 유지관리를 제공하고 도메인 모델 계층에서 데이터베이스에 액세스하는 데 사용되는 기술이나 인프라를 분리합니다. Entity Framework와 같은 ORM(개체 관계 매핑)을 사용하는 경우 LINQ 및 강력한 형식화 덕분에 구현해야 할 코드가 간소화됩니다. 이렇게 하면 데이터 액세스 내부 작업보다 데이터 지 속성 논리에 더 집중하게 합니다.

이런 리포지토리 패턴은 데이터 원본을 사용한 작업의 잘 문서화된 방법입니다. [엔터프라이즈 애플리케이션 아키텍처 패턴(Patterns of Enterprise Application Architecture)](https://www.amazon.com/Patterns-Enterprise-Application-Architecture-Martin/dp/0321127420/)이란 책에서, Martin Fowler는 다음과 같이 리포지토리에 대해 설명 합니다.

> 리포지토리는 도메인 모델 계층과 데이터 매핑의 중간자 역할을 하며 메모리의 도메인 개체 집합에 대해서도 비슷한 방식으로 작업을 수행합니다. 클라이언트 개체는 쿼리를 선언적으로 빌드하고 리포지토리로 보내 답변합니다. 개념적으로, 리포지토리는 데이터베이스 내에 저장된 개체 집합과 수행할 수 있는 작업을 캡슐화해 지속성 계층에 더 가까운 방법을 제공합니다. 리포지토리는 또한 작업 도메인 및 데이터 할당 또는 매핑 간의 종속성을 명확하게 한 방향으로 구분하려는 목적을 지원합니다.

### <a name="define-one-repository-per-aggregate"></a>집계 당 하나의 리포지토리 정의

각 집계 또는 집계 루트에 대해 하나의 리포지토리 클래스를 만들어야 합니다. DDD(도메인 기반 디자인) 패턴을 기반으로 한 마이크로 서비스에서 데이터베이스 업데이트에 사용해야 하는 유일한 채널은 리포지토리여야 합니다. 즉, 집계의 invariant와 트랜잭션 일관성을 제어하는 집계 루트와 일대일 관계를 갖기 때문입니다. 다른 채널(CQRS 방법을 따를 수 있을 때)을 통해 데이터베이스를 쿼리하는 것이 좋습니다. 쿼리는 데이터베이스 상태를 변경하지 않기 때문입니다. 그러나 트랜잭션 영역, 곧 업데이트는 언제나 집계 루트와 리포지토리에 의해 제어되어야 합니다.

기본적으로, 리포지토리는 데이터베이스에서 도메인 엔터티의 형태로 제공되는 메모리에 데이터를 채울 수 있습니다. 엔터티가 메모리에 있으면, 변경되고 트랜잭션을 통해 데이터베이스에서 다시 지속될 수 있습니다.

앞에서 설명한 대로, CQS/CQRS 아키텍처 패턴을 사용하는 경우 초기 쿼리는 Dapper를 사용하는 간단한 SQL 문에 의해 수행된 도메인 모델 외부의 사이드 쿼리에 의해 수행됩니다. 이 방법은 필요한 모든 테이블을 쿼리하고 조인할 수 있으며 또한 이러한 쿼리는 집계 규칙에 의해 제한을 받지 않기 때문에 리포지토리보다 훨씬 더 유연합니다. 해당 데이터는 프레젠테이션 계층 또는 클라이언트 앱으로 이동합니다.

사용자가 변경하는 경우 업데이트될 데이터는 클라이언트 앱 또는 프레젠테이션 계층에서 애플리케이션 계층(예: Web API 서비스)으로 제공됩니다. 명령 처리기에서 명령을 받는 경우 리포지토리를 사용하여 데이터베이스에서 업데이트하고자 하는 데이터를 가져옵니다. 명령으로 전달되는 데이터를 통해 메모리에 이를 업데이트한 다음, 트랜잭션을 통해 데이터베이스에 데이터(도메인 엔터티)를 추가하거나 업데이트합니다.

그림 7-17과 같이 각 집계 루트에 대해 하나의 리포지토리만 정의해야 함을 다시 강조하는 것이 중요합니다. 집계 내 모든 개체 간의 트랜잭션 일관성을 유지하기 위한 집계 루트의 목표를 달성하려면 데이터베이스에 각 테이블에 대한 리포지토리를 결코 만들어서는 안 됩니다.

![도메인과 인프라 계층 간의 관계: 구매자 집계는 IBuyerRepository에 종속되고, 주문 집계는 IOrderRepository 인터페이스에 따라 달라집니다. 이러한 인터페이스는 데이터 계층의 테이블에 액세스하는 UnitOfWork(여기에서도 구현됨)에 의존하는 해당 리포지토리에 의해 인프라 계층에서 구현됩니다.](./media/image18.png)

**그림 7-17**. 리포지토리, 집계, 데이터베이스 테이블 간의 관계

### <a name="enforce-one-aggregate-root-per-repository"></a>리포지토리당 하나의 집계 루트 적용

집계 루트만 리포지토리를 갖는다는 규칙을 적용하는 것과 같은 방법으로 리포지티리 디자인을 구현하는 것은 유용할 수 있습니다. `IAggregateRoot` 마커 인터페이스를 갖도록 함께 작동하는 엔터티 형식을 제한하는 제네릭 또는 기본 리포지토리 형식을 만들 수 있습니다.

따라서 인프라 계층에서 구현되는 각 리포지토리 클래스는 다음 코드에 보이는 것처럼 자체 계약이나 인터페이스를 구현합니다.

```csharp
namespace Microsoft.eShopOnContainers.Services.Ordering.Infrastructure.Repositories
{
    public class OrderRepository : IOrderRepository
    {
      // ...
    }
}
```

각 특정 리포지토리 인터페이스는 제네릭 IRepository 인터페이스를 구현합니다.

```csharp
public interface IOrderRepository : IRepository<Order>
{
    Order Add(Order order);
    // ...
}
```

단, 각 리포지토리가 단일 집계와 관련되어 있는 규칙을 코드에서 적용하도록 하는 더 나은 방법은 제네릭 리포지토리 형식을 구현하는 것입니다. 따라서 리포지토리를 사용하여 특정 집계를 대상으로 지정하는 것이 분명합니다. 다음 코드에서처럼 제네릭 `IRepository` 기본 인터페이스를 구현함으로써 쉽게 설정할 수 있습니다.

```csharp
public interface IRepository<T> where T : IAggregateRoot
{
    //....
}
```

### <a name="the-repository-pattern-makes-it-easier-to-test-your-application-logic"></a>리포지토리 패턴은 애플리케이션 논리를 보다 쉽게 테스트하게 합니다

리포지토리 패턴은 단위 테스트를 사용해 애플리케이션을 쉽게 테스트할 수 있습니다. 단위 테스트만 인프라가 아닌 해당 코드를 테스트함으로써 리포지토리 추상적 개념이 목표를 더 쉽게 달성하게 합니다.

이전 단원에서 설명했듯이, 애플리케이션 계층(예를 들어, Web API 마이크로 서비스)이 실제 리포지토리 클래스를 구현한 인프라 계층에 직접 종속되지 않도록 도메인 모델 계층에서 리포지토리 인터페이스를 정의하고 배치하는 것이 좋습니다. 이렇게 하는 동시에 Web API의 컨트롤러에서 종속성 주입을 사용함으로써 데이터베이스에서 데이터 대신 가짜 데이터를 반환하는 모의 리포지토리를 구현할 수 있습니다. 이 분리 방식을 사용하면 데이터베이스에 연결하지 않고도 애플리케이션의 논리에 중점을 둔 단위 데스트를 생성하고 실행할 수 있습니다.

데이터베이스에 대 한 연결이 실패할 수 하며, 무엇 보다도 데이터베이스에 대해 수백 번의 테스트를 실행 합니다. 잘못 된 두 가지 이유로 합니다. 첫째, 방대한 양의 테스트 때문에 많은 시간이 걸릴 수 있습니다. 둘째, 데이터베이스 레코드는 테스트 결과를 변경하고 영향을 줄 수 있으므로 결과가 일관되지 않을 수 있습니다. 데이터베이스의 테스트는 단위 테스트가 아닌 통합 테스트입니다. 많은 단위 테스트를 신속하게 실행해야 하지만 데이터베이스에 대해 통합 테스트는 거의 실행되지 않습니다.

단위 테스트에 대한 관심의 분리란 관점에서 해당 논리는 메모리의 도메인 엔터티에서 작동합니다. 리포지토리 클래스가 단위 테스트를 전달한 것으로 가정합니다. 일단 해당 논리가 도메인 엔터티를 수정하면 리포지토리 클래스가 이를 올바르게 저장할 것으로 가정합니다. 여기서 중요한 것은 해당 도메인 모델 및 도메인 논리에 대해 단위 테스트를 만드는 것입니다. 집계 루트는 DDD에서의 주된 일관성 경계입니다.

eShopOnContainers에 구현된 리포지토리는 해당 변경 추적기를 사용하여 리포지토리 및 작업 단위 패턴의 EF Core DbContext 구현에 의존하므로 이 기능을 복제하지 않습니다.

### <a name="the-difference-between-the-repository-pattern-and-the-legacy-data-access-class-dal-class-pattern"></a>리포지토리 패턴 및 레거시 데이터 액세스 클래스(DAL 클래스) 패턴의 차이

데이터 액세스 개체는 스토리지에 대한 데이터 액세스 및 지속성 작업을 직접 수행합니다. 리포지토리는 작업 개체 단위(<xref:Microsoft.EntityFrameworkCore.DbContext> 클래스를 사용하는 경우 EF에서처럼)의 메모리에서 수행하고자 하는 작업을 통해 데이터를 표시하지만 이러한 업데이트는 데이터베이스에 대해 즉시 수행되지 않습니다.

작업 단위는 다중 삽입, 업데이트, 삭제 작업과 관련된 단일 트랜잭션이라고도 합니다. 간단히 말해서, 특정 사용자 작업(예: 웹사이트 등록)의 경우 모든 삽입, 업데이트 및 삭제 작업은 단일 트랜잭션으로 처리된다는 의미입니다. 단일 트랜잭션 처리는 복잡한 방식으로 다중 데이터베이스 트랜잭션을 처리하는 것보다 더 효율적입니다.

이러한 다중 지속성 작업은 애플리케이션 계층에서 해당 코드가 명령을 내리는 경우 나중에 단일 작업으로 수행됩니다. 실제 데이터베이스 스토리지에 메모리 내 변경을 적용은 일반적으로 [작업 단위 패턴](https://martinfowler.com/eaaCatalog/unitOfWork.html)에 기반을 두고 결정됩니다. EF에서, 작업 단위 패턴은 <xref:Microsoft.EntityFrameworkCore.DbContext>로서 구현됩니다.

대부분의 경우, 스토리지에 작업을 적용하는 방식이나 패턴은 애플리케이션 성능을 향상시키고 불일치 가능성을 줄일 수 있습니다. 또한, 의도된 모든 작업은 한 트랜잭션의 일부로서 커밋되기 때문에 데이터베이스 테이블에서 트랜잭션 차단을 줄여줍니다. 이 방법은 데이터베이스에 대해 많은 격리된 작업 실행에 비해 더 효율적입니다. 따라서 선택한 ORM은 많은 소형 및 별도 트랜잭션 실행과 대조적으로 동일한 트랜잭션 내에서 여러 가지 업데이트 작업을 그룹화하여 데이터베이스에서의 실행을 최적화할 수 있습니다.

### <a name="repositories-shouldnt-be-mandatory"></a>리포지토리는 필수가 아닙니다

사용자 지정 리포지토리는 앞에서 언급한 이유 때문에 유용하며 eShopOnContainers에서 주문형 마이크로 서비스용 접근방식입니다. 그러나 DDD 디자인이나 일반 .NET 개발에서 구현을 위한 필수 패턴은 아닙니다.

예를 들어, Jimmy Bogard는 이 가이드를 위한 피드백을 직접 제공하면서 다음과 같이 말했습니다.

> 이것이 아마도 나의 가장 큰 피드백일 것입니다. 주로 리포지토리가 기본 지속성 메커니즘의 중요한 세부 정보를 숨기기 때문에 실제로 리포지토리를 좋아하지는 않습니다. 때문에 나는 명령용 MediatR도 사용합니다. 지속성 계층의 모든 기능을 사용할 수 있으며 모든 도메인 동작을 집계 루트로 밀어 넣을 수도 있습니다. 보통 내 리포지토리를 흉내내고 싶지는 않습니다 – 여전히 실제 사물을 통한 통합 테스트가 필요합니다. CQRS로의 전환은 실제로 리포지토리가 더 이상 필요하지 않다는 것을 의미합니다.

리포지토리는 유용할 수 있지만, 집계 패턴과 풍성한 도메인 모델만큼 DDD 디자인에는 중요하지 않습니다. 따라서 필요에 따라 리포지토리 패턴을 사용하거나 사용하지 마십시오. 어쨌든, EF Core를 사용할 때마다 리포지토리 패턴을 사용할 수 있지만 이 경우에는 리포지토리가 전체 마이크로 서비스 또는 바인딩된 컨텍스트를 다룹니다.

## <a name="additional-resources"></a>추가 자료

### <a name="repository-pattern"></a>리포지토리 패턴

- **리포지토리 패턴** \
  <https://deviq.com/repository-pattern/>

- **Edward Hieatt와 Rob Mee. 리포지토리 패턴.** \
  <https://martinfowler.com/eaaCatalog/repository.html>

- **리포지토리 패턴** \
  <https://docs.microsoft.com/previous-versions/msp-n-p/ff649690(v=pandp.10)>

- **Eric Evans. 도메인 기반 디자인: 소프트웨어 핵심에서 복잡성을 처리합니다.** (서적, 리포지토리 패턴 논의 포함)\
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

### <a name="unit-of-work-pattern"></a>작업 단위 패턴

- **Martin Fowler. 작업 단위 패턴.** \
  <https://martinfowler.com/eaaCatalog/unitOfWork.html>

- **ASP.NET MVC 애플리케이션에서 작업 패턴의 리포지토리 및 단위 구현** \
  <https://docs.microsoft.com/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application>

>[!div class="step-by-step"]
>[이전](domain-events-design-implementation.md)
>[다음](infrastructure-persistence-layer-implemenation-entity-framework-core.md)
