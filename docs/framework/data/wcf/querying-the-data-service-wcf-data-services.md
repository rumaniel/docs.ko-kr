---
title: 데이터 서비스 쿼리(WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, client library
- WCF Data Services, querying
- WCF Data Services, accessing data
ms.assetid: 823e9444-27aa-4f1f-be8e-0486d67f54c0
ms.openlocfilehash: cc0e8a5e7d254fc4b34566d2252869a2da4af3db
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894289"
---
# <a name="querying-the-data-service-wcf-data-services"></a>데이터 서비스 쿼리(WCF Data Services)

[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트 라이브러리를 사용하면 LINQ(Language-Integrated Query) 사용을 비롯한 익숙한 .NET Framework 프로그래밍 패턴을 사용하여 데이터 서비스에 대해 쿼리를 실행할 수 있습니다. 클라이언트 라이브러리는 클라이언트에서 <xref:System.Data.Services.Client.DataServiceQuery%601> 클래스의 인스턴스로 정의된 쿼리를 HTTP GET 요청 메시지로 변환합니다. 라이브러리는 응답 메시지를 수신 하 고이를 클라이언트 데이터 서비스 클래스의 인스턴스로 변환 합니다. 이러한 클래스는 <xref:System.Data.Services.Client.DataServiceContext>가 속해 있는 <xref:System.Data.Services.Client.DataServiceQuery%601>에 의해 추적됩니다.

## <a name="data-service-queries"></a>데이터 서비스 쿼리

<xref:System.Data.Services.Client.DataServiceQuery%601> 제네릭 클래스는 0개 이상의 엔터티 형식 인스턴스의 컬렉션을 반환하는 쿼리를 나타냅니다. 데이터 서비스 쿼리는 항상 기존 데이터 서비스 컨텍스트에 속합니다. 이 컨텍스트는 쿼리를 작성하고 실행하는 데 필요한 서비스 URI 및 메타데이터 정보를 유지 관리합니다.

**서비스 참조 추가** 대화 상자를 사용 하 여 데이터 서비스를 .NET Framework 기반 클라이언트 응용 프로그램에 추가 하면 <xref:System.Data.Services.Client.DataServiceContext> 클래스에서 상속 하는 엔터티 컨테이너 클래스가 만들어집니다. 이 클래스에는 형식화된 <xref:System.Data.Services.Client.DataServiceQuery%601> 인스턴스를 반환하는 속성이 포함됩니다. 데이터 서비스에서 노출하는 엔터티 집합마다 속성이 하나씩 있습니다. 이러한 속성을 사용하면 형식화된 <xref:System.Data.Services.Client.DataServiceQuery%601> 인스턴스를 보다 쉽게 만들 수 있습니다.

쿼리는 다음 시나리오에서 실행됩니다.

- 결과가 다음과 같이 암시적으로 열거되는 경우

  - <xref:System.Data.Services.Client.DataServiceContext>(C#) 또는 `foreach`(Visual Basic) 루프 중과 같이 엔터티 집합을 나타내는 `For Each`에 대한 속성이 열거되는 경우

  - 쿼리가 `List` 컬렉션에 할당된 경우

- <xref:System.Data.Services.Client.DataServiceQuery%601.Execute%2A> 또는 <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> 메서드를 명시적으로 호출한 경우

- <xref:System.Linq.Enumerable.First%2A>, <xref:System.Linq.Enumerable.Single%2A> 등의 LINQ 쿼리 실행 연산자를 호출한 경우.

다음 쿼리를 실행하면 Northwind 데이터 서비스에 있는 모든 `Customers` 엔터티가 반환됩니다.

[!code-csharp[Astoria Northwind Client#GetAllCustomersSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getallcustomersspecific)]
[!code-vb[Astoria Northwind Client#GetAllCustomersSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getallcustomersspecific)]

자세한 내용은 [방법: 데이터 서비스 쿼리](how-to-execute-data-service-queries-wcf-data-services.md)를 실행 합니다.

클라이언트 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 는에서 C# *동적* 형식을 사용할 때와 같은 런타임에 바인딩된 개체에 대 한 쿼리를 지원 합니다. 하지만 성능상의 이유로 데이터 서비스에 대해 항상 강력한 형식의 쿼리를 작성해야 합니다. <xref:System.Tuple> 유형 및 동적 개체는 클라이언트에서 지원되지 않습니다.

## <a name="linq-queries"></a>LINQ 쿼리

클래스가 linq로 정의 된 <xref:System.Linq.IQueryable%601> 인터페이스를 구현 하기 때문에 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트 라이브러리는 엔터티 집합 데이터에 대 한 linq 쿼리를 데이터 서비스에 대해 평가 되는 쿼리 식을 나타내는 URI로 변환할 수 있습니다. <xref:System.Data.Services.Client.DataServiceQuery%601> 리소스나. 다음 예제는 운송료가 $30를 초과하는 <xref:System.Data.Services.Client.DataServiceQuery%601>를 반환하고 결과를 운송료순으로 정렬하는 이전 `Orders`와 동일한 LINQ 쿼리입니다.

[!code-csharp[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addqueryoptionslinqspecific)]
[!code-vb[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addqueryoptionslinqspecific)]

이 LINQ 쿼리는 Northwind 기반 [퀵 스타트](quickstart-wcf-data-services.md) 데이터 서비스에 대해 실행 되는 다음 쿼리 URI로 변환 됩니다.

```http
http://localhost:12345/Northwind.svc/Orders?Orderby=ShippedDate&?filter=Freight gt 30
```

> [!NOTE]
> LINQ 구문으로 표현할 수 있는 쿼리 집합은 데이터 서비스에 사용되는 REST(Representational State Transfer) 기반 URI 구문에서 사용할 수 있는 것보다 광범위합니다. 쿼리를 대상 데이터 서비스의 URI에 매핑할 수 없으면 <xref:System.NotSupportedException>이 발생합니다.

자세한 내용은 [LINQ 고려 사항](linq-considerations-wcf-data-services.md)을 참조 하세요.

## <a name="adding-query-options"></a>쿼리 옵션 추가

데이터 서비스 쿼리는 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]에서 제공하는 모든 쿼리 옵션을 지원합니다. 쿼리 옵션을 <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 인스턴스에 추가하려면 <xref:System.Data.Services.Client.DataServiceQuery%601> 메서드를 호출합니다. <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A>은 원래 쿼리와 동일하지만 새 쿼리 옵션 집합이 포함된 새 <xref:System.Data.Services.Client.DataServiceQuery%601> 인스턴스를 반환합니다. 다음 쿼리를 실행하면 `Orders` 값으로 필터링되고 `Freight`를 기준으로 내림차순으로 정렬된 `OrderID`가 반환됩니다.

[!code-csharp[Astoria Northwind Client#AddQueryOptionsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addqueryoptionsspecific)]
[!code-vb[Astoria Northwind Client#AddQueryOptionsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addqueryoptionsspecific)]

`$orderby` 쿼리 옵션을 사용하여 단일 속성에 따라 쿼리를 정렬하고 필터링할 수 있습니다. 다음 예제에서는 반환된 `Orders` 개체를 `Freight` 속성의 값에 따라 필터링하고 정렬합니다.

[!code-csharp[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#orderwithfilter)]
[!code-vb[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#orderwithfilter)]

<xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 메서드를 연속적으로 호출하여 복잡한 쿼리 식을 생성할 수 있습니다. 자세한 내용은 [방법: 데이터 서비스 쿼리에](how-to-add-query-options-to-a-data-service-query-wcf-data-services.md)쿼리 옵션을 추가 합니다.

쿼리 옵션을 통해 LINQ 쿼리의 구문 구성 요소를 표현할 수도 있습니다. 자세한 내용은 [LINQ 고려 사항](linq-considerations-wcf-data-services.md)을 참조 하세요.

> [!NOTE]
> `$select` 쿼리 옵션은 <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 메서드를 사용하여 쿼리 URI에 추가할 수 없습니다. LINQ <xref:System.Linq.Enumerable.Select%2A> 메서드를 사용하여 클라이언트에서 요청 URI에 `$select` 쿼리 옵션을 생성하도록 하는 것이 좋습니다.

<a name="executingQueries"></a>

## <a name="client-versus-server-execution"></a>클라이언트 및 서버 실행

클라이언트는 쿼리를 두 부분으로 실행합니다. 가능한 경우 쿼리의 식이 클라이언트에서 먼저 계산된 다음 URI 기반 쿼리가 생성되고 서비스의 데이터와 비교하여 평가되도록 데이터 서비스로 보내집니다. 다음 LINQ 쿼리를 살펴보세요.

[!code-csharp[Astoria Northwind Client#LinqQueryClientEvalSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqqueryclientevalspecific)]
[!code-vb[Astoria Northwind Client#LinqQueryClientEvalSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqqueryclientevalspecific)]

이 예에서는 `(basePrice – (basePrice * discount))` 식이 클라이언트에서 계산됩니다. 이런 이유로, 데이터 서비스로 보내진 실제 쿼리 URI `http://localhost:12345/northwind.svc/Products()?$filter=(UnitPrice gt 90.00M) and substringof('bike',ProductName)`에는 필터 절의 `90`에 대해 계산된 10진수 값이 이미 포함됩니다. 부분 문자열 식을 포함하는 필터링 식의 다른 부분은 데이터 서비스에서 계산됩니다. 클라이언트에서 계산된 식은 CLR(공용 언어 런타임) 의미 체계를 따르지만 데이터 서비스로 보내지는 식은 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 프로토콜의 데이터 서비스 구현을 활용합니다. 또한 이와 같은 개별 계산으로 인해 클라이언트와 서비스가 서로 다른 시간대에 시간 기반의 계산을 수행하는 경우와 같은 예상치 못한 결과가 발생할 수도 있습니다.

## <a name="query-responses"></a>쿼리 응답

<xref:System.Data.Services.Client.DataServiceQuery%601>를 실행하면 요청된 엔터티 형식의 <xref:System.Collections.Generic.IEnumerable%601>이 반환됩니다. 이 쿼리 결과는 다음 예제와 같이 <xref:System.Data.Services.Client.QueryOperationResponse%601> 개체로 캐스팅될 수 있습니다.

[!code-csharp[Astoria Northwind Client#GetResponseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getresponsespecific)]
[!code-vb[Astoria Northwind Client#GetResponseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getresponsespecific)]

데이터 서비스의 엔터티를 나타내는 엔터티 형식 인스턴스는 개체 구체화라는 프로세스에 의해 클라이언트에서 만들어집니다. 자세한 내용은 [개체 구체화](object-materialization-wcf-data-services.md)를 참조 하세요. <xref:System.Data.Services.Client.QueryOperationResponse%601> 개체는 <xref:System.Collections.Generic.IEnumerable%601>을 구현하여 쿼리 결과에 대한 액세스를 제공합니다.

<xref:System.Data.Services.Client.QueryOperationResponse%601>에는 쿼리 결과에 대한 추가 정보에 액세스할 수 있도록 하는 다음 멤버도 있습니다.

- <xref:System.Data.Services.Client.OperationResponse.Error%2A> - 작업에서 오류가 throw된 경우 해당 오류를 가져옵니다.

- <xref:System.Data.Services.Client.OperationResponse.Headers%2A> - 쿼리 응답과 연결된 HTTP 응답 헤더의 컬렉션을 포함합니다.

- <xref:System.Data.Services.Client.QueryOperationResponse.Query%2A> - <xref:System.Data.Services.Client.DataServiceQuery%601>를 생성한 원래 <xref:System.Data.Services.Client.QueryOperationResponse%601>를 가져옵니다.

- <xref:System.Data.Services.Client.OperationResponse.StatusCode%2A> - 쿼리 응답의 HTTP 응답 코드를 가져옵니다.

- <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> - <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> 메서드가 <xref:System.Data.Services.Client.DataServiceQuery%601>에서 호출된 경우 엔터티 집합의 총 엔터티 수를 가져옵니다.

- <xref:System.Data.Services.Client.QueryOperationResponse.GetContinuation%2A> - 결과의 다음 페이지 URI를 포함하는 <xref:System.Data.Services.Client.DataServiceQueryContinuation> 개체를 반환합니다.

기본적 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 으로는 쿼리 URI에 의해 명시적으로 선택 된 데이터만 반환 합니다. 이에 따라 필요한 경우 데이터 서비스에서 추가 데이터를 명시적으로 로드하는 옵션이 제공됩니다. 데이터 서비스에서 데이터를 명시적으로 로드할 때마다 요청이 데이터 서비스로 전송됩니다. 명시적으로 로드될 수 있는 데이터에는 관련 엔터티, 페이징 응답 데이터 및 이진 데이터 스트림이 포함됩니다.

> [!NOTE]
> 데이터 서비스가 페이징 응답을 반환할 수 있기 때문에 애플리케이션에서 프로그래밍 패턴을 사용하여 페이징 데이터 서비스 응답을 처리하는 것이 좋습니다. 자세한 내용은 [지연 된 콘텐츠 로드](loading-deferred-content-wcf-data-services.md)를 참조 하세요.

쿼리에서 반환되는 데이터의 양은 엔터티의 특정 속성만 응답에서 반환되도록 지정하여 줄일 수도 있습니다. 자세한 내용은 [쿼리 프로젝션](query-projections-wcf-data-services.md)을 참조 하세요.

## <a name="getting-a-count-of-the-total-number-of-entities-in-the-set"></a>집합의 총 엔터티 수 가져오기

일부 시나리오에서는 쿼리에서 반환되는 수뿐만 아니라 엔터티 집합의 총 엔터티 수를 아는 것이 유용합니다. 집합에 있는 이 총 엔터티 수가 쿼리 결과에 포함되도록 요청하려면 <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A>의 <xref:System.Data.Services.Client.DataServiceQuery%601> 메서드를 호출합니다. 이 경우 반환된 <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A>의 <xref:System.Data.Services.Client.QueryOperationResponse%601> 속성은 집합의 총 엔터티 수를 반환합니다.

<xref:System.Int32> 또는 <xref:System.Int64> 메서드를 호출하여 각각 <xref:System.Linq.Enumerable.Count%2A> 또는 <xref:System.Linq.Enumerable.LongCount%2A> 값으로 집합의 총 엔터티 수만 가져올 수도 있습니다. 이러한 메서드를 호출하면 <xref:System.Data.Services.Client.QueryOperationResponse%601>가 반환되지 않고 개수 값만 반환됩니다. 자세한 내용은 [방법: 쿼리에서](number-of-entities-returned-by-a-query-wcf.md)반환 되는 엔터티 수를 결정 합니다.

## <a name="in-this-section"></a>섹션 내용

- [프로젝트 쿼리](query-projections-wcf-data-services.md)

- [개체 구체화](object-materialization-wcf-data-services.md)

- [LINQ 고려 사항](linq-considerations-wcf-data-services.md)

- [방법: 데이터 서비스 쿼리 실행](how-to-execute-data-service-queries-wcf-data-services.md)

- [방법: 데이터 서비스 쿼리에 쿼리 옵션 추가](how-to-add-query-options-to-a-data-service-query-wcf-data-services.md)

- [방법: 쿼리에서 반환 되는 엔터티 수 결정](number-of-entities-returned-by-a-query-wcf.md)

- [방법: 데이터 서비스 요청에 대 한 클라이언트 자격 증명 지정](specify-client-creds-for-a-data-service-request-wcf.md)

- [방법: 클라이언트 요청에서 헤더 설정](how-to-set-headers-in-the-client-request-wcf-data-services.md)

- [방법: 프로젝트 쿼리 결과](how-to-project-query-results-wcf-data-services.md)

## <a name="see-also"></a>참고자료

- [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)
