---
title: 함수
description: 의 함수 및에서 F# 일반적인 함수형 F# 프로그래밍 구문을 지 원하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 6f65ce692169b71abe8d2eff7ef07b66975d478b
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630708"
---
# <a name="functions"></a>함수

함수는 모든 프로그래밍 언어에서 프로그램 실행의 기본 단위입니다. 다른 언어와 마찬가지로 F# 함수는 이름을 가지며, 매개 변수 및 인수를 사용할 수 있고, 본문을 포함합니다. 또한 F#은 함수를 값으로 처리, 식에 명명되지 않은 함수 사용, 함수를 합성하여 새로운 함수 생성, 커리된 함수, 함수 인수를 부분적으로 적용하는 방식의 암시적 함수 정의 등 함수형 프로그래밍 구문도 지원합니다.

`let` 키워드 또는 `let rec` 키워드 조합(함수가 재귀적인 경우)을 사용하여 함수를 정의합니다.

## <a name="syntax"></a>구문

```fsharp
// Non-recursive function definition.
let [inline] function-name parameter-list [ : return-type ] = function-body
// Recursive function definition.
let rec function-name parameter-list = recursive-function-body
```

## <a name="remarks"></a>설명

*function-name*은 함수를 나타내는 식별자입니다. *parameter-list*는 공백으로 구분되는 연속 매개 변수로 구성됩니다. 매개 변수 섹션에 설명된 대로 각 매개 변수에 대해 명시적 형식을 지정할 수 있습니다. 특정 인수 형식을 지정하지 않으면 컴파일러가 함수 본문에서 형식을 유추하려고 합니다. *함수 본문*은 식으로 구성됩니다. 함수 본문을 구성하는 식은 일반적으로 여러 식으로 구성된 복합 식이며, 복합 식은 반환 값이 되는 최종 식으로 수렴됩니다. *반환 형식*은 그 뒤에 콜론이 나오며 선택 사항입니다. 반환 값의 형식을 명시적으로 지정하지 않으면 컴파일러가 최종 식에서 반환 형식을 결정합니다.

간단한 함수 정의는 다음과 같습니다.

```fsharp
let f x = x + 1
```

앞의 예제에서 함수 이름은 `f`이고, 인수는 `x`이고 그 형식은 `int`이며, 함수 본문은 `x + 1`이고, 반환 값의 형식은 `int`입니다.

함수를 `inline`으로 표시할 수 있습니다. `inline`에 대한 내용은 [인라인 함수](../functions/inline-functions.md)를 참조하세요.

## <a name="scope"></a>범위

모듈 범위 이외의 모든 범위 수준에서 값 또는 함수 이름을 다시 사용할 수 있습니다. 이름을 다시 사용하는 경우 나중에 선언된 이름이 이전에 선언된 이름을 섀도 처리합니다. 그러나 모듈의 최상위 수준 범위에서는 이름이 고유해야 합니다. 예를 들어 다음 코드가 모듈 범위에 표시되는 경우에는 오류가 발생하지만 함수 내에 표시되는 경우에는 오류가 발생하지 않습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet101.fs)]

하지만 다음 코드는 범위의 모든 수준에서 허용됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet102.fs)]

### <a name="parameters"></a>매개 변수

매개 변수 이름은 함수 이름 뒤에 나열됩니다. 다음 예제와 같이 매개 변수의 형식을 지정할 수 있습니다.

```fsharp
let f (x : int) = x + 1
```

형식을 지정하는 경우 매개 변수의 이름 다음에 나오며 콜론으로 이름과 구분됩니다. 매개 변수의 형식을 생략하면 컴파일러에서 매개 변수 형식을 유추합니다. 예를 들어 다음 함수 정의에서 1이 `int` 형식이므로`x` 인수는 `int` 형식으로 유추됩니다.

```fsharp
let f x = x + 1
```

그러나 컴파일러는 함수를 가능한 한 일반적인 형식으로 설정하려고 합니다. 예를 들어 다음 코드를 살펴보겠습니다.

```fsharp
let f x = (x, x)
```

이 함수는 임의 형식의 한 가지 인수에서 튜플을 생성합니다. 형식이 지정되어 있지 않으므로 함수를 임의의 인수 형식과 함께 사용할 수 있습니다. 자세한 내용은 [자동 일반화](../generics/automatic-generalization.md)를 참조하세요.

## <a name="function-bodies"></a>함수 본문

함수 본문에는 로컬 변수 및 함수에 대한 정의를 포함할 수 있습니다. 이러한 변수 및 함수는 현재 함수 본문 외부가 아닌 본문 내부에 있습니다. 간단한 구문 옵션을 사용하는 경우 다음 예제와 같이 들여쓰기를 사용하여 정의가 함수 본문 내에 있음을 나타내야 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet103.fs)]

자세한 내용은 [코드 서식 지정 지침](../code-formatting-guidelines.md) 및 [자세한 구문](../verbose-syntax.md)을 참조하세요.

## <a name="return-values"></a>반환 값

컴파일러는 함수 본문의 최종 식을 사용하여 반환 값과 형식을 결정합니다. 컴파일러는 이전 식에서 최종 식의 형식을 유추할 수 있습니다. `cylinderVolume` 함수에서, 이전 섹션과 같이 `pi`의 형식이 `3.14159` 리터럴 형식에서 `float`으로 결정됩니다. 컴파일러는 `pi`의 형식을 사용하여 `h * pi * r * r` 식의 형식을 `float`으로 결정합니다. 따라서 함수의 전체 반환 형식은 `float`입니다.

반환 값을 명시적으로 지정하려면 다음과 같이 코드를 작성합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet105.fs)]

코드가 위와 같이 작성되면 컴파일러에서 전체 함수에 **float**을 적용합니다. 매개 변수 형식에도 이를 적용하려는 경우 다음 코드를 사용합니다.

```fsharp
let cylinderVolume (radius : float) (length : float) : float
```

## <a name="calling-a-function"></a>함수 호출

함수 이름 뒤에 공백을 지정한 후 공백으로 구분된 인수를 지정하여 함수를 호출합니다. 예를 들어, **cylinderVolume** 함수를 호출하여 **vol** 값에 결과를 할당하려면 다음 코드를 작성합니다.

```fsharp
let vol = cylinderVolume 2.0 3.0
```

## <a name="partial-application-of-arguments"></a>인수의 부분 적용

지정된 수보다 적은 인수를 지정하는 경우 나머지 인수를 요구하는 새 함수를 만듭니다. 인수를 처리하는 이 메서드를 *커링*(currying)이라고 하며 F#과 같은 함수형 프로그래밍 언어의 특성입니다. 예를 들어, 두 가지 크기의 파이프(**2.0**의 반지름 및 **3.0**의 반지름)에 대해 작업하고 있다고 가정합니다. 다음과 같이 파이프의 볼륨을 결정하는 함수를 만들 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet106.fs)]

다양한 길이의 두 가지 크기 파이프에 필요한 추가 인수를 제공합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet107.fs)]

## <a name="recursive-functions"></a>재귀 함수

*재귀 함수*는 자신을 호출하는 함수입니다. 이러한 함수에는 **rec** 키워드 다음에 **let** 키워드를 지정해야 합니다. 임의의 함수를 호출하는 경우와 마찬가지로 함수 본문 내에서 재귀 함수를 호출합니다. 다음 재귀 함수는 *n*<sup>번째</sup> 피보나치 수를 계산 합니다. 피보나치 수열은 아주 오래 전부터 알려져 왔으며, 연속되는 각 숫자는 수열에서 이전 두 숫자의 합이 되는 수열입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet108.fs)]

주의를 기울이고 누적기 및 연속의 사용과 같은 특별 기법을 인식하여 재귀 함수를 작성하지 않으면 일부 재귀 함수는 프로그램 스택을 오버플로하거나 비효율적으로 작동할 수 있습니다.

## <a name="function-values"></a>함수 값

F#에서 모든 함수는 값으로 간주됩니다. 사실 이들을 *함수 값*이라고 합니다. 함수가 값이기 때문에 이러한 함수를 값이 사용되는 다른 컨텍스트에서 또는 다른 함수의 인수로 사용할 수 있습니다. 다음은 함수 값을 인수로 사용하는 함수의 예입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet109.fs)]

`->` 토큰을 사용하여 함수 값의 형식을 지정합니다. 이 토큰의 왼쪽에는 인수의 형식이 있고 오른쪽에는 반환 값이 있습니다. 앞의 예제에서 `apply1`은 `transform` 함수를 인수로 사용합니다. 여기서 `transform`은 인수를 사용하고 다른 정수를 반환하는 함수입니다. 다음 코드에서는 `apply1`을 사용하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet110.fs)]

`result`의 값은 앞의 코드가 실행된 후 101이 됩니다.

다음 예와 같이 여러 인수는 연속적인 `->` 토큰으로 구분됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet111.fs)]

해당 결과는 200입니다.

## <a name="lambda-expressions"></a>람다 식

*람다 식*은 명명되지 않은 함수입니다. 이전 예제에서, 명명된 함수인 **increment** 및 **mul**을 정의하는 대신 다음과 같이 람다 식을 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet112.fs)]

`fun` 키워드를 사용하여 람다 식을 정의합니다. 람다 식은 함수 정의와 유사합니다. 단, `=` 토큰 대신 `->` 토큰이 함수 본문에서 인수 목록을 구분하는 데 사용됩니다. 일반 함수 정의에서와 같이, 인수 형식이 명시적으로 유추되거나 지정될 수 있으며 람다 식의 반환 형식은 본문의 마지막 식 형식에서 유추됩니다. 자세한 내용은 람다 식을 [참조 하세요. `fun` 키워드](../functions/lambda-expressions-the-fun-keyword.md)입니다.

## <a name="function-composition-and-pipelining"></a>함수 컴퍼지션 및 파이프라인

F#의 함수는 다른 함수에서 구성할 수 있습니다. 두 함수**function1** 및 **function2**의 컴퍼지션은 **function1**을 적용한 후 **function2**를 적용한다는 것을 나타냅니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet113.fs)]

결과는 202입니다.

파이프라인을 통해 함수 호출을 연속 작업으로 함께 연결할 수 있습니다. 파이프라인은 다음과 같이 작동합니다.

```fsharp
let result = 100 |> function1 |> function2
```

결과는 다시 202입니다.

컴퍼지션 연산자는 두 개의 함수를 사용하고 한 함수를 반환합니다. 반대로 파이프라인 연산자는 함수 및 인수를 사용하고 값을 반환합니다. 다음 코드 예제에서는 함수 시그니처 및 사용 방식의 차이를 나타내어 파이프라인 및 컴퍼지션 연산자 간의 차이를 보여 줍니다.

```fsharp
// Function composition and pipeline operators compared.

let addOne x = x + 1
let timesTwo x = 2 * x

// Composition operator
// ( >> ) : ('T1 -> 'T2) -> ('T2 -> 'T3) -> 'T1 -> 'T3
let Compose2 = addOne >> timesTwo

// Backward composition operator
// ( << ) : ('T2 -> 'T3) -> ('T1 -> 'T2) -> 'T1 -> 'T3
let Compose1 = addOne << timesTwo

// Result is 5
let result1 = Compose1 2

// Result is 6
let result2 = Compose2 2

// Pipelining
// Pipeline operator
// ( |> ) : 'T1 -> ('T1 -> 'U) -> 'U
let Pipeline2 x = addOne x |> timesTwo

// Backward pipeline operator
// ( <| ) : ('T -> 'U) -> 'T -> 'U
let Pipeline1 x = addOne <| timesTwo x

// Result is 5
let result3 = Pipeline1 2

// Result is 6
let result4 = Pipeline2 2
```

## <a name="overloading-functions"></a>함수 오버로드

특정 형식의 메서드는 오버로드할 수 있지만 함수를 오버로드할 수는 없습니다. 자세한 내용은 [메서드](../members/methods.md)를 참조하세요.

## <a name="see-also"></a>참고자료

- [값](../values/index.md)
- [F# 언어 참조](../index.md)
