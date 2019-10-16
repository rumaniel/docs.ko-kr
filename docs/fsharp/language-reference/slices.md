---
title: 조각 (F#)
description: 기존 F# 데이터 형식에 조각을 사용 하는 방법과 다른 데이터 형식에 대 한 사용자 고유의 조각을 정의 하는 방법에 대해 알아봅니다.
ms.date: 01/22/2019
ms.openlocfilehash: 3067982c2b4249312c7e9365bbfb994be840911d
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627138"
---
# <a name="slices"></a>조각

에서 F#조각은 데이터 형식의 하위 집합입니다. 데이터 형식에서 조각을 가져올 수 있으려면 데이터 형식이 범위 내에 있는 `GetSlice` [형식 확장](type-extensions.md) 또는 메서드를 정의 해야 합니다. 이 문서에서는 기존 F# 형식에서 조각을 가져오는 방법 및 사용자 고유의 조각을 정의 하는 방법을 설명 합니다.

조각은 [인덱서와](./members/indexed-properties.md)비슷하지만 기본 데이터 구조에서 단일 값을 생성 하는 대신 여러 개를 생성 합니다.

F#현재에서는 조각화 문자열, 목록, 배열 및 2D 배열에 대 한 기본 지원을 제공 합니다.

## <a name="basic-slicing-with-f-lists-and-arrays"></a>목록 및 배열을 F# 사용 하 여 기본 조각화

가장 일반적으로 분리 되는 데이터 형식은 F# 목록 및 배열입니다. 다음 예제에서는 목록을 사용 하 여이 작업을 수행 하는 방법을 보여 줍니다.

```fsharp
// Generate a list of 100 integers
let fullList = [ 1 .. 100 ]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullList.[1..5]
printfn "Small slice: %A" smallSlice

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullList.[..5]
printfn "Unbounded beginning slice: %A" unboundedBeginning

// Create a slice from an index to the end of the list
let unboundedEnd = fullList.[94..]
printfn "Unbounded end slice: %A" unboundedEnd
```

조각화 된 배열을 조각화 목록 처럼 분리 하는 것입니다.

```fsharp
// Generate an array of 100 integers
let fullArray = [| 1 .. 100 |]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullArray.[1..5]
printfn "Small slice: %A" smallSlice

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullArray.[..5]
printfn "Unbounded beginning slice: %A" unboundedBeginning

// Create a slice from an index to the end of the list
let unboundedEnd = fullArray.[94..]
printfn "Unbounded end slice: %A" unboundedEnd
```

## <a name="slicing-multidimensional-arrays"></a>다차원 배열 조각화

F#는 F# 핵심 라이브러리의 다차원 배열을 지원 합니다. 1 차원 배열과 마찬가지로 다차원 배열의 조각이 유용할 수도 있습니다. 그러나 추가 차원의 도입은 특정 행과 열의 조각을 가져올 수 있도록 약간 다른 구문을 사용 합니다.

다음 예제에서는 2D 배열을 조각화 하는 방법을 보여 줍니다.

```fsharp
// Generate a 3x3 2D matrix
let A = array2D [[1;2;3];[4;5;6];[7;8;9]]
printfn "Full matrix:\n %A" A

// Take the first row
let row0 = A.[0,*]
printfn "Row 0: %A" row0

// Take the first column
let col0 = A.[*,0]
printfn "Column 0: %A" col0

// Take all rows but only two columns
let subA = A.[*,0..1]
printfn "%A" subA

// Take two rows and all columns
let subA' = A.[0..1,*]
printfn "%A" subA'

// Slice a 2x2 matrix out of the full 3x3 matrix
let twoByTwo = A.[0..1,0..1]
printfn "%A" twoByTwo
```

핵심 F# 라이브러리는 3d 배열을 정의 `GetSlice`하지 않습니다. 차원의 다른 배열이 나 다른 배열을 조각화 하려는 경우에는 멤버를 `GetSlice` 직접 정의 해야 합니다.

## <a name="defining-slices-for-other-data-structures"></a>다른 데이터 구조에 대 한 조각 정의

핵심 F# 라이브러리는 제한 된 형식 집합에 대 한 조각을 정의 합니다. 더 많은 데이터 형식에 대 한 조각을 정의 하려는 경우 형식 정의 자체 나 형식 확장에서이 작업을 수행할 수 있습니다.

예를 들어, 편리한 데이터 조작을 허용 하기 위해 <xref:System.ArraySegment%601> 클래스의 조각을 정의 하는 방법은 다음과 같습니다.

```fsharp
open System

type ArraySegment<'TItem> with
    member segment.GetSlice(?start, ?finish) =
        let start = defaultArg start 0
        let finish = defaultArg finish segment.Count
        ArraySegment(segment.Array, segment.Offset + start, finish - start)

let arr = ArraySegment [| 1 .. 10 |]
let slice = arr.[2..5] //[ 3; 4; 5]
```

### <a name="use-inlining-to-avoid-boxing-if-it-is-necessary"></a>필요한 경우 boxing을 방지 하려면 인라인을 사용 합니다.

실제로 struct 인 형식에 대 한 조각을 정의 하는 경우 `inline` `GetSlice` 멤버를 정의 하는 것이 좋습니다. 컴파일러 F# 는 선택적 인수를 최적화 하 여 조각화의 결과로 힙 할당을 방지 합니다. 이는 힙에 할당 될 수 없는와 <xref:System.Span%601> 같은 조각화 구문에 매우 중요 합니다.

```fsharp
open System

type Span<'T> with
    // Note the 'inline' in the member definition
    member inline sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e)

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn "%A" arr

let sp = [| 1; 2; 3; 4; 5 |].AsSpan()
printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
printSpan sp.[..5] // [|1; 2; 3; 4; 5|]
printSpan sp.[0..3] // [|1; 2; 3|]
printSpan sp.[1..2] // |2; 3|]
```

## <a name="see-also"></a>참고자료

- [인덱싱된 속성](./members/indexed-properties.md)
