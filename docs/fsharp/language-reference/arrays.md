---
title: 배열
description: F# 프로그래밍 언어로 배열을 만들고 사용 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: ae8f3cfc84fbba4cac496d4221d140dadec25e10
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71082962"
---
# <a name="arrays"></a>배열

> [!NOTE]
> API 참조 링크를 통해 MSDN으로 이동됩니다.  docs.microsoft.com API 참조가 완전하지 않습니다.

배열은 동일한 형식의 연속 데이터 요소에 대 한 고정 크기의 변경 가능한 컬렉션으로, 0부터 시작 합니다.

## <a name="creating-arrays"></a>배열 만들기

여러 가지 방법으로 배열을 만들 수 있습니다. 다음 예제와 같이 및 `[|` `|]` 사이에 연속 값을 나열 하 고 세미콜론으로 구분 하 여 작은 배열을 만들 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet1.fs)]

각 요소를 별도의 줄에 배치할 수도 있습니다 .이 경우 세미콜론 구분 기호는 선택 사항입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet2.fs)]

배열 요소의 형식은 사용 된 리터럴에서 유추 되며 일치 해야 합니다. 다음 코드는 1.0가 float이 고 2와 3이 정수 이므로 오류가 발생 합니다.

```fsharp
// Causes an error.
// let array2 = [| 1.0; 2; 3 |]
```

시퀀스 식을 사용 하 여 배열을 만들 수도 있습니다. 다음은 1에서 10 사이의 정수 제곱 배열을 만드는 예제입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet3.fs)]

모든 요소가 0으로 초기화 되는 배열을 만들려면를 사용 `Array.zeroCreate`합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet4.fs)]

## <a name="accessing-elements"></a>요소 액세스

점 연산자 (`.`)와 대괄호 (`[` 및 `]`)를 사용 하 여 배열 요소에 액세스할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet5.fs)]

배열 인덱스는 0부터 시작 합니다.

배열의 하위 범위를 지정 하는 데 사용할 수 있는 조각 표기법을 사용 하 여 배열 요소에 액세스할 수도 있습니다. 조각 표기법의 예는 다음과 같습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet51.fs)]

조각 표기법을 사용 하면 배열의 새 복사본이 만들어집니다.

## <a name="array-types-and-modules"></a>배열 형식 및 모듈

모든 F# 배열의 형식은 .NET Framework 형식 <xref:System.Array?displayProperty=nameWithType>입니다. 따라서 F# 배열은에서 <xref:System.Array?displayProperty=nameWithType>사용할 수 있는 모든 기능을 지원 합니다.

라이브러리 모듈 [`Microsoft.FSharp.Collections.Array`](https://msdn.microsoft.com/library/0cda8040-9396-40dd-8dcd-cf48542165a1) 은 1 차원 배열에 대 한 작업을 지원 합니다. 모듈 `Array2D`, `Array3D`및 에는각각2,3및4차원배열에대한작업을지원하는함수가포함되어있습니다.`Array4D` 을 사용 <xref:System.Array?displayProperty=nameWithType>하 여 4 보다 큰 차수 배열을 만들 수 있습니다.

### <a name="simple-functions"></a>간단한 함수

[`Array.get`](https://msdn.microsoft.com/library/dd93e85d-7e80-4d76-8de0-b6d45bcf07bc)요소를 가져옵니다. [`Array.length`](https://msdn.microsoft.com/library/0d775b6a-4a8f-4bd1-83e5-843b3251725f)배열의 길이를 제공 합니다. [`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790)요소를 지정 된 값으로 설정 합니다. 다음 코드 예제에서는 이러한 함수를 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet9.fs)]

출력은 다음과 같습니다.

```console
0 1 2 3 4 5 6 7 8 9
```

### <a name="functions-that-create-arrays"></a>배열을 만드는 함수

여러 함수는 기존 배열을 요구 하지 않고 배열을 만듭니다. [`Array.empty`](https://msdn.microsoft.com/library/c3694b92-1c16-4c54-9bf2-fe398fadce32)요소가 포함 되지 않은 새 배열을 만듭니다. [`Array.create`](https://msdn.microsoft.com/library/e848c8d6-1142-4080-9727-8dacc26066be)지정 된 크기의 배열을 만들고 모든 요소를 제공 된 값으로 설정 합니다. [`Array.init`](https://msdn.microsoft.com/library/ee898089-63b0-40aa-910c-5ae7e32f6665)지정 된 차원과 요소를 생성 하는 함수를 지정 하 여 배열을 만듭니다. [`Array.zeroCreate`](https://msdn.microsoft.com/library/fa5b8e7a-1b5b-411c-8622-b58d7a14d3b2)모든 요소가 배열의 형식에 대해 0 값으로 초기화 되는 배열을 만듭니다. 다음 코드에서는 이러한 함수를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet91.fs)]

출력은 다음과 같습니다.

```console
Length of empty array: 0
Area of floats set to 5.0: [|5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0|]
Array of squares: [|0; 1; 4; 9; 16; 25; 36; 49; 64; 81|]
```

[`Array.copy`](https://msdn.microsoft.com/library/9d0202f1-1ea0-475e-9d66-4f8ccc3c5b5f)기존 배열에서 복사 된 요소를 포함 하는 새 배열을 만듭니다. 복사본은 단순 복사본입니다. 즉, 요소 형식이 참조 형식이 면 참조만 복사 되 고 기본 개체는 복사 되지 않습니다. 다음 코드 예제에서는 그 구체적인 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet11.fs)]

위의 코드의 출력은 다음과 같습니다.

```console
[|Test1; Test2; |]
[|; Test2; |]
```

새 요소 `Test1` 를 만드는 작업은에서 `firstArray` 참조를 덮어쓰므로에서 여전히에 `secondArray`있는 빈 문자열에 대 한 원래 참조에는 영향을 주지 않기 때문에이 문자열은 첫 번째 배열에만 나타납니다. 형식에 `Test2` 대 `Insert` 한 작업이 두 배열에서 참조 되는 기본 <xref:System.Text.StringBuilder?displayProperty=nameWithType> 개체에 영향을 주기 때문에 두 배열에 문자열이 모두 표시 됩니다. <xref:System.Text.StringBuilder?displayProperty=nameWithType>

[`Array.sub`](https://msdn.microsoft.com/library/40fb12ba-41d7-4ef0-b33a-56727deeef9d)배열의 하위 범위에서 새 배열을 생성 합니다. 시작 인덱스 및 길이를 제공 하 여 하위 범위를 지정 합니다. 다음 코드는 `Array.sub`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet12.fs)]

출력은 하위 배열을 요소 5에서 시작 하 고 10 개의 요소를 포함 하는 것을 보여 줍니다.

```console
[|5; 6; 7; 8; 9; 10; 11; 12; 13; 14|]
```

[`Array.append`](https://msdn.microsoft.com/library/08836310-5036-4474-b9a2-2c73e2293911)두 개의 기존 배열을 결합 하 여 새 배열을 만듭니다.

다음 코드에서는 **배열. append**를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet13.fs)]

위의 코드는 다음과 같이 출력 됩니다.

```console
[|1; 2; 3; 4; 5; 6|]
```

[`Array.choose`](https://msdn.microsoft.com/library/f5c8a5e2-637f-44d4-b35c-be96a6618b09)새 배열에 포함할 배열의 요소를 선택 합니다. 다음 코드에서는을 `Array.choose`보여 줍니다. 배열의 요소 형식은 옵션 형식에서 반환 되는 값의 형식과 일치할 필요가 없습니다. 이 예제에서 요소 형식은이 `int` 고 옵션은 다항식 `elem*elem - 1`함수의 결과인 부동 소수점 숫자입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet14.fs)]

위의 코드는 다음과 같이 출력 됩니다.

```console
[|3.0; 15.0; 35.0; 63.0; 99.0|]
```

[`Array.collect`](https://msdn.microsoft.com/library/c3b60c3b-9455-48c9-bc2b-e88f0434342a)기존 배열의 각 배열 요소에 대해 지정 된 함수를 실행 한 다음 함수에 의해 생성 된 요소를 수집 하 여 새 배열로 결합 합니다. 다음 코드에서는을 `Array.collect`보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet15.fs)]

위의 코드는 다음과 같이 출력 됩니다.

```console
[|0; 1; 0; 1; 2; 3; 4; 5; 0; 1; 2; 3; 4; 5; 6; 7; 8; 9; 10|]
```

[`Array.concat`](https://msdn.microsoft.com/library/f7219b79-1ec8-4a25-96b1-edbedb358302)배열의 시퀀스를 사용 하 여 단일 배열로 결합 합니다. 다음 코드에서는을 `Array.concat`보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet16.fs)]

위의 코드는 다음과 같이 출력 됩니다.

```console
[|(1, 1, 1); (1, 2, 2); (1, 3, 3); (2, 1, 2); (2, 2, 4); (2, 3, 6); (3, 1, 3);
(3, 2, 6); (3, 3, 9)|]
```

[`Array.filter`](https://msdn.microsoft.com/library/b885b214-47fc-4639-9664-b8c183a39ede)부울 조건 함수를 사용 하 고 조건이 true 인 입력 배열의 요소만 포함 하는 새 배열을 생성 합니다. 다음 코드에서는을 `Array.filter`보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet17.fs)]

위의 코드는 다음과 같이 출력 됩니다.

```console
[|2; 4; 6; 8; 10|]
```

[`Array.rev`](https://msdn.microsoft.com/library/1bbf822c-763b-4794-af21-97d2e48ef709)기존 배열의 순서를 반대로 하 여 새 배열을 생성 합니다. 다음 코드에서는을 `Array.rev`보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet18.fs)]

위의 코드는 다음과 같이 출력 됩니다.

```console
"Hello world!"
```

다음 예제와 같이 파이프라인 연산자 (`|>`)를 사용 하 여 배열을 변환 하는 배열 모듈의 함수를 쉽게 결합할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet19.fs)]

출력은 다음과 같습니다.

```console
[|100; 36; 16; 4|]
```

### <a name="multidimensional-arrays"></a>다차원 배열

다차원 배열을 만들 수 있지만 다차원 배열 리터럴을 작성 하기 위한 구문이 없습니다. 연산자 [`array2D`](https://msdn.microsoft.com/library/1d52503d-2990-49fc-8fd3-6b0e508aa236) 를 사용 하 여 배열 요소의 시퀀스 시퀀스에서 배열을 만듭니다. 시퀀스는 배열 또는 목록 리터럴일 수 있습니다. 예를 들어 다음 코드는 2 차원 배열을 만듭니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet20.fs)]

또한 함수 [`Array2D.init`](https://msdn.microsoft.com/library/9de07e95-bc21-4927-b5b4-08fdec882c7b) 를 사용 하 여 두 차원의 배열을 초기화할 수 있으며, 3 개 차원 및 4 차원 배열에도 유사한 함수를 사용할 수 있습니다. 이러한 함수는 요소를 만드는 데 사용 되는 함수를 사용 합니다. 함수를 지정 하는 대신 초기 값으로 설정 된 요소를 포함 하는 2 차원 배열을 만들려면 최대 4 차원 [`Array2D.create`](https://msdn.microsoft.com/library/36c9d980-b241-4a20-bc64-bcfa0205d804) 배열에도 사용할 수 있는 함수를 사용 합니다. 다음 코드 예제에서는 먼저 원하는 요소를 포함 하는 배열 배열을 만든 다음를 사용 `Array2D.init` 하 여 원하는 2 차원 배열을 생성 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet21.fs)]

배열 인덱싱 및 조각화 구문은 차수가 4 인 배열에 대해 지원 됩니다. 여러 차원에서 인덱스를 지정 하는 경우 다음 코드 예제에 나와 있는 것 처럼 쉼표를 사용 하 여 인덱스를 구분 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet22.fs)]

2 `<type>[,]` 차원 배열의 형식은 ( `int[,]`예:, `double[,]`)로 작성 되 고 3 차원 배열의 형식은로 작성 되며, 더 큰 차원의 배열에 대해서는로 `<type>[,,]`작성 됩니다.

다차원 배열에는 1 차원 배열에 사용할 수 있는 함수의 하위 집합만 사용할 수 있습니다. 자세한 내용은,, 및 [`Collections.Array Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array-module-%5bfsharp%5d) [`Collections.Array2D Module`을참조](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array2d-module-%5bfsharp%5d) [`Collections.Array3D Module`하십시오](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array3d-module-%5bfsharp%5d) [`Collections.Array4D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array4d-module-%5bfsharp%5d).

### <a name="array-slicing-and-multidimensional-arrays"></a>배열 조각화 및 다차원 배열

2 차원 배열 (행렬)에서 범위를 지정 하 고 와일드 카드 (`*`) 문자를 사용 하 여 하위 행렬을 추출 하 여 전체 행 또는 열을 지정할 수 있습니다.

```fsharp
// Get rows 1 to N from an NxM matrix (returns a matrix):
matrix.[1.., *]

// Get rows 1 to 3 from a matrix (returns a matrix):
matrix.[1..3, *]

// Get columns 1 to 3 from a matrix (returns a matrix):
matrix.[*, 1..3]

// Get a 3x3 submatrix:
matrix.[1..3, 1..3]
```

3\.1의 F# 경우 다차원 배열을 같거나 낮은 차원의 subarrays으로 분해할 수 있습니다. 예를 들어 단일 행 또는 열을 지정 하 여 행렬에서 벡터를 가져올 수 있습니다.

```fsharp
// Get row 3 from a matrix as a vector:
matrix.[3, *]

// Get column 3 from a matrix as a vector:
matrix.[*, 3]
```

요소 액세스 연산자 및 오버 로드 `GetSlice` 된 메서드를 구현 하는 형식에 대해이 조각화 구문을 사용할 수 있습니다. 예를 들어 다음 코드는 F# 2d 배열을 래핑하고, 배열 인덱싱에 대 한 지원을 제공 하기 위해 항목 속성을 구현 하 고, 세 가지 버전의 `GetSlice`를 구현 하는 행렬 유형을 만듭니다. 이 코드를 행렬 형식에 대 한 템플릿으로 사용할 수 있는 경우이 단원에서 설명 하는 모든 조각 작업을 사용할 수 있습니다.

```fsharp
type Matrix<'T>(N: int, M: int) =
    let internalArray = Array2D.zeroCreate<'T> N M

    member this.Item
        with get(a: int, b: int) = internalArray.[a, b]
        and set(a: int, b: int) (value:'T) = internalArray.[a, b] <- value

    member this.GetSlice(rowStart: int option, rowFinish : int option, colStart: int option, colFinish : int option) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[rowStart..rowFinish, colStart..colFinish]

    member this.GetSlice(row: int, colStart: int option, colFinish: int option) =
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[row, colStart..colFinish]

    member this.GetSlice(rowStart: int option, rowFinish: int option, col: int) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        internalArray.[rowStart..rowFinish, col]

module test =
    let generateTestMatrix x y =
        let matrix = new Matrix<float>(3, 3)
        for i in 0..2 do
            for j in 0..2 do
                matrix.[i, j] <- float(i) * x - float(j) * y
        matrix

    let test1 = generateTestMatrix 2.3 1.1
    let submatrix = test1.[0..1, 0..1]
    printfn "%A" submatrix

    let firstRow = test1.[0,*]
    let secondRow = test1.[1,*]
    let firstCol = test1.[*,0]
    printfn "%A" firstCol
```

### <a name="boolean-functions-on-arrays"></a>배열의 부울 함수

각각 하나 [`Array.exists`](https://msdn.microsoft.com/library/8e47ad6c-c065-4876-8cb4-ec960ec3e5c9) 또는 [`Array.exists2`](https://msdn.microsoft.com/library/2e384a6a-f99d-4e23-b677-250ffbc1dd8e) 두 배열의 함수 및 테스트 요소입니다. 이러한 함수는 테스트 함수를 사용 하 `true` 고 조건을 충족 하는 요소 또는에 대 한 `Array.exists2`요소 쌍이 있는 경우를 반환 합니다.

다음 코드에서는 `Array.exists` 및 `Array.exists2`를 사용 하는 방법을 보여 줍니다. 이러한 예제에서는 인수 중 하나 (이 경우에는 함수 인수)만 적용 하 여 새 함수를 만듭니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet23.fs)]

위의 코드는 다음과 같이 출력 됩니다.

```console
true
false
false
true
```

마찬가지로 함수 [`Array.forall`](https://msdn.microsoft.com/library/d88f2cd0-fa7f-45cf-ac15-31eae9086cc4) 는 배열을 테스트 하 여 모든 요소가 부울 조건을 충족 하는지 여부를 확인 합니다. 동일한 길이의 [`Array.forall2`](https://msdn.microsoft.com/library/c68f61a1-030c-4024-b705-c4768b6c96b9) 두 배열의 요소를 포함 하는 부울 함수를 사용 하 여 변형이 동일한 작업을 수행 합니다. 다음 코드에서는 이러한 함수를 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet24.fs)]

이러한 예제에 대 한 출력은 다음과 같습니다.

```console
false
true
true
false
```

### <a name="searching-arrays"></a>배열 검색

[`Array.find`](https://msdn.microsoft.com/library/db6d920a-de19-4520-85a4-d83de77c1b33)부울 함수를 사용 하 여 함수가 반환 `true`하는 첫 번째 요소를 반환 하거나 조건을 충족 하는 요소가 없는 경우을 <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> 발생 시킵니다. [`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f)는 요소 `Array.find`자체 대신 요소의 인덱스를 반환 한다는 점을 제외 하 고와 비슷합니다.

다음 코드에서는 및 `Array.find` `Array.findIndex` 를 사용 하 여 완전 한 정사각형과 완전 한 큐브인 숫자를 찾습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet25.fs)]

출력은 다음과 같습니다.

```console
The first element that is both a square and a cube is 64 and its index is 62.
```

[`Array.tryFind`](https://msdn.microsoft.com/library/7bd65f6c-df77-454c-ac3a-6f7baecec9d9)는 결과가 `Array.find`옵션 형식 이라는 점을 제외 하 고는와 유사 하며, 요소 `None` 를 찾을 수 없는 경우를 반환 합니다. `Array.tryFind`일치 하는 요소가 배열 `Array.find` 에 있는지 여부를 알 수 없는 경우 대신를 사용 해야 합니다. 마찬가지로 옵션 유형이 반환 [`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f) 값 이라는 점을 제외 하 고 [는와유사합니다.`Array.tryFindIndex`](https://msdn.microsoft.com/library/da82f7fe-95e9-4fd5-a924-cd3c9d10618a) 요소를 찾을 수 없는 경우 옵션 `None`은입니다.

다음 코드는 `Array.tryFind`의 사용법을 보여줍니다. 이 코드는 이전 코드에 따라 달라 집니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet26.fs)]

출력은 다음과 같습니다.

```console
Found an element: 1
Found an element: 729
```

요소 [`Array.tryPick`](https://msdn.microsoft.com/library/72d45f85-037b-43a9-97fd-17239f72713e) 를 찾을 뿐만 아니라 요소를 변환 해야 하는 경우에 사용 합니다. 결과는 함수에서 변환 된 요소를 옵션 값으로 반환 하는 첫 번째 요소 이거나 `None` , 이러한 요소가 없는 경우입니다.

다음 코드는 `Array.tryPick`의 사용법을 보여줍니다. 이 경우 람다 식 대신 코드를 단순화 하기 위해 몇 가지 로컬 도우미 함수가 정의 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet27.fs)]

출력은 다음과 같습니다.

```console
Found an element 1 with square root 1 and cube root 1.
Found an element 64 with square root 8 and cube root 4.
Found an element 729 with square root 27 and cube root 9.
Found an element 4096 with square root 64 and cube root 16.
```

### <a name="performing-computations-on-arrays"></a>배열에 대 한 계산 수행

함수 [`Array.average`](https://msdn.microsoft.com/library/7029f2b9-91ea-41cb-be1b-466a5a0db20e) 는 배열의 각 요소에 대 한 평균을 반환 합니다. 정수로 정확히 나누기를 지 원하는 요소 형식으로 제한 됩니다. 여기에는 부동 소수점 형식이 포함 되지만 정수 계열 형식은 포함 되지 않습니다. 함수 [`Array.averageBy`](https://msdn.microsoft.com/library/e9d64609-06a3-48f0-bc07-226ab0f85c54) 는 각 요소에 대해 함수를 호출한 결과의 평균을 반환 합니다. 정수 계열 형식의 배열에 대해를 사용 `Array.averageBy` 하 고 함수에서 각 요소를 계산에 대 한 부동 소수점 형식으로 변환할 수 있습니다.

요소 [`Array.max`](https://msdn.microsoft.com/library/f03fbda0-fce6-40e2-a85d-79c9d81f710b) 형식이 [`Array.min`](https://msdn.microsoft.com/library/d6b3da5f-bac0-4355-9846-4b72d95bc3fd) 지 원하는 경우 또는를 사용 하 여 maximum 또는 minimum 요소를 가져옵니다. [`Array.maxBy`](https://msdn.microsoft.com/library/18dbe7c5-482e-4766-8e01-12a76f847045) 마찬가지로 및 [`Array.minBy`](https://msdn.microsoft.com/library/24091583-be78-4cc9-9fab-de6d7506af4f) 는 비교를 지 원하는 형식으로 변환 하는 등의 방법으로 함수를 먼저 실행할 수 있습니다.

[`Array.sum`](https://msdn.microsoft.com/library/4ffdb8c8-cd94-4b0b-9e5c-a7c9c17963c2)배열의 요소를 추가 하 고 [`Array.sumBy`](https://msdn.microsoft.com/library/41698ba6-1adc-4169-8cc5-7a0e3f8de56b) 각 요소에 대해 함수를 호출 하 고 결과를 함께 추가 합니다.

반환 값을 저장 하지 않고 배열의 각 요소에 대해 함수를 실행 하려면를 사용 [`Array.iter`](https://msdn.microsoft.com/library/94eba0f1-ecd7-459f-b89f-ed2a2923e516)합니다. 길이가 같은 두 배열이 포함 된 함수의 경우를 사용 [`Array.iter2`](https://msdn.microsoft.com/library/018aa9b9-f186-4142-be8a-a62462794fdc)합니다. 함수의 결과 배열을 유지 해야 하는 경우에는 한 번에 두 배열에 [`Array.map`](https://msdn.microsoft.com/library/38cbe824-0480-47be-85fd-df3afdd97a45) 대해 [`Array.map2`](https://msdn.microsoft.com/library/bb7aafe8-4a1f-45b9-92fc-1af9eafbea5c)작동 하는 또는를 사용 합니다.

변형을 [`Array.iteri`](https://msdn.microsoft.com/library/8bbe2ed4-ada7-4906-ac3e-cb09f9db6486) [`Array.mapi`](https://msdn.microsoft.com/library/f7e45994-b0a1-49e6-8fb5-5641cea8fde4) [`Array.mapi2`](https://msdn.microsoft.com/library/5edb33d2-47da-44e1-9290-40c00c47d5b0)사용 하 여 요소의 인덱스를 계산에 포함 시킬 수 있습니다. 및의 경우에도 마찬가지입니다. [`Array.iteri2`](https://msdn.microsoft.com/library/c041b91f-6080-45b7-867b-2ed983a90405)

[`Array.fold`](https://msdn.microsoft.com/library/5ed9dd3b-3694-4567-94d0-fd9a24474e09) [,`Array.foldBack`](https://msdn.microsoft.com/library/1121a453-dead-4711-a0ca-cc147752989c), [,`Array.reduceBack`](https://msdn.microsoft.com/library/4fdd4cbe-2238-4c5c-b286-597a7e9036f9), 및 [함수는배열의모든요소를포함하는를실행합니다`Array.scanBack`.](https://msdn.microsoft.com/library/7610f406-7a5c-41db-a0ca-8e2a2a4826ad) [`Array.reduce`](https://msdn.microsoft.com/library/fd62a985-89fe-4f49-a9d4-0c808ac6749d) [`Array.scan`](https://msdn.microsoft.com/library/f6893608-9146-450d-9ebb-a0016803fbb0) 마찬가지로, 변형이 [`Array.fold2`](https://msdn.microsoft.com/library/5c845087-d041-476e-8cc4-53ae6849ef79) [`Array.foldBack2`](https://msdn.microsoft.com/library/aa51b405-df20-4c51-9998-a6530f7db862) 두 배열에 대해 계산을 수행 합니다.

계산을 수행 하는 이러한 함수는 [목록 모듈](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)에 있는 동일한 이름의 함수에 해당 합니다. 사용 예제는 [목록](lists.md)을 참조 하십시오.

### <a name="modifying-arrays"></a>배열 수정

[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790)요소를 지정 된 값으로 설정 합니다. [`Array.fill`](https://msdn.microsoft.com/library/c83c9886-81d9-44f9-a195-61c7b87f7df2)배열의 요소 범위를 지정 된 값으로 설정 합니다. 다음 코드에서는의 `Array.fill`예제를 제공 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet28.fs)]

출력은 다음과 같습니다.

```console
[|1; 2; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 23; 24; 25|]
```

를 사용 [`Array.blit`](https://msdn.microsoft.com/library/675e13e4-7fb9-4e0d-a5be-a112830de667) 하 여 한 배열의 하위 섹션을 다른 배열로 복사할 수 있습니다.

### <a name="converting-to-and-from-other-types"></a>다른 형식으로 변환 또는 다른 형식에서 변환

[`Array.ofList`](https://msdn.microsoft.com/library/e7225239-f561-45a4-b0b5-69a1cdcae78b)목록에서 배열을 만듭니다. [`Array.ofSeq`](https://msdn.microsoft.com/library/6bedf5e0-4b22-46da-b09c-6aa09eff220c)시퀀스에서 배열을 만듭니다. [`Array.toList`](https://msdn.microsoft.com/library/4deff724-0be4-4688-92e7-9d67a1097786)및 [`Array.toSeq`](https://msdn.microsoft.com/library/ac28dbab-406c-4fe0-ab08-c1ce5e247af4) 는 배열 형식에서 이러한 다른 컬렉션 형식으로 변환 합니다.

### <a name="sorting-arrays"></a>배열 정렬

제네릭 [`Array.sort`](https://msdn.microsoft.com/library/c6679075-e7eb-463c-9be5-c89be140c312) 비교 함수를 사용 하 여 배열을 정렬 하는 데 사용 합니다. 키 [`Array.sortBy`](https://msdn.microsoft.com/library/144498dc-091d-4575-a229-c0bcbd61426b) 에 대 한 제네릭 비교 함수를 사용 하 여 정렬 하려면 *키*라고 하는 값을 생성 하는 함수를 지정 하는 데 사용 합니다. 사용자 [`Array.sortWith`](https://msdn.microsoft.com/library/699d3638-4244-4f42-8496-45f53d43ce95) 지정 비교 함수를 제공 하려는 경우를 사용 합니다. `Array.sort`, `Array.sortBy` 및`Array.sortWith` 는 모두 정렬 된 배열을 새 배열로 반환 합니다. , [`Array.sortInPlace`](https://msdn.microsoft.com/library/36f39947-8a88-4823-9e9b-e9d838d292e0) [`Array.sortInPlaceBy`](https://msdn.microsoft.com/library/7fb9d2dd-d461-4c67-8b43-b5c59fc12c3f)및 [변형은새배열을반환하는대신기존배열을수정합니다.`Array.sortInPlaceWith`](https://msdn.microsoft.com/library/454f9e11-972d-47a6-a854-8031cb0c7b0b)

### <a name="arrays-and-tuples"></a>배열 및 튜플

함수 [`Array.zip`](https://msdn.microsoft.com/library/23e086b8-b266-4db2-8b68-e88e6a8e2187) [및`Array.unzip`](https://msdn.microsoft.com/library/a529b47c-2e2b-4f79-ad44-c578432d2f48) 는 튜플 쌍의 배열을 배열의 튜플로 변환 하 고 그 반대의 경우도 마찬가지입니다. [`Array.zip3`](https://msdn.microsoft.com/library/1745744a-d2ca-4c3e-b825-3f15d9f4000d)및 [`Array.unzip3`](https://msdn.microsoft.com/library/bc3e6db0-f334-444f-8c30-813942880677) 는 세 개의 요소로 된 튜플 또는 세 개의 배열로 된 튜플로 작업 한다는 점을 제외 하 고는 유사 합니다.

## <a name="parallel-computations-on-arrays"></a>배열에 대 한 병렬 계산

모듈 [`Array.Parallel`](https://msdn.microsoft.com/library/60f30b77-5af4-4050-9a5c-bcdb3f5cbb09) 에는 배열에 대 한 병렬 계산을 수행 하는 함수가 포함 되어 있습니다. 버전 4 이전 버전의 .NET Framework를 대상으로 하는 응용 프로그램에서는이 모듈을 사용할 수 없습니다.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [F# 형식](fsharp-types.md)
