---
ms.openlocfilehash: 192873aa5069aa4f96a18716afb066c80b223e29
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002452"
---
### <a name="floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception"></a>부동 소수점 구문 분석 작업은 더 이상 실패하거나 OverflowException을 throw하지 않음

부동 소수점 구문 분석 메서드는 더 이상 <xref:System.OverflowException>을 throw하지 않거나, 숫자 값이 <xref:System.Single> 또는 <xref:System.Double> 부동 소수점 형식의 범위를 벗어난 문자열을 구문 분석할 때 `false`를 반환합니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Core 2.2 및 이전 버전에서 <xref:System.Double.Parse%2A?displayProperty=nameWithType> 및 <xref:System.Single.Parse%2A?displayProperty=nameWithType> 메서드는 해당 형식의 범위를 벗어난 값에 대해 <xref:System.OverflowException>를 throw합니다. <xref:System.Double.TryParse%2A?displayProperty=nameWithType> 및 <xref:System.Single.TryParse%2A?displayProperty=nameWithType> 메서드는 범위를 벗어난 숫자 값의 문자열 표현에 대해 `false`를 반환합니다.

.NET Core 3.0부터 범위를 벗어난 숫자 문자열을 구문 분석할 때 <xref:System.Double.Parse%2A?displayProperty=nameWithType>, <xref:System.Double.TryParse%2A?displayProperty=nameWithType>, <xref:System.Single.Parse%2A?displayProperty=nameWithType> 및 <xref:System.Single.TryParse%2A?displayProperty=nameWithType> 메서드가 더 이상 실패하지 않습니다. 대신 <xref:System.Double> 구문 분석 메서드는 <xref:System.Double.MaxValue?displayProperty=nameWithType>를 초과하는 값에 대해 <xref:System.Double.PositiveInfinity?displayProperty=nameWithType>를 반환하고 <xref:System.Double.MinValue?displayProperty=nameWithType>보다 작은 값에 대해 <xref:System.Double.NegativeInfinity?displayProperty=nameWithType>를 반환합니다. 마찬가지로 <xref:System.Single> 구문 분석 메서드는 <xref:System.Single.MaxValue?displayProperty=nameWithType>를 초과하는 값에 대해 <xref:System.Single.PositiveInfinity?displayProperty=nameWithType>를 반환하고 <xref:System.Single.MinValue?displayProperty=nameWithType>보다 작은 값에 대해 <xref:System.Single.NegativeInfinity?displayProperty=nameWithType>를 반환합니다.

이러한 변경은 개정된 IEEE 754:2008 규정 준수를 위해 이루어졌습니다. 

#### <a name="version-introduced"></a>도입된 버전

3.0

#### <a name="recommended-action"></a>권장 작업

이러한 변경 내용은 다음 두 가지 방법 중 하나로 코드에 영향을 줄 수 있습니다.

- 코드는 오버플로가 발생할 때 실행되는 <xref:System.OverflowException>에 대한 처리기에 따라 다릅니다. 이 경우 `catch` 문을 제거하고 <xref:System.Double.IsInfinity%2A?displayProperty=nameWithType> 또는 <xref:System.Single.IsInfinity%2A?displayProperty=nameWithType>가 `true`인지 여부를 테스트하는 `If` 문에 필요한 코드를 넣어야 합니다.

- 코드에서 부동 소수점 값이 `Infinity`가 아니라고 가정합니다. 이 경우 `PositiveInfinity` 및 `NegativeInfinity`의 부동 소수점 값을 확인하는 데 필요한 코드를 추가해야 합니다.

#### <a name="category"></a>범주

CoreFx

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:System.Double.Parse%2A?displayProperty=nameWithType>
- <xref:System.Double.TryParse%2A?displayProperty=nameWithType>
- <xref:System.Single.Parse%2A?displayProperty=nameWithType>
- <xref:System.Single.TryParse%2A?displayProperty=nameWithType>

<!--

### Affected APIs

- `Overload:System.Double.Parse`
- `Overload:System.Double.TryParse`
- `Overload:System.Single.Parse`
- `Overload:System.Single.TryParse`

-->
