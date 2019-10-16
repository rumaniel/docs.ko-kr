---
title: HttpClientFactory를 사용하여 복원력 있는 HTTP 요청 구현
description: 애플리케이션에서 사용하기 쉽도록 .NET Core 2.1부터 제공되는 HttpClientFactory를 사용하여 `HttpClient` 인스턴스를 만드는 방법을 알아봅니다.
ms.date: 08/08/2019
ms.openlocfilehash: 6c862171ee6b5eda6f95694878bfa43518a9bdfa
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039969"
---
# <a name="use-httpclientfactory-to-implement-resilient-http-requests"></a>HttpClientFactory를 사용하여 복원력 있는 HTTP 요청 구현

`HttpClientFactory`는 애플리케이션에서 사용할 <xref:System.Net.Http.HttpClient> 인스턴스를 만드는 독창적인 팩터리이며, .NET Core 2.1부터 사용할 수 있습니다.

## <a name="issues-with-the-original-httpclient-class-available-in-net-core"></a>.NET Core에서 사용할 수 있는 원래의 HttpClient 클래스 문제

잘 알려진 원래의 <xref:System.Net.Http.HttpClient> 클래스는 쉽게 사용할 수 있지만, 많은 개발자가 제대로 사용하지 못하는 경우도 있습니다.

첫 번째 문제로, 이 클래스는 삭제할 수 있지만, `HttpClient` 개체를 삭제하는 경우에도 기본 소켓이 즉시 해제되지 않고 '소켓 소모'라는 심각한 문제가 발생할 수 있기 때문에 `using` 문과 함께 사용하는 것이 최선의 선택이 아니라는 것입니다. 이 문제에 대한 자세한 내용은 [You're using HttpClient wrong and it's destabilizing your software](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/)(잘못 사용하고 있는 HttpClient로 인해 불안정해지고 있는 소프트웨어) 블로그 게시물을 참조하세요.

따라서 `HttpClient`는 한 번 인스턴스화되어 애플리케이션의 수명 동안 다시 사용됩니다. 모든 요청에 대해 `HttpClient` 클래스를 인스턴스화하면 과도한 부하에서 사용할 수 있는 소켓 수가 소진됩니다. 이 문제로 인해 `SocketException` 오류가 발생합니다. 이 문제를 해결하는 데 가능한 방법은 [HttpClient 사용에 관한 Microsoft 문서](../../../csharp/tutorials/console-webapiclient.md)에서 설명한 대로 `HttpClient` 개체를 싱글톤 또는 정적으로 만드는 것을 기반으로 합니다.

하지만 `HttpClient`에는 싱글톤 또는 정적 개체로 사용할 때 발생할 수 있는 두 번째 문제가 있습니다. 이 경우 dotnet/corefx GitHub 리포지토리에서 이 [문제](https://github.com/dotnet/corefx/issues/11224)에 대해 설명한 대로 싱글톤 또는 정적 `HttpClient`는 DNS 변경 내용을 따르지 않습니다. 

언급한 문제를 해결하고 `HttpClient` 인스턴스를 쉽게 관리하기 위해 .NET Core 2.1에는 Polly를 통합하여 복원력 있는 HTTP 호출을 구현하는 데 사용할 수도 있는 새로운 `HttpClientFactory`가 도입되었습니다.

[Polly](http://www.thepollyproject.org/)는 미리 정의된 정책을 사용하여 개발자가 흐름 및 스레드로부터 안전한 방식으로 애플리케이션에 복원력을 추가하는 데 도움이 되는 일시적인 오류 처리 라이브러리입니다.

## <a name="what-is-httpclientfactory"></a>HttpClientFactory란?

`HttpClientFactory`는 다음과 같이 설계되었습니다.

- 논리적 `HttpClient` 개체를 명명하고 구성하기 위한 중앙 위치를 제공합니다. 예를 들어 특정 마이크로 서비스에 액세스하도록 미리 구성된 클라이언트(서비스 에이전트)를 구성할 수 있습니다.
- `HttpClient`에서 처리기를 위임하고 Polly 기반 미들웨어를 구현하여 나가는 미들웨어에 대한 개념을 체계화하여 Polly의 복원력 정책을 활용합니다.
- `HttpClient`에는 나가는 HTTP 요청을 위해 함께 연결될 수 있는 처리기 위임이라는 개념이 이미 있습니다. HTTP 클라이언트를 팩터리에 등록하고, Polly 처리기를 사용하여 Polly 정책을 다시 시도, 회로 차단기 등에 사용할 수 있습니다.
- `HttpClientMessageHandlers`의 수명을 관리하여 `HttpClient` 수명을 직접 관리할 때 발생할 수 있는 언급된 문제를 방지합니다.

## <a name="multiple-ways-to-use-httpclientfactory"></a>HttpClientFactory를 사용하는 여러 가지 방법

애플리케이션에서 `HttpClientFactory`를 사용할 수 있는 몇 가지 방법은 다음과 같습니다.

- `HttpClientFactory` 직접 사용
- 명명된 클라이언트 사용
- 형식화된 클라이언트 사용
- 생성된 클라이언트 사용

간단히 하기 위해 이 지침에서는 `HttpClientFactory`를 사용하는 가장 구조적인 방법, 즉 형식화된 클라이언트(서비스 에이전트 패턴)를 사용하는 방법을 보여줍니다. 그러나 모든 옵션이 현재 [HttpClientFactory 사용에 대한 이 문서](/aspnet/core/fundamentals/http-requests#consumption-patterns)에 설명되어 있습니다.

## <a name="how-to-use-typed-clients-with-httpclientfactory"></a>형식화된 클라이언트를 HttpClientFactory에 사용하는 방법

그렇다면 “형식화된 클라이언트”란 무엇일까요? `DefaultHttpClientFactory`에 의해 삽입 시 구성되는 `HttpClient`입니다.

다음 다이어그램은 `HttpClientFactory`와 함께 형식화된 클라이언트를 사용하는 방법을 보여 줍니다.

![ClientService(컨트롤러 또는 클라이언트 코드에서 사용됨)는 등록된 IHttpClientFactory에서 만든 HttpClient를 사용합니다. 이 팩터리는 관리하는 풀의 HttpMessageHandler를 HttpClient에 할당합니다. 확장 메서드 AddHttpClient를 사용하여 DI 컨테이너에 IHttpClientFactory를 등록할 때 Polly의 정책을 사용하여 HttpClient를 구성할 수 있습니다.](./media/image3.5.png)

**그림 8-4**. 형식화된 클라이언트 클래스와 함께 HttpClientFactory 사용

먼저 `IServiceCollection`용 `AddHttpClient()` 확장 메서드를 포함하는 `Microsoft.Extensions.Http` NuGet 패키지를 설치하여 애플리케이션에서 `HttpClientFactory`를 설정합니다. 이 확장 메서드는 `IHttpClientFactory` 인터페이스에 대한 싱글톤으로 사용할 `DefaultHttpClientFactory`를 등록하고, `HttpMessageHandlerBuilder`에 대한 일시적인 구성을 정의합니다. 풀에서 가져온 이 메시지 처리기(`HttpMessageHandler` 개체)는 팩터리에서 반환된 `HttpClient`에서 사용합니다.

다음 코드에서는 `AddHttpClient()`를 사용하여 `HttpClient`를 사용해야 하는 형식화된 클라이언트(서비스 에이전트)를 등록하는 방법을 확인할 수 있습니다.

```csharp
// Startup.cs
//Add http client services at ConfigureServices(IServiceCollection services) 
services.AddHttpClient<ICatalogService, CatalogService>();
services.AddHttpClient<IBasketService, BasketService>();
services.AddHttpClient<IOrderingService, OrderingService>();
```

이전 코드에 표시된 대로 클라이언트 서비스를 등록하면 `DefaultClientFactory`에서 각 서비스에 대한 표준 `HttpClient`를 만듭니다.

또한 다음 코드와 같이 등록에 예를 들어 기준 주소를 구성하고 일부 복원력 정책을 추가하기 위한 인스턴스 관련 구성을 추가할 수도 있습니다.

```csharp
services.AddHttpClient<ICatalogService, CatalogService>(client =>
{
    client.BaseAddress = new Uri(Configuration["BaseUrl"])
})
    .AddPolicyHandler(GetRetryPolicy())
    .AddPolicyHandler(GetCircuitBreakerPolicy());
```

예를 들어 다음 코드에서는 위의 정책 중 하나를 볼 수 있습니다.

```csharp
static IAsyncPolicy<HttpResponseMessage> GetRetryPolicy()
{
    return HttpPolicyExtensions
        .HandleTransientHttpError()
        .OrResult(msg => msg.StatusCode == System.Net.HttpStatusCode.NotFound)
        .WaitAndRetryAsync(6, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
}
```

[다음 문서](implement-http-call-retries-exponential-backoff-polly.md)에서 Polly 사용에 대한 자세한 내용을 확인할 수 있습니다.

### <a name="httpclient-lifetimes"></a>HttpClient 수명

`IHttpClientFactory`에서 `HttpClient` 개체를 가져올 때마다 새 인스턴스가 반환됩니다. 그러나 `HttpMessageHandler`의 수명이 만료되지 않은 한, 각 `HttpClient`는 `IHttpClientFactory`에 의해 풀링되어 다시 사용되는 `HttpMessageHandler`를 사용하여 리소스 사용량을 줄입니다.

각 처리기가 일반적으로 자체 기본 HTTP 연결을 관리하고 필요 이상으로 처리기를 만드는 것은 연결 지연을 발생시킬 수 있으므로 처리기의 풀링이 바람직합니다. 또한 일부 처리기는 무한정으로 연결을 열어 놓아 처리기가 DNS 변경에 대응하는 것을 방지할 수 있습니다.

풀의 `HttpMessageHandler` 개체에는 수명이 있으며, 이 수명은 풀의 `HttpMessageHandler` 인스턴스를 다시 사용할 수 있는 기간입니다. 기본값은 2분이지만, 형식화된 클라이언트별로 재정의할 수 있습니다. 재정의하려면 다음 코드와 같이 클라이언트를 만들 때 반환되는 `IHttpClientBuilder`에서 `SetHandlerLifetime()`을 호출합니다.

```csharp
//Set 5 min as the lifetime for the HttpMessageHandler objects in the pool used for the Catalog Typed Client 
services.AddHttpClient<ICatalogService, CatalogService>()
    .SetHandlerLifetime(TimeSpan.FromMinutes(5));
```

클라이언트마다 고유하게 구성된 처리기 수명 값이 있을 수 있습니다. 처리기 만료를 사용하지 않도록 설정하려면 수명을 `InfiniteTimeSpan`으로 설정합니다.

### <a name="implement-your-typed-client-classes-that-use-the-injected-and-configured-httpclient"></a>삽입되고 구성된 HttpClient를 사용하는 형식화된 클라이언트 클래스 구현

앞의 단계와 같이 샘플 코드의 클래스(예: ‘BasketService’, ‘CatalogService’, ‘OrderingService’ 등)와 같은 형식화된 클라이언트 클래스를 정의해야 합니다. 형식화된 클라이언트는 생성자를 통해 삽입된 `HttpClient` 개체를 수락하고, 이를 사용하여 일부 원격 HTTP 서비스를 호출하는 클래스입니다. 예:

```csharp
public class CatalogService : ICatalogService
{
    private readonly HttpClient _httpClient;
    private readonly string _remoteServiceBaseUrl;

    public CatalogService(HttpClient httpClient)
    {
        _httpClient = httpClient;
    }

    public async Task<Catalog> GetCatalogItems(int page, int take, 
                                               int? brand, int? type)
    {
        var uri = API.Catalog.GetAllCatalogItems(_remoteServiceBaseUrl, 
                                                 page, take, brand, type);

        var responseString = await _httpClient.GetStringAsync(uri);

        var catalog = JsonConvert.DeserializeObject<Catalog>(responseString);
        return catalog;
    }
}
```

형식화된 클라이언트(예제에서는 CatalogService)는 DI(종속성 삽입)를 통해 활성화됩니다. 즉, HttpClient 외에도 생성자에서 등록된 모든 서비스를 허용할 수 있습니다.

형식화된 클라이언트는 실제로 임시 개체입니다. 즉, 필요할 때마다 새 인스턴스가 만들어지고, 생성될 때마다 새 `HttpClient` 인스턴스를 받게 됩니다. 그러나 풀의 HttpMessageHandler 개체는 여러 Http 요청에서 다시 사용되는 개체입니다.

### <a name="use-your-typed-client-classes"></a>형식화된 클라이언트 클래스 사용

마지막으로, 형식화된 클래스를 구현하고 `AddHttpClient()`에 등록한 후에는 DI를 사용하여 서비스를 삽입할 수 있는 위치에서 해당 클래스를 사용할 수 있습니다. 예를 들어 eShopOnContainers의 다음 코드와 같이 MVC 웹 앱 컨트롤러 또는 Razor 페이지 코드에서 사용할 수 있습니다.

```csharp
namespace Microsoft.eShopOnContainers.WebMVC.Controllers
{
    public class CatalogController : Controller
    {
        private ICatalogService _catalogSvc;

        public CatalogController(ICatalogService catalogSvc) =>
                                                           _catalogSvc = catalogSvc;

        public async Task<IActionResult> Index(int? BrandFilterApplied,
                                               int? TypesFilterApplied,
                                               int? page,
                                               [FromQuery]string errorMsg)
        {
            var itemsPage = 10;
            var catalog = await _catalogSvc.GetCatalogItems(page ?? 0,
                                                            itemsPage,
                                                            BrandFilterApplied,
                                                            TypesFilterApplied);
            //… Additional code
        }

        }
}
```

이 시점까지 보여 준 코드는 정기적인 HTTP 요청만 수행하는 것이지만, 다음 섹션에서는 정책을 추가하고, 등록된 형식화된 클라이언트에 처리기를 위임하여 `HttpClient`에서 수행할 모든 HTTP 요청을 처리하는 ‘마법 같은 일’이 펼쳐집니다. 이 과정에서 지수 백오프를 사용하는 다시 시도, 회로 차단기 또는 다른 사용자 지정 위임 처리기와 같은 복원력 정책을 고려하여 인증 토큰 사용, 기타 사용자 지정 기능 등의 추가 보안 기능을 구현합니다.

## <a name="additional-resources"></a>추가 자료

- **.NET Core에서 HttpClientFactory 사용** \
  [https://docs.microsoft.com/aspnet/core/fundamentals/http-requests](/aspnet/core/fundamentals/http-requests)

- **HttpClientFactory GitHub 리포지토리** \
  <https://github.com/aspnet/Extensions/tree/master/src/HttpClientFactory>

- **Polly(.NET 복원력 및 transient-fault-handling 라이브러리)**  \
  <http://www.thepollyproject.org/>

>[!div class="step-by-step"]
>[이전](explore-custom-http-call-retries-exponential-backoff.md)
>[다음](implement-http-call-retries-exponential-backoff-polly.md)
