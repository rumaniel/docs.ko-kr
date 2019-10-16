---
title: group 절 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- group
- group_CSharpKeyword
helpviewer_keywords:
- group keyword [C#]
- group clause [C#]
ms.assetid: c817242e-b12c-4baa-a57e-73ee138f34d1
ms.openlocfilehash: 160b25bd93f7d7c69ec104a31a0608e930e2dee3
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54534893"
---
# <a name="group-clause-c-reference"></a>group 절(C# 참조)

`group` 절은 그룹의 키 값과 일치하는 0개 이상의 항목이 포함된 <xref:System.Linq.IGrouping%602> 개체 시퀀스를 반환합니다. 예를 들어 각 문자열의 첫 번째 문자에 따라 문자열 시퀀스를 그룹화할 수 있습니다. 이 경우 첫 번째 문자는 키로, [char](char.md) 형식이며 각 <xref:System.Linq.IGrouping%602> 개체의 `Key` 속성에 저장됩니다. 컴파일러는 키의 형식을 유추합니다.

다음 예제와 같이 쿼리 식을 `group` 절로 끝낼 수 있습니다.

[!code-csharp[cscsrefQueryKeywords#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#10)]

각 그룹에서 추가 쿼리 작업을 수행하려는 경우 [into](into.md) 상황별 키워드를 사용하여 임시 식별자를 지정할 수 있습니다. `into`를 사용하는 경우 쿼리를 계속 진행하고, 다음 예제와 같이 궁극적으로 `select` 문이나 다른 `group` 절로 끝내야 합니다.

[!code-csharp[cscsrefQueryKeywords#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#11)]

`into`를 포함 및 포함하지 않고 `group`을 사용하는 보다 자세한 예제는 이 문서의 예제 섹션에 제공됩니다.

## <a name="enumerating-the-results-of-a-group-query"></a>그룹 쿼리의 결과 열거

`group` 쿼리에 의해 생성된 <xref:System.Linq.IGrouping%602> 개체는 기본적으로 목록의 목록이기 때문에 중첩된 [foreach](foreach-in.md) 루프를 사용하여 각 그룹에 있는 항목에 액세스해야 합니다. 외부 루프는 그룹 키를 반복하고, 내부 루프는 그룹 자체에 있는 각 항목을 반복합니다. 그룹에 키가 있지만 요소는 없을 수도 있습니다. 다음은 앞의 코드 예제에서 쿼리를 실행하는 `foreach` 루프입니다.

[!code-csharp[cscsrefQueryKeywords#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#12)]

## <a name="key-types"></a>키 형식

그룹 키는 문자열, 기본 제공 숫자 형식, 사용자 정의 명명된 형식, 무명 형식 등 모든 형식일 수 있습니다.

### <a name="grouping-by-string"></a>문자열로 그룹화

앞의 코드 예제에서는 `char`를 사용했습니다. 대신, 문자열 키를 전체 성 등으로 쉽게 지정했을 수 있습니다.

[!code-csharp[cscsrefQueryKeywords#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#13)]

### <a name="grouping-by-bool"></a>부울로 그룹화

다음 예제에서는 키에 부울 값을 사용하여 결과를 두 그룹으로 나누는 방법을 보여 줍니다. 값은 `group` 절의 하위 식에서 생성됩니다.

[!code-csharp[cscsrefQueryKeywords#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#14)]

### <a name="grouping-by-numeric-range"></a>숫자 범위로 그룹화

다음 예제에서는 식을 사용하여 백분위수 범위를 나타내는 숫자 그룹 키를 만듭니다. 메서드 호출 결과를 저장할 편리한 위치로 [let](let-clause.md)을 사용하여 `group` 절에서 메서드를 두 번 호출할 필요가 없도록 합니다. 쿼리 식에 메서드를 안전하게 사용하는 방법에 대한 자세한 내용은 [방법: 쿼리 식의 예외 처리](../../programming-guide/linq-query-expressions/how-to-handle-exceptions-in-query-expressions.md)를 참조하세요.

[!code-csharp[cscsrefQueryKeywords#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#15)]

### <a name="grouping-by-composite-keys"></a>복합 키로 그룹화

둘 이상의 키에 따라 요소를 그룹화하려는 경우 복합 키를 사용합니다. 무명 형식이나 명명된 형식을 통해 키 요소를 저장하여 복합 키를 만듭니다. 다음 예제에서는 `Person` 클래스가 `surname` 및 `city`라는 멤버로 선언되었다고 가정합니다. `group` 절은 성과 도시가 동일한 각 개인 집합에 대해 별도 그룹이 생성되도록 합니다.

```csharp
group person by new {name = person.surname, city = person.city};
```

쿼리 변수를 다른 메서드에 전달해야 하는 경우 명명된 형식을 사용합니다. 키에 대해 자동 구현 속성을 사용하여 특수 클래스를 만든 다음 <xref:System.Object.Equals%2A> 및 <xref:System.Object.GetHashCode%2A> 메서드를 재정의합니다. 구조체를 사용할 수도 있으며, 이 경우 이러한 메서드를 엄격하게 재정의하지 않아도 됩니다. 자세한 내용은 [방법: 자동으로 구현된 속성을 사용하여 간단한 클래스 구현](../../programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md) 및 [방법: 디렉터리 트리의 중복 파일 쿼리](../../programming-guide/concepts/linq/how-to-query-for-duplicate-files-in-a-directory-tree-linq.md)를 참조하세요. 두 번째 문서에는 명명된 형식과 함께 복합 키를 사용하는 방법을 보여 주는 코드 예제가 있습니다.

## <a name="example"></a>예제

다음 예제에서는 추가 쿼리 논리가 그룹에 적용되지 않는 경우 소스 데이터를 그룹으로 정렬하기 위한 표준 패턴을 보여 줍니다. 이를 비연속 그룹화라고 합니다. 문자열 배열에 있는 요소는 첫 문자에 따라 그룹화됩니다. 쿼리 결과는 그룹에 각 항목을 포함하는 공용 `Key` 속성 형식 `char` 및 <xref:System.Collections.Generic.IEnumerable%601> 컬렉션을 포함하는 <xref:System.Linq.IGrouping%602> 형식입니다.

`group` 절의 결과는 시퀀스의 시퀀스입니다. 따라서 반환된 각 그룹 내의 개별 요소에 액세스하려면 다음 예제와 같이 그룹 키를 반복하는 루프 안에 중첩된 `foreach` 루프를 사용합니다.

[!code-csharp[cscsrefQueryKeywords#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#16)]

## <a name="example"></a>예제

이 예제에서는 `into`와 함께 *continuation*을 사용하여 그룹을 만든 후 그룹에서 추가 논리를 수행하는 방법을 보여 줍니다. 자세한 내용은 [into](into.md)를 참조하세요. 다음 예제에서는 각 그룹을 쿼리하여 키 값이 모음인 그룹만 선택합니다.

[!code-csharp[cscsrefQueryKeywords#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#17)]

## <a name="remarks"></a>주의

`group` 절은 컴파일 시간에 <xref:System.Linq.Enumerable.GroupBy%2A> 메서드 호출로 변환됩니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Linq.IGrouping%602>
- <xref:System.Linq.Enumerable.GroupBy%2A>
- <xref:System.Linq.Enumerable.ThenBy%2A>
- <xref:System.Linq.Enumerable.ThenByDescending%2A>
- [쿼리 키워드](query-keywords.md)
- [LINQ(Language-Integrated Query)](../../linq/index.md)
- [중첩 그룹 만들기](../../linq/create-a-nested-group.md)
- [쿼리 결과 그룹화](../../linq/group-query-results.md)
- [그룹화 작업에서 하위 쿼리 수행](../../linq/perform-a-subquery-on-a-grouping-operation.md)
