---
title: from 절(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- from_CSharpKeyword
- from
helpviewer_keywords:
- from clause [C#]
- from keyword [C#]
ms.assetid: 1aefd18c-1314-47f8-99ec-9bcefb09e699
ms.openlocfilehash: c8c124f44df292b8323560cce541cca2765e2790
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48033404"
---
# <a name="from-clause-c-reference"></a>from 절(C# 참조)

쿼리 식은 `from` 절로 시작해야 합니다. 또한 쿼리 식은 `from` 절로 시작하는 하위 쿼리를 포함할 수 있습니다. `from` 절은 다음 내용을 지정합니다.

- 쿼리 또는 하위 쿼리가 실행될 데이터 소스.

- 소스 시퀀스의 각 요소를 나타내는 지역 *범위 변수*.

범위 변수 및 데이터 소스 모두 강력한 형식입니다. `from` 절에서 참조되는 데이터 소스는 <xref:System.Collections.IEnumerable> 또는 <xref:System.Collections.Generic.IEnumerable%601> 형식이거나 <xref:System.Linq.IQueryable%601>와 같은 파생 형식이어야 합니다.

다음 예제에서 `numbers`는 데이터 소스이고 `num`은 범위 변수입니다. [var](var.md) 키워드가 사용되어도 두 변수는 모두 강력한 형식입니다.

[!code-csharp[cscsrefQueryKeywords#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/From.cs#1)]

## <a name="the-range-variable"></a>범위 변수

컴파일러는 데이터 소스가 <xref:System.Collections.Generic.IEnumerable%601>을 구현할 경우 범위 변수의 형식을 유추합니다. 예를 들어, 소스의 형식이 `IEnumerable<Customer>`일 경우 범위 변수는 `Customer`로 유추됩니다. 소스가 <xref:System.Collections.ArrayList>와 같이 제네릭이 아닌 `IEnumerable` 형식인 경우에만 형식을 명시적으로 지정하면 됩니다. 자세한 내용은 [LINQ를 사용하여 ArrayList 쿼리](../../programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)를 참조하세요.

위의 예제에서 `num`은 `int` 형식으로 유추됩니다. 범위 변수가 강력한 형식이므로 범위 변수에서 메서드를 호출하거나 다른 작업에서 범위 변수를 사용할 수 있습니다. 예를 들어 `select num`을 작성하는 대신에 `select num.ToString()`을 작성하여 쿼리 식에서 정수 대신 문자열 시퀀스를 반환하게 할 수 있습니다. 또는 `select n + 10`을 작성하여 식에서 14, 11, 13, 12, 10 시퀀스를 반환하게 할 수 있습니다. 자세한 내용은 [select 절](select-clause.md)을 참조하세요.

범위 변수가 소스의 데이터를 실제로 저장하지 않는다는 매우 중요한 한 가지 차이점을 제외하면 범위 변수는 [foreach](foreach-in.md) 문의 반복 변수와 같습니다. 범위 변수는 단순히 쿼리 실행 시에 발생하는 작업을 쿼리에서 설명할 수 있게 하는 구문상의 편리함을 제공합니다. 자세한 내용은 [LINQ 쿼리 소개(C#)](../../programming-guide/concepts/linq/introduction-to-linq-queries.md)를 참조하세요.

## <a name="compound-from-clauses"></a>복합 from 절

경우에 따라 소스 시퀀스의 각 요소 자체가 시퀀스이거나 시퀀스를 포함할 수 있습니다. 예를 들어, 시퀀스의 각 학생 개체에 테스트 점수 목록이 포함된 `IEnumerable<Student>`가 데이터 소스일 수 있습니다. 각 `Student` 요소 내의 내부 목록에 액세스하려면 복합 `from` 절을 사용합니다. 이 기술은 중첩된 [foreach](foreach-in.md) 문을 사용하는 것과 같습니다. [where](partial-method.md) 또는 [orderby](orderby-clause.md) 절을 둘 중 하나의 `from` 절에 추가하여 결과를 필터링할 수 있습니다. 다음 예제에서는 테스트 점수를 나타내는 정수의 내부 `List`를 각각 포함하는 `Student` 개체의 시퀀스를 보여 줍니다. 내부 목록에 액세스하려면 복합 `from` 절을 사용합니다. 필요한 경우 두 `from` 절 사이에 다른 절을 삽입할 수 있습니다.

[!code-csharp[cscsrefQueryKeywords#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/From.cs#2)]

## <a name="using-multiple-from-clauses-to-perform-joins"></a>여러 from 절을 사용하여 조인 수행

복합 `from` 절은 단일 데이터 소스의 내부 컬렉션에 액세스하는 데 사용됩니다. 그러나 독립 데이터 소스의 추가 쿼리를 생성하는 여러 `from` 절이 쿼리에 포함될 수도 있습니다. 이 기술을 사용하면 [join 절](join-clause.md)로 수행할 수 없는 특정 형식의 조인 작업을 수행할 수 있습니다.

다음 예제는 두 개의 `from` 절을 사용하여 두 개의 데이터 소스의 완전한 크로스 조인을 구성하는 방법을 보여 줍니다.

[!code-csharp[cscsrefQueryKeywords#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/From.cs#3)]

여러 `from` 절을 사용하는 조인 작업에 대한 자세한 내용은 [왼쪽 우선 외부 조인 수행](../../linq/perform-left-outer-joins.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [쿼리 키워드(LINQ)](query-keywords.md)  
- [LINQ(Language-Integrated Query)](../../linq/index.md)  
