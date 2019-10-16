---
title: 표준 숫자 형식 문자열
ms.date: 06/10/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- numeric format strings [.NET Framework]
- formatting [.NET Framework], numbers
- standard format strings, numeric
- format strings
- numbers [.NET Framework], formatting
- format specifiers, numeric
- standard numeric format strings
- formatting numbers [.NET Framework]
- format specifiers, standard numeric format strings
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b2f997cf398e59f8e30ac87c1e0360e43a448e85
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216714"
---
# <a name="standard-numeric-format-strings"></a>표준 숫자 형식 문자열

표준 숫자 서식 문자열은 일반 숫자 형식의 서식을 지정하는 데 사용됩니다. 표준 숫자 서식 문자열은 `Axx` 형식을 취합니다. 여기서

- `A`는 *서식 지정자*라는 단일 영문자입니다. 공백을 포함하여 영문자가 두 개 이상 포함된 숫자 서식 문자열은 사용자 지정 숫자 서식 문자열로 해석됩니다. 자세한 내용은 [사용자 지정 숫자 서식 문자열](../../../docs/standard/base-types/custom-numeric-format-strings.md)을 참조하세요.

- `xx`는 *전체 자릿수 지정자*라는 선택적 정수입니다. 전체 자릿수 지정자는 0에서 99 사이의 정수이며 결과의 자릿수에 영향을 줍니다. 전체 자릿수 지정자는 숫자의 문자열 표현에서 자릿수를 제어합니다. 숫자 자체는 반올림하지 않습니다. 반올림 연산을 수행하려면 <xref:System.Math.Ceiling%2A?displayProperty=nameWithType>, <xref:System.Math.Floor%2A?displayProperty=nameWithType> 또는 <xref:System.Math.Round%2A?displayProperty=nameWithType> 메서드를 사용합니다.

  *전체 자릿수 지정자*가 결과 문자열의 소수 자릿수를 제어할 때 결과 문자열은 무한 정밀도 결과에 가장 가까운 대표 결과로 반 올림된 숫자를 반영합니다. 동등하게 대표할 수 있는 결과가 두 개 있는 경우:
  - **.NET Framework 및.NET Core에서 .NET Core 2.0까지** 런타임은 최소 유효 숫자(즉, <xref:System.MidpointRounding.AwayFromZero?displayProperty=nameWithType> 사용)를 사용하여 결과를 선택합니다.
  - **.NET Core 2.1 이상에서** 런타임도 최소 유효 숫자(즉, <xref:System.MidpointRounding.ToEven?displayProperty=nameWithType> 사용)를 사용하여 결과를 선택합니다.

  > [!NOTE]
  > 전체 자릿수 지정자는 결과 문자열의 자릿수를 결정합니다. 선행 또는 후행 공백을 포함한 결과 문자열을 채우려면 서식 항목에서 [복합 서식 지정](../../../docs/standard/base-types/composite-formatting.md) 기능을 사용하고 *맞춤 구성 요소*를 정의합니다.

표준 숫자 형식 문자열은 다음에 의해 지원됩니다.

- 모든 숫자 형식의 `ToString` 메서드 중 일부 오버로드. 예를 들어 <xref:System.Int32.ToString%28System.String%29?displayProperty=nameWithType> 및 <xref:System.Int32.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 메서드에 숫자 형식 문자열을 제공할 수 있습니다.

- <xref:System.Console> 및 <xref:System.IO.StreamWriter> 클래스의 일부 `Write` 및 `WriteLine` 메서드, <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드, <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType> 메서드에 사용되는 .NET [복합 서식 지정 기능](../../../docs/standard/base-types/composite-formatting.md). 합성 서식 기능을 사용하여 단일 문자열에 여러 데이터 항목의 문자열 표현을 포함하고, 필드 너비를 지정하며, 필드에서 숫자를 맞출 수 있습니다. 자세한 내용은 [복합 서식 지정](../../../docs/standard/base-types/composite-formatting.md)을 참조하세요.

- 복합 형식 문자열과 비교했을 때 간소화된 구문을 제공하는 C# 및 Visual Basic의 [보간된 문자열](../../csharp/language-reference/tokens/interpolated.md).

> [!TIP]
> 서식 문자열을 숫자 또는 날짜 및 시간 값에 적용할 수 있도록 지원하고 결과 문자열을 표시하는 .NET Core Windows Forms 애플리케이션인 **서식 유틸리티**를 다운로드할 수 있습니다. [C#](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-cs) 및 [Visual Basic](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-vb)의 소스 코드를 사용할 수 있습니다.

<a name="table"></a> 다음 표에서는 표준 숫자 서식 지정자 및 각 서식 지정자로 생성되는 샘플 출력을 보여 줍니다. 표준 숫자 서식 문자열을 사용하는 방법에 대한 자세한 내용은 [참고](#NotesStandardFormatting) 섹션을 참조하고, 이러한 사용 방법을 자세히 보여 주는 예제를 보려면 [예제](#example) 섹션을 참조하세요.

|형식 지정자|name|설명|예|
|----------------------|----------|-----------------|--------------|
|"C" 또는 "c"|통화|결과: 통화 값.<br /><br /> 지원 대상: 모든 숫자 형식.<br /><br /> 전체 자릿수 지정자: 십진수의 수.<br /><br /> 기본 전체 자릿수 지정자: <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A?displayProperty=nameWithType>에 의해 정의됩니다.<br /><br /> 추가 정보: [통화("C") 서식 지정자](#CFormatString).|123.456 ("C", en-US) -> \\$123.46<br /><br /> 123.456 ("C", fr-FR) -> 123,46 €<br /><br /> 123.456 ("C", ja-JP) -> ¥123<br /><br /> -123.456 ("C3", en-US) -> (\\$123.456)<br /><br /> -123.456 ("C3", fr-FR) -> -123,456 €<br /><br /> -123.456 ("C3", ja-JP) -> -¥123.456|
|"D" 또는 "d"|Decimal|결과: 정수(선택적 음수 기호 포함).<br /><br /> 지원 대상: 정수 형식만.<br /><br /> 전체 자릿수 지정자: 최소 자릿수.<br /><br /> 기본 전체 자릿수 지정자: 필요한 최소 자릿수.<br /><br /> 추가 정보: [10진수("D") 서식 지정자](#DFormatString).|1234 ("D") -> 1234<br /><br /> -1234 ("D6") -> -001234|
|"E" 또는 "e"|지수(과학적 표기법)|결과: 지수 표기법.<br /><br /> 지원 대상: 모든 숫자 형식.<br /><br /> 전체 자릿수 지정자: 십진수의 수.<br /><br /> 기본 전체 자릿수 지정자: 6.<br /><br /> 추가 정보: [지수("E") 서식 지정자](#EFormatString).|1052.0329112756 ("E", en-US) -> 1.052033E+003<br /><br /> 1052.0329112756 ("e", fr-FR) -> 1,052033e+003<br /><br /> -1052.0329112756 ("e2", en-US) -> -1.05e+003<br /><br /> -1052.0329112756 ("E2", fr-FR) -> -1,05E+003|
|"F" 또는 "f"|고정 소수점|결과: 선택적 음수 기호가 있는 정수 부분과 소수 부분.<br /><br /> 지원 대상: 모든 숫자 형식.<br /><br /> 전체 자릿수 지정자: 십진수의 수.<br /><br /> 기본 전체 자릿수 지정자: <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=nameWithType>에 의해 정의됩니다.<br /><br /> 추가 정보: [고정 소수점("F") 서식 지정자](#FFormatString).|1234.567 ("F", en-US) -> 1234.57<br /><br /> 1234.567 ("F", de-DE) -> 1234,57<br /><br /> 1234 ("F1", en-US) -> 1234.0<br /><br /> 1234 ("F1", de-DE) -> 1234,0<br /><br /> -1234.56 ("F4", en-US) -> -1234.5600<br /><br /> -1234.56 ("F4", de-DE) -> -1234,5600|
|"G" 또는 "g"|일반|결과: 더 간단한 형태의 고정 소수점 또는 과학적 표기법.<br /><br /> 지원 대상: 모든 숫자 형식.<br /><br /> 전체 자릿수 지정자: 유효 자릿수.<br /><br /> 기본 전체 자릿수 지정자: 숫자 형식에 따라 달라집니다.<br /><br /> 추가 정보: [일반("G") 서식 지정자](#GFormatString).|-123.456 ("G", en-US) -> -123.456<br /><br /> -123.456 ("G", sv-SE) -> -123,456<br /><br /> 123.4546 ("G4", en-US) -> 123.5<br /><br /> 123.4546 ("G4", sv-SE) -> 123,5<br /><br /> -1.234567890e-25 ("G", en-US) -> -1.23456789E-25<br /><br /> -1.234567890e-25 ("G", sv-SE) -> -1,23456789E-25|
|"N" 또는 "n"|번호|결과: 선택적 음수 기호가 있는 정수 부분과 소수 부분, 그룹 구분 기호 및 소수 구분 기호.<br /><br /> 지원 대상: 모든 숫자 형식.<br /><br /> 전체 자릿수 지정자: 원하는 소수 자릿수.<br /><br /> 기본 전체 자릿수 지정자: <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=nameWithType>에 의해 정의됩니다.<br /><br /> 추가 정보: [숫자("N") 서식 지정자](#NFormatString).|1234.567 ("N", en-US) -> 1,234.57<br /><br /> 1234.567 ("N", ru-RU) -> 1 234,57<br /><br /> 1234 ("N1", en-US) -> 1,234.0<br /><br /> 1234 ("N1", ru-RU) -> 1 234,0<br /><br /> -1234.56 ("N3", en-US) -> -1,234.560<br /><br /> -1234.56 ("N3", ru-RU) -> -1 234,560|
|"P" 또는 "p"|백분율|결과: 100으로 곱하고 백분율 기호와 함께 표시되는 숫자.<br /><br /> 지원 대상: 모든 숫자 형식.<br /><br /> 전체 자릿수 지정자: 원하는 소수 자릿수.<br /><br /> 기본 전체 자릿수 지정자: <xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits%2A?displayProperty=nameWithType>에 의해 정의됩니다.<br /><br /> 추가 정보: [백분율("P") 서식 지정자](#PFormatString).|1 ("P", en-US) -> 100.00 %<br /><br /> 1 ("P", fr-FR) -> 100,00 %<br /><br /> -0.39678 ("P1", en-US) -> -39.7 %<br /><br /> -0.39678 ("P1", fr-FR) -> -39,7 %|
|"R" 또는 "r"|라운드트립|결과: 해당 숫자로 라운드트립할 수 있는 문자열.<br /><br /> 지원되는 형식: <xref:System.Single>, <xref:System.Double> 및 <xref:System.Numerics.BigInteger><br /><br /> 참고: <xref:System.Numerics.BigInteger> 형식에만 권장됩니다. <xref:System.Double> 형식에는 “G17”을 사용하고 <xref:System.Single> 형식에는 “G9”을 사용합니다. <br> 전체 자릿수 지정자: 무시됩니다.<br /><br /> 추가 정보: [라운드트립("R") 서식 지정자](#RFormatString).|123456789.12345678 ("R") -> 123456789.12345678<br /><br /> -1234567890.12345678 ("R") -> -1234567890.1234567|
|"X" 또는 "x"|16진수|결과: 16진수 문자열.<br /><br /> 지원 대상: 정수 형식만.<br /><br /> 전체 자릿수 지정자: 결과 문자열의 자릿수.<br /><br /> 추가 정보: [16진수("X") 서식 지정자](#XFormatString).|255 ("X") -> FF<br /><br /> -1 ("x") -> ff<br /><br /> 255 ("x4") -> 00ff<br /><br /> -1 ("X4") -> 00FF|
|기타 모든 단일 문자|알 수 없는 지정자|결과: 런타임에 <xref:System.FormatException>을 throw합니다.||

<a name="Using"></a>

## <a name="using-standard-numeric-format-strings"></a>표준 숫자 서식 문자열 사용

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

표준 숫자 서식 문자열을 사용하여 다음 두 가지 방법 중 하나로 숫자 값의 서식을 정의할 수 있습니다.

- 이 서식 문자열은 `ToString` 매개 변수가 있는 `format` 메서드의 오버로드에 전달될 수 있습니다. 다음 예제에서는 숫자 값의 서식을 현재 문화권(이 예제의 경우 en-US)의 통화 문자열로 지정합니다.

  [!code-cpp[Formatting.Numeric.Standard#10](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/standardusage1.cpp#10)]
  [!code-csharp-interactive[Formatting.Numeric.Standard#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/standardusage1.cs#10)]
  [!code-vb[Formatting.Numeric.Standard#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/standardusage1.vb#10)]

- 이 형식 문자열은 <xref:System.String.Format%2A?displayProperty=nameWithType>, <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> 및 <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType> 같은 메서드와 함께 사용되는 서식 항목의 `formatString` 인수로 제공될 수 있습니다. 자세한 내용은 [복합 서식 지정](../../../docs/standard/base-types/composite-formatting.md)을 참조하세요. 다음 예제에서는 서식 항목을 사용하여 문자열에 통화 값을 삽입합니다.

  [!code-cpp[Formatting.Numeric.Standard#11](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/standardusage1.cpp#11)]
  [!code-csharp-interactive[Formatting.Numeric.Standard#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/standardusage1.cs#11)]
  [!code-vb[Formatting.Numeric.Standard#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/standardusage1.vb#11)]

  필요에 따라 `alignment` 인수를 제공하여 숫자 필드의 너비 및 해당 값이 오른쪽 맞춤인지 또는 왼쪽 맞춤인지 지정할 수 있습니다. 다음 예제에서는 28자 필드의 통화 값을 왼쪽 맞춤으로, 14자 필드의 통화 값을 오른쪽 맞춤으로 지정합니다.

  [!code-cpp[Formatting.Numeric.Standard#12](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/standardusage1.cpp#12)]
  [!code-csharp-interactive[Formatting.Numeric.Standard#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/standardusage1.cs#12)]
  [!code-vb[Formatting.Numeric.Standard#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/standardusage1.vb#12)]

- 보간된 문자열의 보간된 식 항목에서 `formatString` 인수로 제공될 수 있습니다. 자세한 내용은 C# 참조의 [문자열 보간](../../csharp/language-reference/tokens/interpolated.md) 토픽 또는 Visual Basic 참조의 [문자열 보간](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md) 토픽을 참조하세요.

다음 단원에서는 각 표준 숫자 서식 문자열에 대해 자세히 설명합니다.

<a name="CFormatString"></a>

## <a name="the-currency-c-format-specifier"></a>통화("C") 서식 지정자

통화("C") 서식 지정자는 숫자를 통화 금액을 나타내는 숫자로 변환합니다. 전체 자릿수 지정자는 결과 문자열에 필요한 소수 자릿수를 나타냅니다. 전체 자릿수 지정자를 생략하면 <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A?displayProperty=nameWithType> 속성에 의해 기본 전체 자릿수가 정의됩니다.

서식을 지정할 값의 소수 자릿수가 지정된 소수 자릿수 또는 기본 소수 자릿수보다 크면 결과 문자열에서 소수 값이 반올림됩니다. 지정한 소수 자릿수의 오른쪽에 있는 값이 5 이상인 경우 결과 문자열에서 마지막 자릿수가 양수인 경우 올림, 음수인 경우 내림됩니다(Round Away From Zero 방식).

결과 문자열은 현재 <xref:System.Globalization.NumberFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.NumberFormatInfo> 속성을 보여 줍니다.

|NumberFormatInfo 속성|설명|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.CurrencyPositivePattern%2A>|양수 값의 통화 기호 위치를 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern%2A>|음수 값의 통화 기호 위치를 정의하고 음수 기호를 괄호로 나타낼지 아니면 <xref:System.Globalization.NumberFormatInfo.NegativeSign%2A> 속성으로 나타낼지 여부를 지정합니다.|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|<xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern%2A>이 괄호가 사용되지 않음을 나타내는 경우에 사용되는 음수 기호를 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.CurrencySymbol%2A>|통화 기호를 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A>|통합 값의 기본 소수 자릿수를 정의합니다. 전체 자릿수 지정자를 사용하여 이 값을 재정의할 수 있습니다.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator%2A>|정수 부분과 소수 부분을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator%2A>|정수 그룹을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyGroupSizes%2A>|그룹에 표시할 정수 자릿수를 정의합니다.|

다음 예제에서는 통화 서식 지정자를 사용하여 <xref:System.Double> 값의 서식을 지정합니다.

[!code-cpp[Formatting.Numeric.Standard#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#1)]
[!code-csharp[Formatting.Numeric.Standard#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#1)]
[!code-vb[Formatting.Numeric.Standard#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#1)]

[표로 이동](#table)

<a name="DFormatString"></a>

## <a name="the-decimal-d-format-specifier"></a>10진수("D") 서식 지정자

10진수("D") 서식 지정자는 숫자를 10진수(0-9) 문자열로 변환하며, 숫자가 음수이면 앞에 빼기 기호를 붙입니다. 이 서식은 정수 계열 형식에만 사용할 수 있습니다.

전체 자릿수 지정자는 결과 문자열에서 요구하는 최소 자릿수를 나타냅니다. 필요하면 수의 왼쪽을 0으로 채워서 전체 자릿수 지정자에서 지정한 자릿수를 만듭니다. 전체 자릿수 지정자가 지정되지 않은 경우 기본값은 앞에 0이 없이 정수를 나타내는 데 필요한 최소값입니다.

결과 문자열은 현재 <xref:System.Globalization.NumberFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표와 같이 단일 속성은 결과 문자열의 서식에 영향을 줍니다.

|NumberFormatInfo 속성|설명|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|숫자가 음수임을 나타내는 문자열을 정의합니다.|

다음 예제에서는 10진수 서식 지정자를 사용하여 <xref:System.Int32> 값의 서식을 지정합니다.

[!code-cpp[Formatting.Numeric.Standard#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#2)]
[!code-csharp-interactive[Formatting.Numeric.Standard#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#2)]
[!code-vb[Formatting.Numeric.Standard#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#2)]

[표로 이동](#table)

<a name="EFormatString"></a>

## <a name="the-exponential-e-format-specifier"></a>지수("E") 서식 지정자

지수("E") 서식 지정자는 숫자를 "-d.ddd…E+ddd" 또는 "-d.ddd…e+ddd" 형태의 문자열로 변환합니다. 여기서 각 "d"는 숫자(0-9)를 나타냅니다. 숫자가 음수이면 문자열 앞에 빼기 기호가 붙습니다. 소수점 앞에는 항상 숫자가 하나만 있어야 합니다.

전체 자릿수 지정자는 소수점 뒤에 필요한 자릿수를 나타냅니다. 전체 자릿수 지정자가 생략되면 소수점 뒤에 기본 6자리가 사용됩니다.

서식 지정자의 대/소문자에 따라 지수에 "E" 또는 "e" 접두사를 붙일 것인지가 결정됩니다. 지수는 항상 더하기 또는 빼기 기호가 포함된 최소 3자리로 구성됩니다. 필요하면 지수를 0으로 채워서 이 조건을 만족시킵니다.

결과 문자열은 현재 <xref:System.Globalization.NumberFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.NumberFormatInfo> 속성을 보여 줍니다.

|NumberFormatInfo 속성|설명|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|계수와 지수가 둘 다 음수임을 나타내는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|계수에서 정수 부분과 소수 부분을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.PositiveSign%2A>|지수가 양수임을 나타내는 문자열을 정의합니다.|

다음 예제에서는 지수 서식 지정자를 사용하여 <xref:System.Double> 값의 서식을 지정합니다.

[!code-cpp[Formatting.Numeric.Standard#3](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#3)]
[!code-csharp[Formatting.Numeric.Standard#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#3)]
[!code-vb[Formatting.Numeric.Standard#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#3)]

[표로 이동](#table)

<a name="FFormatString"></a>

## <a name="the-fixed-point-f-format-specifier"></a>고정 소수점("F") 서식 지정자

고정 소수점("F") 서식 지정자는 숫자를 "-ddd.ddd…" 형태의 문자열로 변환합니다. 여기서 각 "d"는 숫자(0-9)를 나타냅니다. 숫자가 음수이면 문자열 앞에 빼기 기호가 붙습니다.

전체 자릿수 지정자는 필요한 소수 자릿수를 나타냅니다. 전체 자릿수 지정자를 생략하면 현재 <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=nameWithType> 속성에서 숫자 전체 자릿수를 제공합니다.

결과 문자열은 현재 <xref:System.Globalization.NumberFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 결과 문자열의 서식을 제어하는 <xref:System.Globalization.NumberFormatInfo> 개체의 속성을 보여 줍니다.

|NumberFormatInfo 속성|설명|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|숫자가 음수임을 나타내는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|정수 부분과 소수 부분을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A>|기본 소수 자릿수를 정의합니다. 전체 자릿수 지정자를 사용하여 이 값을 재정의할 수 있습니다.|

다음 예제에서는 고정 소수점 서식 지정자를 사용하여 <xref:System.Double> 및 <xref:System.Int32> 값의 서식을 지정합니다.

[!code-cpp[Formatting.Numeric.Standard#4](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#4)]
[!code-csharp[Formatting.Numeric.Standard#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#4)]
[!code-vb[Formatting.Numeric.Standard#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#4)]

[표로 이동](#table)

<a name="GFormatString"></a>

## <a name="the-general-g-format-specifier"></a>일반("G") 서식 지정자

일반("G") 서식 지정자는 숫자의 형식 및 전체 자릿수 지정자의 유무에 따라 숫자를 고정 소수점 또는 과학적 표기법 중에서 더 간단한 서식으로 변환합니다. 전체 자릿수 지정자는 결과 문자열에 표시할 수 있는 최대 유효 자릿수를 정의합니다. 전체 자릿수 지정자가 생략되거나 0이면 다음 표에 나와 있는 대로 숫자의 형식에 따라 기본 자릿수가 결정됩니다.

|숫자 형식|기본 전체 자릿수|
|------------------|-----------------------|
|<xref:System.Byte> 또는 <xref:System.SByte>|3개의 자릿수|
|<xref:System.Int16> 또는 <xref:System.UInt16>|5개의 자릿수|
|<xref:System.Int32> 또는 <xref:System.UInt32>|10개의 자릿수|
|<xref:System.Int64>|19개의 자릿수|
|<xref:System.UInt64>|20개의 자릿수|
|<xref:System.Numerics.BigInteger>|무제한(["R"](#RFormatString)과 동일)|
|<xref:System.Single>|7개의 자릿수|
|<xref:System.Double>|15개의 자릿수|
|<xref:System.Decimal>|29개의 자릿수|

숫자를 과학적 표기법으로 나타낸 값이 -5보다 크고 전체 자릿수 지정자보다 작으면 고정 소수점 표기법이 사용되고 그러지 않으면 과학적 표기법이 사용됩니다. 필요한 경우 결과에 소수점이 포함되고 소수점 뒤에 오는 0은 생략됩니다. 전체 자릿수 지정자가 있고 결과의 유효 숫자가 지정된 자릿수를 초과하면 뒤에 오는 초과 자릿수는 반올림을 통해 제거됩니다.

그러나 숫자가 <xref:System.Decimal>일 때 전체 자릿수 지정자가 생략되면 항상 고정 소수점 표기법이 사용되며 뒤에 오는 0은 그대로 표시됩니다.

과학적 표기법이 사용되면 서식 지정자가 'G'인 경우 결과의 지수 값 앞에 "E"가 붙고 서식 지정자가 "g"인 경우 앞에 "e"가 붙습니다. 지수는 최소한 2자리로 구성됩니다. 이는 지수 서식 지정자에 의해 생성되며 계수가 최소한 3자리로 구성되는 과학적 표기법의 서식과 다른 점입니다.

<xref:System.Double> 값과 함께 사용될 때 “G17” 형식 지정자는 원래 <xref:System.Double> 값이 성공적으로 라운드트립되도록 합니다. 이는 <xref:System.Double>이 최대 17자의 전체 유효 자릿수를 제공하는 IEEE 754-2008 규격의 배정밀도(`binary64`) 부동 소수점 숫자이기 때문입니다. 일부 경우에 “R”이 배정밀도 부동 소수점 값을 성공적으로 라운드트립하지 못하기 때문에 [“R” 형식 지정자](#RFormatString) 대신 사용하는 것이 좋습니다. 다음 예제는 이러한 사례를 한 가지 보여줍니다.

[!code-csharp-interactive[Round-tripping a Double](../../../samples/snippets/standard/base-types/format-strings/csharp/g17.cs#GeneralFormatSpecifier)]
[!code-vb[Round-tripping a Double](../../../samples/snippets/standard/base-types/format-strings/vb/g17.vb)]

<xref:System.Single> 값과 함께 사용될 때 “G9” 형식 지정자는 원래 <xref:System.Single> 값이 성공적으로 라운드트립되도록 합니다. 이는 <xref:System.Single>이 최대 9자의 전체 유효 자릿수를 제공하는 IEEE 754-2008 규격의 단정밀도(`binary32`) 부동 소수점 숫자이기 때문입니다. 성능을 위해 ["R" 형식 지정자](#RFormatString) 대신 사용하는 것이 좋습니다.

결과 문자열은 현재 <xref:System.Globalization.NumberFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 결과 문자열의 서식을 제어하는 <xref:System.Globalization.NumberFormatInfo> 속성을 보여 줍니다.

|NumberFormatInfo 속성|설명|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|숫자가 음수임을 나타내는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|정수 부분과 소수 부분을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.PositiveSign%2A>|지수가 양수임을 나타내는 문자열을 정의합니다.|

다음 예제에서는 일반 서식 지정자를 사용하여 분류된 부동 소수점 값에 서식을 지정합니다.

[!code-cpp[Formatting.Numeric.Standard#5](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#5)]
[!code-csharp[Formatting.Numeric.Standard#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#5)]
[!code-vb[Formatting.Numeric.Standard#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#5)]

[표로 이동](#table)

<a name="NFormatString"></a>

## <a name="the-numeric-n-format-specifier"></a>숫자("N") 서식 지정자

숫자("N") 서식 지정자는 숫자를 "-d,ddd,ddd.ddd…" 형태의 문자열로 변환합니다. 여기서 "-"는 필요한 경우 음수 기호를 나타내고, "d"는 숫자(0-9)를 나타내고, ","는 그룹 구분 기호를 나타내고, "."은 소수점 기호를 나타냅니다. 전체 자릿수 지정자는 소수점 뒤에 필요한 자릿수를 나타냅니다. 전체 자릿수 지정자를 생략하면 현재 <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=nameWithType> 속성에 의해 소수 자릿수가 정의됩니다.

결과 문자열은 현재 <xref:System.Globalization.NumberFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 결과 문자열의 서식을 제어하는 <xref:System.Globalization.NumberFormatInfo> 속성을 보여 줍니다.

|NumberFormatInfo 속성|설명|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|숫자가 음수임을 나타내는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberNegativePattern%2A>|음수 값의 서식을 정의하고 음수 기호를 괄호로 나타낼지 아니면 <xref:System.Globalization.NumberFormatInfo.NegativeSign%2A> 속성으로 나타낼지 여부를 지정합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberGroupSizes%2A>|그룹 구분 기호 사이에 표시할 정수 자릿수를 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator%2A>|정수 그룹을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|정수 부분과 소수 부분을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A>|기본 소수 자릿수를 정의합니다. 전체 자릿수 지정자를 사용하여 이 값을 재정의할 수 있습니다.|

다음 예제에서는 숫자 서식 지정자를 사용하여 분류된 부동 소수점 값에 서식을 지정합니다.

[!code-cpp[Formatting.Numeric.Standard#6](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#6)]
[!code-csharp[Formatting.Numeric.Standard#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#6)]
[!code-vb[Formatting.Numeric.Standard#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#6)]

[표로 이동](#table)

<a name="PFormatString"></a>

## <a name="the-percent-p-format-specifier"></a>백분율("P") 서식 지정자

백분율("P") 서식 지정자는 숫자를 100으로 곱한 다음 백분율을 나타내는 문자열로 변환합니다. 전체 자릿수 지정자는 필요한 소수 자릿수를 나타냅니다. 전체 자릿수 지정자를 생략하면 현재 <xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits%2A> 속성에서 제공하는 기본 숫자 전체 자릿수가 사용됩니다.

다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.NumberFormatInfo> 속성을 보여 줍니다.

|NumberFormatInfo 속성|설명|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.PercentPositivePattern%2A>|양수 값의 백분율 기호 위치를 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.PercentNegativePattern%2A>|백분율 기호 위치와 음수 값의 음수 기호 위치를 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|숫자가 음수임을 나타내는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.PercentSymbol%2A>|백분율 기호를 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits%2A>|백분율 값의 기본 소수 자릿수를 정의합니다. 전체 자릿수 지정자를 사용하여 이 값을 재정의할 수 있습니다.|
|<xref:System.Globalization.NumberFormatInfo.PercentDecimalSeparator%2A>|정수 부분과 소수 부분을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.PercentGroupSeparator%2A>|정수 그룹을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.PercentGroupSizes%2A>|그룹에 표시할 정수 자릿수를 정의합니다.|

다음 예제에서는 백분율 서식 지정자를 사용하여 부동 소수점 값에 서식을 지정합니다.

[!code-cpp[Formatting.Numeric.Standard#7](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#7)]
[!code-csharp[Formatting.Numeric.Standard#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#7)]
[!code-vb[Formatting.Numeric.Standard#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#7)]

[표로 이동](#table)

<a name="RFormatString"></a>

## <a name="the-round-trip-r-format-specifier"></a>라운드트립("R") 서식 지정자

라운드트립(“R”) 형식 지정자는 문자열로 변환된 숫자 값이 같은 숫자 값으로 다시 구문 분석되도록 시도합니다. 이 서식은 <xref:System.Single>, <xref:System.Double> 및 <xref:System.Numerics.BigInteger> 형식에만 사용할 수 있습니다.

<xref:System.Double> 값의 경우 "R" 형식 지정자가 원래 값을 성공적으로 라운드트립하지 못하는 경우가 있습니다. 또한 <xref:System.Double> 및 <xref:System.Single> 값 모두에 상대적으로 낮은 성능을 제공합니다. 대신 <xref:System.Double> 값에는 [“G17”](#GFormatString) 형식 지정자, <xref:System.Single> 값에는 [“G9”](#GFormatString) 형식 지정자를 사용하여 원래 값을 라운드트립하는 것이 좋습니다.

이 지정자를 사용하여 <xref:System.Numerics.BigInteger> 값의 서식을 지정하면 해당 문자열 표현에 <xref:System.Numerics.BigInteger> 값의 모든 유효 자릿수가 포함됩니다.

전체 자릿수 지정자는 포함되어 있더라도 무시됩니다. 이 지정자를 사용할 때는 라운드트립이 전체 자릿수보다 우선합니다.
결과 문자열은 현재 <xref:System.Globalization.NumberFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 결과 문자열의 서식을 제어하는 <xref:System.Globalization.NumberFormatInfo> 속성을 보여 줍니다.

|NumberFormatInfo 속성|설명|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|숫자가 음수임을 나타내는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|정수 부분과 소수 부분을 구분하는 문자열을 정의합니다.|
|<xref:System.Globalization.NumberFormatInfo.PositiveSign%2A>|지수가 양수임을 나타내는 문자열을 정의합니다.|

다음 예제에서는 라운드트립 형식 지정자를 사용하여 <xref:System.Numerics.BigInteger> 값의 서식을 지정합니다.

[!code-cpp[R format specifier with a BigInteger](../../../samples/snippets/standard/base-types/format-strings/biginteger-r.cpp)]
[!code-csharp[R format specifier with a BigInteger](../../../samples/snippets/standard/base-types/format-strings/biginteger-r.cs)]
[!code-vb[R format specifier with a BigInteger](../../../samples/snippets/standard/base-types/format-strings/biginteger-r.vb)]

> [!IMPORTANT]
> `/platform:x64` 또는 `/platform:anycpu` 스위치를 사용하여 컴파일되고 64비트 시스템에서 실행되는 경우 "R" 표준 숫자 형식 문자열로 형식이 지정된 <xref:System.Double> 값이 성공적으로 라운드트립되지 않는 경우가 있습니다. 자세한 내용은 다음 단락을 참조하세요.

`/platform:x64` 또는 `/platform:anycpu` 스위치를 사용하여 컴파일되고 64비트 시스템에서 실행되는 경우 "R" 표준 숫자 형식 문자열로 형식이 지정된 <xref:System.Double> 값이 성공적으로 라운드트립되지 않는 문제를 해결하려면 "G17" 표준 숫자 서식 문자열을 사용하여 <xref:System.Double> 값에 서식을 지정하면 됩니다. 다음 예제에서는 성공적으로 라운드트립되지 않는 <xref:System.Double> 값에 "R" 형식 문자열을 사용하고 "G17" 형식 문자열도 사용하여 원래 값을 성공적으로 라운드트립합니다.

[!code-csharp[System.Double.ToString#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Double.ToString/cs/roundtripex1.cs#RoundTrip)]
[!code-vb[System.Double.ToString#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Double.ToString/vb/roundtripex1.vb#5)]

[표로 이동](#table)

<a name="XFormatString"></a>

## <a name="the-hexadecimal-x-format-specifier"></a>16진수("X") 서식 지정자

16진수("X") 서식 지정자는 숫자를 16진수 문자열로 변환합니다. 서식 지정자의 대/소문자에 따라 9보다 큰 16진수에 대문자를 사용할지 아니면 소문자를 사용할지 여부가 결정됩니다. 예를 들어, "X"를 사용하면 "ABCDEF"가 만들어지고 "x"를 사용하면 "abcdef"가 만들어집니다. 이 서식은 정수 계열 형식에만 사용할 수 있습니다.

전체 자릿수 지정자는 결과 문자열에서 요구하는 최소 자릿수를 나타냅니다. 필요하면 수의 왼쪽을 0으로 채워서 전체 자릿수 지정자에서 지정한 자릿수를 만듭니다.

결과 문자열은 현재 <xref:System.Globalization.NumberFormatInfo> 개체에 대한 서식 지정 정보의 영향을 받지 않습니다.

다음 예제에서는 16진수 서식 지정자를 사용하여 <xref:System.Int32> 값의 서식을 지정합니다.

[!code-cpp[Formatting.Numeric.Standard#9](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#9)]
[!code-csharp-interactive[Formatting.Numeric.Standard#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#9)]
[!code-vb[Formatting.Numeric.Standard#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#9)]

[표로 이동](#table)

<a name="NotesStandardFormatting"></a>

## <a name="notes"></a>참고

### <a name="control-panel-settings"></a>제어판 설정

제어판에 있는 **국가 및 언어 옵션** 항목의 설정은 서식 지정 작업으로 생성되는 결과 문자열에 영향을 줍니다. 이러한 설정은 서식을 제어하는 데 사용되는 값을 제공하는 현재 스레드 문화권과 연결된 <xref:System.Globalization.NumberFormatInfo> 개체를 초기화하는 데 사용됩니다. 다른 설정을 사용하는 컴퓨터는 다른 결과 문자열을 생성합니다.

또한 현재 시스템 문화권과 같은 문화권을 나타내는 새 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화하는 데 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%29?displayProperty=nameWithType> 생성자가 사용된 경우 제어판의 **국가 및 언어 옵션** 항목을 통해 설정된 사용자 지정 내용이 새 <xref:System.Globalization.CultureInfo> 개체에도 적용됩니다. <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 생성자를 사용하면 시스템의 사용자 지정 내용이 반영되지 않는 <xref:System.Globalization.CultureInfo> 개체를 만들 수 있습니다.

### <a name="numberformatinfo-properties"></a>NumberFormatInfo 속성

서식 지정 작업은 현재 <xref:System.Globalization.NumberFormatInfo> 개체의 속성에 따라 영향을 받으며 이 개체는 현재 스레드 문화권에 의해 암시적으로 제공되거나 서식 지정 작업을 호출하는 메서드의 <xref:System.IFormatProvider> 매개 변수를 통해 명시적으로 제공됩니다. 이 매개 변수에는 <xref:System.Globalization.NumberFormatInfo> 또는 <xref:System.Globalization.CultureInfo> 개체를 지정합니다.

> [!NOTE]
> 숫자 값 서식 지정에 사용되는 패턴 또는 문자열에 대한 자세한 내용은 <xref:System.Globalization.NumberFormatInfo> 클래스 항목을 참조하세요.

### <a name="integral-and-floating-point-numeric-types"></a>정수 계열 및 부동 소수점 숫자 형식

표준 숫자 서식 지정자에 대한 설명 중에는 정수 계열 및 부동 소수점 숫자 형식이 언급되어 있습니다. 정수 계열 숫자 형식은 <xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64> 및 <xref:System.Numerics.BigInteger>이고, 부동 소수점 숫자 형식은 <xref:System.Decimal>, <xref:System.Single> 및 <xref:System.Double>입니다.

### <a name="floating-point-infinities-and-nan"></a>부동 소수점 무한대 및 NaN

서식 문자열에 관계없이 <xref:System.Single> 또는 <xref:System.Double> 부동 소수점 형식의 값이 양의 무한대, 음의 무한대 또는 NaN(Not a Number)이면 서식이 지정된 문자열은 각각 현재 적용 가능한 <xref:System.Globalization.NumberFormatInfo.PositiveInfinitySymbol%2A> 개체에서 지정하는 해당 <xref:System.Globalization.NumberFormatInfo.NegativeInfinitySymbol%2A>, <xref:System.Globalization.NumberFormatInfo.NaNSymbol%2A> 또는 <xref:System.Globalization.NumberFormatInfo> 속성의 값입니다.

## <a name="example"></a>예

[!INCLUDE[interactive-note](~/includes/csharp-interactive-partial-note.md)]

다음 예제에서는 en-US 문화권 및 모든 표준 숫자 서식 지정자를 사용하여 정수 숫자 값과 부동 소수점 숫자 값의 서식을 지정합니다. 이 코드 예제에서는 두 개의 특정 숫자 형식(<xref:System.Double> 및 <xref:System.Int32>)을 사용하지만 다른 기타 숫자 기본 형식(<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64>, <xref:System.Numerics.BigInteger>, <xref:System.Decimal> 및 <xref:System.Single>)을 사용해도 유사한 결과가 생성됩니다.

[!code-csharp[system.x.tostring-and-culture#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.X.ToString-and-Culture/cs/xts.cs#FinalExample)]
[!code-vb[system.x.tostring-and-culture#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.X.ToString-and-Culture/vb/xts.vb#1)]

## <a name="see-also"></a>참고 항목

- <xref:System.Globalization.NumberFormatInfo>
- [Custom Numeric Format Strings](../../../docs/standard/base-types/custom-numeric-format-strings.md)
- [형식 서식 지정](../../../docs/standard/base-types/formatting-types.md)
- [방법: 숫자 앞에 0으로 채우기](../../../docs/standard/base-types/how-to-pad-a-number-with-leading-zeros.md)
- [복합 형식 지정](../../../docs/standard/base-types/composite-formatting.md)
- [샘플: .NET Core WinForms 서식 유틸리티(C#)](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-cs)
- [샘플: .NET Core WinForms 서식 유틸리티(Visual Basic)](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-vb)
