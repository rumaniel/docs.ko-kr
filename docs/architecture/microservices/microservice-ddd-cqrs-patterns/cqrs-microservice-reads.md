---
title: CQRS 마이크로 서비스에서 읽기/쿼리 구현
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | Dapper를 사용하여 eShopOnContainers의 주문 마이크로 서비스에서 CQRS 쿼리 측면의 구현을 이해합니다.
ms.date: 10/08/2018
ms.openlocfilehash: c39a42b7f5200208a0f812665a2d1c87b4433ba9
ms.sourcegitcommit: 992f80328b51b165051c42ff5330788627abe973
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72275790"
---
# <a name="implement-readsqueries-in-a-cqrs-microservice"></a>CQRS 마이크로 서비스에서 읽기/쿼리 구현

읽기/쿼리의 경우 eShopOnContainers 참조 애플리케이션의 주문 마이크로 서비스에서 DDD 모델 및 트랜잭션 영역과 별도로 쿼리를 구현합니다. 이 작업은 주로 쿼리와 트랜잭션에 대한 요구가 매우 다르기 때문에 수행되었습니다. 쓰기는 도메인 논리와 호환되어야 하는 트랜잭션을 실행합니다. 반면에 쿼리는 idempotent(멱등원)이며 도메인 규칙과 분리될 수 있습니다.

이 접근 방식은 그림 7-3과 같이 간단합니다. API 인터페이스는 마이크로 ORM(Object Relational Mapper)(예: Dapper)과 같은 인프라를 사용하는 웹 API 컨트롤러에서 구현되며, UI 애플리케이션의 필요에 따라 동적 ViewModel을 반환합니다.

![간소화된 CQRS 접근 방식에서 쿼리 측면에 대한 가장 간단한 방법은 데이터베이스를 Dapper 같은 Micro-ORM으로 쿼리하고 동적 ViewModels를 반환함으로써 구현될 수 있습니다.](./media/image3.png)

**그림 7-3**. CQRS 마이크로 서비스에서 가장 간단한 쿼리 방법

가능한 가장 간단한 쿼리 방법입니다. 쿼리 정의는 데이터베이스를 쿼리하고 각 쿼리에 대해 즉시 작성된 동적 ViewModel을 반환합니다. 쿼리는 idempotent이므로 쿼리 실행 횟수와 관계없이 데이터를 변경하지 않습니다. 따라서 집계 및 다른 패턴과 같은 트랜잭션 측면에서 사용되는 DDD 패턴으로 제한할 필요가 없으므로 쿼리가 트랜잭션 영역과 분리됩니다. 데이터베이스에 대해 UI에 필요한 데이터를 쿼리하기만 하면, SQL 문 자체를 제외하고 어디서든 정적으로 정의할 필요가 없는 동적 ViewModel(ViewModel에 대한 클래스 없음)을 반환합니다.

간단한 방법이므로 쿼리 측면(예: [Dapper](https://github.com/StackExchange/Dapper)와 같은 마이크로 ORM을 사용하는 코드)에 필요한 코드는 [동일한 웹 API 프로젝트 내에서](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Queries/OrderQueries.cs) 구현할 수 있습니다. 그림 7-4에서 이를 보여줍니다. 쿼리는 eShopOnContainers 솔루션 내의 **Ordering.API** 마이크로 서비스 프로젝트에서 정의됩니다.

![애플리케이션 > 쿼리 폴더를 표시하는 Ordering.API 프로젝트의 솔루션 탐색기 보기.](./media/image4.png)

**그림 7-4**. eShopOnContainers에서 주문 마이크로 서비스의 쿼리

## <a name="use-viewmodels-specifically-made-for-client-apps-independent-from-domain-model-constraints"></a>도메인 모델 제약 조건과 별도로 클라이언트 앱용으로 특별히 제작된 ViewModels 사용

쿼리는 클라이언트 애플리케이션에 필요한 데이터를 가져오기 위해 수행되므로 쿼리에서 반환된 데이터에 기반하여 클라이언트에 대해 반환되는 형식을 구체적으로 만들 수 있습니다. 이러한 모델 또는 DTO(데이터 전송 개체)를 ViewModel이라고 합니다.

반환된 데이터(ViewModel)는 데이터베이스의 여러 엔터티 또는 테이블의 데이터, 심지어 트랜잭션 영역에 대한 도메인 모델에 정의된 여러 집계 간의 데이터를 조인한 결과일 수 있습니다. 이 경우 도메인 모델과 별도로 쿼리를 만들기 때문에 집계 경계와 제약 조건은 완전히 무시되며 필요한 테이블과 열을 자유롭게 쿼리할 수 있습니다. 이 방법은 쿼리를 만들거나 업데이트하는 데 있어 뛰어난 유연성과 생산성을 개발자에게 제공합니다.

ViewModel은 클래스에 정의된 정적 형식이 될 수 있습니다. 또는 개발자에게 매우 민첩한 주문 마이크로 서비스에서 구현되는 것과 같이 수행된 쿼리에 따라 동적으로 만들 수 있습니다.

## <a name="use-dapper-as-a-micro-orm-to-perform-queries"></a>Dapper를 마이크로 ORM으로 사용하여 쿼리를 수행합니다. 

마이크로 ORM, Entity Framework Core 또는 일반 ADO.NET을 쿼리에 사용할 수 있습니다. 샘플 애플리케이션에서 Dapper는 인기 있는 마이크로 ORM의 좋은 예인 eShopOnContainers에서 주문 마이크로 서비스로 선택되었습니다. 매우 작은 프레임워크이므로 뛰어난 성능으로 일반 SQL 쿼리를 실행할 수 있습니다. Dapper를 사용하면 여러 테이블에 액세스하고 조인할 수 있는 SQL 쿼리를 작성할 수 있습니다.

Dapper는 오픈 소스 프로젝트(원래 Sam Saffron이 만듦)이며 [Stack Overflow](https://stackoverflow.com/)에서 사용되는 구성 요소의 일부입니다. Dapper를 사용하려면 다음 그림과 같이 [Dapper NuGet 패키지](https://www.nuget.org/packages/Dapper)를 통해 이를 설치해야 합니다.

![VS에서 NuGet 패키지 관리 보기에 표시되는 Dapper 패키지.](./media/image4.1.png)

또한 코드에서 Dapper 확장 메서드에 액세스할 수 있도록 using 문도 추가해야 합니다.

코드에서 Dapper를 사용하면 <xref:System.Data.SqlClient> 네임스페이스에서 사용할 수 있는 <xref:System.Data.SqlClient.SqlConnection> 클래스를 직접 사용할 수 있습니다. QueryAsync 메서드 및 <xref:System.Data.SqlClient.SqlConnection> 클래스를 확장하는 다른 확장 메서드를 통해 간단하고 성능이 뛰어난 방식으로 쿼리를 실행할 수 있습니다.

## <a name="dynamic-versus-static-viewmodels"></a>동적 및 정적 ViewModel

ViewModels를 서버 쪽에서 클라이언트 앱으로 반환할 때, ViewModels는 클라이언트 앱이 요구하는 방식으로 데이터를 저장하기 때문에 해당 ViewModels를 엔터티 모델의 내부 도메인 엔터티와 다를 수 있는 DTO(데이터 전송 개체)로 생각할 수 있습니다. 따라서 대부분의 경우 여러 도메인 엔터티에서 가져온 데이터를 집계하고, 클라이언트 앱에서 해당 데이터가 필요한 방식에 따라 ViewModel을 정확하게 구성할 수 있습니다.

이러한 ViewModels 또는 DTO는 나중에 코드 조각에 표시된 `OrderSummary` 클래스와 같이 명시적으로 정의(데이터 보유자 클래스로)하거나 단순히 쿼리에서 반환한 특성에 따라 동적 ViewModels 또는 동적 DTO를 동적 유형으로만 반환할 수도 있습니다.

### <a name="viewmodel-as-dynamic-type"></a>동적 형식으로 ViewModel 반환

다음 코드에서 볼 수 있듯이 `ViewModel`은 쿼리에서 반환된 속성에 따라 내부적으로 *동적* 유형을 반환하기만 하면 쿼리에서 직접 반환할 수 있습니다. 즉 반환될 특성의 하위 집합은 쿼리 자체를 기반으로 합니다. 따라서 쿼리 또는 조인에 새 열을 추가하면 해당 데이터가 반환된 `ViewModel`에 동적으로 추가됩니다.

```csharp
using Dapper;
using Microsoft.Extensions.Configuration;
using System.Data.SqlClient;
using System.Threading.Tasks;
using System.Dynamic;
using System.Collections.Generic;

public class OrderQueries : IOrderQueries
{
    public async Task<IEnumerable<dynamic>> GetOrdersAsync()
    {
        using (var connection = new SqlConnection(_connectionString))
        {
            connection.Open();
            return await connection.QueryAsync<dynamic>(
                @"SELECT o.[Id] as ordernumber,
                o.[OrderDate] as [date],os.[Name] as [status],
                SUM(oi.units*oi.unitprice) as total
                FROM [ordering].[Orders] o
                LEFT JOIN[ordering].[orderitems] oi ON o.Id = oi.orderid
                LEFT JOIN[ordering].[orderstatus] os on o.OrderStatusId = os.Id
                GROUP BY o.[Id], o.[OrderDate], os.[Name]");
        }
    }
}
```

중요한 점은 동적 형식을 사용하면 반환되는 데이터 컬렉션이 ViewModel로 동적으로 어셈블된다는 것입니다.

**장점:** 이 방법은 쿼리의 SQL 문장을 업데이트할 때마다 정적 ViewModel 클래스를 수정할 필요성을 줄이므로 이후의 변경과 관련하여 간단하고 빠르게 진화할 수 있도록 코딩할 때 이 디자인 방법을 매우 민첩하게 만들 수 있습니다.

**단점:** 장기적으로 동적 유형은 클라이언트 앱과 서비스의 명확성 및 호환성에 부정적인 영향을 줄 수 있습니다. 또한 Swashbuckle과 같은 미들웨어 소프트웨어는 동적 유형을 사용하는 경우 반환되는 형식에 대해 동일한 수준의 문서를 제공할 수 없습니다.

### <a name="viewmodel-as-predefined-dto-classes"></a>미리 정의된 DTO 클래스인 ViewModel

**장점**: 명시적 DTO 클래스를 기반으로 하는 “계약”과 같이 미리 정의된 정적 ViewModel 클래스를 사용하면, 동일한 애플리케이션에서만 사용되는 경우에도 공용 API뿐만 아니라 장기적인 마이크로 서비스에도 확실히 더 좋습니다.

Swagger에 대한 응답 형식을 지정하려면 명시적 DTO 클래스를 반환 형식으로 사용해야 합니다. 따라서 미리 정의된 DTO 클래스를 사용하면 Swagger에서 더 많은 정보를 제공할 수 있습니다. API를 사용할 때 API 문서화 및 호환성이 향상됩니다.

**단점**: 앞에서 언급했듯이 코드를 업데이트할 때 DTO 클래스를 업데이트하는 데 몇 가지 단계가 필요합니다.

경험을 기반으로 한 팁:  eShopOnContainers의 주문 마이크로 서비스에서 구현된 쿼리에서, 초기 개발 단계에서 매우 간단하고 민첩했기 때문에 동적 ViewModels를 사용하여 개발하기 시작했습니다. 그러나 개발이 안정화된 후에는 API를 리팩터링하고 ViewModel에 정적 또는 미리 정의된 DTO를 사용하도록 결정했습니다. 이는 마이크로 서비스 소비자에서 명시적 DTO 형식을 인식하고 "계약"으로 사용하는 것이 더 명확하기 때문입니다.

다음 예제에서는 명시적 ViewModel DTO 클래스인 OrderSummary 클래스를 사용하여 쿼리에서 데이터를 반환하는 방법을 확인할 수 있습니다.

```csharp
using Dapper;
using Microsoft.Extensions.Configuration;
using System.Data.SqlClient;
using System.Threading.Tasks;
using System.Dynamic;
using System.Collections.Generic;

public class OrderQueries : IOrderQueries
{
  public async Task<IEnumerable<OrderSummary>> GetOrdersAsync()
    {
        using (var connection = new SqlConnection(_connectionString))
        {
            connection.Open();
            return await connection.QueryAsync<OrderSummary>(
                  @"SELECT o.[Id] as ordernumber, 
                  o.[OrderDate] as [date],os.[Name] as [status], 
                  SUM(oi.units*oi.unitprice) as total
                  FROM [ordering].[Orders] o
                  LEFT JOIN[ordering].[orderitems] oi ON  o.Id = oi.orderid 
                  LEFT JOIN[ordering].[orderstatus] os on o.OrderStatusId = os.Id
                  GROUP BY o.[Id], o.[OrderDate], os.[Name]
                  ORDER BY o.[Id]");
        }
    } 
}
```

#### <a name="describe-response-types-of-web-apis"></a>Web API의 응답 형식 설명

웹 API 및 마이크로 서비스를 사용하는 개발자는 반환되는 항목, 특히 응답 형식 및 오류 코드 (표준이 아닌 경우)에 많은 관심을 가지고 있습니다. 이러한 항목은 XML 주석 및 데이터 주석에서 처리됩니다.

Swagger UI에 적절한 문서화가 없으면 반환되는 형식 또는 반환될 수 있는 HTTP 코드에 대한 정보가 부족하게 됩니다. 해당 문제는 <xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute?displayProperty=nameWithType>을 추가하여 해결되므로 다음 코드에서와 같이 Swashbuckle API 반환 모델과 값에 대한 더 풍부한 정보를 생성할 수 있습니다.

```csharp
namespace Microsoft.eShopOnContainers.Services.Ordering.API.Controllers
{
    [Route("api/v1/[controller]")]
    [Authorize]
    public class OrdersController : Controller
    {
        //Additional code...
        [Route("")]
        [HttpGet]
        [ProducesResponseType(typeof(IEnumerable<OrderSummary>),
            (int)HttpStatusCode.OK)]
        public async Task<IActionResult> GetOrders()
        {
            var userid = _identityService.GetUserIdentity();
            var orders = await _orderQueries
                .GetOrdersFromUserAsync(Guid.Parse(userid));
            return Ok(orders);
        }
    }
}
```

그러나 `ProducesResponseType` 특성은 다음과 같이 동적 형식을 사용할 수 없지만 `OrderSummary` ViewModel DTO와 같은 명시적 형식을 사용해야 합니다.

```csharp
public class OrderSummary
{
    public int ordernumber { get; set; }
    public DateTime date { get; set; }
    public string status { get; set; }
    public double total { get; set; }
}
```

이는 반환된 명시적 형식이 장기적으로 동적 형식보다 더 나은 또 다른 이유입니다. `ProducesResponseType` 특성을 사용할 때 200, 400 등과 같이 가능한 HTTP 오류/코드와 관련하여 예상되는 결과를 지정할 수도 있습니다.

다음 이미지에서 Swagger UI에서 ResponseType 정보를 표시하는 방법을 확인할 수 있습니다.

![Ordering API에 대한 Swagger UI 페이지의 브라우저 보기.](./media/image5.png)

**그림 7-5**. 웹 API에서 응답 형식 및 가능한 HTTP 상태 코드를 보여 주는 Swagger UI

위의 이미지에서는 ViewModel 형식 및 반환될 수 있는 가능한 HTTP 상태 코드에 기반한 몇 가지 예제 값을 확인할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

- **Dapper**  
 <https://github.com/StackExchange/dapper-dot-net>

- **Julie Lerman. 데이터 요소 - Dapper, Entity Framework 및 하이브리드 앱(MSDN 매거진 문서)**  
  <https://msdn.microsoft.com/magazine/mt703432>

- **Swagger를 사용한 ASP.NET Core Web API 도움말 페이지**  
  <https://docs.microsoft.com/aspnet/core/tutorials/web-api-help-pages-using-swagger?tabs=visual-studio>

>[!div class="step-by-step"]
>[이전](eshoponcontainers-cqrs-ddd-microservice.md)
>[다음](ddd-oriented-microservice.md)
