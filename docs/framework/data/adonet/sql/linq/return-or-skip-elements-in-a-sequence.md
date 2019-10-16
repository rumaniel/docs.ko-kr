---
title: 시퀀스에서 요소 반환 또는 건너뛰기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 81a31acd-e0f1-4bca-9a12-fa1ad5752374
ms.openlocfilehash: 7c98681493738b4e94ed14417fa1437efb6c12ac
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72003315"
---
# <a name="return-or-skip-elements-in-a-sequence"></a>시퀀스에서 요소 반환 또는 건너뛰기
<xref:System.Linq.Queryable.Take%2A> 연산자를 사용하여 지정된 수의 시퀀스 요소를 반환한 다음 나머지는 건너뜁니다.  
  
 <xref:System.Linq.Queryable.Skip%2A> 연산자를 사용하여 지정된 수의 시퀀스 요소를 건너뛴 다음 나머지를 반환합니다.  
  
> [!NOTE]
> <xref:System.Linq.Enumerable.Take%2A> 및 <xref:System.Linq.Enumerable.Skip%2A>에는 SQL Server 2000에 대한 쿼리에서 사용할 경우 몇 가지 제한이 따릅니다. 자세한 내용은 [문제 해결](troubleshooting.md)에서 "SQL Server 2000의 Skip 및 Take 예외" 항목을 참조 하세요.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 하위 쿼리와 함께 SQL <xref:System.Linq.Queryable.Skip%2A> 절을 사용하여 `NOT EXISTS`을 변환합니다. 이 변환에는 다음과 같은 제한 사항이 있습니다.  
  
- 인수는 집합이어야 합니다. 다중 집합은 정렬된 경우에도 지원되지 않습니다.  
  
- 생성된 쿼리는 <xref:System.Linq.Queryable.Skip%2A>이 적용된 기본 쿼리에 대해 생성된 쿼리보다 더 복잡할 수 있습니다. 이러한 복잡성은 성능을 감소시키거나 시간이 초과될 수도 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Take`를 사용하여 고용된 처음 다섯 명의 `Employees`를 선택합니다. 컬렉션은 우선 `HireDate`로 정렬됩니다.  
  
 [!code-csharp[DLinqQueryExamples#16](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#16)]
 [!code-vb[DLinqQueryExamples#16](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#16)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Linq.Queryable.Skip%2A>을 사용하여 10개의 가장 비싼 `Products`를 제외한 모두를 선택합니다.  
  
 [!code-csharp[DLinqQueryExamples#17](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#17)]
 [!code-vb[DLinqQueryExamples#17](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#17)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Linq.Queryable.Skip%2A>과 <xref:System.Linq.Queryable.Take%2A> 메서드를 결합하여 처음 50개의 레코드를 건너뛴 다음 그 이후 10개의 레코드를 반환합니다.  
  
 [!code-csharp[DLinqQueryExamples#18](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#18)]
 [!code-vb[DLinqQueryExamples#18](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#18)]  
  
 <xref:System.Linq.Queryable.Take%2A> 및 <xref:System.Linq.Queryable.Skip%2A> 작업은 정렬된 집합에 대해서만 제대로 정의됩니다. 정렬되지 않는 집합 또는 다중 집합에 대한 의미는 정의되어 있지 않습니다.  
  
 SQL의 정렬에 대한 제한 사항 때문에 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 <xref:System.Linq.Queryable.Take%2A> 또는 <xref:System.Linq.Queryable.Skip%2A> 연산자의 정렬 인수가 연산자의 결과로 이동합니다.  
  
> [!NOTE]
> SQL Server 2000 및 SQL Server 2005에서는 번역이 다릅니다. 복잡성 쿼리를 사용 하 여 <xref:System.Linq.Queryable.Skip%2A>을 사용 하려면 SQL Server 2005를 사용 합니다.  
  
 SQL Server 2000에 대 한 다음 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 쿼리를 참조 하세요.  
  
 [!code-csharp[DLinqQueryExamples#19](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#19)]
 [!code-vb[DLinqQueryExamples#19](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#19)]  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 다음과 같이 정렬을 SQL 코드의 끝 부분으로 이동합니다.  
  
```sql
SELECT TOP 1 [t0].[CustomerID], [t0].[CompanyName],  
FROM [Customers] AS [t0]  
WHERE (NOT (EXISTS(  
    SELECT NULL AS [EMPTY]  
    FROM (  
        SELECT TOP 1 [t1].[CustomerID]  
        FROM [Customers] AS [t1]  
        WHERE [t1].[City] = @p0  
        ORDER BY [t1].[CustomerID]  
        ) AS [t2]  
    WHERE [t0].[CustomerID] = [t2].[CustomerID]  
    ))) AND ([t0].[City] = @p1)  
ORDER BY [t0].[CustomerID]  
```  
  
 <xref:System.Linq.Queryable.Take%2A>과 <xref:System.Linq.Queryable.Skip%2A>을 함께 연결하면 모든 지정된 정렬이 일치해야 합니다. 그렇지 않으면 결과가 정의되지 않습니다.  
  
 SQL 사양을 기반으로 하는 정수 계열 상수 인수로 음수가 아닌 경우 <xref:System.Linq.Queryable.Take%2A>과 <xref:System.Linq.Queryable.Skip%2A>은 제대로 정의됩니다.  
  
## <a name="see-also"></a>참조

- [쿼리 예제](query-examples.md)
- [표준 쿼리 연산자 변환](standard-query-operator-translation.md)
