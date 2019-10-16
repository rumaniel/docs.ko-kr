---
title: 구별된 공용 구조체
description: 구별 된 공용 구조체 F# 를 사용 하는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 79da6c6ff9d3699818014d86f6c95edc3e43b4c1
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083036"
---
# <a name="discriminated-unions"></a>구별된 공용 구조체

구별 된 공용 구조체는 여러 개의 명명 된 사례 중 하나일 수 있는 값을 지원 합니다. 각각의 값과 형식이 서로 다를 수 있습니다. 구별 된 공용 구조체는 다른 유형의 데이터에 유용 합니다. 유효한 및 오류 사례를 포함 하 여 특수 한 경우를 포함 하는 데이터 한 인스턴스에서 다른 인스턴스로의 형식에 따라 달라 지는 데이터 및는 작은 개체 계층 구조에 대 한 대 안으로 사용할 수도 있습니다. 또한 재귀적으로 구분 된 공용 구조체는 트리 데이터 구조를 나타내는 데 사용 됩니다.

## <a name="syntax"></a>구문

```fsharp
[ attributes ]
type [accessibility-modifier] type-name =
    | case-identifier1 [of [ fieldname1 : ] type1 [ * [ fieldname2 : ] type2 ...]
    | case-identifier2 [of [fieldname3 : ]type3 [ * [ fieldname4 : ]type4 ...]

    [ member-list ]
```

## <a name="remarks"></a>설명

구별 된 공용 구조체는 다른 언어의 공용 구조체 형식과 비슷하지만 차이가 있습니다. 의 C++ union 형식 또는 Visual Basic의 variant 형식과 마찬가지로 값에 저장 된 데이터는 수정 되지 않습니다. 여러 가지 다른 옵션 중 하나를 사용할 수 있습니다. 그러나 이러한 다른 언어의 공용 구조체와는 달리 각각의 가능한 옵션에는 *case 식별자*가 제공 됩니다. Case 식별자는 이러한 형식의 개체가 가질 수 있는 다양 한 형식의 값에 대 한 이름입니다. 값은 선택 사항입니다. 값이 없는 경우 대/소문자는 열거 사례와 동일 합니다. 값이 있는 경우 각 값은 지정 된 형식의 단일 값 이거나 동일 하거나 다른 형식의 여러 필드를 집계 하는 튜플입니다 수 있습니다. 개별 필드에 이름을 지정할 수 있지만 동일한 사례의 다른 필드가 명명 된 경우에도 이름은 선택 사항입니다.

구분 된 공용 구조체에 대 `public`한 접근성은 기본적으로로 설정 됩니다.

예를 들어 다음과 같은 모양 형식의 선언을 살펴보겠습니다.

```fsharp
type Shape =
    | Rectangle of width : float * length : float
    | Circle of radius : float
    | Prism of width : float * float * height : float
```

위의 코드는 다음과 같은 세 가지 경우의 값을 가질 수 있는 구별 된 공용 구조체 셰이프를 선언 합니다. 사각형, 원 및 프리즘입니다. 각 사례에는 서로 다른 필드 집합이 있습니다. 사각형의 경우에는 두 개의 명명 된 필드 ( `float`형식)가 있으며 이름에는 너비와 길이가 있습니다. 원 케이스에는 하나의 명명 된 필드인 반지름이 있습니다. 프리즘 사례에는 세 개의 필드가 있으며,이 필드에는 두 개의 필드 (너비와 높이)가 명명 된 필드가 있습니다. 명명 되지 않은 필드를 익명 필드 라고 합니다.

다음 예제에 따라 명명 된 필드 및 익명 필드에 값을 제공 하 여 개체를 생성 합니다.

```fsharp
let rect = Rectangle(length = 1.3, width = 10.0)
let circ = Circle (1.0)
let prism = Prism(5., 2.0, height = 3.0)
```

이 코드에서는 초기화에 명명 된 필드를 사용 하거나, 선언의 필드 순서를 사용 하 고, 각 필드의 값을 차례로 제공 하는 방법에 대해 설명 합니다. 이전 코드의에 `rect` 대 한 생성자 호출은 명명 된 필드를 사용 하지만의 `circ` 생성자 호출은 순서를 사용 합니다. 의 `prism`생성에서와 같이 순서가 지정 된 필드와 명명 된 필드를 혼합할 수 있습니다.

`option` 형식은 F# 핵심 라이브러리의 단순한 구별 된 공용 구조체입니다. `option` 형식은 다음과 같이 선언 됩니다.

```fsharp
// The option type is a discriminated union.
type Option<'a> =
    | Some of 'a
    | None
```

이전 코드에서는 형식이 `Option` 와 `None`이라는 두 가지 경우를 `Some` 포함 하는 구별 된 공용 구조체 임을 지정 합니다. Case에는 형식이 형식 매개 변수로 `'a`표시 되는 익명 필드 하나로 구성 된 연결 된 값이 있습니다. `Some` `None` 케이스에 연결 된 값이 없습니다. `option` 따라서 형식이 일부 형식의 값 또는 값이 없는 제네릭 형식을 지정 합니다. 또한이 `Option` 형식에는 보다 일반적으로 사용 `option`되는 소문자 형식 별칭이 있습니다.

Case 식별자를 구별 된 공용 구조체 형식에 대 한 생성자로 사용할 수 있습니다. 예를 들어 다음 코드는 `option` 형식의 값을 만드는 데 사용 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2001.fs)]

Case 식별자는 패턴 일치 식에도 사용 됩니다. 패턴 일치 식에서 개별 사례와 관련 된 값에 대 한 식별자가 제공 됩니다. 예를 들어 다음 코드 `x` 에서는 `option` 형식의 `Some` 케이스와 연결 된 값을 제공 하는 식별자입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2002.fs)]

패턴 일치 식에서 명명 된 필드를 사용 하 여 구별 된 공용 구조체 일치를 지정할 수 있습니다. 이전에 선언 된 셰이프 형식의 경우 다음 코드와 같이 명명 된 필드를 사용 하 여 필드 값을 추출할 수 있습니다.

```fsharp
let getShapeHeight shape =
    match shape with
    | Rectangle(height = h) -> h
    | Circle(radius = r) -> 2. * r
    | Prism(height = h) -> h
```

일반적으로 대/소문자 식별자는 공용 구조체의 이름으로 한정 하지 않고 사용할 수 있습니다. 이름을 항상 공용 구조체의 이름으로 정규화 하려면 [RequireQualifiedAccess](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.requirequalifiedaccessattribute-class-[fsharp]) 특성을 공용 구조체 형식 정의에 적용 하면 됩니다.

### <a name="unwrapping-discriminated-unions"></a>래핑 해제 구별 된 공용 구조체

F# 구분 된 공용 구조체는 단일 형식을 래핑하는 도메인 모델링에 자주 사용 됩니다. 패턴 일치를 통해 내부 값을 추출 하는 것도 쉽습니다. 단일 사례에 대해 일치 식을 사용할 필요는 없습니다.

```fsharp
let ([UnionCaseIdentifier] [values]) = [UnionValue]
```

다음은 이에 대한 예입니다.

```fsharp
type ShaderProgram = | ShaderProgram of id:int

let someFunctionUsingShaderProgram shaderProgram =
    let (ShaderProgram id) = shaderProgram
    // Use the unwrapped value
    ...
```

또한 패턴 일치는 함수 매개 변수에서 직접 사용할 수 있으므로 단일 사례를 래핑을 해제할 수 있습니다.

```fsharp
let someFunctionUsingShaderProgram (ShaderProgram id) =
    // Use the unwrapped value
    ...
```

## <a name="struct-discriminated-unions"></a>구별 된 공용 구조체 구조체

구별 된 공용 구조체를 구조체로 나타낼 수도 있습니다.  이 작업은 `[<Struct>]` 특성을 사용 하 여 수행 됩니다.

```fsharp
[<Struct>]
type SingleCase = Case of string

[<Struct>]
type Multicase =
    | Case1 of Case1 : string
    | Case2 of Case2 : int
    | Case3 of Case3 : double
```

이러한 값 형식은 참조 형식이 아니라 값 형식 이므로 참조 구별 된 공용 구조체와 비교 하 여 추가로 고려해 야 할 사항이 있습니다.

1. 값 형식으로 복사 되 고 값 형식 의미 체계가 있습니다.
2. Multicase 구조체와 구별 된 공용 구조체에는 재귀 형식 정의를 사용할 수 없습니다.
3. Multicase 구조체 구별 된 공용 구조체에 대 한 고유한 대/소문자 이름을 제공 해야 합니다.

## <a name="using-discriminated-unions-instead-of-object-hierarchies"></a>개체 계층 구조 대신 구별 된 공용 구조체 사용

종종 구별 된 공용 구조체를 작은 개체 계층에 대 한 보다 간단한 방법으로 사용할 수 있습니다. 예를 들어 원, 사각형 등에 대해 파생 된 형식이 있는 `Shape` 기본 클래스 대신 다음과 같은 구별 된 공용 구조체를 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2003.fs)]

영역 또는 둘레를 계산 하는 가상 메서드 대신 개체 지향 구현에서 사용 하는 것 처럼 패턴 일치를 사용 하 여 적절 한 수식으로 분기 하 고 이러한 수량을 계산할 수 있습니다. 다음 예에서는 도형에 따라 서로 다른 수식을 사용 하 여 영역을 계산 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2004.fs)]

출력은 다음과 같습니다.

```console
Area of circle that has radius 15.000000: 706.858347
Area of square that has side 10.000000: 100.000000
Area of rectangle that has height 5.000000 and width 10.000000 is 50.000000
```

## <a name="using-discriminated-unions-for-tree-data-structures"></a>트리 데이터 구조에 대해 구별 된 공용 구조체 사용

구분 된 공용 구조체는 재귀적 일 수 있습니다. 즉, union 자체는 하나 이상의 사례 형식에 포함 될 수 있습니다. 재귀 구별 된 공용 구조체를 사용 하 여 프로그래밍 언어로 식을 모델링 하는 데 사용 되는 트리 구조를 만들 수 있습니다. 다음 코드에서 재귀적으로 구분 된 공용 구조체를 사용 하 여 이진 트리 데이터 구조를 만듭니다. Union은 정수 값과 왼쪽 및 `Node`오른쪽 하위 트리가 포함 된 노드인 및 `Tip`트리를 종료 하는 두 가지 case로 구성 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2005.fs)]

이전 코드 `resultSumTree` 에서의 값은 10입니다. 다음 그림에서는의 `myTree`트리 구조를 보여 줍니다.

![MyTree의 트리 구조를 표시 하는 다이어그램입니다.](../media/discriminated-unions/tree-structure-mytree.png)

구별 된 공용 구조체는 트리의 노드가 다른 유형이 면 잘 작동 합니다. 다음 코드에서 형식은 `Expression` 숫자 및 변수의 더하기와 곱셈을 지 원하는 간단한 프로그래밍 언어의 식에 대 한 추상 구문 트리를 나타냅니다. 일부 공용 구조체 케이스는 재귀적이 아니고 숫자 (`Number`) 또는 변수 (`Variable`)를 나타냅니다. 다른 경우는 재귀이 고 연산자 (`Add` 및 `Multiply`)를 나타내지만 피연산자도 식입니다. 함수 `Evaluate` 는 일치 식을 사용 하 여 구문 트리를 재귀적으로 처리 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2006.fs)]

이 코드가 실행 되 면의 `result` 값은 5입니다.

## <a name="members"></a>멤버

구별 된 공용 구조체에 멤버를 정의할 수 있습니다. 다음 예제에서는 속성을 정의 하 고 인터페이스를 구현 하는 방법을 보여 줍니다.

```fsharp
open System

type IPrintable =
    abstract Print: unit -> unit

type Shape =
    | Circle of float
    | EquilateralTriangle of float
    | Square of float
    | Rectangle of float * float

    member this.Area =
        match this with
        | Circle r -> 2.0 * Math.PI * r
        | EquilateralTriangle s -> s * s * sqrt 3.0 / 4.0
        | Square s -> s * s
        | Rectangle(l, w) -> l * w

    interface IPrintable with
        member this.Print () =
            match this with
            | Circle r -> printfn "Circle with radius %f" r
            | EquilateralTriangle s -> printfn "Equilateral Triangle of side %f" s
            | Square s -> printfn "Square with side %f" s
            | Rectangle(l, w) -> printfn "Rectangle with length %f and width %f" l w
```

## <a name="common-attributes"></a>공통 특성

다음 특성은 일반적으로 구분 된 공용 구조체에서 볼 수 있습니다.

- `[<RequireQualifiedAccess>]`
- `[<NoEquality>]`
- `[<NoComparison>]`
- `[<Struct>]`

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
