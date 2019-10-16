---
title: 마이크로 서비스 도메인 모델 디자인
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | DDD 지향 도메인 모델을 디자인할 때 주요 개념을 이해합니다.
ms.date: 10/08/2018
ms.openlocfilehash: c6d2e84189ff542a2ed4c584c4a47bf7bf0e946a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68676450"
---
# <a name="design-a-microservice-domain-model"></a>마이크로 서비스 도메인 모델 디자인

*각 비즈니스 마이크로 서비스 또는 바인딩된 컨텍스트에 대해 하나의 풍부한 도메인 모델을 정의합니다.*

여기서의 목표는 각 비즈니스 마이크로 서비스 또는 바인딩된 컨텍스트(BC)에 대한 단일 결합 도메인 모델을 만드는 것입니다. 하지만 BC 또는 비즈니스 마이크로 서비스가 때로는 단일 도메인 모델을 공유하는 여러 물리적 서비스로 구성될 수도 있다는 것을 주의하세요. 도메인 모델은 단일 바인딩된 컨텍스트(BC) 또는 BC가 대표하는 비즈니스 마이크로 서비스의 제약 조건, 규칙, 동작, 비즈니스 언어를 캡처해야 합니다.

## <a name="the-domain-entity-pattern"></a>도메인 엔터티 패턴

엔터티는 도메인 개체를 대표하며, 주로 ID, 연속성, 시간의 흐름에 따른 지속성 및 이들을 포괄하는 특성에 의해 정의됩니다. Eric Evans의 말처럼 "기본적으로 해당 ID로 정의되는 개체를 엔터티라고 합니다." 엔터티는 모델의 기본이기 때문에 도메인 모델에서 아주 중요합니다. 따라서 엔터티를 신중하게 식별하고 디자인해야 합니다.

*엔터티 ID는 다중 마이크로 서비스나 바인딩된 컨텍스트를 교차할 수 있습니다.*

동일한 ID(즉, 동일한 도메인 엔터티는 아닐 수 있지만 동일한 `Id` 값)는 여러 바인딩된 컨텍스트 또는 마이크로 서비스 전체에 걸쳐 모델링될 수 있습니다. 그러나 동일한 특성 및 논리를 가진 동일한 엔터티가 다중 바인딩된 컨텍스트에서 구현된다는 의미는 아닙니다. 대신, 각 바운딩된 컨텍스트의 엔터티는 그 속성과 행동을 해당 바운딩된 컨텍스트의 도메인에서 요구하는 속성과 행동에 맞게 제한합니다.

예를 들어, 구매자 엔터티는 ID를 포함해 프로필이나 ID 마이크로 서비스의 사용자 엔터티에서 정의되는 사람의 특성 대부분을 가질 수 있습니다. 그러나 주문형 마이크로 서비스에서 구매자 엔터티는 특성을 거의 가질 수 없는데 특정 구매자 데이터만 주문 프로세스에 관련돼 있기 때문입니다. 각 마이크로 서비스의 컨텍스트 또는 바인딩된 컨텍스트는 해당 도메인 모델에 영향을 줍니다.

*도메인 엔터티는 데이터 특성을 구현하는 것 외에도 동작을 구현해야 합니다.*

DDD에서 도메인 엔터티는 엔터티 데이터(메모리에 액세스된 개체)와 관련된 도메인 논리나 행동을 구현해야 합니다. 예를 들어, 주문 엔터티 클래스의 일부로서 주문 항목, 데이터 유효성 검사, 총계를 추가하는 것 같은 작업 메서드로서 구현된 비즈니스 작업 및 논리가 포함돼야 합니다. 해당 엔터티의 메서드는 애플리케이션 계층에 엔터티 규칙을 분산하는 대신 엔터티의 규칙 및 고정화에 신경을 써야 합니다.

그림 7-8은 데이터 특성뿐만 아니라 관련 도메인 논리를 통해 작업 또는 메서드까지 구현하는 도메인 엔터티를 보여줍니다.

![도메인 모델 엔터티는 메서드를 통해 동작을 구현합니다. 즉, 이는 "빈약한" 모델이 아닙니다.](./media/image9.png)

**그림 7-8**. 데이터와 동작을 구현하는 도메인 엔터티 디자인의 예

물론, 경우에 따라 엔터티 클래스의 일부로 모든 논리를 구현하지는 않는 엔터티를 포함할 수 있습니다. 이런 경우는 대부분의 논리가 집계 루트에서 정의되기 때문에 자식 엔터티가 특별한 논리를 갖지 않은 경우 집계하지 않는 자식 엔터티에서 발생할 수 있습니다. 도메인 엔터티 대신 서비스 클래스에서 구현된 많은 로직을 갖는 복잡한 마이크로 서비스가 포함된 경우 다음 섹션에서 설명될 빈약한 도메인 모델이 될 수 있습니다.

### <a name="rich-domain-model-versus-anemic-domain-model"></a>풍성한(rich) 도메인 모델 대 빈약한(anemic) 도메인 모델

[AnemicDomainModel](https://martinfowler.com/bliki/AnemicDomainModel.html)이라는 게시물에서, Martin Fowler는 빈약한 도메인 모델을 이렇게 설명합니다.

빈약한 도메인 모델의 기본 증상은 언뜻 보기에 실제처럼 보인다는 것입니다. 개체는 대부분 도메인 공간의 명사를 따라 이름 짓습니다. 이런 개체는 진정한 도메인 모델이 갖는 풍성한 관계 및 구조와 연결돼 있습니다. 동작을 보면 Catch가 실현되는데, getter 및 setter의 모음보다 조금 더 많이 움직일 뿐 이러한 개체에서는 거의 아무런 동작이 없습니다.

물론, 빈약한 도메인 모델을 사용하는 경우 이러한 데이터 모델은 모든 도메인 또는 비즈니스 논리를 캡처하는 서비스 개체 집합(보통 *비즈니스 계층*으로 명명)에서 사용되게 됩니다. 비즈니스 계층은 데이터 모델 위에 배치되고 데이터와 마찬가지로 데이터 모델을 사용합니다.

빈약한 도메인 모델은 절차적 스타일 디자인일 뿐입니다. 빈약한 엔터티 개체는 동작(메서드)이 부족하기 때문에 실제 개체가 아닙니다. 이 개체는 데이터 속성을 보유하므로 개체 지향 디자인이 아닙니다. 모든 동작을 서비스 개체(비즈니스 계층)에 입력함으로써 기본적으로 [스파케티 코드](https://en.wikipedia.org/wiki/Spaghetti_code) 또는 [트랜잭션 스크립트](https://martinfowler.com/eaaCatalog/transactionScript.html)로 종료하기에 도메인 모델이 제공하는 이점을 상실합니다.

마이크로 서비스 또는 바인딩된 컨텍스트가 매우 간단한지에 상관 없이(CRUD 서비스) 데이터 속성을 지닌 엔터티 개체의 형태로 된 빈약한 도메인 모델로도 충분할 수 있으며 더 복잡한 DDD 패턴을 구현할 만한 가치가 없을 수 있습니다. 이 경우, 의도적으로 데이터만 지닌 엔터티를 CRUD 목적으로 만들었기 때문에 단순히 지속성 모델이 되게 됩니다.

그렇기에 마이크로 서비스 아키텍처는 각 바운딩된 컨텍스트에 따라 다중 아키텍처 방법에 완벽합니다. 예를 들어, eShopOnContainers에서 주문형 마이크로 서비스는 DDD 패턴을 구현하지만 단순한 CRUD 서비스인 카탈로그 마이크로 서비스는 그러지 않습니다.

몇몇 사람은 빈약한 도메인 모델을 안티패턴이라고도 합니다. 이 모델은 실제로 구현하는 내용에 따라 달라집니다. 만들려는 마이크로 서비스가 충분히 단순하다면(예를 들어, CRUD 서비스) 빈약한 도메인 모델을 따르는 것은 안티패턴이 아닙니다. 그러나 끊임없이 변화하는 비즈니스 규칙이 많은 마이크로 서비스 도메인의 복잡성을 해결해야 하는 경우 빈약한 도메인 모델은 해당 마이크로 서비스 또는 바운딩된 컨텍스트에게는 안티패턴일 수 있습니다. 이 경우, 빈약한 모델을 데이터와 동작을 포함할 뿐 아니라 추가적인 DDD 패턴(집계, 가치 개체 등)을 구현하는 엔터티를 지닌 풍성한 모델로 디자인하는 것은 이러한 마이크로 서비스의 장기적인 성공으로 인한 큰 혜택이 있을 수 있습니다.

#### <a name="additional-resources"></a>추가 자료

- **DevIQ. 도메인 엔터티** \
  <https://deviq.com/entity/>

- **Martin Fowler. 도메인 모델** \
  <https://martinfowler.com/eaaCatalog/domainModel.html>

- **Martin Fowler. 빈약한 도메인 모델** \
  <https://martinfowler.com/bliki/AnemicDomainModel.html>

### <a name="the-value-object-pattern"></a>가치 개체 패턴

Eric Evans의 지적처럼 "많은 개체는 개념적 ID를 갖고 있지 않습니다. 이런 개체는 사물의 일정한 특성을 설명합니다."

엔터티는 ID를 요구하지만 가치 개체 패턴처럼 시스템의 많은 개체는 이를 요구하지 않습니다. 가치 개체는 도메인 양상을 설명하는 개념적 ID가 없는 개체입니다. 이 개체는 일시적으로 사용자를 배려하는 디자인 요소를 나타내기 위해 인스턴스화합니다. 중요한 것은 이 개체가 *누구*가 아닌 *무엇*이냐는 것입니다. 예제는 숫자와 문자열을 포함하지만 특성 그룹 같이 고수준의 개념일 수도 있습니다.

마이크로 서비스의 엔터티인 어떤 것이 또 다른 마이크로 서비스의 엔터티가 될 수는 없습니다. 두 번째 경우에 바운딩된 컨텍스트가 다른 의미를 가질 수 있기 때문입니다. 예를 들어, 전자 상거래 애플리케이션의 주소는 개인 또는 회사에 대해 고객 프로필의 특성 그룹을 나타낼 수 있기에 ID를 전혀 가질 수 없습니다. 이 경우, 해당 주소는 가치 개체로 분류돼야 합니다. 그러나 전원 유틸리티 회사의 애플리케이션에서 고객 주소는 비즈니스 도메인에 대해 중요할 수 있습니다. 따라서 해당 주소는 청구 시스템이 직접 해당 주소에 연결될 수 있도록 반드시 ID를 가져야 합니다. 이 경우, 주소는 도메인 엔터티로 분류돼야 합니다.

성과 이름이 있는 사람은 이런 이름이 다른 사람을 지칭하는 경우처럼 비록 성과 이름이 또 다른 가치 집합과 일치한다 해도 사람은 ID를 갖기 때문에 대개 엔터티입니다.

가치 개체는 EF 같은 ORM과 관계형 데이터베이스에서는 관리하기가 어렵습니다. 반면에 문서 지향 데이터베이스에서는 구현과 사용이 훨신 쉽습니다.

EF Core 2.0에는 값 개체를 더 쉽게 처리할 수 있는 [소유한 엔터티](https://devblogs.microsoft.com/dotnet/announcing-entity-framework-core-2-0/#owned-entities-and-table-splitting) 기능이 포함되어 있습니다. 자세한 내용은 나중에 살펴보겠습니다.

#### <a name="additional-resources"></a>추가 자료

- **Martin Fowler. 값 개체 패턴** \
  <https://martinfowler.com/bliki/ValueObject.html>

- **값 개체** \
  <https://deviq.com/value-object/>

- **테스트 기반 개발의 값 개체** \
  [https://leanpub.com/tdd-ebook/read\#leanpub-auto-value-objects](https://leanpub.com/tdd-ebook/read#leanpub-auto-value-objects)

- **Eric Evans. 도메인 기반 디자인: 소프트웨어 핵심에서 복잡성을 처리합니다.** (도서; 값 개체의 토론 포함) \
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

### <a name="the-aggregate-pattern"></a>집계 모듈

도메인 모델은 주문 완료나 재고 등의 중요한 기능 영역을 제어할 수 있는 다른 데이터 엔터티 및 프로세스의 클러스터를 포함합니다. 더욱 정교한 DDD 단위는 응집력 있는 단위로 취급될 수 있는 동작 및 엔터티의 그룹이나 클러스터를 설명하는 집계입니다.

일반적으로 필요한 트랜잭션을 기반으로 집계를 정의 합니다. 전형적인 예는 주문 항목 목록을 포함하는 주문입니다. 주문 항목은 대개 엔터티가 되지만, 일반적으로 집계 루트라고 하는 해당 루트 엔터티로서 주문 엔터티를 포함하는 주문 집계 내에서 자식 엔터티가 됩니다.

집계를 식별하기는 어려울 수 있습니다. 집계는 서로 일치 해야 하는 개체 그룹이지만 개체 그룹을 막 선택하고 이를 집계라고 레이블을 붙일 수 없습니다. 도메인 개념부터 시작해서 해당 개념과 관련된 가장 일반적인 트랜잭션에서 사용되는 엔터티를 고려해야 합니다. 트랜잭션 관점에서 일관성이 있는 이런 엔터티가 집계를 형성하는 것입니다. 트랜잭션 작업에 대한 생각이 아마도 집계를 식별하는 가장 좋은 방법입니다.

### <a name="the-aggregate-root-or-root-entity-pattern"></a>집계 루트 또는 루트 엔터티 패턴

집계는 최소 하나 이상의 엔터티로 구성돼 있습니다. 루트 엔터티 또는 기본 엔터티라고도 하는 집계 루트입니다. 또한 집계는 모든 엔터티 및 개체가 필요한 동작 및 트랜잭션을 구현하기 위해 함께 작업하는 가운데 여러 자식 엔터티와 가치 개체를 가질 수 있습니다.

집계 루트의 목적은 집계의 일관성을 확보하는 데 있으며, 집계 루트 클래스에서 메서드나 작업을 통해 집계를 업데이트하기 위한 유일한 진입점이 되어야 합니다. 집계 루트를 통해서만 집계 내에서 엔터티를 변경해야 합니다. 집계의 일관성 보호자는 집계를 위해 준수해야 할 모든 고정불변 및 일관성 규칙을 고려해야 합니다. 독립적으로 자식 엔터티나 가치 개체를 변경하는 경우 집계 루트는 집계가 유효한 상태인지를 보장할 수 없습니다. 이는 마치 느슨한 다리를 가진 테이블과 같습니다. 일관성을 유지하는 것은 집계 루트의 주요 목적입니다.

그림 7-9에서, 단일 엔터티(집계 루트 구매자)를 포함하는 구매자 집계 같은 샘플 집계를 확인할 수 있습니다. 해당 구매 집계는 여러 엔터티 및 가치 개체를 포함합니다.

![DDD 도메인 모델은 집계로 구성되며, 집계는 하나 이상의 엔터티만 가질 수 있으며 값 개체도 포함할 수 있습니다.](./media/image10.png)

**그림 7-9**. 다중 또는 단일 엔터티 집계의 예

구매자 집계는 eShopOnContainers 참조 애플리케이션의 주문 마이크로 서비스에서 그러는 것처럼 해당 도메인에 따라 추가적인 자식 엔터티를 가질 수 있음에 유의하십시오. 그림 7-9는 구매자가 집계 루트만 포함된 집계의 예로서 단일 엔터티를 갖고 있음을 보여줍니다.

집계 분리를 유지하고 집계 간에 명확한 경계를 유지하기 위해서는 eShopOnContainers에서 [마이크로 서비스 도메인 모델 주문하기](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.Domain/AggregatesModel/OrderAggregate/Order.cs)에서 구현된 것처럼 외래 키(FK) 필드만 갖고 집계 간 직접 탐색을 허용하지 않는 것이 DDD 도메인 모델의 좋은 관행입니다. 주문 엔터티는 다음 코드에서 보여지는 것처럼 EF Core 탐색 속성이 아닌 구매자를 위한 FK 필드만 갖습니다.

```csharp
public class Order : Entity, IAggregateRoot
{
    private DateTime _orderDate;
    public Address Address { get; private set; }
    private int? _buyerId; //FK pointing to a different aggregate root
    public OrderStatus OrderStatus { get; private set; }
    private readonly List<OrderItem> _orderItems;
    public IReadOnlyCollection<OrderItem> OrderItems => _orderItems;
    // ... Additional code
}
```

집계를 통한 식별과 작업에는 연구와 경험이 필요합니다. 자세한 내용은 다음의 추가 리소스 목록을 참조하십시오.

#### <a name="additional-resources"></a>추가 자료

- **Vaughn Vernon. 효율적인 집계 디자인 - 1부: 단일 집계 모델링**(<http://dddcommunity.org/>에서) \
  <http://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_1.pdf>

- **Vaughn Vernon. 효율적인 집계 디자인 - 2부: 집계가 함께 작동하도록 만들기**(<http://dddcommunity.org/>에서) \
  <http://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf>

- **Vaughn Vernon. 효율적인 집계 디자인 - 3부: 검색을 통해 Insight 얻기**(<http://dddcommunity.org/>에서) \
  <http://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_3.pdf>

- **Sergey Grybniak. DDD 전술적 디자인 패턴** \
  <https://www.codeproject.com/Articles/1164363/Domain-Driven-Design-Tactical-Design-Patterns-Part>

- **Chris Richardson. 집계를 사용한 트랜잭션 마이크로 서비스 개발** \
  <https://www.infoq.com/articles/microservices-aggregates-events-cqrs-part-1-richardson>

- **DevIQ. 집계 패턴** \
  <https://deviq.com/aggregate-pattern/>

>[!div class="step-by-step"]
>[이전](ddd-oriented-microservice.md)
>[다음](net-core-microservice-domain-model.md)
