---
title: 값 옵션
description: 에 대해 알아봅니다는 F# 옵션 종류의 구조체 버전인 값 옵션 종류입니다.
ms.date: 02/06/2019
ms.openlocfilehash: e1036c83189c853b3704d94ca245e4818acc98c1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61982581"
---
# <a name="value-options"></a>값 옵션

값 옵션 형식 F# 다음 두 경우 저장할 때 사용 됩니다.

1. 시나리오에 적합 한 [ F# 옵션](options.md)합니다.
2. 구조체를 사용 하는 시나리오의 성능 이점을 제공 합니다.

일부 성능에 민감한 시나리오는 "해결" 구조체를 사용 하 여 합니다. 참조 형식 대신 사용 하는 경우 복사 하는 추가 비용을 고려해 야 합니다. 그러나 많은 F# 프로그램 일반적으로 실행 부하 과다 경로 통해 이동 하는 다양 한 선택적 형식을 인스턴스화하고 이러한 경우 구조체 수 종종 성능이 향상 전체 프로그램의 수명 동안.

## <a name="definition"></a>정의

값 옵션으로 정의 됩니다는 [구분 된 공용 구조체 구조체](discriminated-unions.md#struct-discriminated-unions) 참조 옵션 형식과 비슷한입니다. 해당 정의가 이러한 방식으로 생각할 수 있습니다.

```fsharp
[<StructuralEquality; StructuralComparison>]
[<Struct>]
type ValueOption<'T> =
    | ValueNone
    | ValueSome of 'T
```

구조적 같음 및 비교 값 옵션이 따릅니다. 주요 차이점은는 컴파일된 이름, 형식 이름 및 경우 대/소문자가 모든 이라는 것을 나타내는 값 형식입니다.

## <a name="using-value-options"></a>값 옵션을 사용 하 여

값 옵션 처럼 사용 됩니다 [옵션](options.md)합니다. `ValueSome` 값이 있는지를 나타내는 데 사용 되 고 `ValueNone` 값 없을 때 사용 됩니다.

```fsharp
let tryParseDateTime (s: string) =
    match System.DateTime.TryParse(s) with
    | (true, dt) -> ValueSome dt
    | (false, _) -> ValueNone

let possibleDateString1 = "1990-12-25"
let possibleDateString2 = "This is not a date"

let result1 = tryParseDateTime possibleDateString1
let result2 = tryParseDateTime possibleDateString2

match (result1, result2) with
| ValueSome d1, ValueSome d2 -> printfn "Both are dates!"
| ValueSome d1, ValueNone -> printfn "Only the first is a date!"
| ValueNone, ValueSome d2 -> printfn "Only the second is a date!"
| ValueNone, ValueNone -> printfn "None of them are dates!"
```

와 마찬가지로 [옵션](options.md)를 반환 하는 함수에 대 한 명명 규칙 `ValueOption` 사용 하 여 접두사를 지정 하는 `try`합니다.

## <a name="value-option-properties-and-methods"></a>값 옵션 속성 및 메서드

지금은 값 옵션에 대 한 하나의 속성은: `Value`합니다. <xref:System.InvalidOperationException> 값이 현재가이 속성을 호출할 때 발생 합니다.

## <a name="value-option-functions"></a>값 옵션 함수

값 옵션에 대 한 하나의 모듈 바인딩된 함수는 현재 `defaultValueArg`:

```fsharp
val defaultValueArg : arg:'T voption -> defaultValue:'T -> 'T 
```

와 마찬가지로 합니다 `defaultArg` 함수를 `defaultValueArg` 경우 지정 된 값 옵션의 기본 값을 반환 존재 않으면 그렇지 않은 경우 지정된 된 기본값을 반환 합니다.

이때 값 옵션에 대 한 다른 모듈 바인딩된 함수가 없는 있습니다.

## <a name="see-also"></a>참고자료

- [옵션](options.md)
