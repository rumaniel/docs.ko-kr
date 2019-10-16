---
ms.openlocfilehash: ce4f09908b1025e8e5a0380c9bf035c6b0db479a
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182001"
---
### <a name="floating-point-formatting-and-parsing-behavior-changed"></a>부동 소수점 서식 및 구문 분석 동작 변경됨

이제 부동 소수점 구문 분석 및 서식 동작(<xref:System.Double> 및 <xref:System.Single> 형식 사용)이 IEEE 규격으로 변경되었습니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Core 2.2 및 이전 버전에서는 <xref:System.Double.ToString%2A?displayProperty=nameWithType> 및 <xref:System.Single.ToString%2A?displayProperty=nameWithType>을 사용한 서식과 <xref:System.Double.Parse%2A?displayProperty=nameWithType>, <xref:System.Double.TryParse%2A?displayProperty=nameWithType>, <xref:System.Single.Parse%2A?displayProperty=nameWithType>, <xref:System.Single.TryParse%2A?displayProperty=nameWithType>을 사용한 구문 분석이 IEEE 규격이 아닙니다. 따라서 지원되는 표준 또는 사용자 지정 형식 문자열로 값이 왕복한다고 보장할 수 없습니다. 입력에 따라 서식이 지정된 값을 구문 분석하려는 시도가 실패하는 경우도 있고, 구문 분석된 값이 원래 값과 달라지는 경우도 있습니다.

.NET Core 3.0부터는 구문 분석 및 서식 작업이 IEEE 754 규격입니다. 따라서 .NET의 부동 소수점 형식 동작이 C#과 같은 IEEE 규격 언어의 동작과 일치합니다. 자세한 내용은 [Floating-point parsing and formatting improvements in .NET Core 3.0](https://devblogs.microsoft.com/dotnet/floating-point-parsing-and-formatting-improvements-in-net-core-3-0/)(.NET Core 3.0의 부동 소수점 구문 분석 및 서식 개선 사항)에 대한 블로그 게시물을 참조하세요.

#### <a name="version-introduced"></a>도입된 버전

3.0

#### <a name="recommended-action"></a>권장 작업

[Floating-point parsing and formatting improvements in .NET Core 3.0](https://devblogs.microsoft.com/dotnet/floating-point-parsing-and-formatting-improvements-in-net-core-3-0/)(.NET Core 3.0의 부동 소수점 구문 분석 및 서식 개선 사항) 블로그 게시물의 “기존 코드에 대한 잠재적 영향” 섹션에서는 .NET Core 2.2 애플리케이션과 비교해서 동작이 변경된 경우 코드를 변경하도록 제안합니다. 이 제안을 따르려면 일반적으로 다른 표준 또는 사용자 지정 형식 문자열을 사용하여 필요한 동작을 적용해야 합니다. 이전에 잘못된 일부 결과는 해결 방법이 없을 수도 있습니다.

#### <a name="category"></a>범주

CoreFx

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:System.Double.ToString%2A?displayProperty=nameWithType>
- <xref:System.Single.ToString%2A?displayProperty=nameWithType>
- <xref:System.Double.Parse%2A?displayProperty=nameWithType>
- <xref:System.Double.TryParse%2A?displayProperty=nameWithType>
- <xref:System.Single.Parse%2A?displayProperty=nameWithType>
- <xref:System.Single.TryParse%2A?displayProperty=nameWithType>

<!-- 

### Affected APIs

- `Overload:System.Double.ToString`
- `Overload:System.Single.ToString`
- `Overload:System.Double.Parse`
- `Overload:System.Double.TryParse`
- `Overload:System.Single.Parse`
- `Overload:System.Single.TryParse`

-->
