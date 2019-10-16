---
title: 목록
description: 동일한 형식의 F# 변경 되지 않은 순서가 지정 된 일련의 요소 목록에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 72f1779d7d077da0f1f4804df93fa4ac11f9b2e3
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71082905"
---
# <a name="lists"></a>목록

> [!NOTE]
> 이 문서의 API 참조 링크를 통해 MSDN으로 이동됩니다.  docs.microsoft.com API 참조가 완전하지 않습니다.

F#의 목록은 순서가 지정되고 변경할 수 없는 일련의 동일 형식 요소입니다. 목록에 대 한 기본 작업을 수행 하려면 [목록 모듈](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)의 함수를 사용 합니다.

## <a name="creating-and-initializing-lists"></a>목록 만들기 및 초기화

아래 코드 줄에 나와 있는 것처럼 세미콜론으로 구분되고 대괄호로 묶인 요소를 명시적으로 목록 처리하여 목록을 정의할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1301.fs)]

요소 간에 줄 바꿈을 삽입하고 필요에 따라 세미콜론을 사용할 수도 있습니다. 요소 초기화 식이 더 길거나 각 요소에 대해 주석을 추가하려는 경우에는 이 두 번째 구문을 사용하면 코드를 더 쉽게 읽을 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet13011.fs)]

일반적으로 모든 목록 요소는 같은 형식이어야 합니다. 단, 요소가 기본 형식으로 지정된 목록에는 파생 형식 요소를 포함할 수 있습니다. 그러므로 `Button` 및 `CheckBox`가 모두 `Control`에서 파생되는 아래 코드는 정상적으로 사용 가능합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet13012.fs)]

아래 코드에 나와 있는 것처럼 범위 연산자(`..`)로 구분된 정수로 표시되는 범위를 사용하여 목록 요소를 정의할 수도 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1302.fs)]

빈 목록은 안에 아무 내용이 없는 대괄호 쌍으로 지정됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1304.fs)]

시퀀스 식을 사용하여 목록을 만들 수도 있습니다. 자세한 내용은 [시퀀스 식](sequences.md#sequence-expressions) 을 참조 하세요. 예를 들어 다음 코드는 정수 1~10의 제곱 목록을 만듭니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1303.fs)]

## <a name="operators-for-working-with-lists"></a>목록 사용을 위한 연산자

`::`(cons) 연산자를 사용하여 목록에 요소를 연결할 수 있습니다. `list1`이 `[2; 3; 4]`이면 다음 코드는 `list2`를 `[100; 2; 3; 4]`로 작성합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1305.fs)]

다음 코드와 같이 `@` 연산자를 사용하여 호환 형식을 포함하는 목록을 연결할 수 있습니다. `list1`이 `[2; 3; 4]`이고 `list2`가 `[100; 2; 3; 4]`이면 다음 코드는 `list3`을 `[2; 3; 4; 100; 2; 3; 4]`로 작성합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1306.fs)]

목록에서 작업을 수행 하는 함수는 [목록 모듈](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)에서 사용할 수 있습니다.

F#의 목록은 변경이 불가능하므로 수정 작업을 수행하면 기존 목록이 수정되는 대신 새 목록이 생성됩니다.

의 F# 목록은 단일 연결 목록으로 구현 됩니다. 즉, 목록의 헤드에만 액세스 하는 작업은 o (1)이 고 요소 액세스는 o (*n*)입니다.

## <a name="properties"></a>속성

목록 형식이 지원하는 속성은 다음과 같습니다.

|속성|형식|설명|
|--------|----|-----------|
|[사장](https://msdn.microsoft.com/library/5f9414fd-6bdb-470a-8b72-40016db30740)|`'T`|첫 번째 요소입니다.|
|[비어 있음](https://msdn.microsoft.com/library/44406ecb-1918-4d32-b32a-ca1f69840386)|`'T list`|해당 형식의 빈 목록을 반환하는 정적 속성입니다.|
|[IsEmpty](https://msdn.microsoft.com/library/3ba087b2-2fc2-406d-b10a-cff6a19322da)|`bool`|목록에 요소가 없으면 `true`입니다.|
|[항목](https://msdn.microsoft.com/library/bdb2553a-0e54-4ff8-baed-ab1aac8f5dae)|`'T`|지정한 인덱스에 있는 요소로서 0부터 시작합니다.|
|[길이](https://msdn.microsoft.com/library/25f715c8-9daa-4c4d-a6c7-26772f9dab4d)|`int`|요소의 수입니다.|
|[비상](https://msdn.microsoft.com/library/2a6f8eb9-dc32-41aa-8b62-2baffaface91)|`'T list`|첫 번째 요소가 없는 목록입니다.|

이러한 속성을 사용하는 몇 가지 예는 다음과 같습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1307.fs)]

## <a name="using-lists"></a>목록 사용

목록을 사용하여 프로그래밍할 때는 적은 양의 코드만으로도 복잡한 작업을 수행할 수 있습니다. 이 섹션에서는 기능적인 프로그래밍에 중요한 일반적인 목록 관련 작업에 대해 설명합니다.

### <a name="recursion-with-lists"></a>목록을 사용한 재귀

목록을 고유한 방식으로 재귀 프로그래밍 기술에 맞게 사용할 수 있습니다. 목록의 모든 요소에 대해 수행해야 하는 작업을 고려해 보세요. 목록 헤드에 대해 작업을 수행한 다음 목록 꼬리(첫 번째 요소를 제외한 원래 목록으로 구성되는 더 작은 목록)를 다음 재귀 수준으로 다시 전달하는 재귀적인 방식으로 이 작업을 수행할 수 있습니다.

이러한 재귀 함수를 작성하려면 패턴 일치에서 cons 연산자(`::`)를 사용합니다. 그러면 목록 헤드를 꼬리에서 분리할 수 있습니다.

다음 코드 예제에서는 패턴 일치를 사용하여 목록에 대해 작업을 수행하는 재귀 함수를 구현하는 방법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet13071.fs)]

위의 코드는 작은 목록에서는 효율적으로 작동하지만 큰 목록에서는 스택이 오버플로될 수 있습니다. 위의 코드보다 개선된 다음 코드에서는 재귀 함수 사용을 위한 표준 기술인 누적기 인수를 사용합니다. 누적기 인수를 사용하면 함수 꼬리가 재귀적으로 적용되므로 스택 공간이 절약됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet13072.fs)]

`RemoveAllMultiples` 함수는 목록 두 개를 사용하는 재귀 함수입니다. 첫 번째 목록은 배수를 제거할 숫자를 포함하며 두 번째 목록은 숫자를 제거할 목록입니다. 다음 예의 코드에서는 이 재귀 함수를 사용하여 목록에서 소수가 아닌 숫자를 모두 삭제해 소수만 포함된 목록을 생성합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1308.fs)]

출력은 다음과 같습니다.

```console
Primes Up To 100:
[2; 3; 5; 7; 11; 13; 17; 19; 23; 29; 31; 37; 41; 43; 47; 53; 59; 61; 67; 71; 73; 79; 83; 89; 97]
```

## <a name="module-functions"></a>모듈 함수

[목록 모듈](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788) 은 목록의 요소에 액세스 하는 함수를 제공 합니다. 가장 빠르고 쉽게 액세스할 수 있는 요소는 헤드 요소입니다. 속성 [head](https://msdn.microsoft.com/library/5f9414fd-6bdb-470a-8b72-40016db30740) 또는 모듈 함수 [List. head](https://msdn.microsoft.com/library/22514cc5-0511-498b-a2cc-837b688a6da2)를 사용 합니다. [Tail 속성 또는](https://msdn.microsoft.com/library/2a6f8eb9-dc32-41aa-8b62-2baffaface91) [list. tail](https://msdn.microsoft.com/library/da0a0638-4420-4571-84b6-d09ae601f601) 함수를 사용 하 여 목록의 꼬리 부분에 액세스할 수 있습니다. 인덱스를 기준으로 요소를 찾으려면 [List. n a n](https://msdn.microsoft.com/library/1f717d57-89be-4007-a971-9cf5a28d83b1) 함수를 사용 합니다. `List.nth`는 목록을 트래버스하므로 따라서 O (*n*)입니다. 코드에서 `List.nth`를 자주 사용하는 경우 목록 대신 배열을 사용해볼 수 있습니다. 배열의 요소 액세스는 O(1)입니다.

### <a name="boolean-operations-on-lists"></a>목록에 대한 부울 작업

[IsEmpty](https://msdn.microsoft.com/library/a7941d44-9e92-427c-b806-c378f4558107) 함수는 목록에 요소가 있는지 여부를 확인 합니다.

[Exists](https://msdn.microsoft.com/library/15a3ebd5-98f0-44c0-8220-7dedec3e68a8) 함수는 목록 요소에 부울 테스트를 적용 하 고, 어떤 요소가 테스트 `true` 를 충족 하는지 여부를 반환 합니다. [Array.exists2](https://msdn.microsoft.com/library/7532b39e-3f4f-4534-a60b-d7721dc6fa7e) 는 유사 하지만 두 목록에서 연속 되는 요소 쌍에 대해 작동 합니다.

다음 코드는 `List.exists`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet1.fs)]

출력은 다음과 같습니다.

```console
For list [0; 1; 2; 3], contains zero is true
```

다음 예에서는 `List.exists2`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet2.fs)]

출력은 다음과 같습니다.

```console
Lists [1; 2; 3; 4; 5] and [5; 4; 3; 2; 1] have at least one equal element at the same position.
```

목록의 모든 요소가 조건을 충족 하는지 여부를 테스트 하려는 경우 forall를 사용할 수 있습니다 [.](https://msdn.microsoft.com/library/e11a5233-d612-40ac-833b-d5cf496900b7)

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet3.fs)]

출력은 다음과 같습니다.

```console
true
false
```

마찬가지로 [list.forall2](https://msdn.microsoft.com/library/bb611f02-8277-48f5-9af3-6194ae27d07e) 는 두 목록의 해당 위치에 있는 모든 요소가 각 요소 쌍을 포함 하는 부울 식을 만족 하는지 여부를 확인 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet4.fs)]

출력은 다음과 같습니다.

```console
true
false
```

### <a name="sort-operations-on-lists"></a>목록에 대한 정렬 작업

[List. sort](https://msdn.microsoft.com/library/17f1030e-aa7e-41dd-94ea-72cb6c04fd3d), [sortBy](https://msdn.microsoft.com/library/955bfc5f-ad9c-4f2d-a7ab-91e43eb21359)및 lists는 함수 정렬 목록을 [사용](https://msdn.microsoft.com/library/1d806a54-9166-4198-906d-15101f7916c7) 합니다. 정렬 함수는 이 세 함수 중 사용할 함수를 결정합니다. `List.sort`는 기본 제네릭 비교를 사용합니다. 제네릭 비교에서는 제네릭 비교 함수를 기반으로 전역 연산자를 사용해 값을 비교합니다. 이 함수는 단순한 숫자 형식, 튜플, 레코드, 구분된 공용 구조체, 목록, 배열, 그리고 `System.IComparable`을 구현하는 모든 형식과 같은 광범위한 요소 형식에서 효율적으로 작동합니다. `System.IComparable`을 구현하는 형식의 경우 제네릭 비교에서는 `System.IComparable.CompareTo()` 함수를 사용합니다. 제네릭 비교는 문자열에도 작동하지만 이 경우에는 문화권과 독립적인 정렬 순서를 사용합니다. 함수 형식 등의 지원되지 않는 형식에는 제네릭 비교를 사용하면 안 됩니다. 또한 기본 제네릭 비교의 성능은 작은 구조의 형식에서 가장 우수합니다. 자주 비교하고 정렬해야 하는 큰 구조의 형식에 대해서는 `System.IComparable`을 구현하고 효율적인 `System.IComparable.CompareTo()` 메서드 구현을 제공하는 것이 좋습니다.

`List.sortBy`는 정렬 기준으로 사용되는 값을 반환하는 함수를 사용하며 `List.sortWith`는 비교 함수를 인수로 사용합니다. 비교를 지원하지 않는 형식으로 작업 중이거나 비교 시 문화권 인식 문자열과 같이 보다 복잡한 비교 의미 체계를 사용할 때는 이 두 함수가 유용합니다.

다음 예에서는 `List.sort`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet5.fs)]

출력은 다음과 같습니다.

```console
[-2; 1; 4; 5; 8]
```

다음 예에서는 `List.sortBy`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet6.fs)]

출력은 다음과 같습니다.

```console
[1; -2; 4; 5; 8]
```

다음 예에서는 `List.sortWith`의 사용법을 보여줍니다. 이 예에서는 사용자 지정 비교 함수 `compareWidgets`를 사용하여 먼저 사용자 지정 형식의 한 필드를 비교한 다음 첫 필드의 값이 같으면 다른 필드를 비교합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet7.fs)]

출력은 다음과 같습니다.

```console
[{ID = 92;
Rev = 1;}; {ID = 92;
Rev = 1;}; {ID = 100;
Rev = 2;}; {ID = 100;
Rev = 5;}; {ID = 110;
Rev = 1;}]
```

### <a name="search-operations-on-lists"></a>목록에 대한 검색 작업

목록에는 다양한 검색 작업이 지원됩니다. 가장 간단한 [List. find](https://msdn.microsoft.com/library/0594593e-9c75-44c1-8f5a-a37b2e561c06)를 사용 하면 지정 된 조건과 일치 하는 첫 번째 요소를 찾을 수 있습니다.

다음 코드 예제에서는 `List.find`를 사용하여 목록에서 5로 나눌 수 있는 첫 번째 숫자를 찾습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet8.fs)]

해당 결과는 5입니다.

요소를 먼저 변환해야 하는 경우에는 [옵션을 반환하는](https://msdn.microsoft.com/library/0430b515-7fe4-49a1-a616-d2286d8b08b2) 함수를 사용 하고 첫 번째 옵션 값 `Some(x)`을 검색하는 pick를 호출합니다. `List.pick`은 요소를 반환하는 대신 `x` 결과를 반환합니다. 일치하는 요소가 없으면 `List.pick`은 `System.Collections.Generic.KeyNotFoundException`을 throw합니다. 다음 코드는 `List.pick`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet9.fs)]

출력은 다음과 같습니다.

```console
"b"
```

다른 검색 작업 그룹인 [\Find ](https://msdn.microsoft.com/library/37f4532e-9fd0-4802-8bbd-e1aa2380287d) 및 관련 함수는 옵션 값을 반환합니다. `List.tryFind` 함수는 조건을 만족하는 목록의 첫 번째 요소가 있으면 해당 요소를 반환하고 요소가 없으면 옵션 값 `None`을 반환합니다. 변형 [목록. tryFindIndex](https://msdn.microsoft.com/library/5e31968c-c3d3-43d2-859a-0526825895ec) 는 요소 자체가 아닌 요소 (있는 경우)의 인덱스를 반환 합니다. 다음 코드에서는 이러한 함수를 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet10.fs)]

출력은 다음과 같습니다.

```console
The first even value is 22.
The first even value is at position 8.
```

### <a name="arithmetic-operations-on-lists"></a>목록에 대한 산술 연산

합계 및 평균과 같은 일반적인 산술 연산은 [목록 모듈](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)에 기본 제공 됩니다. [List. sum](https://msdn.microsoft.com/library/54d47fe3-5ecf-4883-beb5-e915342a17f9)을 사용 하려면 목록 요소 형식이 연산자를 `+` 지원 하 고 값이 0 이어야 합니다. 모든 기본 제공 연산 형식은 이러한 조건을 만족합니다. [Average](https://msdn.microsoft.com/library/2b9a627b-106d-4548-8c4c-ab5058b8f8e1)를 사용 하 여 작업 하려면 요소 형식이 나머지 없이 나누기를 지원 해야 합니다 .이는 정수 형식을 제외 하지만 부동 소수점 형식을 허용 합니다. [List. sumBy](https://msdn.microsoft.com/library/b7623389-0fe1-4762-9c67-51079903ab7d) 및 [array.averageby](https://msdn.microsoft.com/library/936cc9ec-62af-464d-8726-7999c2f48403) 함수는 함수를 매개 변수로 사용 하며,이 함수의 결과는 합계 또는 평균 값을 계산 하는 데 사용 됩니다.

다음 코드는 `List.sum`, `List.sumBy` 및 `List.average`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet11.fs)]

출력은 `1.000000`입니다.

다음 코드는 `List.averageBy`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet12.fs)]

출력은 `5.5`입니다.

### <a name="lists-and-tuples"></a>목록 및 튜플

튜플을 포함하는 목록은 zip 및 unzip 함수를 통해 조작할 수 있습니다. 이러한 함수는 단일 값의 두 목록을 튜플 목록 하나로 결합하거나 튜플 목록 하나를 단일 값의 두 목록으로 분리합니다. 가장 간단한 [.zip](https://msdn.microsoft.com/library/3028d790-8f48-4c94-bf08-b058bec3689c) 함수는 두 개의 단일 요소로 이루어진 목록을 사용 하 고 단일 튜플 쌍 목록을 생성 합니다. 또 다른 버전인 [list.zip3](https://msdn.microsoft.com/library/003cc28e-0de3-4d99-89ed-cb19028e3c5b)는 단일 요소 목록 세 개를 사용 하 고 세 개의 요소가 있는 튜플 목록을 하나 생성 합니다. 다음 코드 예제에서는 `List.zip`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet13.fs)]

출력은 다음과 같습니다.

```console
[(1, -1); (2, -2); (3; -3)]
```

다음 코드 예제에서는 `List.zip3`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet14.fs)]

출력은 다음과 같습니다.

```console
[(1, -1, 0); (2, -2, 0); (3, -3, 0)]
```

해당 하는 압축 풀기 버전 (list.unzip3 및 [목록](https://msdn.microsoft.com/library/43078c77-32ec-4342-85b3-c31ccf984db4))은 튜플에 있는 튜플 및 반환 목록 목록을 사용 합니다. 여기서 첫 번째 목록에는 각 튜플의 첫 번째 요소를 포함 하 고 두 번째 목록에는 각각의 두 번째 요소가 포함 됩니다 [.](https://msdn.microsoft.com/library/639db80c-41b5-45bb-a6b4-1eaa04d61d21) 튜플을 설정 합니다.

다음 코드 예제에서는 [List. 압축](https://msdn.microsoft.com/library/639db80c-41b5-45bb-a6b4-1eaa04d61d21)해제를 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet15.fs)]

출력은 다음과 같습니다.

```console
([1; 3], [2; 4])
[1; 3] [2; 4]
```

다음 코드 예제에서는 [list.unzip3](https://msdn.microsoft.com/library/43078c77-32ec-4342-85b3-c31ccf984db4)를 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet16.fs)]

출력은 다음과 같습니다.

```console
([1; 4], [2; 5], [3; 6])
```

### <a name="operating-on-list-elements"></a>목록 요소에 대한 작업

F#에서는 목록 요소에 대한 여러 작업을 지원합니다. 가장 간단한 방법은 목록의 모든 요소에 대해 함수를 호출할 수 있도록 하는 [iter입니다.](https://msdn.microsoft.com/library/f778d075-81a9-4994-af60-cddcc53a201f) 변형 include [list.iter2](https://msdn.microsoft.com/library/ea3b7761-916c-4016-9bd8-651124c98b40)를 사용 하면 각 요소의 인덱스가 각각에 대해 호출 되는 함수에 인수로 전달 되는 경우를 `List.iter`제외하고는 두 목록의 요소에 대 한 작업을 수행할 수 있습니다. [list.iteri](https://msdn.microsoft.com/library/6dd21ae6-5c00-41cd-8306-821e513d8f60). 요소 및 `List.iter2`및`List.iteri`의 기능을 조합한 [list.iteri2](https://msdn.microsoft.com/library/9658d740-9be5-4bf7-b663-c8ab2b3e196c). 다음 코드 예제에서는 이러한 함수를 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet17.fs)]

출력은 다음과 같습니다.

```console
List.iter: element is 1
List.iter: element is 2
List.iter: element is 3
List.iteri: element 0 is 1
List.iteri: element 1 is 2
List.iteri: element 2 is 3
List.iter2: elements are 1 4
List.iter2: elements are 2 5
List.iter2: elements are 3 6
List.iteri2: element 0 of list1 is 1; element 0 of list2 is 4
List.iteri2: element 1 of list1 is 2; element 1 of list2 is 5
List.iteri2: element 2 of list1 is 3; element 2 of list2 is 6
```

자주 사용 되는 또 다른 함수는 목록 요소를 변환 하는 [목록입니다. map](https://msdn.microsoft.com/library/c6b49c99-d4f3-4ba3-b1d0-85a312683dc6)을 사용 하면 목록의 각 요소에 함수를 적용 하 고 모든 결과를 새 목록에 넣을 수 있습니다. [Array.map2](https://msdn.microsoft.com/library/5f48cce7-6eaf-4e54-8996-2b04d3c31e57) 및 [list.map3](https://msdn.microsoft.com/library/dd9fb190-6980-4537-be96-5645a64908f8) 는 여러 목록을 사용 하는 변형입니다. [Array.mapi2 및 list.](https://msdn.microsoft.com/library/680643af-233c-40a3-82f2-43d5af27ec49)를 사용할 수도 [있습니다. 요소](https://msdn.microsoft.com/library/284b9234-3d26-409b-b328-ac79638d9e14) 외에도 함수는 각 요소의 인덱스를 전달 해야 합니다. `List.mapi2`와 `List.mapi`의 차이점은 `List.mapi2`의 경우 목록 두 개를 사용한다는 것뿐입니다. 다음 예에서는 [map](https://msdn.microsoft.com/library/c6b49c99-d4f3-4ba3-b1d0-85a312683dc6)을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet18.fs)]

출력은 다음과 같습니다.

```console
[2; 3; 4]
```

다음 예에서는 `List.map2`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet19.fs)]

출력은 다음과 같습니다.

```console
[5; 7; 9]
```

다음 예에서는 `List.map3`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet20.fs)]

출력은 다음과 같습니다.

```console
[7; 10; 13]
```

다음 예에서는 `List.mapi`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet21.fs)]

출력은 다음과 같습니다.

```console
[1; 3; 5]
```

다음 예에서는 `List.mapi2`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet22.fs)]

출력은 다음과 같습니다.

```console
[0; 7; 18]
```

Lists `List.map` [는와 유사 합니다. 단](https://msdn.microsoft.com/library/cd08bbc7-a3b9-40ab-8c20-4e85ec84664f) , 각 요소는 목록을 생성 하 고 이러한 모든 목록은 최종 목록에 연결 됩니다. 다음 코드에서는 목록의 각 요소가 숫자 3개를 생성합니다. 이러한 숫자는 모두 목록 하나에 수집됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet23.fs)]

출력은 다음과 같습니다.

```console
[1; 2; 3; 2; 4; 6; 3; 6; 9]
```

부울 조건을 사용 하 고 지정 된 조건을 충족 하는 요소로만 구성 된 새 목록을 생성 하는 [list. filter](https://msdn.microsoft.com/library/11a8c926-547b-44dd-bbae-98d44f3dd248)를 사용할 수도 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet24.fs)]

그러면 `[2; 4; 6]` 목록이 생성됩니다.

지도와 필터 [목록의 조합입니다 .를 선택](https://msdn.microsoft.com/library/2e21d3fb-ce35-4824-8a57-c4404616093d) 하면 요소를 동시에 변환 하 고 선택할 수 있습니다. `List.choose`는 목록의 각 요소에 대한 옵션을 반환하는 함수를 적용하고, 함수가 옵션 값 `Some`을 반환하면 요소에 대해 새 결과 목록을 반환합니다.

다음 코드는 `List.choose`를 사용하여 단어 목록에서 대문자로 표기된 단어를 선택하는 방법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet25.fs)]

출력은 다음과 같습니다.

```console
["Rome's"; "Bob's"]
```

### <a name="operating-on-multiple-lists"></a>여러 목록에 대한 작업

여러 목록을 연결할 수 있습니다. 두 목록을 하나로 조인 하려면 [List. append](https://msdn.microsoft.com/library/2954da80-3f4a-4a4b-9371-794645c03426)를 사용 합니다. 세 개 이상의 목록을 조인 하려면 [concat](https://msdn.microsoft.com/library/c5afd433-8764-4ea8-a6a8-937fb4d77c4c)를 사용 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet26.fs)]

### <a name="fold-and-scan-operations"></a>접기 및 검사 작업

모든 목록 요소가 상호 종속되어야 하는 목록 작업도 있습니다. 접기 및 검사 작업은 각 요소 `List.iter` 에서 `List.map` 함수를 호출 하는 및와 유사 하지만 이러한 연산은 계산을 통해 정보를 전달 하는 *누적기* 라는 추가 매개 변수를 제공 합니다.

목록에 대해 계산을 수행하려면 `List.fold`를 사용합니다.

다음 코드 예제에서는 [List. 접기](https://msdn.microsoft.com/library/c272779e-bae7-4983-8d7f-16b345bb33a0) 를 사용 하 여 다양 한 작업을 수행 하는 방법을 보여 줍니다.

이 함수는 목록을 트래버스합니다. 누적기 `acc`는 계산이 진행되면서 전달되는 값입니다. 첫 번째 인수는 누적기와 목록 요소를 사용하여 해당 목록 요소에 대한 계산의 중간 결과를 반환합니다. 두 번째 인수는 누적기의 초기 값입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet27.fs)]

이러한 함수 중 함수 이름에 숫자가 있는 버전은 둘 이상의 목록에 대해 작동합니다. 예를 들어 [list.fold2](https://msdn.microsoft.com/library/6cfcd043-a65d-4423-805a-2ab234cb5343) 는 두 개의 목록에서 계산을 수행 합니다.

다음 예에서는 `List.fold2`의 사용법을 보여줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet28.fs)]

`List.fold`및 [List. scan](https://msdn.microsoft.com/library/21f636db-885c-4a72-970e-e3841f33a1b8) `List.fold` 은 추가 매개 변수의 최종 값을 반환 하지만 `List.scan` 추가 매개 변수의 최종 값과 함께 중간 값의 목록을 반환 합니다.

이러한 각 함수에는 목록이 트래버스 되는 순서와 인수의 순서와 다른 역방향 변형 (예: [foldBack](https://msdn.microsoft.com/library/b9a58e66-efe1-445f-a90c-ac9ffb9d40c7))이 포함 되어 있습니다. 또한 및 `List.fold` `List.foldBack` 에는 동일한 길이의 두 목록을 사용 하는 [list.fold2](https://msdn.microsoft.com/library/6cfcd043-a65d-4423-805a-2ab234cb5343) 및 [array.foldback2](https://msdn.microsoft.com/library/56371d3e-5271-4183-9e8c-15a02eda9aa2)변형이 있습니다. 각 요소에 대해 실행되는 함수는 두 목록의 해당 요소를 사용하여 일부 작업을 수행할 수 있습니다. 다음 예에서와 같이 두 목록의 요소 형식은 다를 수 있습니다. 여기서 한 목록은 은행 계좌의 거래 금액을 포함하고 다른 목록은 거래 형식(입금 또는 출금)을 포함합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet29.fs)]

합계와 같은 계산의 경우 `List.fold` 및 `List.foldBack`을 사용해도 결과는 동일합니다. 트래버스 순서에 따라 결과가 달라지지 않기 때문입니다. 다음 예에서는 `List.foldBack`을 사용하여 목록에 요소를 추가합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet30.fs)]

다음 예에서는 은행 계좌 예로 다시 돌아옵니다. 이번에는 새로운 거래 형식인 이자 계산을 추가합니다. 따라서 최종 잔액은 거래 순서에 따라 달라집니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet34.fs)]

함수 [목록. 감소](https://msdn.microsoft.com/library/048e1f95-691b-49cb-bb99-fb85f68f3d8b) 는 및 `List.scan`와 유사 `List.fold` 합니다. 단, 별도의 누적기를 전달 하는 대신 `List.reduce` 요소 형식의 두 인수를 사용 하는 함수를 사용 하 고 그 중 하나를 사용 합니다. 인수는 계산의 중간 결과를 저장 하는 누적기의 역할을 합니다. `List.reduce`는 먼저 처음 두 목록 요소에 대해 실행된 후 해당 작업의 결과를 다음 요소와 함께 사용합니다. 고유한 형식이 지정된 별도의 누적기가 없으므로 `List.reduce`는 누적기와 요소 형식이 같을 때만 `List.fold` 대신 사용할 수 있습니다. 다음 코드는 `List.reduce`의 사용법을 보여줍니다. 제공된 목록에 요소가 없으면 `List.reduce`는 예외를 throw합니다.

다음 코드에서는 첫 번째 람다 식 호출에 인수 2와 4가 사용되며 결과로 6이 반환됩니다. 그 다음 호출에는 인수 6과 10이 사용되며 결과로 16이 반환됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lists/snippet33.fs)]

### <a name="converting-between-lists-and-other-collection-types"></a>목록과 기타 컬렉션 형식 간 변환

`List` 모듈은 시퀀스와 배열 간 변환을 위한 함수를 제공합니다. 시퀀스에서 또는 시퀀스로 변환 하려면 [list. toseq](https://msdn.microsoft.com/library/7024be4b-ee70-43cc-8d0a-e6564a4ff7c0) 또는 [List. ofseq](https://msdn.microsoft.com/library/74ab9289-4a59-4433-92eb-3f662d7f7db0)를 사용 합니다. 배열과 변환 하려면 [list. toArray](https://msdn.microsoft.com/library/ac87dd82-a0cd-40b3-b1fa-dd3168134547) 또는 [List. ofarray](https://msdn.microsoft.com/library/f4bddc26-8c8f-4307-a6d7-a49dceb97032)를 사용 합니다.

### <a name="additional-operations"></a>추가 작업

목록의 추가 작업에 대 한 자세한 내용은 라이브러리 참조 항목 [컬렉션. 목록 모듈](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.list-module-%5bfsharp%5d)을 참조 하세요.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [F# 형식](fsharp-types.md)
- [시퀀스](sequences.md)
- [배열](arrays.md)
- [옵션](options.md)
