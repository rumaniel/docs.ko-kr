---
title: docker-compose.yml을 사용하여 다중 컨테이너 애플리케이션 정의
description: docker-compose.yml을 사용하여 다중 컨테이너 애플리케이션에서 마이크로 서비스 컴퍼지션을 지정하는 방법입니다.
ms.date: 10/02/2018
ms.openlocfilehash: 8c0f1a654d27b32e613b84d3862198ad96f32e1c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039740"
---
# <a name="defining-your-multi-container-application-with-docker-composeyml"></a>docker-compose.yml을 사용하여 다중 컨테이너 애플리케이션 정의

이 가이드에서 [docker compose.yml](https://docs.docker.com/compose/compose-file/) 파일은 섹션 [4단계. 다중 컨테이너 Docker 애플리케이션을 빌드할 때 docker compose.yml 파일에서 서비스 정의](../docker-application-development-process/docker-app-development-workflow.md#step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application)에서 도입되었습니다. 그러나 더 자세히 살펴볼 가치가 있는 docker-compose 파일을 사용하는 다른 방법이 있습니다.

예를 들어 docker-compose.yml 파일에서 다중 컨테이너 애플리케이션을 배포하려는 방법을 명시적으로 설명할 수 있습니다. 필요에 따라 사용자 지정 Docker 이미지를 작성하려는 방법을 설명할 수도 있습니다. (사용자 지정 Docker 이미지는 Docker CLI를 사용하여 빌드될 수도 있습니다.)

기본적으로 배포하려는 각 컨테이너와 각 컨테이너 배포에 대한 특정 특성을 정의합니다. 다중 컨테이너 배포 설명 파일을 가지면 [docker-compose up](https://docs.docker.com/compose/overview/) CLI 명령으로 오케스트레이션된 단일 작업에서 전체 솔루션을 배포하거나 Visual Studio에서 투명하게 배포할 수 있습니다. 그렇지 않은 경우 명령 줄에서 `docker run` 명령을 사용하여 여러 단계에서 컨테이너별로 배포하는 Docker CLI를 사용해야 합니다. 따라서 docker-compose.yml에 정의된 각 서비스는 정확하게 하나의 이미지 또는 빌드를 지정해야 합니다. 다른 키는 선택 사항이며 `docker run` 명령줄 함수와 유사합니다.

다음 YAML 코드는 가능한 전역의 정의이며 eShopOnContainers 샘플에 대한 단일 docker-compose.yml 파일이 아닙니다. eShopOnContainers에서 실제 docker-compose 파일이 아닙니다. 대신 단일 파일에서 단순화되고 통합된 버전입니다. 나중에 설명되는 것처럼 docker-compose 파일을 사용하는 가장 좋은 방법이 아닙니다.

```yml
version: '3.4'

services:
  webmvc:
    image: eshop/webmvc
    environment:
      - CatalogUrl=http://catalog.api
      - OrderingUrl=http://ordering.api
      - BasketUrl=http://basket.api
    ports:
      - "5100:80"
    depends_on:
      - catalog.api
      - ordering.api
      - basket.api

  catalog.api:
    image: eshop/catalog.api
    environment:
      - ConnectionString=Server=sql.data;Initial Catalog=CatalogData;User Id=sa;Password=your@password
    expose:
      - "80"
    ports:
      - "5101:80"
    #extra hosts can be used for standalone SQL Server or services at the dev PC
    extra_hosts:
      - "CESARDLSURFBOOK:10.0.75.1"
    depends_on:
      - sql.data

  ordering.api:
    image: eshop/ordering.api
    environment:
      - ConnectionString=Server=sql.data;Database=Services.OrderingDb;User Id=sa;Password=your@password
    ports:
      - "5102:80"
    #extra hosts can be used for standalone SQL Server or services at the dev PC
    extra_hosts:
      - "CESARDLSURFBOOK:10.0.75.1"
    depends_on:
      - sql.data

  basket.api:
    image: eshop/basket.api
    environment:
      - ConnectionString=sql.data
    ports:
      - "5103:80"
    depends_on:
      - sql.data

  sql.data:
    environment:
      - SA_PASSWORD=your@password
      - ACCEPT_EULA=Y
    ports:
      - "5434:1433"

  basket.data:
    image: redis
```

이 파일의 루트 키는 서비스입니다. 해당 키 아래에서 `docker-compose up` 명령을 실행하거나 이 docker-compose.yml 파일을 사용하여 Visual Studio에서 배포할 때 배포 및 실행하려는 서비스를 정의합니다. 이 경우 docker-compose.yml 파일에는 다음 표에 설명된 대로 정의된 여러 서비스가 있습니다.

| 서비스 이름 | 설명 |
|--------------|-------------|
| webmvc       | 서버 쪽 C\#에서 마이크로 서비스를 사용하는 ASP.NET Core MVC 애플리케이션을 포함하는 컨테이너|
| catalog.api  | Catalog ASP.NET Core Web API 마이크로 서비스를 포함하는 컨테이너 |
| ordering.api | Ordering ASP.NET Core Web API 마이크로 서비스를 포함하는 컨테이너 |
| sql.data     | 마이크로 서비스 데이터베이스를 보유하는 Linux용 SQL Server를 실행하는 컨테이너 |
| basket.api   | Basket ASP.NET Core Web API 마이크로 서비스가 있는 컨테이너 |
| basket.data  | REDIS 캐시로 바구니 데이터베이스가 있는 REDIS 캐시 서비스를 실행하는 컨테이너 |

### <a name="a-simple-web-service-api-container"></a>단순한 Web Service API 컨테이너

단일 컨테이너에 집중하는 catalog.api 컨테이너 마이크로 서비스에는 간단한 정의가 있습니다.

```yml
  catalog.api:
    image: eshop/catalog.api
    environment:
      - ConnectionString=Server=sql.data;Initial Catalog=CatalogData;User Id=sa;Password=your@password
    expose:
      - "80"
    ports:
      - "5101:80"
    #extra hosts can be used for standalone SQL Server or services at the dev PC
    extra_hosts:
      - "CESARDLSURFBOOK:10.0.75.1"
    depends_on:
      - sql.data
```

이 컨테이너화된 서비스에는 다음과 같은 기본 구성이 있습니다.

- 사용자 지정 eshop/catalog.api 이미지를 기반으로 합니다. 편의상 파일에 키 설정이라는 빌드가 없습니다. 즉, 이미지는 모든 Docker 레지스트리에서 이전에 docker 빌드로 빌드되었거나 docker pull 명령으로 다운로드되었어야 합니다.

- 카탈로그 데이터 모델을 포함하는 SQL Server 인스턴스에 액세스하기 위해 Entity Framework에서 사용되는 연결 문자열로 ConnectionString이라는 환경 변수를 정의합니다. 이 경우 동일한 SQL Server 컨테이너는 여러 데이터베이스를 보유하고 있습니다. 따라서 Docker에 대한 개발 컴퓨터에 적은 메모리가 필요합니다. 그러나 각 마이크로 서비스 데이터베이스에 대해 하나의 SQL Server 컨테이너를 배포할 수도 있습니다.

- SQL Server 이름은 sql.data입니다. 이는 Linux용 SQL Server 인스턴스를 실행하는 컨테이너에 사용되는 동일한 이름입니다. 이 방법은 편리합니다. 이 이름 확인(Docker 호스트에 대한 내부)을 사용할 수 있는 것은 네트워크 주소를 해결하므로 다른 컨테이너에서 액세스하는 컨테이너에 대한 내부 IP를 알지 않아도 됩니다.

연결 문자열은 환경 변수에 의해 정의되므로 다른 메커니즘을 통해 다른 시간에 해당 변수를 설정할 수 있습니다. 예를 들어 최종 호스트에서 프로덕션에 배포할 때 또는 Azure DevOps Services 또는 기본 DevOps 시스템의 CI/CD 파이프라인에서 수행하여 다른 연결 문자열을 설정할 수 있습니다.

- Docker 호스트 내에서 catalog.api 서비스에 대한 내부 엑세스에 대해 포트 80을 노출합니다. 호스트는 Linux용 Docker 이미지를 기반으로 하므로 현재 Linux VM이지만 Windows 이미지에서 대신 실행하도록 컨테이너를 구성할 수 있습니다.

- 컨테이너의 노출된 포트 80을 Docker 호스트 컴퓨터(Linux VM)의 포트 5101에 전달합니다.

- 웹 서비스를 sql.data 서비스(컨테이너에서 실행되는 Linux 데이터베이스에 대한 SQL Server 인스턴스)에 연결합니다. 이 종속성을 지정하면 catalog.api 컨테이너는 sql.data 컨테이너가 시작하기 전까지 시작하지 않습니다. catalog.api는 실행 중인 SQL Server 데이터베이스가 먼저 있어야 하기 때문에 중요합니다. 그러나 이러한 종류의 컨테이너 종속성은 Docker가 컨테이너 수준에서만 확인하기 때문에 많은 경우에서 충분하지 않습니다. 경우에 따라 서비스(이 경우 SQL Server)는 여전히 준비되지 않을 수 있으므로 클라이언트 마이크로 서비스에서 지수 백오프로 재시도 논리를 구현하는 것이 좋습니다. 이런 방식으로 종속성 컨테이너가 짧은 시간 동안 준비되지 않는 경우 애플리케이션은 계속해서 복원됩니다.

- 외부 서버에 대한 액세스를 허용하도록 구성됩니다. 추가\_호스트 설정을 통해 개발 PC의 로컬 SQL Server 인스턴스와 같은 외부 서버 또는 Docker 호스트 외부의 컴퓨터에 액세스할 수 있습니다(즉, 개발 Docker 호스트인 기본 Linux VM의 외부).

다음 섹션에서 다룰 더욱 고급의 다른 docker-compose.yml 설정도 있습니다.

### <a name="using-docker-compose-files-to-target-multiple-environments"></a>여러 환경을 대상으로 하는 docker-compose 파일 사용

docker-compose.yml 파일은 정의 파일이며 해당 형식을 이해하는 여러 인프라에서 사용될 수 있습니다. 가장 간단한 도구는 docker-compose 명령입니다.

따라서 docker-compose 명령을 사용하여 다음과 같은 주요 시나리오를 대상으로 지정할 수 있습니다.

#### <a name="development-environments"></a>개발 환경

애플리케이션을 개발하는 경우 격리된 개발 환경에서 애플리케이션을 실행할 수 있어야 하는 것은 중요합니다. docker-compose CLI 명령을 사용하여 해당 환경을 만들거나 내부에서 docker-compose를 사용하는 Visual Studio를 사용할 수 있습니다.

docker-compose.yml 파일을 사용하면 모든 애플리케이션의 서비스 종속성(다른 서비스, 캐시, 데이터베이스, 큐 등)을 구성하고 문서화할 수 있습니다. docker-compose CLI 명령을 사용하여 단일 명령(docker-compose up)으로 각 종속성에 대해 하나 이상의 컨테이너를 만들고 시작할 수 있습니다.

docker-compose.yml 파일은 Docker 엔진으로 해석되는 구성 파일이지만 다중 컨테이너 애플리케이션의 구성에 대한 편리한 문서 파일의 역할도 합니다.

#### <a name="testing-environments"></a>테스트 환경

모든 CD(지속적인 배포) 또는 CI(지속적인 통합) 프로세스의 중요한 부분은 단위 테스트 및 통합 테스트입니다. 이러한 자동화된 테스트는 격리된 환경이 필요하므로 사용자 또는 애플리케이션 데이터의 다른 변경 내용에 의해 영향을 받지 않습니다.

Docker Compose를 사용하여 다음 명령과 같이 명령 프롬프트 또는 스크립트의 몇 가지 명령에서 매우 쉽게 격리된 해당 환경을 만들고 제거할 수 있습니다.

```console
docker-compose -f docker-compose.yml -f docker-compose-test.override.yml up -d
./run_unit_tests
docker-compose -f docker-compose.yml -f docker-compose.test.override.yml down
```

#### <a name="production-deployments"></a>프로덕션 배포

Compose를 사용하여 원격 Docker 엔진에 배포할 수도 있습니다. 일반적인 경우는 단일 Docker 호스트 인스턴스를 배포하는 것입니다(예: 프로덕션 VM 또는 [Docker 컴퓨터](https://docs.docker.com/machine/overview/)로 프로비전된 서버).

다른 오케스트레이터(Azure Service Fabric, Kubernetes 등)를 사용하는 경우 다른 오케스트레이터에서 필요한 형식이 아닌 docker-compose.yml의 형식과 같은 설정 및 메타데이터 구성 설정을 추가해야 합니다.

어떤 경우에서든 docker-compose는 프로덕션 워크플로가 사용하는 오케스트레이터에 따라 다를 수 있음에도 불구하고 개발, 테스트 및 프로덕션 워크플로에 편리한 도구 및 메타데이터 형식입니다.

### <a name="using-multiple-docker-compose-files-to-handle-several-environments"></a>여러 환경을 처리하는 데 다중 docker-compose 파일 사용

다양한 환경을 대상으로 하는 경우 다중 compose 파일을 사용해야 합니다. 이를 통해 환경에 따라 여러 구성 변형을 만들 수 있습니다.

#### <a name="overriding-the-base-docker-compose-file"></a>기본 docker-compose 파일 재정의

이전 섹션에 표시된 간소화된 예제에서와 같이 단일 docker-compose.yml 파일을 사용할 수 있습니다. 그러나 대부분의 애플리케이션에 권장하지 않습니다.

기본적으로 Compose는 두 개의 파일, docker-compose.yml 및 선택적 docker-compose.override.yml 파일을 읽습니다. 그림 6-11과 같이 Visual Studio를 사용하고 Docker 지원을 활성화 하도록 설정하여, Visual Studio도 애플리케이션의 디버깅을 위한 추가 docker-compose.vs.debug.g.yml 파일을 만듭니다. 기본 솔루션 폴더에서 obj\\Docker\\ 폴더에서 이 파일을 볼 수 있습니다.

![docker compose 프로젝트 파일 구조: .dockerignore, 파일 무시; docker-compose.yml, 마이크로 서비스 구성; docker-compose.override.yml, 마이크로 서비스 환경 설정.](./media/image12.png)

**그림 6-11**. Visual Studio 2017의 docker-compose 파일

Visual Studio Code 또는 Sublime과 같은 편집기를 사용하여 docker-compose 파일을 편집하고 docker-compose up 명령을 사용하여 애플리케이션을 실행할 수 있습니다.

규칙에 따라 docker-compose.yml 파일은 기본 구성 및 기타 정적 설정을 포함합니다. 즉, 서비스 구성은 대상으로 하는 배포 환경에 따라 변경되지 않아야 합니다.

해당 이름에서 알 수 있듯이 docker-compose.override.yml 파일은 배포 환경에 따라 달라지는 구성과 같은 기본 구성을 재정의하는 구성 설정을 포함합니다. 또한 서로 다른 이름을 가진 여러 재정의 파일을 포함할 수 있습니다. 재정의 파일은 일반적으로 환경 또는 배포에 관련된 애플리케이션에 필요한 추가 정보를 포함합니다.

#### <a name="targeting-multiple-environments"></a>여러 환경을 대상으로 지정

일반적인 사용 사례는 프로덕션, 준비, CI 또는 개발과 같은 여러 환경을 대상으로 지정할 수 있도록 여러 compose 파일을 정의하는 경우입니다. 이러한 차이를 지원하기 위해 그림 6-12에 나와 있는 것처럼 Compose 구성을 여러 파일로 분할할 수 있습니다.

![여러 docker-compose*.fml 파일을 결합하여 다른 환경을 처리할 수 있습니다.](./media/image13.png)

**그림 6-12**. 기본 docker-compose.yml 파일에서 값을 재정의하는 다중 docker-compose 파일

기본 docker-compose.yml 파일로 시작합니다. 이 기본 파일은 환경에 따라 변경되지 않는 기본 또는 정적 구성 설정을 포함해야 합니다. 예를 들어 eShopOnContainers에는 기본 파일로 다음과 같은 docker-compose.yml(더 적은 서비스로 단순화된) 파일이 있습니다.

```yml
#docker-compose.yml (Base)
version: '3.4'
services:
  basket.api:
    image: eshop/basket.api:${TAG:-latest}
    build:
      context: .
      dockerfile: src/Services/Basket/Basket.API/Dockerfile
    depends_on:
      - basket.data
      - identity.api
      - rabbitmq

  catalog.api:
    image: eshop/catalog.api:${TAG:-latest}
    build:
      context: .
      dockerfile: src/Services/Catalog/Catalog.API/Dockerfile
    depends_on:
      - sql.data
      - rabbitmq

  marketing.api:
    image: eshop/marketing.api:${TAG:-latest}
    build:
      context: .
      dockerfile: src/Services/Marketing/Marketing.API/Dockerfile
    depends_on:
      - sql.data
      - nosql.data
      - identity.api
      - rabbitmq

  webmvc:
    image: eshop/webmvc:${TAG:-latest}
    build:
      context: .
      dockerfile: src/Web/WebMVC/Dockerfile
    depends_on:
      - catalog.api
      - ordering.api
      - identity.api
      - basket.api
      - marketing.api

  sql.data:
    image: microsoft/mssql-server-linux:2017-latest

  nosql.data:
    image: mongo

  basket.data:
    image: redis

  rabbitmq:
    image: rabbitmq:3-management

```

다른 대상 배포 환경으로 인해 기본 docker-compose.yml 파일의 값을 변경하지 마십시오.

예를 들어 webmvc 서비스 정의에 집중하는 경우 대상으로 할 수 있는 환경에 관계 없이 해당 정보가 동일한 것을 확인할 수 있습니다. 다음 정보가 있습니다.

- 서비스 이름: webmvc

- 컨테이너의 사용자 지정 이미지: eshop/webmvc

- 사용할 Dockerfile을 나타내는 사용자 지정 Docker 이미지를 빌드하는 명령

- 다른 서비스에 대한 종속성, 따라서 이 컨테이너는 다른 종속성 컨테이너가 시작될 때까지 시작되지 않습니다.

추가 구성을 가질 수 있지만 중요한 점은 기본 docker-compose.yml 파일에서 환경에 공통되는 정보를 설정하려 한다는 것입니다. 그런 다음, docker-compose.override.yml 또는 프로덕션 또는 스테이징에 대한 유사한 파일에서 각 환경에 관련된 구성을 배치해야 합니다.

일반적으로 docker-compose.override.yml은 eShopOnContainers의 다음 예제에서와 같이 개발 환경에 사용됩니다.

```yml
#docker-compose.override.yml (Extended config for DEVELOPMENT env.)
version: '3.4'

services:
# Simplified number of services here:

  basket.api:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=http://0.0.0.0:80
      - ConnectionString=${ESHOP_AZURE_REDIS_BASKET_DB:-basket.data}
      - identityUrl=http://identity.api
      - IdentityUrlExternal=http://${ESHOP_EXTERNAL_DNS_NAME_OR_IP}:5105
      - EventBusConnection=${ESHOP_AZURE_SERVICE_BUS:-rabbitmq}
      - EventBusUserName=${ESHOP_SERVICE_BUS_USERNAME}
      - EventBusPassword=${ESHOP_SERVICE_BUS_PASSWORD}
      - AzureServiceBusEnabled=False
      - ApplicationInsights__InstrumentationKey=${INSTRUMENTATION_KEY}
      - OrchestratorType=${ORCHESTRATOR_TYPE}
      - UseLoadTest=${USE_LOADTEST:-False}

    ports:
      - "5103:80"

  catalog.api:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=http://0.0.0.0:80
      - ConnectionString=${ESHOP_AZURE_CATALOG_DB:-Server=sql.data;Database=Microsoft.eShopOnContainers.Services.CatalogDb;User Id=sa;Password=Pass@word}
      - PicBaseUrl=${ESHOP_AZURE_STORAGE_CATALOG_URL:-http://localhost:5202/api/v1/catalog/items/[0]/pic/}
      - EventBusConnection=${ESHOP_AZURE_SERVICE_BUS:-rabbitmq}
      - EventBusUserName=${ESHOP_SERVICE_BUS_USERNAME}
      - EventBusPassword=${ESHOP_SERVICE_BUS_PASSWORD}
      - AzureStorageAccountName=${ESHOP_AZURE_STORAGE_CATALOG_NAME}
      - AzureStorageAccountKey=${ESHOP_AZURE_STORAGE_CATALOG_KEY}
      - UseCustomizationData=True
      - AzureServiceBusEnabled=False
      - AzureStorageEnabled=False
      - ApplicationInsights__InstrumentationKey=${INSTRUMENTATION_KEY}
      - OrchestratorType=${ORCHESTRATOR_TYPE}
    ports:
      - "5101:80"

  marketing.api:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=http://0.0.0.0:80
      - ConnectionString=${ESHOP_AZURE_MARKETING_DB:-Server=sql.data;Database=Microsoft.eShopOnContainers.Services.MarketingDb;User Id=sa;Password=Pass@word}
      - MongoConnectionString=${ESHOP_AZURE_COSMOSDB:-mongodb://nosql.data}
      - MongoDatabase=MarketingDb
      - EventBusConnection=${ESHOP_AZURE_SERVICE_BUS:-rabbitmq}
      - EventBusUserName=${ESHOP_SERVICE_BUS_USERNAME}
      - EventBusPassword=${ESHOP_SERVICE_BUS_PASSWORD}
      - identityUrl=http://identity.api
      - IdentityUrlExternal=http://${ESHOP_EXTERNAL_DNS_NAME_OR_IP}:5105
      - CampaignDetailFunctionUri=${ESHOP_AZUREFUNC_CAMPAIGN_DETAILS_URI}
      - PicBaseUrl=${ESHOP_AZURE_STORAGE_MARKETING_URL:-http://localhost:5110/api/v1/campaigns/[0]/pic/}
      - AzureStorageAccountName=${ESHOP_AZURE_STORAGE_MARKETING_NAME}
      - AzureStorageAccountKey=${ESHOP_AZURE_STORAGE_MARKETING_KEY}
      - AzureServiceBusEnabled=False
      - AzureStorageEnabled=False
      - ApplicationInsights__InstrumentationKey=${INSTRUMENTATION_KEY}
      - OrchestratorType=${ORCHESTRATOR_TYPE}
      - UseLoadTest=${USE_LOADTEST:-False}
    ports:
      - "5110:80"

  webmvc:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=http://0.0.0.0:80
      - PurchaseUrl=http://webshoppingapigw
      - IdentityUrl=http://10.0.75.1:5105
      - MarketingUrl=http://webmarketingapigw
      - CatalogUrlHC=http://catalog.api/hc
      - OrderingUrlHC=http://ordering.api/hc
      - IdentityUrlHC=http://identity.api/hc
      - BasketUrlHC=http://basket.api/hc
      - MarketingUrlHC=http://marketing.api/hc
      - PaymentUrlHC=http://payment.api/hc
      - SignalrHubUrl=http://${ESHOP_EXTERNAL_DNS_NAME_OR_IP}:5202
      - UseCustomizationData=True
      - ApplicationInsights__InstrumentationKey=${INSTRUMENTATION_KEY}
      - OrchestratorType=${ORCHESTRATOR_TYPE}
      - UseLoadTest=${USE_LOADTEST:-False}
    ports:
      - "5100:80"
  sql.data:
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"
  nosql.data:
    ports:
      - "27017:27017"
  basket.data:
    ports:
      - "6379:6379"
  rabbitmq:
    ports:
      - "15672:15672"
      - "5672:5672"

```

이 예제에서 개발 재정의 구성은 일부 포트를 호스트에 노출하고, 리디렉션 URL로 환경 변수를 정의하고, 개발 환경에 대한 연결 문자열을 지정합니다. 이러한 설정은 모두 개발 환경을 위한 것입니다.

`docker-compose up`을 실행하는 경우(또는 Visual Studio에서 시작) 명령은 두 파일을 병합하는 것처럼 재정의를 자동으로 읽습니다.

프로덕션 환경에 대해 다른 구성 값, 포트 또는 연결 문자열이 있는 다른 Compose 파일을 원한다고 가정합니다. 다른 설정 및 환경 변수가 있는 `docker-compose.prod.yml`이라는 파일과 같은 다른 재정의 파일을 만들 수 있습니다. 해당 파일은 다른 Git 리포지토리에 저장되거나 다른 팀에 의해 관리 및 보호될 수 있습니다.

#### <a name="how-to-deploy-with-a-specific-override-file"></a>특정 재정의 파일로 배포하는 방법

여러 재정의 파일 또는 다른 이름이 있는 재정의 파일을 사용하려면 docker-compose 명령과 함께 -f 옵션을 사용하고 파일을 지정할 수 있습니다. Compose는 명령줄에 지정된 순서로 파일을 병합합니다. 다음 예제에서는 재정의 파일로 배포하는 방법을 보여 줍니다.

```console
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

#### <a name="using-environment-variables-in-docker-compose-files"></a>docker-compose 파일에서 환경 변수 사용

이전 예제에서 본 것처럼 환경 변수에서 구성 정보를 얻을 수 있는 것은 특히 프로덕션 환경에서 편리합니다. 구문 ${MY\_VAR}을 사용하여 docker-compose 파일에서 환경 변수를 참조합니다. docker-compose.prod.yml 파일에서 다음 줄은 환경 변수의 값을 참조하는 방법을 보여 줍니다.

```yml
IdentityUrl=http://${ESHOP_PROD_EXTERNAL_DNS_NAME_OR_IP}:5105
```

환경 변수는 호스트 환경(Linux, Windows, 클라우드 클러스터 등)에 따라 다양한 방법으로 생성 및 초기화됩니다. 그러나 편리한 방법은 .env 파일을 사용하는 것입니다. docker-compose 파일은 .env 파일의 기본 환경 변수 선언을 지원합니다. 환경 변수에 대한 이러한 값은 기본값입니다. 그러나 각 환경(호스트 OS 또는 클러스터의 환경 변수)에서 정의했을 수 있는 값으로 재정의될 수 있습니다. 이 .env 파일을 docker-compose 명령이 실행되는 폴더에 배치합니다.

다음 예제에서는 eShopOnContainers 애플리케이션에 대한 [.env](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/.env) 파일과 같은 .env 파일을 보여 줍니다.

```env
# .env file

ESHOP_EXTERNAL_DNS_NAME_OR_IP=localhost

ESHOP_PROD_EXTERNAL_DNS_NAME_OR_IP=10.121.122.92
```

docker-compose는 .env 파일의 각 줄이 \<변수\>=\<값\> 형식이 되도록 예상합니다.

런타임 환경에서 설정된 값은 항상 .env 파일 내부에 정의된 값을 재정의합니다. 비슷한 방식으로 명령줄 명령 인수를 통해 전달된 값도 .env 파일에 설정된 기본값을 재정의합니다.

#### <a name="additional-resources"></a>추가 자료

- **Docker Compose 개요** \
    <https://docs.docker.com/compose/overview/>

- **다중 계산 파일** \
    [https://docs.docker.com/compose/extends/\#multiple-compose-files](https://docs.docker.com/compose/extends/#multiple-compose-files)

### <a name="building-optimized-aspnet-core-docker-images"></a>최적화된 ASP.NET Core Docker 이미지 빌드

인터넷에서 원본의 Docker 및 .NET Core를 탐색하는 경우 원본을 컨테이너에 복사하여 Docker 이미지를 빌드하는 것의 용이함을 보여 주는 Dockerfile을 찾을 수 있습니다. 이러한 예제는 간단한 구성을 사용하는 것을 제안합니다. 애플리케이션과 함께 제공되는 환경으로 Docker 이미지를 가질 수 있습니다. 다음 예제에서는 이 맥락에서 간단한 Dockerfile을 보여 줍니다.

```Dockerfile
FROM mcr.microsoft.com/dotnet/core/sdk:2.2
WORKDIR /app
ENV ASPNETCORE_URLS http://+:80
EXPOSE 80
COPY . .
RUN dotnet restore
ENTRYPOINT ["dotnet", "run"]
```

이와 같은 Dockerfile은 작동합니다. 그러나 실질적으로 이미지, 특히 프로덕션 이미지를 최적화할 수 있습니다.

컨테이너 및 마이크로 서비스 모델에서 컨테이너를 지속적으로 시작하고 있습니다. 컨테이너를 사용하는 일반적인 방법은 컨테이너가 삭제 가능하므로 중지 중인 컨테이너를 다시 시작하지 않습니다. 오케스트레이터(예: Kubernetes 및 Azure Service Fabric)는 단순히 이미지의 새 인스턴스를 만듭니다. 즉, 인스턴스화 프로세스의 속도가 더 빨라지도록 빌드될 때 애플리케이션을 미리 컴파일하여 최적화해야 합니다. 컨테이너가 시작될 때 실행할 준비가 되어야 합니다. .NET Core 및 Docker에 대한 다양한 블로그 게시물에 나와 있는 것처럼 dotnet CLI에서 `dotnet restore` and `dotnet build` 명령을 사용하여 런타임 시 복원 및 컴파일해서는 안 됩니다.

.NET 팀은 .NET Core 및 ASP.NET Core를 컨테이너 최적화된 프레임워크로 만들도록 중요한 작업을 수행하고 있습니다. .NET Core는 작은 메모리 공간을 가진 경량 프레임워크일 뿐만 아니라, 팀은 세 가지 주요 시나리오에 최적화된 Docker 이미지를 중점적으로 사용해 *dotnet/core*에서 버전 2.1부터 Docker 허브 레지스트리에 게시했습니다.

1. **개발**: 여기서 우선 순위는 변경 사항을 신속하게 반복하고 디버그할 수 있는 기능이며, 크기는 부차적 문제입니다.

2. **빌드:** 우선 순위는 애플리케이션을 컴파일하고 이진 파일 및 다른 종속성을 포함하여 이진 파일을 최적화하는 것입니다.

3. **프로덕션**: 컨테이너의 빠른 배포 및 시작에 중점을 두는 경우 이러한 이미지는 애플리케이션을 실행하는 데 필요한 이진 파일 및 콘텐츠로 제한됩니다.

이를 위해 .NET 팀은 [dotnet/core](https://hub.docker.com/_/microsoft-dotnet-core/)(Docker 허브)에서 네 가지 기본 변형을 제공합니다.

1. **sdk**: 개발 및 빌드 시나리오용
1. **aspnet**: ASP.NET 프로덕션 시나리오용
1. **runtime**: .NET 프로덕션 시나리오용
1. **runtime-deps**: [자체 포함된 애플리케이션](../../../core/deploying/index.md#self-contained-deployments-scd)의 프로덕션 시나리오용.

빠른 시작을 위해 런타임 이미지도 자동으로 aspnetcore\_urls를 포트 80으로 설정하고 Ngen을 사용하여 어셈블리의 네이티브 이미지 캐시를 만듭니다.

#### <a name="additional-resources"></a>추가 자료

- **ASP.NET Core를 사용하여 최적화된 Docker 이미지 빌드**  
  <https://blogs.msdn.microsoft.com/stevelasker/2016/09/29/building-optimized-docker-images-with-asp-net-core/>

- **.NET Core 애플리케이션에 대한 Docker 이미지 작성**  
  [https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images](../../../core/docker/building-net-docker-images.md)

> [!div class="step-by-step"]
> [이전](data-driven-crud-microservice.md)
> [다음](database-server-container.md)
