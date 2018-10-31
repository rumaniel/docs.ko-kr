---
title: NoSQL 데이터베이스를 지속성 인프라로 사용
description: 컨테이너화된 .NET 응용 프로그램을 위한 .NET 마이크로 서비스 아키텍처 | NoSQL 데이터베이스를 지속성 인프라로 사용
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 12/12/2017
ms.openlocfilehash: bb119d62691a714a0c7dbc99079dfc1a1fac3aae
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50188562"
---
# <a name="using-nosql-databases-as-a-persistence-infrastructure"></a>NoSQL 데이터베이스를 지속성 인프라로 사용

인프라 데이터 계층에 대해 NoSQL 데이터베이스를 사용하는 경우 일반적으로 Entity Framework Core와 같은 ORM을 사용하지 않습니다. 대신 Azure Cosmos DB, MongoDB, Cassandra, RavenDB, CouchDB 또는 Azure Storage Tables와 같은 NoSQL 엔진에 의해 제공되는 API를 사용합니다.

그러나 NoSQL 데이터베이스, 특히 Azure Cosmos DB, CouchDB 또는 RavenDB와 같은 문서 기반 데이터베이스를 사용하는 경우 DDD 집계를 사용하여 모델을 디자인하는 방식은 집계 루트, 자식 엔터티 클래스 및 값 개체 클래스의 식별과 관련하여 EF Core에서 수행하는 방법과 부분적으로 유사합니다. 그러나 궁극적으로 데이터베이스 선택은 디자인에 영향을 줍니다.

문서 기반 데이터베이스를 사용하면 JSON 또는 다른 형식으로 직렬화되는 단일 문서로 집계를 구현합니다. 그러나 데이터베이스의 사용은 도메인 모델 코드 관점에서 투명합니다. NoSQL 데이터베이스를 사용할 때 계속해서 엔터티 클래스 및 집계 루트 클래스를 사용하지만 지속성은 관계형이 아니기 때문에 EF Core를 사용할 때 보다 더 유연성이 있습니다.

차이점은 해당 모델을 유지하는 방법에 있습니다. POCO 엔터티 클래스에 따라 도메인 모델을 구현한 경우 인프라 지속성에 상관 없이 다른 지속성 인프라로 이동할 수 있는 것처럼 보일 수 있습니다(관계형에서 NoSQL로도). 그러나 목표가 될 수는 없습니다. 서로 다른 데이터베이스에는 사용자를 다시 푸시하는 제약 조건이 항상 있으므로 관계형 또는 NoSQL 데이터베이스에 대해 동일한 모델을 가질 수 없습니다. 트랜잭션 및 지속성 작업은 매우 달라지므로 지속성 모델을 변경하는 것은 간단하지 않습니다.

예를 들어 문서 기반 데이터베이스에서 집계 루트에 여러 개의 자식 컬렉션 속성을 포함하는 것은 괜찮습니다. 관계형 데이터베이스에서 여러 개의 자식 컬렉션 속성을 쿼리하는 것은 EF에서 UNION ALL SQL 문을 다시 가져오므로 좋지 않습니다. 관계형 데이터베이스 또는 NoSQL 데이터베이스에 대해 동일한 도메인 모델을 갖는 것은 간단하지 않으며 시도해서는 안 됩니다. 데이터가 각 특정 데이터베이스에서 사용되는 방법에 대한 이해와 함께 모델을 디자인해야 합니다.

NoSQL 데이터베이스를 사용하는 경우 이점은 엔터티가 더욱 비정규화되므로 테이블 매핑을 설정하지 않는다는 것입니다. 도메인 모델은 관계형 데이터베이스를 사용할 때보다 좀 더 유연할 수 있습니다.

집계를 기반으로 도메인 모델을 디자인할 때 NoSQL 및 문서 기반 데이터베이스로 이동하는 것은 디자인하는 집계가 문서 기반 데이터베이스의 직렬화된 문서와 유사하므로 관계형 데이터베이스를 사용하는 것보다 더욱 쉬울 수 있습니다. 그런 다음, 해당 집계에 필요할 수 있는 모든 정보를 해당 "모음"에 포함할 수 있습니다.

예를 들어 다음 JSON 코드는 문서 기반 데이터베이스를 사용할 때 순서 집계의 샘플 구현입니다. eShopOnContainers 샘플에서 구현한 순서 집계와 비슷하지만 아래 EF Core를 사용하지 않습니다.

```json
{
    "id": "2017001",
    "orderDate": "2/25/2017",
    "buyerId": "1234567",
    "address": [
        {
        "street": "100 One Microsoft Way",
        "city": "Redmond",
        "state": "WA",
        "zip": "98052",
        "country": "U.S."
        }
    ],
    "orderItems": [
        {"id": 20170011, "productId": "123456", "productName": ".NET T-Shirt",
        "unitPrice": 25, "units": 2, "discount": 0},
        {"id": 20170012, "productId": "123457", "productName": ".NET Mug",
        "unitPrice": 15, "units": 1, "discount": 0}
    ]
}
```

## <a name="introduction-to-azure-cosmos-db-and-the-native-cosmos-db-api"></a>Azure Cosmos DB 및 네이티브 Cosmos DB API 소개

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)는 중요 응용 프로그램에 대한 Microsoft의 전 세계적으로 분산된 데이터베이스 서비스입니다. Azure Cosmos DB는 [업계 최고의 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/)로 지원되는 [턴키 방식으로 전역 배포](https://docs.microsoft.com/azure/cosmos-db/distribute-data-globally), 전 세계적인 [처리량 및 저장소의 탄력적인 확장](https://docs.microsoft.com/azure/cosmos-db/partition-data), 한 자릿수 밀리초 대기 시간(99번째 백분위수), [5개의 잘 정의된 일관성 수준](https://docs.microsoft.com/azure/cosmos-db/consistency-levels) 및 보장되는 높은 가용성을 제공합니다. Azure Cosmos DB는 스키마 및 인덱스 관리를 처리할 필요 없이 [데이터를 자동으로 인덱싱합니다](https://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). 다중 모델이며 문서, 키-값, 그래프 및 열 형식 데이터 모델을 지원합니다.

![](./media/image19.1.png) 그림 9-19. Azure Cosmos DB 전역 배포

C\# 모델을 사용하여 Azure Cosmos DB API에서 사용될 집계를 구현하는 경우 집계는 EF Core와 함께 사용되는 C\# POCO 클래스와 유사할 수 있습니다. 차이점은 다음 코드에서처럼 응용 프로그램 및 인프라 계층에서 사용하는 방법에 있습니다.

```csharp
// C# EXAMPLE OF AN ORDER AGGREGATE BEING PERSISTED WITH AZURE COSMOS DB API
// *** Domain Model Code ***
// Aggregate: Create an Order object with its child entities and/or value objects.
// Then, use AggregateRoot’s methods to add the nested objects so invariants and
// logic is consistent across the nested properties (value objects and entities).

Order orderAggregate = new Order
{
    Id = "2017001",
    OrderDate = new DateTime(2005, 7, 1),
    BuyerId = "1234567",
    PurchaseOrderNumber = "PO18009186470"
}

Address address = new Address
{
    Street = "100 One Microsoft Way",
    City = "Redmond",
    State = "WA",
    Zip = "98052",
    Country = "U.S."
}

orderAggregate.UpdateAddress(address);

OrderItem orderItem1 = new OrderItem
{
    Id = 20170011,
    ProductId = "123456",
    ProductName = ".NET T-Shirt",
    UnitPrice = 25,
    Units = 2,
    Discount = 0;
};

//Using methods with domain logic within the entity. No anemic-domain model
orderAggregate.AddOrderItem(orderItem1);
orderAggregate.AddOrderItem(orderItem2);
// *** End of Domain Model Code ***

// *** Infrastructure Code using Cosmos DB Client API ***
Uri collectionUri = UriFactory.CreateDocumentCollectionUri(databaseName,
    collectionName);

await client.CreateDocumentAsync(collectionUri, orderAggregate);

// As your app evolves, let's say your object has a new schema. You can insert
// OrderV2 objects without any changes to the database tier.
Order2 newOrder = GetOrderV2Sample("IdForSalesOrder2");
await client.CreateDocumentAsync(collectionUri, newOrder);
```

도메인 모델을 사용하는 방법은 인프라가 EF인 경우 도메인 모델 계층에서 사용하는 방법과 유사할 수 있음을 확인할 수 있습니다. 여전히 동일한 집계 루트 메서드를 사용하여 집계 내에서 일관성, 고정 및 유효성 검사를 확인합니다.

그러나 NoSQL 데이터베이스로 모델을 유지하는 경우 코드 및 API는 EF Core 코드 또는 관계형 데이터베이스와 관련된 다른 코드에 비해 크게 변경됩니다.

## <a name="implementing-net-code-targeting-mongodb-and-azure-cosmos-db"></a>MongoDB 및 Azure Cosmos DB를 대상으로 하는 .NET 코드 구현

### <a name="using-azure-cosmos-db-from-net-containers"></a>.NET 컨테이너에서 Azure Cosmos DB 사용

다른 .NET 응용 프로그램에서와 같이 컨테이너에서 실행되는 .NET 코드에서 Azure Cosmos DB 데이터베이스에 액세스할 수 있습니다. 예를 들어 eShopOnContainers의 Locations.API 및 Marketing.API 마이크로 서비스는 Azure Cosmos DB 데이터베이스를 사용할 수 있도록 구현됩니다.

그러나 Docker 개발 환경 관점에서 Azure Cosmos DB에 제한이 있습니다. 2017년 말을 기준으로, 로컬 개발 컴퓨터(예: PC)에서 실행할 수 있는 온-프레미스 [Azure Cosmos DB 에뮬레이터](https://docs.microsoft.com/azure/cosmos-db/local-emulator)가 있는 경우에도 Linux가 아닌 Windows만 지원합니다. 

Docker에서 이 에뮬레이터를 실행할 가능성도 있지만 Linux 컨테이너가 아닌 Windows 컨테이너에서만 입니다. 현재 Windows의 경우 Docker에 Linux 및 Windows 컨테이너를 동시에 배포할 수 없으므로 응용 프로그램이 Linux 컨테이너로 배포되는 경우 개발 환경에 대한 초기 핸디캡이 있습니다. 배포되는 모든 컨테이너는 Linux 또는 Windows용이어야 합니다.  

개발/테스트 솔루션에 대한 이상적이고 더욱 간단한 배포는 개발/테스트 환경이 항상 일치하도록 사용자 지정 컨테이너와 함께 컨테이너로 데이터베이스 시스템을 배포할 수 있어야 합니다.

### <a name="use-mongodb-api-for-local-devtest-linuxwindows-containers-plus-azure-cosmos-db"></a>로컬 개발/테스트 Linux/Windows 컨테이너와 Azure Cosmos DB에 대해 MongoDB API 사용

Cosmos DB 데이터베이스는 .NET용 MongoDB API뿐만 아니라 네이티브 MongoDB 유선 프로토콜도 지원합니다. 즉, 기존 드라이버를 사용하여 MongoDB용으로 작성된 응용 프로그램은 이제 그림 9-20에 나와 있는 것처럼 Cosmos DB와 통신하고 MongoDB 데이터베이스 대신 Cosmos DB 데이터베이스를 사용할 수 있습니다.

![](./media/image19.2.png) 그림 9-20. MongoDB API 및 프로토콜을 사용하여 Azure Cosmos DB에 액세스

[MongoDB Docker 이미지](https://hub.docker.com/r/_/mongo/)는 Docker Linux 컨테이너 및 Docker Windows 컨테이너를 지원하는 다중 아치 이미지이므로 Linux 컨테이너를 사용하는 Docker 환경에서 개념의 증명에 매우 편리한 방법입니다.

그림 9-21에서 표시된 것처럼 MongoDB API를 사용하여 eShopOnContainers는 로컬 개발 환경에 대해 MongoDB Linux 및 Windows 컨테이너를 지원하지만 [MongoDB 연결 문자열을 Azure Cosmos DB를 가리키도록](https://docs.microsoft.com/azure/cosmos-db/connect-mongodb-account) 단순히 변경하여 Azure Cosmos DB로 확장 가능한 PaaS 클라우드 솔루션으로 이동할 수 있습니다. 

![](./media/image20-bis.png) 그림 9-21. 개발 환경 또는 프로덕션용 Azure Cosmos DB에 대해 MongoDB 컨테이너를 사용하는 eShopOnContainers

프로덕션 Azure Cosmos DB는 PaaS 및 확장 가능한 서비스로 Azure의 클라우드에서 실행됩니다.

사용자 지정 .NET Core 컨테이너는 로컬 개발 Docker 호스트(Windows 10 컴퓨터에서 Windows용 Docker 사용)에서 실행되거나 Azure AKS 또는 Azure Service Fabric에서 Kubernetes와 같은 프로덕션 환경에 배포될 수 있습니다. 이 두 번째 환경에서는 프로덕션에서 데이터를 처리하기 위해 클라우드에서 Azure Cosmos DB를 사용하므로 MongoDB 컨테이너가 아닌 .NET Core 사용자 지정 컨테이너만 배포합니다.

MongoDB API를 사용하는 명백한 이점은 솔루션이 두 데이터베이스 엔진, MongoDB 또는 Azure Cosmos DB에서 실행될 수 있으므로 다른 환경으로의 마이그레이션이 용이해야 한다는 것입니다. 그러나 경우에 따라 특정 데이터베이스 엔진의 기능을 완전히 활용하기 위해 네이티브 API(즉 네이티브 Cosmos DB API)를 사용하는 것이 유용합니다.

클라우드에서 단순히 MongoDB와 Cosmos DB 사용 간의 자세한 비교는 [이 페이지에서 Azure Cosmos DB 사용의 이점](https://docs.microsoft.com/azure/cosmos-db/mongodb-introduction)을 참조하세요. 


### <a name="analyze-your-approach-for-production-applications-mongodb-api-vs-cosmos-db-api"></a>프로덕션 응용 프로그램에 대한 접근 방식 분석: MongoDB API와 Cosmos DB API 비교

eShopOnContainers에서 우선 순위는 근본적으로 Azure Cosmos DB를 함께 사용할 수 있는 NoSQL 데이터베이스를 사용하여 일관성 있는 개발/테스트 환경을 갖는 것이었으므로 MongoDB API를 사용합니다.

그러나 MongoDB API를 사용하여 프로덕션 응용 프로그램에 대해 Azure에서 Azure Cosmos DB에 액세스하려는 경우 네이티브 Azure Cosmos DB API를 사용하는 것과 비교하여 MongoDB API를 사용하여 Azure Cosmos DB 데이터베이스에 액세스할 때 기능 및 성능에서의 차이점을 분석해야 합니다. 유사한 경우 MongoDB API를 사용할 수 있으며, 동시에 두 개의 NoSQL 데이터베이스 엔진을 지원하는 이점을 얻을 수 있습니다. 

또한 [MongoDB Azure 서비스](https://www.mongodb.com/scale/mongodb-azure-service)와 함께 Azure의 클라우드에서 프로덕션 데이터베이스로 MongoDB 클러스터를 사용할 수도 있습니다. 그러나 Microsoft에서 제공하는 PaaS 서비스가 아닙니다. 이 경우 Azure는 MongoDB에서 오는 해당 솔루션만 호스팅합니다.

기본적으로 Linux 컨테이너에 대한 편리한 선택이므로 eShopOnContainers에서 수행한 것처럼 Azure Cosmos DB에 대해 항상 MongoDB API를 사용해서는 안 된다는 고지 사항입니다. 결정은 프로덕션 응용 프로그램에 대해 수행해야 하는 특정 요구 사항 및 테스트를 기준으로 해야 합니다.  

### <a name="the-code-using-mongodb-api-in-net-core-applications"></a>코드: .NET Core 응용 프로그램에서 MongoDB API 사용

.NET용 MongoDB API는 그림 9-22에 표시된 것처럼 Locations.API와 같이 프로젝트에 추가해야 하는 NuGet 패키지를 기반으로 합니다.

![](./media/image21-bis.png) 그림 9-22. .NET Core 프로젝트에서 MongoDB API NuGet 패키지 참조

다음 섹션에서 코드를 검토하겠습니다.

#### <a name="a-model-used-by-mongodb-api"></a>MongoDB API에서 사용하는 모델

먼저 응용 프로그램의 메모리 공간에 데이터베이스에서 가져온 데이터를 보유하는 모델을 정의해야 합니다. eShopOnContainers에서 Locations에 대해 사용되는 모델의 예는 다음과 같습니다.

```csharp
using MongoDB.Bson;
using MongoDB.Bson.Serialization.Attributes;
using MongoDB.Driver.GeoJsonObjectModel;
using System.Collections.Generic;

public class Locations
{
    [BsonId]
    [BsonRepresentation(BsonType.ObjectId)]
    public string Id { get; set; }
    public int LocationId { get; set; }
    public string Code { get; set; }
    [BsonRepresentation(BsonType.ObjectId)]
    public string Parent_Id { get; set; }
    public string Description { get; set; }
    public double Latitude { get; set; }
    public double Longitude { get; set; }
    public GeoJsonPoint<GeoJson2DGeographicCoordinates> Location 
                                                             { get; private set; }
    public GeoJsonPolygon<GeoJson2DGeographicCoordinates> Polygon 
                                                             { get; private set; }
    public void SetLocation(double lon, double lat) => SetPosition(lon, lat);
    public void SetArea(List<GeoJson2DGeographicCoordinates> coordinatesList) 
                                                    => SetPolygon(coordinatesList);

    private void SetPosition(double lon, double lat)
    {
        Latitude = lat;
        Longitude = lon;
        Location = new GeoJsonPoint<GeoJson2DGeographicCoordinates>(
            new GeoJson2DGeographicCoordinates(lon, lat));
    }

    private void SetPolygon(List<GeoJson2DGeographicCoordinates> coordinatesList)
    {
        Polygon = new GeoJsonPolygon<GeoJson2DGeographicCoordinates>(
                  new GeoJsonPolygonCoordinates<GeoJson2DGeographicCoordinates>(
                  new GeoJsonLinearRingCoordinates<GeoJson2DGeographicCoordinates>(
                                                                 coordinatesList)));
    }
}
```

MongoDB NuGet 패키지에서 가져온 몇 가지 특성 및 형식을 볼 수 있습니다.

NoSQL 데이터베이스는 일반적으로 비관계형 계층적 데이터를 사용하는 데 매우 적합합니다. 이 예제에서는 `GeoJson2DGeographicCoordinates`와 같이 지역 위치에 대해 특별히 만들어진 MongoDB 형식을 사용합니다.

#### <a name="retrieve-the-database-and-the-collection"></a>데이터베이스 및 컬렉션 검색

eShopOnContainers에서 다음 코드에서와 같이 데이터베이스 및 MongoCollections를 검색하는 코드를 구현하는 사용자 지정 데이터베이스 컨텍스트를 만들었습니다.

```csharp
public class LocationsContext
{
    private readonly IMongoDatabase _database = null;

    public LocationsContext(IOptions<LocationSettings> settings)
    {
        var client = new MongoClient(settings.Value.ConnectionString);
        if (client != null)
            _database = client.GetDatabase(settings.Value.Database);
    }

    public IMongoCollection<Locations> Locations
    {
        get
        {
            return _database.GetCollection<Locations>("Locations");
        }
    }       
}
```

#### <a name="retrieve-the-data"></a>데이터 검색

C# 코드에서는 Web API 컨트롤러 또는 사용자 지정 리포지토리 구현과 같이 MongoDB API를 통해 쿼리할 때 다음과 유사한 코드를 작성할 수 있습니다. `_context` 개체는 이전 `LocationsContext` 클래스의 인스턴스입니다.

```csharp
public async Task<Locations> GetAsync(int locationId)
{
    var filter = Builders<Locations>.Filter.Eq("LocationId", locationId);
    return await _context.Locations
                            .Find(filter)
                            .FirstOrDefaultAsync();
}
```

#### <a name="use-an-env-var-in-the-docker-composeoverrideyml-file-for-the-mongodb-connection-string"></a>MongoDB 연결 문자열에 대해 docker-compose.override.yml 파일에서 env-var를 사용합니다.

MongoClient 개체를 만들 때 올바른 데이터베이스를 가리키는 정확한 `ConnectionString` 매개 변수인 기본 매개 변수가 필요합니다. eShopOnContainers의 경우 연결 문자열은 로컬 MongoDB Docker 컨테이너 또는 "프로덕션" Azure Cosmos DB 데이터베이스를 가리킬 수 있습니다.  해당 연결 문자열은 다음 yml 코드에서처럼 docker-compose 또는 Visual Studio를 사용하여 배포할 때 사용되는 `docker-compose.override.yml` 파일에서 정의된 환경 변수에서 제공됩니다.

```yml
# docker-compose.override.yml
version: '3'
services:
  # Other services
  locations.api:
    environment:
      # Other settings
      - ConnectionString=${ESHOP_AZURE_COSMOSDB:-mongodb://nosql.data}

```

`ConnectionString` 환경 변수는 이러한 방식으로 해결됩니다. `ESHOP_AZURE_COSMOSDB` 전역 변수가 Azure Cosmos DB 연결 문자열로 `.env` 파일에서 정의되는 경우 클라우드에서 Azure Cosmos DB 데이터베이스에 액세스하는 데 사용합니다. 

다음 코드는 eShopOnContainers에서 구현된 것처럼 Azure Cosmos DB 연결 문자열 전역 환경 변수가 있는 `.env` 파일을 보여 줍니다.

```yml
# .env file, in eShopOnContainers root folder
# Other Docker environment variables

ESHOP_EXTERNAL_DNS_NAME_OR_IP=localhost
ESHOP_PROD_EXTERNAL_DNS_NAME_OR_IP=<YourDockerHostIP>

#ESHOP_AZURE_COSMOSDB=<YourAzureCosmosDBConnData>

#Other environment variables for additional Azure infrastructure assets
#ESHOP_AZURE_REDIS_BASKET_DB=<YourAzureRedisBasketInfo>
#ESHOP_AZURE_STORAGE_CATALOG_URL=<YourAzureStorage_Catalog_BLOB_URL>
#ESHOP_AZURE_SERVICE_BUS=<YourAzureServiceBusInfo>
```

[Azure Cosmos DB에 MongoDB 응용 프로그램 연결](https://docs.microsoft.com/azure/cosmos-db/connect-mongodb-account)에 설명된 것처럼 ESHOP_AZURE_COSMOSDB 줄의 주석 처리를 제거하고 Azure Portal에서 가져온 Azure Cosmos DB 연결 문자열로 업데이트해야 합니다.

`ESHOP_AZURE_COSMOSDB` 전역 변수가 비어 있는 경우(`.env` 파일에서 주석으로 처리된 것을 의미함) 컨테이너는 다음 .yml 코드에 표시된 것처럼 `nosql.data`라는 eShopOnContainers에 배포된 로컬 MongoDB 컨테이너를 가리키는 기본 MongoDB 연결 문자열을 사용합니다. 

#### <a name="additional-resources"></a>추가 자료

-   **NoSQL 데이터베이스용 문서 데이터 모델링**
    [*https://docs.microsoft.com/azure/cosmos-db/modeling-data*](https://docs.microsoft.com/azure/cosmos-db/modeling-data)

-   **Vaughn Vernon. 이상적인 도메인 기반 디자인 집계 저장소?**
    [*https://vaughnvernon.co/?p=942*](https://vaughnvernon.co/?p=942)

-   **Azure DB Cosmos 소개: MongoDB용 API** 
    [*https://docs.microsoft.com/azure/cosmos-db/mongodb-introduction*](https://docs.microsoft.com/azure/cosmos-db/mongodb-introduction)

-   **Azure Cosmos DB: .NET 및 Azure Portal에서 MongoDB API 웹앱 빌드** 
    [*https://docs.microsoft.com/azure/cosmos-db/create-mongodb-dotnet *](https://docs.microsoft.com/azure/cosmos-db/create-mongodb-dotnet )

-   **로컬 개발 및 테스트에 Azure Cosmos DB 에뮬레이터 사용** 
    [*https://docs.microsoft.com/azure/cosmos-db/local-emulator*](https://docs.microsoft.com/azure/cosmos-db/local-emulator)

-   **Azure Cosmos DB에 MongoDB 응용 프로그램 연결** 
    [*https://docs.microsoft.com/azure/cosmos-db/connect-mongodb-account*](https://docs.microsoft.com/azure/cosmos-db/connect-mongodb-account)

-   **Cosmos DB 에뮬레이터 Docker 이미지(Windows 컨테이너)** 
    [*https://hub.docker.com/r/microsoft/azure-cosmosdb-emulator/*](https://hub.docker.com/r/microsoft/azure-cosmosdb-emulator/)

-   **MongoDB Docker 이미지(Linux 및 Windows 컨테이너)** 
    [*https://hub.docker.com/r/_/mongo/*](https://hub.docker.com/r/_/mongo/)

-   **Azure Cosmos DB에서 MongoChef(Studio 3T) 사용: MongoDB 계정용 API** 
    [*https://docs.microsoft.com/azure/cosmos-db/mongodb-mongochef*](https://docs.microsoft.com/azure/cosmos-db/mongodb-mongochef)


>[!div class="step-by-step"]
[이전](infrastructure-persistence-layer-implemenation-entity-framework-core.md)
[다음](microservice-application-layer-web-api-design.md)
