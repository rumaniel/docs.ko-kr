---
title: 단순 데이터 기반 CRUD 마이크로 서비스 만들기
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | 마이크로 서비스 애플리케이션의 컨텍스트 내에서 단순 CRUD(데이터 기반) 마이크로 서비스의 생성을 이해합니다.
ms.date: 01/07/2019
ms.openlocfilehash: 74d9022ffa70ade6ae6e7d405403524dfbc2145a
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039908"
---
# <a name="creating-a-simple-data-driven-crud-microservice"></a>단순 데이터 기반 CRUD 마이크로 서비스 만들기

이 섹션에서는 데이터 원본에서 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 수행하는 간단한 마이크로 서비스를 만드는 방법을 소개합니다.

## <a name="designing-a-simple-crud-microservice"></a>간단한 CRUD 마이크로 서비스 설계

설계의 관점에서 보면 이런 종류의 컨테이너화된 마이크로 서비스는 매우 간단합니다. 아마도 풀어야 할 문제가 간단하거나 구현이 개념 증명 수준에 불과할 것입니다.

![단순 CRUD 마이크로 서비스는 내부 설계 패턴입니다.](./media/image4.png)

**그림 6-4** 간단한 CRUD 마이크로 서비스를 위한 내부 설계

이러한 종류의 단순 데이터 중심 서비스 예로 eShopOnContainers 애플리케이션 샘플의 카탈로그 마이크로 서비스가 있습니다. 이런 종류의 서비스는 모든 기능을 데이터 모델, 비즈니스 논리, 데이터 액세스 코드에 대한 클래스를 포함한 단일 ASP.NET Core Web API 프로젝트에서 구현합니다. 또한 관련 데이터를 SQL Server를 실행하는 데이터베이스에 개발/테스트용 다른 컨테이너로 저장하지만 그림 6-5에서처럼 일반 SQL Server 호스트가 될 수도 있습니다.

![논리 카탈로그 마이크로 서비스에는 카탈로그 데이터베이스가 포함되어 있으며 동일한 Docker 호스트에 위치하거나 위치하지 않을 수 있습니다. 프로덕션이 아닌 개발의 경우에 동일한 Docker 호스트에 데이터베이스를 포함하는 것이 좋습니다.](./media/image5.png)

**그림 6-5** 단순 데이터 기반 CRUD 마이크로 서비스 설계

이런 종류의 서비스를 개발할 때는 [ASP.NET Core](https://docs.microsoft.com/aspnet/core/) 및 데이터 액세스 API나 [Entity Framework Core](https://docs.microsoft.com/ef/core/index) 같은 ORM만 있으면 됩니다. [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore)을 통해 [Swagger](https://swagger.io/) 메타데이터를 자동으로 생성하여 다음 섹션에서 설명한 대로 서비스가 제공하는 항목의 설명을 제공할 수 있습니다.

Docker 컨테이너 안에서 SQL Server 같은 데이터베이스 서버를 실행하면 클라우드나 온-프레미스에 데이터베이스를 프로비전하지 않고도 모든 종속성을 실행할 수 있기 때문에 개발 환경에 매우 유용합니다. 통합 테스트를 실행할 때는 매우 편리합니다. 그러나 프로덕션 환경의 경우 컨테이너에서 데이터베이스 서버를 실행하는 것은 권장되지 않습니다. 이 방법에서는 일반적으로 가용성이 높지 않기 때문입니다. Azure의 프로덕션 환경에서는 높은 가용성과 확장성을 제공할 수 있는 Azure SQL DB 또는 기타 데이터베이스 기술을 사용하는 것이 좋습니다. 예를 들어 NoSQL 방법의 경우 CosmosDB를 선택할 수 있습니다.

마지막으로, Dockerfile 및 docker-compose.yml 메타데이터 파일을 편집하여 이 컨테이너 이미지가 만들어지는 방법 및 사용하는 기본 이미지와, 내부 및 외부 이름, TCP 포트 같은 설계 설정을 구성할 수 있습니다.

## <a name="implementing-a-simple-crud-microservice-with-aspnet-core"></a>ASP.NET Core로 간단한 CRUD 마이크로 서비스 구현

.NET Core 및 Visual Studio를 사용하여 단순 CRUD 마이크로 서비스를 구현하려면 먼저 그림 6-6에서처럼 Linux Docker 호스트에서 실행될 수 있도록 .NET Core에서 실행하는 단순 ASP.NET Core Web API 프로젝트를 만듭니다.

![ASP.NET Core 웹 API 프로젝트를 만들려면 먼저 ASP.NET Core 웹 애플리케이션을 선택한 다음, API 형식을 선택합니다.](./media/image6.png)

**그림 6-6** Visual Studio에서 ASP.NET Core Web API 프로젝트 만들기

프로젝트를 만든 후에는 다른 Web API 프로젝트에서와 마찬가지로 Entity Framework API 또는 타 API를 사용하여 MVC 컨트롤러를 구현할 수 있습니다. 새 Web API 프로젝트에서는 마이크로 서비스의 종속성이 ASP.NET Core 자체 밖에 없습니다. 내부적으로 *Microsoft.AspNetCore.All* 종속성 내에서는 그림 6-7에서처럼 Entity Framework 및 기타 여러 .NET Core NuGet 패키지를 참조하고 있습니다.

![API 프로젝트에는 모든 필수 패키지에 대한 참조를 포함하는 Microsoft.AspNetCore.App NuGet 패키지에 대한 참조가 포함되어 있습니다. 여기에는 다른 패키지도 포함할 수 있습니다.](./media/image8.png)

**그림 6-7** 간단한 CRUD Web API 마이크로 서비스의 종속성

### <a name="implementing-crud-web-api-services-with-entity-framework-core"></a>Entity Framework Core를 사용한 CRUD Web API 구현

EF(Entity Framework) Core는 널리 사용되는 Entity Framework 데이터 액세스 기술의 가볍고 확장 가능하며 플랫폼 교차적인 버전입니다. EF Core는 개체 관계형 매퍼(ORM)로, .NET 개발자들이 .NET 개체를 사용하여 데이터베이스 작업을 수행할 수 있습니다.

카탈로그 마이크로 서비스는 그 데이터베이스가 SQL Server for Linux Docker 이미지가 있는 컨테이너에서 실행되기 때문에 EF 및 SQL Server 공급자를 사용합니다. 그러나 데이터베이스는 Windows 온-프레미스 또는 Azure SQL DB 등, 모든 SQL Server에 배포할 수 있습니다. 변경이 필요한 유일한 항목은 ASP.NET Web API 마이크로 서비스의 연결 문자열입니다.

#### <a name="the-data-model"></a>데이터 모델

EF Core에서는 데이터 액세스가 모델을 통해 수행됩니다. 모델은 도메인 모델 엔터티 클래스와, 데이터베이스를 포함한 세션을 나타내는 파생된 컨텍스트(DbContext)로 구성되어 데이터를 쿼리하고 저장할 수 있습니다. 기존 데이터베이스에서 모델을 생성하거나, 데이터베이스에 맞는 모델을 수동으로 작성하거나, EF 마이그레이션을 사용하여 모델의 데이터베이스를 만들 수 있습니다. 그러면 시간에 따라 모델이 변경되면 데이터베이스를 쉽게 발전시킬 수 있는 코드 중심 방법을 사용할 수 있습니다. 카탈로그 마이크로 서비스에는 마지막 방법을 사용합니다. 다음 코드 예제에서 [POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object)(Plain Old CLR Object) 엔터티 클래스인 CatalogItem 항목 클래스의 예를 확인할 수 있습니다.

```csharp
public class CatalogItem
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }
    public string PictureFileName { get; set; }
    public string PictureUri { get; set; }
    public int CatalogTypeId { get; set; }
    public CatalogType CatalogType { get; set; }
    public int CatalogBrandId { get; set; }
    public CatalogBrand CatalogBrand { get; set; }
    public int AvailableStock { get; set; }
    public int RestockThreshold { get; set; }
    public int MaxStockThreshold { get; set; }

    public bool OnReorder { get; set; }
    public CatalogItem() { }

    // Additional code ...
}
```

데이터베이스와의 세션을 나타내는 DbContext도 필요합니다. 카탈로그 마이크로 서비스의 경우 다음 예제와 같이 CatalogContext 클래스가 DbContext 기본 클래스에서 파생됩니다.

```csharp
public class CatalogContext : DbContext
{
    public CatalogContext(DbContextOptions<CatalogContext> options) : base(options)
    { }
    public DbSet<CatalogItem> CatalogItems { get; set; }
    public DbSet<CatalogBrand> CatalogBrands { get; set; }
    public DbSet<CatalogType> CatalogTypes { get; set; }

    // Additional code ...
}
```

추가적인 `DbContext` 구현도 가능합니다. 예를 들어 예제의 Catalog.API 마이크로 서비스에는 `CatalogContextSeed`라는 두 번째 `DbContext`가 있는데 최초로 데이터베이스 액세스를 시도할 때 샘플 데이터를 자동으로 입력합니다. 이 방법은 데모 데이터와 자동 테스트 시나리오에 모두 유용합니다.

`DbContext` 내에서는 `OnModelCreating` 메서드를 사용하여 개체/데이터베이스 엔터티 매핑 및 다른 [EF 확장 지점](https://devblogs.microsoft.com/dotnet/implementing-seeding-custom-conventions-and-interceptors-in-ef-core-1-0/)을 사용자 지정합니다.

##### <a name="querying-data-from-web-api-controllers"></a>Web API 컨트롤러에서 데이터 쿼리

엔터티 클래스의 인스턴스는 일반적으로 다음 예제에서처럼 LINQ(Language Integrated Query)를 사용하여 데이터베이스에서 검색됩니다.

```csharp
[Route("api/v1/[controller]")]
public class CatalogController : ControllerBase
{
    private readonly CatalogContext _catalogContext;
    private readonly CatalogSettings _settings;
    private readonly ICatalogIntegrationEventService _catalogIntegrationEventService;

    public CatalogController(
        CatalogContext context,
        IOptionsSnapshot<CatalogSettings> settings,
        ICatalogIntegrationEventService catalogIntegrationEventService)
    {
        _catalogContext = context ?? throw new ArgumentNullException(nameof(context));
        _catalogIntegrationEventService = catalogIntegrationEventService 
            ?? throw new ArgumentNullException(nameof(catalogIntegrationEventService));

        _settings = settings.Value;
        context.ChangeTracker.QueryTrackingBehavior = QueryTrackingBehavior.NoTracking;
    }

    // GET api/v1/[controller]/items[?pageSize=3&pageIndex=10]
    [HttpGet]
    [Route("[action]")]
    [ProducesResponseType(typeof(PaginatedItemsViewModel<CatalogItem>), (int)HttpStatusCode.OK)]
    public async Task<IActionResult> Items([FromQuery]int pageSize = 10,
                                           [FromQuery]int pageIndex = 0)

    {
        var totalItems = await _catalogContext.CatalogItems
            .LongCountAsync();

        var itemsOnPage = await _catalogContext.CatalogItems
            .OrderBy(c => c.Name)
            .Skip(pageSize * pageIndex)
            .Take(pageSize)
            .ToListAsync();

        itemsOnPage = ChangeUriPlaceholder(itemsOnPage);

        var model = new PaginatedItemsViewModel<CatalogItem>(
            pageIndex, pageSize, totalItems, itemsOnPage);

        return Ok(model);
    }
    //...
}
```

##### <a name="saving-data"></a>데이터 저장

데이터는 엔터티 클래스의 인스턴스를 통해 데이터베이스에서 만들어지고 삭제되며 수정됩니다. 다음 하드 코딩된 예제(이 경우 모의 데이터) 같은 코드를 Web API 컨트롤러에 추가할 수 있습니다.

```csharp
var catalogItem = new CatalogItem() {CatalogTypeId=2, CatalogBrandId=2,
                                     Name="Roslyn T-Shirt", Price = 12};
_context.Catalog.Add(catalogItem);
_context.SaveChanges();
```

##### <a name="dependency-injection-in-aspnet-core-and-web-api-controllers"></a>ASP.NET Core 및 Web API에서 종속성 주입

ASP.NET Core에서는 DI(Dependency Injection)를 즉시 사용할 수 있습니다. 원한다면 선호하는 IoC 컨테이너를 ASP.NET Core 인프라에 연결할 수 있지만 타사 IoC(Inversion of Control) 컨테이너를 사용할 필요가 없습니다. 이 경우 컨트롤러 생성자를 통해 필요한 EF DBContext나 추가 저장소를 직접 주입할 수 있습니다.

위의 `CatalogController` 클래스 예제에서는 `CatalogController()` 생성자를 통해 `CatalogContext` 유형의 개체와 다른 개체를 주입합니다.

Web API 프로젝트를 설정하는 데 중요한 구성은 서비스의 IoC 컨테이너에 DbContext 클래스를 등록하는 것입니다. 일반적으로 다음 예제에서처럼 `ConfigureServices()` 메서드 안에서 `services.AddDbContext<DbContext>()` 메서드를 호출하여 `Startup` 클래스에서 이를 수행합니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Additional code...

    services.AddDbContext<CatalogContext>(options =>
    {
        options.UseSqlServer(Configuration["ConnectionString"],
        sqlServerOptionsAction: sqlOptions =>
        {
            sqlOptions.MigrationsAssembly(
                typeof(Startup).GetTypeInfo().Assembly.GetName().Name);

           //Configuring Connection Resiliency:
           sqlOptions.
               EnableRetryOnFailure(maxRetryCount: 5,
               maxRetryDelay: TimeSpan.FromSeconds(30),
               errorNumbersToAdd: null);

       });

       // Changing default behavior when client evaluation occurs to throw.
       // Default in EFCore would be to log warning when client evaluation is done.
       options.ConfigureWarnings(warnings => warnings.Throw(
           RelationalEventId.QueryClientEvaluationWarning));
   });

  //...
}
```

### <a name="additional-resources"></a>추가 자료

- **데이터 쿼리** \
  [https://docs.microsoft.com/ef/core/querying/index](/ef/core/querying/index)

- **데이터 저장** \
  [https://docs.microsoft.com/ef/core/saving/index](/ef/core/saving/index)

## <a name="the-db-connection-string-and-environment-variables-used-by-docker-containers"></a>Docker 컨테이너에서 사용하는 DB 연결 문자열 및 환경 변수

다음 예제와 같이 ASP.NET Core 설정을 사용하고 settings.json 파일에 ConnectionString 속성을 추가할 수 있습니다.

```json
{
    "ConnectionString": "Server=tcp:127.0.0.1,5433;Initial Catalog=Microsoft.eShopOnContainers.Services.CatalogDb;User Id=sa;Password=Pass@word",
    "ExternalCatalogBaseUrl": "http://localhost:5101",
    "Logging": {
        "IncludeScopes": false,
        "LogLevel": {
            "Default": "Debug",
            "System": "Information",
            "Microsoft": "Information"
        }
    }
}
```

settings.json 파일에는 ConnectionString 속성 또는 다른 속성에 대한 기본값이 있습니다. 그러나 이러한 속성은 Docker를 사용하는 경우 docker-compose.override.yml 파일에서 지정한 환경 변수 값에 의해 재정의됩니다.

다음 docker-compose.yml 또는 docker-compose.override.yml 파일에서 이러한 환경 변수를 초기화하여 docker-compose.override.yml 파일에서처럼 Docker가 이를 OS 환경 변수로 설정하게 할 수 있습니다(이 예제에서는 연결 문자열 및 기타 자동 줄 바꿈이지만 사용자 고유 파일에서는 자동 줄 바꿈 안 함).

```yml
# docker-compose.override.yml

#
catalog.api:
  environment:
    - ConnectionString=Server=sql.data;Database=Microsoft.eShopOnContainers.Services.CatalogDb;User Id=sa;Password=Pass@word
    # Additional environment variables for this service
  ports:
    - "5101:80"
```

Azure DevOps Services Docker 배포 작업처럼 배포 도구에서 설정한 값으로 docker-compose 파일에서 선언한 환경 변수를 재정의할 경우 솔루션 수준의 docker-compose.yml 파일은 프로젝트나 마이크로 서비스 수준에서 구성 파일보다 더 유연할 뿐 아니라 안전합니다.

마지막으로 이전 코드 예제의 ConfigureServices 메소드에서처럼 Configuration\["ConnectionString"\]을 사용하여 코드에서 값을 가져올 수 있습니다.

그러나 프로덕션 환경의 경우 연결 문자열처럼 비밀을 저장하는 다른 방법을 모색하고자 할 수 있습니다. 애플리케이션 비밀을 관리하는 가장 좋은 방법은 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/)를 사용하는 것입니다.

Azure Key Vault를 통해 클라우드 애플리케이션 및 서비스에서 사용되는 암호화 키와 비밀을 저장하고 보호할 수 있습니다. 비밀은 API 키, 연결 문자열, 암호 등의 엄격한 제어를 유지하려는 모든 항목이며, 엄격한 제어는 사용 현황 로깅, 만료 설정, 액세스 관리, *기타*를 포함합니다.

Azure Key Vault를 사용하면 누군가에게 알리지 않고 애플리케이션 비밀 사용 현황을 매우 세부적으로 제어할 수 있습니다. 비밀은 개발 또는 작업을 방해하지 않고 보안을 강화하기 위해 회전될 수도 있습니다.

애플리케이션은 Key Vault를 사용할 수 있도록 조직의 Active Directory에 등록되야 합니다.

자세한 내용은 *Key Vault 개념 설명서*를 확인하면 됩니다.

### <a name="implementing-versioning-in-aspnet-web-apis"></a>ASP.NET Web API의 버전 관리 구현

비즈니스 요구 사항 변화에 따라 새 리소스 컬렉션이 추가되고 리소스 사이의 관계가 변화하며 리소스 내 데이터 구조가 변경될 수 있습니다. 새 요구 사항을 처리하기 위한 Web API 업데이트는 상대적으로 간단한 프로세스이나 이러한 변경이 Web API를 사용하는 클라이언트 애플리케이션에 미치는 영향을 고려해야 합니다. Web API의 개발자 설계 및 구현은 API를 완전히 제어할 수 있으나 타 조직에서 원격으로 운영하는 클라이언트 애플리케이션에 대해서는 개발자가 그 수준 만큼 제어할 수 없습니다.

버전 관리를 통해 Web API가 자신이 노출하는 기능 및 리소스를 표시하게 할 수 있습니다. 그러면 클라이언트 애플리케이션이 특정 버전의 기능이나 리소스에 대해 요청을 제출할 수 있습니다. 버전 관리를 구현하는 방법에는 몇 가지가 있습니다.

- URI 버전 관리

- 쿼리 문자열 버전 관리

- 헤더 버전 관리

쿼리 문자열과 URI 버전 관리가 가장 구현이 간단합니다. 헤더 버전 관리는 좋은 방법입니다. 그러나 헤더 버전 관리는 URI 버전 관리 만큼 명시적이거나 간단하지 않습니다. URL 버전 관리가 가장 간단하고 명시적이므로 eShopOnContainers 애플리케이션 예제에서는 URI 버전 관리를 사용합니다.

EShopOnContainers 애플리케이션 예제에서처럼 URI 버전 관리를 사용하면 Web API를 수정할 때나 리소스 스키마를 변경할 때마다 버전 번호를 각 리소스의 URI에 추가합니다. 기존 URI는 전처럼 작동하고 요청된 버전에 부합하는 스키마에 따른 리소스를 반환하게 됩니다.

다음 코드 예제와 같이 버전은 Web API 컨트롤러의 Route 속성을 사용하여 설정할 수 있고 이렇게 하면 URI에서 버전이 명확해집니다(이 경우 v1).

```csharp
[Route("api/v1/[controller]")]
public class CatalogController : ControllerBase
{
    // Implementation ...
```

이 버전 관리 메커니즘은 간단하며 적합한 엔드포인트에 요청을 전달하는 서버에 따라 달라집니다. 그러나 더 복잡한 버전 관리와, REST를 사용할 때 가장 좋은 방법은 하이퍼미디어를 사용하고 [HATEOAS(Hypertext as the Engine of Application State)](https://docs.microsoft.com/azure/architecture/best-practices/api-design#use-hateoas-to-enable-navigation-to-related-resources)를 구현하는 것입니다.

### <a name="additional-resources"></a>추가 자료

- **Scott Hanselman. 쉬워진 ASP.NET Core RESTful Web API 버전 관리** \
  <https://www.hanselman.com/blog/ASPNETCoreRESTfulWebAPIVersioningMadeEasy.aspx>

- **RESTful Web API 버전 관리** \
  <https://docs.microsoft.com/azure/architecture/best-practices/api-design#versioning-a-restful-web-api>

- **Roy Fielding. 버전 관리, 하이퍼미디어 및 REST** \
  <https://www.infoq.com/articles/roy-fielding-on-versioning>

## <a name="generating-swagger-description-metadata-from-your-aspnet-core-web-api"></a>ASP.NET Core Web API에서 Swagger 설명 메타데이터 생성

[Swagger](https://swagger.io/)는 RESTful API의 설계, 빌드, 문서화, 사용에 도움이 되는 인기 있는 오픈 소스 프레임워크로, 대형 도구 생태계로부터 지원을 받습니다. API 설명 메타데이터 도메인의 표준으로 자리하고 있습니다. 데이터 중심 마이크로 서비스 또는 더 높은 수준의 도메인 중심 마이크로 서비스 등, 모든 종류의 마이크로 서비스에 Swagger 설명 메타데이터를 포함해야 합니다(다음 섹션에서 설명).

Swagger의 핵심은 JSON 또는 YAML 파일의 API 설명 메타데이터인Swagger 사양입니다. 이 사양은 API에 대한 RESTful 계약을 생성하며 간편한 개발, 검색 및 통합을 위해 사람과 기계가 모두 판독 가능한 형식으로 리소스 및 작업을 상세히 설명합니다.

사양은 OAS(OpenAPI 사양)의 기본이며 RESTful 인터페이스 정의 방법을 표준화하기 위해 투명하고 협력적이며 개방된 커뮤니티에서 개발됩니다.

서비스가 검색될 수 있는 방법과 기능을 이해하는 방법에 대한 구조를 정의합니다. 웹 편집기 및 Spotify, Uber, Slack 및 Microsoft 등의 Swagger 사양 예제에 대한 자세한 내용은 Swagger 사이트(<https://swagger.io>)를 참조하세요.

### <a name="why-use-swagger"></a>Swagger를 사용하는 이유

API에 대해 Swagger 메타데이터를 생성하는 주된 이유는 다음과 같습니다.

**다른 제품이 자동으로 API를 사용하고 통합하도록 합니다**. 다양 한 제품 및 [고급 도구](https://swagger.io/commercial-tools/)와 여러 [라이브러리 및 프레임워크](https://swagger.io/open-source-integrations/)가 Swagger를 지원합니다. Microsoft는 다음과 같이 Swagger 기반 API를 자동으로 사용할 수 있는 높은 수준의 제품 및 도구를 갖추고 있습니다.

- [AutoRest](https://github.com/Azure/AutoRest). Swagger를 호출하기 위한 .NET 클라이언트 클래스를 자동으로 생성할 수 있습니다. 이 도구는 CLI에서 사용할 수 있고 Visual Studio와 통합하여 GUI를 통해 간편하게 사용할 수 있습니다.

- [Microsoft Flow](https://flow.microsoft.com/). 자동으로 [API를 사용하고 높은 수준의 Microsoft Flow 워크플로에 통합할 수 있으며](https://flow.microsoft.com/blog/integrating-custom-api/) 프로그래밍 기술이 필요하지 않습니다.

- [Microsoft PowerApps](https://powerapps.microsoft.com/). [PowerApps Studio](https://powerapps.microsoft.com/build-powerapps/)의 [PowerApps 모바일 앱](https://powerapps.microsoft.com/blog/register-and-use-custom-apis-in-powerapps/)에서 자동으로 API를 사용할 수 있으며 프로그래밍 기술이 필요하지 않습니다.

- [Azure App Service Logic Apps](https://docs.microsoft.com/azure/app-service-logic/app-service-logic-what-are-logic-apps). 자동으로 API를 사용하고 [Azure App Service Logic App](https://docs.microsoft.com/azure/app-service-logic/app-service-logic-custom-hosted-api)에 통합할 수 있으며 프로그래밍 기술이 필요하지 않습니다.

**API 문서를 자동으로 생성하는 기능**. 복잡한 마이크로 서비스 기반 애플리케이션처럼 대규모 RESTful API를 만들 때는 요청과 응답 페이로드에서 사용되는 다양한 데이터 모델에서 많은 엔드포인트를 처리해야 합니다. Swagger를 통해 얻을 수 있는 적절한 문서와 견고한 API 탐색기는 API 및 개발자의 채택 성공을 위한 핵심입니다.

Swagger의 메타데이터는 Microsoft Flow, PowerApps 및 Azure Logic Apps에서 API 사용 방법을 이해하고 API를 연결하는 데 사용합니다.

*swagger-ui*에 따라 기능 API 도움말 페이지의 양식으로 ASP.NET Core REST API 애플리케이션에 대한 Swagger 메타데이터 생성을 자동화하는 방법은 여러 가지가 있습니다.

가장 잘 알고 있는 방법은 아마도 [eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers)에서 현재 사용되는 [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore)일 것입니다. 이 가이드에서 자세히 다루겠지만 Swagger 또는 OpenAPI 사양에서 및 [NSwagStudio](https://github.com/RSuter/NSwag/wiki/NSwagStudio)를 사용하는 컨트롤러가 포함된 .dll을 검사하여 Typescript 및 C\# API 클라이언트뿐만 아니라 C\# 컨트롤러를 생성할 수 있는 [NSwag](https://github.com/RSuter/NSwag)를 사용하는 옵션도 있습니다.

### <a name="how-to-automate-api-swagger-metadata-generation-with-the-swashbuckle-nuget-package"></a>Swashbuckle NuGet 패키지에서 API Swagger 메타데이터 생성을 자동화하는 방법

수동으로 Swagger 메타데이터를 생성하는 작업(JSON 또는 YAML 파일로)은 지루할 수 있습니다. 그렇지만 [Swashbuckle NuGet 패키지](https://aka.ms/swashbuckledotnetcore)를 사용하여 동적으로 Swagger API 메타 데이터를 생성함으로써 ASP.NET Web API 서비스의 API 검색을 자동화할 수 있습니다.

Swashbuckle은 ASP.NET Web API 프로젝트에 대한 Swagger 메타 데이터를 자동으로 생성합니다. ASP.NET Core Web API 프로젝트 및 기존의 ASP.NET Web API와, ASP.NET 기반의 Azure API 앱, Azure Mobile App, Azure Service Fabric 마이크로 서비스 등의 다른 항목을 지원 합니다. 또한 참조 애플리케이션에서와 같이 컨테이너에 배포된 일반 Web API도 지원합니다.

Swashbuckle은 API Explorer 및 Swagger 또는 [swagger-ui](https://github.com/swagger-api/swagger-ui)를 결합하여 API 사용자를 위한 풍부한 검색 및 문서 환경을 제공합니다. Swashbuckle에는 Swagger 메타 데이터 생성기 엔진 외에도 Swashbuckle 설치 후 자동으로 서비스를 시작하는 swagger-ui의 임베디드 버전이 포함되어 있습니다.

즉, 개발자가 API를 사용하는 데 도움이 되는 좋은 검색 UI로 API를 보완할 수 있습니다. 자동으로 생성되므로 코드와 유지 관리 작업이 매우 적기 때문에 API 구축에 전념할 수 있습니다. API Explorer의 결과는 그림 6-8과 유사합니다.

![Swashbuckle 생성 Swagger UI API 설명서에는 게시된 모든 작업이 포함됩니다.](./media/image9.png)

**그림 6-8** Swagger 메타 데이터 기반 Swashbuckle API 탐색기 -eShopOnContainers 카탈로그 마이크로 서비스

여기서 가장 중요한 것은 API 탐색기가 아닙니다. Swagger 메타 데이터에서 스스로를 설명할 수 있는 Web API가 있으면 여러 플랫폼을 대상으로 할 수 있는 클라이언트 프록시-클래스 코드 생성기를 포함하여 Swagger 기반 도구에서 API를 자연스럽게 사용할 수 있습니다. 예를 들어, 설명한 것처럼 [AutoRest](https://github.com/Azure/AutoRest)는 .NET 클라이언트 클래스를 자동으로 생성합니다. 그렇지만 API 클라이언트 라이브럴, 서버 스텁, 설명서의 코드 자동 생성을 지원하는 [swagger-codegen](https://github.com/swagger-api/swagger-codegen) 같은 다른 도구도 사용할 수 있습니다.

현재 Swashbuckle은 ASP.NET Core 애플리케이션에 대해 높은 수준의 메타패키지 [Swashbuckle.AspNetCore](https://www.nuget.org/packages/Swashbuckle.AspNetCore)에서 다섯 개의 내부 NuGet 패키지로 구성되어 있습니다.

Web API 프로젝트에 이러한 NuGet 패키지를 설치한 후에 간소화된 다음 코드에서처럼 시작 클래스에 Swagger를 구성해야 합니다.

```csharp
public class Startup
{
    public IConfigurationRoot Configuration { get; }
    // Other startup code...

    public void ConfigureServices(IServiceCollection services)
    {
        // Other ConfigureServices() code...

        // Add framework services.
        services.AddSwaggerGen(options =>
        {
            options.DescribeAllEnumsAsStrings();
            options.SwaggerDoc("v1", new Swashbuckle.AspNetCore.Swagger.Info
            {
                Title = "eShopOnContainers - Catalog HTTP API",
                Version = "v1",
                Description = "The Catalog Microservice HTTP API. This is a Data-Driven/CRUD microservice sample",
                TermsOfService = "Terms Of Service"
            });
        });

        // Other ConfigureServices() code...
    }

    public void Configure(IApplicationBuilder app,
        IHostingEnvironment env,
        ILoggerFactory loggerFactory)
    {
        // Other Configure() code...
        // ...
        app.UseSwagger()
            .UseSwaggerUI(c =>
            {
                c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
            });
    }
}
```

이 작업이 완료되면 애플리케이션을 시작하고 다음과 같이 URL을 사용하여 다음 Swagger JSON 및 UI 엔드포인트를 탐색할 수 있습니다.

```url
  http://<your-root-url>/swagger/v1/swagger.json

  http://<your-root-url>/swagger/
```

앞서 본 것처럼 URL에 대해 Swashbuckle에서 생성된 UI는 `http://<your-root-url>/swagger`와 같습니다. 그림 6-9에서는 모든 API 메서드를 테스트하는 방법을 확인할 수 있습니다.

![Swagger UI API 세부 정보에서는 응답의 예제를 보여주고, 개발자 검색에 적합한 실제 API를 실행하는 데 사용될 수 있습니다.](./media/image10.png)

**그림 6-9** 카탈로그/항목 API 메서드를 테스트하는 Swashbuckle UI

그림 6-10은 [Postman](https://www.getpostman.com/)을 사용하여 `http://<your-root-url>/swagger/v1/swagger.json`을 요청하면 아래의 도구에서 사용한 eShopOnContainers 마이크로 서비스에서 생성된 Swagger JSON 메타데이터를 보여 줍니다.

![Swagger JSON 메타데이터를 보여주는 샘플 Postman UI](./media/image11.png)

**그림 6-10** Swagger JSON 메타데이터

이렇게 간단합니다. 그리고 자동으로 생성되기 때문에 API에 더 많은 기능을 추가하면 Swagger 메타데이터가 커집니다.

### <a name="additional-resources"></a>추가 자료

- **Swagger를 사용한 ASP.NET Web API 도움말 페이지** \
  [https://docs.microsoft.com/aspnet/core/tutorials/web-api-help-pages-using-swagger](/aspnet/core/tutorials/web-api-help-pages-using-swagger)

- **Swashbuckle 및 ASP.NET Core 시작** \
  [https://docs.microsoft.com/aspnet/core/tutorials/getting-started-with-swashbuckle](/aspnet/core/tutorials/getting-started-with-swashbuckle)

- **NSwag 및 ASP.NET Core 시작** \
  [https://docs.microsoft.com/aspnet/core/tutorials/getting-started-with-nswag](/aspnet/core/tutorials/getting-started-with-nswag)

> [!div class="step-by-step"]
> [이전](microservice-application-design.md)
> [다음](multi-container-applications-docker-compose.md)
