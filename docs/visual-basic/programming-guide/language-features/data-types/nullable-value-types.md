---
title: Nullable 값 형식-Visual Basic
ms.date: 07/20/2015
f1_keywords:
- vb.Nullable
helpviewer_keywords:
- nullable types [Visual Basic]
- '? [Visual Basic]'
- types [Visual Basic], nullable
- nullable types [Visual Basic]
- data types [Visual Basic], nullable
ms.assetid: 9ac3b602-6f96-4e6d-96f7-cd4e81c468a6
ms.openlocfilehash: 072496a560775a8f79274f1d44dd389d6ed5b40d
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71351769"
---
# <a name="nullable-value-types-visual-basic"></a>Nullable 값 형식(Visual Basic)

특정 상황에서 정의 된 값이 없는 값 형식을 사용 하는 경우가 있습니다. 예를 들어 데이터베이스의 필드는 할당 된 값이 있는 것을 의미 하는 값이 할당 되는 것을 구분 해야 할 수 있습니다. 값 형식은 일반 값 이나 null 값을 사용 하도록 확장할 수 있습니다. 이러한 확장을 *nullable 형식*이라고 합니다.

각 nullable 형식은 제네릭 <xref:System.Nullable%601> 구조체로 생성 됩니다. 작업 관련 작업을 추적 하는 데이터베이스를 고려 합니다. 다음 예제에서는 nullable `Boolean` 형식을 생성 하 고 해당 형식의 변수를 선언 합니다. 다음 세 가지 방법으로 선언을 작성할 수 있습니다.

[!code-vb[VbVbalrNullableValue#1](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#1)]

변수 `True`은 @no__t 값, `False` 값 또는 값 없음을 저장할 수 있습니다. 초기 기본값은 값이 아닙니다 .이 경우이 사용자에 대 한 정보가 아직 획득 되지 않았음을 의미할 수 있습니다. 반면 `False`은 정보를 얻고 사용자가 버스를 사용 하 여 작업을 수행 하지 않았음을 의미할 수 있습니다.

Nullable 형식을 사용 하 여 변수 및 속성을 선언할 수 있으며 nullable 형식의 요소가 포함 된 배열을 선언할 수 있습니다. Nullable 형식을 매개 변수로 사용 하 여 프로시저를 선언 하 고 `Function` 프로시저에서 nullable 형식을 반환할 수 있습니다.

배열, `String` 또는 클래스와 같은 참조 형식에 nullable 형식을 생성할 수 없습니다. 내부 형식은 값 형식 이어야 합니다. 자세한 내용은 [Value Types and Reference Types](value-types-and-reference-types.md)을 참조하세요.

## <a name="using-a-nullable-type-variable"></a>Nullable 형식 변수 사용

Nullable 형식의 가장 중요 한 멤버는 <xref:System.Nullable%601.HasValue%2A> 및 <xref:System.Nullable%601.Value%2A> 속성입니다. Nullable 형식의 변수에 대해 <xref:System.Nullable%601.HasValue%2A>은 변수에 정의 된 값이 포함 되어 있는지 여부를 알려 줍니다. @No__t-0 `True` 인 경우에는 <xref:System.Nullable%601.Value%2A>의 값을 읽을 수 있습니다. @No__t-0 및 <xref:System.Nullable%601.Value%2A>은 `ReadOnly` 속성입니다.

### <a name="default-values"></a>기본값

Nullable 형식을 사용 하 여 변수를 선언 하는 경우 <xref:System.Nullable%601.HasValue%2A> 속성의 기본값은 `False`입니다. 즉, 기본적으로 변수에는 기본 값 형식의 기본 값 대신 정의 된 값이 없습니다. 다음 예에서는 `Integer` 형식의 기본값은 0 이더라도 변수 `numberOfChildren`은 처음에는 정의 된 값이 없습니다.

[!code-vb[VbVbalrNullableValue#2](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#2)]

Null 값은 정의 되지 않거나 알 수 없는 값을 나타내는 데 유용 합니다. @No__t-0이 `Integer`로 선언 된 경우 정보를 현재 사용할 수 없음을 나타낼 수 있는 값이 없습니다.

### <a name="storing-values"></a>값 저장

일반적으로 nullable 형식의 변수 또는 속성에 값을 저장 합니다. 다음 예제에서는 이전 예제에서 선언 된 `numberOfChildren` 변수에 값을 할당 합니다.

[!code-vb[VbVbalrNullableValue#3](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#3)]

Nullable 형식의 변수 또는 속성이 정의 된 값을 포함 하는 경우 해당 값이 할당 되지 않은 초기 상태로 되돌아갈 수 있습니다. 다음 예제와 같이 변수 또는 속성을 `Nothing`으로 설정 하 여이 작업을 수행 합니다.

[!code-vb[VbVbalrNullableValue#4](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#4)]

> [!NOTE]
> Nullable 형식의 변수에는 0 @no__t 할당할 수 있지만 등호를 사용 하 여 `Nothing`에 대해 테스트할 수는 없습니다. 등호 (`someVar = Nothing`)를 사용 하는 비교는 항상-1 @no__t로 계산 됩니다. @No__t-1에 대해 변수의 <xref:System.Nullable%601.HasValue%2A> 속성을 테스트 하거나 `Is` 또는 `IsNot` 연산자를 사용 하 여 테스트할 수 있습니다.

### <a name="retrieving-values"></a>값 검색

Nullable 형식의 변수 값을 검색 하려면 먼저 <xref:System.Nullable%601.HasValue%2A> 속성을 테스트 하 여 값이 있는지 확인 해야 합니다. @No__t-0이-1 @no__t 때 값을 읽으려고 하는 경우 Visual Basic <xref:System.InvalidOperationException> 예외를 throw 합니다. 다음 예에서는 이전 예제의 `numberOfChildren` 변수를 읽는 데 권장 되는 방법을 보여 줍니다.

[!code-vb[VbVbalrNullableValue#5](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#5)]

## <a name="comparing-nullable-types"></a>Nullable 형식 비교

부울 식에서 nullable `Boolean` 변수를 사용 하는 경우 결과는-1, `False` 또는 `Nothing` @no__t 수 있습니다. 다음은 `And` 및 `Or`에 대 한 참 테이블입니다. @No__t-0 및 `b2`에는 가능한 값이 세 개 있으므로 평가할 조합 수는 9 개입니다.

|b1|b2|b1 및 b2|b1 또는 b2|
|--------|--------|---------------|--------------|
|`Nothing`|`Nothing`|`Nothing`|`Nothing`|
|`Nothing`|`True`|`Nothing`|`True`|
|`Nothing`|`False`|`False`|`Nothing`|
|`True`|`Nothing`|`Nothing`|`True`|
|`True`|`True`|`True`|`True`|
|`True`|`False`|`False`|`True`|
|`False`|`Nothing`|`False`|`Nothing`|
|`False`|`True`|`False`|`True`|
|`False`|`False`|`False`|`False`|

부울 변수나 식의 값이-0 @no__t 경우에는-1 또는 `false`가 @no__t 않습니다. 다음 예제를 살펴보십시오.

[!code-vb[VbVbalrNullableValue#6](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#6)]

이 예제에서 `b1 And b2`은 `Nothing`로 계산 됩니다. 따라서 `Else` 절은 각 `If` 문에서 실행 되며 출력은 다음과 같습니다.

`Expression is not true`

`Expression is not false`

> [!NOTE]
> `AndAlso` 및 단락 계산을 사용 하는 `OrElse`은 첫 번째 피연산자가 `Nothing`로 계산 될 때 두 번째 피연산자를 계산 해야 합니다.

## <a name="propagation"></a>전파

산술 연산자, 비교 연산자 또는 형식 작업의 피연산자 중 하나 또는 둘 다가 null을 허용 하면 작업 결과도 nullable입니다. 두 피연산자의 값이 모두 0이 @no__t 아닌 값을 가지 면 nullable 형식이 아닌 것 처럼 피연산자의 기본 값에 대해 연산이 수행 됩니다. 다음 예에서는 변수 `compare1` 및 `sum1`을 암시적으로 형식화 합니다. 마우스 포인터를 올려 놓으면 컴파일러가 두 항목 모두에 대해 nullable 형식을 유추 하 게 됩니다.

[!code-vb[VbVbalrNullableValue#7](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#7)]

피연산자 중 하나 또는 둘 다의 값이-0 @no__t 이면 @no__t 결과는-1이 됩니다.

[!code-vb[VbVbalrNullableValue#8](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrNullableValue/VB/Class1.vb#8)]

## <a name="using-nullable-types-with-data"></a>데이터에 Nullable 형식 사용

데이터베이스는 nullable 형식을 사용 하는 가장 중요 한 위치 중 하나입니다. 일부 데이터베이스 개체는 현재 nullable 형식을 지원 하지만 디자이너에서 생성 한 테이블 어댑터는 지원 하지 않습니다. [Nullable 형식에 대 한 TableAdapter 지원을](/visualstudio/data-tools/fill-datasets-by-using-tableadapters#tableadapter-support-for-nullable-types)참조 하세요.

## <a name="see-also"></a>참조

- <xref:System.InvalidOperationException>
- <xref:System.Nullable%601.HasValue%2A>
- [데이터 형식](index.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [데이터 형식 문제 해결](troubleshooting-data-types.md)
- [TableAdapter를 사용하여 데이터 세트 채우기](/visualstudio/data-tools/fill-datasets-by-using-tableadapters)
- [If 연산자](../../../language-reference/operators/if-operator.md)
- [지역 형식 유추](../variables/local-type-inference.md)
- [Is 연산자](../../../language-reference/operators/is-operator.md)
- [IsNot 연산자](../../../language-reference/operators/isnot-operator.md)
- [Nullable 값 형식 (C#) 사용](../../../../csharp/programming-guide/nullable-types/using-nullable-types.md)
