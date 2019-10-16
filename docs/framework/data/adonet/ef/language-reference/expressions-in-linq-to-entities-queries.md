---
title: LINQ to Entities 쿼리의 식
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d70b502f-6a15-4120-b4fe-500b173ad9cc
ms.openlocfilehash: e625ac3968542c65e737093c0ac292de4c2ffa37
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854463"
---
# <a name="expressions-in-linq-to-entities-queries"></a>LINQ to Entities 쿼리의 식
식은 단일 값, 개체, 메서드, 네임스페이스 등으로 계산될 수 있는 코드의 일부입니다. 식에는 리터럴 값, 메서드 호출, 연산자와 해당 피연산자, 단순한 이름 등이 포함될 수 있습니다. 단순한 이름이란 변수, 형식 멤버, 메서드 매개 변수, 네임스페이스 또는 형식의 이름일 수 있습니다. 식은 다른 식을 매개 변수로 사용하는 연산자를 사용할 수 있으며 다른 메서드 호출을 매개 변수로 가지는 메서드 호출을 사용할 수도 있습니다. 따라서 식은 단순한 형태에서 매우 복잡한 형태까지 다양합니다.  
  
 LINQ to Entities 쿼리에서 식에는 람다 식을 포함 하 여 <xref:System.Linq.Expressions> 네임 스페이스 내의 형식에서 허용 되는 모든 항목이 포함 될 수 있습니다. LINQ to Entities 쿼리에서 사용할 수 있는 식은 Entity Framework을 쿼리 하는 데 사용할 수 있는 식의 상위 집합입니다. Entity Framework에 대 한 쿼리의 일부인 식은 및에서 `ObjectQuery<T>` 지 원하는 작업으로 제한 됩니다. 내부 데이터 소스입니다.  
  
 다음 예제에서 `Where` 절의 비교는 식입니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#whereexpression)]
 [!code-vb[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#whereexpression)]  
  
> [!NOTE]
> C# 과`unchecked`같은 특정 언어 구문은 LINQ to Entities 의미가 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [상수 식](constant-expressions.md)  
  
 [식 비교](comparison-expressions.md)  
  
 [null 비교](null-comparisons.md)  
  
 [초기화 식](initialization-expressions.md)  
  
 [관계, 탐색 속성 및 외래 키](/ef/ef6/fundamentals/relationships)  
  
## <a name="see-also"></a>참고자료

- [ADO.NET Entity Framework](../index.md)
