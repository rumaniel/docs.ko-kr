---
title: 부동 소수점 숫자 형식 - C# 참조
description: 기본 제공 C# 부동 소수점 형식의 개요
ms.date: 06/30/2019
f1_keywords:
- float
- float_CSharpKeyword
- double
- double_CSharpKeyword
- decimal_CSharpKeyword
- decimal
helpviewer_keywords:
- floating-point numbers [C#]
- ranges of floating-point types [C#]
- size of floating-point types [C#]
- types [C#], floating-point types
- float keyword [C#]
- floating-point numbers [C#], float keyword
- double data type [C#]
- decimal keyword [C#]
ms.openlocfilehash: 17ae154780679dd1f42f43f1ec345cdc722815d3
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002198"
---
# <a name="floating-point-numeric-types-c-reference"></a>부동 소수점 숫자 형식(C# 참조)

**부동 소수점 형식**은 **단순 형식**의 하위 집합이며 [*리터럴*](#floating-point-literals)을 사용하여 초기화할 수 있습니다. 모든 부동 소수점 형식도 값 형식입니다. 모든 부동 소수점 숫자 형식은 [산술](../operators/arithmetic-operators.md), [비교 및 같음](../operators/equality-operators.md) 연산자를 지원합니다.

## <a name="characteristics-of-the-floating-point-types"></a>부동 소수점 형식의 특성

C#은 다음과 같은 미리 정의된 부동 소수점 형식을 지원합니다.
  
|C# 형식/키워드|근사 범위|전체 자릿수|Size|.NET 형식|
|----------|-----------------------|---------------|--------------|--------------|
|`float`|±1.5 x 10<sup>−45</sup> ~ ±3.4 x 10<sup>38</sup>|~6-9개 자릿수|4바이트|<xref:System.Single?displayProperty=nameWithType>|
|`double`|±5.0 × 10<sup>−324</sup> ~ ±1.7 × 10<sup>308</sup>|~15-17개 자릿수|8바이트|<xref:System.Double?displayProperty=nameWithType>|
|`decimal`|±1.0 x 10<sup>-28</sup> ~ ±7.9228 x 10<sup>28</sup>|28-29개의 자릿수|16바이트|<xref:System.Decimal?displayProperty=nameWithType>|

이전 표에서 맨 왼쪽 열의 각 C# 형식 키워드는 해당하는 .NET 형식의 별칭입니다. 서로 교환하여 사용할 수 있습니다. 예를 들어 다음 선언은 동일한 형식의 변수를 선언합니다.

```csharp
double a = 12.3;
System.Double b = 12.3;
```

각 부동 소수점 형식의 기본값은 `0`입니다. 각 부동 소수점 형식에는 해당 형식의 최소 및 최대 유한값을 제공하는 `MinValue` 및 `MaxValue` 상수가 있습니다. 또한 `float` 및 `double` 형식은 숫자가 아닌 무한 값을 나타내는 상수를 제공합니다. 예를 들어 `double` 형식은 <xref:System.Double.NaN?displayProperty=nameWithType>, <xref:System.Double.NegativeInfinity?displayProperty=nameWithType> 및 <xref:System.Double.PositiveInfinity?displayProperty=nameWithType>와 같은 상수를 제공합니다.

`decimal` 형식은 `float` 및 `double`보다 정밀도가 높고 범위가 작으므로 재무 및 통화 계산에 적합합니다.

식에서 [정수](integral-numeric-types.md) 형식과 부동 소수점 형식을 혼합할 수 있습니다. 이 경우 정수 형식이 부동 소수점 형식으로 변환됩니다. 식의 계산은 다음 규칙에 따라 수행됩니다.

- 부동 소수점 형식 중 하나가 `double`인 경우 식은 관계형 비교 및 같음에 대한 비교에서 `double` 또는 [bool](../keywords/bool.md)로 계산됩니다.
- 식에 `double` 형식이 없는 경우 식은 같음에 대한 관계형 비교 또는 비교에서 `float` 또는 [bool](../keywords/bool.md)로 계산됩니다.

부동 소수점 식에는 다음과 같은 값 집합이 포함될 수 있습니다.

- 양수 및 음수 0
- 양수 및 음수 무한대
- NaN(Not-a-Number) 값
- 한정된 0이 아닌 값의 집합

이러한 값에 대한 자세한 내용은 [IEEE](https://www.ieee.org) 웹 사이트에서 제공되는 이진 부동 소수점 연산에 대한 IEEE 표준을 참조하세요.

[표준 숫자 서식 문자열](../../../standard/base-types/standard-numeric-format-strings.md) 또는 [사용자 지정 숫자 서식 문자열](../../../standard/base-types/custom-numeric-format-strings.md)을 사용하여 부동 소수점 값의 형식을 지정할 수 있습니다.

## <a name="floating-point-literals"></a>부동 소수점 리터럴

기본적으로 대입 연산자 오른쪽의 부동 소수점 숫자 리터럴은 `double`로 처리됩니다. 접미사를 사용하여 부동 소수점 또는 정수 리터럴을 특정 형식으로 변환할 수 있습니다.

- `d` 또는 `D` 접미사는 리터럴을 `double`로 변환합니다.
- `f` 또는 `F` 접미사는 리터럴을 `float`로 변환합니다.
- `m` 또는 `M` 접미사는 리터럴을 `decimal`로 변환합니다.

다음 예제는 각 접미사를 보여줍니다.

```csharp
double d = 3D;
d = 4d;
float f = 3.5F;
f = 5.4f;
decimal myMoney = 300.5m;
myMoney = 400.75M;
```

## <a name="conversions"></a>변환

`float` 값의 범위는 `double`의 적절한 하위 집합이고 `float`에서 `double`까지의 정밀도 손실이 없으므로 `float`에서 `double`로의 암시적 변환(*확대 변환*이라고 함)이 있습니다.

암시적 변환이 소스 유형에서 대상 유형으로 정의되지 않은 경우 명시적 캐스트를 사용하여 하나의 부동 소수점 형식을 다른 부동 소수점 형식으로 변환해야 합니다. 이를 *축소 변환*이라고 합니다. 변환이 데이터 손실을 초래할 수 있기 때문에 명시적인 사례가 필요합니다. `decimal` 유형은 `float` 또는 `double`보다 더 높은 정밀도를 가지므로 다른 부동 소수점 형식과 `decimal` 형식 간의 암시적 변환은 없습니다.

암시적 숫자 변환에 대한 자세한 내용은 [암시적 숫자 변환 표](../keywords/implicit-numeric-conversions-table.md)를 참조하세요.

명시적 숫자 변환에 대한 자세한 내용은 [명시적 숫자 변환 표](../keywords/explicit-numeric-conversions-table.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [정수 형식](integral-numeric-types.md)
- [기본 제공 형식 표](../keywords/built-in-types-table.md)
- [.NET의 숫자](../../../standard/numerics.md)
- [캐스팅 및 형식 변환](../../programming-guide/types/casting-and-type-conversions.md)
- [암시적 숫자 변환 표](../keywords/implicit-numeric-conversions-table.md)
- [명시적 숫자 변환 표](../keywords/explicit-numeric-conversions-table.md)
- <xref:System.Numerics.Complex?displayProperty=nameWithType>
- [숫자 결과 형식 지정 표](../keywords/formatting-numeric-results-table.md)
- [Standard Numeric Format Strings](../../../standard/base-types/standard-numeric-format-strings.md)
