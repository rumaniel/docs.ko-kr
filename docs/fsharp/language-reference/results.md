---
title: 결과
description: 사용 하는 방법을 알아봅니다는 F# 오류 코드를 작성할 수 있도록 'Result'를 입력 합니다.
ms.date: 04/24/2017
ms.openlocfilehash: 36f60df8a2991c1d318e4921af6c9e89a0156918
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645318"
---
# <a name="results"></a>결과

부터 F# 4.1 있습니다는 `Result<'T,'TFailure>` 종류입니다. 구성할 수 있는 오류 코드를 작성에 사용할 수 있습니다.

## <a name="syntax"></a>구문

```fsharp
// The definition of Result in FSharp.Core
[<StructuralEquality; StructuralComparison>]
[<CompiledName("FSharpResult`2")>]
[<Struct>]
type Result<'T,'TError> = 
    | Ok of ResultValue:'T 
    | Error of ErrorValue:'TError
```

## <a name="remarks"></a>설명

결과 형식은 [구조체 구분 된 공용 구조체](discriminated-unions.md#struct-discriminated-unions)에 또 다른 기능은에 도입 F# 4.1 합니다.  구조적 같음 의미 체계 여기에 적용 됩니다.

합니다 `Result` 유형은 monadic 오류 처리에는 라 불리는 일반적으로 사용 됩니다 [철도 지향 프로그래밍](https://swlaschin.gitbooks.io/fsharpforfunandprofit/content/posts/recipe-part2.html) 내에서 F# 커뮤니티입니다.  다음 간단한 예제에서는이 방법을 보여 줍니다.

```fsharp
// Define a simple type which has fields that can be validated
type Request = 
    { Name: string
      Email: string }

// Define some logic for what defines a valid name.
//
// Generates a Result which is an Ok if the name validates;
// otherwise, it generates a Result which is an Error.
let validateName req =
    match req.Name with
    | null -> Error "No name found."
    | "" -> Error "Name is empty."
    | "bananas" -> Error "Bananas is not a name."
    | _ -> Ok req

// Similarly, define some email validation logic.
let validateEmail req =
    match req.Email with
    | null -> Error "No email found."
    | "" -> Error "Email is empty."
    | s when s.EndsWith("bananas.com") -> Error "No email from bananas.com is allowed."
    | _ -> Ok req

let validateRequest reqResult =
    reqResult 
    |> Result.bind validateName
    |> Result.bind validateEmail

let test() = 
    // Now, create a Request and pattern match on the result.
    let req1 = { Name = "Phillip"; Email = "phillip@contoso.biz" }
    let res1 = validateRequest (Ok req1)
    match res1 with
    | Ok req -> printfn "My request was valid! Name: %s Email %s" req.Name req.Email
    | Error e -> printfn "Error: %s" e
    // Prints: "My request was valid!  Name: Phillip Email: phillip@consoto.biz"

    let req2 = { Name = "Phillip"; Email = "phillip@bananas.com" }
    let res2 = validateRequest (Ok req2)
    match res2 with
    | Ok req -> printfn "My request was valid! Name: %s Email %s" req.Name req.Email
    | Error e -> printfn "Error: %s" e
    // Prints: "Error: No email from bananas.com is allowed."

test()
```

알 수 있듯이 무척 쉽습니다 모두 반환 하려면 할 경우 다양 한 유효성 검사 함수 함께 연결 하는 `Result`합니다.  수 있도록 필요에 따라 구성할 수 있는 작은 조각으로 다음과 같은 기능을 중단할 수이 있습니다.  이 역시의 추가 가치 *적용* 사용 [패턴 일치](pattern-matching.md) 끝에 일련의 유효성 검사, 결과적으로 적용 하는 더 높은 수준의 프로그램 정확성을 합니다.

## <a name="see-also"></a>참고자료

- [구별된 공용 구조체](discriminated-unions.md)
- [패턴 일치](pattern-matching.md)
