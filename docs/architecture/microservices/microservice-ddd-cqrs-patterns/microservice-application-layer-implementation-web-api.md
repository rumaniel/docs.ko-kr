---
title: Web API를 사용하여 마이크로 서비스 애플리케이션 계층 구현
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | Web API 애플리케이션 계층에서 종속성 주입 및 중재자 패턴과 해당 구현 정보를 이해합니다.
ms.date: 10/08/2018
ms.openlocfilehash: df304ffbe2406323e3dcf42b9eb989b02a62b28b
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72249741"
---
# <a name="implement-the-microservice-application-layer-using-the-web-api"></a>Web API를 사용하여 마이크로 서비스 에플리케이션 계층 구현

## <a name="use-dependency-injection-to-inject-infrastructure-objects-into-your-application-layer"></a>종속성 주입을 사용하여 애플리케이션 계층에 인프라 개체 주입

앞에서 언급했듯이 애플리케이션 계층은 Web API 프로젝트 또는 MVC 웹앱 프로젝트와 같이 빌드하고 있는 아티팩트(어셈블리)의 일부로 구현될 수 있습니다. ASP.NET Core로 구축된 마이크로 서비스의 경우 애플리케이션 계층은 일반적으로 Web API 라이브러리입니다. ASP.NET Core(인프라와 컨트롤러)를 사용자 지정 애플리케이션 계층 코드에서 분리하려는 경우 애플리케이션 계층을 별도의 클래스 라이브러리에 배치할 수도 있지만 이것은 선택 사항입니다.

예를 들어 Ordering(주문) 마이크로 서비스의 애플리케이션 계층 코드는 그림 7-23과 같이 **Ordering.API** 프로젝트(ASP.NET Core Web API 프로젝트)의 일부로 직접 구현됩니다.

![Application 폴더의 하위 폴더를 보여주는 Ordering.API 마이크로 서비스의 솔루션 탐색기 보기: Behaviors, Commands, DomainEventHandlers, IntegrationEvents, Models, Queries 및 Validations.](./media/image20.png)

**그림 7-23**. Ordering.API ASP.NET Core Web API 프로젝트의 애플리케이션 계층

ASP.NET Core에는 생성자 주입을 기본으로 지원하는 간단한 [내장 IoC 컨테이너](https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection)(IServiceProvider 인터페이스로 표시됨)가 포함되며, ASP.NET은 DI를 통해 특정 서비스를 사용할 수 있도록 합니다. ASP.NET Core는 DI를 통해 주입될 사용자가 등록하는 모든 형식에 *서비스*라는 용어를 사용합니다. 내장 컨테이너의 서비스는 애플리케이션의 Startup 클래스에 있는 ConfigureServices 메서드에 구성합니다. 종속성은 형식에 필요하며 IoC 컨테이너에 등록하는 서비스에 구현됩니다.

일반적으로 인프라 개체를 구현하는 종속성을 주입하려고 합니다. 매우 일반적으로 주입하는 종속성은 리포지토리입니다. 하지만 다른 인프라 종속성을 주입할 수도 있습니다. 간단한 구현을 위해 작업 단위 패턴 개체(EF DbContext 개체)를 직접 주입할 수 있는데, DBContext 역시 인프라 지속성 개체의 구현이기 때문입니다.

다음 예제에서는 .NET Core가 생성자를 통해 필요한 리포지토리 개체를 어떻게 주입하는지 볼 수 있습니다. 클래스는 명령 처리기이며, 다음 섹션에 설명되어 있습니다.

```csharp
public class CreateOrderCommandHandler
    : IAsyncRequestHandler<CreateOrderCommand, bool>
{
    private readonly IOrderRepository _orderRepository;
    private readonly IIdentityService _identityService;
    private readonly IMediator _mediator;

    // Using DI to inject infrastructure persistence Repositories
    public CreateOrderCommandHandler(IMediator mediator,
                                     IOrderRepository orderRepository,
                                     IIdentityService identityService)
    {
        _orderRepository = orderRepository ??
                          throw new ArgumentNullException(nameof(orderRepository));
        _identityService = identityService ??
                          throw new ArgumentNullException(nameof(identityService));
        _mediator = mediator ??
                                 throw new ArgumentNullException(nameof(mediator));
    }

    public async Task<bool> Handle(CreateOrderCommand message)
    {
        // Create the Order AggregateRoot
        // Add child entities and value objects through the Order aggregate root
        // methods and constructor so validations, invariants, and business logic
        // make sure that consistency is preserved across the whole aggregate
        var address = new Address(message.Street, message.City, message.State,
                                  message.Country, message.ZipCode);
        var order = new Order(message.UserId, address, message.CardTypeId,
                              message.CardNumber, message.CardSecurityNumber,
                              message.CardHolderName, message.CardExpiration);

        foreach (var item in message.OrderItems)
        {
            order.AddOrderItem(item.ProductId, item.ProductName, item.UnitPrice,
                               item.Discount, item.PictureUrl, item.Units);
        }

        _orderRepository.Add(order);

        return await _orderRepository.UnitOfWork
            .SaveEntitiesAsync();
    }
}
```

클래스는 삽입된 리포지토리를 사용하여 트랜잭션을 실행하고 상태 변경 내용을 유지합니다. 클래스가 명령 처리기이든, .NET Core Web API 컨트롤러 메서드이든 [DDD 애플리케이션 서비스](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/)이든 상관없습니다. 궁극적으로 리포지토리, 도메인 엔터티 및 기타 애플리케이션 조합을 명령 처리기와 비슷한 방식으로 사용하는 간단한 클래스입니다. 종속성 주입은 생성자를 기반으로 DI를 사용하는 예제처럼 언급된 모든 클래스에 대해 동일한 방식으로 작동합니다.

### <a name="register-the-dependency-implementation-types-and-interfaces-or-abstractions"></a>종속성 구현 형식 및 인터페이스 또는 추상화 등록

생성자를 통해 주입된 개체를 사용하기 전에 DI를 통해 애플리케이션 클래스에 삽입되는 개체를 생성하는 인터페이스와 클래스를 어디에 등록해야 하는지 알아야 합니다. (이전에 표시된 생성자에 기반한 DI와 유사합니다.)

#### <a name="use-the-built-in-ioc-container-provided-by-aspnet-core"></a>ASP.NET Core에 제공되는 기본 제공 IoC 컨테이너 사용

ASP.NET Core에 제공되는 내장 IoC 컨테이너를 사용하는 경우, Startup.cs 파일의 ConfigureServices 메서드에 삽입할 형식을 다음 코드와 같이 등록합니다.

```csharp
// Registration of types into ASP.NET Core built-in container
public void ConfigureServices(IServiceCollection services)
{
    // Register out-of-the-box framework services.
    services.AddDbContext<CatalogContext>(c =>
    {
        c.UseSqlServer(Configuration["ConnectionString"]);
    },
    ServiceLifetime.Scoped
    );
    services.AddMvc();
    // Register custom application dependencies.
    services.AddScoped<IMyCustomRepository, MyCustomSQLRepository>();
}
```

IoC 컨테이너에 형식을 등록할 때 가장 일반적인 패턴은 한 쌍의 형식(인터페이스 및 관련된 구현 클래스)을 등록하는 것입니다. 그런 다음, 생성자를 통해 IoC 컨테이너에서 개체를 요청하면 특정 형식의 인터페이스 개체를 요청합니다. 예를 들어, 이전 예제의 마지막 줄에는 IMyCustomRepository에 대한 종속성이 있는 생성자가 있으면 IoC 컨테이너는 MyCustomSQLServerRepository 구현 클래스의 인스턴스를 삽입한다는 내용이 언급되어 있습니다.

#### <a name="use-the-scrutor-library-for-automatic-types-registration"></a>자동 형식 등록을 위해 Scrutor 라이브러리 사용

.NET Core에서 DI를 사용하는 경우 어셈블리를 스캔하고 규칙에 따라 해당 형식을 자동으로 등록할 수 있도록 하는 것이 좋습니다. 이 기능은 현재 ASP.NET Core에서 사용할 수 없습니다. 하지만 [Scrutor](https://github.com/khellang/Scrutor) 라이브러리를 대신 사용할 수 있습니다. 이 방법은 IoC 컨테이너에 등록해야 하는 형식이 수십 개인 경우에 유용합니다.

#### <a name="additional-resources"></a>추가 자료

- **Matthew King. Scrutor에 서비스 등록** \
  <https://www.mking.net/blog/registering-services-with-scrutor>

- **Kristian Hellang. Scrutor.** GitHub 리포지토리. \
  <https://github.com/khellang/Scrutor>

#### <a name="use-autofac-as-an-ioc-container"></a>IoC 컨테이너로 Autofac 사용

또한 추가 IoC 컨테이너를 사용하고 이것을 ASP.NET Core 파이프라인에 연결할 수도 있습니다. 이것은 [Autofac](https://autofac.org/)을 사용하는 eShopOnContainers의 Ordering(주문) 마이크로 서비스와 유사합니다. Autofac을 사용할 때 일반적으로 모듈을 통해 형식을 등록하기 때문에, 애플리케이션 형식을 여러 클래스 라이브러리에 분산할 수 있듯이, 형식의 위치에 따라 여러 파일 간에 등록 형식을 분할할 수 있습니다.

예를 들어 다음은 삽입하려는 형식이 있는 [Ordering.API Web API](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/Services/Ordering/Ordering.API) 프로젝트의 [Autofac 애플리케이션 모듈](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Infrastructure/AutofacModules/ApplicationModule.cs)입니다.

```csharp
public class ApplicationModule : Autofac.Module
{
    public string QueriesConnectionString { get; }
    public ApplicationModule(string qconstr)
    {
        QueriesConnectionString = qconstr;
    }

    protected override void Load(ContainerBuilder builder)
    {
        builder.Register(c => new OrderQueries(QueriesConnectionString))
            .As<IOrderQueries>()
            .InstancePerLifetimeScope();
        builder.RegisterType<BuyerRepository>()
            .As<IBuyerRepository>()
            .InstancePerLifetimeScope();
        builder.RegisterType<OrderRepository>()
            .As<IOrderRepository>()
            .InstancePerLifetimeScope();
        builder.RegisterType<RequestManager>()
            .As<IRequestManager>()
            .InstancePerLifetimeScope();
   }
}
```

Autofac에는 [이름 규칙에 따라 어셈블리 및 등록 형식 검사](https://autofac.readthedocs.io/en/latest/register/scanning.html)에 대한 기능도 있습니다.

등록 프로세스와 개념은 내장 ASP.NET Core IoC 컨테이너로 형식을 등록하는 방식과 매우 유사하지만 Autofac을 사용하는 경우에는 구문이 조금 다릅니다.

예제 코드에서 추상화 IOrderRepository는 구현 클래스 OrderRepository와 함께 등록됩니다. 즉, 생성자가 IOrderRepository 추상화 또는 인터페이스를 통해 종속성을 선언할 때마다 IoC 컨테이너는 OrderRepository 클래스의 인스턴스를 주입합니다.

인스턴스 범위 형식은 동일한 서비스 또는 종속성에 대한 요청 사이에 인스턴스가 공유되는 방식을 결정합니다. 종속성에 대한 요청이 있을 때 IoC 컨테이너는 다음을 반환할 수 있습니다.

- 수명 범위당 단일 인스턴스(ASP.NET Core IoC 컨테이너에 *scoped*(범위 지정됨)라고 참조됨)

- 종속성당 새 인스턴스 하나(ASP.NET Core IoC 컨테이너에 *transient*(일시적 )라고 참조됨)

- IoC 컨테이너를 사용하는 모든 개체에서 공유되는 단일 인스턴스(ASP.NET Core IoC 컨테이너에 *singleton*(단일)으로 참조됨)

#### <a name="additional-resources"></a>추가 자료

- **ASP.NET Core에서 종속성 주입 소개** \
  [https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection](/aspnet/core/fundamentals/dependency-injection)

- **Autofac.** 공식 문서. \
  <https://docs.autofac.org/en/latest/>

- **ASP.NET Core IoC 컨테이너 서비스 수명과 Autofac IoC 컨테이너 인스턴스 범위 비교 - Cesar de la Torre.** \
  <https://devblogs.microsoft.com/cesardelatorre/comparing-asp-net-core-ioc-service-life-times-and-autofac-ioc-instance-scopes/>

## <a name="implement-the-command-and-command-handler-patterns"></a>명령 및 명령 처리기 패턴 구현

이전 섹션의 DI-through-constructor(생성자를 통한 DI) 예제에서 IoC 컨테이너는 클래스의 생성자를 통해 리포지토리를 주입했습니다. 그렇다면 정확이 어디에 주입했습니까? 간단한 Web API(예: eShopOnContainers의 카탈로그 마이크로 서비스)에서는 ASP.NET Core의 요청 파이프라인의 일부로 컨트롤러 생성자의 MVC 컨트롤러 수준에 주입합니다. 하지만 이 섹션의 초기 코드(eShopOnContainers의 Ordering.API 서비스에 있는 [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) 클래스)에서 종속성 주입은 특정 명령 처리기의 생성자를 통해 수행됩니다. 명령 처리기가 무엇인지 왜 사용해야 하는지에 대해 설명해 드리겠습니다.

명령 패턴은 이 가이드의 앞부분에 소개된 CQRS 패턴과 본질적으로 관련이 있습니다. CQRS에는 두 가지 측면이 있습니다. 첫 번째 영역은 앞에서 설명한 [Dapper](https://github.com/StackExchange/dapper-dot-net) 마이크로 ORM으로 간단한 쿼리를 사용하는 쿼리입니다. 두 번째 영역은 트랜잭션의 시작점인 명령과 서비스 외부의 입력 채널입니다.

그림 7-24에서 볼 수 있듯이, 패턴은 클라이언트 쪽의 명령을 수락하고, 이 명령을 도메인 모델 규칙에 따라 처리하고, 마지막으로 트랜잭션으로 상태를 유지하는 것을 기반으로 합니다.

![CQRS의 쓰기 쪽에 대한 상위 수준 보기: UI 앱은 도메인 모델 및 데이터베이스를 업데이트할 인프라에 따라 달라지는 CommandHandler를 가져오는 API를 통해 명령을 보냅니다.](./media/image21.png)

**그림 7-24**. CQRS 패턴의 명령 또는 "트랜잭션 쪽"에 대한 개괄적인 보기

### <a name="the-command-class"></a>명령 클래스

명령은 시스템의 상태를 변경하는 동작을 수행하도록 시스템에 보내는 요청입니다. 명령은 반드시 수행해야 하고 한 번만 처리해야 합니다.

명령은 반드시 수행해야 하기 때문에 일반적으로 명령형 동사(예: "create" 또는 "update")를 사용하여 이름을 지정하며 CreateOrderCommand와 같은 집합체 형식을 포함할 수 있습니다. 이벤트와 달리 명령은 과거의 팩트가 아니며 요청이기 때문에 거부될 수 있습니다.

명령은 사용자가 요청을 시작한 결과로 UI로부터 생성되거나 프로세스 관리자가 동작을 수행하기 위해 집계를 지시할 때 프로세스 관리자로부터 생성될 수 있습니다.

명령의 중요한 특징은 단일 수신자에 의해 한 번만 처리되어야 한다는 점입니다. 명령은 애플리케이션에서 수행하려는 단일 동작 또는 트랜잭션이기 때문입니다. 예를 들어, 동일한 주문 생성 명령이 두 번 이상 처리되지 말아야 합니다. 이 점이 명령과 이벤트의 중요한 차이점입니다. 이벤트는 여러 번 처리될 수 있으며, 이것은 다수의 시스템 또는 마이크로 서비스가 이벤트에 관심을 가질 수 있기 때문입니다.

또한 명령이 idempotent가 아닌 경우 명령은 한 번만 처리되는 것이 중요합니다. 명령의 특성으로 인해 또는 시스템에서 명령을 처리하는 방식으로 인해 결과를 변경하지 않고 여러 번 실행할 수 있는 명령은 idempotent 입니다.

도메인의 비즈니스 규칙 및 불변성에 적합한 경우 명령과 업데이트를 idempotent로 만드는 것이 좋습니다. 예를 들어, 동일한 예제를 사용하기 위해, 어떤 이유로든(다시 시도 논리, 해킹 등) 동일한 CreateOrder 명령이 시스템에 여러 번 도달하면, 이것을 식별하고 주문이 여러 건 생성되지 않도록 해야 합니다. 이렇게 하려면 작업에 일종의 ID를 첨부하여 명령이나 업데이트가 이미 처리되었는지 식별해야 합니다.

명령은 단일 수신자에게 보내는 것이며 게시하는 것이 아닙니다. 게시는 무언가가 발생했고 이벤트 수신기가 관심을 가질 수 있다는 팩트를 설명하는 이벤트를 위한 것입니다. 이벤트의 경우, 게시자는 어떤 수신자가 이벤트를 받았는지, 또는 무엇을 하는지에 대해 아무 관심이 없습니다. 하지만 도메인 또는 통합 이벤트는 이전 섹션에서 이미 소개한 내용과 다릅니다.

명령은 명령을 실행하는 데 필요한 모든 정보가 있는 데이터 필드나 컬렉션이 포함된 클래스로 구현됩니다. 명령은 변경이나 트랜잭션을 요청하는 데 명확히 사용되는 특별한 종류의 DTO(데이터 전송 개체)입니다. 명령 자체는 명령 처리에 필요한 정확한 정보만을 기반으로 합니다.

다음 예제는 간소화된 `CreateOrderCommand` 클래스를 보여줍니다. eShopOnContainers의 Ordering(주문) 마이크로 서비스에 사용되는 변경할 수 없는 명령입니다.

```csharp
// DDD and CQRS patterns comment
// Note that we recommend that you implement immutable commands
// In this case, immutability is achieved by having all the setters as private
// plus being able to update the data just once, when creating the object
// through the constructor.
// References on immutable commands:
// http://cqrs.nu/Faq
// https://docs.spine3.org/motivation/immutability.html
// http://blog.gauffin.org/2012/06/griffin-container-introducing-command-support/
// https://docs.microsoft.com/dotnet/csharp/programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties
[DataContract]
public class CreateOrderCommand
    :IAsyncRequest<bool>
{
    [DataMember]
    private readonly List<OrderItemDTO> _orderItems;
    [DataMember]
    public string City { get; private set; }
    [DataMember]
    public string Street { get; private set; }
    [DataMember]
    public string State { get; private set; }
    [DataMember]
    public string Country { get; private set; }
    [DataMember]
    public string ZipCode { get; private set; }
    [DataMember]
    public string CardNumber { get; private set; }
    [DataMember]
    public string CardHolderName { get; private set; }
    [DataMember]
    public DateTime CardExpiration { get; private set; }
    [DataMember]
    public string CardSecurityNumber { get; private set; }
    [DataMember]
    public int CardTypeId { get; private set; }
    [DataMember]
    public IEnumerable<OrderItemDTO> OrderItems => _orderItems;

    public CreateOrderCommand()
    {
        _orderItems = new List<OrderItemDTO>();
    }

    public CreateOrderCommand(List<BasketItem> basketItems, string city,
        string street,
        string state, string country, string zipcode,
        string cardNumber, string cardHolderName, DateTime cardExpiration,
        string cardSecurityNumber, int cardTypeId) : this()
    {
        _orderItems = MapToOrderItems(basketItems);
        City = city;
        Street = street;
        State = state;
        Country = country;
        ZipCode = zipcode;
        CardNumber = cardNumber;
        CardHolderName = cardHolderName;
        CardSecurityNumber = cardSecurityNumber;
        CardTypeId = cardTypeId;
        CardExpiration = cardExpiration;
    }

    public class OrderItemDTO
    {
        public int ProductId { get; set; }
        public string ProductName { get; set; }
        public decimal UnitPrice { get; set; }
        public decimal Discount { get; set; }
        public int Units { get; set; }
        public string PictureUrl { get; set; }
    }
}
```

기본적으로 명령 클래스에는 도메인 모델 개체를 사용하여 비즈니스 트랜잭션을 수행하는 데 필요한 모든 데이터가 포함됩니다. 따라서 명령은 읽기 전용 데이터가 포함되고 동작은 포함되지 않은 데이터 구조일 뿐입니다. 명령의 이름은 용도를 나타냅니다. C#과 같은 많은 언어에서 명령은 클래스로 표현되지만 실제 개체 지향적 의미에서는 진정한 클래스가 아닙니다.

명령의 추가적인 특징은 변경할 수 없다는 점입니다. 예상되는 사용법이 도메인 모델에 의해 직접 처리되기 때문입니다. 예상된 수명 내에 변경할 필요가 없습니다. C# 클래스에서 불변성은 setter 또는 내부 상태를 변경하는 다른 메서드를 두지 않는 방식으로 달성할 수 있습니다.

명령이 직렬화/역 직렬화 프로세스를 수행하는 것을 의도하거나 기대한다면 속성에는 전용 setter와 `[DataMember]`(또는 `[JsonProperty]`) 특성이 있어야 하며, 그렇지 않으면 deserializer는 필요한 값을 사용하여 대상에 개체를 다시 구성할 수 없습니다.

예를 들어 주문 생성을 위한 명령 클래스가 데이터 측면에서는 생성하려는 주문과 유사할 수 있지만 동일한 특성이 필요하지 않을 수도 있습니다. 예를 들어 `CreateOrderCommand`에는 주문 ID가 없는데, 이것은 주문이 아직 생성되지 않았기 때문입니다.

많은 명령 클래스는 간단하며, 변경이 필요한 상태에 대해 몇 개의 필드만 필요할 수 있습니다. 이런 경우는 다음과 유사한 명령을 사용하여 주문의 상태를 "처리 중"에서 "지불됨" 또는 "배송됨"으로 변경하는 경우가 될 수 있습니다.

```csharp
[DataContract]
public class UpdateOrderStatusCommand
    :IAsyncRequest<bool>
{
    [DataMember]
    public string Status { get; private set; }

    [DataMember]
    public string OrderId { get; private set; }

    [DataMember]
    public string BuyerIdentityGuid { get; private set; }
}
```

일부 개발자는 UI 요청 개체를 명령 DTO와 별도로 만들지만 이것은 취향에 따라 달라질 수 있습니다. 이러한 분리는 부가 가치가 별로 없는 번거로운 작업이며 개체의 모양은 거의 정확히 동일합니다. 예를 들어, eShopOnContainers에서 일부 명령은 클라이언트 쪽에서 직접 제공됩니다.

### <a name="the-command-handler-class"></a>명령 처리기 클래스

각 명령에 대해 특정 명령 처리기 클래스를 구현해야 합니다. 이런 식으로 패턴이 작동하며 여기에 명령 개체, 도메인 개체 및 인프라 리포지토리 개체를 사용합니다. 명령 처리기는 실제로 CQRS와 DDD 측면에서 애플리케이션 계층의 핵심입니다. 하지만 모든 도메인 논리는 도메인 클래스 내에 포함되어야 합니다. 집계 루트(루트 엔터티), 자식 엔터티 또는 [도메인 서비스](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/) 내에 포함되어야 하지만 애플리케이션 계층의 클래스인 명령 처리기 내에 포함되지 말아야 합니다.

명령 처리기 클래스는 이전 섹션에서 언급한 SRP(단일 책임 원칙)를 달성하기 위한 강력한 발판을 제공합니다.

명령 처리기는 명령을 수신하고 사용된 집계로부터 결과를 가져옵니다. 결과는 명령 실행 성공 또는 예외가 되어야 합니다. 예외의 경우 시스템 상태가 변경되지 않아야 합니다.

명령 처리기는 일반적으로 다음 단계를 수행합니다.

- DTO와 같은 명령 개체를 수신합니다([중재자](https://en.wikipedia.org/wiki/Mediator_pattern)(mediator) 또는 기타 인프라 개체로부터).

- 명령이 유효한지 검사합니다(중재자(mediator)가 유효성을 검사하지 않은 경우).

- 현재 명령의 대상인 집계 루트 인스턴스를 인스턴스화합니다.

- 집계 루트 인스턴스에서 메서드를 실행하여 명령으로부터 필요한 데이터를 가져옵니다.

- 집계의 새로운 상태를 관련 데이터베이스에 유지합니다. 이 마지막 작업이 실제 트랜잭션입니다.

일반적으로 명령 처리기는 집계 루트(루트 엔터티)에서 발생한 단일 집계를 처리합니다. 단일 명령을 수신하여 여러 집합체가 영향을 받는 경우에는 도메인 이벤트를 사용하여 여러 집합체에 상태나 동작을 전파할 수 있습니다.

여기서 중요한 점은, 명령이 처리될 때 모든 도메인 논리는 완전히 캡슐화되고 유닛 테스트 준비가 된 도메인 모델(집합체) 내에 있어야 한다는 점입니다. 명령 처리기는 데이터베이스로부터 도메인 모델을 가져오는 방법으로만 사용되며, 마지막 단계에서는 모델이 변경될 때 인프라 계층(리포지토리)에 변경 내용을 유지하도록 알려주는 방법으로 사용됩니다. 이런 방식의 장점은 배관 수준(명령 처리가, Web API, 리포지토리 등)인 애플리케이션이나 인프라 계층의 코드를 변경하지 않고도 격리되고 완전히 캡슐화된 풍부한 동작 도메인 모델에서 도메인 논리를 리팩터링할 수 있다는 점입니다.

논리가 너무 많아져서 명령 처리기가 너무 복잡해지면 코드 냄새가 될 수 있습니다. 검토 후 도메인 논리를 찾으면 코드를 리팩터링하여 해당 도메인 동작을 도메인 개체의 메서드(집계 루트 및 자식 엔터티)로 이동합니다.

명령 처리기 클래스의 예인 다음 코드는 이 장의 시작 부분에 표시된 것과 동일한 `CreateOrderCommandHandler` 클래스입니다. 이 경우 도메인 모델 개체/집합체를 사용하는 작업과 Handle 메서드에 중점을 두겠습니다.

```csharp
public class CreateOrderCommandHandler
    : IAsyncRequestHandler<CreateOrderCommand, bool>
{
    private readonly IOrderRepository _orderRepository;
    private readonly IIdentityService _identityService;
    private readonly IMediator _mediator;

    // Using DI to inject infrastructure persistence Repositories
    public CreateOrderCommandHandler(IMediator mediator,
                                     IOrderRepository orderRepository,
                                     IIdentityService identityService)
    {
        _orderRepository = orderRepository ??
                          throw new ArgumentNullException(nameof(orderRepository));
        _identityService = identityService ??
                          throw new ArgumentNullException(nameof(identityService));
        _mediator = mediator ??
                                 throw new ArgumentNullException(nameof(mediator));
    }

    public async Task<bool> Handle(CreateOrderCommand message)
    {
        // Create the Order AggregateRoot
        // Add child entities and value objects through the Order aggregate root
        // methods and constructor so validations, invariants, and business logic
        // make sure that consistency is preserved across the whole aggregate
        var address = new Address(message.Street, message.City, message.State,
                                  message.Country, message.ZipCode);
        var order = new Order(message.UserId, address, message.CardTypeId,
                              message.CardNumber, message.CardSecurityNumber,
                              message.CardHolderName, message.CardExpiration);

        foreach (var item in message.OrderItems)
        {
            order.AddOrderItem(item.ProductId, item.ProductName, item.UnitPrice,
                               item.Discount, item.PictureUrl, item.Units);
        }

        _orderRepository.Add(order);

        return await _orderRepository.UnitOfWork
            .SaveEntitiesAsync();
    }
}
```

다음은 명령 처리기에서 수행해야 하는 추가 단계입니다.

- 명령의 데이터를 사용하여 집계 루트의 메서드 및 동작을 작동시킵니다.

- 내부적으로 도메인 개체 내에서, 트랜잭션이 실행되는 동안 도메인 이벤트를 발생시키지만 명령 처리기 관점에서 볼 때 투명합니다.

- 집계의 작업 결과가 성공적이면 트랜잭션이 완료된 후 통합 이벤트를 발생시킵니다. (리포지토리와 같은 인프라 클래스를 통해 발생시킬 수도 있습니다.)

#### <a name="additional-resources"></a>추가 자료

- **Mark Seemann. 경계에서 애플리케이션은 개체 지향적이지 않음** \
  <https://blog.ploeh.dk/2011/05/31/AttheBoundaries,ApplicationsareNotObject-Oriented/>

- **명령 및 이벤트** \
  <http://cqrs.nu/Faq/commands-and-events>

- **명령 처리기는 무엇을 수행하나요?** \
  <http://cqrs.nu/Faq/command-handlers>

- **Jimmy Bogard. 도메인 명령 패턴 - 처리기** \
  <https://jimmybogard.com/domain-command-patterns-handlers/>

- **Jimmy Bogard. 도메인 명령 패턴 - 유효성 검사** \
  <https://jimmybogard.com/domain-command-patterns-validation/>

## <a name="the-command-process-pipeline-how-to-trigger-a-command-handler"></a>명령 프로세스 파이프라인: 명령 처리기를 트리거하는 방법

다음 질문은 명령 처리기를 호출하는 방법입니다. 각각의 관련된 ASP.NET Core 컨트롤러에서 수동으로 호출할 수 있습니다. 하지만 이런 방식은 연결이 너무 많아서 이상적이지 않습니다.

권장되는 다른 두 가지 주요 옵션은 다음과 같습니다.

- 메모리 내 중재자(mediator) 패턴 아티팩트를 통해

- 컨트롤러와 처리기 사이에 비동기 메시지 큐를 통해

### <a name="use-the-mediator-pattern-in-memory-in-the-command-pipeline"></a>명령 파이프라인에 중재자 패턴(메모리 내) 사용

그림 7-25에서 볼 수 있듯이 CQRS 방식에서는 메모리 내 버스와 유사한 지능형 중재자(mediator)를 사용하며, 수신되는 명령 또는 DTO의 형식을 기반으로 올바른 명령 처리기로 리디렉션할만큼 스마트합니다. 구성 요소 사이의 검은색 화살표는 관련 상호 작용이 있는 개체(많은 경우에 DI를 통해 주입됨) 간의 종속성을 나타냅니다.

![이전 이미지에서 확대/축소: ASP.NET Core 컨트롤러는 MediatR의 명령 파이프라인에 명령을 전송하여 적절한 처리기로 보냅니다.](./media/image22.png)

**그림 7-25**. 단일 CQRS 마이크로 서비스의 프로세스에 중재자(Mediator) 패턴 사용

중재자(Mediator) 패턴을 사용하는 것이 타당한 이유는 엔터프라이즈 애플리케이션에서 처리 요청이 복잡해질 수 있기 때문입니다. 로깅, 유효성 검사, 감사 및 보안과 같은 여러 가지 교차 편집 문제를 추가하는 것이 필요할 수 있습니다. 이런 경우 중재자(mediator) 파이프라인([중재자(Mediator) 패턴](https://en.wikipedia.org/wiki/Mediator_pattern) 참조)에 의존하여 이러한 추가 동작이나 교차 편집 문제를 위한 수단을 제공할 수 있습니다.

중재자(mediator)는 프로세스의 “방식(how)”을 캡슐화하는 개체입니다. 상태, 명령 처리기가 호출되는 방식 또는 처리기에 제공하는 페이로드를 기반으로 실행을 조정합니다. 중재자(mediator) 구성 요소를 사용하면 데코레이터(또는 [MediatR 3](https://www.nuget.org/packages/MediatR/3.0.0) 이후의 [파이프라인 동작](https://github.com/jbogard/MediatR/wiki/Behaviors))를 적용하여 중앙 집중식으로 투명하게 교차 편집 문제를 적용할 수 있습니다. 자세한 내용은 [데코레이터(decorator) 패턴](https://en.wikipedia.org/wiki/Decorator_pattern)을 참조하세요.

데코레이터(decorator)와 동작은 AOP([Aspect Oriented Programming](https://en.wikipedia.org/wiki/Aspect-oriented_programming))와 유사하며 중재자(mediator) 구성 요소가 관리하는 특정 프로세스 파이프라인에만 적용됩니다. 교차 편집 문제를 구현하는 AOP의 측면은 컴파일 시간에 주입된 *관점 생성기(aspect weaver)* 또는 개체 호출 인터셉션을 기반으로 적용됩니다. 일반적인 APO 방식은 AOP가 해당 작업을 어떻게 수행하는지 보기가 쉽지 않기 때문에 "마술처럼" 작동한다고 말하기도 합니다. 심각한 문제나 버그를 처리할 때 AOP는 디버그가 어려울 수 있습니다. 이러한 데코레이터/동작은 명시적이며 중재자(mediator)의 맥락에서만 적용되기 때문에 디버깅을 훨씬 더 쉽게 예측할 수 있습니다.

예를 들어 eShopOnContainers Ordering(주문) 마이크로 서비스에 [LogBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) 클래스 및 [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) 클래스라는 두 가지 샘플 동작을 구현했습니다. 동작의 구현은 eShopOnContainers가 [MediatR 3](https://www.nuget.org/packages/MediatR/3.0.0) [동작](https://github.com/jbogard/MediatR/wiki/Behaviors)을 사용하는 방법을 보여줌으로써 다음 섹션에 설명되어 있습니다.

### <a name="use-message-queues-out-of-proc-in-the-commands-pipeline"></a>명령의 파이프라인에서 메시지 큐(out-of-proc) 사용

또 다른 옵션은 그림 7-26과 같이 broker 또는 메시지 큐를 기반으로 비동기 메시지를 사용하는 것입니다. 이 옵션은 명령 처리기 바로 전에 중재자(mediator) 구성 요소와 결합될 수도 있습니다.

![명령의 파이프라인은 고가용성 메시지 큐에 의해 처리되어 명령을 해당 처리기로 전달할 수도 있습니다.](./media/image23.png)

**그림 7-26**. CQRS 명령으로 메시지 큐(프로세스 외부 및 프로세스 간 통신) 사용

메시지 큐를 사용하여 명령을 수락하면 명령의 파이프라인이 복잡해질 수 있습니다. 파이프라인을 외부 메시지 큐를 통해 연결된 두 개의 프로세스로 분할하는 것이 필요할 수 있기 때문입니다. 하지만 비동기 메시지를 기반으로 확장성과 성능을 향상시키려면 사용해야 합니다. 그림 7-26의 경우 컨트롤러는 명령 메시지를 큐에 게시만 하고 반환합니다. 그런 다음, 명령 처리기는 원하는 속도로 메시지를 처리합니다. 이것이 큐의 커다란 장점입니다. 주식 또는 송신 데이터가 대규모인 그 밖의 시나리오와 같이 엄청난 확장성이 필요한 경우에, 메시지 큐는 버퍼로 작동할 수 있습니다.

하지만 메시지 큐의 비동기적인 특성으로 인해, 명령 프로세스의 성공 또는 실패에 대해 클라이언트 애플리케이션과 통신할 방법을 알아내야 합니다. 원칙적으로 “fire and forget”명령은 절대 사용하지 말아야 합니다. 모든 비즈니스 애플리케이션은 명령이 성공적으로 처리되었는지 아니면 최소한 유효성이 검사되고 수락되었는지를 알아야 합니다.

따라서 비동기 큐에 제출된 명령 메시지의 유효성을 검사한 후 클라이언트에 응답할 수 있으려면 트랜잭션을 실행 한 후 작업 결과를 반환하는 in-process 명령 프로세스에 비해 시스템이 더 복잡해집니다. 큐를 사용하면 명령 프로세스의 결과를 다른 작업 결과 메시지를 통해 반환해야 할 수 있으며 이렇게 하려면 시스템에 추가 구성 요소 및 사용자 지정 통신이 필요합니다.

또한 비동기 명령은 단방향 명령이기 때문에 많은 경우에 필요하지 않으며, 이 내용은 [온라인 대화](https://groups.google.com/forum/#!msg/dddcqrs/xhJHVxDx2pM/WP9qP8ifYCwJ)에 있는 Burtsev Alexey와 Greg Young 사이의 다음과 같은 흥미로운 대화에 설명되어 있습니다.

> \[Burtsev Alexey\] 많은 코드에서 아무 이유 없이 비동기 코드 처리 또는 단방향 명령 메시지를 사용하는 경우를 봤습니다. (긴 작업을 수행하는 경우도, 외부 비동기 코드를 실행하는 경우도, 심지어 메시지 버스를 사용하기 위해 애플리케이션 경계를 넘는 경우도 아닙니다.) 이런 불필요한 복잡성을 적용하는 이유가 무엇인가요? 그리고 실제로 명령 처리기를 차단하는 CQRS 코드를 여태까지 본 적이 없습니다. 대부분의 경우 제대로 작동할 텐데도 말입니다.
>
> \[Greg Young\] \[...\] 비동기 명령은 존재하지 않으며 실제로는 또 다른 이벤트입니다. 상대방이 내게 보낸 것을 받아들이고 동의하지 않는 경우 이벤트를 발생시켜야 한다면, 더 이상 내게 무언가를 수행하라고 알려주는 것이 아닙니다. \[ 즉, 명령이 아닙니다\]. 수행이 완료되었다는 것을 알려 주는 것입니다. 처음엔 약간의 차이처럼 보이지만 여기에는 많은 내용이 함축되어 있습니다.

비동기 명령은 실패를 나타낼 간단한 방법이 없기 때문에 시스템의 복잡성을 크게 증가시킵니다. 따라서 크기 조정 요구 사항이 필요하거나 메시지를 통해 내부 마이크로 서비스를 통신하는 특수한 경우가 아니라면 비동기 명령은 사용하지 않는 것이 좋습니다. 이런 경우 장애에 대한 별도의 보고 및 복구 시스템을 설계해야 합니다.

eShopOnContainers의 초기 버전에서, HTTP 요청으로 시작하여 중재자(Mediator) 패턴에 의해 구동되는 동기 명령 처리를 사용하기로 결정했습니다. 이를 통해 프로세스의 성공 또는 실패를 [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) 구현에서처럼 쉽게 반환할 수 있습니다.

어떤 경우에서든, 이러한 결정은 애플리케이션 또는 마이크로 서비스의 비즈니스 요구 사항에 기반하여 내려져야 합니다.

## <a name="implement-the-command-process-pipeline-with-a-mediator-pattern-mediatr"></a>중재자 패턴(MediatR)으로 명령 프로세스 파이프라인 구현

샘플 구현인 이 가이드에서는 중재자(Mediator) 패턴을 기반으로 in-process 파이프라인을 사용하여 명령 수집을 유도하고 명령을 메모리 내에서 올바른 명령 처리기로 라우팅할 것을 제안합니다. 또한 이 가이드에서는 교차 편집 문제를 분리하기 위해 [동작](https://github.com/jbogard/MediatR/wiki/Behaviors) 적용을 제안합니다.

.NET Core의 구현에는 중재자(Mediator) 패턴을 구현하는 데 사용할 수 있는 여러 개의 오픈 소스 라이브러리가 있습니다. 이 가이드에 사용된 라이브러리는 [MediatR](https://github.com/jbogard/MediatR) 오픈 소스 라이브러리(작성자: Jimmy Bogard)이지만 다른 방식을 사용할 수도 있습니다. MediatR은 작고 간단한 라이브러리이며 명령과 같은 메모리 내 메시지를 처리하면서 데코레이터(decorator)나 동작을 적용할 수 있습니다.

Mediator 패턴을 사용하면 작업을 수행하는 처리기(이 경우 명령 처리기)에 자동으로 연결하면서 결합을 줄이고 요청된 작업의 문제를 격리시키는 데 도움이 됩니다.

Mediator 패턴을 사용하는 또 다른 좋은 이유는 이 가이드를 검토하면서 Jimmy Bogard가 다음과 같이 설명했습니다.

> 시스템 동작에 일관된 창을 제공하기 때문에 테스트를 언급하는 것이 유용하다고 생각합니다. 요청이 들어가고(Request-in), 응답이 나오는(response-out) 이러한 측면은 일관되게 동작하는 테스트를 구축하는 데 매우 유용했습니다.

먼저, 중재자(mediator) 개체를 실제로 사용할 샘플 WebAPI 컨트롤러를 살펴보겠습니다. 중재자(mediator) 개체를 사용하지 않는 경우에는 해당 컨트롤러에 대한 모든 종속성(예: 로거 개체 등)을 주입해야 합니다. 따라서 생성자가 매우 복잡합니다. 반면에 중재자(mediator) 개체를 사용하면, 교차 편집 작업당 종속성이 하나일 경우 다수의 종속성이 있지만 다음 예제와 같이 적은 수의 종속성만 있기 때문에 컨트롤러의 생성자는 훨씬 더 간단해 질 수 있습니다.

```csharp
public class MyMicroserviceController : Controller
{
    public MyMicroserviceController(IMediator mediator,
                                    IMyMicroserviceQueries microserviceQueries)
    {
        // ...
    }
}
```

중재자가 명확하고 간단한 Web API 컨트롤러 생성자를 제공하는 것을 볼 수 있습니다. 또한, 컨트롤러 메서드 내에서 중재자(mediator) 개체에 명령을 보내는 코드는 거의 한 줄입니다.

```csharp
[Route("new")]
[HttpPost]
public async Task<IActionResult> ExecuteBusinessOperation([FromBody]RunOpCommand
                                                               runOperationCommand)
{
    var commandResult = await _mediator.SendAsync(runOperationCommand);

    return commandResult ? (IActionResult)Ok() : (IActionResult)BadRequest();
}
```

### <a name="implement-idempotent-commands"></a>idempotent 명령 구현

**eShopOnContainers**에서는 위의 경우보다 고급 예제가 Ordering(주문) 마이크로 서비스에서 CreateOrderCommand 개체를 제출합니다. 하지만 Ordering 비즈니스 프로세스가 좀 더 복잡하고, 이 경우, 실제로는 Basket 마이크로 서비스에서 시작되기 때문에 CreateOrderCommand 개체를 제출하는 동작은 이전의 간단한 예제에서처럼 클라이언트 앱에서 호출되는 간단한 WebAPI 컨트롤러 대신 [UserCheckoutAcceptedIntegrationEventHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/IntegrationEvents/EventHandling/UserCheckoutAcceptedIntegrationEventHandler.cs)라는 통합 이벤트 처리기에서 수행됩니다.

그럼에도 불구하고 MediatR에 명령을 제출하는 동작은 다음 코드와 매우 유사합니다.

```csharp
var createOrderCommand = new CreateOrderCommand(eventMsg.Basket.Items,
                                                eventMsg.UserId, eventMsg.City,
                                                eventMsg.Street, eventMsg.State,
                                                eventMsg.Country, eventMsg.ZipCode,
                                                eventMsg.CardNumber,
                                                eventMsg.CardHolderName,
                                                eventMsg.CardExpiration,
                                                eventMsg.CardSecurityNumber,
                                                eventMsg.CardTypeId);

var requestCreateOrder = new IdentifiedCommand<CreateOrderCommand,bool>(createOrderCommand,
                                                                        eventMsg.RequestId);
result = await _mediator.Send(requestCreateOrder);
```

하지만 이 경우는 idempotent 명령도 구현하기 때문에 조금 더 고급입니다. CreateOrderCommand 프로세스는 idempotent여야 하기 때문에 동일한 메시지가 네트워크를 통해 중복되어 들어오면(재시도 등과 같은 이유로 인해) 동일한 비즈니스 명령은 한 번만 처리됩니다.

이러한 내용은 비즈니스 명령(이 경우 CreateOrderCommand)을 래핑하고, idempotent여야 하는 네트워크를 통해 들어오는 모든 메시지의 ID로 추적되는 제네릭 IdentifiedCommand에 포함하여 구현됩니다.

아래 코드에서 IdentifiedCommand는 ID와 래핑된 비즈니스 명령 개체가 있는 DTO에 불과하다는 것을 알 수 있습니다.

```csharp
public class IdentifiedCommand<T, R> : IRequest<R>
    where T : IRequest<R>
{
    public T Command { get; }
    public Guid Id { get; }
    public IdentifiedCommand(T command, Guid id)
    {
        Command = command;
        Id = id;
    }
}
```

[IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs)라는 IdentifiedCommand에 대한 CommandHandler는 메시지의 일부로 들어오는 ID가 이미 테이블에 있는지 기본적으로 확인합니다. 이미 존재하는 경우 해당 명령이 다시 처리되지 않기 때문에 idempotent 명령으로 작동합니다. 해당 인프라 코드는 아래 `_requestManager.ExistAsync` 메서드 호출에 의해 수행됩니다.

```csharp
// IdentifiedCommandHandler.cs
public class IdentifiedCommandHandler<T, R> :
                                   IAsyncRequestHandler<IdentifiedCommand<T, R>, R>
                                   where T : IRequest<R>
{
    private readonly IMediator _mediator;
    private readonly IRequestManager _requestManager;

    public IdentifiedCommandHandler(IMediator mediator,
                                    IRequestManager requestManager)
    {
        _mediator = mediator;
        _requestManager = requestManager;
    }

    protected virtual R CreateResultForDuplicateRequest()
    {
        return default(R);
    }

    public async Task<R> Handle(IdentifiedCommand<T, R> message)
    {
        var alreadyExists = await _requestManager.ExistAsync(message.Id);
        if (alreadyExists)
        {
            return CreateResultForDuplicateRequest();
        }
        else
        {
            await _requestManager.CreateRequestForCommandAsync<T>(message.Id);

            // Send the embedded business command to mediator
            // so it runs its related CommandHandler
            var result = await _mediator.Send(message.Command);

            return result;
        }
    }
}
```

IdentifiedCommand는 비즈니스 명령의 봉투(Envelope)처럼 작동하기 때문에 반복된 ID가 아니라서 비즈니스 명령을 처리해야 하는 경우에는, [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs)에서 `_mediator.Send(message.Command)`를 실행할 때 위에 표시된 코드의 마지막 부분처럼 내부 비즈니스 명령을 가져다가 중재자(Mediator)에 다시 제출합니다.

그렇게 하면 이 경우 다음 코드와 같이 Ordering 데이터베이스에 대해 트랜잭션을 실행하는 [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) 비즈니스 명령 처리기를 연결하고 실행합니다.

```csharp
// CreateOrderCommandHandler.cs
public class CreateOrderCommandHandler
                                   : IAsyncRequestHandler<CreateOrderCommand, bool>
{
    private readonly IOrderRepository _orderRepository;
    private readonly IIdentityService _identityService;
    private readonly IMediator _mediator;

    // Using DI to inject infrastructure persistence Repositories
    public CreateOrderCommandHandler(IMediator mediator,
                                     IOrderRepository orderRepository,
                                     IIdentityService identityService)
    {
        _orderRepository = orderRepository ??
                          throw new ArgumentNullException(nameof(orderRepository));
        _identityService = identityService ??
                          throw new ArgumentNullException(nameof(identityService));
        _mediator = mediator ??
                                 throw new ArgumentNullException(nameof(mediator));
    }

    public async Task<bool> Handle(CreateOrderCommand message)
    {
        // Add/Update the Buyer AggregateRoot
        var address = new Address(message.Street, message.City, message.State,
                                  message.Country, message.ZipCode);
        var order = new Order(message.UserId, address, message.CardTypeId,
                              message.CardNumber, message.CardSecurityNumber,
                              message.CardHolderName, message.CardExpiration);

        foreach (var item in message.OrderItems)
        {
            order.AddOrderItem(item.ProductId, item.ProductName, item.UnitPrice,
                               item.Discount, item.PictureUrl, item.Units);
        }

        _orderRepository.Add(order);

        return await _orderRepository.UnitOfWork
            .SaveEntitiesAsync();
    }
}
```

### <a name="register-the-types-used-by-mediatr"></a>MediatR에서 사용하는 형식 등록

MediatR에서 명령 처리기 클래스를 인식하려면 IoC 컨테이너에 중재자(mediator) 클래스와 명령 처리기 클래스를 등록해야 합니다. 기본적으로 MediatR은 Autofac을 IoC 컨테이너로 사용하지만 내장 ASP.NET Core IoC 컨테이너 또는 MediatR에서 지원하는 다른 컨테이너를 사용할 수도 있습니다.

다음 코드는 Autofac 모듈을 사용할 때 중재자(Mediator) 형식 및 명령을 등록하는 방법을 보여줍니다.

```csharp
public class MediatorModule : Autofac.Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterAssemblyTypes(typeof(IMediator).GetTypeInfo().Assembly)
            .AsImplementedInterfaces();

        // Register all the Command classes (they implement IAsyncRequestHandler)
        // in assembly holding the Commands
        builder.RegisterAssemblyTypes(
                              typeof(CreateOrderCommand).GetTypeInfo().Assembly).
                                   AsClosedTypesOf(typeof(IAsyncRequestHandler<,>));
        // Other types registration
        //...
    }
}
```

여기가 MediatR로 "마술이 일어나는 곳"입니다.

각 명령 처리기는 제네릭 `IAsyncRequestHandler<T>` 인터페이스를 구현하기 때문에 어셈블리를 등록할 때 코드는 다음 예제와 같이 `CommandHandler` 클래스에 명시된 관계 덕분에 `CommandHandlers`를 해당 `Commands`와 연결하는 동안 `IAsyncRequestHandler`으로 표시된 모든 유형을 `RegisteredAssemblyTypes`에 등록합니다.

```csharp
public class CreateOrderCommandHandler
  : IAsyncRequestHandler<CreateOrderCommand, bool>
{
```

이것이 명령을 명령 처리기와 연관시키는 코드입니다. 처리기는 단지 간단한 클래스이지만 `RequestHandler<T>`에서 상속받습니다. 여기서 T는 명령 유형이며 MediatR은 올바른 페이로드(명령)로 호출되는지 확인합니다.

## <a name="apply-cross-cutting-concerns-when-processing-commands-with-the-behaviors-in-mediatr"></a>MediatR의 동작을 사용하여 명령을 처리하는 경우 교차 편집 문제 적용

한 가지가 더 있습니다. 중재자(mediator) 파이프라인에 교차 편집 문제를 적용할 수 있습니다. Autofac 등록 모듈 코드의 끝에서 동작 형식, 특히 LoggingBehavior 클래스 및 ValidatorBehavior 클래스를 어떻게 등록하는지 볼 수도 있습니다. 하지만 다른 사용자 지정 동작도 추가할 수 있습니다.

```csharp
public class MediatorModule : Autofac.Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterAssemblyTypes(typeof(IMediator).GetTypeInfo().Assembly)
            .AsImplementedInterfaces();

        // Register all the Command classes (they implement IAsyncRequestHandler)
        // in assembly holding the Commands
        builder.RegisterAssemblyTypes(
                              typeof(CreateOrderCommand).GetTypeInfo().Assembly).
                                   AsClosedTypesOf(typeof(IAsyncRequestHandler<,>));
        // Other types registration
        //...
        builder.RegisterGeneric(typeof(LoggingBehavior<,>)).
                                                   As(typeof(IPipelineBehavior<,>));
        builder.RegisterGeneric(typeof(ValidatorBehavior<,>)).
                                                   As(typeof(IPipelineBehavior<,>));
    }
}
```

[LoggingBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) 클래스는 다음 코드로 구현될 수 있으며, 실행 중인 명령 처리기 및 성공 여부에 대한 정보를 기록합니다.

```csharp
public class LoggingBehavior<TRequest, TResponse>
         : IPipelineBehavior<TRequest, TResponse>
{
    private readonly ILogger<LoggingBehavior<TRequest, TResponse>> _logger;
    public LoggingBehavior(ILogger<LoggingBehavior<TRequest, TResponse>> logger) =>
                                                                  _logger = logger;

    public async Task<TResponse> Handle(TRequest request,
                                        RequestHandlerDelegate<TResponse> next)
    {
        _logger.LogInformation($"Handling {typeof(TRequest).Name}");
        var response = await next();
        _logger.LogInformation($"Handled {typeof(TResponse).Name}");
        return response;
    }
}
```

이 동작 클래스를 구현하고 파이프라인(위의 MediatorModule에서)에 등록하는 것만으로 MediatR을 통해 처리되는 모든 명령은 실행에 대한 정보를 로깅합니다.

eShopOnContainers Ordering(주문) 마이크로 서비스는 기본 유효성 검사의 두 번째 동작도 적용하며 이것은 다음 코드와 같이 [FluentValidation](https://github.com/JeremySkinner/FluentValidation) 라이브러리에 의존하는 [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) 클래스입니다.

```csharp
public class ValidatorBehavior<TRequest, TResponse>
         : IPipelineBehavior<TRequest, TResponse>
{
    private readonly IValidator<TRequest>[] _validators;
    public ValidatorBehavior(IValidator<TRequest>[] validators) =>
                                                         _validators = validators;

    public async Task<TResponse> Handle(TRequest request,
                                        RequestHandlerDelegate<TResponse> next)
    {
        var failures = _validators
            .Select(v => v.Validate(request))
            .SelectMany(result => result.Errors)
            .Where(error => error != null)
            .ToList();

        if (failures.Any())
        {
            throw new OrderingDomainException(
                $"Command Validation Errors for type {typeof(TRequest).Name}",
                        new ValidationException("Validation exception", failures));
        }

        var response = await next();
        return response;
    }
}
```

여기서 동작은 유효성 검사가 실패할 경우 예외를 발생시키지만, 성공한 경우에는 명령 결과를, 그렇지 않으면 유효성 검사 메시지가 포함된 결과 개체를 반환할 수도 있습니다. 이렇게 하면 사용자에게 유효성 검사 결과를 더 쉽게 표시할 수 있습니다.

그런 다음, [FluentValidation](https://github.com/JeremySkinner/FluentValidation) 라이브러리를 기반으로 다음 코드와 같이 CreateOrderCommand와 함께 전달된 데이터에 대한 유효성 검사를 생성했습니다.

```csharp
public class CreateOrderCommandValidator : AbstractValidator<CreateOrderCommand>
{
    public CreateOrderCommandValidator()
    {
        RuleFor(command => command.City).NotEmpty();
        RuleFor(command => command.Street).NotEmpty();
        RuleFor(command => command.State).NotEmpty();
        RuleFor(command => command.Country).NotEmpty();
        RuleFor(command => command.ZipCode).NotEmpty();
        RuleFor(command => command.CardNumber).NotEmpty().Length(12, 19);
        RuleFor(command => command.CardHolderName).NotEmpty();
        RuleFor(command => command.CardExpiration).NotEmpty().Must(BeValidExpirationDate).WithMessage("Please specify a valid card expiration date");
        RuleFor(command => command.CardSecurityNumber).NotEmpty().Length(3);
        RuleFor(command => command.CardTypeId).NotEmpty();
        RuleFor(command => command.OrderItems).Must(ContainOrderItems).WithMessage("No order items found");
    }

    private bool BeValidExpirationDate(DateTime dateTime)
    {
        return dateTime >= DateTime.UtcNow;
    }

    private bool ContainOrderItems(IEnumerable<OrderItemDTO> orderItems)
    {
        return orderItems.Any();
    }
}

```

추가 유효성 검사를 만들 수 있습니다. 이것은 명령 유효성 검사를 구현하는 매우 명확하고 세련된 방법입니다.

유사한 방식으로, 명령을 처리할 때 명령에 적용할 추가적인 측면이나 교차 편집 문제에 다른 동작은 구현할 수 있습니다.

#### <a name="additional-resources"></a>추가 자료

##### <a name="the-mediator-pattern"></a>중재자(mediator) 패턴

- **중재자(mediator) 패턴** \
  [https://en.wikipedia.org/wiki/Mediator\_pattern](https://en.wikipedia.org/wiki/Mediator_pattern)

##### <a name="the-decorator-pattern"></a>데코레이터(decorator) 패턴

- **데코레이터(decorator) 패턴** \
  [https://en.wikipedia.org/wiki/Decorator\_pattern](https://en.wikipedia.org/wiki/Decorator_pattern)

##### <a name="mediatr-jimmy-bogard"></a>MediatR(Jimmy Bogard)

- **MediatR.** GitHub 리포지토리. \
  <https://github.com/jbogard/MediatR>

- **MediatR 및 AutoMapper를 포함한 CQRS** \
  <https://lostechies.com/jimmybogard/2015/05/05/cqrs-with-mediatr-and-automapper/>

- **다이어트에 컨트롤러 넣기: POST 및 명령.** \
  <https://lostechies.com/jimmybogard/2013/12/19/put-your-controllers-on-a-diet-posts-and-commands/>

- **중재자(mediator) 파이프라인으로 교차 편집 문제 해결** \
  <https://lostechies.com/jimmybogard/2014/09/09/tackling-cross-cutting-concerns-with-a-mediator-pipeline/>

- **CQRS 및 REST: 완벽한 일치 항목** \
  <https://lostechies.com/jimmybogard/2016/06/01/cqrs-and-rest-the-perfect-match/>

- **MediatR 파이프라인 예제** \
  <https://lostechies.com/jimmybogard/2016/10/13/mediatr-pipeline-examples/>

- **MediatR 및 ASP.NET Core에 대한 수직 조각 테스트 설비** \
  <https://lostechies.com/jimmybogard/2016/10/24/vertical-slice-test-fixtures-for-mediatr-and-asp-net-core/>

- **Microsoft 종속성 주입에 대한 MediatR 확장이 릴리스됨** \
  <https://lostechies.com/jimmybogard/2016/07/19/mediatr-extensions-for-microsoft-dependency-injection-released/>

##### <a name="fluent-validation"></a>Fluent validation

- **Jeremy Skinner. FluentValidation.** GitHub 리포지토리. \
  <https://github.com/JeremySkinner/FluentValidation>

> [!div class="step-by-step"]
> [이전](microservice-application-layer-web-api-design.md)
> [다음](../implement-resilient-applications/index.md)
