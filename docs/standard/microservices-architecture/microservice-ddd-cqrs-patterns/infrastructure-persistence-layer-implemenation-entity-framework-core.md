---
title: Entity Framework Core를 사용하여 인프라 지속성 레이어 구현
description: 컨테이너화된 .NET 응용 프로그램을 위한 .NET 마이크로 서비스 아키텍처 | Entity Framework Core를 사용하여 인프라 지속성 레이어 구현
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 12/12/2017
ms.openlocfilehash: 663515e0a863ef703006df0f96b4bc8a2976ca78
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50205297"
---
# <a name="implementing-the-infrastructure-persistence-layer-with-entity-framework-core"></a>Entity Framework Core를 사용하여 인프라 지속성 레이어 구현

SQL Server, Oracle 또는 PostgreSQL 같은 관계형 데이터베이스를 사용하는 경우 EF(Entity Framework) 기반의 지속성 레이어를 구현하는 것이 좋습니다. EF는 LINQ 지원하며 데이터베이스에 간소화된 지속성을 제공할 뿐 아니라 모델에 대한 강력한 형식의 개체를 제공합니다.

Entity Framework는 .NET Framework의 일부로 오랜 역사를 갖고 있습니다. .NET Core를 사용하는 경우 .NET Core와 마찬가지로 Windows 또는 Linux에서 실행되는 Entity Framework Core도 사용 해야 합니다. EF Core는 Entity Framework를 완전히 새로 작성한 것으로, 훨씬 적은 공간을 차지하며 성능이 대폭 향상되었습니다.

## <a name="introduction-to-entity-framework-core"></a>Entity Framework Core 소개

EF(Entity Framework) Core는 널리 사용되는 Entity Framework 데이터 액세스 기술의 가볍고 확장 가능하며 플랫폼 교차적인 버전입니다. 2016년 중순에 .NET Core에 도입되었습니다.

EF Core를 소개하는 내용은 이미 Microsoft 설명서에 있으므로 여기서는 간단하게 해당 정보에 대한 링크만 제공하겠습니다.

#### <a name="additional-resources"></a>추가 자료

-   **Entity Framework Core**
    [*https://docs.microsoft.com/ef/core/*](https://docs.microsoft.com/ef/core/)

-   **Visual Studio를 사용하여 ASP.NET Core 및 Entity Framework Core 시작**
    [*https://docs.microsoft.com/aspnet/core/data/ef-mvc/*](https://docs.microsoft.com/aspnet/core/data/ef-mvc/)

-   **DbContext Class**
    [*https://docs.microsoft.com/ef/core/api/microsoft.entityframeworkcore.dbcontext*](https://docs.microsoft.com/ef/core/api/microsoft.entityframeworkcore.dbcontext)

-   **EF Core & EF6.x 비교**
    [*https://docs.microsoft.com/ef/efcore-and-ef6/index*](https://docs.microsoft.com/ef/efcore-and-ef6/index)

## <a name="infrastructure-in-entity-framework-core-from-a-ddd-perspective"></a>DDD 관점에서 본 Entity Framework Core의 인프라

DDD 관점에서 본 EF의 중요한 기능은 POCO 도메인 엔터티를 사용하는 기능으로, EF 용어로는 POCO *코드 중심 엔터티*라고 합니다. POCO 도메인 엔터티를 사용하는 경우 도메인 모델 클래스는 [지속성 무시](https://deviq.com/persistence-ignorance/) 및 [인프라 무시](https://ayende.com/blog/3137/infrastructure-ignorance) 원칙에 따라 지속성을 무시합니다.

DDD 패턴마다 엔터티 클래스 자체 내의 도메인 동작과 규칙을 캡슐화해야만 컬렉션에 액세스할 때 고정, 유효성 검사 및 규칙을 제어할 수 있습니다. 따라서 DDD에서 자식 엔터티 또는 값 개체 컬렉션에 대한 공용 액세스를 허용하는 것은 좋지 않습니다. 그 대신, 속성 컬렉션을 업데이트할 수 있는 방법 및 시기 그리고 속성 컬렉션 업데이트가 발생할 때 수행할 동작 및 작업을 제어하는 메서드를 노출하는 것이 좋습니다.

EF Core 1.1부터는 DDD 요구 사항을 충족하기 위해 엔터티에 공용 속성 대신 일반 필드를 사용할 수 있습니다. 외부에서 엔터티 필드에 액세스하지 못하게 하려면 속성 대신 특성 또는 필드를 만들면 됩니다. 개인 속성 setter를 사용하면 됩니다.

이와 비슷한 방법으로, 이제 `IReadOnlyCollection<T>`으로 형식화된 공용 속성을 사용하여 컬렉션에 읽기 전용으로 액세스할 수 있으며, 이 형식은 지속성 때문에 EF를 사용하는 엔터티의 컬렉션에 대한 전용 필드 멤버(예: `List<T>`)를 통해 지원됩니다. 이전 버전의 Entity Framework는 `ICollection<T>`을 지원하려면 컬렉션 속성이 필요했으며, 부모 엔터티 클래스를 사용하는 개발자가 속성 컬렉션을 통해 항목을 추가 또는 제거할 수 있었다는 의미입니다. 이 가능성은 DDD의 권장 패턴과 상반됩니다.

다음 코드 예제와 같이, 읽기 전용 `IReadOnlyCollection<T>` 개체를 노출할 때 전용 컬렉션을 사용할 수 있습니다.

```csharp
public class Order : Entity
{
    // Using private fields, allowed since EF Core 1.1
    private DateTime _orderDate;
    // Other fields ...

    private readonly List<OrderItem> _orderItems; 
    public IReadOnlyCollection<OrderItem> OrderItems => _orderItems;

    protected Order() { }

    public Order(int buyerId, int paymentMethodId, Address address)
    {
        // Initializations ...
    }

    public void AddOrderItem(int productId, string productName,
                             decimal unitPrice, decimal discount,
                             string pictureUrl, int units = 1)
    {
        // Validation logic...

        var orderItem = new OrderItem(productId, productName, 
                                      unitPrice, discount,
                                      pictureUrl, units);
        _orderItems.Add(orderItem);
    }
}
```

`OrderItems` 속성은 `IReadOnlyCollection<OrderItem>`을 사용하여 읽기 전용으로만 액세스할 수 있습니다. 이 형식은 읽기 전용이므로 정기적인 업데이트로부터 보호됩니다. 

EF Core는 도메인 모델을 "오염"시키지 않고 도메인 모델을 물리적 데이터베이스에 매핑할 수 있는 방법을 제공합니다. 매핑 작업이 지속성 레이어에서 구현되는 순수 .NET POCO 코드입니다. 이 매핑 작업에서 필드-데이터베이스 매핑을 구성해야 합니다. 다음 OnModelCreating 메서드 예제에서 강조 표시된 코드는 필드를 통해 OrderItems 속성에 액세스하라고 EF 코어에 알려줍니다.

```csharp
// At OrderingContext.cs from eShopOnContainers
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
   // ...
   modelBuilder.ApplyConfiguration(new OrderEntityTypeConfiguration());
   // Other entities’ configuration ...
}

// At OrderEntityTypeConfiguration.cs from eShopOnContainers
class OrderEntityTypeConfiguration : IEntityTypeConfiguration<Order>
{
    public void Configure(EntityTypeBuilder<Order> orderConfiguration)
    {
        orderConfiguration.ToTable("orders", OrderingContext.DEFAULT_SCHEMA);
        // Other configuration

        var navigation = 
              orderConfiguration.Metadata.FindNavigation(nameof(Order.OrderItems));

        //EF access the OrderItem collection property through its backing field
        navigation.SetPropertyAccessMode(PropertyAccessMode.Field);

        // Other configuration
    }
}
```

속성 대신 필드를 사용하면 OrderItem 엔터티는 마치 List&lt;OrderItem&gt; 속성이 있는 것처럼 유지됩니다. 그러나 주문에 새 항목을 추가하기 위한 단일 접근자인 `AddOrderItem` 메서드를 노출합니다. 결과적으로 동작 및 데이터는 서로 연결되고 도메인 모델을 사용하는 응용 프로그램 코드 전체에서 일관적으로 유지됩니다.

## <a name="implementing-custom-repositories-with-entity-framework-core"></a>Entity Framework Core를 사용하여 사용자 지정 리포지토리 구현

구현 수준에서 보자면, 리포지토리는 다음 클래스에서 볼 수 있듯이 업데이트를 수행할 때 작업 단위(EF Core의 DBContext)에 의해 조정되는 데이터 지속성 코드가 있는 클래스일 뿐입니다.

```csharp
// using statements...
namespace Microsoft.eShopOnContainers.Services.Ordering.Infrastructure.Repositories
{
    public class BuyerRepository : IBuyerRepository
    {
        private readonly OrderingContext _context;
        public IUnitOfWork UnitOfWork
        {
            get
            {
                return _context;
            }
        }

        public BuyerRepository(OrderingContext context)
        {
            _context = context ?? throw new ArgumentNullException(nameof(context));
        }

        public Buyer Add(Buyer buyer)
        {
            return _context.Buyers.Add(buyer).Entity; 
        }

        public async Task<Buyer> FindAsync(string BuyerIdentityGuid)
        {
            var buyer = await _context.Buyers
                .Include(b => b.Payments)
                .Where(b => b.FullName == BuyerIdentityGuid)
                .SingleOrDefaultAsync();

            return buyer;
        }
    }
}
```

IBuyerRepository 인터페이스는 도메인 모델 레이어에서 계약으로 가져옵니다. 그러나 리포지토리 구현은 지속성 및 인프라 레이어에서 수행됩니다.

EF DbContext는 종속성 주입을 통해 생성자를 거쳐 가져옵니다. IoC 컨테이너(services.AddDbContext&lt;&gt;를 사용하여 명시적으로도 설정 가능)의 기본 수명 주기(ServiceLifetime.Scoped) 덕분에 동일한 HTTP 요청 범위 내의 여러 리포지토리 간에 공유됩니다.

### <a name="methods-to-implement-in-a-repository-updates-or-transactions-versus-queries"></a>리포지토리에서 구현하는 메서드(업데이트 또는 트랜잭션과 쿼리 비교)

각 리포지토리 클래스 내에서, 관련 집계에 의해 포함되는 엔터티 상태를 업데이트하는 지속성 메서드를 배치해야 합니다. 집계와 집계 관련 리포지토리 사이에는 일대일 관계가 성립합니다. 집계 루트 엔터티 개체가 EF 그래프 내에 자식 엔터티를 포함할 수 있다는 점을 고려해야 합니다. 예를 들어 구매자가 관련 자식 엔터티로 여러 지불 방법을 보유할 수 있습니다.

eShopOnContainers에서 마이크로 서비스를 주문하는 방식도 CQS/CQRS 기반이므로 대부분의 쿼리가 사용자 지정 리포지토리에서 구현되지 않습니다. 개발자는 집계, 집계별 사용자 지정 리포지토리 그리고 일반적으로 DDD에서 부과하는 제한 없이 프레젠테이션 레이어에 필요한 쿼리 및 조인을 자유롭게 만들 수 있습니다. 이 가이드에서 권장하는 대부분의 사용자 지정 리포지토리는 여러 업데이트 또는 트랜잭션 메서드를 갖고 있지만 데이터를 가져오는 데 필요한 쿼리 메서드만 업데이트해야 합니다. 예를 들어 BuyerRepository 리포지토리는 FindAsync 메서드를 구현합니다. 응용 프로그램에서 특정 구매자의 존재 여부를 알아야만 주문과 관련된 새 구매자를 만들 수 있기 때문입니다.

그러나 프레젠테이션 레이어 또는 클라이언트 앱으로 보낼 데이터를 가져오는 실제 쿼리 메서드는 앞서 언급했듯이 Dapper를 사용하여 유연한 쿼리를 기반으로 CQRS 쿼리로 구현됩니다.

### <a name="using-a-custom-repository-versus-using-ef-dbcontext-directly"></a>사용자 지정 리포지토리를 사용하는 방법과 EF DbContext를 직접 사용하는 방법 비교

Entity Framework DbContext 클래스는 작업 단위 및 리포지토리 패턴을 기반으로 하며, ASP.NET Core MVC 컨트롤러처럼 코드에서 직접 사용할 수 있습니다. eShopOnContainers의 CRUD 카탈로그 마이크로 서비스에서 하듯이, 이 방법으로 가장 간단한 코드를 만들 수 있습니다. 최대한 간단한 코드를 원하는 경우 여러 개발자들이 하는 것처럼 DbContext 클래스를 직접 사용할 수 있습니다.

그러나 사용자 지정 리포지토리를 구현하면 보다 복잡한 마이크로 서비스 또는 응용 프로그램을 구현할 때 여러 가지 이점이 있습니다. 작업 단위 및 리포지토리 패턴은 응용 프로그램 및 도메인 모델 레이어에서 분리되는 인프라 지속성 레이어를 캡슐화하는 데 사용됩니다. 이러한 패턴을 구현하면 모의 리포지토리를 사용하여 데이터베이스에 대한 액세스를 시뮬레이션할 수 있습니다.

그림 9-18에서는 리포지토리를 사용하지 않을 때와(EF DbContext를 직접 사용) 리포지토리를 사용하여 좀 더 쉽게 리포지토리 모형을 만들 때의 차이를 볼 수 있습니다.

![](./media/image19.png)

**그림 9-18**. 사용자 지정 리포지토리와 일반 DbContext 비교

모형을 만들 때 여러 가지 대안이 있습니다. 리포지토리 모형만 만들 수도 있고 작업 단위 전체의 모형을 만들 수도 있습니다. 일반적으로 리포지토리 모형만 만들면 충분하며, 복잡하게 작업 단위 전체를 추상화하고 모형을 만들 필요는 없습니다.

뒤에서 응용 프로그램 계층을 살펴볼 때, ASP.NET Core에서 종속성 주입의 작동 원리와 리포지토리를 사용할 때 구현 방식을 볼 수 있습니다.

요약하자면, 사용자 지정 리포지토리를 사용하면 데이터 계층 상태의 영향을 받지 않는 단위 테스트로 코드를 보다 쉽게 테스트할 수 있습니다. Entity Framework를 통해 실제 데이터베이스에 액세스하는 테스트를 실행하는 경우 통합 테스트가 아닌 단위 테스트이며, 속도가 훨씬 느립니다.

DbContext를 직접 사용하는 경우 개발자가 할 수 있는 유일한 선택은 예측 가능한 데이터와 함께 메모리 내 SQL Server를 단위 테스트에 사용하여 단위 테스트를 실행하는 것입니다. 모의 개체 및 모조 데이터를 리포지토리 수준에서 하는 것과 동일한 방식으로 제어할 수 없습니다. 물론, 항상 MVC 컨트롤러를 테스트할 수 있습니다.

## <a name="ef-dbcontext-and-iunitofwork-instance-lifetime-in-your-ioc-container"></a>IoC 컨테이너의 EF DbContext 및 IUnitOfWork 인스턴스 수명

DbContext 개체(IUnitOfWork 개체로 노출)는 동일한 HTTP 요청 범위 내에 있는 여러 리포지토리 간에 공유해야 합니다. 실행 중인 작업에서 여러 집계를 처리해야 하거나 여러 리포지토리 인스턴스를 사용하는 경우를 예로 들 수 있습니다. IUnitOfWork 인터페이스는 EF Core 형식이 아닌 도메인 레이어의 일부라는 점도 언급해야 합니다.

그러려면 DbContext 개체 인스턴스의 서비스 수명이 ServiceLifetime.Scoped로 설정되어야 합니다. 이것은 ASP.NET Core Web API 프로젝트에서 Startup.cs 파일의 ConfigureServices 메서드에 있는 IoC 컨테이너의 services.AddDbContext에 DbContext를 등록할 때 기본 수명입니다. 다음 코드에서는 이를 보여 줍니다.

```csharp
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    // Add framework services.
    services.AddMvc(options =>
    {
        options.Filters.Add(typeof(HttpGlobalExceptionFilter));
    }).AddControllersAsServices();

    services.AddEntityFrameworkSqlServer()
      .AddDbContext<OrderingContext>(options =>
      {
          options.UseSqlServer(Configuration["ConnectionString"],
                               sqlOptions => sqlOptions.MigrationsAssembly(typeof(Startup).GetTypeInfo().
                                                                                    Assembly.GetName().Name));
      },
      ServiceLifetime.Scoped // Note that Scoped is the default choice
                             // in AddDbContext. It is shown here only for
                             // pedagogic purposes.
      );
}
```

DbContext 인스턴스화 모드를 ServiceLifetime.Transient 또는 ServiceLifetime.Singleton로 구성하면 안 됩니다.

## <a name="the-repository-instance-lifetime-in-your-ioc-container"></a>IoC 컨테이너의 리포지토리 인스턴스 수명

마찬가지로 리포지토리 수명은 일반적으로 그 범위를 지정해야 합니다(Autofac의 InstancePerLifetimeScope). 임시로 지정할 수도 있지만(Autofac의 InstancePerDependency) 수명 범위를 지정하면 메모리와 관련한 서비스 효율이 향상됩니다.

```csharp
// Registering a Repository in Autofac IoC container
builder.RegisterType<OrderRepository>()
    .As<IOrderRepository>()
    .InstancePerLifetimeScope();
```

리포지토리에 singleton 수명을 사용하면 DbContext를 범위가 지정된(InstancePerLifetimeScope) 수명으로 설정(DBContext의 기본 수명)할 경우 심각한 동시성 문제가 발생할 수 있습니다.

#### <a name="additional-resources"></a>추가 자료

-   **ASP.NET MVC 응용 프로그램에서 작업 패턴의 리포지토리 및 단위 구현**
    [*https://www.asp.net/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application*](https://www.asp.net/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application)

-   **Jonathan Allen. Entity Framework, Dapper 및 Chain을 사용하여 리포지토리 패턴에 대한 전략 구현**
    [*https://www.infoq.com/articles/repository-implementation-strategies*](https://www.infoq.com/articles/repository-implementation-strategies)

-   **Cesar de la Torre. ASP.NET Core IoC 컨테이너 서비스 수명과 Autofac IoC 컨테이너 인스턴스 범위 비교**
    [*https://blogs.msdn.microsoft.com/cesardelatorre/2017/01/26/comparing-asp-net-core-ioc-service-life-times-and-autofac-ioc-instance-scopes/*](https://blogs.msdn.microsoft.com/cesardelatorre/2017/01/26/comparing-asp-net-core-ioc-service-life-times-and-autofac-ioc-instance-scopes/)

## <a name="table-mapping"></a>테이블 매핑

테이블 매핑은 데이터베이스에서 쿼리하고 저장할 테이블 데이터를 식별합니다. 앞에서 도메인 엔터티(예: 제품 또는 주문 도메인)를 사용하여 관련 데이터베이스 스키마를 생성하는 방법을 살펴보았습니다. EF는 *규칙* 개념을 중심으로 강력하게 설계됩니다. 규칙은 "테이블의 이름은 무엇이 될까요?" 또는 “기본 키는 무슨 속성입니까?”와 같은 질문을 해결합니다. 규칙은 일반적으로 관습적 이름을 기반으로 합니다. 예를 들어 일반적으로 기본 키는 Id로 끝나는 속성이 됩니다.

규칙에 따라 각 엔터티는 파생 컨텍스트에 엔터티를 노출하는 DbSet&lt;TEntity&gt; 속성과 이름이 같은 테이블에 매핑되도록 설정됩니다. 특정 엔터티에 DbSet&lt;TEntity&gt; 값이 제공되지 않으면 클래스 이름이 사용됩니다.

### <a name="data-annotations-versus-fluent-api"></a>데이터 주석과 흐름 API 비교

여러 가지 추가 EF Core 규칙이 있으며, 그 중 대부분은 데이터 주석 또는 흐름 API를 사용하여 변경하고, OnModelCreating 메서드 내에서 구현할 수 있습니다.

데이터 주석은 엔터티 모델 클래스 자체에 사용해야 하며, DDD 관점에서 개입 수준이 높은 방법입니다. 인프라 데이터베이스와 관련된 데이터 주석으로 모델을 오염시키기 때문입니다. 반면 흐름 API는 데이터 지속성 인프라 계층 내부의 규칙과 매핑을 대부분 변경할 수 있는 편리한 방법으로, 엔터티 모델이 깔끔하고 지속성 인프라와 분리됩니다.

### <a name="fluent-api-and-the-onmodelcreating-method"></a>흐름 API 및 OnModelCreating 메서드

앞서 언급했듯이, 규칙 및 매핑을 변경하려면 DbContext 클래스의 OnModelCreating 메서드를 사용하면 됩니다. 

eShopOnContainers의 주문 마이크로 서비스는 다음 코드에 보이는 것처럼 필요에 따라 명시적 매핑 및 구성을 구현합니다.

```csharp
// At OrderingContext.cs from eShopOnContainers
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
   // ...
   modelBuilder.ApplyConfiguration(new OrderEntityTypeConfiguration());
   // Other entities’ configuration ...
}

// At OrderEntityTypeConfiguration.cs from eShopOnContainers
class OrderEntityTypeConfiguration : IEntityTypeConfiguration<Order>
{
    public void Configure(EntityTypeBuilder<Order> orderConfiguration)
    {
            orderConfiguration.ToTable("orders", OrderingContext.DEFAULT_SCHEMA);

            orderConfiguration.HasKey(o => o.Id);

            orderConfiguration.Ignore(b => b.DomainEvents);

            orderConfiguration.Property(o => o.Id)
                .ForSqlServerUseSequenceHiLo("orderseq", OrderingContext.DEFAULT_SCHEMA);

            //Address Value Object persisted as owned entity type supported since EF Core 2.0
            orderConfiguration.OwnsOne(o => o.Address);

            orderConfiguration.Property<DateTime>("OrderDate").IsRequired();
            orderConfiguration.Property<int?>("BuyerId").IsRequired(false);
            orderConfiguration.Property<int>("OrderStatusId").IsRequired();
            orderConfiguration.Property<int?>("PaymentMethodId").IsRequired(false);
            orderConfiguration.Property<string>("Description").IsRequired(false);

            var navigation = orderConfiguration.Metadata.FindNavigation(nameof(Order.OrderItems));
            
            // DDD Patterns comment:
            //Set as field (New since EF 1.1) to access the OrderItem collection property through its field
            navigation.SetPropertyAccessMode(PropertyAccessMode.Field);

            orderConfiguration.HasOne<PaymentMethod>()
                .WithMany()
                .HasForeignKey("PaymentMethodId")
                .IsRequired(false)
                .OnDelete(DeleteBehavior.Restrict);

            orderConfiguration.HasOne<Buyer>()
                .WithMany()
                .IsRequired(false)
                .HasForeignKey("BuyerId");

            orderConfiguration.HasOne(o => o.OrderStatus)
                .WithMany()
                .HasForeignKey("OrderStatusId");
    }
}
```

동일한 OnModelCreating 메서드 내에서 모든 흐름 API 매핑을 설정할 수 있지만, 예제에 보이는 것처럼 해당 코드를 분할하여 여러 구성 클래스를 두는 것이 좋습니다. 특히 매우 큰 모델의 경우 여러 엔터티 형식을 구성하기 위한 별도의 클래스를 두는 것이 좋습니다.

예제의 코드는 몇 가지 명시적 선언 및 매핑을 보여줍니다. 그러나 EF Core 규칙에서 이러한 매핑의 상당수를 자동으로 처리하므로 필요한 실제 코드 크기는 더 작아질 수 있습니다.


### <a name="the-hilo-algorithm-in-ef-core"></a>EF Core의 Hi/Lo 알고리즘

앞의 예제에서 본 코드의 흥미로운 점은 키 생성 전략으로 [Hi/Lo 알고리즘](https://vladmihalcea.com/the-hilo-algorithm/)을 사용한다는 것입니다.

Hi/Lo 알고리즘은 고유 키가 필요한 경우에 유용합니다. 요약하자면, Hi-Lo 알고리즘은 테이블 행에 고유 식별자를 할당하지만 행을 데이터베이스에 즉시 저장하지 않습니다. 따라서 일반 순차적 데이터베이스 ID와 마찬가지로 식별자를 사용하여 바로 시작할 수 있습니다.

Hi/Lo 알고리즘은 데이터베이스가 아닌 클라이언트 쪽에서 안전한 ID를 생성하는 메커니즘을 설명합니다. 여기서 말하는 *안전*이란 충돌이 없다는 의미입니다. 이 알고리즘이 흥미로운 이유는 다음과 같습니다.

-   작업 단위 패턴을 중단하지 않습니다.

-   시퀀스 생성기가 다른 DBMS에서 하는 방식으로 라운드트립을 할 필요가 없습니다.

-   GUID를 사용하는 기술은 달리, 사람이 읽을 수 있는 식별자를 생성합니다.

EF Core는 앞의 예제와 같이 ForSqlServerUseSequenceHiLo 메서드를 통해 [HiLo](https://stackoverflow.com/questions/282099/whats-the-hi-lo-algorithm)를 지원합니다.

### <a name="mapping-fields-instead-of-properties"></a>속성 대신 필드 매핑

EF Core 1.1부터 제공되는 이 기능을 사용하면 열을 필드로 직접 매핑할 수 있습니다. 엔터티 클래스에서 속성을 사용하지 않고 테이블에서 필드로 열을 매핑할 수 있습니다. 엔터티 외부에서 액세스할 필요가 없는 내부 상태에 대한 전용 필드가 대표적인 사용 사례입니다. 

단일 필드를 사용하여 또는 `List<>` 필드 같은 컬렉션을 사용하여 이렇게 할 수 있습니다. 이 부분은 도메인 모델 클래스 모델링에 대해 토론할 때 살펴보았지만, 여기서는 이전 코드에서 강조 표시된 `PropertyAccessMode.Field` 구성을 통해 매핑이 수행되는 방식을 살펴볼 수 있습니다.

### <a name="using-shadow-properties-in-ef-core-hidden-at-the-infrastructure-level"></a>인프라 수준에서 숨겨진 EF Core의 섀도 속성 사용

EF Core의 섀도 속성은 엔터티 클래스 모델에 존재하지 않는 속성입니다. 이러한 속성의 값과 상태는 인프라 수준에서 [ChangeTracker](https://docs.microsoft.com/ef/core/api/microsoft.entityframeworkcore.changetracking.changetracker) 클래스에 순수하게 유지됩니다.


## <a name="implementing-the-specification-pattern"></a>사양 패턴 구현

디자인 섹션에서 언급했듯이, 사양 패턴(전체 이름은 쿼리 사양 패턴입니다)은 선택적 정렬과 페이징 논리를 사용해 쿼리를 정의 내릴 수 있는 공간으로 디자인된 도메인 기반 디자인 패턴입니다. 사양 패턴은 개체에서 쿼리를 정의합니다. 예를 들어 일부 제품을 검색하는 페이징된 쿼리를 캡슐화하려면 필요한 입력 매개 변수(pageNumber, pageSize, 필터 등)를 사용하는 PagedProduct 사양을 만들 수 있습니다. 그런 다음, 리포지토리의 메서드(일반적으로 목록() 오버로드)가 ISpecification을 수용하고 해당 사양을 기반으로 필요한 쿼리를 실행합니다.

제네릭 사양 인터페이스의 예제는 [eShopOnweb](https://github.com/dotnet-architecture/eShopOnWeb)의 다음 코드입니다. 

```csharp
// GENERIC SPECIFICATION INTERFACE
// https://github.com/dotnet-architecture/eShopOnWeb 

public interface ISpecification<T>
{
    Expression<Func<T, bool>> Criteria { get; }
    List<Expression<Func<T, object>>> Includes { get; }
    List<string> IncludeStrings { get; }
}
```

그런 다음, 제네릭 사양 기본 클래스의 구현은 다음과 같습니다.

```csharp
// GENERIC SPECIFICATION IMPLEMENTATION (BASE CLASS)
// https://github.com/dotnet-architecture/eShopOnWeb
 
public abstract class BaseSpecification<T> : ISpecification<T>
{
    public BaseSpecification(Expression<Func<T, bool>> criteria)
    {
        Criteria = criteria;
    }
    public Expression<Func<T, bool>> Criteria { get; }

    public List<Expression<Func<T, object>>> Includes { get; } = 
                                           new List<Expression<Func<T, object>>>();

    public List<string> IncludeStrings { get; } = new List<string>();
 
    protected virtual void AddInclude(Expression<Func<T, object>> includeExpression)
    {
        Includes.Add(includeExpression);
    }
    
    // string-based includes allow for including children of children
    // e.g. Basket.Items.Product
    protected virtual void AddInclude(string includeString)
    {
        IncludeStrings.Add(includeString);
    }
}
```

다음 사양은 장바구니의 ID 또는 장바구니가 속한 구매자의 ID가 지정된 단일 장바구니 엔터티를 로드합니다. 장바구니의 항목 컬렉션을 [즉시 로드](https://docs.microsoft.com/ef/core/querying/related-data)합니다.

```csharp
// SAMPLE QUERY SPECIFICATION IMPLEMENTATION

public class BasketWithItemsSpecification : BaseSpecification<Basket>
{
    public BasketWithItemsSpecification(int basketId)
        : base(b => b.Id == basketId)
    {
        AddInclude(b => b.Items);
    }
    public BasketWithItemsSpecification(string buyerId)
        : base(b => b.BuyerId == buyerId)
    {
        AddInclude(b => b.Items);
    }
}
```

마지막으로, 아래를 보시면 제네릭 EF 리포지토리가 사양을 사용하여 특정 엔터티 형식 T와 관련된 데이터를 필터링하고 즉시 로드하는 원리를 살펴볼 수 있습니다.

```csharp
// GENERIC EF REPOSITORY WITH SPECIFICATION
// https://github.com/dotnet-architecture/eShopOnWeb

public IEnumerable<T> List(ISpecification<T> spec)
{
    // fetch a Queryable that includes all expression-based includes
    var queryableResultWithIncludes = spec.Includes
        .Aggregate(_dbContext.Set<T>().AsQueryable(),
            (current, include) => current.Include(include));
 
    // modify the IQueryable to include any string-based include statements
    var secondaryResult = spec.IncludeStrings
        .Aggregate(queryableResultWithIncludes,
            (current, include) => current.Include(include));
 
    // return the result of the query using the specification's criteria expression
    return secondaryResult
                    .Where(spec.Criteria)
                    .AsEnumerable();
}
```
사양은 필터링 논리를 캡슐화할 뿐 아니라 채울 속성을 포함하여 반환될 데이터의 모양을 지정할 수 있습니다. 

리포지토리에서 IQueryable을 반환하는 것을 권장하지는 않지만, 리포지토리 내에서 사용하여 결과 집합을 빌드하는 데 사용하는 것은 아무 문제 없습니다. 위의 List 메서드에 이 접근 방식이 사용된 것을 볼 수 있습니다. 중간 IQueryable 식을 사용하여 쿼리의 포함 목록을 빌드한 후 마지막 줄에서 사양의 기준을 사용하여 쿼리가 실행됩니다.


#### <a name="additional-resources"></a>추가 자료

-   **테이블 매핑**
    [*https://docs.microsoft.com/ef/core/modeling/relational/tables*](https://docs.microsoft.com/ef/core/modeling/relational/tables)

-   **Entity Framework Core를 사용하여 키를 생성하도록 HiLo 사용**
    [*http://www.talkingdotnet.com/use-hilo-to-generate-keys-with-entity-framework-core/*](http://www.talkingdotnet.com/use-hilo-to-generate-keys-with-entity-framework-core/)

-   **지원 필드**
    [*https://docs.microsoft.com/ef/core/modeling/backing-field*](https://docs.microsoft.com/ef/core/modeling/backing-field)

-   **Steve Smith. Entity Framework Core에서 캡슐화된 컬렉션**
    [*https://ardalis.com/encapsulated-collections-in-entity-framework-core*](https://ardalis.com/encapsulated-collections-in-entity-framework-core)

-   **섀도 속성**
    [*https://docs.microsoft.com/ef/core/modeling/shadow-properties*](https://docs.microsoft.com/ef/core/modeling/shadow-properties)

-   **사양 패턴**
    [*https://deviq.com/specification-pattern/*](https://deviq.com/specification-pattern/)
    

>[!div class="step-by-step"]
[이전](infrastructure-persistence-layer-design.md)
[다음](nosql-database-persistence-infrastructure.md)
