---
title: 패턴 일치
description: 에서 F# 패턴을 사용 하 여 데이터를 논리적 구조와 비교 하거나 데이터를 구성 부분으로 분해 하거나 데이터에서 정보를 추출 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 0e14fa00103742bbf5f054f8c04a7669ed767e63
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216806"
---
# <a name="pattern-matching"></a>패턴 일치

패턴은 입력 데이터를 변환 하는 규칙입니다. 이는 데이터를 논리적 F# 구조와 비교 하거나 데이터를 구성 부분으로 분해 하거나 다양 한 방법으로 데이터에서 정보를 추출 하기 위해 언어 전체에서 사용 됩니다.

## <a name="remarks"></a>설명

패턴은 `match` 식과 같은 다양 한 언어 구문에서 사용 됩니다. 이러한 함수는 `let` 바인딩, 람다 식 및 `try...with` 식과 연결 된 예외 처리기의 함수에 대 한 인수를 처리할 때 사용 됩니다. 자세한 내용은 [일치 식](match-expressions.md), [let 바인딩](./functions/let-bindings.md), [람다 식을 참조 하세요. `fun` 키워드](./functions/lambda-expressions-the-fun-keyword.md)및 예외[: `try...with` 식](./exception-handling/the-try-with-expression.md)입니다.

예를 들어 `match` 식에서 *패턴* 은 파이프 기호 뒤에 오는 것입니다.

```fsharp
match expression with
| pattern [ when condition ] -> result-expression
...
```

각 패턴은 특정 방식으로 입력을 변환 하는 규칙 역할을 합니다. `match` 식에서 각 패턴을 검사 하 여 입력 데이터가 패턴과 호환 되는지 확인 합니다. 일치 하는 항목이 있으면 결과 식이 실행 됩니다. 일치 항목을 찾을 수 없는 경우 다음 패턴 규칙을 테스트 합니다. 선택적 when *조건* 부분은 [일치 식](match-expressions.md)에 설명 되어 있습니다.

다음 표에서는 지원 되는 패턴을 보여 줍니다. 런타임에 입력은 테이블에 나열 된 순서 대로 다음 각 패턴에 대해 테스트 되 고 패턴은 코드에 표시 되는 첫 번째부터 마지막으로, 각 줄의 패턴에 대해 왼쪽에서 오른쪽으로 적용 됩니다.

|name|설명|예제|
|----|-----------|-------|
|상수 패턴|모든 숫자, 문자 또는 문자열 리터럴, 열거형 상수 또는 정의 된 리터럴 식별자|`1.0`, `"test"`, `30`, `Color.Red`|
|식별자 패턴|구분 된 공용 구조체, 예외 레이블 또는 활성 패턴 사례의 case 값|`Some(x)`<br /><br />`Failure(msg)`|
|변수 패턴|*identifier*|`a`|
|`as`되풀이|*식별자* 로 서의 *패턴*|`(a, b) as tuple1`|
|OR 패턴|*pattern1* &#124; *pattern2*|<code>([h] &#124; [h; _])</code>|
|및 패턴|*pattern1* &amp; *pattern2*|`(a, b) & (_, "test")`|
|단점 패턴|*identifier* :: *list 식별자*|`h :: t`|
|목록 패턴|[ *pattern_1*; ... ; *pattern_n* ]|`[ a; b; c ]`|
|배열 패턴|[&#124; *pattern_1*; ... *pattern_n* &#124;]|<code>[&#124; a; b; c &#124;]</code>|
|괄호로 묶인 패턴|( *패턴* )|`( a )`|
|튜플 패턴|( *pattern_1*, ... , *pattern_n* )|`( a, b )`|
|레코드 패턴|{ *identifier1* = *pattern_1*; ...; *identifier_n*  =  *pattern_n* }|`{ Name = name; }`|
|와일드 카드 패턴|_|`_`|
|형식 주석과 함께 패턴|*패턴* : *형식*|`a : int`|
|형식 테스트 패턴|:? *유형* [as *식별자* ]|`:? System.DateTime as dt`|
|Null 패턴|null|`null`|

## <a name="constant-patterns"></a>상수 패턴

상수 패턴은 숫자, 문자 및 문자열 리터럴, 열거형 상수 (열거형 형식 이름 포함)입니다. 상수 패턴만 있는 식은 다른 언어의 case 문과 비교할 수 있습니다. `match` 입력을 리터럴 값과 비교 하 고 값이 같으면 패턴이 일치 합니다. 리터럴의 형식은 입력의 형식과 호환 되어야 합니다.

다음 예제에서는 리터럴 패턴을 사용 하는 방법을 보여 줍니다. 또한 변수 패턴과 또는 패턴을 사용 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4801.fs)]

리터럴 패턴의 또 다른 예로는 열거 상수를 기반으로 하는 패턴이 있습니다. 열거형 상수를 사용 하는 경우 열거형 형식 이름을 지정 해야 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4802.fs)]

## <a name="identifier-patterns"></a>식별자 패턴

패턴이 유효한 식별자를 구성 하는 문자열인 경우 식별자의 형식에 따라 패턴이 일치 하는 방법이 결정 됩니다. 식별자가 단일 문자 보다 길고 대문자로 시작 하는 경우 컴파일러는 식별자 패턴에 대해 일치를 수행 하려고 합니다. 이 패턴의 식별자는 리터럴 특성, 구분 된 공용 구조체 케이스, 예외 식별자 또는 활성 패턴 사례로 표시 된 값일 수 있습니다. 일치 하는 식별자를 찾을 수 없으면 일치가 실패 하 고 다음 패턴 규칙 인 변수 패턴은 입력과 비교 됩니다.

구분 된 공용 구조체 패턴은 단순한 명명 된 사례 이거나 값 또는 여러 값이 포함 된 튜플을 가질 수 있습니다. 값이 있는 경우 값에 대 한 식별자를 지정 해야 합니다. 튜플의 경우 하나 이상의 명명 된 공용 구조체 필드에 대 한 필드 이름이 포함 된 식별자 나 튜플의 각 요소에 대 한 식별자를 사용 하 여 튜플 패턴을 제공 해야 합니다. 예제는이 섹션의 코드 예제를 참조 하세요.

`option` 형식은 `Some` 및 의`None`두 가지 경우를 포함 하는 구별 된 공용 구조체입니다. 한 case (`Some`)에는 값이 있지만`None`다른 하나는 명명 된 case입니다. 따라서는 `Some` 사례와 연결 된 값에 대 한 변수를 포함 해야 하지만 `None` 자체로 표시 되어야 합니다. `Some` 다음 코드에서 변수에 `var1` 는 `Some` case와 일치 하 여 얻은 값이 제공 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4803.fs)]

다음 예제에서 `PersonName` 구별 된 공용 구조체에는 가능한 형식의 이름을 나타내는 문자열과 문자의 혼합이 포함 되어 있습니다. 구분 된 공용 구조체 `FirstOnly`의 사례는, `LastOnly`및 `FirstLast`입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4804.fs)]

명명 된 필드가 있는 구별 된 공용 구조체의 경우에는 등호 (=)를 사용 하 여 명명 된 필드의 값을 추출 합니다. 예를 들어 다음과 같은 선언으로 구분 된 공용 구조체를 생각해 보겠습니다.

```fsharp
type Shape =
    | Rectangle of height : float * width : float
    | Circle of radius : float
```

패턴 일치 식에서 다음과 같이 명명 된 필드를 사용할 수 있습니다.

```fsharp
let matchShape shape =
    match shape with
    | Rectangle(height = h) -> printfn "Rectangle with length %f" h
    | Circle(r) -> printfn "Circle with radius %f" r
```

명명 된 필드의 사용은 선택 사항 이므로 앞의 예제에서 및 `Circle(r)` `Circle(radius = r)` 는 모두 동일한 효과를 가집니다.

여러 필드를 지정 하는 경우 세미콜론 (;)을 사용 합니다. 구분 기호로.

```fsharp
match shape with
| Rectangle(height = h; width = w) -> printfn "Rectangle with height %f and width %f" h w
| _ -> ()
```

활성 패턴을 사용 하면 보다 복잡 한 사용자 지정 패턴 일치를 정의할 수 있습니다. 활성 패턴에 대 한 자세한 내용은 [활성 패턴](active-patterns.md)을 참조 하세요.

식별자가 예외인 경우 예외 처리기의 컨텍스트에서 패턴 일치에 사용 됩니다. 예외 처리 [의 패턴 일치에 대 한 자세한 내용은 예외: `try...with` 식](./exception-handling/the-try-with-expression.md)입니다.

## <a name="variable-patterns"></a>변수 패턴

변수 패턴은 변수 이름에 일치 하는 값을 할당 합니다. 그런 다음 `->` 기호 오른쪽의 실행 식에 사용할 수 있습니다. 변수 패턴 단독은 모든 입력과 일치 하지만 변수 패턴은 종종 다른 패턴 내에 표시 되므로 튜플 및 배열과 같은 보다 복잡 한 구조를 변수로 분해할 수 있습니다.

다음 예제에서는 튜플 패턴 내의 변수 패턴을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4805.fs)]

## <a name="as-pattern"></a>as 패턴

패턴은 `as` 절이 추가 된 패턴입니다. `as` 절 `as` 은 일치 하는 값을 `match` 식의 실행 식에 사용할 수 있는 이름에 바인딩합니다. 또는이 `let` 패턴을 바인딩에서 사용 하는 경우에는 이름이 로컬 범위에 바인딩으로 추가 됩니다.

다음 예제에서는 패턴을 `as` 사용 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4806.fs)]

## <a name="or-pattern"></a>OR 패턴

또는 패턴은 입력 데이터가 여러 패턴을 일치 시킬 수 있는 경우와 같은 코드를 결과로 실행 하려고 할 때 사용 됩니다. 또는 패턴 양쪽의 형식이 호환 되어야 합니다.

다음 예제에서는 또는 패턴을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4807.fs)]

## <a name="and-pattern"></a>및 패턴

및 패턴에서는 입력이 두 패턴에 일치 해야 합니다. 및 패턴의 양쪽 모두 형식이 호환 되어야 합니다.

다음 예제는이 항목 `detectZeroTuple` 의 뒷부분에 나오는 [튜플 패턴](https://msdn.microsoft.com/library/#tuple) 단원에 나와 있는 것과 유사 하지만 `var1` 및 `var2` 패턴을 사용 하 여 및 모두 값으로 가져옵니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4808.fs)]

## <a name="cons-pattern"></a>단점 패턴

단점 패턴은 목록을 첫 번째 요소, *헤드*및 나머지 요소 ( *tail*)가 포함 된 목록으로 분해 하는 데 사용 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4809.fs)]

## <a name="list-pattern"></a>목록 패턴

목록 패턴을 사용 하면 목록을 여러 요소로 분해할 수 있습니다. 목록 패턴 자체는 특정 수의 요소 목록만 일치 시킬 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4810.fs)]

## <a name="array-pattern"></a>배열 패턴

배열 패턴은 목록 패턴과 비슷하며 특정 길이의 배열을 분해 하는 데 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4811.fs)]

## <a name="parenthesized-pattern"></a>괄호로 묶인 패턴

괄호는 원하는 결합성을 얻기 위해 패턴을 기준으로 그룹화 할 수 있습니다. 다음 예제에서는 괄호를 사용 하 여 및 패턴과 단점 패턴 간의 연관성을 제어 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4812.fs)]

## <a name="tuple-pattern"></a>튜플 패턴

튜플 패턴은 튜플 형식의 입력과 일치 하며 튜플의 각 위치에 대해 패턴 일치 변수를 사용 하 여 튜플을 구성 요소로 분해할 수 있습니다.

다음 예제에서는 튜플 패턴을 보여 주고 리터럴 패턴, 변수 패턴 및 와일드 카드 패턴을 사용 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4813.fs)]

## <a name="record-pattern"></a>레코드 패턴

레코드 패턴은 레코드를 분해 하 여 필드 값을 추출 하는 데 사용 됩니다. 패턴은 레코드의 모든 필드를 참조할 필요가 없습니다. 생략 된 필드는 일치에 참여 하지 않으며 추출 되지 않습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4814.fs)]

## <a name="wildcard-pattern"></a>와일드 카드 패턴

와일드 카드 패턴은 밑줄 (`_`) 문자로 표시 되 고 변수 패턴과 마찬가지로 입력을 일치 시킵니다. 단, 입력은 변수에 할당 되는 것이 아니라 무시 됩니다. 와일드 카드 패턴은 `->` 기호 오른쪽의 식에 필요 하지 않은 값에 대 한 자리 표시자로 다른 패턴 내에서 자주 사용 됩니다. 또한 와일드 카드 패턴은 일치 하지 않는 입력을 일치 시키기 위해 패턴 목록의 끝에 자주 사용 됩니다. 와일드 카드 패턴은이 항목의 여러 코드 예제에서 보여 줍니다. 한 가지 예는 위의 코드를 참조 하세요.

## <a name="patterns-that-have-type-annotations"></a>형식 주석이 있는 패턴

패턴에 형식 주석을 사용할 수 있습니다. 다른 형식 주석과 같은 다른 형식 주석과 가이드 유추와 같은 방식으로 동작 합니다. 패턴의 형식 주석 앞뒤에는 괄호가 필요 합니다. 다음 코드에서는 형식 주석이 있는 패턴을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4815.fs)]

## <a name="type-test-pattern"></a>형식 테스트 패턴

형식 테스트 패턴은 입력을 형식에 대해 일치 시키는 데 사용 됩니다. 입력 형식이 패턴에 지정 된 형식 (또는 파생 형식)과 일치 하면 일치가 성공 합니다.

다음 예제에서는 형식 테스트 패턴을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4816.fs)]

## <a name="null-pattern"></a>Null 패턴

Null 패턴은 null 값을 허용 하는 형식으로 작업할 때 나타날 수 있는 null 값과 일치 합니다. Null 패턴은 .NET Framework 코드와 상호 작용할 때 자주 사용 됩니다. 예를 들어 .net API의 반환 값은 `match` 식에 대 한 입력이 될 수 있습니다. 반환 값이 null 인지 여부 및 반환 된 값의 다른 특성에 따라 프로그램 흐름을 제어할 수 있습니다. Null 패턴을 사용 하 여 null 값이 프로그램의 나머지 부분에 전파 되지 않도록 할 수 있습니다.

다음 예에서는 null 패턴과 변수 패턴을 사용 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4817.fs)]

## <a name="see-also"></a>참고 항목

- [일치 식](match-expressions.md)
- [활성 패턴](active-patterns.md)
- [F# 언어 참조](index.md)
