---
title: F# 코딩 규칙
description: 작성 하는 경우 일반 지침 및 코드에 알아봅니다 F# 코드입니다.
ms.date: 05/14/2018
ms.openlocfilehash: c8df654cbb94fff1ef7ffb909655439398f30bf5
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67402371"
---
# <a name="f-coding-conventions"></a>F# 코딩 규칙

다음 규칙에 작업 환경에서 공식화 됩니다 F# 코드 베이스입니다. 합니다 [good의 다섯 가지 원칙 F# 코드](index.md#five-principles-of-good-f-code) 각 권장 사항의 기반이 됩니다. 관련이 합니다 [ F# 구성 요소 디자인 지침](component-design-guidelines.md), 이지만에 적용할 수 있습니다 F# 코드 라이브러리와 같은 뿐 아니라 구성 요소입니다.

## <a name="organizing-code"></a>코드를 구성합니다.

F#코드를 구성 하는 두 가지 기능: 모듈 및 네임 스페이스입니다. 이러한 유사 하지만 다음과 같은 차이가 있습니다.

* 네임 스페이스는.NET 네임 스페이스도 컴파일됩니다. 모듈은 정적 클래스로 컴파일됩니다.
* 네임 스페이스는 항상 최상위 수준입니다. 최상위 및 다른 모듈 내에 중첩 모듈 수 있습니다.
* 네임 스페이스는 여러 파일을 확장할 수 있습니다. 모듈 수 없습니다.
* 모듈을 데코 레이트 할 수 있습니다 `[<RequireQualifiedAccess>]` 고 `[<AutoOpen>]`입니다.

다음 지침은 세미콜론을 사용 하 여 코드를 구성 하는 데 도움이 됩니다.

### <a name="prefer-namespaces-at-the-top-level"></a>최상위 수준에서 네임 스페이스를 선호 합니다.

공개적으로 사용할 수 있는 모든 코드에 대 한 네임 스페이스는 최상위 모듈에 기본 설정. .NET 네임 스페이스를 컴파일되지 때문에 문제 없이 C#에서 사용 됩니다.

```fsharp
// Good!
namespace MyCode

type MyClass() =
    ...
```

최상위 모듈을 사용 하 여 다른 에서만 호출 될 때 나타날 수 없습니다 F#, 하지만 C# 소비자를 한정할 필요에서 달라진 것을 호출자에 게 수 `MyClass` 사용 하 여는 `MyCode` 모듈.

```fsharp
// Bad!
module MyCode

type MyClass() =
    ...
```

### <a name="carefully-apply-autoopen"></a>신중 하 게 적용 `[<AutoOpen>]`

`[<AutoOpen>]` 구문을 호출자에 게 사용할 수 있는 항목의 범위를 손상 시 키 지 수 및 항목에서 원본 위치에 대 한 답은 "매직"입니다. 이 일반적으로 유용 하지 않습니다. 이 규칙의 예외는 F# (하지만 이것이 약간 논쟁의 여지가) 자체 핵심 라이브러리입니다.

그러나 것 편의 위해 해당 공용 API에서 개별적으로 구성 하려는 공용 API에 대 한 도우미 기능이 있습니다.

```fsharp
module MyAPI =
    [<AutoOpen>]
    module private Helpers =
        let helper1 x y z =
            ...

    let myFunction1 x =
        let y = ...
        let z = ...

        helper1 x y z
```

이렇게 하면 완벽 하 게 호출 될 때마다 도우미를 한정할 필요 없이 공용 API 함수에서 명확 하 게 별도 구현 세부 사항이 있습니다.

또한 확장 메서드 및 식 작성기는 네임 스페이스 수준에서 노출 깔끔하게으로 표현할 수 `[<AutoOpen>]`입니다.

### <a name="use-requirequalifiedaccess-whenever-names-could-conflict-or-you-feel-it-helps-with-readability"></a>사용 하 여 `[<RequireQualifiedAccess>]` 이름이 충돌할 수 있습니다 또는 수 있다고 생각 가독성을 높이 데 도움이 될 때마다

추가 된 `[<RequireQualifiedAccess>]` 모듈을 열 수 있습니다 하 액세스를 정규화 하는 모듈의 요소에 대 한 참조가 필요 명시적 특성을 모듈을 나타냅니다. 예를 들어를 `Microsoft.FSharp.Collections.List` 모듈에이 특성이 있습니다.

이 함수 및 모듈의 값 이름이 다른 모듈에서 이름이 충돌할 가능성이 있는 경우에 유용 합니다. 정규화 된 액세스가 필요한 장기적 유지 관리성 및 라이브러리의 진화를 크게 증가할 수 있습니다.

```fsharp
[<RequireQualifiedAccess>]
module StringTokenization =
    let parse s = ...

...

let s = getAString()
let parsed = StringTokenization.parse s // Must qualify to use 'parse'
```

### <a name="sort-open-statements-topologically"></a>정렬 `open` 문을 표면

F#를 선언 측면을 비롯 한 순서 `open` 문입니다. 이 C#과 달리 여기서 미치는 `using` 및 `using static` 파일에서 이러한 문은 순서와 무관 합니다.

F#를 범위로 열 요소는 이미 다른 섀도잉할 수 있습니다. 즉, 해당 재정렬 `open` 문을 코드의 의미를 변경할 수 있습니다. 결과적으로 모든 정렬 임의의 `open` 문 (예를 들어, 사전순으로) 일반적으로 권장 되지 않습니다 내용을 볼 수 있는 다른 동작을 생성 합니다.

대신 좋습니다 정렬 하기 [표면](https://en.wikipedia.org/wiki/Topological_sorting); 순서 즉, 프로그램 `open` 문은 나타나는 순서 대로 _계층_ 정의 된 시스템의 합니다. 다양 한 토폴로지 계층 정렬 영숫자 수행도 고려할 수 있습니다.

예를 들어 다음은 정렬에 대 한 토폴로지는 F# 컴파일러 서비스 공개 API 파일:

```fsharp
namespace Microsoft.FSharp.Compiler.SourceCodeServices

open System
open System.Collections.Generic
open System.Collections.Concurrent
open System.Diagnostics
open System.IO
open System.Reflection
open System.Text

open Microsoft.FSharp.Compiler
open Microsoft.FSharp.Compiler.AbstractIL
open Microsoft.FSharp.Compiler.AbstractIL.Diagnostics
open Microsoft.FSharp.Compiler.AbstractIL.IL
open Microsoft.FSharp.Compiler.AbstractIL.ILBinaryReader
open Microsoft.FSharp.Compiler.AbstractIL.Internal
open Microsoft.FSharp.Compiler.AbstractIL.Internal.Library

open Microsoft.FSharp.Compiler.AccessibilityLogic
open Microsoft.FSharp.Compiler.Ast
open Microsoft.FSharp.Compiler.CompileOps
open Microsoft.FSharp.Compiler.CompileOptions
open Microsoft.FSharp.Compiler.Driver
open Microsoft.FSharp.Compiler.ErrorLogger
open Microsoft.FSharp.Compiler.Infos
open Microsoft.FSharp.Compiler.InfoReader
open Microsoft.FSharp.Compiler.Lexhelp
open Microsoft.FSharp.Compiler.Layout
open Microsoft.FSharp.Compiler.Lib
open Microsoft.FSharp.Compiler.NameResolution
open Microsoft.FSharp.Compiler.PrettyNaming
open Microsoft.FSharp.Compiler.Parser
open Microsoft.FSharp.Compiler.Range
open Microsoft.FSharp.Compiler.Tast
open Microsoft.FSharp.Compiler.Tastops
open Microsoft.FSharp.Compiler.TcGlobals
open Microsoft.FSharp.Compiler.TypeChecker
open Microsoft.FSharp.Compiler.SourceCodeServices.SymbolHelpers

open Internal.Utilities
open Internal.Utilities.Collections
```

줄 바꿈을 나중에 사전순으로 정렬 하 고 각 계층을 사용 하 여 토폴로지 계층을 구분 하는 참고 합니다. 이 값을 실수로 섀도잉 없이 코드를 완전히 구성 합니다.

## <a name="use-classes-to-contain-values-that-have-side-effects"></a>의도 하지 않은 값을 포함 하도록 클래스를 사용 합니다.

경우가 많은 경우 값을 초기화 있습니다 데이터베이스나 다른 원격 리소스에 대 한 컨텍스트를 인스턴스화하고 같은 부작용이 발생 합니다. 모듈에서 이러한 작업을 초기화 하 고 후속 함수에서 사용 하기 쉽습니다.

```fsharp
// This is bad!
module MyApi =
    let dep1 = File.ReadAllText "/Users/{your name}/connectionstring.txt"
    let dep2 = Environment.GetEnvironmentVariable "DEP_2"

    let private r = Random()
    let dep3() = r.Next() // Problematic if multiple threads use this

    let function1 arg = doStuffWith dep1 dep2 dep3 arg
    let function2 arg = doSutffWith dep1 dep2 dep3 arg
```

이 자주 좋은 몇 가지 이유로:

응용 프로그램 구성을 사용 하 여 코드 베이스에 푸시됩니다. 먼저 `dep1` 고 `dep2`입니다. 이 더 큰 코드 베이스에서 유지 관리 하기가 어렵습니다.

두 번째, 정적으로 초기화 된 데이터는 구성 요소 자체 여러 스레드에서 사용 하는 경우 스레드로부터 안전 하지 않은 값을 포함 되지 않습니다. 이 명확 하 게에 위반 `dep3`합니다.

마지막으로 모듈을 초기화 전체 컴파일 단위에 대 한 정적 생성자로 컴파일합니다. 으로 매니페스트는 모듈의 let 바인딩 값 초기화에서 오류가 발생할 경우를 `TypeInitializationException` 는 다음 응용 프로그램의 전체 수명 동안 캐시 됩니다. 이 진단이 어려울 수 있습니다. 일반적으로 내부 예외에 대 한 이유를 시작할 수 있습니다 하지만 없는 경우 다음이 근본 원인을 새로운 기능입니다.

대신,만 사용 하 여 간단한 클래스 종속성을 갖는.

```fsharp
type MyParametricApi(dep1, dep2, dep3) =
    member __.Function1 arg1 = doStuffWith dep1 dep2 dep3 arg1
    member __.Function2 arg2 = doStuffWith dep1 dep2 dep3 arg2
```

이 후 다음이 가능 합니다.

1. API 자체 외부 종속 된 모든 상태를 푸시합니다.
2. 구성은 API를 외부에서 지금 수행할 수 있습니다.
3. 종속 값에 대 한 초기화 오류도 나타날 가능성이 없는 `TypeInitializationException`입니다.
4. API를 쉽게 테스트 되었습니다.

## <a name="error-management"></a>오류 관리

대규모 시스템의 오류 관리는 복잡 하 고 미묘한 노력, 되며 없습니다 silver 시스템 보장 글머리 기호는 내결함성 및 잘 작동 합니다. 다음 지침은 이동이 어렵게 공간에 대 한 지침을 제공 해야 합니다.

### <a name="represent-error-cases-and-illegal-state-in-types-intrinsic-to-your-domain"></a>오류 사례 및 도메인에 기본 형식에 잘못 된 상태를 나타내는

사용 하 여 [구별 된 공용 구조체](../language-reference/discriminated-unions.md), F# 형식 시스템에 결함이 있는 프로그램 상태를 나타낼 수 있습니다. 예를 들어:

```fsharp
type MoneyWithdrawalResult =
    | Success of amount:decimal
    | InsufficientFunds of balance:decimal
    | CardExpired of DateTime
    | UndisclosedFailure
```

이 경우 세 가지 알려진 money 은행 계좌에서 출금 실패할 수 있는 합니다. 각 오류 사례 형식으로 표현 되 고 있으므로 처리할 수 있습니다 사용 하 여 안전 하 게 프로그램 전체에서.

```fsharp
let handleWithdrawal amount =
    let w = withdrawMoney amount
    match w with
    | Success am -> printfn "Successfully withdrew %f" am
    | InsufficientFunds balance -> printfn "Failed: balance is %f" balance
    | CardExpired expiredDate -> printfn "Failed: card expired on %O" expiredDate
    | UndisclosedFailure -> printfn "Failed: unknown"
```

일반적으로 다양 한 방법을 모델링할 수 없습니다. 했을 수 없습니다 **실패** 도메인에서 다음 오류 처리 코드는 더 이상 처리 일반 프로그램 흐름 외에도 처리 해야 하는 것으로 합니다. 단순히 일반 프로그램 흐름의 일부 이며 간주 되지 않습니다 **예외적인**합니다. 이 두 가지 주요 이점을 가지 있습니다.

1. 시간이 지남에 따라 변경 되는 도메인을 유지 하는 것이 쉽습니다.
2. 오류 사례는 단위 테스트 하기 쉽습니다.

### <a name="use-exceptions-when-errors-cannot-be-represented-with-types"></a>오류 형식으로 표현할 수 없는 경우 예외를 사용 합니다.

문제 도메인의 모든 오류를 나타낼 수 있습니다. 이러한 종류의 오류를 *예외적인* 본질적으로 따라서 시키고 예외를 catch 하는 기능 F#합니다.

첫째, 것이 좋습니다 읽어 합니다 [예외 디자인 지침](../../standard/design-guidelines/exceptions.md)합니다. 이러한 경우에 적용할 F#입니다.

기본 구문에서 사용할 수 있는 F# 다음 우선 순위에서 예외를 발생 시키기 위해 고려해 야에 대 한 합니다.

| 함수 | 구문 | 용도 |
|----------|--------|---------|
| `nullArg` | `nullArg "argumentName"` | 발생 한 `System.ArgumentNullException` 지정한 인수 이름을 사용 하 여 합니다. |
| `invalidArg` | `invalidArg "argumentName" "message"` | 발생 한 `System.ArgumentException` 지정 된 인수 이름과 메시지를 사용 하 여 합니다. |
| `invalidOp` | `invalidOp "message"` | 발생 한 `System.InvalidOperationException` 지정된 된 메시지를 사용 하 여 합니다. |
|`raise`| `raise (ExceptionType("message"))` | 예외를 throw 하는 것에 대 한 일반 용도의 메커니즘입니다. |
| `failwith` | `failwith "message"` | 발생 한 `System.Exception` 지정된 된 메시지를 사용 하 여 합니다. |
| `failwithf` | `failwithf "format string" argForFormatString` | 발생을 `System.Exception` 서식 문자열 및 해당 입력에 따른 메시지와 함께 합니다. |

사용 하 여 `nullArg`, `invalidArg` 하 고 `invalidOp` throw 하는 메커니즘으로 `ArgumentNullException`를 `ArgumentException` 및 `InvalidOperationException` 적절 한 합니다.

합니다 `failwith` 및 `failwithf` 함수 기본 발생 하므로 피해 야 일반적으로 `Exception` 특정 예외가 아닌를 입력 합니다. 기준으로 합니다 [예외 디자인 지침](../../standard/design-guidelines/exceptions.md), 가능한 경우 보다 구체적인 예외를 발생 시키려면 합니다.

### <a name="using-exception-handling-syntax"></a>예외 처리 구문을 사용 하 여

F#통해 예외 패턴을 지원 합니다 `try...with` 구문:

```fsharp
try
    tryGetFileContents()
with
| :? System.IO.FileNotFoundException as e -> // Do something with it here
| :? System.Security.SecurityException as e -> // Do something with it here
```

패턴 일치와 함께 예외가 발생 하는 경우 수행 하는 기능을 조정 하는 정리 코드를 유지 하려는 경우에 약간 까다로울 수 있습니다. 이 처리 하기 위해 이러한 방법 중 하나를 사용 하는 것 [활성 패턴](../language-reference/active-patterns.md) 자체 예외를 사용 하 여 오류 사례를 둘러싼 그룹 기능을 하는 것입니다. 예를 들어, 예외를 throw 할 때 예외 메타 데이터에서 중요 한 정보를 포함 하는 API 사용 수 있습니다. 활성 패턴 내에서 캡처된 예외의 본문에 유용한 값을 래핑 해제 및 반환 값 일부 상황에서 유용 합니다.

### <a name="do-not-use-monadic-error-handling-to-replace-exceptions"></a>Monadic 오류 예외를 바꾸려면 처리를 사용 하지 마세요

예외는 함수형 프로그래밍에서 다소 taboo로 표시 됩니다. 실제로 예외 not 상당히 기능으로 간주 해도 이므로 무결성을 위반 합니다. 그러나이 코드 실행 해야 합니다는 위치 및 해당 런타임 오류가 발생할 수 있습니다 실제로 무시 합니다. 일반적으로 대부분의 항목이 순수 아니고 총 반갑지 않은 놀라움을 최소화 하기 위해 가정 하에서 코드를 작성 합니다.

것이 핵심 장점/의 다음 측면을 예외는 관련성 및 전체.NET 런타임 및 언어 간 에코 시스템의 적합성에 대해 고려해 야 할 중요 합니다.

1. 문제를 디버깅 하는 경우 매우 유용 하는 자세한 진단 정보를 포함 합니다.
2. 런타임 및 기타.NET 언어에서 잘 인식 됩니다.
3. 해당 방법에서 사용 되는 코드를 비교할 때 중요 한 상용구 줄일 수 있습니다 *방지* 임시 단위로 해당 의미 체계의 일부 하위 집합을 구현 하 여 예외입니다.

이 세 번째 점이 중요 합니다. 복잡 한 작업의 중요 한 경우 예외를 사용 하지 않고이 같은 구조를 사용 하 여 처리에서 발생할 수 있습니다.

```fsharp
Result<Result<MyType, string>, string list>
```

"형식의 stringly" 오류에 패턴 일치와 같은 취약 한 코드를 쉽게 발생할 수 있습니다.

```fsharp
let result = doStuff()
match result with
| Ok r -> ...
| Error e ->
    if e.Contains "Error string 1" then ...
    elif e.Contains "Error string 2" then ...
    else ... // Who knows?
```

또한 "멋진" 형식을 반환 하는 "단순" 함수에 대 한 원하는 모든 예외를 무시 하 고 싶을 수 있습니다.

```fsharp
// This is bad!
let tryReadAllText (path : string) =
    try System.IO.File.ReadAllText path |> Some
    with _ -> None
```

아쉽게도 `tryReadAllText` 무수 한 파일 시스템에서 발생할 수 있는 작업을 기반으로 하는 다양 한 예외를 throw 할 수 있습니다 및이 코드를 지금 삭제 수 실제로 수 무엇이 환경의 대 한 정보입니다. 결과 형식을 사용 하 여이 코드를 대체 하는 경우 작성할 때는 메시지 구문 분석 오류 "형식의 stringly" 돌아가기:

```fsharp
// This is bad!
let tryReadAllText (path : string) =
    try System.IO.File.ReadAllText path |> Ok
    with e -> Error e.Message

let r = tryReadAllText "path-to-file"
match r with
| Ok text -> ...
| Error e ->
    if e.Contains "uh oh, here we go again..." then ...
    else ...
```

예외 개체 자체를 배치 하 고에 `Error` 아닌 함수 호출 사이트에서 예외 형식으로 제대로 처리 하는 생성자만 강제 합니다. 이렇게 효율적으로 악명이 높습니다 재미 API의 호출자가 처리 되지 않는 확인된 예외를 만듭니다.

위의 예제에 대 한 좋은 대안은 catch 하는 것 *특정* 예외 및 해당 예외의 컨텍스트에서 의미 있는 값을 반환 합니다. 수정 하는 경우는 `tryReadAllText` 함수를 다음과 같이 `None` 자세한 의미가:

```fsharp
let tryReadAllTextIfPresent (path : string) =
    try System.IO.File.ReadAllText path |> Some
    with :? FileNotFoundException -> None
```

범용으로 작동 하는 대신이 함수는 이제 제대로 처리 경우 파일을 찾을 수 없습니다 하 고 반환 하는 의미를 할당 합니다. 반환 값이 모든 컨텍스트 정보를 삭제 하거나 호출자가 코드의 해당 지점에서 적절 하지 않을 경우를 처리 하도록 강제 하지 하는 동안 해당 오류 사례를 매핑할 수 있습니다.

와 같은 형식 `Result<'Success, 'Error>` 적합 한 기본 작업에 대 한 중첩 되지 않습니다 여기서 및 F# 선택적 형식은 완벽 한 반환 없습니다 것을 나타내는 경우에 대 한 *무언가* 또는 *아무것도*. 예외에 대 한 대체 하지는 하지만 하며 해서는 안 시도할 때에서 예외를 교체할 수 있습니다. 대신 이러한 해야 신중 하 게 요소에 적용할 수 주소 특정 예외 및 오류 관리 정책의 대상으로 지정 된 방식에서입니다.

## <a name="partial-application-and-point-free-programming"></a>부분 응용 프로그램 및 지점 무료 프로그래밍

F#지점 무료 스타일에서 부분 응용 프로그램 및 따라서 다양 한 프로그램을 지원합니다. 이 모듈 또는 항목의 구현 내에서 코드 재사용에 대 한 도움이 될 수 있지만 이것은 일반적으로 공개적으로 노출 하 합니다. 일반적으로 지점 무료 프로그래밍에 자체의 전문화 아니며 스타일을 사용 하지는 사람들에 게 중요 한 cognitive barrier를 추가할 수 있습니다.

### <a name="do-not-use-partial-application-and-currying-in-public-apis"></a>부분 응용 프로그램 및 공용 api에서 (currying) 사용 하지 마십시오

거의 예외를 제외 하 고, 공용 Api에서 부분 응용 프로그램의 사용 소비자에 대 한 혼동 될 수 있습니다. 일반적으로 `let`-값에 바인딩된 F# 코드 **값**아니라 **함수 값**. 와 같은 연산자를 사용 하 여 결합 하는 경우에 특히 소수의 cognitive 오버 헤드를 줄이려면 상당한 대가로 코드 줄을 저장 하는 중 발생할 수 있습니다 함수 값과 함께 혼합 `>>` 함수를 작성 하 합니다.

### <a name="consider-the-tooling-implications-for-point-free-programming"></a>지점 무료 프로그래밍 도구 결과 고려해 야

커리 된 함수는 해당 인수 레이블이 지정 되지 않습니다. 이 의미를 도구에 있습니다. 다음 두 가지 함수를 고려 합니다.

```fsharp
let func name age =
    printfn "My name is %s and I am %d years old!" name age

let funcWithApplication =
    printfn "My name is %s and I am %d years old!"
```

둘 다 유효 함수 있지만 `funcWithApplication` 커리 된 함수입니다. 편집기에서 해당 형식의 마우스로 가리키면이 표시 됩니다.

```fsharp
val func : name:string -> age:int -> unit

val funcWithApplication : (string -> int -> unit)
```

호출 사이트에서 Visual Studio와 같은 도구에서 도구 설명을 제공 되지 것입니다 어떤 의미 있는 정보를 `string` 고 `int` 입력된 형식은 실제로 나타냅니다.

다음과 같은 코드 포인트 무료 발생 하는 경우 `funcWithApplication` 는 공개적으로 사용할 수 있는 것이 좋습니다 도구 수에 의미 있는 이름을 인수에 대 한 작업을 전체 η 확장을 수행 합니다.

또한 지점 해제 코드를 디버깅 어려울 수 있습니다, 거의 불가능 합니다. 이름에 바인딩된 값에 의존 하는 디버깅 도구 (예를 들어 `let` 바인딩) 실행 중간 중간 값을 검사할 수 있도록 합니다. 코드를 검사할 값이 없는 있는 경우 디버그 것이 없습니다. 나중에 디버깅 도구 이전에 실행된 경로에 따라 이러한 값을 만드는 진화 할 수 있지만 사용자 선택에서 다변화 하는 좋은 방법이 아닙니다 *잠재적인* 기능을 디버그 합니다.

### <a name="consider-partial-application-as-a-technique-to-reduce-internal-boilerplate"></a>내부 상용구를 줄이기 위해 기술로 서 부분 응용 프로그램

앞서 달리 부분 응용 프로그램은 응용 프로그램 또는 API의 심층적인 내부 내부 상용구를 줄이기 위한 훌륭한 도구. 단위 테스트 상용구 경우가 얼마나 많은 노력을 처리 하는 더 복잡 한 Api 구현 하는 데 도움이 수 있습니다. 예를 들어, 수행 하는 방법은 다음 코드와 어떤 가장 모의 프레임 워크를 제공 하면 이러한 프레임 워크 외부 종속성을 수행 하지 않고 API를 맞춤식 관련 배울 필요 하며

예를 들어, 다음 솔루션 토폴로지를 고려 합니다.

```
MySolution.sln
|_/ImplementationLogic.fsproj
|_/ImplementationLogic.Tests.fsproj
|_/API.fsproj
```

`ImplementationLogic.fsproj` 와 같은 코드를 노출 될 수 있습니다.

```fsharp
module Transactions =
    let doTransaction txnContext txnType balance =
        ...

type Transactor(ctx, currentBalance) =
    member __.ExecuteTransaction(txnType) =
        Transactions.doTransaction ctx txtType currentBalance
        ...
```

단위 테스트 `Transactions.doTransaction` 에서 `ImplementationLogic.Tests.fsproj` 쉽습니다.

```fsharp
namespace TransactionsTestingUtil

open Transactions

module TransactionsTestable =
    let getTestableTransactionRoutine mockContext = Transactions.doTransaction mockContext
```

부분적으로 적용 `doTransaction` 모의 컨텍스트를 사용 하 여 개체 때마다 모의 컨텍스트를 생성 하지 않고도 단위 테스트의 모든 함수를 호출할 수 있습니다.

```fsharp
namespace TransactionTests

open Xunit
open TransactionTypes
open TransactionsTestingUtil
open TransactionsTestingUtil.TransactionsTestable

let testableContext =
    { new ITransactionContext with
        member __.TheFirstMember() = ...
        member __.TheSecondMember() = ... }

let transactionRoutine = getTestableTransactionRoutine testableContext

[<Fact>]
let ``Test withdrawal transaction with 0.0 for balance``() =
    let expected = ...
    let actual = transactionRoutine TransactionType.Withdraw 0.0
    Assert.Equal(expected, actual)
```

전체 코드 베이스에이 기술을 보편적으로 적용 되지 해야 하지만 복잡 한 내부 및 단위 테스트 해당 내부 요소에 대 한 상용구를 줄이기 위해 좋은 방법입니다.

## <a name="access-control"></a>액세스 제어

F#에 대 한 여러 옵션이 [액세스 제어](../language-reference/access-control.md).NET 런타임에서 사용할 수 있는 항목에서 상속 합니다. 이러한 형식에 대 한 바로 사용할 수 없는 경우-도 사용할 수 있습니다 이러한 함수에 대 한 합니다.

* 비-선호`public` 형식 및 공개적으로 사용할 수 있도록 하는 데 필요할 때까지 멤버입니다. 또한 어떤 소비자 결합을 되도록 최소화 됩니다.
* 모든 도우미 기능을 유지 하도록 `private`합니다.
* 사용을 고려 `[<AutoOpen>]` 도우미 함수의 다양 한 경우 개인 모듈입니다.

## <a name="type-inference-and-generics"></a>형식 유추 및 제네릭

형식 유추 상용구 많은 입력에서 절약할 수 있습니다. 및 자동 일반화에는 F# 컴파일러는 하면 사용자의 추가 작업 없이 거의 보다 일반적인 코드를 작성할 수 있습니다. 그러나 이러한 기능은 일반적으로 좋은 되지 않습니다.

* 공용 Api의 명시적 형식 인수 이름 레이블을 지정 하는 것이 좋습니다. 및이 대 한 형식 유추에 의존 하지 마십시오.

    이유 **있습니다** 컴파일러가 아닌 API의 모양 제어에서 해야 합니다. 컴파일러를 형식 유추에서 세밀 하 게 작업을 수행할 수 이지만 의존 하는 내부 형식을 변경한 경우 변경 내용을 API의 모양을 가질 수 있습니다. 원하는 항목을이 수 있지만 다운스트림 소비자가 처리 하는 주요 API 변경 내용을 거의 발생 합니다. 대신 공용 API의 모양의 명시적으로 제어 하는 경우 이러한 주요 변경 내용을 제어할 수 있습니다. DDD 용어에서이 수 생각할 수 손상 방지 레이어를 합니다.

* 제네릭 인수에 의미 있는 이름을 제공 하는 것이 좋습니다.

    특정 도메인에 한정 되지 않은 제네릭 실제로 코드를 작성 하는 경우가 아니면에 의미 있는 이름을 하는 도메인을 이해 하는 프로그래머에 게 다른 데 도움이 됩니다. 예를 들어, 형식 매개 변수 라는 `'Document` 문서와 상호 작용의 컨텍스트에서 데이터베이스 더 명확 하 게 제네릭 문서 형식을 함수 또는 멤버를 사용 하 여 사용할 수 있습니다.

* PascalCase 사용 하 여 제네릭 형식 매개 변수를 명명 하는 것이 좋습니다.

    이것이 하므로 camelCase 또는 snake_case를 사용 하는 대신 PascalCase를 사용 하는 것이 좋습니다..NET 작업을 수행 하는 일반적인 방법은입니다.

마지막으로, 자동 일반화 되지 항상 처음 사용 하는 사람들에 게 유용 하 게 F# 또는 큰 코드 베이스입니다. 일반적인 구성 요소를 사용 하 여 cognitive 오버 헤드가 있습니다. 또한 자동으로 다른 입력 형식 (let 마찬가지로 사용 되어야 하는 경우에), 일반화 된 함수를 사용 되지 않습니다 경우는 해당 시점에 제네릭에 실제 이점이 없습니다. 항상 코드를 작성 하는 제네릭에서 실제로 이익을 경우 하는 것이 좋습니다.

## <a name="performance"></a>성능

F#값은 특정 부류의 버그 (특히 해당 관련 된 동시성 및 병렬 처리 수준)를 방지할 수 있습니다는 기본적으로 변경할 수 없습니다. 그러나 경우에 따라 실행 시간 또는 메모리 할당의 최적의 (또는 합당 한도) 효율성을 달성 하기 위해 작업의 범위를 가장 잘 구현 될 수 있습니다 상태의 전체 변형을 사용 하 여. 이것이 가능한 것으로 옵트인 별로 F# 와 `mutable` 키워드입니다.

그러나 이용 `mutable` 에서 F# 기능 순도 잘 어울리지 생각 될 수도 있습니다. 해도 괜찮은 사용자 기대 수준에는 순수성 조정 하는 경우 이것이 [참조 투명성](https://en.wikipedia.org/wiki/Referential_transparency)합니다. 참조 투명성-순도-작성 하는 경우 최종 목표는 F# 함수입니다. 이 옵션을 사용 하면 성능이 중요 한 코드는 변이 기반 구현을 통해 기능 인터페이스를 작성할 수 있습니다.

### <a name="wrap-mutable-code-in-immutable-interfaces"></a>변경할 수 없는 인터페이스에서 변경할 수 있는 코드를 줄 바꿈

이 목표로 참조 투명성을 사용 하 여 성능이 중요 한 함수를 변경할 수 있는 언더 벨 리를 노출 하지 않는 코드를 쓸 중요 합니다. 예를 들어, 다음 코드 구현 된 `Array.contains` 함수는 F# 핵심 라이브러리:

```fsharp
[<CompiledName("Contains")>]
let inline contains value (array:'T[]) =
    checkNonNull "array" array
    let mutable state = false
    let mutable i = 0
    while not state && i < array.Length do
        state <- value = array.[i]
        i <- i + 1
    state
```

이 함수를 여러 번 호출 기본 배열에는 변경 되지 않습니다 요구 하지도 않습니다 사용에서 변경할 수 있는 상태를 유지할 수 있습니다. 그는 코드의 거의 모든 줄 변형을 사용 하는 경우에 것 참조가 투명 합니다.

### <a name="consider-encapsulating-mutable-data-in-classes"></a>클래스에서 변경할 수 있는 데이터를 캡슐화 하는 것이 좋습니다.

변경할 수 있는 데이터를 사용 하 여 작업을 캡슐화 하는 단일 함수를 사용 하는 앞의 예제입니다. 이 부족 항상 더 복잡 한 데이터 집합에 대 한 합니다. 다음 함수 집합을 고려 합니다.

```fsharp
open System.Collections.Generic

let addToClosureTable (key, value) (t: Dictionary<_,_>) =
    if not (t.ContainsKey(key)) then
        t.Add(key, value)
    else
        t.[key] <- value

let closureTableCount (t: Dictionary<_,_>) = t.Count

let closureTableContains (key, value) (t: Dictionary<_, HashSet<_>>) =
    match t.TryGetValue(key) with
    | (true, v) -> v.Equals(value)
    | (false, _) -> false
```

이 코드가 성능이 있지만 호출자가 유지 관리 하는 것에 대 한 책임이 있으며 기반 데이터 구조를 노출 합니다. 이 변경할 수 있는 기본 멤버 없이 클래스 내부 래핑할 수 있습니다.

```fsharp
open System.Collections.Generic

/// The results of computing the LALR(1) closure of an LR(0) kernel
type Closure1Table() =
    let t = Dictionary<Item0, HashSet<TerminalIndex>>()

    member __.Add(key, value) =
        if not (t.ContainsKey(key)) then
            t.Add(key, value)
        else
            t.[key] <- value

    member __.Count = t.Count

    member __.Contains(key, value) =
        match t.TryGetValue(key) with
        | (true, v) -> v.Equals(value)
        | (false, _) -> false
```

`Closure1Table` 호출자가 기본 데이터 구조를 유지 하도록 강제 적용 하지 않는 것으로 기본 변이 기반 데이터 구조를 캡슐화 합니다. 클래스는 데이터와 루틴 호출자에 게 세부 정보를 노출 하지 않고 변이 기반을 캡슐화 하는 강력한 방법입니다.

### <a name="prefer-let-mutable-to-reference-cells"></a>원하는 `let mutable` 참조 셀

참조 셀은 자체 값이 아닌 값에 대 한 참조를 나타내는 방법입니다. 성능이 중요 한 코드를 사용할 수 있습니다, 있지만 이러한 일반적으로 권장 되지 않습니다. 다음 예제를 참조하세요.

```fsharp
let kernels =
    let acc = ref Set.empty

    processWorkList startKernels (fun kernel ->
        if not ((!acc).Contains(kernel)) then
            acc := (!acc).Add(kernel)
        ...)

    !acc |> Seq.toList
```

참조 셀을 이제 사용 "오염" 역참조를 다시 참조 하려면 기본 데이터를 갖는 모든 후속 코드입니다. 대신 `let mutable`:

```fsharp
let kernels =
    let mutable acc = Set.empty

    processWorkList startKernels (fun kernel ->
        if not (acc.Contains(kernel)) then
            acc <- acc.Add(kernel)
        ...)

    acc |> Seq.toList
```

람다 식 중간 변경의 단일 지점 외에도 다른 모든 코드는 터치 `acc` 는 더 일반적인 사용에 다른 방식으로 수행할 수 `let`-바인딩된 변경할 수 없는 값입니다. 이 쉽게 시간이 지남에 따라 변경 합니다.

## <a name="object-programming"></a>개체 프로그래밍

F#개체 및 개체 지향 (개체 지향) 개념에 대 한 전체 지원 합니다. 여러 개체 지향 개념 강력 하 고 유용 하지만, 그 중 일부는 데 적합 합니다. 다음 목록에서는 높은 수준에서 개체 지향 기능 범주에 대 한 지침을 제공합니다.

**대부분의 경우에서 이러한 기능을 사용 하는 것이 좋습니다.**

* 점 표기법 (`x.Length`)
* 인스턴스 멤버
* 암시적 생성자
* 정적 멤버
* 인덱서 표기법 (`arr.[x]`)
* 명명 된 인수와 선택적 인수
* 인터페이스 및 인터페이스 구현

**먼저 이러한 기능에 대 한 도달 하지 않으므로 없지만 편리 하 게 문제를 해결 하는 경우에 적용할 신중 하 게 수행 합니다.**

* 메서드 오버로드
* 변경할 수 있는 데이터를 캡슐화합니다.
* 형식에 연산자
* 자동 속성
* 구현 `IDisposable` 및 `IEnumerable`
* 형식 확장명
* 이벤트
* 구조체
* 대리자
* 열거형

**일반적으로 사용 하지 않는 한 이러한 기능을 방지 합니다.**

* 형식 상속 기반 계층 구조 및 상속 구현
* Null 및 `Unchecked.defaultof<_>`

### <a name="prefer-composition-over-inheritance"></a>상속을 사용 하 여 컴퍼지션 선호합니다

[상속을 통해 컴포지션](https://en.wikipedia.org/wiki/Composition_over_inheritance) 장기 관용구는 양호 F# 코드 준수 수 있습니다. 기본 원칙 해야 하지 기본 클래스를 노출 하는 호출자 기능을 활용 하려면 해당 기본 클래스에서 상속 하도록 강제 됩니다.

### <a name="use-object-expressions-to-implement-interfaces-if-you-dont-need-a-class"></a>개체 식을 사용 하 여 클래스 필요가 없는 경우 인터페이스를 구현 합니다.

[개체 식](../language-reference/object-expressions.md) 클래스 내부 작업을 수행 하지 않고도 값으로 구현된 된 인터페이스를 바인딩 즉석에서 인터페이스를 구현할 수 있습니다. 이 편리 하 고 경우에 특히 있습니다 _만_ 전체 클래스에 대 한 필요가 없습니다 인터페이스를 구현 해야 합니다.

예를 들어, 다음은 코드에서 실행 되는 [Ionide](http://ionide.io/) 가지고 있지 않은 기호를 추가한 경우 코드 수정 작업을 제공 하는 `open` 문을:

```fsharp
    let private createProvider () =
        { new CodeActionProvider with
            member this.provideCodeActions(doc, range, context, ct) =
                let diagnostics = context.diagnostics
                let diagnostic = diagnostics |> Seq.tryFind (fun d -> d.message.Contains "Unused open statement")
                let res =
                    match diagnostic with
                    | None -> [||]
                    | Some d ->
                        let line = doc.lineAt d.range.start.line
                        let cmd = createEmpty<Command>
                        cmd.title <- "Remove unused open"
                        cmd.command <- "fsharp.unusedOpenFix"
                        cmd.arguments <- Some ([| doc |> unbox; line.range |> unbox; |] |> ResizeArray)
                        [|cmd |]
                res
                |> ResizeArray
                |> U2.Case1
        }
```

에 있기 때문에 클래스 하지 않아도 Visual Studio Code API와 상호 작용할 때 개체 식이란이 이상적인 도구입니다. 단위 테스트, 임시 방식으로 테스트 루틴을 사용 하 여 인터페이스를 없애는 하려고 할 때 유용할 수도 있습니다.

## <a name="type-abbreviations"></a>형식 약어

[형식 약어](../language-reference/type-abbreviations.md) 은 함수 서명 등 보다 복잡 한 형식을 다른 형식에 레이블을 지정 하는 편리한 방법입니다. 다음 별칭 레이블을 사용 하 여 계산을 정의 하는 데 필요한 항목을 할당 하는 예를 들어 [CNTK](https://docs.microsoft.com/cognitive-toolkit/), 심층 학습 라이브러리:

```fsharp
open CNTK

// DeviceDescriptor, Variable, and Function all come from CNTK
type Computation = DeviceDescriptor -> Variable -> Function
```

`Computation` 이름은 편리 하 게 시그니처와 일치 하는 것이 별칭을 지정 하는 모든 함수를 나타냅니다. 다음과 같은 형식 약어를 사용 하 여 편리 하 고 더 간결한 코드 허용 합니다.

### <a name="avoid-using-type-abbreviations-to-represent-your-domain"></a>도메인을 나타내는 형식 약어를 사용 하지 마십시오

형식 약어 함수 서명에 이름을 지정 하는 것에 대 한 편리 하기는 하지만 이러한 혼동 될 수 있습니다 다른 형식 이니셜 하는 경우입니다. 이 약어를 고려 합니다.

```fsharp
// Does not actually abstract integers.
type BufferSize = int
```

이 여러 가지 방법으로 혼동 될 수 있습니다.

* `BufferSize` 추상화; 아닙니다. 정수에 대 한 다른 이름입니다.
* 하는 경우 `BufferSize` 노출 된 공용 API에서이 쉽게 잘못 해석 될 수 이상의 의미 `int`합니다. 일반적으로 도메인에 여러 특성이 형식과 같은 기본 형식이 아닌 `int`합니다. 이 약어 위반 가정 합니다.
* 대/소문자 `BufferSize` (PascalCase)는이 이와 같은 더 많은 데이터를 보유 하는 것을 의미 합니다.
* 이 별칭 함수에 명명 된 인수를 제공에 비해 향상 된 명확성을 제공 하지 않습니다.
* 약어 컴파일된 IL; 영향은 없습니다. 마찬가지로 정수 이므로이 별칭은 컴파일 타임 구문.

```fsharp
module Networking =
    ...
    let send data (bufferSize: int) =
        ...
```

요약 하자면, 형식 약어를 사용 하 여 문제는 이들이 **되지** 이니셜는 이러한 형식을 통해 추상화 합니다. 이전 예에서 `BufferSize` 것을 `int` 없는 추가 데이터 나 내용 외에도 형식 시스템에서 모든 혜택을 사용 하 여 내부적으로 `int` 이미 합니다.
