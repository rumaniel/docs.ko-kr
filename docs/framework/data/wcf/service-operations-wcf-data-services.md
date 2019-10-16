---
title: 서비스 작업(WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service operations [WCF Data Services]
- WCF Data Services, service operations
ms.assetid: 583a690a-e60f-4990-8991-d6efce069d76
ms.openlocfilehash: 4f36081ef1a3eec84f3cc2ced3c629109acd6a38
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894277"
---
# <a name="service-operations-wcf-data-services"></a>서비스 작업(WCF Data Services)

[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 사용하면 데이터 서비스에 서버의 메서드를 노출하는 서비스 작업을 정의할 수 있습니다. 다른 데이터 서비스 리소스와 마찬가지로 서비스 작업도 URI로 주소가 지정됩니다. 서비스 작업을 사용하면 유효성 검사 논리 구현, 역할 기반 보안 적용 또는 특수 쿼리 기능 노출 등을 위해 데이터 서비스에 비즈니스 논리를 노출할 수 있습니다. 서비스 작업은 <xref:System.Data.Services.DataService%601>에서 파생되는 데이터 서비스 클래스에 추가된 메서드입니다. 다른 모든 데이터 서비스 리소스와 마찬가지로 서비스 작업 메서드에 매개 변수를 제공할 수 있습니다. 예를 들어 다음 서비스 작업 URI ( [퀵 스타트](quickstart-wcf-data-services.md) 데이터 서비스 기반)는 값 `London` `city` 을 매개 변수에 전달 합니다.

```http
http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'
```

이 서비스 작업의 정의는 다음과 같습니다.

[!code-csharp[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#serviceoperationdef)]
[!code-vb[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#serviceoperationdef)]

<xref:System.Data.Services.DataService%601.CurrentDataSource%2A>의 <xref:System.Data.Services.DataService%601>를 사용하여 데이터 서비스에서 사용하는 데이터 소스에 직접 액세스할 수 있습니다. 자세한 내용은 [방법: 서비스 작업](how-to-define-a-service-operation-wcf-data-services.md)을 정의 합니다.

.NET Framework 클라이언트 응용 프로그램에서 서비스 작업을 호출 하는 방법에 대 한 자세한 내용은 [서비스 작업 호출](calling-service-operations-wcf-data-services.md)을 참조 하세요.

## <a name="service-operation-requirements"></a>서비스 작업 요구 사항

데이터 서비스에 서비스 작업을 정의할 때 적용되는 요구 사항은 다음과 같습니다. 이러한 요구 사항을 충족하지 않는 메서드는 데이터 서비스의 서비스 작업으로 노출되지 않습니다.

- 작업은 데이터 서비스 클래스의 멤버인 공용 인스턴스 메서드여야 합니다.

- 작업 메서드는 입력 매개 변수만 허용할 수 있습니다. 메시지 본문에 전송되는 데이터는 데이터 서비스가 액세스할 수 없습니다.

- 매개 변수를 정의할 때 각 매개 변수의 형식은 기본 형식이어야 합니다. 기본이 아닌 형식의 모든 데이터는 serialize한 다음 문자열 매개 변수로 전달해야 합니다.

- 메서드는 다음 중 하나를 반환해야 합니다.

  - `void`(Visual Basic에서는 `Nothing`)

  - <xref:System.Collections.Generic.IEnumerable%601>

  - <xref:System.Linq.IQueryable%601>

  - 데이터 서비스에서 노출하는 데이터 모델의 엔터티 형식

  - 정수 또는 문자열과 같은 기본 클래스

- 정렬, 페이징, 필터링 등의 쿼리 옵션을 지원할 수 있도록 서비스 작업 메서드가 <xref:System.Linq.IQueryable%601>를 반환해야 합니다. <xref:System.Collections.Generic.IEnumerable%601>만 반환하는 작업의 경우 쿼리 옵션을 포함하는 서비스 작업 요청이 거부됩니다.

- 탐색 속성을 사용하여 관련 엔터티에 액세스할 수 있도록 지원하려면 서비스 작업이 <xref:System.Linq.IQueryable%601>을 반환해야 합니다.

- 메서드에 `[WebGet]` 또는 `[WebInvoke]` 특성으로 주석을 달아야 합니다.

  - `[WebGet]`을 사용하면 GET 요청을 통해 메서드를 호출할 수 있습니다.

  - `[WebInvoke(Method = "POST")]`을 사용하면 POST 요청을 통해 메서드를 호출할 수 있습니다. 다른 <xref:System.ServiceModel.Web.WebInvokeAttribute> 메서드는 지원되지 않습니다.

- 메서드의 반환 값이 엔터티 컬렉션이 아니라 단일 엔터티가 되도록 지정하는 <xref:System.Data.Services.SingleResultAttribute>를 서비스 작업에 주석으로 추가할 수도 있습니다. 이 특성은 응답의 결과 serialization과 추가 탐색 속성 통과가 URI에 표시되는 방식을 제어합니다. 예를 들어 AtomPub serialization을 사용할 경우 단일 리소스 형식 인스턴스는 entry 요소로 나타나고 인스턴스 집합은 feed 요소로 나타납니다.

## <a name="addressing-service-operations"></a>서비스 작업 주소 지정

URI의 첫 번째 경로 세그먼트에 메서드 이름을 배치하여 서비스 작업의 주소를 지정할 수 있습니다. 예를 들어 다음 URI는 `GetOrdersByState` 개체의 <xref:System.Linq.IQueryable%601> 컬렉션을 반환하는 `Orders` 작업에 액세스합니다.

```http
http://localhost:12345/Northwind.svc/GetOrdersByState?state='CA'&includeItems=true
```

서비스 작업을 호출할 때 매개 변수는 쿼리 옵션으로 제공됩니다. 이전 서비스 작업은 문자열 매개 변수 `state`와 관련 `includeItems` 개체를 응답에 포함해야 하는지 여부를 나타내는 부울 매개 변수 `Order_Detail` 둘 다를 허용합니다.

서비스 작업에 대해 유효한 반환 형식은 다음과 같습니다.

|유효한 반환 형식|URI 규칙|
|------------------------|---------------|
|`void`(Visual Basic에서는 `Nothing`)<br /><br /> 또는<br /><br /> 엔터티 형식<br /><br /> 또는<br /><br /> 기본 형식|URI는 서비스 작업의 이름에 해당하는 단일 경로 세그먼트여야 합니다. 쿼리 옵션은 허용되지 않습니다.|
|<xref:System.Collections.Generic.IEnumerable%601>|URI는 서비스 작업의 이름에 해당하는 단일 경로 세그먼트여야 합니다. 결과 형식이 <xref:System.Linq.IQueryable%601> 형식이 아니므로 쿼리 옵션은 허용되지 않습니다.|
|<xref:System.Linq.IQueryable%601>|서비스 작업의 이름에 해당하는 경로 외에도 쿼리 경로 세그먼트가 허용됩니다. 쿼리 옵션도 허용됩니다.|

서비스 작업의 반환 형식에 따라 추가 경로 세그먼트나 쿼리 옵션이 URI에 추가될 수도 있습니다. 예를 들어 다음 URI는 관련 `GetOrdersByCity` 개체와 함께 <xref:System.Linq.IQueryable%601> 개체의 `Orders` 컬렉션을 `RequiredDate`의 내림차순으로 정렬하여 반환하는 `Order_Details` 작업에 액세스합니다.

```http
http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$expand=Order_Details&$orderby=RequiredDate desc
```

## <a name="service-operations-access-control"></a>서비스 작업 액세스 제어

서비스 전반에 걸친 서비스 작업의 표시는 <xref:System.Data.Services.IDataServiceConfiguration.SetServiceOperationAccessRule%2A> 클래스의 <xref:System.Data.Services.IDataServiceConfiguration> 메서드에 의해 제어되며, 이는 엔터티 집합의 표시가 <xref:System.Data.Services.IDataServiceConfiguration.SetEntitySetAccessRule%2A> 메서드를 사용하여 제어되는 방식과 상당 부분 유사합니다. 예를 들어, 데이터 서비스 정의의 다음 코드 줄은 `CustomersByCity` 서비스 작업에 액세스할 수 있도록 합니다.

[!code-csharp[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#serviceoperationconfig)]
[!code-vb[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#serviceoperationconfig)]

> [!NOTE]
> 서비스 작업의 반환 형식이 기본 엔터티 집합에 대한 액세스를 제한하여 숨겨진 경우에는 클라이언트 애플리케이션에서 서비스 작업을 사용할 수 없습니다.

자세한 내용은 [방법: 서비스 작업](how-to-define-a-service-operation-wcf-data-services.md)을 정의 합니다.

## <a name="raising-exceptions"></a>예외 발생

데이터 서비스 실행에서 예외를 발생시킬 때마다 <xref:System.Data.Services.DataServiceException> 클래스를 사용하는 것이 좋습니다. 그 이유는 데이터 서비스 런타임이 이 예외 개체의 속성을 HTTP 응답 메시지에 올바르게 매핑하는 방법을 알기 때문입니다. 서비스 작업에서 <xref:System.Data.Services.DataServiceException>을 발생시키면 반환된 예외가 <xref:System.Reflection.TargetInvocationException>으로 래핑됩니다. <xref:System.Data.Services.DataServiceException>을 묶지 않고 기본 <xref:System.Reflection.TargetInvocationException>을 반환하려면 다음 예제와 같이 <xref:System.Data.Services.DataService%601.HandleException%2A>에 <xref:System.Data.Services.DataService%601> 메서드를 재정의하고 <xref:System.Data.Services.DataServiceException>에서 <xref:System.Reflection.TargetInvocationException>을 추출해서 최상위 오류로 반환해야 합니다.

[!code-csharp[Astoria Northwind Service#HandleExceptions](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#handleexceptions)]
[!code-vb[Astoria Northwind Service#HandleExceptions](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#handleexceptions)]

## <a name="see-also"></a>참고자료

- [인터셉터](interceptors-wcf-data-services.md)
