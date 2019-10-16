---
title: .NET의 숫자
ms.date: 10/18/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- SIMD
- System.Numerics.Vectors
- vectors
- scientific computing
- Complex
- numerics
- BigInteger
ms.assetid: dfebc18e-acde-4510-9fa7-9a0f4aa3bd11
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7f180e459764d6e8e4484072218f01c8bab8a3b5
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50191157"
---
# <a name="numerics-in-net"></a>.NET의 숫자

.NET에서는 다양한 숫자 정수 및 부동 소수점 기본 형식과 <xref:System.Numerics.BigInteger?displayProperty=nameWithType>(이론적 상한 또는 하한이 없는 정수 형식), <xref:System.Numerics.Complex?displayProperty=nameWithType>(복소수) 및 <xref:System.Numerics> 네임스페이스의 SIMD 사용 형식 집합을 제공합니다.
  
## <a name="integer-types"></a>정수 형식

.NET은 다음 표에 나열된 부호 있는/부호 없는 8비트, 16비트, 32비트 및 64비트 정수 형식을 모두 지원합니다.
  
|형식|부호 있음/부호 없음|크기(바이트)|최소값|최대값|  
|----------|----------------------|--------------------|-------------------|-------------------|  
|<xref:System.Byte?displayProperty=nameWithType>|부호 없음|1|0|255|  
|<xref:System.Int16?displayProperty=nameWithType>|서명|2|-32,768|32,767|  
|<xref:System.Int32?displayProperty=nameWithType>|서명|4|-2,147,483,648|2,147,483,647|  
|<xref:System.Int64?displayProperty=nameWithType>|서명|8|-9,223,372,036,854,775,808|9,223,372,036,854,775,807|  
|<xref:System.SByte?displayProperty=nameWithType>|서명|1|-128|127|  
|<xref:System.UInt16?displayProperty=nameWithType>|부호 없음|2|0|65,535|  
|<xref:System.UInt32?displayProperty=nameWithType>|부호 없음|4|0|4,294,967,295|  
|<xref:System.UInt64?displayProperty=nameWithType>|부호 없음|8|0|18,446,744,073,709,551,615|  
  
각 정수 형식은 표준 산술 연산자 집합을 지원합니다. <xref:System.Math?displayProperty=nameWithType> 클래스는 광범위한 수학 함수 집합에 대한 메서드를 제공합니다.

<xref:System.BitConverter?displayProperty=nameWithType> 클래스를 사용하여 정수 값의 개별 비트를 사용할 수도 있습니다.  

> [!NOTE]  
> 부호 없는 정수 형식은 CLS 규격이 아닙니다. 자세한 내용은 [Language Independence and Language-Independent Components](language-independence-and-language-independent-components.md)을 참조하십시오.

## <a name="biginteger"></a>BigInteger

<xref:System.Numerics.BigInteger?displayProperty=nameWithType> 구조체는 이론상 값에 상한이나 하한이 없는 임의로 큰 정수를 나타내는 변경할 수 없는 형식입니다. <xref:System.Numerics.BigInteger> 형식의 메서드는 기타 정수 계열 형식의 메서드와 매우 유사합니다.
  
## <a name="floating-point-types"></a>부동 소수점 형식

.NET에는 다음 표에 나열된 세 가지 기본 부동 소수점 형식이 포함되어 있습니다.
  
|형식|크기(바이트)|근사 범위|전체 자릿수|  
|----------|--------|---------------------|--------------------|  
|<xref:System.Single?displayProperty=nameWithType>|4|±1.5 x 10<sup>−45</sup> ~ ±3.4 x 10<sup>38</sup>|~6-9개 자릿수|  
|<xref:System.Double?displayProperty=nameWithType>|8|±5.0 × 10<sup>−324</sup> ~ ±1.7 × 10<sup>308</sup>|~15-17개 자릿수|  
|<xref:System.Decimal?displayProperty=nameWithType>|16|±1.0 x 10<sup>-28</sup> ~ ±7.9228 x 10<sup>28</sup>|28-29개의 자릿수|  
  
<xref:System.Single> 및 <xref:System.Double> 형식은 숫자가 아니고 무한대임을 나타내는 특수 값을 지원합니다. 예를 들어 <xref:System.Double> 형식은 <xref:System.Double.NaN?displayProperty=nameWithType>, <xref:System.Double.NegativeInfinity?displayProperty=nameWithType> 및 <xref:System.Double.PositiveInfinity?displayProperty=nameWithType>와 같은 값을 제공합니다. <xref:System.Double.IsNaN%2A?displayProperty=nameWithType>, <xref:System.Double.IsInfinity%2A?displayProperty=nameWithType>, <xref:System.Double.IsPositiveInfinity%2A?displayProperty=nameWithType> 및 <xref:System.Double.IsNegativeInfinity%2A?displayProperty=nameWithType> 메서드를 사용하여 이러한 특수 값을 테스트합니다.

각 부동 소수점 형식은 표준 산술 연산자 집합을 지원합니다. <xref:System.Math?displayProperty=nameWithType> 클래스는 광범위한 수학 함수 집합에 대한 메서드를 제공합니다. .NET Core 2.0 이상에는 <xref:System.Single> 형식의 인수를 허용하는 메서드를 제공하는 <xref:System.MathF?displayProperty=nameWithType> 클래스가 포함되어 있습니다.

<xref:System.BitConverter?displayProperty=nameWithType> 클래스를 사용하여 <xref:System.Double> 및 <xref:System.Single> 값의 개별 비트를 사용할 수도 있습니다. <xref:System.Decimal?displayProperty=nameWithType> 구조체에는 10진수 값의 개별 비트를 사용하기 위한 고유한 메서드인 <xref:System.Decimal.GetBits%2A?displayProperty=nameWithType> 및 <xref:System.Decimal.%23ctor%28System.Int32%5B%5D%29?displayProperty=nameWithType>와 몇몇 추가적인 수치 연산을 수행하기 위한 고유한 메서드 집합이 있습니다.
  
<xref:System.Double> 및 <xref:System.Single> 형식은 기본적으로 정확하지 않은 값(예: 두 별 사이의 거리) 및 정밀도가 높고 반올림 오류가 적을 필요 없는 응용 프로그램에 사용해야 합니다. 정밀도가 더 높아야 하고 반올림 오류가 최소화되어야 하는 경우에는 <xref:System.Decimal?displayProperty=nameWithType> 형식을 사용해야 합니다.

> [!NOTE]
> <xref:System.Decimal> 형식을 사용하면 반올림이 필요하지 않습니다. 오히려 반올림으로 인한 오류를 최소화합니다.
  
## <a name="complex"></a>복합

<xref:System.Numerics.Complex?displayProperty=nameWithType> 구조체는 실수 부분과 허수 부분이 포함된 숫자인 복소수를 나타냅니다. 이 형식은 산술, 비교, 같음, 명시적 및 암시적 변환 연산자의 표준 집합과 수치, 대수 및 삼각 메서드를 지원합니다.  
  
## <a name="simd-enabled-types"></a>SIMD 사용 형식

<xref:System.Numerics> 네임스페이스에는 .NET SIMD 사용 형식 집합이 포함됩니다. SIMD(Single Instruction Multiple Data) 작업은 하드웨어 수준에서 병렬 처리할 수 있습니다. 이를 통해 수학, 과학 및 그래픽 앱에서 공통적인 벡터화된 계산의 처리량이 증가합니다.
  
.NET SIMD 사용 형식은 다음과 같습니다.

- <xref:System.Numerics.Vector2>, <xref:System.Numerics.Vector3> 및 <xref:System.Numerics.Vector4> 형식은 2, 3 및 4 <xref:System.Single> 값이 있는 벡터를 나타냅니다.

- 두 가지 행렬 형식이 있습니다. <xref:System.Numerics.Matrix3x2>는 3x2 행렬을 나타내고 <xref:System.Numerics.Matrix4x4>는 4x4 행렬을 나타냅니다.

- <xref:System.Numerics.Plane> 형식은 평면을 3차원 공간으로 나타냅니다.

- <xref:System.Numerics.Quaternion> 형식은 3차원 물리적 회전을 인코드하는 데 사용되는 벡터를 나타냅니다.

- <xref:System.Numerics.Vector%601> 형식은 지정된 숫자 형식의 벡터를 나타내고 SIMD 지원을 활용하는 광범위한 연산자 집합을 제공합니다. <xref:System.Numerics.Vector%601> 인스턴스 개수는 고정되지만 해당 <xref:System.Numerics.Vector%601.Count%2A?displayProperty=nameWithType> 값은 코드가 실행되는 머신의 CPU에 따라 다릅니다.
  > [!NOTE]
  > <xref:System.Numerics.Vector%601> 형식은 .NET Framework에 포함되지 않습니다. 이 형식에 액세스하려면 [System.Numerics.Vectors](https://www.nuget.org/packages/System.Numerics.Vectors) NuGet 패키지를 설치해야 합니다.
  
SIMD 사용 형식은 SIMD 미사용 하드웨어 또는 JIT 컴파일러와 함께 사용할 수 있는 방식으로 구현됩니다. SIMD 지침을 활용하려면 .NET Core 및 .NET Framework 4.6 이상 버전에 포함된 RyuJIT 컴파일러를 사용하는 런타임을 통해 64비트 앱을 실행해야 합니다. 64비트 프로세서를 대상으로 지정할 때 SIMD 지원을 추가합니다.

## <a name="see-also"></a>참고 항목

- [응용 프로그램 주요 사항](application-essentials.md)
- [Standard Numeric Format Strings](base-types/standard-numeric-format-strings.md)
