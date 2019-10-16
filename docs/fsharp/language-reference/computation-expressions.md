---
title: 계산 식
description: 제어 흐름 구문 및 바인딩을 사용 하 여 시퀀싱 하 F# 고 결합할 수 있는 계산을 작성 하기 위한 편리한 구문을 만드는 방법에 대해 알아봅니다.
ms.date: 03/15/2019
ms.openlocfilehash: 9222be5a585914761d3001d6649b196030eec05e
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083049"
---
# <a name="computation-expressions"></a>계산 식

의 F# 계산 식은 제어 흐름 구문 및 바인딩을 사용 하 여 시퀀싱 하 고 결합할 수 있는 계산을 작성 하는 편리한 구문을 제공 합니다. 계산 식의 종류에 따라 monads, monoids, monad 변환기 및 applicative 함수를 표현 하는 방법으로 간주할 수 있습니다. 그러나 Haskell의 *do 표기법* 과 같은 다른 언어와 달리, 이러한 언어는 단일 추상화에 연결 되지 않으며, 매크로 또는 다른 형태의 메타 프로그래밍를 사용 하 여 편리 하 고 상황에 맞는 구문을 수행 하지 않습니다.

## <a name="overview"></a>개요

계산은 많은 형태를 사용할 수 있습니다. 가장 일반적인 계산 형태는 단일 스레드 실행 이며 이해 하 고 수정 하기 쉽습니다. 그러나 일부 계산 형태는 단일 스레드 실행 만큼 간단 하지 않습니다. 예를 들면 다음과 같습니다.

- 비결 정적 계산
- 비동기 계산
- Effectful 계산
- 인기 계산

일반적으로 응용 프로그램의 특정 부분에서 수행 해야 하는 *상황* 에 맞는 계산이 있습니다. 컨텍스트를 구분 하는 코드를 작성 하는 것이 더 어려울 수 있습니다 .이 작업을 수행 하는 것을 방지 하기 위해 추상화 없이 지정 된 컨텍스트 외부에서 계산을 "누수" 하는 것이 이러한 추상화는 종종 직접 작성 하기가 쉽지 않으므로 **계산 식**이라고 하 F# 는 일반화 된 방법이 있습니다.

계산 식은 상황에 맞는 계산을 인코딩하기 위한 일관 된 구문 및 추상화 모델을 제공 합니다.

모든 계산 식은 *작성기* 형식에 의해 지원 됩니다. 작성기 유형은 계산 식에 사용할 수 있는 작업을 정의 합니다. 사용자 지정 계산 식을 만드는 방법을 보여 주는 [새 계산 식 형식 만들기](computation-expressions.md#creating-a-new-type-of-computation-expression)를 참조 하세요.

### <a name="syntax-overview"></a>구문 개요

모든 계산 식의 형식은 다음과 같습니다.

```fsharp
builder-expr { cexper }
```

여기서 `builder-expr` 는 계산 식을 정의 하는 작성기 형식의 이름이 고 `cexper` 는 계산 식의 식 본문입니다. 예를 `async` 들어 계산 식 코드는 다음과 같습니다.

```fsharp
let fetchAndDownload url =
    async {
        let! data = downloadData url

        let processedData = processData data

        return processedData
    }
```

이전 예제와 같이 계산 식 내에서 사용할 수 있는 특별 한 추가 구문이 있습니다. 계산 식에는 다음과 같은 식 형식이 가능 합니다.

```fsharp
expr { let! ... }
expr { do! ... }
expr { yield ... }
expr { yield! ... }
expr { return ... }
expr { return! ... }
expr { match! ... }
```

이러한 각 키워드와 기타 표준 F# 키워드는 지원 빌더 유형에 정의 된 경우 계산 식 에서만 사용할 수 있습니다. 이에 대 한 유일한 예외 `match!`는를 `let!` 사용 하 고 그 다음에 패턴 일치를 사용 하 여 결과에 sugar는 것입니다.

작성기 형식은 계산 식의 조각이 결합 되는 방법을 제어 하는 특수 메서드를 정의 하는 개체입니다. 즉, 해당 메서드는 계산 식이 동작 하는 방식을 제어 합니다. 작성기 클래스를 설명 하는 또 다른 방법은 루프 및 바인딩과 같은 여러 F# 구문의 작업을 사용자 지정할 수 있다는 것입니다.

### `let!`

키워드 `let!` 는 다른 계산 식에 대 한 호출 결과를 이름에 바인딩합니다.

```fsharp
let doThingsAsync url =
    async {
        let! data = getDataAsync url
        ...
    }
```

를 사용 `let`하 여 계산 식에 대 한 호출을 바인딩하는 경우 계산 식의 결과를 얻을 수 없습니다. 대신 계산 식에 대 한 계산 되지 *않은 호출 값* 을 바인딩 했습니다. 를 `let!` 사용 하 여 결과에 바인딩합니다.

`let!`는 작성기 형식의 `Bind(x, f)` 멤버에 의해 정의 됩니다.

### `do!`

키워드 `do!` `unit` 는`Zero` 형식 (작성기의 멤버에 의해 정의 됨)을 반환 하는 계산 식을 호출 하기 위한 것입니다.

```fsharp
let doThingsAsync data url =
    async {
        do! submitData data url
        ...
    }
```

[비동기 워크플로의](asynchronous-workflows.md)경우이 형식은 `Async<unit>`입니다. 다른 계산 식의 경우 형식은이 될 수 `CExpType<unit>`있습니다.

`do!`는 작성기 형식의 `Bind(x, f)` 멤버에 의해 정의 됩니다. 여기서 `f` 는을 `unit`생성 합니다.

### `yield`

키워드 `yield` 는 계산 식에서 값을 반환 하 여 <xref:System.Collections.Generic.IEnumerable%601>로 사용할 수 있도록 하는 데 사용 됩니다.

```fsharp
let squares =
    seq {
        for i in 1..10 do
            yield i * i
    }

for sq in squares do
    printfn "%d" sq
```

[ C#에서 yield 키워드 ](../../csharp/language-reference/keywords/yield.md)와 마찬가지로 계산 식의 각 요소는 반복 될 때 다시 생성 됩니다.

`yield`는 작성기 형식의 `Yield(x)` 멤버에 의해 정의 됩니다. 여기서 `x` 은 다시 생성할 항목입니다.

### `yield!`

키워드 `yield!` 는 계산 식에서 값의 컬렉션을 평면화 하는 데 사용할 수 있습니다.

```fsharp
let squares =
    seq {
        for i in 1..3 -> i * i
    }

let cubes =
    seq {
        for i in 1..3 -> i * i * i
    }

let squaresAndCubes =
    seq {
        yield! squares
        yield! cubes
    }

printfn "%A" squaresAndCubes // Prints - 1; 4; 9; 1; 8; 27
```

평가 되는 경우에 의해 `yield!` 호출 되는 계산 식에서 해당 항목이 하나씩 다시 생성 되어 결과를 평면화 합니다.

`yield!`는 작성기 형식의 `YieldFrom(x)` 멤버에 의해 정의 됩니다. 여기서 `x` 는 값의 컬렉션입니다.

### `return`

키워드 `return` 는 계산 식에 해당 하는 형식의 값을 래핑합니다. 를 사용 하 `yield`는 계산 식 외에도 계산 식을 "완료" 하는 데 사용 됩니다.

```fsharp
let req = // 'req' is of type is 'Async<data>'
    async {
        let! data = fetch url
        return data
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

`return`는 작성기 형식의 `Return(x)` 멤버에 의해 정의 됩니다. 여기서 `x` 은 래핑할 항목입니다.

### `return!`

키워드 `return!` 는 계산 식의 값을 인식 하 고 해당 결과를 계산 식에 해당 하는 형식으로 래핑합니다.

```fsharp
let req = // 'req' is of type is 'Async<data>'
    async {
        return! fetch url
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

`return!`는 작성기 형식의 `ReturnFrom(x)` 멤버에 의해 정의 됩니다. 여기서 `x` 는 다른 계산 식입니다.

### `match!`

F# 4.5`match!` 부터 키워드를 사용 하면 결과에 대해 다른 계산 식과 패턴 일치에 대 한 호출을 인라인 할 수 있습니다.

```fsharp
let doThingsAsync url =
    async {
        match! callService url with
        | Some data -> ...
        | None -> ...
    }
```

를 사용 `match!`하 여 계산 식을 호출 하는 경우와 같은 `let!`호출의 결과를 인식 합니다. 이는 결과가 [선택적인](options.md)인 계산 식을 호출할 때 주로 사용 됩니다.

## <a name="built-in-computation-expressions"></a>기본 제공 계산 식

핵심 F# 라이브러리는 세 가지 기본 제공 계산 식을 정의 합니다. [시퀀스 식](sequences.md), [비동기 워크플로](asynchronous-workflows.md)및 [쿼리 식](query-expressions.md)입니다.

## <a name="creating-a-new-type-of-computation-expression"></a>새 계산 식 형식 만들기

작성기 클래스를 만들고 클래스에 특정 특수 메서드를 정의 하 여 계산 식의 특성을 정의할 수 있습니다. 작성기 클래스는 다음 표에 나열 된 대로 메서드를 선택적으로 정의할 수 있습니다.

다음 표에서는 workflow builder 클래스에서 사용할 수 있는 메서드에 대해 설명 합니다.

|**메서드**|**일반적인 서명**|**설명**|
|----|----|----|
|`Bind`|`M<'T> * ('T -> M<'U>) -> M<'U>`|계산 식 `let!` 에서 `do!` 및에 대해 호출 됩니다.|
|`Delay`|`(unit -> M<'T>) -> M<'T>`|계산 식을 함수로 래핑합니다.|
|`Return`|`'T -> M<'T>`|계산 식 `return` 에서에 대해 호출 됩니다.|
|`ReturnFrom`|`M<'T> -> M<'T>`|계산 식 `return!` 에서에 대해 호출 됩니다.|
|`Run`|`M<'T> -> M<'T>` 또는<br /><br />`M<'T> -> 'T`|계산 식을 실행 합니다.|
|`Combine`|`M<'T> * M<'T> -> M<'T>` 또는<br /><br />`M<unit> * M<'T> -> M<'T>`|계산 식의 시퀀싱을 위해 호출 됩니다.|
|`For`|`seq<'T> * ('T -> M<'U>) -> M<'U>` 또는<br /><br />`seq<'T> * ('T -> M<'U>) -> seq<M<'U>>`|계산 식 `for...do` 의 식에 대해 호출 됩니다.|
|`TryFinally`|`M<'T> * (unit -> unit) -> M<'T>`|계산 식 `try...finally` 의 식에 대해 호출 됩니다.|
|`TryWith`|`M<'T> * (exn -> M<'T>) -> M<'T>`|계산 식 `try...with` 의 식에 대해 호출 됩니다.|
|`Using`|`'T * ('T -> M<'U>) -> M<'U> when 'U :> IDisposable`|계산 식 `use` 의 바인딩에 대해 호출 됩니다.|
|`While`|`(unit -> bool) * M<'T> -> M<'T>`|계산 식 `while...do` 의 식에 대해 호출 됩니다.|
|`Yield`|`'T -> M<'T>`|계산 식 `yield` 의 식에 대해 호출 됩니다.|
|`YieldFrom`|`M<'T> -> M<'T>`|계산 식 `yield!` 의 식에 대해 호출 됩니다.|
|`Zero`|`unit -> M<'T>`|계산 식에서 `else` 식의 `if...then` 빈 분기에 대해 호출 됩니다.|
|`Quote`|`Quotations.Expr<'T> -> Quotations.Expr<'T>`|계산 식이 `Run` 멤버에 따옴표로 전달 됨을 나타냅니다. 계산의 모든 인스턴스를 따옴표로 변환 합니다.|

작성기 클래스의 여러 메서드는 `M<'T>` 생성자를 사용 하 고 반환 합니다 .이는 일반적으로 결합 되는 계산의 종류 ( `Async<'T>` 예: 비동기 워크플로 및 `Seq<'T>` )에 해당 하는 개별적으로 정의 된 형식입니다. 시퀀스 워크플로의 경우. 이러한 메서드의 시그니처를 사용 하 여 서로 결합 하 고 중첩할 수 있으므로 한 구문에서 반환 된 워크플로 개체를 다음에 전달할 수 있습니다. 컴파일러는 계산 식을 구문 분석할 때 앞의 테이블에 있는 메서드와 계산 식의 코드를 사용 하 여 식을 일련의 중첩 된 함수 호출로 변환 합니다.

중첩 식은 다음과 같은 형식입니다.

```fsharp
builder.Run(builder.Delay(fun () -> {| cexpr |}))
```

위의 코드에서 및 `Run` `Delay` 에 대 한 호출은 계산 식 작성기 클래스에서 정의 되지 않은 경우 생략 됩니다. 여기에서로 `{| cexpr |}`표시 된 계산 식의 본문은 다음 표에 설명 된 번역에 의해 작성기 클래스의 메서드와 관련 된 호출로 변환 됩니다. 계산 식은 `{| cexpr |}` 이러한 번역에 따라 재귀적으로 정의 됩니다. `expr` 여기서은 F# 식 이며 `cexpr` 계산 식입니다.

|식|이동|
|----------|-----------|
|<code>{ let binding in cexpr }</code>|<code>let binding in {&#124; cexpr &#124;}</code>|
|<code>{ let! pattern = expr in cexpr }</code>|<code>builder.Bind(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{ do! expr in cexpr }</code>|<code>builder.Bind(expr, (fun () -> {&#124; cexpr &#124;}))</code>|
|<code>{ yield expr }</code>|`builder.Yield(expr)`|
|<code>{ yield! expr }</code>|`builder.YieldFrom(expr)`|
|<code>{ return expr }</code>|`builder.Return(expr)`|
|<code>{ return! expr }</code>|`builder.ReturnFrom(expr)`|
|<code>{ use pattern = expr in cexpr }</code>|<code>builder.Using(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{ use! value = expr in cexpr }</code>|<code>builder.Bind(expr, (fun value -> builder.Using(value, (fun value -> { cexpr }))))</code>|
|<code>{ if expr then cexpr0 &#124;}</code>|<code>if expr then { cexpr0 } else binder.Zero()</code>|
|<code>{ if expr then cexpr0 else cexpr1 &#124;}</code>|<code>if expr then { cexpr0 } else { cexpr1 }</code>|
|<code>{ match expr with &#124; pattern_i -> cexpr_i }</code>|<code>match expr with &#124; pattern_i -> { cexpr_i }</code>|
|<code>{ for pattern in expr do cexpr }</code>|<code>builder.For(enumeration, (fun pattern -> { cexpr }))</code>|
|<code>{ for identifier = expr1 to expr2 do cexpr }</code>|<code>builder.For(enumeration, (fun identifier -> { cexpr }))</code>|
|<code>{ while expr do cexpr }</code>|<code>builder.While(fun () -> expr, builder.Delay({ cexpr }))</code>|
|<code>{ try cexpr with &#124; pattern_i -> expr_i }</code>|<code>builder.TryWith(builder.Delay({ cexpr }), (fun value -> match value with &#124; pattern_i -> expr_i &#124; exn -> reraise exn)))</code>|
|<code>{ try cexpr finally expr }</code>|<code>builder.TryFinally(builder.Delay( { cexpr }), (fun () -> expr))</code>|
|<code>{ cexpr1; cexpr2 }</code>|<code>builder.Combine({ cexpr1 }, { cexpr2 })</code>|
|<code>{ other-expr; cexpr }</code>|<code>expr; { cexpr }</code>|
|<code>{ other-expr }</code>|`expr; builder.Zero()`|

위의 표에서 `other-expr` 는 표에 나열 되지 않은 식에 대해 설명 합니다. 작성기 클래스는 모든 메서드를 구현할 필요가 없으며 앞의 표에 나열 된 모든 번역을 지원 합니다. 구현 되지 않은 구문은 해당 형식의 계산 식에서 사용할 수 없습니다. 예를 들어 계산 식에서 `use` 키워드를 지원 하지 않으려면 작성기 클래스에서의 `Use` 정의를 생략할 수 있습니다.

다음 코드 예제에서는 한 번에 하나의 단계를 평가할 수 있는 일련의 단계로 계산을 캡슐화 하는 계산 식을 보여 줍니다. 구분 된 공용 구조체 형식인 `OkOrException`는 지금까지 계산 된 식의 오류 상태를 인코딩합니다. 이 코드에서는 몇 가지 일반적인 패턴을 보여 줍니다. 몇 가지 일반적인 패턴은 몇 가지 작성기 메서드의 상용구 구현과 같이 계산 식에서 사용할 수 있습니다.

```fsharp
// Computations that can be run step by step
type Eventually<'T> =
    | Done of 'T
    | NotYetDone of (unit -> Eventually<'T>)

module Eventually =
    // The bind for the computations. Append 'func' to the
    // computation.
    let rec bind func expr =
        match expr with
        | Done value -> func value
        | NotYetDone work -> NotYetDone (fun () -> bind func (work()))

    // Return the final value wrapped in the Eventually type.
    let result value = Done value

    type OkOrException<'T> =
        | Ok of 'T
        | Exception of System.Exception

    // The catch for the computations. Stitch try/with throughout
    // the computation, and return the overall result as an OkOrException.
    let rec catch expr =
        match expr with
        | Done value -> result (Ok value)
        | NotYetDone work ->
            NotYetDone (fun () ->
                let res = try Ok(work()) with | exn -> Exception exn
                match res with
                | Ok cont -> catch cont // note, a tailcall
                | Exception exn -> result (Exception exn))

    // The delay operator.
    let delay func = NotYetDone (fun () -> func())

    // The stepping action for the computations.
    let step expr =
        match expr with
        | Done _ -> expr
        | NotYetDone func -> func ()

    // The rest of the operations are boilerplate.
    // The tryFinally operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryFinally expr compensation =
        catch (expr)
        |> bind (fun res -> 
            compensation();
            match res with
            | Ok value -> result value
            | Exception exn -> raise exn)

    // The tryWith operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryWith exn handler =
        catch exn
        |> bind (function Ok value -> result value | Exception exn -> handler exn)

    // The whileLoop operator.
    // This is boilerplate in terms of "result" and "bind".
    let rec whileLoop pred body =
        if pred() then body |> bind (fun _ -> whileLoop pred body)
        else result ()

    // The sequential composition operator.
    // This is boilerplate in terms of "result" and "bind".
    let combine expr1 expr2 =
        expr1 |> bind (fun () -> expr2)

    // The using operator.
    let using (resource: #System.IDisposable) func =
        tryFinally (func resource) (fun () -> resource.Dispose())

    // The forLoop operator.
    // This is boilerplate in terms of "catch", "result", and "bind".
    let forLoop (collection:seq<_>) func =
        let ie = collection.GetEnumerator()
        tryFinally 
            (whileLoop 
                (fun () -> ie.MoveNext()) 
                (delay (fun () -> let value = ie.Current in func value)))
            (fun () -> ie.Dispose())

// The builder class.
type EventuallyBuilder() =
    member x.Bind(comp, func) = Eventually.bind func comp
    member x.Return(value) = Eventually.result value
    member x.ReturnFrom(value) = value
    member x.Combine(expr1, expr2) = Eventually.combine expr1 expr2
    member x.Delay(func) = Eventually.delay func
    member x.Zero() = Eventually.result ()
    member x.TryWith(expr, handler) = Eventually.tryWith expr handler
    member x.TryFinally(expr, compensation) = Eventually.tryFinally expr compensation
    member x.For(coll:seq<_>, func) = Eventually.forLoop coll func
    member x.Using(resource, expr) = Eventually.using resource expr

let eventually = new EventuallyBuilder()

let comp = eventually {
    for x in 1..2 do
        printfn " x = %d" x
    return 3 + 4 }

// Try the remaining lines in F# interactive to see how this
// computation expression works in practice.
let step x = Eventually.step x

// returns "NotYetDone <closure>"
comp |> step

// prints "x = 1"
// returns "NotYetDone <closure>"
comp |> step |> step

// prints "x = 1"
// prints "x = 2"
// returns "Done 7"
comp |> step |> step |> step |> step 
```

계산 식에는 식이 반환 하는 기본 형식이 있습니다. 기본 형식은 계산 된 결과 또는 수행 될 수 있는 지연 계산을 나타내거나 일부 형식의 컬렉션을 반복 하는 방법을 제공할 수 있습니다. 이전 예제에서는 기본 형식이 **결국**였습니다. 시퀀스 식의 경우 기본 형식은 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>입니다. 쿼리 식의 경우 기본 형식은 <xref:System.Linq.IQueryable?displayProperty=nameWithType>입니다. 비동기 워크플로의 경우 기본 형식은 [`Async`](https://msdn.microsoft.com/library/03eb4d12-a01a-4565-a077-5e83f17cf6f7)입니다. 개체 `Async` 는 결과를 계산 하기 위해 수행할 작업을 나타냅니다. 예를 들어를 호출 [`Async.RunSynchronously`](https://msdn.microsoft.com/library/0a6663a9-50f2-4d38-8bf3-cefd1a51fd6b) 하 여 계산을 실행 하 고 결과를 반환 합니다.

## <a name="custom-operations"></a>사용자 지정 작업

계산 식에 대 한 사용자 지정 작업을 정의 하 고 계산 식에서 사용자 지정 작업을 연산자로 사용할 수 있습니다. 예를 들어 쿼리 식에 쿼리 연산자를 포함할 수 있습니다. 사용자 지정 작업을 정의 하는 경우 계산 식의 메서드에 Yield 및를 정의 해야 합니다. 사용자 지정 작업을 정의 하려면 계산 식의 작성기 클래스에 배치한 다음를 [`CustomOperationAttribute`](https://msdn.microsoft.com/library/199f3927-79df-484b-ba66-85f58cc49b19)적용 합니다. 이 특성은 사용자 지정 작업에 사용 되는 이름인 문자열을 인수로 사용 합니다. 이 이름은 계산 식의 여는 중괄호의 시작 부분에서 범위에 제공 됩니다. 따라서이 블록에서 사용자 지정 작업과 이름이 같은 식별자를 사용 하면 안 됩니다. 예를 들어 쿼리 식에서 또는 `all` `last` 와 같은 식별자를 사용 하지 않습니다.

### <a name="extending-existing-builders-with-new-custom-operations"></a>새 사용자 지정 작업으로 기존 작성기 확장

작성기 클래스가 이미 있는 경우이 작성기 클래스 외부에서 해당 사용자 지정 작업을 확장할 수 있습니다. 모듈에서 확장을 선언 해야 합니다. 네임 스페이스는 동일한 파일 및 형식이 정의 된 동일한 네임 스페이스 선언 그룹을 제외 하 고 확장 멤버를 포함할 수 없습니다.

다음 예제에서는 기존 `Microsoft.FSharp.Linq.QueryBuilder` 클래스의 확장을 보여 줍니다.

```fsharp
type Microsoft.FSharp.Linq.QueryBuilder with

    [<CustomOperation("existsNot")>]
    member __.ExistsNot (source: QuerySource<'T, 'Q>, predicate) =
        Enumerable.Any (source.Source, Func<_,_>(predicate)) |> not
```

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [비동기 워크플로](asynchronous-workflows.md)
- [시퀀스](https://msdn.microsoft.com/library/6b773b6b-9c9a-4af8-bd9e-d96585c166db)
- [쿼리 식](query-expressions.md)
