---
title: 쿼리 식 기본 사항(C#의 LINQ)
description: 쿼리 식과 관련된 개념 소개
ms.date: 11/30/2016
ms.assetid: 027db1f8-346f-44d2-a16e-043fcea3a4e0
ms.openlocfilehash: 96ef75fe702e60eaa38acef77a73a5ea7f2076f4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54709119"
---
# <a name="query-expression-basics"></a>쿼리 식 기본 사항

이 문서에서는 C#의 쿼리 식과 관련된 기본 개념을 소개합니다.

## <a name="what-is-a-query-and-what-does-it-do"></a>쿼리란 무엇이며 쿼리의 기능은 무엇인가요?

*쿼리*는 지정된 데이터 소스(또는 소스)에서 검색할 데이터 및 반환된 데이터에 필요한 모양과 구성을 설명하는 지침 집합입니다. 쿼리와 쿼리에서 생성되는 결과는 다릅니다.

일반적으로 소스 데이터는 논리적으로 같은 종류의 요소 시퀀스로서 구성됩니다. 예를 들어 SQL Database 테이블은 행 시퀀스를 포함합니다. XML 파일에는 XML 요소의 "시퀀스"가 있습니다(트리 구조에서는 계층적으로 구성되지만). 메모리 내 컬렉션은 개체의 시퀀스를 포함합니다.

애플리케이션의 관점에서 소스 데이터의 특정 형식과 구조는 중요하지 않습니다. 애플리케이션에는 소스 데이터가 항상 <xref:System.Collections.Generic.IEnumerable%601> 또는 <xref:System.Linq.IQueryable%601> 컬렉션으로 표시됩니다. 예를 들어 LINQ to XML에서 소스 데이터는 `IEnumerable`\<<xref:System.Xml.Linq.XElement>>로 표시됩니다.

이 소스 시퀀스에서 쿼리는 다음 세 가지 중 하나를 수행할 수 있습니다.

- 개별 요소를 수정하지 않고 요소의 하위 집합을 검색하여 새 시퀀스를 생성합니다. 그런 다음 쿼리는 다음 예제와 같이 여러 가지 방법으로 반환된 시퀀스를 정렬 또는 그룹화할 수 있습니다(`scores`를 `int[]`로 가정).

    [!code-csharp[csrefQueryExpBasics#45](~/samples/snippets/csharp/concepts/linq/query-expression-basics_1.cs)]

- 이전 예제와 같이 요소의 시퀀스를 검색하지만, 이를 새로운 개체 형식으로 변환합니다. 예를 들어 쿼리를 통해 데이터 소스에 있는 특정 고객 레코드에서 성만 검색할 수 있습니다. 또는 전체 레코드를 검색한 다음 이를 사용하여 최종 결과 시퀀스를 생성하기 전에 다른 메모리 내 개체 유형 또는 XML 데이터를 구성할 수 있습니다. 다음 예제는 `int`에서 `string`으로의 프로젝션을 보여 줍니다. `highScoresQuery`의 새 형식을 참조하세요.

    [!code-csharp[csrefQueryExpBasics#46](~/samples/snippets/csharp/concepts/linq/query-expression-basics_2.cs)]

- 소스 데이터에 대한 다음과 같은 singleton 값을 검색합니다.

  - 특정 조건과 일치하는 요소의 수.

  - 최대값 또는 최소값을 가지고 있는 요소.

  - 조건과 일치하는 첫 번째 요소 또는 지정된 요소 집합에서 특정 값의 합계. 예를 들어 다음 쿼리는 `scores` 정수 배열에서 80보다 큰 점수를 반환합니다.

    [!code-csharp[csrefQueryExpBasics#47](~/samples/snippets/csharp/concepts/linq/query-expression-basics_3.cs)]

    이전 예제에서는 `Count` 메서드를 호출하기 전에 쿼리 식 주변에 괄호를 사용했습니다. 구체적인 결과를 저장하기 위한 새 변수를 사용하여 식을 표현할 수도 있습니다. 이 기술은 결과를 저장하는 쿼리와 별도로 쿼리를 저장하는 변수를 유지하기 때문에 더 읽기 쉽습니다.

    [!code-csharp[csrefQueryExpBasics#48](~/samples/snippets/csharp/concepts/linq/query-expression-basics_4.cs)]

이전 예에서는 `highScoresQuery`에 의해 반환된 요소 수를 확인하려면 `Count`가 결과를 반복해야 하기 때문에 `Count`에 대한 호출에서 쿼리가 실행됩니다.

## <a name="what-is-a-query-expression"></a>쿼리 식이란 무엇입니까?

*쿼리 식*은 쿼리 구문으로 표현되는 쿼리입니다. 쿼리 식은 고급 언어 구문으로서, 다른 식과 같으며 C# 식이 유효한 모든 컨텍스트에서 사용할 수 있습니다. 쿼리 식은 SQL 또는 XQuery와 유사한 선언적 구문으로 작성된 절 집합으로 구성됩니다. 각 절에는 하나 이상의 C# 식이 포함되며, 이러한 식은 자체가 쿼리 식이거나 쿼리 식을 포함할 수 있습니다.

쿼리 식은 [from](../language-reference/keywords/from-clause.md) 절로 시작하고 [select](../language-reference/keywords/select-clause.md) 또는 [group](../language-reference/keywords/group-clause.md) 절로 끝나야 합니다. 첫 번째 `from` 절과 마지막 `select` 또는 `group` 절 사이에 선택적으로 [where](../language-reference/keywords/where-clause.md), [orderby](../language-reference/keywords/orderby-clause.md), [join](../language-reference/keywords/join-clause.md), [let](../language-reference/keywords/let-clause.md) 절과 심지어 추가 [from](../language-reference/keywords/from-clause.md) 절 중에서 하나 이상을 포함할 수 있습니다. 또한 [into](../language-reference/keywords/into.md) 키워드를 사용하여, `join` 또는 `group` 절의 결과를 동일한 쿼리 식의 추가 쿼리 절에 대한 소스로 사용할 수 있습니다.

### <a name="query-variable"></a>쿼리 변수

LINQ에서 쿼리 변수는 쿼리의 *결과* 대신 *쿼리*를 저장하는 변수입니다. 좀 더 구체적으로, 쿼리 변수는 항상 `foreach` 문이나 `IEnumerator.MoveNext` 메서드에 대한 직접 호출에서 반복될 때 요소 시퀀스를 생성하는 Enumerable 형식입니다.

다음 코드 예제는 하나의 데이터 소스, 하나의 필터링 절, 하나의 순서 지정 절, 변환 없는 원본 요소로 간단한 쿼리 식을 보여 줍니다. `select` 절은 쿼리를 종료합니다.

[!code-csharp[csrefQueryExpBasics#49](~/samples/snippets/csharp/concepts/linq/query-expression-basics_5.cs)]

이전 예제에서 `scoreQuery`는 *쿼리 변수*이며, 간단히 *쿼리*라고 하는 경우도 있습니다. 쿼리 변수는 `foreach` 루프에서 생성되는 실제 결과 데이터를 저장하지 않습니다. 그리고 `foreach` 문이 실행될 때, 쿼리 변수 `scoreQuery`를 통해 쿼리 결과가 반환되지 않습니다. 오히려 반복 변수 `testScore`를 통해 반환됩니다. `scoreQuery` 변수는 두 번째 `foreach` 루프에서 반복될 수 있습니다. 변수 또는 데이터 소스를 수정하지 않는 한 동일한 결과가 생성됩니다.

쿼리 변수는 쿼리 구문이나 메서드 구문 또는 이 두 가지 조합으로 표현된 쿼리를 저장할 수 있습니다. 다음 예제에서는 `queryMajorCities` 및 `queryMajorCities2` 모두 쿼리 변수입니다.

[!code-csharp[csrefQueryExpBasics#50](~/samples/snippets/csharp/concepts/linq/query-expression-basics_6.cs)]

반면에 다음 두 예제는 각각의 변수가 쿼리로 초기화되더라도 쿼리 변수가 아닌 변수를 보여 줍니다. 이들은 결과를 저장하기 때문에 쿼리 변수가 아닙니다.

[!code-csharp[csrefQueryExpBasics#51](~/samples/snippets/csharp/concepts/linq/query-expression-basics_7.cs)]

쿼리를 표현하는 다양한 방법에 대한 자세한 내용은 [LINQ의 쿼리 구문 및 메서드 구문](../programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)을 참조하세요.

#### <a name="explicit-and-implicit-typing-of-query-variables"></a>쿼리 변수의 명시적 형식 및 암시적 형식

이 문서는 일반적으로 쿼리 변수와 [select 절](../language-reference/keywords/select-clause.md) 간의 형식 관계를 표시하기 위해 쿼리 변수의 명시적 형식을 제공합니다. 그러나 [var](../language-reference/keywords/var.md) 키워드를 사용하여 컴파일 시간에 쿼리 변수(또는 다른 지역 변수)의 형식을 추론하도록 컴파일러에 지시할 수도 있습니다. 예를 들어 이 항목의 앞에 나온 쿼리 예제를 암시적 형식을 사용하여 표현할 수도 있습니다.

[!code-csharp[csrefQueryExpBasics#52](~/samples/snippets/csharp/concepts/linq/query-expression-basics_8.cs)]

자세한 내용은 [암시적으로 형식화된 지역 변수](../programming-guide/classes-and-structs/implicitly-typed-local-variables.md) 및 [LINQ 쿼리 작업의 형식 관계](../programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)를 참조하세요.

### <a name="starting-a-query-expression"></a>쿼리 식 시작

쿼리 식은 `from` 절로 시작해야 합니다. 쿼리 식은 범위 변수와 함께 데이터 소스를 지정합니다. 범위 변수는 소스 시퀀스가 트래버스할 때 소스 시퀀스의 각 연속 요소를 나타냅니다. 범위 변수는 데이터 소스의 요소 형식을 기반으로 강력하게 형식이 지정됩니다. 다음 예제에서 `countries`는 `Country` 개체의 배열이므로 범위 변수의 형식도 `Country`로 지정됩니다. 범위 변수의 형식은 강력하게 지정되므로 사용 가능한 형식 멤버에 액세스하기 위해 점 연산자를 사용할 수 있습니다.

[!code-csharp[csrefQueryExpBasics#53](~/samples/snippets/csharp/concepts/linq/query-expression-basics_9.cs)]

쿼리가 세미콜론 또는 *continuation* 절로 종료될 때까지 범위 변수는 범위 내에 있습니다.

쿼리 식에는 여러 `from` 절이 포함될 수 있습니다. 소스 시퀀스의 각 요소가 컬렉션이거나 컬렉션을 포함하는 경우 `from` 절을 추가로 사용합니다. 예를 들어 `Country` 개체의 컬렉션이 있으며, 각각에 `Cities`라는 이름의 `City` 개체 컬렉션이 포함되어 있다고 가정해 보겠습니다. 각 `Country`에서 `City` 개체를 쿼리하려면 다음과 같이 두 개의 `from` 절을 사용합니다.

[!code-csharp[csrefQueryExpBasics#54](~/samples/snippets/csharp/concepts/linq/query-expression-basics_10.cs)]

자세한 내용은 [from 절](../language-reference/keywords/from-clause.md)을 참조하세요.

### <a name="ending-a-query-expression"></a>쿼리 식 종료

쿼리 식은 `group` 절 또는 `select` 절로 끝나야 합니다.

#### <a name="group-clause"></a>group 절

지정한 키로 구성되는 그룹의 시퀀스를 생성하려면 `group` 절을 사용합니다. 키의 데이터 형식은 무엇이든 가능합니다. 예를 들어 다음 쿼리는 하나 이상의 `Country` 개체를 포함하며 키가 `char` 값인 그룹의 시퀀스를 만듭니다.

[!code-csharp[csrefQueryExpBasics#55](~/samples/snippets/csharp/concepts/linq/query-expression-basics_11.cs)]

그룹화에 대한 자세한 내용은 [group 절](../language-reference/keywords/group-clause.md)을 참조하세요.

#### <a name="select-clause"></a>select 절

다른 모든 시퀀스 형식을 생성하려면 `select` 절을 사용합니다. 간단한 `select` 절은 데이터 소스에 포함된 개체와 동일한 개체 형식의 시퀀스를 생성합니다. 이 예제에서는 데이터 소스에 `Country` 개체가 포함됩니다. `orderby` 절은 단지 요소를 새로운 순서로 정렬하고, `select` 절은 다시 정렬된 `Country` 개체의 시퀀스를 생성합니다.

[!code-csharp[csrefQueryExpBasics#56](~/samples/snippets/csharp/concepts/linq/query-expression-basics_12.cs)]

소스 데이터를 새 형식의 시퀀스로 변환하려면 `select` 절을 사용할 수 있습니다. 이 변환을 *프로젝션*이라고도 합니다. 다음 예에서 `select` 절은 원래 요소에 필드의 하위 집합만 포함하는 일련의 무명 형식을 *프로젝션*합니다. 새 개체는 개체 이니셜라이저를 사용하여 초기화됩니다.

[!code-csharp[csrefQueryExpBasics#57](~/samples/snippets/csharp/concepts/linq/query-expression-basics_13.cs)]

소스 데이터를 변환하기 위해 `select` 절을 사용하는 모든 방법에 대한 자세한 내용은 [select 절](../language-reference/keywords/select-clause.md)을 참조하세요.

#### <a name="continuations-with-into"></a>"into"를 사용한 연속

`select` 또는 `group` 절에서 `into` 키워드를 사용하여 쿼리를 저장하는 임시 식별자를 만들 수 있습니다. 그룹화 또는 선택 작업 후에 쿼리에 대해 추가 쿼리 작업을 수행해야 하는 경우 이렇게 할 수 있습니다. 다음 예제에서 `countries`는 인구 1,000만 명 범위에 따라 그룹화됩니다. 이러한 그룹을 만든 후에는 추가 절이 일부 그룹을 필터링한 다음 오름차순으로 그룹을 정렬합니다. 추가 작업을 수행하려면 `countryGroup`으로 표현되는 연속이 필요합니다.

[!code-csharp[csrefQueryExpBasics#58](~/samples/snippets/csharp/concepts/linq/query-expression-basics_14.cs)]

자세한 내용은 [into](../language-reference/keywords/into.md)를 참조하세요.

### <a name="filtering-ordering-and-joining"></a>필터링, 정렬 및 조인

시작 절 `from`과 종료 절 `select` 또는 `group` 사이의 다른 모든 절(`where`, `join`, `orderby`, `from`, `let`)은 선택 사항입니다. 선택 사항인 절은 쿼리 본문에서 0번 또는 여러 번 사용할 수 있습니다.

#### <a name="where-clause"></a>where 절

하나 이상의 조건자 식을 기반으로 소스 데이터에서 요소를 필터링하려면 `where` 절을 사용합니다. 다음 예제의 `where` 절에는 조건자 하나와 조건 두 개가 있습니다.

[!code-csharp[csrefQueryExpBasics#59](~/samples/snippets/csharp/concepts/linq/query-expression-basics_15.cs)]

자세한 내용은 [where 절](../language-reference/keywords/where-clause.md)을 참조하세요.

#### <a name="orderby-clause"></a>orderby 절

결과를 오름차순 또는 내림차순으로 정렬하려면 `orderby` 절을 사용합니다. 2차 정렬 순서를 지정할 수도 있습니다. 다음 예제에서는 `Area` 속성을 사용하여 `country` 개체에 대해 1차 정렬을 수행합니다. 그런 다음 `Population` 속성을 사용하여 2차 정렬을 수행합니다.

[!code-csharp[csrefQueryExpBasics#60](~/samples/snippets/csharp/concepts/linq/query-expression-basics_16.cs)]

`ascending` 키워드는 선택 사항이며, 순서가 지정되지 않은 경우 기본 정렬 순서입니다. 자세한 내용은 [orderby 절](../language-reference/keywords/orderby-clause.md)을 참조하세요.

#### <a name="join-clause"></a>join 절

각 요소의 지정된 키 간 동일성 비교에 따라 하나의 데이터 소스의 요소를 다른 데이터 소스의 요소와 연결하거나 결합하려면 `join` 절을 사용합니다. LINQ에서는 요소의 형식이 서로 다른 개체의 시퀀스에 대해 조인 작업이 수행됩니다. 두 개의 시퀀스를 조인한 후 `select` 또는 `group` 문을 사용하여 출력 시퀀스에 저장할 요소를 지정해야 합니다. 연결된 각 요소 집합의 속성을 출력 시퀀스의 새 형식으로 결합하는 데에도 무명 형식을 사용할 수 있습니다. 다음 예제는 `Category` 속성이 `categories` 문자열 배열의 범주 중 하나와 일치하는 `prod` 개체를 연결합니다. `Category`가 `categories`의 문자열과 일치하지 않는 제품은 필터링됩니다. `select` 문은 속성을 `cat` 및 `prod`에서 가져오는 새 형식을 프로젝션합니다.

[!code-csharp[csrefQueryExpBasics#61](~/samples/snippets/csharp/concepts/linq/query-expression-basics_17.cs)]

[into](../language-reference/keywords/into.md) 키워드를 사용하여 `join` 작업의 결과를 임시 변수에 저장함으로써 그룹 조인을 수행할 수 있습니다. 자세한 내용은 [join 절](../language-reference/keywords/join-clause.md)을 참조하세요.

#### <a name="let-clause"></a>let 절 

식의 결과(예: 메서드 호출)를 새 범위 변수에 저장하려면 `let` 절을 사용합니다. 다음 예제에서 범위 변수 `firstName`은 `Split`에서 반환하는 문자열 배열의 첫 번째 요소를 저장합니다.

[!code-csharp[csrefQueryExpBasics#62](~/samples/snippets/csharp/concepts/linq/query-expression-basics_18.cs)]

자세한 내용은 [let 절](../language-reference/keywords/let-clause.md)을 참조하세요.

### <a name="subqueries-in-a-query-expression"></a>쿼리 식의 하위 쿼리

쿼리 절 자체에 쿼리 식을 포함할 수 있는데, 이를 *하위 쿼리*라고도 합니다. 각 하위 쿼리는 자체 `from` 절로 시작되는데, 이것이 반드시 첫 번째 `from` 절에 있는 동일한 데이터 소스를 가리킬 필요는 없습니다. 예를 들어 다음 쿼리는 그룹화 작업의 결과를 검색하기 위해 select 문에서 사용되는 쿼리 식을 보여 줍니다.

[!code-csharp[csrefQueryExpBasics#63](~/samples/snippets/csharp/concepts/linq/query-expression-basics_19.cs)]

자세한 내용은 [방법: 그룹화 작업에서 하위 쿼리 수행](perform-a-subquery-on-a-grouping-operation.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../programming-guide/index.md)
- [LINQ(Language-Integrated Query)](index.md)
- [쿼리 키워드(LINQ)](../language-reference/keywords/query-keywords.md)
- [표준 쿼리 연산자 개요](../programming-guide/concepts/linq/standard-query-operators-overview.md)
