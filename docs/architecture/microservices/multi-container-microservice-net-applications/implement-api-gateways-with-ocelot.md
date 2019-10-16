---
title: Ocelot을 사용하여 API 게이트웨이 구현
description: Ocelot을 사용하여 API 게이트웨이를 구현하는 방법과 컨테이너 기반 환경에서 Ocelot을 사용하는 방법을 알아봅니다.
ms.date: 10/02/2018
ms.openlocfilehash: 2a1c7b0f4baa979864ac32d555f65397531884b8
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68676190"
---
# <a name="implement-api-gateways-with-ocelot"></a>Ocelot을 사용하여 API 게이트웨이 구현

[eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers)에서는 eShopOnContainers에서 사용되는 다음 환경과 같이 마이크로 서비스/컨테이너와 함께 어디서나 배포할 수 있는 간단하고 가벼운 API 게이트웨이이므로 참조 마이크로 서비스 애플리케이션인 [Ocelot](https://github.com/ThreeMammals/Ocelot)을 사용합니다.

- 로컬 개발 PC, 온-프레미스 또는 클라우드에 있는 Docker 호스트
- 온-프레미스 또는 관리되는 클라우드(예: AKS(Azure Kubernetes Service))에 있는 Kubernetes 클러스터
- 온-프레미스 또는 클라우드에 있는 Service Fabric 클러스터
- Azure에 있는 Service Fabric 메시(예: PaaS/Serverless)

## <a name="architect-and-design-your-api-gateways"></a>API 게이트웨이 구성 및 설계

다음 아키텍처 다이어그램에서는 eShopOnContainers에서 Ocelot을 사용하여 API 게이트웨이를 구현하는 방법을 보여 줍니다.

![사이에 있는 클라이언트 응용 프로그램, 마이크로 서비스 및 API 게이트웨이를 보여 주는 eShopOnContainers 아키텍처 다이어그램](./media/image28.png)

**그림 6-28** API 게이트웨이가 있는 eShopOnContainers 아키텍처

이 다이어그램에서는 "Windows용 Docker" 또는 "Mac용 Docker"를 사용하여 전체 애플리케이션을 단일 Docker 호스트 또는 개발 PC에 배포하는 방법을 보여 줍니다. 그러나 모든 오케스트레이터에 배포하는 것은 매우 비슷하지만, 다이어그램의 모든 컨테이너는 오케스트레이터에서 확장할 수 있습니다.

또한 데이터베이스, 캐시 및 메시지 broker와 같은 인프라 자산을 오케스트레이터에서 오프로드하여 인프라용 고가용성 시스템(예: Azure SQL Database, Azure Cosmos DB, Azure Redis, Azure Service Bus 또는 온-프레미스의 모든 HA 클러스터링 솔루션)에 배포해야 합니다.

다이어그램에서 알 수 있듯이 여러 API 게이트웨이를 사용하면 마이크로 서비스와 관련 API 게이트웨이를 개발하고 배포할 때 여러 개발 팀에서 자율적으로 운영할 수 있습니다(이 경우 마케팅 기능 대 쇼핑 기능).

단일 모놀리식 API 게이트웨이가 있으면 여러 개발 팀에서 단일 지점을 업데이트해야 하므로 모든 마이크로 서비스를 애플리케이션의 단일 부분으로 연결할 수 있습니다.

설계 측면에서 더 나아가, 때로는 세분화된 API 게이트웨이가 선택한 아키텍처에 따라 단일 비즈니스 마이크로 서비스로 제한될 수도 있습니다. API 게이트웨이의 경계가 비즈니스 또는 도메인에 의해 결정되면 더 나은 디자인을 얻는 데 도움이 됩니다.

예를 들어, 세분화된 API 게이트웨이 계층의 개념은 UI 컴퍼지션 서비스와 비슷하므로 세분화된 API 게이트웨이 계층은 마이크로 서비스 기반의 향상된 복합 UI 애플리케이션에 특히 유용할 수 있습니다.

자세한 내용은 이전 섹션 [마이크로 서비스 기반 복합 UI 만들기](../architect-microservice-container-applications/microservice-based-composite-ui-shape-layout.md)에서 자세히 살펴봅니다.

중요한 사항으로, 많은 중대형 애플리케이션의 경우 사용자 지정 API 게이트웨이 제품을 사용하는 것이 일반적으로 좋은 방법이지만, API 게이트웨이에서 자치 마이크로 서비스를 만드는 여러 개발 팀에 독립적인 여러 구성 영역을 허용하지 않는 한 단일 모놀리식 집계 또는 고유한 사용자 지정 중앙 API 게이트웨이가 아닙니다.

### <a name="sample-microservicescontainers-to-re-route-through-the-api-gateways"></a>API 게이트웨이를 통해 다시 라우팅하는 마이크로 서비스/컨테이너 샘플

예를 들어 eShopOnContainers에는 다음 이미지와 같이 API 게이트웨이를 통해 게시되어야 하는 약 6개의 내부 마이크로 서비스 형식이 있습니다.

![장바구니, 카탈로그, 위치, 마케팅, 주문 및 결제 마이크로 서비스는 API 게이트웨이를 통해서만 게시됩니다.](./media/image29.png)

**그림 6-29** Visual Studio에서 eShopOnContainers 솔루션의 마이크로 서비스 폴더

ID 서비스에 대한 설계에서 이 서비스는 시스템에서 유일한 교차 편집 문제이므로 API 게이트웨이 라우팅에서 빠져 있지만 Ocelot을 사용하면 재라우팅 목록의 일부로 포함할 수도 있습니다.

코드에서 알 수 있듯이 이러한 모든 서비스는 현재 ASP.NET Core Web API 서비스로 구현되어 있습니다. Catalog 마이크로 서비스 코드와 같은 마이크로 서비스 중 하나에 집중하여 살펴보겠습니다.

![Catalog.API 프로젝트의 솔루션 탐색기 보기](./media/image30.png)

**그림 6-30** Web API 마이크로 서비스(Catalog 마이크로 서비스) 샘플

Catalog(카탈로그) 마이크로 서비스는 다음 코드와 같은 몇 가지 컨트롤러와 메서드가 있는 일반적인 ASP.NET Core Web API 프로젝트임을 알 수 있습니다.

```csharp
[HttpGet]
[Route("items/{id:int}")]
[ProducesResponseType((int)HttpStatusCode.BadRequest)]
[ProducesResponseType((int)HttpStatusCode.NotFound)]
[ProducesResponseType(typeof(CatalogItem),(int)HttpStatusCode.OK)]
public async Task<IActionResult> GetItemById(int id)
{
    if (id <= 0)
    {
        return BadRequest();
    }
    var item = await _catalogContext.CatalogItems.
                                          SingleOrDefaultAsync(ci => ci.Id == id);
    //…

    if (item != null)
    {
        return Ok(item);
    }
    return NotFound();
}
```

HTTP 요청은 마이크로 서비스 데이터베이스에 액세스하는 종류의 C# 코드 및 필수 추가 작업을 실행하게 됩니다.

마이크로 서비스 URL과 관련하여 컨테이너가 로컬 개발 PC(로컬 Docker 호스트)에 배포되면 각 마이크로 서비스의 컨테이너에는 항상 다음 dockerfile과 같이 docker 파일에 지정된 내부 포트(일반적으로 포트 80)가 포함됩니다.

```Dockerfile
FROM microsoft/aspnetcore:2.0.5 AS base
WORKDIR /app
EXPOSE 80
```

코드에 표시된 포트 80은 Docker 호스트 내부에 있으므로 클라이언트 앱에서 연결할 수 없습니다.

클라이언트 앱은 `docker-compose`를 사용하여 배포할 때 게시된 외부 포트(있는 경우)에만 액세스할 수 있습니다.

프로덕션 환경에 배포하는 경우 이러한 외부 포트는 게시되지 않아야 합니다. 이는 정확히 클라이언트 응용 프로그램과 마이크로 서비스 간의 직접 통신을 방지하기 위해 API 게이트웨이를 사용하려는 이유입니다.

그러나 개발하는 경우에는 마이크로 서비스/컨테이너에 직접 액세스하여 Swagger를 통해 실행하려고 합니다. 이로 인해 eShopOnContainers에서 외부 포트는 API 게이트웨이 또는 클라이언트 응용 프로그램에서 사용되지 않는 경우에도 계속 지정됩니다.

Catalog 마이크로 서비스에 대한 `docker-compose.override.yml` 파일의 예제는 다음과 같습니다.

```yml
catalog.api:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - ASPNETCORE_URLS=http://0.0.0.0:80
    - ConnectionString=YOUR_VALUE
    - ... Other Environment Variables
  ports:
    - "5101:80"   # Important: In a production environment you should remove the external port (5101) kept here for microservice debugging purposes.
                  # The API Gateway redirects and access through the internal port (80).
```

docker-compose.override.yml 구성에서 Catalog 컨테이너에 대한 내부 포트는 80 포트이지만 외부 액세스에 대한 포트가 5101임을 알 수 있습니다. 그러나 이 포트는 API 게이트웨이를 사용할 때 애플리케이션에서 사용할 수 없으며, Catalog 마이크로 서비스만 디버그, 실행 및 테스트할 뿐입니다.

일반적으로 마이크로 서비스에 적합한 프로덕션 배포 환경은 Kubernetes 또는 Service Fabric과 같은 오케스트레이터이므로 docker-compose를 사용하여 프로덕션 환경에 배포하지 않습니다. 이러한 환경에 배포하는 경우에는 마이크로 서비스용 외부 포트를 직접 게시하지 않는 다른 구성 파일을 사용하지만 항상 API 게이트웨이로부터 역방향 프록시를 사용합니다.

Visual Studio에서 eShopOnContainers 솔루션 전체를 실행하거나(docker-compose 파일의 모든 서비스를 실행함), `docker-compose.yml` 및 docker-compose.override.yml이 배치된 폴더에 있는 CMD 또는 PowerShell에서 다음 docker-compose 명령으로 Catalog 마이크로 서비스를 시작하여 로컬 Docker 호스트에서 카탈로그 마이크로 서비스를 실행합니다.

```console
docker-compose run --service-ports catalog.api
```

이 명령은 catalog.api 서비스 컨테이너와 docker-compose.yml에 지정된 종속성만 실행합니다. 이 경우 SQL Server 컨테이너와 RabbitMQ 컨테이너가 있습니다.

그런 다음, 카탈로그 마이크로 서비스에 직접 액세스하고 해당 "외부" 포트(이 경우 `http://localhost:5101/swagger`)를 통해 직접 액세스하는 Swagger UI를 통해 해당 메서드를 볼 수 있습니다.

![Catalog.API REST API에 대한 Swagger UI 기간의 브라우저 보기.](./media/image31.png)

**그림 6-31** Swagger UI를 사용하여 Catalog 마이크로 서비스 테스트

이 시점에서 Visual Studio에서 C# 코드에 중단점을 설정하고, Swagger UI에 노출된 메서드를 사용하여 마이크로 서비스를 테스트한 다음, 마지막으로 `docker-compose down` 명령을 사용하여 모든 항목을 정리할 수 있습니다.

그러나 5101 외부 포트를 통한 경우 마이크로 서비스에 대한 직접 액세스 통신은 정확히 애플리케이션에서 방지하려는 내용입니다. 그리고 API 게이트웨이(이 경우 Ocelot)의 간접 참조에 대한 추가 수준을 설정하여 이를 방지할 수 있습니다. 클라이언트 응용 프로그램은 이러한 방식으로 마이크로 서비스에 직접 액세스하지 않습니다.

## <a name="implementing-your-api-gateways-with-ocelot"></a>Ocelot을 사용하여 API 게이트웨이 구현

Ocelot은 기본적으로 특정 순서로 적용할 수 있는 일단의 미들웨어입니다.

Ocelot은 ASP.NET Core에서만 작동하도록 설계되었습니다. .NET Core 2.0 런타임 및 .NET Framework 4.6.1 런타임 이상이 포함된 .NET Standard 2.0이 지원되는 곳이면 어디서나 사용할 수 있도록 netstandard2.0을 대상으로 합니다.

Visual Studio에서 [Ocelot의 NuGet 패키지](https://www.nuget.org/packages/Ocelot/)를 사용하여 ASP.NET Core 프로젝트에 Ocelot 및 해당 종속성을 설치합니다.

```powershell
Install-Package Ocelot
```

eShopOnContainers에서 API 게이트웨이 구현은 간단한 ASP.NET Core WebHost 프로젝트이며, Ocelot의 미들웨어에서 다음 이미지와 같이 모든 API 게이트웨이 기능을 처리합니다.

![Ocelot API 게이트웨이 프로젝트의 솔루션 탐색기 보기](./media/image32.png)

**그림 6-32** eShopOnContainers의 OcelotApiGw 기본 프로젝트

이 ASP.NET Core WebHost 프로젝트는 기본적으로 간단한 두 개의 파일(`Program.cs` 및 `Startup.cs`)로 빌드됩니다.

Program.cs는 일반적인 ASP.NET Core BuildWebHost를 만들고 구성하기만 하면 됩니다.

```csharp
namespace OcelotApiGw
{
    public class Program
    {
        public static void Main(string[] args)
        {
            BuildWebHost(args).Run();
        }

        public static IWebHost BuildWebHost(string[] args)
        {
            var builder = WebHost.CreateDefaultBuilder(args);

            builder.ConfigureServices(s => s.AddSingleton(builder))
                    .ConfigureAppConfiguration(
                          ic => ic.AddJsonFile(Path.Combine("configuration",
                                                            "configuration.json")))
                    .UseStartup<Startup>();
            var host = builder.Build();
            return host;
        }
    }
}
```

여기서 Ocelot에 대해 중요한 점은 `AddJsonFile()` 메서드를 통해 작성기에 제공해야 하는 `configuration.json` 파일입니다. 이 `configuration.json`은 모든 API 게이트웨이 ReRoutes를 지정하는 곳입니다. 특정 포트가 있는 외부 엔드포인트 및 상관 관계가 있는 내부 엔드포인트를 의미하며, 일반적으로 서로 다른 포트를 사용합니다.

```json
{
    "ReRoutes": [],
    "GlobalConfiguration": {}
}
```

구성에는 재라우팅(Re-Routes) 배열과 GlobalConfiguration(전역 구성)의 두 가지 섹션이 있습니다. 재라우팅은 업스트림 요청을 처리하는 방법을 Ocelot에 알려주는 개체입니다. 전역 구성을 사용하면 재라우팅 특정 설정을 재정의할 수 있습니다. 이는 많은 재라우팅 특정 설정을 관리하지 않으려는 경우에 유용합니다.

eShopOnContainers의 API 게이트웨이 중 하나에 있는 [ReRoute 구성 파일](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/ApiGateways/Web.Bff.Shopping/apigw/configuration.json)을 간단히 보여주는 예제는 다음과 같습니다.

```json
{
  "ReRoutes": [
    {
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "catalog.api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/c/{everything}",
      "UpstreamHttpMethod": [ "POST", "PUT", "GET" ]
    },
    {
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "basket.api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/b/{everything}",
      "UpstreamHttpMethod": [ "POST", "PUT", "GET" ],
      "AuthenticationOptions": {
        "AuthenticationProviderKey": "IdentityApiKey",
        "AllowedScopes": []
      }
    }

  ],
    "GlobalConfiguration": {
      "RequestIdKey": "OcRequestId",
      "AdministrationPath": "/administration"
    }
  }
```

Ocelot API 게이트웨이의 주요 기능은 들어오는 HTTP 요청을 가져오고, 현재 다른 HTTP 요청으로 다운스트림 서비스에 전달하는 것입니다. Ocelot은 한 요청에서 다른 요청으로의 라우팅을 재라우팅(Re-Route)으로 설명합니다.

예를 들어 위의 configuration.json에 있는 재라우팅 중 하나인 Basket(장바구니) 마이크로 서비스의 구성에 집중하여 살펴보겠습니다.

```json
{
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "basket.api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/b/{everything}",
      "UpstreamHttpMethod": [ "POST", "PUT", "GET" ],
      "AuthenticationOptions": {
        "AuthenticationProviderKey": "IdentityApiKey",
        "AllowedScopes": []
      }
}
```

DownstreamPathTemplate, Scheme 및 DownstreamHostAndPorts는 이 요청이 전달되는 내부 마이크로 서비스 URL을 만듭니다.

포트는 서비스에서 사용하는 내부 포트입니다. 컨테이너를 사용하는 경우 포트는 dockerfile에 지정됩니다.

`Host`는 사용하는 서비스 이름 확인에 따라 달라지는 서비스 이름입니다. docker-compose를 사용하는 경우 서비스 이름은 docker-compose 파일에 제공된 서비스 이름을 사용하는 Docker 호스트에서 제공합니다. Kubernetes 또는 Service Fabric과 같은 오케스트레이터를 사용하는 경우 해당 이름은 각 오케스트레이터에서 제공한 DNS 또는 이름 확인을 통해 확인해야 합니다.

DownstreamHostAndPorts는 요청을 전달하려는 모든 다운스트림 서비스의 호스트와 포트를 포함하는 배열입니다. 일반적으로 이 배열에는 하나의 항목만 포함되지만, 때로는 요청의 부하를 다운스트림 서비스에 분산하려는 경우가 있으며 Ocelot을 사용하면 둘 이상의 항목을 추가한 다음, 부하 분산 장치를 선택할 수 있습니다. 그러나 Azure와 모든 오케스트레이터를 사용하는 경우 클라우드 및 오케스트레이터 인프라의 부하를 분산하는 것이 좋습니다.

UpstreamPathTemplate은 Ocelot에서 클라이언트로부터 지정된 요청에 사용할 DownstreamPathTemplate을 식별하는 데 사용할 URL입니다. 마지막으로, Ocelot에서 동일한 URL에 대한 다른 요청(GET, POST, PUT)을 구별할 수 있도록 UpstreamHttpMethod를 사용합니다.

이 시점에서 하나 또는 여러 개의 [병합된 configuration.json 파일](https://ocelot.readthedocs.io/en/latest/features/configuration.html#merging-configuration-files)을 사용하여 단일 Ocelot API 게이트웨이(ASP.NET Core WebHost)를 만들거나 [Consul KV 저장소에 구성을 저장](https://ocelot.readthedocs.io/en/latest/features/configuration.html#store-configuration-in-consul)할 수도 있습니다.

그러나 구성 및 설계 섹션에서 소개한 대로 자치 마이크로 서비스를 실제로 원하는 경우, 단일 모놀리식 API 게이트웨이를 여러 API 게이트웨이 및/또는 BFF(프런트 엔드에 대한 백 엔드)로 분할하는 것이 좋습니다. 이를 위해 Docker 컨테이너를 사용하여 이 방법을 구현하는 방법을 살펴보겠습니다.

### <a name="using-a-single-docker-container-image-to-run-multiple-different-api-gateway--bff-container-types"></a>단일 Docker 컨테이너 이미지를 사용하여 별도의 여러 API 게이트웨이/BFF 컨테이너 유형 실행

eShopOnContainers에서 Ocelot API 게이트웨이를 사용하여 단일 Docker 컨테이너 이미지를 사용하지만, 실행 시 각 서비스에 다른 PC 폴더에 액세스하기 위해 Docker 볼륨을 사용하는 다른 configuration.json 파일을 제공하여 각 형식의 API-Gateway/BFF에 대해 다른 서비스/컨테이너를 만듭니다.

![Ocelot API 게이트웨이의 단일 Docker 이미지는 4개의 모든 API 게이트웨이에 사용됩니다.](./media/image33.png)

**그림 6-33** 여러 API 게이트웨이 형식에서 단일 Ocelot Docker 이미지 재사용

eShopOnContainers에서는 "OcelotApiGw"라는 프로젝트와 docker-compose.yml 파일에 지정된 "eshop/ocelotapigw" 이미지 이름을 사용하여 "제네릭 Ocelot API 게이트웨이 Docker 이미지"가 만들어집니다. 그런 다음, Docker에 배포하면 docker-compose.yml 파일에서 나오는 다음 추출과 같이 동일한 Docker 이미지에서 만들어진 네 개의 API 게이트웨이 컨테이너가 있습니다.

```yml
  mobileshoppingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile

  mobilemarketingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile

  webshoppingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile

  webmarketingapigw:
    image: eshop/ocelotapigw:${TAG:-latest}
    build:
      context: .
      dockerfile: src/ApiGateways/ApiGw-Base/Dockerfile
```

또한 다음 docker-compose.override.yml 파일에서 볼 수 있듯이 이러한 API 게이트웨이 컨테이너 간의 유일한 차이점은 Ocelot 구성 파일입니다. 이 파일은 각 서비스 컨테이너마다 다르며, 런타임 시 Docker 볼륨을 통해 지정됩니다.

```yml
mobileshoppingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity.api
  ports:
    - "5200:80"
  volumes:
    - ./src/ApiGateways/Mobile.Bff.Shopping/apigw:/app/configuration

mobilemarketingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity.api
  ports:
    - "5201:80"
  volumes:
    - ./src/ApiGateways/Mobile.Bff.Marketing/apigw:/app/configuration

webshoppingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity.api
  ports:
    - "5202:80"
  volumes:
    - ./src/ApiGateways/Web.Bff.Shopping/apigw:/app/configuration

webmarketingapigw:
  environment:
    - ASPNETCORE_ENVIRONMENT=Development
    - IdentityUrl=http://identity.api
  ports:
    - "5203:80"
  volumes:
    - ./src/ApiGateways/Web.Bff.Marketing/apigw:/app/configuration
```

앞의 코드와 아래의 Visual Studio 탐색기에서 보여 주듯이 네 개의 API 게이트웨이가 동일한 Docker 이미지를 기반으로 하므로 각 특정 비즈니스/BFF API 게이트웨이를 정의하는 데 필요한 유일한 파일은 configuration.json 파일뿐입니다.

![모든 API 게이트웨이 간의 유일한 차이점은 각각의 configuration.json 파일입니다.](./media/image34.png)

**그림 6-34** Ocelot을 사용하여 각 API 게이트웨이/BFF를 정의하는 데 필요한 유일한 구성 파일

API 게이트웨이를 여러 API 게이트웨이로 분할하면 마이크로 서비스의 여러 하위 집합에 집중하는 여러 개발 팀에서 독립적인 Ocelot 구성 파일을 사용하여 자신의 API 게이트웨이를 관리할 수 있습니다. 이와 동시에 Ocelot Docker 이미지를 다시 사용할 수 있습니다.

이제 API 게이트웨이(eShopOnContainers-ServicesAndWebApps.sln 솔루션을 열거나 "docker-compose up"을 실행하는 경우 기본적으로 VS에 포함됨)를 사용하여 eShopOnContainers를 실행하면 다음과 같은 샘플 경로가 수행됩니다.

예를 들어 webshoppingapigw API 게이트웨이에서 제공하는 업스트림 URL(`http://localhost:5202/api/v1/c/catalog/items/2/`)을 방문하면 다음 브라우저와 같이 Docker 호스트 내의 내부 다운스트림 URL(`http://catalog.api/api/v1/2`)에서 동일한 결과를 가져옵니다.

![API 게이트웨이를 통해 이동하는 Catalog.api 응답의 브라우저 보기](./media/image35.png)

**그림 6-35** API 게이트웨이에서 제공하는 URL을 통해 마이크로 서비스에 액세스

테스트 또는 디버깅 이유로 인해 API 게이트웨이를 통과하지 않고 Catalog Docker 컨테이너에 직접 액세스하려는 경우(개발 환경에서만), 'catalog.api'는 Docker 호스트 내부의 DNS 확인(docker-compose 서비스 이름으로 처리되는 서비스 검색)이므로 컨테이너에 직접 액세스하는 유일한 방법은 다음 브라우저의 `http://localhost:5101/api/v1/Catalog/items/1`과 같이 개발 테스트용으로만 제공되는 docker-compose.override.yml에 게시된 외부 포트를 통해 액세스하는 것입니다.

![API 게이트웨이를 통한 응답과 동일한 Catalog.api에 직접 이동하는 Catalog.api 응답의 브라우저 보기](./media/image36.png)

**그림 6-36** 테스트 목적으로 마이크로 서비스에 직접 액세스

그러나 애플리케이션은 직접 포트 "바로 가기"가 아니라 API 게이트웨이를 통해 모든 마이크로 서비스에 액세스하도록 구성됩니다.

### <a name="the-gateway-aggregation-pattern-in-eshoponcontainers"></a>eShopOnContainers의 게이트웨이 집계 패턴

앞에서 설명한 대로 요청 집계를 구현하는 유연한 방법은 코드에서 사용자 지정 서비스를 사용하는 것입니다. 또한 [Ocelot의 요청 집계 기능](https://ocelot.readthedocs.io/en/latest/features/requestaggregation.html#request-aggregation)을 사용하여 요청 집계를 구현할 수 있지만 필요에 따라 유연하지 않을 수도 있습니다. 따라서 eShopOnContainers에서 집계를 구현하기 위해 선택한 방법은 각 집계에 대해 ASP.NET Core Web API 서비스를 사용하는 것입니다.

이 방법에 따르면 앞에서 표시된 간소화된 글로벌 아키텍처 다이어그램에 표시되지 않은 집계 서비스를 고려하면 API 게이트웨이 컴퍼지션 다이어그램은 실제로 조금 더 확대됩니다.

다음 다이어그램에서는 집계 서비스에서 관련 API 게이트웨이를 사용하는 방식도 확인할 수 있습니다.

![집계 서비스를 보여주는 eShopOnContainers 아키텍처](./media/image37.png)

**그림 6-37** 집계 서비스가 있는 eShopOnContainers 아키텍처

더 확대하면 다음 이미지의 "쇼핑" 비즈니스 영역에서 API 게이트웨이에서 수집기 서비스를 사용하는 경우 클라이언트 앱과 마이크로 서비스 간에 전송량이 감소되었음을 확인할 수 있습니다.

![수집기 서비스를 보여주는 eShopOnContainers 아키텍처 확대는 최종 클라이언트에서 전송량을 줄이기 위해 여러 마이크로 서비스의 응답을 "조인"하여 응답을 "어셈블"합니다.](./media/image38.png)

**그림 6-38** 집계 서비스의 비전 확대

다이어그램에 API 게이트웨이에서 들어오는 가능한 요청이 표시되는 경우 이는 매우 복잡해질 수 있습니다. 클라이언트 응용 프로그램 관점에서 청색 화살표가 간소화될 수 있는 방법을 알 수 있지만, 통신의 데이터 전송량과 대기 시간을 줄여 집계 패턴을 사용하는 경우 궁극적으로 특히 원격 응용 프로그램(모바일 및 SPA 응용 프로그램)의 사용자 환경이 크게 향상됩니다.

"마케팅" 비즈니스 영역 및 마이크로 서비스의 경우 매우 간단한 사용 사례이므로 집계를 사용할 필요는 없지만 필요한 경우 사용할 수도 있습니다.

### <a name="authentication-and-authorization-in-ocelot-api-gateways"></a>Ocelot API 게이트웨이의 인증 및 권한 부여

Ocelot API 게이트웨이에서 권한 부여 토큰을 제공하는 [IdentityServer](https://identityserver.io/)를 통해 API 게이트웨이 외부 또는 내부에 인증 서비스(예: ASP.NET Core Web API 서비스)를 배치할 수 있습니다.

eShopOnContainers는 BFF 및 비즈니스 영역에 따른 경계가 있는 여러 개의 API 게이트웨이를 사용하므로 다음 다이어그램에서 노란색으로 강조 표시된 대로 Identity/Auth(ID/권한 부여) 서비스는 API 게이트웨이에서 제외됩니다.

![API 게이트웨이 아래의 ID 마이크로 서비스를 보여주는 eShopOnContainers 아키텍처 다이어그램](./media/image39.png)

**그림 6-39** eShopOnContainers에서 Identity 서비스의 위치

그러나 Ocelot은 다른 다이어그램과 같이 API 게이트웨이 경계 내에 ID/인증 마이크로 서비스를 배치하도록 지원할 수도 있습니다.

![AG(API 게이트웨이) 아래의 ID 마이크로 서비스를 사용하여 인증: 1) AG는 ID 마이크로 서비스에서 인증 토큰을 요청하고, 2) ID 마이크로 서비스는 AG에 토큰을 반환하고, 3-4) AG는 인증 토큰을 사용하여 마이크로 서비스에서 요청합니다.](./media/image40.png)

**그림 6-40** Ocelot에서 인증

eShopOnContainers 애플리케이션에서 API 게이트웨이를 여러 BFF(프런트 엔드에 대한 백 엔드) 및 비즈니스 영역 API 게이트웨이로 분할했으므로 교차 편집 문제에 대한 추가 API 게이트웨이를 만드는 것이 또 다른 옵션이었습니다. 이 선택은 여러 교차 편집 문제 마이크로 서비스가 있는 더 복잡한 마이크로 서비스 기반 아키텍처에 적합합니다. eShopOnContainers에는 하나의 교차 편집 문제만 있으므로 간단히 하기 위해 API 게이트웨이 영역에서 보안 서비스를 처리하기로 결정했습니다.

어떤 경우이든 응용 프로그램이 API 게이트웨이 수준에서 보안이 설정되면 보안 마이크로 서비스를 사용하려고 할 때 Ocelot API 게이트웨이의 인증 모듈을 처음 방문합니다. 이렇게 하면 액세스 토큰을 가져오기 위해 Identity 또는 Auth 마이크로 서비스를 방문하도록 HTTP 요청을 리디렉션하므로 access_token으로 보호된 서비스를 방문할 수 있습니다.

API 게이트웨이 수준에서 인증을 통해 모든 서비스를 보호하는 방법은 configuration.json의 관련 설정에서 AuthenticationProviderKey를 설정하는 것입니다.

```json
    {
      "DownstreamPathTemplate": "/api/{version}/{everything}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "basket.api",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/api/{version}/b/{everything}",
      "UpstreamHttpMethod": [],
      "AuthenticationOptions": {
        "AuthenticationProviderKey": "IdentityApiKey",
        "AllowedScopes": []
      }
    }
```

Ocelot이 실행되면 AuthenticationOptions.AuthenticationProviderKey 재라우팅을 살펴보고 지정된 키에 등록된 인증 공급자가 있는지 확인합니다. 해당 공급자가 없는 경우 Ocelot이 시작되지 않습니다. 있는 경우 실행할 때 재라우팅에서 해당 공급자를 사용합니다.

Ocelot WebHost는 `authenticationProviderKey = "IdentityApiKey"`를 사용하여 구성되므로 권한 부여 토큰이 없는 요청이 서비스에 있을 때마다 인증이 필요합니다.

```csharp
namespace OcelotApiGw
{
    public class Startup
    {
        private readonly IConfiguration _cfg;

        public Startup(IConfiguration configuration) => _cfg = configuration;

        public void ConfigureServices(IServiceCollection services)
        {
            var identityUrl = _cfg.GetValue<string>("IdentityUrl");
            var authenticationProviderKey = "IdentityApiKey";
                         //…
            services.AddAuthentication()
                .AddJwtBearer(authenticationProviderKey, x =>
                {
                    x.Authority = identityUrl;
                    x.RequireHttpsMetadata = false;
                    x.TokenValidationParameters = new Microsoft.IdentityModel.Tokens.TokenValidationParameters()
                    {
                        ValidAudiences = new[] { "orders", "basket", "locations", "marketing", "mobileshoppingagg", "webshoppingagg" }
                    };
                });
            //...
        }
    }
}
```

그런 다음, 다음 Basket 마이크로 서비스 컨트롤러와 같이 마이크로 서비스처럼 액세스할 모든 리소스에 대해 [Authorize] 특성을 사용하여 권한 부여를 설정해야 합니다.

```csharp
namespace Microsoft.eShopOnContainers.Services.Basket.API.Controllers
{
    [Route("api/v1/[controller]")]
    [Authorize]
    public class BasketController : Controller
    {
      //...
    }
}
```

"basket"과 같은 ValidAudiences는 아래 코드와 같이 스타트업 클래스의 ConfigureServices()에서 `AddJwtBearer()`를 사용하여 각 마이크로 서비스에 정의된 대상과 상관 관계가 있습니다.

```csharp
// prevent from mapping "sub" claim to nameidentifier.
JwtSecurityTokenHandler.DefaultInboundClaimTypeMap.Clear();

var identityUrl = Configuration.GetValue<string>("IdentityUrl");

services.AddAuthentication(options =>
{
    options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;

}).AddJwtBearer(options =>
{
    options.Authority = identityUrl;
    options.RequireHttpsMetadata = false;
    options.Audience = "basket";
});
```

`http://localhost:5202/api/v1/b/basket/1`과 같은 API 게이트웨이를 기반으로 하는 재라우팅 URL을 사용하여 Basket 마이크로 서비스와 같은 보안 마이크로 서비스에 액세스하려고 할 때 유효한 토큰을 제공하지 않으면 401 권한이 없음이 표시됩니다. 반면에 재라우팅 URL이 인증되면 Ocelot에서 이(내부 마이크로 서비스 URL)와 연결된 다운스트림 구성표를 호출합니다.

**Ocelot의 재라우팅 계층에서 권한 부여**  Ocelot은 인증 후에 평가된 클레임 기반 권한 부여를 지원합니다. 재라우팅 구성에 다음 줄을 추가하여 경로 수준에서 권한 부여를 설정합니다.

```json
"RouteClaimsRequirement": {
    "UserType": "employee"
}
```

이 예제에서 권한 부여 미들웨어가 호출되면 Ocelot에서 사용자의 토큰에 'UserType' 클레임 유형이 있고 해당 클레임의 값이 'employee'인지 여부를 확인합니다. 그렇지 않은 경우 해당 사용자에게 권한이 부여되지 않으며 응답은 403 사용할 수 없음이 됩니다.

## <a name="using-kubernetes-ingress-plus-ocelot-api-gateways"></a>Kubernetes 수신 및 Ocelot API 게이트웨이 사용

Azure Kubernetes Service 클러스터에서처럼 Kubernetes를 사용하는 경우 일반적으로 *Nginx*를 기반으로 하는 [Kubernetes 수신 계층](https://kubernetes.io/docs/concepts/services-networking/ingress/)을 통해 모든 HTTP 요청을 통합합니다.

Kubernetes에서 수신 방식을 사용하지 않으면 서비스와 Pod에 클러스터 네트워크에서만 라우팅할 수 있는 IP가 있습니다.

하지만 수신 방식을 사용하는 경우 인터넷과 서비스(API 게이트웨이 포함) 사이에 역방향 프록시 역할을 하는 중간 계층이 있습니다.

정의에 따라 수신은 인바운드 연결이 클러스터 서비스에 도달할 수 있도록 하는 규칙 모음입니다. 수신은 일반적으로 외부에서 연결할 수 있는 URL, 부하 분산 트래픽, SSL 종료 등의 서비스를 제공하도록 구성됩니다. 사용자는 수신 리소스를 API 서버에 POST(게시)하여 수신을 요청합니다.

eShopOnContainers에서 로컬로 개발하고 개발 머신을 Docker 호스트로만 사용하는 경우 수신이 아니라 여러 API 게이트웨이만 사용합니다.

그러나 Kubernetes를 기반으로 한 “프로덕션” 환경을 대상으로 하는 경우 eShopOnContainers에서는 API 게이트웨이 앞에 수신을 사용합니다. 그러면 클라이언트에서 동일한 기본 URL을 계속 호출하지만 요청은 여러 API 게이트웨이 또는 BFF로 라우팅됩니다.

API 게이트웨이는 일반적으로 서비스 범위를 벗어나는 웹 애플리케이션이 아닌 서비스만 표시하는 프런트 엔드 또는 외관입니다. 또한 API 게이트웨이는 특정 내부 마이크로 서비스를 숨길 수 있습니다.

하지만 수신은 HTTP 요청만 리디렉션하고, 마이크로 서비스 또는 웹앱을 숨기려고 하지 않습니다.

다음 다이어그램과 같이 Kubernetes에서 웹 애플리케이션과 여러 Ocelot API 게이트웨이/BFF 앞에 수신 Nginx 계층이 있는 것이 이상적인 아키텍처입니다.

![Kubernetes 수신은 일반적으로 API 게이트웨이 범위를 벗어난 웹 애플리케이션을 비롯한 앱의 모든 트래픽에 대해 역방향 프록시로 작동합니다.](./media/image41.png)

**그림 6-41** Kubernetes에 배포 시 eShopOnContainers의 수신 계층

eShopOnContainers를 Kubernetes에 배포하면 _수신_을 통해 몇 가지 서비스 또는 엔드포인트만 노출되며, URL에 대한 접미사 목록은 기본적으로 다음과 같습니다.

- `/`: 클라이언트 SPA 웹 애플리케이션의 경우
- `/webmvc`: 클라이언트 MVC 웹 애플리케이션의 경우
- `/webstatus`: 상태/healthchecks를 표시하는 클라이언트 웹앱의 경우
- `/webshoppingapigw`: 웹 BFF 및 쇼핑 비즈니스 프로세스의 경우
- `/webmarketingapigw`: 웹 BFF 및 마케팅 비즈니스 프로세스의 경우
- `/mobileshoppingapigw`: 모바일 BFF 및 쇼핑 비즈니스 프로세스의 경우
- `/mobilemarketingapigw`: 모바일 BFF 및 마케팅 비즈니스 프로세스의 경우

Kubernetes에 배포하는 경우 각 Ocelot API 게이트웨이는 API 게이트웨이를 실행하는 각 _Pod_에 대해 서로 다른 "configuration.json" 파일을 사용합니다. 이러한 “configuration.json” 파일은 ‘ocelot’이라는 Kubernetes ‘구성 맵’에 따라 만들어진 볼륨을 탑재하여(원래는 deploy.ps1 스크립트 사용) 제공됩니다.  각 컨테이너는 `/app/configuration`이라는 컨테이너 폴더에 관련 구성 파일을 탑재합니다.

eShopOnContainers의 소스 코드 파일에서 원래 "configuration.json" 파일은 `k8s/ocelot/` 폴더 내에서 찾을 수 있습니다. 각 BFF/API 게이트웨이마다 하나의 구성 파일이 있습니다.

## <a name="additional-cross-cutting-features-in-an-ocelot-api-gateway"></a>Ocelot API 게이트웨이의 추가 교차 편집 기능

Ocelot API 게이트웨이를 사용하는 경우 연구하고 사용할 다른 중요한 기능이 있으며, 다음 링크에서 설명하고 있습니다.

- **Consul 또는 Eureka와 Ocelot을 통합한 클라이언트 쪽 서비스 검색** \
  <https://ocelot.readthedocs.io/en/latest/features/servicediscovery.html>

- **API 게이트웨이 계층에서 캐싱** \
  <https://ocelot.readthedocs.io/en/latest/features/caching.html>

- **API 게이트웨이 계층에서 로깅** \
  <https://ocelot.readthedocs.io/en/latest/features/logging.html>

- **API 게이트웨이 계층의 서비스 품질(다시 시도 및 회로 차단기)**  \
  <https://ocelot.readthedocs.io/en/latest/features/qualityofservice.html>

- **속도 제한** \
  [https://ocelot.readthedocs.io/en/latest/features/ratelimiting.html](https://ocelot.readthedocs.io/en/latest/features/ratelimiting.html )

> [!div class="step-by-step"]
> [이전](background-tasks-with-ihostedservice.md)
> [다음](../microservice-ddd-cqrs-patterns/index.md)
