---
title: 값 개체 구현
description: 컨테이너화된 .NET 애플리케이션의 .NET 마이크로 서비스 아키텍처 | 새로운 Entity Framework 기능을 사용하여 값 개체를 구현하는 세부 정보 및 옵션을 가져옵니다.
ms.date: 10/08/2018
ms.openlocfilehash: b2f7b0f36fea25c25edd47731d9387810bd2b44d
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674150"
---
# <a name="implement-value-objects"></a>값 개체 구현

엔터티 및 집계에 대한 이전 섹션에서 설명한 대로, ID는 엔터티의 근본입니다. 그러나 시스템에는 값 개체처럼 ID 및 ID 추적이 필요 없는 여러 개체와 데이터 항목이 있습니다.

값 개체는 다른 엔터티를 참조할 수 있습니다. 예를 들어 한 지점에서 다른 지점으로 이동하는 경로를 생성하는 애플리케이션에서는 해당 경로가 값 개체입니다. 특정 경로에 있는 지점의 스냅샷이 되겠지만, 이 제안 경로는 내부적으로 도시, 로드 등의 엔터티를 참조하더라도 ID를 갖지 않습니다.

그림 7-13은 순서 집계 내의 주소 값 개체를 보여줍니다.

![순서 집계 내의 주소 값 개체](./media/image14.png)

**그림 7-13** 순서 집계 내부의 주소 값 개체

그림 7-13에 표시된 것처럼, 엔터티는 일반적으로 여러 특성으로 구성됩니다. 예를 들어 `Order` 엔터티는 ID가 있는 엔터티로 모델링하고 내부적으로 OrderId, OrderDate, OrderItems 등의 특성 집합으로 구성할 수 있습니다. 하지만 국가/지역, 거리, 도시 등으로 구성되고 이 도메인의 ID를 갖지 않는 복잡한 값인 주소는 값 개체로 모델링되고 처리되어야 합니다.

## <a name="important-characteristics-of-value-objects"></a>값 개체의 중요한 특징

값 개체의 두 가지 주요 특징이 있습니다.

- ID가 없습니다.

- 변경할 수 없습니다.

첫 번째 특징은 이미 설명했습니다. 변경 불가능은 중요한 요구 사항입니다. 일단 개체가 생성된 후에는 값 개체의 값을 변경할 수 없어야 합니다. 따라서 개체가 생성될 때 필요한 값을 제공해야 하지만, 개체의 수명 주기 동안 값이 변경되는 것을 허용하면 안 됩니다.

값 개체의 변경 불가능이라는 성질 덕분에 값 개체를 사용하여 성능을 높일 수 있는 방법이 있습니다. 특히 수천 개의 값 개체 인스턴스가 있고 그 중 많은 수가 같은 값을 갖는 시스템에서 더욱 그렇습니다. 변경 불가능이라는 성질 덕분에 재사용이 가능합니다. 값이 같고 ID가 없기 때문에 교환이 가능합니다. 이와 같은 유형의 최적화는 때때로 느리게 실행되는 소프트웨어와 고성능 소프트웨어 간의 차이를 만들 수 있습니다. 물론, 이 모든 것은 애플리케이션 환경과 배포 상황에 따라 달라집니다.

## <a name="value-object-implementation-in-c"></a>C에서 값 개체 구현\#

구현의 측면에서, 모든 특성(값 개체는 ID를 기반으로 할 수 없으므로)과 기타 기본 특성 간의 동등함처럼 기본 유틸리티 메서드가 있는 개체 기본 클래스를 사용할 수 있습니다. 다음 예제에서는 eShopOnContainers의 주문 마이크로 서비스에 사용되는 값 개체 기본 클래스를 보여줍니다.

```csharp
public abstract class ValueObject
{
    protected static bool EqualOperator(ValueObject left, ValueObject right)
    {
        if (ReferenceEquals(left, null) ^ ReferenceEquals(right, null))
        {
            return false;
        }
        return ReferenceEquals(left, null) || left.Equals(right);
    }

    protected static bool NotEqualOperator(ValueObject left, ValueObject right)
    {
        return !(EqualOperator(left, right));
    }

    protected abstract IEnumerable<object> GetAtomicValues();

    public override bool Equals(object obj)
    {
        if (obj == null || obj.GetType() != GetType())
        {
            return false;
        }

        ValueObject other = (ValueObject)obj;
        IEnumerator<object> thisValues = GetAtomicValues().GetEnumerator();
        IEnumerator<object> otherValues = other.GetAtomicValues().GetEnumerator();
        while (thisValues.MoveNext() && otherValues.MoveNext())
        {
            if (ReferenceEquals(thisValues.Current, null) ^
                ReferenceEquals(otherValues.Current, null))
            {
                return false;
            }

            if (thisValues.Current != null &&
                !thisValues.Current.Equals(otherValues.Current))
            {
                return false;
            }
        }
        return !thisValues.MoveNext() && !otherValues.MoveNext();
    }

    public override int GetHashCode()
    {
        return GetAtomicValues()
         .Select(x => x != null ? x.GetHashCode() : 0)
         .Aggregate((x, y) => x ^ y);
    }
    // Other utility methods
}
```

다음 예제의 주소 값 개체와 마찬가지로, 실제 값 개체를 구현할 때 이 클래스를 사용할 수 있습니다.

```csharp
public class Address : ValueObject
{
    public String Street { get; private set; }
    public String City { get; private set; }
    public String State { get; private set; }
    public String Country { get; private set; }
    public String ZipCode { get; private set; }

    private Address() { }

    public Address(string street, string city, string state, string country, string zipcode)
    {
        Street = street;
        City = city;
        State = state;
        Country = country;
        ZipCode = zipcode;
    }

    protected override IEnumerable<object> GetAtomicValues()
    {
        // Using a yield return statement to return each element one at a time
        yield return Street;
        yield return City;
        yield return State;
        yield return Country;
        yield return ZipCode;
    }
}
```

주소의 이 값 개체 구현에 ID가 없으며 따라서 Address 클래스 및 ValueObject 클래스에도 ID 필드가 없도록 하는 방법을 확인할 수 있습니다.

ID가 없는 값 개체를 구현하는 데 크게 데 도움이 되는 EF Core 2.0까지는 클래스에 Entity Framework에서 사용할 ID 필드가 있습니다. 정확한 다음 섹션의 설명입니다.

변경할 수 없는 개체 값이 읽기 전용(예: 가져오기 전용 속성)이라고 주장할 수 있고 실제로 그렇습니다. 그러나 값 개체는 일반적으로 직렬화되고 deserialize되어 메시지 큐를 거치고, 읽기 전용이므로 역직렬 변환기가 값을 할당하지 않도록 중지합니다. 따라서 값 개체를 읽기 전용이 충분히 실용적인 비공개 세트로 둡니다.

## <a name="how-to-persist-value-objects-in-the-database-with-ef-core-20"></a>EF Core 2.0을 사용하여 데이터베이스에서 개체 값을 유지하는 방법

도메인 모델에서 값 개체를 정의하는 방법을 알아보았습니다. 하지만 일반적으로 ID가 있는 엔터티를 대상으로 하는 EF(Entity Framework) Core를 통해 개체 값을 데이터베이스에 유지하려면 어떻게 해야 할까요?

### <a name="background-and-older-approaches-using-ef-core-11"></a>배경 지식 및 EF Core 1.1을 사용한 기존의 접근 방식

배경지식으로 알려드리자면, EF Core 1.0 및 1.1을 사용하는 경우 기존 .NET Framework의 EF 6.x에서 정의된 것처럼 [복합 형식](xref:System.ComponentModel.DataAnnotations.Schema.ComplexTypeAttribute)을 사용할 수 없다는 제한이 있습니다. 따라서 EF Core 1.0 또는 1.1을 사용하는 경우 값 개체를 ID 필드가 있는 EF 엔터티로 저장해야 했습니다. 그래서 마치 ID가 없는 값 개체처럼 보이기 때문에 ID를 숨겨서 값 개체의 ID가 도메인 모델에서 중요하지 않다는 점을 분명히 할 수 있습니다. ID를 [섀도 속성](https://docs.microsoft.com/ef/core/modeling/shadow-properties )으로 사용하여 해당 ID를 숨길 수 있습니다. 모델에서 ID를 숨기는 구성이 EF 인프라 수준에서 설정되므로 도메인 모델에 대해 투명하다고 할 수 있습니다.

eShopOnContainers 초기 버전(.NET Core 1.1)에서, EF Core 인프라에 필요한 숨겨진 ID는 DbContext 수준에서 인프라 프로젝트에 흐름 API를 사용하여 다음과 같은 방식으로 구현되었습니다. 따라서 ID가 보기의 도메인 모델 관점에서 숨겨지더라도 인프라에 계속 존재합니다.

```csharp
// Old approach with EF Core 1.1
// Fluent API within the OrderingContext:DbContext in the Infrastructure project
void ConfigureAddress(EntityTypeBuilder<Address> addressConfiguration)
{
    addressConfiguration.ToTable("address", DEFAULT_SCHEMA);

    addressConfiguration.Property<int>("Id")  // Id is a shadow property
        .IsRequired();
    addressConfiguration.HasKey("Id");   // Id is a shadow property
}
```

그러나 값 개체가 데이터베이스에 유지되는 것은 다른 테이블의 일반 엔터티처럼 수행되었습니다.

EF Core 2.0에서는 값 개체를 유지하는 보다 나은 방법이 도입되었습니다.

## <a name="persist-value-objects-as-owned-entity-types-in-ef-core-20"></a>EF Core 2.0에서 소유된 엔터티 형식으로 값 개체 유지

DDD의 정식 값 개체 패턴과 EF Core의 소유된 엔터티 형식 사이에 차이가 있더라도 현재는 EF Core 2.0을 사용하여 값 개체를 유지하는 것이 가장 좋은 방법입니다. 제한 사항은 이 섹션의 마지막 부분에서 확인할 수 있습니다.

소유된 엔터티 형식 기능은 EF Core 버전 2.0부터 추가되었습니다.

소유된 엔터티 형식을 사용하면 엔터티 내의 값 개체처럼 도메인 모델에 명시적으로 정의된 고유 ID가 없고 속성으로 사용되는 형식을 매핑할 수 있습니다. 소유된 엔터티 형식은 다른 엔터티 형식과 동일한 CLR 형식을 공유합니다(즉, 일반 클래스임). 정의 탐색을 포함하는 엔터티는 소유자 엔터티입니다. 소유자를 쿼리할 때 소유된 형식은 기본적으로 포함됩니다.

도메인 모델을 그냥 보면 소유된 형식에는 ID가 없는 것처럼 보입니다. 하지만 내부로 들어가면 소유된 형식에 ID가 있고 소유자 탐색 속성은 이 ID의 일부입니다.

고유 형식의 인스턴스 ID가 오직 그 자체로만 구성되는 것은 아닙니다. 다음과 같은 세 가지 구성 요소로 구성됩니다.

- 소유자 ID

- 소유자 ID를 가리키는 탐색 속성

- 소유된 형식의 컬렉션인 경우 독립 구성 요소(아직 EF Core 2.0에서 지원되지 않으며 2.2에서 제공될 예정임).

예를 들어 eShopOnContainers의 주문 도메인 모델에서, 주문 엔터티의 일부로 주소 값 개체가 소유자 엔터티 내부의 소유된 엔터티 형식으로 구현되며, 이것이 주문 엔터티입니다. 주소는 도메인 모델에 정의된 ID 속성이 없는 형식입니다. 특정 주문의 배송 주소를 지정하기 위한 Order 형식 속성으로 사용됩니다.

규칙에 따라, 소유된 형식에 대해 섀도 기본 키가 만들어지며 테이블 분할을 사용하여 소유자와 동일한 테이블에 매핑됩니다. 따라서 기존 .NET Framework의 EF6에서 복합 형식이 사용되는 방식과 유사하게 소유된 형식을 사용할 수 있습니다.

소유된 형식은 규칙에 따라 EF Core에서 절대로 검색되지 않으므로 명시적으로 선언해야 한다는 점을 기억해야 합니다.

EShopOnContainers에서, OrderingContext.cs의 OnModelCreating() 메서드 내부에는 여러 인프라 구성이 적용됩니다. 그 중 하나는 주문 엔터티와 관련이 있습니다.

```csharp
// Part of the OrderingContext.cs class at the Ordering.Infrastructure project
//
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.ApplyConfiguration(new ClientRequestEntityTypeConfiguration());
    modelBuilder.ApplyConfiguration(new PaymentMethodEntityTypeConfiguration());
    modelBuilder.ApplyConfiguration(new OrderEntityTypeConfiguration());
    modelBuilder.ApplyConfiguration(new OrderItemEntityTypeConfiguration());
    //...Additional type configurations
}
```

다음 코드에서는 주문 엔터티에 대해 지속성 인프라가 정의됩니다.

```csharp
// Part of the OrderEntityTypeConfiguration.cs class
//
public void Configure(EntityTypeBuilder<Order> orderConfiguration)
{
    orderConfiguration.ToTable("orders", OrderingContext.DEFAULT_SCHEMA);
    orderConfiguration.HasKey(o => o.Id);
    orderConfiguration.Ignore(b => b.DomainEvents);
    orderConfiguration.Property(o => o.Id)
        .ForSqlServerUseSequenceHiLo("orderseq", OrderingContext.DEFAULT_SCHEMA);

    //Address value object persisted as owned entity in EF Core 2.0
    orderConfiguration.OwnsOne(o => o.Address);

    orderConfiguration.Property<DateTime>("OrderDate").IsRequired();

    //...Additional validations, constraints and code...
    //...
}
```

이전 코드에서 `orderConfiguration.OwnsOne(o => o.Address)` 메서드는 `Address` 속성을 `Order` 형식의 소유된 엔터티로 지정했습니다.

기본적으로 EF Core 규칙에서는 소유된 엔터티 형식의 속성에 대한 데이터베이스 열 이름을 `EntityProperty_OwnedEntityProperty`로 명명합니다. 그러므로 `Address`의 내부 속성이 `Orders` 테이블에 `Address_Street`, `Address_City`(`State`, `Country`, `ZipCode`에 대해서도 같은 방식으로)라는 이름으로 표시됩니다.

`Property().HasColumnName()` fluent 메서드를 추가하여 열 이름을 바꿀 수 있습니다. `Address`가 공용 속성인 경우 매핑은 다음과 같습니다.

```csharp
orderConfiguration.OwnsOne(p => p.Address)
                            .Property(p=>p.Street).HasColumnName("ShippingStreet");

orderConfiguration.OwnsOne(p => p.Address)
                            .Property(p=>p.City).HasColumnName("ShippingCity");
```

fluent 매핑에서 `OwnsOne` 메서드를 연결할 수 있습니다. 다음과 같은 가상의 예제에서 `OrderDetails`는 `BillingAddress` 및 `ShippingAddress`를 소유하며, 둘 다 `Address` 형식입니다. 그리고 `OrderDetails`는 `Order` 형식입니다.

```csharp
orderConfiguration.OwnsOne(p => p.OrderDetails, cb =>
    {
        cb.OwnsOne(c => c.BillingAddress);
        cb.OwnsOne(c => c.ShippingAddress);
    });
//...
//...
public class Order
{
    public int Id { get; set; }
    public OrderDetails OrderDetails { get; set; }
}

public class OrderDetails
{
    public Address BillingAddress { get; set; }
    public Address ShippingAddress { get; set; }
}

public class Address
{
    public string Street { get; set; }
    public string City { get; set; }
}
```

### <a name="additional-details-on-owned-entity-types"></a>소유된 엔터티 형식에 대한 추가 정보

- 소유된 형식은 OwnsOne 흐름 API를 사용하여 탐색 속성을 특정 형식으로 구성할 때 정의됩니다.

- 메타데이터 모델의 소유된 형식 정의는 소유된 형식의 소유자 형식, 탐색 속성 및 CLR 형식으로 구성됩니다.

- 스택의 소유된 형식 인스턴스의 ID(키)는 소유자 형식의 ID와 소유된 형식의 정의로 구성됩니다.

#### <a name="owned-entities-capabilities"></a>소유된 엔터티 기능:

- 소유된 형식은 소유된 엔터티(중첩된 소유된 형식) 또는 소유되지 않은 엔터티(다른 엔터티에 대한 일반 참조 탐색 속성)라는 다른 엔터티를 참조할 수 있습니다.

- 별도의 탐색 속성을 통해 동일한 소유자 엔터티의 다른 소유된 형식과 동일한 CLR 형식을 매핑할 수 있습니다.

- 테이블 분할은 규칙에 따라 설정되지만, ToTable을 사용하여 소유된 형식을 다른 테이블로 매핑하여 옵트아웃할 수 있습니다.

- 즉시 로드는 소유된 형식에서 자동으로 수행되므로 쿼리에서 include()를 호출할 필요가 없습니다.

- EF Core 2.1으로 \[소유된\] 특성을 사용하여 구성될 수 있습니다.

#### <a name="owned-entities-limitations"></a>소유된 엔터티의 제한 사항:

- 소유된 형식의 DbSet\<T\>를 만들 수 없습니다(설계 상).

- 소유된 형식에 대해 ModelBuilder.Entity\<T\>()를 호출할 수 없습니다(현재 설계 상).

- 아직 EF Core 2.1로 소유된 형식의 컬렉션이 없습니다(하지만 2.2에서 지원될 예정).

- 동일한 테이블(예: 테이블 분할 사용)에서 소유자로 매핑되는 선택적(예: null 허용) 소유된 형식이 지원되지 않습니다. 각 속성에 대해 매핑이 수행되기 때문에 null 복합 값에 대한 별도 sentinel이 전체로 포함되지 않습니다.

- 소유된 형식에 대한 상속 매핑이 지원되지 않지만, 다른 소유된 형식과 상속 계층 구조가 동일한 두 가지 리프 형식을 매핑할 수 있습니다. EF Core는 이러한 형식이 동일한 계층 구조의 일부라는 사실의 근거가 되지 못합니다.

#### <a name="main-differences-with-ef6s-complex-types"></a>EF6의 복합 형식과 다른 주요 차이점

- 테이블 분할은 선택 사항입니다. 즉, 별도 테이블에 선택적으로 매핑할 수 있으며 계속해서 소유된 형식이 될 수 있습니다.

- 다른 엔터티를 참조할 수 있습니다. 즉, 다른 소유되지 않은 형식과의 관계에서 종속되는 쪽의 역할을 할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

- **Martin Fowler. ValueObject 패턴** \
  <https://martinfowler.com/bliki/ValueObject.html>

- **Eric Evans. 도메인 기반 디자인: 소프트웨어 핵심에서 복잡성을 처리합니다.** (도서; 값 개체의 토론 포함) \
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

- **Vaughn Vernon. 도메인 기반 디자인 구현.** (도서; 값 개체의 토론 포함) \
  <https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/>

- **섀도 속성** \
  [https://docs.microsoft.com/ef/core/modeling/shadow-properties](/ef/core/modeling/shadow-properties)

- **복합 형식 및/또는 값 개체**. EF Core GitHub 리포지토리에서 토론(문제 탭) \
  <https://github.com/aspnet/EntityFramework/issues/246>

- **ValueObject.cs.** eShopOnContainers의 기준 값 개체 클래스. \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/SeedWork/ValueObject.cs>

- **주소 클래스.** eShopOnContainers의 동일한 값 개체 클래스. \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/AggregatesModel/OrderAggregate/Address.cs>

> [!div class="step-by-step"]
> [이전](seedwork-domain-model-base-classes-interfaces.md)
> [다음](enumeration-classes-over-enum-types.md)
