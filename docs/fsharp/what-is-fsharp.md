---
title: F#이란
description: F# 프로그래밍 언어와 F# 프로그래밍이 어떤 것인지 알아봅니다. 풍부한 데이터 유형과 기능, 이들이 함께 어울리는 방법을 알아봅니다.
ms.date: 08/03/2018
ms.openlocfilehash: 3cba509f59a8e81e1a0264de7451e9d80304d768
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332729"
---
# <a name="what-is-f"></a>F\#이란

F#은 정확하고 유지 보수가 쉬운 코드를 만들 수 있는 함수형 프로그래밍 언어입니다.

F# 프로그래밍은 주로 자동으로 형식이 유추되고 일반화되는 형식 및 함수를 정의하는 것을 포함합니다. 따라서 프로그래밍의 세부 사항보다는 문제 도메인에 집중하고 데이터를 조작하는 데 집중할 수 있습니다.

```fsharp
open System // Gets access to functionality in System namespace.

// Defines a function that takes a name and produces a greeting.
let getGreeting name =
    sprintf "Hello, %s! Isn't F# great?" name

[<EntryPoint>]
let main args =
    // Defines a list of names
    let names = [ "Don"; "Julia"; "Xi" ]

    // Prints a greeting for each name!
    names
    |> List.map getGreeting
    |> List.iter (fun greeting -> printfn "%s" greeting)

    0
```

F#은 다음과 같은 다양한 기능이 있습니다.

* 간단한 구문
* 기본적으로 변경 불가능
* 타입 추론 및 자동화된 일반화
* 일급 함수
* 강력한 데이터 타입
* 패턴 매칭
* 비동기 프로그래밍

전체 기능은 [F# 언어 참조](./language-reference/index.md)에 문서화되어 있습니다.

## <a name="rich-data-types"></a>다양한 데이터 형식

[Records](./language-reference/records.md) 및 [Discriminated Unions](./language-reference/discriminated-unions.md)와 같은 데이터 타입을 사용하면 복잡한 데이터와 도메인을 표현할 수 있습니다.

```fsharp
// Group data with Records
type SuccessfulWithdrawal = {
    Amount: decimal
    Balance: decimal
}

type FailedWithdrawal = {
    Amount: decimal
    Balance: decimal
    IsOverdraft: bool
}

// Use discriminated unions to represent data of 1 or more forms
type WithdrawalResult =
    | Success of SuccessfulWithdrawal
    | InsufficientFunds of FailedWithdrawal
    | CardExpired of System.DateTime
    | UndisclosedFailure
```

F# Record와 Discriminated Union는 기본적으로 null이 아니며 변경 불가능하고 비교할 수 있으므로 아주 쉽게 사용할 수 있습니다.

## <a name="enforced-correctness-with-functions-and-pattern-matching"></a>함수 및 패턴 매칭을 통한 정확성 강화

F# 함수는 실제로 사용할 때 선언하기 쉽고 강력합니다. [패턴 일치](./language-reference/pattern-matching.md)와 함께 사용하면 컴파일러에 의해 적용되는 정확한 동작을 정의할 수 있습니다.

```fsharp
// Returns a WithdrawalResult
let withdrawMoney amount = // Implementation elided

let handleWithdrawal amount =
    let w = withdrawMoney amount

    // The F# compiler enforces accounting for each case!
    match w with
    | Success s -> printfn "Successfully withdrew %f" s.Amount
    | InsufficientFunds f -> printfn "Failed: balance is %f" f.Balance
    | CardExpired d -> printfn "Failed: card expired on %O" d
    | UndisclosedFailure -> printfn "Failed: unknown :("
```

F# 함수는 또한 일급 클래스이며, 매개변수로 전달되고 다른 함수에서 반환될 수 있습니다.

## <a name="functions-to-define-operations-on-objects"></a>객체에 대한 연산을 정의하는 함수

F#은 객체를 완벽하게 지원합니다. 객체는 데이터와 기능을 혼합해야 할 때 유용한 데이터 타입입니다.

```fsharp
type Set<'T when 'T: comparison>(elements: seq<'T>) =
    member s.IsEmpty = // Implementation elided
    member s.Contains (value) =// Implementation elided
    member s.Add (value) = // Implementation elided
    // ...
    // Further Implementation elided
    // ...
    interface IEnumerable<‘T>
    interface IReadOnlyCollection<‘T>

module Set =
    let isEmpty (set: Set<'T>) = set.IsEmpty

    let contains element (set: Set<'T>) = set.Contains(element)

    let add value (set: Set<'T>) = set.Add(value)
```

F#에서는 객체 지향적 코드를 작성하는 대신 함수를 조작하는 데 필요한 다른 데이터 타입으로 객체를 처리하는 코드를 작성합니다. [제네릭 인터페이스](./language-reference/interfaces.md), [객체 식](./language-reference/object-expressions.md) 및 [멤버](./language-reference/members/index.md)의 적절한 사용과 같은 기능은 대부분의 F# 프로그램에서 일반적입니다.

## <a name="next-steps"></a>다음 단계

더 많은 F# 기능은 [F# 둘러보기](tour.md)를 확인하세요.
