---
title: C#에서 LINQ 쿼리 작성하기
description: C#에서 LINQ 쿼리를 작성하는 방법을 알아봅니다.
ms.date: 12/01/2016
ms.assetid: 30703f79-cf3a-4d02-b892-c95d58a1d9ed
ms.openlocfilehash: ed32543b0422e0664a8577f2c27f7c7c00a719a1
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632891"
---
# <a name="write-linq-queries-in-c"></a>C\#에서 LINQ 쿼리 작성하기

이 문서에서는 C#에서 LINQ 쿼리를 작성할 수 있는 세 가지 방법을 보여 줍니다.

1. 쿼리 구문을 사용합니다.

2. 메서드 구문을 사용합니다.

3. 쿼리 구문과 메서드 구문을 조합해서 사용합니다.

다음 예제에서는 앞서 나열한 각 방법을 사용하여 몇몇 간단한 LINQ 쿼리를 보여 줍니다. 일반적인 규칙은 가능한 경우 항상 (1)을 사용하고, 필요할 때마다 (2) 및 (3)을 사용하는 것입니다.

> [!NOTE]
> 이러한 쿼리는 간단한 메모리 내 컬렉션에서 작동합니다. 그러나 기본 구문은 LINQ to Entities 및 LINQ to XML에서 사용되는 구문과 동일합니다.

## <a name="example---query-syntax"></a>예제 - 쿼리 구문

대부분의 쿼리를 작성하는 권장 방법은 *쿼리 구문*을 사용하여 *쿼리 식*을 만드는 것입니다. 다음 예제는 세 개의 쿼리 식을 보여 줍니다. 첫 번째 쿼리 식은 `where` 절과 함께 조건을 적용하여 결과를 필터링 또는 제한하는 방법을 보여 줍니다. 이 식은 값이 7보다 크거나 3보다 작은 소스 시퀀스의 모든 요소를 반환합니다. 두 번째 식은 반환된 결과를 정렬하는 방법을 보여 줍니다. 세 번째 식은 키에 따라 결과를 그룹화하는 방법을 보여 줍니다. 이 쿼리는 단어의 첫 글자를 기반으로 두 그룹을 반환합니다.

[!code-csharp[csProgGuideLINQ#5](~/samples/snippets/csharp/concepts/linq/how-to-write-linq-queries_1.cs)]

쿼리의 형식은 <xref:System.Collections.Generic.IEnumerable%601>입니다. 다음 예제와 같이 이러한 모든 쿼리는 `var`을 사용해 작성할 수 있습니다.

`var query = from num in numbers...`

이전의 각 예제에서는 `foreach` 문 또는 다른 문에서 쿼리 변수를 반복할 때까지 실제로 쿼리가 실행되지 않습니다. 자세한 내용은 [LINQ 쿼리 소개](../programming-guide/concepts/linq/introduction-to-linq-queries.md)를 참조하세요.

## <a name="example---method-syntax"></a>예제 - 메서드 구문

일부 쿼리 작업은 메서드 호출로 표현해야 합니다. 가장 일반적인 메서드는 singleton 숫자 값을 반환하는 <xref:System.Linq.Enumerable.Sum%2A>, <xref:System.Linq.Enumerable.Max%2A>, <xref:System.Linq.Enumerable.Min%2A>, <xref:System.Linq.Enumerable.Average%2A> 등입니다. 이러한 메서드는 단일 값만 나타내며 추가 쿼리 작업의 소스로 사용할 수 없기 때문에 항상 모든 쿼리에서 마지막에 호출해야 합니다. 다음 예제는 쿼리 식에서의 메서드 호출을 보여 줍니다.

[!code-csharp[csProgGuideLINQ#6](~/samples/snippets/csharp/concepts/linq/how-to-write-linq-queries_2.cs)]

메서드에 Action 또는 Func 매개 변수가 있는 경우 다음 예제와 같이 [lambda](../programming-guide/statements-expressions-operators/lambda-expressions.md) 식의 형식으로 제공됩니다.

[!code-csharp[csProgGuideLINQ#7](~/samples/snippets/csharp/concepts/linq/how-to-write-linq-queries_3.cs)]

이전 쿼리에서 쿼리 #4만 즉시 실행됩니다. 그 이유는 해당 쿼리가 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 컬렉션이 아니라 단일 값을 반환하기 때문입니다. 메서드 자체는 값을 계산하기 위해 `foreach`를 사용해야 합니다.

다음 예제와 같이 [var](../language-reference/keywords/var.md)과 함께 암시적 형식을 사용하여 각각의 이전 쿼리를 작성할 수 있습니다.

[!code-csharp[csProgGuideLINQ#8](~/samples/snippets/csharp/concepts/linq/how-to-write-linq-queries_4.cs)]

## <a name="example---mixed-query-and-method-syntax"></a>예제 - 혼합된 쿼리 및 메서드 구문

이 예제는 쿼리 절의 결과에서 메서드 구문을 사용하는 방법을 보여 줍니다. 쿼리 식을 괄호로 묶은 다음 점 연산자를 적용하고 메서드를 호출하면 됩니다. 다음 예제에서 쿼리 #7은 값이 3과 7 사이인 숫자의 수를 반환합니다. 그러나 일반적으로 두 번째 변수를 사용하여 메서드 호출의 결과를 저장하는 것이 좋습니다. 이렇게 하면 쿼리가 쿼리의 결과와 혼동될 가능성이 줄어듭니다.

[!code-csharp[csProgGuideLINQ#9](~/samples/snippets/csharp/concepts/linq/how-to-write-linq-queries_5.cs)]

쿼리 #7은 컬렉션이 아닌 단일 값을 반환하므로 쿼리가 즉시 실행됩니다.

이전 쿼리는 다음과 같이 `var`과 함께 암시적 형식을 사용하여 작성할 수 있습니다.

```csharp
var numCount = (from num in numbers...
```

다음과 같이 메서드 구문에서 작성할 수 있습니다.

```csharp
var numCount = numbers.Where(n => n < 3 || n > 7).Count();
```

다음과 같이 명시적 형식을 사용하여 작성할 수 있습니다.

```csharp
int numCount = numbers.Where(n => n < 3 || n > 7).Count();
```

## <a name="see-also"></a>참고 항목

- [연습: C#에서 쿼리 작성](../programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)
- [LINQ(Language-Integrated Query)](index.md)
- [where 절](../language-reference/keywords/where-clause.md)
