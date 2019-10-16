---
title: 익명 기록
description: 구문을 사용 하 여 익명 레코드를 사용 하 여 데이터를 조작 하는 언어 기능을 사용 하는 방법에 알아봅니다.
ms.date: 06/12/2019
ms.openlocfilehash: e576210d4fb76ccfd09f8feb157ef4542aa94ccf
ms.sourcegitcommit: c4dfe37032c64a1fba2cc3d5947550d79f95e3b5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/13/2019
ms.locfileid: "67041807"
---
# <a name="anonymous-records"></a>익명 기록

익명 레코드는 사용 하기 전에 선언 하지 않아도 되는 명명 된 값의 간단한 집계입니다. 구조체 또는 참조 형식으로 선언할 수 있습니다. 기본적으로 참조 형식이 됩니다.

## <a name="syntax"></a>구문

다음 예제에서는 익명 레코드 구문을 보여 줍니다. 항목으로 구분 된 `[item]` 는 선택 사항입니다.

```fsharp
// Construct an anonymous record
let value-name = [struct] {| Label1: Type1; Label2: Type2; ...|}

// Use an anonymous record as a type parameter
let value-name = Type-Name<[struct] {| Label1: Type1; Label2: Type2; ...|}>

// Define a parameter with an anonymous record as input
let function-name (arg-name: [struct] {| Label1: Type1; Label2: Type2; ...|}) ...
```

## <a name="basic-usage"></a>기본 사용

익명 레코드는 가장 생각할 F# 레코드 종류는 인스턴스화 앞 선언할 필요가 없습니다.

예를 들어, 다음 함수를 사용 하 여 상호 작용할 수는 방법을 생성 하는 익명 레코드를:

```fsharp

open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

다음 예제에서는 사용 하 여 이전에 확장을 `printCircleStats` 입력으로 익명 레코드를 사용 하는 함수:

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let printCircleStats r (stats: {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

호출 `printCircleStats` 입력된 형식이 컴파일하는 데 실패 하는 대로 동일한 "shape"이 없는 레코드 익명 형식을 사용 하 여:

```fsharp
printCircleStats r {| Diameter = 2.0; Area = 4.0; MyCircumference = 12.566371 |}
// Two anonymous record types have mismatched sets of field names
// '["Area"; "Circumference"; "Diameter"]' and '["Area"; "Diameter"; "MyCircumference"]'
```

## <a name="struct-anonymous-records"></a>익명 구조체 레코드

선택적 구조체와 익명 레코드를 정의할 수도 있습니다 `struct` 키워드입니다. 다음 예제에서는 생성 하 고 구조체 익명 레코드를 사용 하 여 이전과 보강 합니다.

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    // Note that the keyword comes before the '{| |}' brace pair
    struct {| Area = a; Circumference = c; Diameter = d |}

// the 'struct' keyword also comes before the '{| |}' brace pair when declaring the parameter type
let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

### <a name="structness-inference"></a>Structness 유추

익명 구조체 레코드도 허용 "structness 유추" 지정할 필요가 없습니다 여기서는 `struct` 호출 사이트에서 키워드입니다. 이 예제에서는 elide를 `struct` 키워드를 호출할 때 `printCircleStats`:

```fsharp

let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

printCircleStats r {| Area = 4.0; Circumference = 12.6; Diameter = 12.6 |}
```

반대 패턴-지정 `struct` 입력된 형식이 익명 구조체 레코드-없는 경우 컴파일하는 데 실패 합니다.

## <a name="embedding-anonymous-records-within-other-types"></a>다른 형식 내에서 익명 레코드를 포함합니다.

선언 하는 것이 유용 [구별 된 공용 구조체](discriminated-unions.md) 레코드가 있는 경우. 하지만 상호 재귀 유형도 레코드의 데이터를 동일한 구별 된 공용 구조체 형식 경우 정의 해야 합니다. 익명 레코드를 사용 하 여이 제한을 피할 수 있습니다. 예제는 다음 위로 가져가면 해당 패턴 일치 형식 및 함수:

```fsharp
type FullName = { FirstName: string; LastName: string }

// Note that using a named for Manager and Executive would require mutually recursive definitions.
type Employee =
    | Engineer of FullName
    | Manager of {| Name: FullName; Reports: Employee list |}
    | Executive of {| Name: FullName; Reports: Employee list; Assistant: Employee |}

let getFirstName e =
    match e with
    | Engineer fullName -> fullName.FirstName
    | Manager m -> m.Name.FirstName
    | Executive ex -> ex.Name.FirstName
```

## <a name="copy-and-update-expressions"></a>복사한 식 업데이트

익명 기록 구문을 사용 하 여 지원 [복사 하 고 식을 업데이트](copy-and-update-record-expressions.md)합니다. 예를 들어, 어떻게 기존 1의 복사 하는 익명 레코드의 새 인스턴스를 생성할 수 있습니다 다음은 데이터:

```fsharp
let data = {| X = 1; Y = 2 |}
let data' = {| data with Y = 3 |}
```

그러나 명명 된 레코드와 달리 익명 레코드 수 복사를 사용 하 여 완전히 다른 폼을 생성 하 고 식을 업데이트 합니다. 다음 예제에서는 이전 예제에서 동일한 익명 레코드를 사용 및 새 익명 레코드를 확장 합니다.

```fsharp
let data = {| X = 1; Y = 2 |}
let expandedData = {| data with Z = 3 |} // Gives {| X=1; Y=2; Z=3 |}
```

명명 된 레코드 인스턴스의 익명 레코드를 생성 하는 것도 가능 합니다.

```fsharp
type R = { X: int }
let data = { X = 1 }
let data' = {| data with Y = 2 |} // Gives {| X=1; Y=2 |}
```

또한 익명 레코드 참조 및 구조체에서 데이터를 복사할 수 있습니다.

```fsharp
// Copy data from a reference record into a struct anonymous record
type R1 = { X: int }
let r1 = { X = 1 }

let data1 = struct {| r1 with Y = 1 |}

// Copy data from a struct record into a reference anonymous record
[<Struct>]
type R2 = { X: int }
let r2 = { X = 1 }

let data2 = {| r1 with Y = 1 |}

// Copy the reference anonymous record data into a struct anonymous record
let data3 = struct {| data2 with Z = r2.X |}
```

## <a name="properties-of-anonymous-records"></a>익명 레코드의 속성

익명 레코드는 완벽 하 게 사용 하는 방법을 이해 하는 데 필요한 특성의 수입니다.

### <a name="anonymous-records-are-nominal"></a>익명 레코드는 명목

익명 레코드가 [명목 형식-](https://en.wikipedia.org/wiki/Nominal_type_system)합니다. 이름이 같은 간주 되기 [레코드](records.md) 유형 (명목 역시)는 초기 선언을 사용할 필요가 없습니다.

두 개의 익명 레코드 선언 사용 하 여 다음 예제를 살펴보세요.

```fsharp
let x = {| X = 1 |}
let y = {| Y = 1 |}
```

합니다 `x` 고 `y` 값 형식이 다르고 서로 호환 되지 않습니다. 비교가 없는는 비교할 수 없습니다. 를 설명 하기 위해이 명명 된 레코드를 동일한 것으로 간주 합니다.

```fsharp
type X = { X: int }
type Y = { Y: int }

let x = { X = 1 }
let y = { Y = 1 }
```

기본적으로 형식 동일성 또는 비교와 관련 된 경우 해당 명명 된 레코드를 비교할 때 익명 레코드에 대 한 다른 없습니다.

### <a name="anonymous-records-use-structural-equality-and-comparison"></a>구조적 같음 및 비교를 사용 하는 익명 레코드

레코드 형식과 마찬가지로 익명 레코드는 구조적으로 비교 및 비교할 수입니다. 경우에 모든 구성 요소 형식에서 레코드 종류를 사용 하 여 같은 같음 및 비교를 지원 합니다. 같음 또는 비교를 지원 하려면 동일한 "모양" 두 개의 익명 레코드에 있어야 합니다.

```fsharp
{| a = 1+1 |} = {| a = 2 |} // true
{| a = 1+1 |} > {| a = 1 |} // true

// error FS0001: Two anonymous record types have mismatched sets of field names '["a"]' and '["a"; "b"]'
{| a = 1 + 1 |} = {| a = 2;  b = 1|}
```

### <a name="anonymous-records-are-serializable"></a>익명 레코드는 직렬화 가능

명명 된 레코드가 있는 경우와 마찬가지로 익명 레코드를 serialize 할 수 있습니다. 다음은 예제를 사용 하 여 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/):

```fsharp
open Newtonsoft.Json

let phillip = {| name="Phillip"; age=28 |}
JsonConvert.SerializeObject(phillip)

let phillip = JsonConvert.DeserializeObject<{|name: string; age: int|}>(str)
printfn "Name: %s Age: %d" phillip.name phillip.age
```

익명 레코드 형식 직렬화/역직렬화 사전에 대 한 도메인을 정의 하지 않고도 네트워크를 통해 간단한 데이터를 보내는 데 유용 합니다.

### <a name="anonymous-records-interoperate-with-c-anonymous-types"></a>익명 레코드와 상호 운용 C# 익명 형식

사용 해야 하는.NET API를 사용 하는 것이 불가능 [ C# 익명 형식](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)합니다. C#익명 형식은 익명 레코드를 사용 하 여 상호 운용 되도록 어렵지 않습니다. 다음 예제에서는 익명 레코드를 호출 하는 데는 [LINQ](../../csharp/programming-guide/concepts/linq/index.md) 무명 형식이 필요로 하는 오버 로드.

```fsharp
open System.Linq

let names = [ "Ana"; "Felipe"; "Emilia"]
let nameGrouping = names.Select(fun n -> {| Name = n; FirstLetter = n.[0] |})
for ng in nameGrouping do
    printfn "%s has first letter %c" ng.Name ng.FirstLetter
```

익명 형식에서 전달 사용 해야 하는.NET 전체에서 사용 되는 다른 Api의 여러 가지가 있습니다. 익명 레코드는 사용 하기 위한 도구입니다.

## <a name="limitations"></a>제한 사항

익명 기록 용도에 몇 가지 제한 사항이 있습니다. 일부는 해당 디자인에 내재 된 되지만 다른 적응성을 변경 합니다.

### <a name="limitations-with-pattern-matching"></a>패턴 일치의 제한 사항

익명 레코드는 명명 된 레코드와 달리 패턴 일치를 지원 하지 않습니다. 다음과 같은 세 가지가 있습니다.

1. 패턴의 명명 된 레코드 형식과 달리 익명 레코드를 모든 필드에 대 한 계정 것입니다. 익명 기록 구조적 동등을 지원 하지 않습니다 – 명목 형식 때문입니다.
2. (1)으로 인해 경우 패턴 일치 식에 추가 패턴을 사용할 수 있는 기능이 없습니다 알 수 있듯이 각 고유 패턴은 다른 익명 레코드 종류
3. (3)으로 인해 모든 익명 레코드 패턴 "점" 표기법을 사용 하 여 보다 자세한 것입니다.

열고 언어 제안 하는 [컨텍스트 제한에 패턴 일치를 허용](https://github.com/fsharp/fslang-suggestions/issues/713)합니다.

### <a name="limitations-with-mutability"></a>가변성의 제한 사항

현재 사용 하 여 익명 레코드를 정의할 수 없는 `mutable` 데이터입니다. [언어 제안 엽니다](https://github.com/fsharp/fslang-suggestions/issues/732) 변경할 수 있는 데이터를 허용 하도록 합니다.

### <a name="limitations-with-struct-anonymous-records"></a>익명 구조체 레코드의 제한 사항

익명 레코드는 구조체를 선언할 수 있지 `IsByRefLike` 또는 `IsReadOnly`합니다. [언어 제안 엽니다](https://github.com/fsharp/fslang-suggestions/issues/712) 에 대 한 `IsByRefLike` 및 `IsReadOnly` 익명 레코드입니다.
