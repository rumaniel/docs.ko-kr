---
title: 숫자 결과 형식 지정 표(C# 참조)
description: C# 표준 숫자 형식 문자열에 대한 자세한 정보
ms.date: 09/20/2018
helpviewer_keywords:
- formatting [C#]
- numeric formatting [C#]
- String.Format method
ms.assetid: 120ba537-4448-4c62-8676-7a8fdd98f496
ms.openlocfilehash: 6f1cb5b49139cf9661e678cfc0ecc884a2749622
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "47863704"
---
# <a name="formatting-numeric-results-table-c-reference"></a>숫자 결과 형식 지정 표(C# 참조)

다음 표에서는 숫자 결과 형식 지정에 대해 지원되는 형식 지정자를 보여 줍니다. 마지막 열의 형식 지정 결과는 “en-US” <xref:System.Globalization.CultureInfo>에 해당합니다.

|형식 지정자|설명|예제|결과|  
|----------------------|-----------------|--------------|------------|  
|C 또는 c|통화|`string s = $"{2.5:C}";`<br /><br /> `string s = $"{-2.5:C}";`|$2.50<br /><br /> ($2.50)|  
|D 또는 d|Decimal|`string s = $"{25:D5}";`|00025|  
|E 또는 e|지수|`string s = $"{250000:E2}";`|2.50E+005|  
|F 또는 f|고정 소수점|`string s = $"{2.5:F2}";`<br /><br /> `string s = $"{2.5:F0}";`|2.50<br /><br /> 3|  
|G 또는 g|일반|`string s = $"{2.5:G}";`|2.5|  
|N 또는 n|Numeric|`string s = $"{2500000:N}";`|2,500,000.00|  
|P 또는 p|백분율|`string s = $"{0.25:P}";`|25.00%|  
|R 또는 r|라운드트립|`string s = $"{2.5:R}";`|2.5|  
|X 또는 x|16진수|`string s = $"{250:X}";`<br /><br /> `string s = $"{0xffff:X}";`|FA<br /><br /> FFFF|  

## <a name="remarks"></a>설명

형식 지정자를 사용하여 형식 문자열을 만듭니다. 형식 문자열은 `Axx` 형식입니다. 여기서 각 요소는 다음을 나타냅니다.

- `A`는 숫자 값에 적용되는 형식 지정의 유형을 제어하는 형식 지정자입니다.
- `xx`는 형식 지정 결과의 자릿수에 영향을 주는 전체 자릿수 지정자입니다. 전체 자릿수 지정자의 값은 0에서 99 사이입니다.

10진수(“D” 또는 “d”) 및 16진수(“X” 또는 “x”) 형식 지정자는 정수 형식에만 지원됩니다. 왕복(“R” 또는 “r”) 형식 지정자는 <xref:System.Single>, <xref:System.Double> 및 <xref:System.Numerics.BigInteger> 형식에만 지원됩니다.

표준 숫자 형식 문자열은 다음에 의해 지원됩니다.

- 모든 숫자 형식의 `ToString` 메서드 중 일부 오버로드. 예를 들어 <xref:System.Int32.ToString%28System.String%29?displayProperty=nameWithType> 및 <xref:System.Int32.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 메서드에 숫자 형식 문자열을 제공할 수 있습니다.

- 예를 들어 <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드에서 지원하는 .NET [복합 형식 지정 기능](../../../standard/base-types/composite-formatting.md)입니다.

- [보간된 문자열](../tokens/interpolated.md).

자세한 내용은 [표준 숫자 형식 문자열](../../../standard/base-types/standard-numeric-format-strings.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [형식 참조 테이블](reference-tables-for-types.md)
- [형식 서식 지정](../../../standard/base-types/formatting-types.md)
- [복합 형식 지정](../../../standard/base-types/composite-formatting.md)
- [문자열 보간](../tokens/interpolated.md)
- [string](string.md)
