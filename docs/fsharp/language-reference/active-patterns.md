---
title: 활성 패턴
description: 활성 패턴을 사용 하 여 F# 프로그래밍 언어로 입력 데이터를 세분 하는 명명 된 파티션을 정의 하는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 0c1315f2386b3cea2def698f4725e4c1cf030609
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083074"
---
# <a name="active-patterns"></a>활성 패턴

*활성 패턴* 을 사용 하면 입력 데이터를 구분 하는 명명 된 파티션을 정의할 수 있으므로 구분 된 공용 구조체의 경우와 마찬가지로 패턴 일치 식에 이러한 이름을 사용할 수 있습니다. 활성 패턴을 사용하여 각 파티션에 대한 사용자 지정 방식으로 데이터를 분해할 수 있습니다.

## <a name="syntax"></a>구문

```fsharp
// Active pattern of one choice.
let (|identifier|) [arguments] valueToMatch= expression

// Active Pattern with multiple choices.
// Uses a FSharp.Core.Choice<_,...,_> based on the number of case names. In F#, the limitation n <= 7 applies.
let (|identifer1|identifier2|...|) valueToMatch = expression

// Partial active pattern definition.
// Uses a FSharp.Core.option<_> to represent if the type is satisfied at the call site.
let (|identifier|_|) [arguments ] valueToMatch = expression
```

## <a name="remarks"></a>설명

이전 구문에서 식별자는 *인수로*표시 되는 입력 데이터의 파티션에 대 한 이름입니다. 즉, 인수 값 집합의 하위 집합에 대 한 이름입니다. 활성 패턴 정의에는 최대 7 개의 파티션이 있을 수 있습니다. *식은* 데이터를 분해할 폼을 설명 합니다. 활성 패턴 정의를 사용 하 여 인수로 지정 된 값이 속하는 명명 된 파티션을 결정 하는 규칙을 정의할 수 있습니다. (| 및 |) 기호를 *바나나 클립* 이라고 하며이 유형의 let 바인딩을 통해 만든 함수를 *활성 인식기*라고 합니다.

예를 들어 인수를 사용 하는 다음 활성 패턴을 고려 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5001.fs)]

다음 예제와 같이 패턴 일치 식에 활성 패턴을 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5002.fs)]

이 프로그램의 출력은 다음과 같습니다.

```console
7 is odd
11 is odd
32 is even
```

활성 패턴의 또 다른 용도는 동일한 기본 데이터에 가능한 여러 표현이 있는 경우와 같이 여러 가지 방법으로 데이터 형식을 분해 하는 것입니다. 예를 들어 개체 `Color` 를 RGB 표현 또는 HSB 표현으로 분해할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5003.fs)]

위의 프로그램의 출력은 다음과 같습니다.

```console
Red
 Red: 255 Green: 0 Blue: 0
 Hue: 360.000000 Saturation: 1.000000 Brightness: 0.500000
Black
 Red: 0 Green: 0 Blue: 0
 Hue: 0.000000 Saturation: 0.000000 Brightness: 0.000000
White
 Red: 255 Green: 255 Blue: 255
 Hue: 0.000000 Saturation: 0.000000 Brightness: 1.000000
Gray
 Red: 128 Green: 128 Blue: 128
 Hue: 0.000000 Saturation: 0.000000 Brightness: 0.501961
BlanchedAlmond
 Red: 255 Green: 235 Blue: 205
 Hue: 36.000000 Saturation: 1.000000 Brightness: 0.901961
```

이러한 두 가지 방법을 함께 사용 하면 활성 패턴을 사용 하 여 데이터를 적절 한 형식으로 분할 및 분해 하 고 계산에 가장 편리한 형태로 적절 한 데이터에 대 한 적절 한 계산을 수행할 수 있습니다.

결과 패턴 일치 식을 사용 하면 매우 쉽게 읽을 수 있는 편리한 방식으로 데이터를 작성 하 여 복잡 한 분기 및 데이터 분석 코드를 크게 간소화할 수 있습니다.

## <a name="partial-active-patterns"></a>부분 활성 패턴

경우에 따라 입력 공간의 일부만 분할 해야 합니다. 이 경우 일부 입력을 일치 하지만 다른 입력과 일치 하지 않는 partial 패턴 집합을 작성 합니다. 항상 값을 생성 하지 않는 활성 패턴을 *부분 활성 패턴*이라고 합니다. 이러한 값에는 옵션 유형인 반환 값이 있습니다. 부분 활성 패턴을 정의 하려면 바나나 클립 내부의 패턴 목록 끝에\_와일드 카드 문자 ()를 사용 합니다. 다음 코드에서는 부분 활성 패턴을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5004.fs)]

이전 예제의 출력은 다음과 같습니다.

```console
1.100000 : Floating point
0 : Integer
0.000000 : Floating point
10 : Integer
Something else : Not matched.
```

부분 활성 패턴을 사용 하는 경우 개별 선택 항목은 분리 되거나 함께 사용할 수 없지만 그렇지 않아도 됩니다. 다음 예에서는 일부 숫자가 사각형과 큐브 (예: 64) 이기 때문에 패턴 사각형과 패턴 큐브는 비연속이 아닙니다. 다음 프로그램에서는 및 패턴을 사용 하 여 사각형과 큐브 패턴을 결합 합니다. 사각형 및 큐브와 큐브와 큐브와 같은 모든 1000 정수를 출력 합니다 .이는 큐브 전용입니다. 

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5005.fs)]

출력은 다음과 같습니다.

```console
1 is a cube and a square
8 is a cube
27 is a cube
64 is a cube and a square
125 is a cube
216 is a cube
343 is a cube
512 is a cube
729 is a cube and a square
1000 is a cube
```

## <a name="parameterized-active-patterns"></a>매개 변수가 있는 활성 패턴

활성 패턴은 항상 일치 하는 항목에 대 한 인수를 하나 이상 사용 하지만 추가 인수도 사용할 수 있습니다 .이 경우에는 이름 *매개 변수가 있는 활성 패턴이* 적용 됩니다. 추가 인수를 사용 하면 일반 패턴을 특수화할 수 있습니다. 예를 들어, 정규식을 사용 하 여 문자열을 구문 분석 하는 활성 패턴은 다음 코드와 같이 정규식을 추가 매개 변수로 포함 하는 경우가 많습니다 .이 코드 `Integer` 는 앞의 코드 예제에서 정의 된 부분 활성 패턴도 사용 합니다. 이 예제에서는 일반 ParseRegex 활성 패턴을 사용자 지정 하기 위해 다양 한 날짜 형식에 정규식을 사용 하는 문자열을 제공 합니다. 정수 활성 패턴은 일치 하는 문자열을 DateTime 생성자에 전달할 수 있는 정수로 변환 하는 데 사용 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5006.fs)]

이전 코드의 출력은 다음과 같습니다.

```console
12/22/2008 12:00:00 AM 1/1/2009 12:00:00 AM 1/15/2008 12:00:00 AM 12/28/1995 12:00:00 AM
```

활성 패턴은 패턴 일치 식 으로만 제한 되지 않으며 let 바인딩에서 사용할 수도 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5007.fs)]

이전 코드의 출력은 다음과 같습니다.

```console
Hello, random citizen!
Hello, George!
```

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [일치 식](match-expressions.md)
