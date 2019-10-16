---
title: '방법: 쿼리에 람다 식 사용 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [C#], in LINQ
ms.assetid: 3cac4d25-d11f-4abd-9e7c-0f02e97ae06d
ms.openlocfilehash: bb784528226c706417166025a2469ed9f72f9cc2
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588656"
---
# <a name="how-to-use-lambda-expressions-in-a-query-c-programming-guide"></a>방법: 쿼리에 람다 식 사용(C# 프로그래밍 가이드)
람다 식은 쿼리 구문에 직접 사용하지 않고 메서드 호출에 사용하며, 쿼리 식에 메서드 호출이 포함될 수 있습니다. 실제로 일부 쿼리 작업은 메서드 구문으로만 표현할 수 있습니다. 쿼리 구문과 메서드 구문 간의 차이점에 대한 자세한 내용은 [LINQ의 쿼리 구문 및 메서드 구문](../concepts/linq/query-syntax-and-method-syntax-in-linq.md)을 참조하세요.  
  
## <a name="example"></a>예  
 다음 예제에서는 <xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType> 표준 쿼리 연산자를 사용하여 메서드 기반 쿼리에 람다 식을 사용하는 방법을 보여 줍니다. 이 예제의 <xref:System.Linq.Enumerable.Where%2A> 메서드에는 대리자 형식 <xref:System.Func%602>의 입력 매개 변수가 있으며, 해당 대리자는 정수를 입력으로 사용하고 부울을 반환합니다. 람다 식을 해당 대리자로 변환할 수 있습니다. <xref:System.Linq.Queryable.Where%2A?displayProperty=nameWithType> 메서드를 사용하는 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 쿼리인 경우 매개 변수 형식은 `Expression<Func<int,bool>>`이지만 람다 식은 정확히 동일하게 표시됩니다. 식 형식에 대한 자세한 내용은 <xref:System.Linq.Expressions.Expression?displayProperty=nameWithType>을 참조하세요.  
  
 [!code-csharp[csProgGuideLINQ#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csrefLINQHowTos.cs#1)]  
  
## <a name="example"></a>예  
 다음 예제에서는 쿼리 식의 메서드 호출에 람다 식을 사용하는 방법을 보여 줍니다. 쿼리 구문을 사용하여 <xref:System.Linq.Enumerable.Sum%2A> 표준 쿼리 연산자를 호출할 수 없기 때문에 람다가 필요합니다.  
  
 쿼리는 먼저 `GradeLevel` 열거형에 정의된 성적 수준에 따라 학생을 그룹화합니다. 그런 다음 각 그룹에 대해 각 학생의 총 점수를 더합니다. 이 경우 두 개의 `Sum` 연산이 필요합니다. 안쪽 `Sum`은 각 학생의 총 점수를 계산하고, 바깥쪽 `Sum`은 그룹에 속한 모든 학생에 대해 합산된 누계를 유지합니다.  
  
 [!code-csharp[csProgGuideLINQ#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csrefLINQHowTos.cs#2)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 코드를 실행하려면 메서드를 복사하여 [방법: 개체 컬렉션 쿼리](../linq-query-expressions/how-to-query-a-collection-of-objects.md)에 제공된 로 붙여넣은 후 `Main` 메서드에서 호출합니다.  
  
## <a name="see-also"></a>참고 항목

- [람다 식](./lambda-expressions.md)
- [식 트리(C#)](../concepts/expression-trees/index.md)
