---
title: 매개 변수 및 인수
description: 매개 변수 F# 를 정의 하 고 함수, 메서드 및 속성에 인수를 전달 하는 언어 지원에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: e8094ffbc55870b5de75acb740aa2736ec6590a5
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216830"
---
# <a name="parameters-and-arguments"></a>매개 변수 및 인수

이 항목에서는 매개 변수를 정의 하 고 함수, 메서드 및 속성에 인수를 전달 하는 언어 지원에 대해 설명 합니다. 여기에는 참조로 전달 하는 방법 및 다양 한 수의 인수를 사용할 수 있는 메서드를 정의 하 고 사용 하는 방법에 대 한 정보가 포함 되어 있습니다.

## <a name="parameters-and-arguments"></a>매개 변수 및 인수

Term *매개 변수* 는 제공 될 것으로 예상 되는 값의 이름을 설명 하는 데 사용 됩니다. Term *인수* 는 각 매개 변수에 제공 된 값에 사용 됩니다.

매개 변수는 튜플 또는 커리 된 형식으로 지정 하거나 둘 중 일부를 조합 하 여 지정할 수 있습니다. 명시적 매개 변수 이름을 사용 하 여 인수를 전달할 수 있습니다. 메서드의 매개 변수는 선택적으로 지정할 수 있으며 기본값을 지정할 수 있습니다.

## <a name="parameter-patterns"></a>매개 변수 패턴

함수 및 메서드에 제공 되는 매개 변수는 일반적으로 공백으로 구분 되는 패턴입니다. 즉, 원칙적으로 [일치 식](match-expressions.md) 에 설명 된 모든 패턴을 함수 또는 멤버에 대 한 매개 변수 목록에서 사용할 수 있습니다.

메서드는 일반적으로 인수를 전달 하는 튜플 형식을 사용 합니다. 이는 튜플 형식이 .NET 메서드에 인수가 전달 되는 방식과 일치 하므로 다른 .NET 언어의 관점에서 보다 명확한 결과를 얻을 수 있습니다.

커리 된 형식은 바인딩을 사용 하 `let` 여 만든 함수와 가장 자주 사용 됩니다.

다음 의사 코드에서는 튜플 및 커리 된 인수의 예를 보여 줍니다.

```fsharp
// Tuple form.
member this.SomeMethod(param1, param2) = ...
// Curried form.
let function1 param1 param2 = ...
```

일부 인수는 튜플에 있고 일부는 그렇지 않은 경우 결합 된 폼을 사용할 수 있습니다.

```fsharp
let function2 param1 (param2a, param2b) param3 = ...
```

다른 패턴은 매개 변수 목록에서 사용할 수도 있지만 매개 변수 패턴이 가능한 모든 입력과 일치 하지 않는 경우 런타임에 불완전 하 게 일치 하는 항목이 있을 수 있습니다. 이 예외 `MatchFailureException` 는 인수 값이 매개 변수 목록에 지정 된 패턴과 일치 하지 않는 경우에 생성 됩니다. 컴파일러는 매개 변수 패턴에서 불완전 한 일치 항목을 허용할 때 경고를 발생 시킵니다. 하나 이상의 다른 패턴은 일반적으로 매개 변수 목록에 유용 하며 와일드 카드 패턴입니다. 제공 된 인수를 무시 하려는 경우에는 매개 변수 목록에서 와일드 카드 패턴을 사용 합니다. 다음 코드에서는 인수 목록에서 와일드 카드 패턴을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3801.fs)]

와일드 카드 패턴은 다음 코드와 같이 일반적으로 문자열 배열로 제공 되는 명령줄 인수에 관심이 없는 경우에 전달 된 인수가 필요 하지 않을 때마다 유용할 수 있습니다 (예: 프로그램에 대 한 기본 진입점).

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3802.fs)]

인수에 사용 되는 다른 패턴은 `as` 패턴 및 구분 된 공용 구조체와 활성 패턴과 관련 된 식별자 패턴입니다. 다음과 같이 단일 대/소문자 구분 된 공용 구조체 패턴을 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3803.fs)]

출력은 다음과 같습니다.

```console
Data begins at 0 and ends at 4 in string Et tu, Brute?
Et tu
```

활성 패턴은 예를 들어 다음 예제와 같이 인수를 원하는 형식으로 변환 하는 경우 매개 변수로 유용할 수 있습니다.

```fsharp
type Point = { x : float; y : float }

let (| Polar |) { x = x; y = y} =
    ( sqrt (x*x + y*y), System.Math.Atan (y/ x) )

let radius (Polar(r, _)) = r
let angle (Polar(_, theta)) = theta
```

`as` 패턴을 사용 하 여 다음 코드 줄에 표시 된 것 처럼 일치 하는 값을 로컬 값으로 저장할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3805.fs)]

때때로 사용 되는 다른 패턴은 함수의 본문으로 암시적 인수에서 패턴 일치를 즉시 수행 하는 람다 식을 제공 하 여 명명 되지 않은 마지막 인수를 유지 하는 함수입니다. 이에 대 한 예제는 다음 코드 줄입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3804.fs)]

이 코드는 제네릭 목록을 사용 하 고 목록이 비어 `true` `false` 있는 경우를 반환 하 고 그렇지 않으면를 반환 하는 함수를 정의 합니다. 이러한 기술을 사용 하면 코드를 읽기가 더 어려울 수 있습니다.

때로는 불완전 한 일치 항목을 포함 하는 패턴이 유용 합니다. 예를 들어 프로그램의 목록에 요소가 세 개만 있는 경우에는 매개 변수 목록에서 다음과 같은 패턴을 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3806.fs)]

불완전 한 일치 항목이 있는 패턴의 사용은 빠른 프로토타입 및 기타 임시 용도로 사용 하기에 가장 적합 합니다. 컴파일러는 이러한 코드에 대 한 경고를 실행 합니다. 이러한 패턴은 가능한 모든 입력의 일반적인 경우를 포함할 수 없으므로 구성 요소 Api에 적합 하지 않습니다.

## <a name="named-arguments"></a>명명된 인수

메서드에 대 한 인수는 쉼표로 구분 된 인수 목록에서 위치로 지정 하거나, 이름, 앞에 등호 및 전달 될 값을 제공 하 여 명시적으로 메서드에 전달할 수 있습니다. 이름을 제공 하 여 지정 하는 경우 선언에 사용 된 것과 다른 순서로 표시 될 수 있습니다.

명명 된 인수를 사용 하면 메서드 매개 변수를 다시 정렬 하는 등 API의 특정 변경 내용에 대 한 코드를 더 읽기 쉽고 더 쉽게 조정할 수 있습니다.

명명 된 인수는 바인딩된 함수, 함수 값 또는 `let`람다 식이 아닌 메서드에만 사용할 수 있습니다.

다음 코드 예제에서는 명명 된 인수를 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3807.fs)]

클래스 생성자에 대 한 호출에서 명명 된 인수의 구문과 유사한 구문을 사용 하 여 클래스의 속성 값을 설정할 수 있습니다. 다음 예제에서는이 구문을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3506.fs)]

자세한 내용은 [생성자 (F#)](https://msdn.microsoft.com/library/2cd0ed07-d214-4125-8317-4f288af99f05)를 참조 하세요.

## <a name="optional-parameters"></a>선택적 매개 변수

매개 변수 이름 앞에 물음표를 사용 하 여 메서드에 대 한 선택적 매개 변수를 지정할 수 있습니다. 선택적 매개 F# 변수는 옵션 유형으로 해석 되므로 `match` `Some` 및 `None`를 사용 하는 식을 사용 하 여 옵션 유형을 쿼리 하는 일반적인 방법으로 쿼리할 수 있습니다. 선택적 매개 변수는 바인딩을 사용 하 `let` 여 만든 함수가 아닌 멤버에만 허용 됩니다.

또는 `?arg=None` `?arg=Some(3)` 또는 와같은매개변수이름을통해메서드에기존선택적값을전달할수있습니다.`?arg=arg` 이는 다른 메서드에 선택적 인수를 전달 하는 메서드를 작성할 때 유용할 수 있습니다.

선택적 인수의 기본값을 설정 하 `defaultArg`는 함수를 사용할 수도 있습니다. 함수 `defaultArg` 는 선택적 매개 변수를 첫 번째 인수로 사용 하 고 기본값을 두 번째 인수로 사용 합니다.

다음 예에서는 선택적 매개 변수를 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3808.fs)]

출력은 다음과 같습니다.

```console
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
Baud Rate: 300 Duplex: Half Parity: true
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
```

C# 및 Visual Basic interop를 위해 호출자가 인수를 선택적으로 볼 `[<Optional; DefaultParameterValue<(...)>]` 수 F#있도록의 특성을 사용할 수 있습니다. 이는의 C# `MyMethod(int i = 3)`에서와 같이 인수를 선택적으로 정의 하는 것과 같습니다.

```fsharp
open System
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue("Hello world")>] message) =
        printfn "%s" message
```

새 개체를 기본 매개 변수 값으로 지정할 수도 있습니다. 예를 들어, `Foo` 멤버는 다음과 같이 선택적인 `CancellationToken` 항목을 입력할 수 있습니다.

```fsharp
open System.Threading
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue(CancellationToken())>] ct: CancellationToken) =
        printfn "%A" ct
```

에 대 한 `DefaultParameterValue` 인수로 지정 된 값은 매개 변수의 형식과 일치 해야 합니다. 예를 들어 다음은 허용 되지 않습니다.

```fsharp
type C =
    static member Wrong([<Optional; DefaultParameterValue("string")>] i:int) = ()
```

이 경우 컴파일러는 경고를 생성 하 고 두 특성을 모두 무시 합니다. 컴파일러가 잘못 된 형식 ( `null` `[<Optional; DefaultParameterValue(null:obj)>] o:obj`예:)을 유추 하기 때문에 기본값은 형식으로 주석을 지정 해야 합니다.

## <a name="passing-by-reference"></a>참조로 전달

참조로 F# 값을 전달 하는 데는 관리 되는 포인터 형식인 [byref 배열과 같은](byrefs.md)이 포함 됩니다. 사용할 형식에 대 한 지침은 다음과 같습니다.

- 포인터 `inref<'T>` 를 읽기만 하면를 사용 합니다.
- 포인터 `outref<'T>` 에만 써야 하는 경우에는를 사용 합니다.
- 포인터 `byref<'T>` 에 대 한 읽기 및 쓰기를 모두 수행 해야 하는 경우에는를 사용 합니다.

```fsharp
let example1 (x: inref<int>) = printfn "It's %d" x

let example2 (x: outref<int>) = x <- x + 1

let example3 (x: byref<int>) =
    printfn "It'd %d" x
    x <- x + 1

// No need to make it mutable, since it's read-only
let x = 1
example1 &x

// Needs to be mutable, since we write to it
let mutable y = 2
example2 &y
example3 &y // Now 'y' is 3
```

매개 변수는 포인터이 고 값은 변경할 수 있으므로 값에 대 한 모든 변경 내용은 함수를 실행 한 후에도 유지 됩니다.

튜플을 반환 값으로 사용 하 여 .net 라이브러리 메서드에서 `out` 매개 변수를 저장할 수 있습니다. 또는 매개 변수를 `out` `byref` 매개 변수로 취급할 수 있습니다. 다음 코드 예제에서는 두 가지 방법을 모두 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3810.fs)]

## <a name="parameter-arrays"></a>매개 변수 배열

경우에 따라 형식이 다른 형식의 매개 변수를 임의로 사용 하는 함수를 정의 해야 합니다. 사용 가능한 모든 형식을 고려 하는 오버 로드 된 모든 메서드를 만드는 것은 실용적이 지 않습니다. .NET 구현은 매개 변수 배열 기능을 통해 이러한 메서드에 대 한 지원을 제공 합니다. 시그니처에 매개 변수 배열을 사용 하는 메서드는 임의의 수의 매개 변수를 사용 하 여 제공할 수 있습니다. 매개 변수는 배열에 배치 됩니다. 배열 요소의 형식은 함수에 전달 될 수 있는 매개 변수 형식을 결정 합니다. 를 요소 형식으로 사용 `System.Object` 하 여 매개 변수 배열을 정의 하는 경우 클라이언트 코드는 모든 형식의 값을 전달할 수 있습니다.

에서 F#매개 변수 배열은 메서드에만 정의할 수 있습니다. 모듈에 정의 된 독립 실행형 함수 또는 함수에서 사용할 수 없습니다.

`ParamArray` 특성을 사용 하 여 매개 변수 배열을 정의 합니다. 특성 `ParamArray` 은 마지막 매개 변수에만 적용할 수 있습니다.

다음 코드에서는 매개 변수 배열을 사용 하는 .NET 메서드를 호출 하는 방법과에서 F# 매개 변수 배열을 사용 하는 메서드가 있는 형식의 정의를 모두 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-2/snippet3811.fs)]

프로젝트에서 실행 하는 경우 이전 코드의 출력은 다음과 같습니다.

```console
a 1 10 Hello world 1 True
"a"
1
10.0
"Hello world"
1u
true
```

## <a name="see-also"></a>참고 항목

- [멤버](./members/index.md)
