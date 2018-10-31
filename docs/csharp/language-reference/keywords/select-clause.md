---
title: select 절(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- select_CSharpKeyword
- select
helpviewer_keywords:
- select keyword [C#]
- select clause [C#]
ms.assetid: df01e266-5781-4aaa-80c4-67cf28ea093f
ms.openlocfilehash: 3fa60d4e7546fc88ac2a2ffea45ae69b0da7a6a6
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50183544"
---
# <a name="select-clause-c-reference"></a>select 절(C# 참조)

쿼리 식에서 `select` 절은 쿼리를 실행할 때 생성되는 값의 형식을 지정합니다. 결과는 모든 이전 절의 평가와 `select` 절 자체의 모든 계산을 기반으로 합니다. 쿼리 식은 `select` 절이나 [group](group-clause.md) 절로 끝나야 합니다.

다음 예제에서는 쿼리 식의 간단한 `select` 절을 보여 줍니다.

[!code-csharp[cscsrefQueryKeywords#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Select.cs#8)]  

`select` 절에서 생성된 시퀀스의 형식에 따라 쿼리 변수 `queryHighScores`의 형식이 결정됩니다. 가장 단순한 경우에서는 `select` 절이 범위 변수를 지정합니다. 이렇게 하면 반환된 시퀀스에 데이터 소스와 동일한 형식의 요소가 포함됩니다. 자세한 내용은 [LINQ 쿼리 작업의 형식 관계](../../programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)를 참조하세요. 그러나 `select` 절은 소스 데이터를 새 형식으로 변환(또는 *프로젝션*)하기 위한 강력한 메커니즘도 제공합니다. 자세한 내용은 [LINQ를 통한 데이터 변환(C#)](../../programming-guide/concepts/linq/data-transformations-with-linq.md)을 참조하세요.

## <a name="example"></a>예

다음 예제에서는 `select` 절에 사용할 수 있는 모든 형식을 보여 줍니다. 각 쿼리에서 `select` 절과 *쿼리 변수* 형식(`studentQuery1`, `studentQuery2` 등) 간의 관계를 확인합니다.

[!code-csharp[cscsrefQueryKeywords#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Select.cs#9)]

앞의 예제에서 `studentQuery8`에 표시된 대로 반환된 시퀀스의 요소에 소스 요소의 속성 하위 집합만 포함하려는 경우도 있습니다. 반환된 시퀀스를 최대한 작게 유지하면 메모리 요구 사항을 줄이고 쿼리 실행 속도를 높일 수 있습니다. `select` 절에서 무명 형식을 만들고 개체 이니셜라이저를 사용하여 소스 요소의 적절한 속성으로 초기화하면 됩니다. 이 작업을 수행하는 방법의 예를 보려면 [개체 및 컬렉션 이니셜라이저](../../programming-guide/classes-and-structs/object-and-collection-initializers.md)를 참조하세요.

## <a name="remarks"></a>설명

컴파일 시간에 `select` 절은 <xref:System.Linq.Enumerable.Select%2A> 표준 쿼리 연산자에 대한 메서드 호출로 변환됩니다.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [쿼리 키워드(LINQ)](query-keywords.md)
- [from 절](from-clause.md)
- [partial(메서드)(C# 참조)](partial-method.md)
- [익명 형식](../../programming-guide/classes-and-structs/anonymous-types.md)
- [LINQ 쿼리 식](../../programming-guide/linq-query-expressions/index.md)
- [C#에서 LINQ 시작](../../programming-guide/concepts/linq/getting-started-with-linq.md)