---
title: 연산자 오버로드
description: 클래스 또는 레코드 형식과의 F#전역 수준에서 산술 연산자를 오버 로드 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: d902a06193481ed87131b3336cd8a2ff54b811b4
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216839"
---
# <a name="operator-overloading"></a>연산자 오버로드

이 항목에서는 클래스 또는 레코드 형식과 전역 수준에서 산술 연산자를 오버 로드 하는 방법에 대해 설명 합니다.

## <a name="syntax"></a>구문

```fsharp
// Overloading an operator as a class or record member.
static member (operator-symbols) (parameter-list) =
    method-body
// Overloading an operator at the global level
let [inline] (operator-symbols) parameter-list = function-body
```

## <a name="remarks"></a>설명

위의 구문에서 *연산자-기호* 는 `+` `-` `*` `/`,,,, 등중하나입니다.`=` *매개 변수 목록* 은 해당 연산자에 대 한 일반적인 구문에서 피연산자를 표시 하는 순서 대로 지정 합니다. *메서드 본문* 은 결과 값을 생성 합니다.

연산자의 연산자 오버 로드는 정적 이어야 합니다. `+` `~`및 와`-`같은 단항 연산자에 대 한 연산자 오버 로드는 다음과 같이 연산자가 이항 연산자가 아니라 단항 연산자 임을 나타내기 위해 *연산자-기호* 에 물결표 ()를 사용 해야 합니다. 선언한.

```fsharp
static member (~-) (v : Vector)
```

다음 코드에서는 연산자가 두 개뿐인 벡터 클래스를 보여 줍니다. 그 중 하나는 단항 빼기 연산자이고 다른 하나는 스칼라 값을 곱하기 위한 연산자입니다. 이 예제에서는 벡터와 스칼라가 표시 되는 순서에 관계 없이 연산자가 작동 해야 하므로 스칼라 곱셈에 대 한 두 개의 오버 로드가 필요 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4001.fs)]

## <a name="creating-new-operators"></a>새 운영자 만들기

모든 표준 연산자를 오버 로드할 수 있지만 특정 문자의 시퀀스에서 새 연산자를 만들 수도 있습니다. 허용 되는 연산자 `!`문자 `%`는 `&`, `*` `+` ,`-`,, ,,`.`,,,,,입니다. `/` `<` `=` `>` `?`,,, 및`~`가 있습니다. `@` `^` `|` 문자 `~` 는 연산자 단항을 만드는 특별 한 의미를 가지 며 연산자 문자 시퀀스의 일부가 아닙니다. 모든 연산자를 단항로 설정할 수 있는 것은 아닙니다.

사용 하는 정확한 문자 시퀀스에 따라 연산자는 특정 우선 순위와 결합성을 갖습니다. 결합성은 왼쪽에서 오른쪽 또는 오른쪽에서 왼쪽으로 지정할 수 있으며, 동일한 수준의 우선 순위의 연산자가 괄호 없이 순서 대로 나타날 때마다 사용 됩니다.

연산자 문자 `.` 는 우선 순위에 영향을 주지 않으므로 예를 들어 일반 곱하기와 우선 순위와 결합성이 같은 고유한 곱셈 버전을 정의 하려는 경우와 같은연산자를만들수있습니다 `.*`.

연산자 `?` 와 `?<-` 만 시작할`?`수 있습니다.

에서 F# 모든 연산자의 우선 순위를 보여 주는 테이블은 [기호 및 연산자 참조](./symbol-and-operator-reference/index.md)에서 찾을 수 있습니다.

## <a name="overloaded-operator-names"></a>오버 로드 된 연산자 이름

F# 컴파일러가 연산자 식을 컴파일하는 경우 해당 연산자에 대해 컴파일러에서 생성 된 이름이 있는 메서드를 생성 합니다. 메서드의 MSIL (Microsoft 중간 언어)에 표시 되는 이름이 며 리플렉션 및 IntelliSense 에서도이 이름이 표시 됩니다. 일반적으로는 이러한 이름을 코드에서 F# 사용할 필요가 없습니다.

다음 표에서는 표준 연산자와 해당 하는 생성 된 이름을 보여 줍니다.

|연산자|생성 된 이름|
|--------|--------------|
|`[]`|`op_Nil`|
|`::`|`op_Cons`|
|`+`|`op_Addition`|
|`-`|`op_Subtraction`|
|`*`|`op_Multiply`|
|`/`|`op_Division`|
|`@`|`op_Append`|
|`^`|`op_Concatenate`|
|`%`|`op_Modulus`|
|`&&&`|`op_BitwiseAnd`|
|<code>&#124;&#124;&#124;</code>|`op_BitwiseOr`|
|`^^^`|`op_ExclusiveOr`|
|`<<<`|`op_LeftShift`|
|`~~~`|`op_LogicalNot`|
|`>>>`|`op_RightShift`|
|`~+`|`op_UnaryPlus`|
|`~-`|`op_UnaryNegation`|
|`=`|`op_Equality`|
|`<=`|`op_LessThanOrEqual`|
|`>=`|`op_GreaterThanOrEqual`|
|`<`|`op_LessThan`|
|`>`|`op_GreaterThan`|
|`?`|`op_Dynamic`|
|`?<-`|`op_DynamicAssignment`|
|<code>&#124;></code>|`op_PipeRight`|
|<code><&#124;</code>|`op_PipeLeft`|
|`!`|`op_Dereference`|
|`>>`|`op_ComposeRight`|
|`<<`|`op_ComposeLeft`|
|`<@ @>`|`op_Quotation`|
|`<@@ @@>`|`op_QuotationUntyped`|
|`+=`|`op_AdditionAssignment`|
|`-=`|`op_SubtractionAssignment`|
|`*=`|`op_MultiplyAssignment`|
|`/=`|`op_DivisionAssignment`|
|`..`|`op_Range`|
|`.. ..`|`op_RangeStep`|

여기에 나열 되지 않은 연산자 문자의 다른 조합은 연산자로 사용할 수 있으며 다음 표의 개별 문자에 대 한 이름을 연결 하 여 구성 된 이름을 갖습니다. 예: +! 가 `op_PlusBang`됩니다.

|연산자 문자|name|
|------------------|----|
|`>`|`Greater`|
|`<`|`Less`|
|`+`|`Plus`|
|`-`|`Minus`|
|`*`|`Multiply`|
|`/`|`Divide`|
|`=`|`Equals`|
|`~`|`Twiddle`|
|`%`|`Percent`|
|`.`|`Dot`|
|`&`|`Amp`|
|<code>&#124;</code>|`Bar`|
|`@`|`At`|
|`^`|`Hat`|
|`!`|`Bang`|
|`?`|`Qmark`|
|`(`|`LParen`|
|`,`|`Comma`|
|`)`|`RParen`|
|`[`|`LBrack`|
|`]`|`RBrack`|

## <a name="prefix-and-infix-operators"></a>전위 및 중 위 연산자

*전위* 연산자는 함수와 매우 유사 하 게 피연산자 또는 피연산자 앞에 배치 되어야 합니다. 중 *위* 연산자는 두 피연산자 사이에 배치 될 것으로 예상 됩니다.

특정 연산자만 전위 연산자로 사용할 수 있습니다. 일부 연산자는 항상 전위 연산자이 고, 다른 연산자는 중 위 또는 접두사가 될 수 있으며 나머지 연산자는 항상 중 위 연산자입니다. `!`를 제외한 `!=`로 시작하는 연산자와 `~` 연산자 또는 `~` 연산자의 반복적인 시퀀스는 항상 전위 연산자입니다. `+`연산자 ,`&`,, ,,`%`, 및`%%` 는 전위 연산자 또는 중 위 연산자 일 수 있습니다. `-.` `-` `+.` `&&` 접두사 연산자가 정의 될 때 접두사 연산자의 시작 부분에를 `~` 추가 하 여 이러한 연산자의 전위 버전을 중 위 버전과 구분 합니다. 연산자 `~` 를 사용 하는 경우 (정의 된 경우에만)는 사용 되지 않습니다.

## <a name="example"></a>예제

다음 코드에서는 연산자 오버 로드를 사용 하 여 분수 형식을 구현 하는 방법을 보여 줍니다. 분수는 분자와 분모로 표시 됩니다. 함수 `hcf` 는 분수를 줄이는 데 사용 되는 가장 높은 공통 요소를 결정 하는 데 사용 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4002.fs)]

**출력:**

```console
3/4 + 1/2 = 5/4
3/4 - 1/2 = 1/4
3/4 * 1/2 = 3/8
3/4 / 1/2 = 3/2
3/4 + 1 = 7/4
```

## <a name="operators-at-the-global-level"></a>전역 수준의 연산자

전역 수준에서 연산자를 정의할 수도 있습니다. 다음 코드에서는 연산자 `+?`를 정의 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4003.fs)]

위의 코드 `12`의 출력은입니다.

새로 정의 된 연산자에 대 한 F# 범위 지정 규칙이 기본 제공 연산자 보다 우선적으로 적용 되기 때문에 이러한 방식으로 정규 산술 연산자를 다시 정의할 수 있습니다.

키워드 `inline` 는 일반적으로 호출 코드에 가장 잘 통합 된 작은 함수인 전역 연산자와 함께 사용 됩니다. 또한 연산자 함수를 인라인으로 만들면 정적으로 확인 된 형식 매개 변수와 함께 작동 하 여 정적으로 확인 된 제네릭 코드를 생성할 수 있습니다. 자세한 내용은 [인라인 함수](./functions/inline-functions.md) 및 [정적으로 확인 된 형식 매개 변수](./generics/statically-resolved-type-parameters.md)를 참조 하세요.

## <a name="see-also"></a>참고 항목

- [멤버](./members/index.md)
