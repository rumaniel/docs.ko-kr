---
title: null 비교
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ef88af8c-8dfe-4556-8b56-81df960a900b
ms.openlocfilehash: 0996b7d864c5892e383cb98d4065e99b096206d1
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854327"
---
# <a name="null-comparisons"></a>null 비교
데이터 소스의 `null` 값은 값을 알 수 없음을 나타냅니다. LINQ to Entities 쿼리에서는 null 값을 확인할 수 있습니다. 즉, null 값 또는 null이 아닌 데이터가 있는 행 에서만 특정 계산 또는 비교가 수행 되도록 할 수 있습니다. 그러나 CLR Null 의미 체계는 데이터 소스의 Null 의미 체계와 다를 수 있습니다. 대부분의 데이터베이스는 세 개의 값으로 구성된 논리 버전을 사용하여 Null 비교를 처리합니다. 즉, Null 값에 대한 비교는 `true` 또는 `false`가 되지 않고 `unknown`이 됩니다. ANSI Null은 이렇게 구현되는 경우가 많지만 항상 그런 것은 아닙니다.  
  
 기본적으로 SQL Server에서 Null은 Null과 같음 비교는 Null 값을 반환합니다. 다음 예에서는 `ShipDate` 가 null 인 행은 결과 집합에서 제외 되 고 transact-sql 문은 0 개 행을 반환 합니다.  
  
```  
-- Find order details and orders with no ship date.  
SELECT h.SalesOrderID  
FROM Sales.SalesOrderHeader h  
JOIN Sales.SalesOrderDetail o ON o.SalesOrderID = h.SalesOrderID  
WHERE h.ShipDate IS Null  
```  
  
 Null은 Null과 같음 비교에서 true를 반환하는 CLR Null 의미 체계와 이 동작은 전혀 다릅니다.  
  
 다음 LINQ 쿼리는 CLR로 표현되지만 데이터 소스에서 실행됩니다. CLR 의미 체계가 데이터 소스에서 반영될 것이라는 보장이 없으므로 예상 동작을 결정할 수 없습니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#JoinOnNull](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#joinonnull)]
 [!code-vb[DP L2E Conceptual Examples#JoinOnNull](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#joinonnull)]  
  
## <a name="key-selectors"></a>키 선택기  
 *키 선택기* 는 표준 쿼리 연산자가 요소에서 키를 추출 하는 데 사용 되는 함수입니다. 키 선택기 함수에서 식을 상수와 비교할 수 있습니다. 식을 Null 상수와 비교하거나 두 개의 Null 상수를 비교하면 CLR Null 의미 체계가 표시됩니다. 데이터 소스에서 Null 값을 가진 두 개의 열을 비교하면 저장소 Null 의미 체계가 표시됩니다. 키 선택기는 <xref:System.Linq.Queryable.GroupBy%2A>과 같은 대부분의 그룹화 및 정렬 표준 쿼리 연산자에서 발견되며, 쿼리 결과를 정렬하거나 그룹화하는 기준 키를 선택하는 데 사용됩니다.  
  
## <a name="null-property-on-a-null-object"></a>Null 개체의 Null 속성  
 Entity Framework에서 null 개체의 속성은 null입니다. CLR에서 Null 개체의 속성을 참조하려고 하면 <xref:System.NullReferenceException>이 발생합니다. LINQ 쿼리에 Null 개체의 속성이 필요한 경우 일관성 없는 동작이 발생할 수 있습니다.  
  
 예를 들어, 다음 쿼리에서 `NewProduct`로의 캐스팅은 명령 트리 계층에서 수행되며, 이로 인해 `Introduced` 속성이 Null이 될 수 있습니다. <xref:System.DateTime> 비교가 true가 되도록 데이터베이스에서 Null 비교를 정의한 경우 해당 행이 포함됩니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#CastResultsIsNull](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#castresultsisnull)]
 [!code-vb[DP L2E Conceptual Examples#CastResultsIsNull](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#castresultsisnull)]  
  
## <a name="passing-null-collections-to-aggregate-functions"></a>Null 컬렉션을 집계 함수에 전달  
 LINQ to Entities에서를 지 원하는 `IQueryable` 컬렉션을 집계 함수에 전달 하면 데이터베이스에서 집계 작업이 수행 됩니다. 메모리 내에서 수행 된 쿼리와 데이터베이스에서 수행 된 쿼리 결과에 차이가 있을 수 있습니다. 메모리 내 쿼리를 사용 하는 경우 일치 하는 항목이 없는 경우 쿼리는 0을 반환 합니다. 데이터베이스에서 동일한 쿼리가 `null`을 반환합니다. `null` 값이 LINQ 집계 함수에 전달 되 면 예외가 throw 됩니다. 가능한 `null` 값을 허용 하려면 쿼리 결과를 수신 하는 형식의 형식 및 속성을 nullable 형식으로 캐스팅 합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to Entities 쿼리의 식](expressions-in-linq-to-entities-queries.md)
