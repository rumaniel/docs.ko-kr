---
title: 측정 단위
description: 의 부동 소수점 및 부호 있는 정수 값에 F# 일반적으로 길이, 볼륨 및 질량을 나타내는 데 사용 되는 관련 측정 단위를 사용할 수 있는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: a81f7760301dc580e333d4659a72e6259d2c916b
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216681"
---
# <a name="units-of-measure"></a>측정 단위

의 부동 소수점 및 부호 있는 정수 F# 값에는 일반적으로 길이, 볼륨, 질량 등을 나타내는 데 사용 되는 관련 측정 단위가 있을 수 있습니다. 단위가 포함 된 수량을 사용 하면 컴파일러에서 산술 관계의 단위가 올바른지 확인 하 여 프로그래밍 오류를 방지할 수 있습니다.

## <a name="syntax"></a>구문

```fsharp
[<Measure>] type unit-name [ = measure ]
```

## <a name="remarks"></a>설명

위의 구문은 *단위 이름을* 측정 단위로 정의 합니다. 선택적 부분은 이전에 정의 된 단위를 기준으로 새 측정값을 정의 하는 데 사용 됩니다. 예를 들어 다음 줄은 측정값 `cm` (센티미터)을 정의 합니다.

```fsharp
[<Measure>] type cm
```

다음 줄은 measure `ml` (milliliter)를 입방 센티미터 (`cm^3`)로 정의 합니다.

```fsharp
[<Measure>] type ml = cm^3
```

이전 구문에서 *측정값* 은 단위를 포함 하는 수식입니다. 단위를 포함 하는 수식에서 정수 거듭제곱이 지원 됩니다 (긍정 및 부정). 단위 사이의 공백은 두 단위의 `*` 곱을 나타내고 단위 곱을 `/` 나타내며 단위의 몫을 나타냅니다. 역 단위의 경우 음의 정수 거듭제곱을 사용 하거나 단위 수식의 분자와 분모를 `/` 구분 하는을 사용할 수 있습니다. 분모의 여러 단위는 괄호로 묶어야 합니다. 뒤 `/` 에 공백으로 구분 된 단위는 분모의 일부로 해석 되지만 뒤에 `*` 오는 단위는 분자의 일부로 해석 됩니다.

단위 식에 1을 사용 하 여 dimensionless 수량을 나타내거나 분자와 같이 다른 단위를 함께 사용할 수 있습니다. 예를 들어 rate의 단위는로 `1/s`작성 됩니다. 여기서 `s` 은 초를 나타냅니다. 단위 수식에는 괄호가 사용 되지 않습니다. 단위 수식에는 숫자 변환 상수를 지정 하지 않습니다. 그러나 단위를 사용 하 여 변환 상수를 별도로 정의 하 고 단위 검사 계산에 사용할 수 있습니다.

동일한 항목을 의미 하는 단위 수식을 다양 한 방법으로 작성할 수 있습니다. 따라서 컴파일러는 단위 수식을 일관 된 형식으로 변환 합니다. 그러면 음수 거듭제곱을 reciprocals로 변환 하 고, 단위를 단일 분자와 분모로 그룹화 하 고, 분자와 분모의 단위를 alphabetizes.

예를 들어 단위 수식 `kg m s^-2` 와 `m /s s * kg` 는 모두로 `kg m/s^2`변환 됩니다.

부동 소수점 식에서는 측정 단위를 사용 합니다. 관련 측정 단위와 부동 소수점 숫자를 함께 사용 하면 다른 수준의 형식 안전성이 추가 되 고 약한 형식의 부동 소수점 숫자를 사용 하는 경우 수식에서 발생할 수 있는 단위 불일치 오류가 방지 됩니다. 단위를 사용 하는 부동 소수점 식을 작성 하는 경우 식의 단위가 일치 해야 합니다.

다음 예제에 표시 된 것 처럼 꺾쇠 괄호 안의 단위 수식을 사용 하 여 리터럴에 주석을 추가할 수 있습니다.

```fsharp
1.0<cm>
55.0<miles/hour>
```

숫자와 꺾쇠 괄호 사이에는 공백을 두지 않습니다. 그러나 다음 예제와 같이와 같은 `f`리터럴 접미사를 포함할 수 있습니다.

```fsharp
// The f indicates single-precision floating point.
55.0f<miles/hour>
```

이러한 주석은 리터럴의 형식을 기본 형식 (예 `float`:)에서 `float<cm>` 또는 등의 치수화 된 형식 (이 경우 `float<miles/hour>`)으로 변경 합니다. 의 `<1>` 단위 주석은 dimensionless 수량을 나타내며, 해당 형식은 unit 매개 변수가 없는 기본 형식에 해당 합니다.

측정 단위 형식은 괄호 안에 표시 되는 추가 단위 주석과 함께 부동 소수점 또는 부호 있는 정수 계열 형식입니다. 따라서 (그램)에서 `g` (킬로그램)로 `kg` 변환 형식을 작성 하는 경우 다음과 같이 형식을 설명 합니다.

```fsharp
let convertg2kg (x : float<g>) = x / 1000.0<g/kg>
```

측정 단위는 컴파일 시간 단위 검사에 사용 되지만 런타임 환경에서는 유지 되지 않습니다. 따라서 성능에 영향을 주지 않습니다.

측정 단위는 부동 소수점 형식이 아니라 모든 형식에 적용할 수 있습니다. 그러나 부동 소수점 형식, 부호 있는 정수 형식 및 decimal 형식만 차원을 지 원하는 수량을 지원 합니다. 따라서 기본 형식의 측정 단위와 이러한 기본 형식을 포함 하는 집계를 사용 하는 것이 좋습니다.

다음 예에서는 측정 단위를 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6901.fs)]

다음 코드 예제에서는 dimensionless 부동 소수점 숫자에서 치수화 된 부동 소수점 값으로 변환 하는 방법을 보여 줍니다. 1\.0에 곱하여 크기를 1.0에 적용 합니다. 이를와 같은 `degreesFahrenheit`함수로 추상화할 수 있습니다.

또한 dimensionless 부동 소수점 숫자가 필요한 함수에 치수화 된 값을 전달 하는 경우에는 `float` `float` 연산자를 사용 하 여 단위를 취소 하거나로 캐스팅 해야 합니다. 이 예제에서는가 `1.0<degC>` dimensionless 수량을 예상 하기 `printf` 때문 `printf` 에에 대 한 인수를로 나눕니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6902.fs)]

다음 예제 세션에서는에서의 출력과이 코드에 대 한 입력을 보여 줍니다.

```console
Enter a temperature in degrees Fahrenheit.
90
That temperature in degrees Celsius is    32.22.
```

## <a name="using-generic-units"></a>제네릭 단위 사용

연결 된 측정 단위가 있는 데이터에 대해 작동 하는 제네릭 함수를 작성할 수 있습니다. 이 작업을 수행 하려면 다음 코드 예제와 같이 제네릭 단위와 함께 형식을 형식 매개 변수로 지정 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6903.fs)]

## <a name="creating-aggregate-types-with-generic-units"></a>제네릭 단위를 사용 하 여 집계 형식 만들기

다음 코드에서는 일반적인 단위가 있는 개별 부동 소수점 값으로 구성 된 집계 형식을 만드는 방법을 보여 줍니다. 이렇게 하면 다양 한 단위에서 작동 하는 단일 형식을 만들 수 있습니다. 또한 제네릭 단위는 한 단위의 집합을 포함 하는 제네릭 형식이 다른 단위 집합을 가진 동일한 제네릭 형식과 다른 형식 인지 확인 하 여 형식 안전성을 유지 합니다. 이 기술의 기본은 형식 매개 변수에 `Measure` 특성을 적용할 수 있다는 것입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6904.fs)]

## <a name="units-at-runtime"></a>런타임에 단위

측정 단위는 정적 형식 검사에 사용 됩니다. 부동 소수점 값이 컴파일되면 측정 단위가 제거 되므로 단위는 런타임에 손실 됩니다. 따라서 런타임에 단위를 확인 하는 데 종속 된 기능을 구현 하려는 시도는 불가능 합니다. 예를 들어 단위를 `ToString` 출력 하는 함수를 구현 하는 것은 불가능 합니다.

## <a name="conversions"></a>변환

단위가 있는 형식 (예: `float<'u>`)을 단위가 없는 형식으로 변환 하려면 표준 변환 함수를 사용 하면 됩니다. 예를 들어 다음 코드와 `float` 같이를 사용 하 `float` 여 단위가 없는 값으로 변환할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6905.fs)]

단위 없는 값을 단위가 있는 값으로 변환 하려면 적절 한 단위로 주석이 지정 된 값 1 또는 1.0을 곱합니다. 그러나 상호 운용성 계층을 작성 하는 데 사용할 수 있는 몇 가지 명시적인 함수도 있습니다. 단위 값을 단위 값으로 변환 하는 데 사용할 수 있습니다. 이러한 [요소는 fsharp.core](https://msdn.microsoft.com/library/69d08ac5-5d51-4c20-bf1e-850fd312ece3) 모듈에 있습니다. 예를 들어 단위를에서 `float` `float<cm>`로 변환 하려면 다음 코드와 같이 [FloatWithMeasure](https://msdn.microsoft.com/library/69520bc7-d67b-46b8-9004-7cac9646b8d9)를 사용 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6906.fs)]

## <a name="units-of-measure-in-the-f-core-library"></a>F# 핵심 라이브러리의 측정 단위

단위 라이브러리는 `FSharp.Data.UnitSystems.SI` 네임 스페이스에서 사용할 수 있습니다. 하위 네임 스페이스 `m` 의 기호 형식 (예: 미터) `UnitNames` `meter` 과 하위 네임 스페이스의 전체 이름 (예: 미터)에 SI 단위를 포함 합니다. `UnitSymbols`

## <a name="see-also"></a>참고 항목

- [F# 언어 참조](index.md)
