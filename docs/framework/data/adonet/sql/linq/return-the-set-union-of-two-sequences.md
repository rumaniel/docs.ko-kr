---
title: 두 시퀀스의 합집합 반환
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8b8bd3cb-86d4-4a3b-9906-61f68726dd1f
ms.openlocfilehash: ffdc1dc0f9b5c2ed3b9898d0c71c9b384723fe05
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200562"
---
# <a name="return-the-set-union-of-two-sequences"></a>두 시퀀스의 합집합 반환
<xref:System.Linq.Queryable.Union%2A> 연산자를 사용하여 두 시퀀스의 합집합을 반환합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 <xref:System.Linq.Queryable.Union%2A>을 사용하여 `Customers` 또는 `Employees`가 있는 모든 국가의 시퀀스를 반환합니다.  
  
 [!code-csharp[DLinqQueryExamples#43](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#43)]
 [!code-vb[DLinqQueryExamples#43](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#43)]  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]는 <xref:System.Linq.Queryable.Union%2A> 다중 집합의 순서가 지정 되지 않은 연결으로 다중 집합에 대해 연산자가 정의 (효율적인 결과 합니다 [ `UNION ALL` ](https://docs.microsoft.com/sql/t-sql/language-elements/set-operators-union-transact-sql?view=sql-server-2017) SQL 절).

자세한 정보 및 예제를 참조 하세요. <xref:System.Linq.Queryable.Union%2A?displayProperty=nameWithType>합니다.
  
## <a name="see-also"></a>참고 항목  
 [쿼리 예제](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)  
 [표준 쿼리 연산자 변환](../../../../../../docs/framework/data/adonet/sql/linq/standard-query-operator-translation.md)
