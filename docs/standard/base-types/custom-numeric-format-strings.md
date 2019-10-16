---
title: 사용자 지정 숫자 형식 문자열
ms.date: 06/25/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- numeric format strings [.NET Framework]
- formatting [.NET Framework], numbers
- format strings
- custom numeric format strings
- numbers [.NET Framework], formatting
- format specifiers, numeric
- formatting numbers [.NET Framework]
- format specifiers, custom numeric format strings
ms.assetid: 6f74fd32-6c6b-48ed-8241-3c2b86dea5f4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5cacccc182b3361ffd635f2b5f32ce8c17100d08
ms.sourcegitcommit: 77e33b682db39955e331b8e8eda4ef1925a24e78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70133627"
---
# <a name="custom-numeric-format-strings"></a>사용자 지정 숫자 형식 문자열

하나 이상의 사용자 지정 숫자 서식 지정자로 구성된 사용자 지정 숫자 서식 문자열을 만들어 숫자 데이터의 서식을 지정하는 방법을 정의할 수 있습니다. 사용자 지정 숫자 서식 문자열은 [표준 숫자 서식 문자열](../../../docs/standard/base-types/standard-numeric-format-strings.md)이 아닌 모든 서식 문자열입니다.

사용자 지정 숫자 서식 문자열은 모든 숫자 형식의 `ToString` 메서드를 오버로드하여 사용할 수 있습니다. 예를 들어 <xref:System.Int32.ToString%28System.String%29> 형식의 <xref:System.Int32.ToString%28System.String%2CSystem.IFormatProvider%29> 및 <xref:System.Int32> 메서드에 숫자 서식 문자열을 제공할 수 있습니다. <xref:System.Console> 및 <xref:System.IO.StreamWriter> 클래스의 일부 `Write` 및 `WriteLine` 메서드, <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드, <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType> 메서드에 사용되는 .NET [복합 서식 지정 기능](../../../docs/standard/base-types/composite-formatting.md)을 통해서도 사용자 지정 숫자 형식 문자열을 사용할 수 있습니다. [문자열 보간](../../csharp/language-reference/tokens/interpolated.md) 기능은 사용자 지정 숫자 형식 문자열도 지원합니다.

> [!TIP]
> 서식 문자열을 숫자 또는 날짜 및 시간 값에 적용할 수 있도록 지원하고 결과 문자열을 표시하는 .NET Core Windows Forms 애플리케이션인 **서식 유틸리티**를 다운로드할 수 있습니다. [C#](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-cs) 및 [Visual Basic](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-vb)의 소스 코드를 사용할 수 있습니다.

<a name="table"></a> 다음 표에서는 사용자 지정 숫자 서식 지정자 및 각 서식 지정자로 생성되는 샘플 출력을 보여 줍니다. 사용자 지정 숫자 서식 문자열을 사용하는 방법에 대한 자세한 내용은 [참고](#NotesCustomFormatting) 단원을 참조하고, 이러한 사용 방법을 자세히 보여 주는 예제를 보려면 [예제](#example) 단원을 참조하세요.

|형식 지정자|name|설명|예제|
|----------------------|----------|-----------------|--------------|
|"0"|0 자리 표시자|해당 숫자가 있을 경우 0을 해당 숫자로 바꾸고, 그렇지 않으면 결과 문자열에 0을 표시합니다.<br /><br /> 추가 정보: ["0" 사용자 지정 지정자](#Specifier0).|1234.5678 ("00000") -> 01235<br /><br /> 0.45678 ("0.00", en-US) -> 0.46<br /><br /> 0.45678 ("0.00", fr-FR) -> 0,46|
|"#"|10진수 자리 표시자|해당 숫자가 있을 경우 "#" 기호를 해당 숫자로 바꾸고, 그렇지 않으면 결과 문자열에 숫자를 표시하지 않습니다.<br /><br /> 입력 문자열의 해당 숫자가 의미 없는 0인 경우 결과 문자열에 숫자를 표시하지 않습니다. 예를 들어 0003 ("####") -> 3입니다.<br /><br /> 추가 정보: ["#" 사용자 지정 지정자](#SpecifierD).|1234.5678 ("#####") -> 1235<br /><br /> 0.45678 ("#.##", en-US) -> .46<br /><br /> 0.45678 ("#.##", fr-FR) -> ,46|
|"."|소수점|결과 문자열에서 소수 구분 기호의 위치를 결정합니다.<br /><br /> 추가 정보: ["." 사용자 지정 지정자](#SpecifierPt).|0.45678 ("0.00", en-US) -> 0.46<br /><br /> 0.45678 ("0.00", fr-FR) -> 0,46|
|","|그룹 구분 기호 및 숫자 배율|그룹 구분 기호 지정자와 숫자 배율 지정자로 모두 사용됩니다. 그룹 구분 기호로 사용될 경우 각 그룹 사이에 지역화된 그룹 구분 기호 문자를 삽입합니다. 숫자 배율 지정자로 사용될 경우 숫자를 쉼표 단위로 끊어서 1000으로 나눕니다.<br /><br /> 추가 정보: ["," 사용자 지정 지정자](#SpecifierTh).|그룹 구분 기호 지정자:<br /><br /> 2147483647 ("##,#", en-US) -> 2,147,483,647<br /><br /> 2147483647 ("##,#", es-ES) -> 2.147.483.647<br /><br /> 배율 지정자:<br /><br /> 2147483647 ("#,#,,", en-US) -> 2,147<br /><br /> 2147483647 ("#,#,,", es-ES) -> 2.147|
|"%"|백분율 자리 표시자|숫자에 100을 곱하고 결과 문자열에 지역화된 백분율 기호를 삽입합니다.<br /><br /> 추가 정보: ["%" 사용자 지정 지정자](#SpecifierPct).|0.3697 ("%#0.00", en-US) -> %36.97<br /><br /> 0.3697 ("%#0.00", el-GR) -> %36,97<br /><br /> 0.3697 ("##.0 %", en-US) -> 37.0 %<br /><br /> 0.3697 ("##.0 %", el-GR) -> 37,0 %|
|"‰"|천분율 자리 표시자|숫자에 1000을 곱하고 결과 문자열에 지역화된 천분율 기호를 삽입합니다.<br /><br /> 추가 정보: ["‰" 사용자 지정 지정자](#SpecifierPerMille).|0.03697 ("#0.00‰", en-US) -> 36.97‰<br /><br /> 0.03697 ("#0.00‰", ru-RU) -> 36,97‰|
|"E0"<br /><br /> "E+0"<br /><br /> "E-0"<br /><br /> "E0"<br /><br /> "E+0"<br /><br /> "E-0"|지수 표기법|적어도 하나의 0이 뒤에 오면 지수 표기법을 사용하여 결과의 서식을 지정합니다. "E" 또는 "e" 문자는 결과 문자열에 표시되는 지수 기호의 대/소문자를 나타냅니다. "E" 또는 "e" 문자 뒤에 오는 0의 수에 따라 지수의 최소 자릿수가 결정됩니다. 더하기 기호(+)는 기호 문자가 항상 지수 앞에 온다는 것을 나타냅니다. 빼기 기호(-)는 기호 문자가 음의 지수 앞에만 온다는 것을 나타냅니다.<br /><br /> 추가 정보: ["E" 및 "e" 사용자 지정 지정자](#SpecifierExponent).|987654 ("#0.0e0") -> 98.8e4<br /><br /> 1503.92311 ("0.0##e+00") -> 1.504e+03<br /><br /> 1.8901385E-16 ("0.0e+00") -> 1.9e-16|
|"\\"|이스케이프 문자|뒤에 오는 문자가 사용자 지정 형식 지정자가 아닌 리터럴로 해석되도록 합니다.<br /><br /> 추가 정보: ["\\"이스케이프 문자](#SpecifierEscape).|987654 ("\\###00\\#") -> #987654#|
|'*string*'<br /><br /> "*string*"|리터럴 문자열 구분 기호|괄호로 묶인 문자가 변경되지 않은 상태로 결과 문자열에 복사되어야 함을 나타냅니다.<br/><br/>추가 정보: [문자 리터럴](#character-literals).|68 (“# ‘degrees’”) -> 68 degrees<br /><br /> 68 ("#' degrees'") -> 68 degrees|
|;|섹션 구분 기호|양수, 음수 및 0에 따라 별도의 서식 문자열을 사용하여 섹션을 정의합니다.<br /><br /> 추가 정보: [";" 섹션 구분 기호](#SectionSeparator).|12.345 ("#0.0#;(#0.0#);-\0-") -> 12.35<br /><br /> 0 ("#0.0#;(#0.0#);-\0-") -> -0-<br /><br /> -12.345 ("#0.0#;(#0.0#);-\0-") -> (12.35)<br /><br /> 12.345 ("#0.0#;(#0.0#)") -> 12.35<br /><br /> 0 ("#0.0#;(#0.0#)") -> 0.0<br /><br /> -12.345 ("#0.0#;(#0.0#)") -> (12.35)|
|기타|다른 모든 문자|문자가 변경되지 않은 상태로 결과 문자열에 복사됩니다.<br/><br/>추가 정보: [문자 리터럴](#character-literals).|68 ("# °") -> 68 °|

다음 단원에서는 각 사용자 지정 숫자 서식 지정자에 대해 자세히 설명합니다.

[!INCLUDE[C# interactive-note](~/includes/csharp-interactive-partial-note.md)]

<a name="Specifier0"></a>

## <a name="the-0-custom-specifier"></a>"0" 사용자 지정 지정자

"0" 사용자 지정 지정자는 0 자리 표시자 기호로 사용됩니다. 서식을 지정할 값이 서식 문자열의 0이 표시된 위치에 숫자를 가지고 있으면 해당 숫자가 결과 문자열로 복사되고, 그렇지 않으면 결과 문자열에 0이 표시됩니다. 소수점 앞 가장 왼쪽의 0과 소수점 뒤 가장 오른쪽 0의 위치는 결과 문자열에 항상 표시될 자릿수의 범위를 결정합니다.

"00" 지정자를 사용하면 해당 값이 소수점 뒤 첫째 자리에서 반올림되며 항상 0 이상의 정수 값으로 표시됩니다. 예를 들어, 34.5의 서식을 "00"으로 지정하면 결과는 35가 됩니다.

다음 예제에서는 0 자리 표시자가 포함된 사용자 지정 서식 문자열을 사용하여 여러 가지 값을 표시합니다.

[!code-cpp[Formatting.Numeric.Custom#1](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#1)]
[!code-csharp[Formatting.Numeric.Custom#1](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#1)]
[!code-vb[Formatting.Numeric.Custom#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#1)]

[표로 이동](#table)

<a name="SpecifierD"></a>

## <a name="the--custom-specifier"></a>"#" 사용자 지정 지정자

"#" 사용자 지정 지정자는 숫자 표시자 기호로 사용됩니다. 서식을 지정할 값이 서식 문자열의 "#" 기호가 표시된 위치에 숫자를 가지고 있으면 해당 숫자가 결과 문자열로 복사되고, 그렇지 않으면 결과 문자열의 해당 위치에 아무 것도 저장되지 않습니다.

0이 유효 자릿수가 아니면 이 지정자는 문자열에서 0이 유일한 숫자라 할지라도 0을 표시하지 않습니다. 표시되는 숫자에서 0이 유효 자릿수이면 이 지정자는 0을 표시합니다.

"##" 서식 문자열을 사용하면 해당 값이 소수점 뒤 첫째 자리에서 반올림되며 항상 0 이상의 정수로 표시됩니다. 예를 들어, 34.5의 서식을 "##"으로 지정하면 결과는 35가 됩니다.

다음 예제에서는 숫자 자리 표시자가 포함된 사용자 지정 서식 문자열을 사용하여 여러 가지 값을 표시합니다.

[!code-cpp[Formatting.Numeric.Custom#2](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#2)]
[!code-csharp[Formatting.Numeric.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#2)]
[!code-vb[Formatting.Numeric.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#2)]

빈 숫자나 선행 0이 공백으로 대체되는 결과 문자열을 반환하려면 다음 예제와 같이 [복합 서식 지정 기능](../../../docs/standard/base-types/composite-formatting.md) 을 사용하고 필드 너비를 지정합니다.

[!code-cpp[Formatting.Numeric.Custom#12](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/SpaceOrDigit1.cpp#12)]
[!code-csharp[Formatting.Numeric.Custom#12](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/SpaceOrDigit1.cs#12)]
[!code-vb[Formatting.Numeric.Custom#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/SpaceOrDigit1.vb#12)]

[표로 이동](#table)

<a name="SpecifierPt"></a>

## <a name="the--custom-specifier"></a>"." 사용자 지정 지정자

"." 사용자 지정 서식 지정자는 결과 문자열에 지역화된 소수 구분 기호를 삽입합니다. 서식 문자열의 첫째 마침표 문자는 서식이 지정될 값에서 소수 구분 기호의 위치를 결정하며, 다른 마침표 문자는 무시됩니다.

결과 문자열에서 소수 구분 기호로 사용되는 문자는 항상 마침표는 아니며 서식 지정을 제어하는 <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> 개체의 <xref:System.Globalization.NumberFormatInfo> 속성에 의해 결정됩니다.

다음 예제에서는 "." 서식 지정자를 사용하여 여러 결과 문자열에서 소수점의 위치를 정의합니다.

[!code-cpp[Formatting.Numeric.Custom#3](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#3)]
[!code-csharp[Formatting.Numeric.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#3)]
[!code-vb[Formatting.Numeric.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#3)]

[표로 이동](#table)

<a name="SpecifierTh"></a>

## <a name="the--custom-specifier"></a>"," 사용자 지정 지정자

"," 문자는 그룹 구분 기호 지정자와 숫자 배율 지정자로 사용됩니다.

- 그룹 구분 기호: 두 개의 10진수 자리 표시자(0 또는 #) 사이에 정수 계열 자릿수의 서식을 지정하는 하나 이상의 쉼표 문자가 지정된 경우 정수 계열 출력 부분의 각 숫자 그룹 사이에 그룹 구분 문자가 삽입됩니다.

  현재 <xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator%2A> 개체의 <xref:System.Globalization.NumberFormatInfo.NumberGroupSizes%2A> 및 <xref:System.Globalization.NumberFormatInfo> 속성은 숫자 그룹 구분 기호로 사용되는 문자와 각 숫자 그룹의 크기를 결정합니다. 예를 들어, 문자열 "#,#"과 고정 문화권을 사용하여 숫자 1000의 서식을 지정할 경우 "1,000"이 출력됩니다.

- 숫자 배율 지정자: 명시적 또는 암시적 소수점의 바로 왼쪽에 하나 이상의 쉼표가 지정된 경우 서식이 지정될 숫자는 쉼표 단위로 끊어서 1000으로 나뉩니다. 예를 들어, 문자열 "0,,"을 사용하여 숫자 100000000의 서식을 지정할 경우 "100"이 출력됩니다.

동일한 서식 문자열에 그룹 구분 기호와 숫자 배율 지정자를 함께 사용할 수 있습니다. 예를 들어, 문자열 "#,0,,"과 고정 문화권을 사용하여 숫자 1000000000의 서식을 지정할 경우 "1,000"이 출력됩니다.

다음 예제에서는 쉼표를 그룹 구분 기호로 사용하는 방법을 보여 줍니다.

[!code-cpp[Formatting.Numeric.Custom#4](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#4)]
[!code-csharp[Formatting.Numeric.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#4)]
[!code-vb[Formatting.Numeric.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#4)]

다음 예제에서는 쉼표를 숫자 배율 지정자로 사용하는 방법을 보여 줍니다.

[!code-cpp[Formatting.Numeric.Custom#5](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#5)]
[!code-csharp[Formatting.Numeric.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#5)]
[!code-vb[Formatting.Numeric.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#5)]

[표로 이동](#table)

<a name="SpecifierPct"></a>

## <a name="the--custom-specifier"></a>"%" 사용자 지정 지정자

서식 문자열에 백분율 기호(%)가 있으면 서식이 지정되기 전에 해당 수에 100이 곱해집니다. 서식 문자열에서 %가 표시된 위치에 있는 숫자에는 지역화된 백분율 기호가 삽입됩니다. 사용된 백분율 문자는 <xref:System.Globalization.NumberFormatInfo.PercentSymbol%2A> 개체의 <xref:System.Globalization.NumberFormatInfo> 속성에 의해 정의됩니다.

다음 예제에서는 "%" 사용자 지정 지정자가 포함된 여러 가지 사용자 지정 서식 문자열을 정의합니다.

[!code-cpp[Formatting.Numeric.Custom#6](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#6)]
[!code-csharp[Formatting.Numeric.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#6)]
[!code-vb[Formatting.Numeric.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#6)]

[표로 이동](#table)

<a name="SpecifierPerMille"></a>

## <a name="the--custom-specifier"></a>"‰" 사용자 지정 지정자

서식 문자열에 천분율 문자(‰ 또는 \u2030)가 있으면 서식이 지정되기 전에 해당 수에 1000이 곱해집니다. 서식 문자열에서 ‰가 표시된 위치에 있는 반환된 문자열에는 적절한 천분율 기호가 삽입됩니다. 사용되는 천분율 문자는 문화권별 서식 지정 정보를 제공하는 개체의 <xref:System.Globalization.NumberFormatInfo.PerMilleSymbol%2A?displayProperty=nameWithType> 속성에 정의되어 있습니다.

다음 예제에서는 "‰" 사용자 지정 지정자가 포함된 사용자 지정 서식 문자열을 정의합니다.

[!code-cpp[Formatting.Numeric.Custom#9](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#9)]
[!code-csharp[Formatting.Numeric.Custom#9](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#9)]
[!code-vb[Formatting.Numeric.Custom#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#9)]

[표로 이동](#table)

<a name="SpecifierExponent"></a>

## <a name="the-e-and-e-custom-specifiers"></a>"E" 및 "e" 사용자 지정 지정자

서식 문자열에 "E", "E+", "E-", "e", "e+" 또는 "e-" 문자열이 표시되고 바로 뒤에 적어도 하나의 0이 오면, 해당 수와 지수 사이에 "E" 또는 "e"가 삽입되는 과학적 표기법으로 서식이 지정됩니다. 과학적 표기법 표시기 뒤에 오는 0의 개수는 이 숫자의 지수로 나타낼 최소 자릿수를 결정합니다. "E+" 및 "e+" 서식은 더하기 기호나 빼기 기호가 항상 지수 앞에 와야 한다는 것을 나타냅니다. "E", "E-", "e" 또는 "e-" 서식은 기호 문자가 음의 지수 앞에만 와야 한다는 것을 나타냅니다.

다음 예제에서는 과학적 표기법 지정자를 사용하여 여러 가지 숫자 값에 서식을 지정합니다.

[!code-cpp[Formatting.Numeric.Custom#7](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#7)]
[!code-csharp[Formatting.Numeric.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#7)]
[!code-vb[Formatting.Numeric.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#7)]

[표로 이동](#table)

<a name="SpecifierEscape"></a>

## <a name="the--escape-character"></a>"\\" 이스케이프 문자

서식 문자열의 "#", "0", ".", ",", "%" 및 "‰" 기호는 리터럴 문자가 아닌 서식 지정자로 해석됩니다. 사용자 지정 서식 문자열에서 이러한 문자가 있는 위치에 따라 대문자 및 소문자 "E"와 + 및 - 기호도 서식 지정자로 해석될 수 있습니다.

문자가 서식 지정자로 해석되지 않도록 하려면 해당 문자 앞에 이스케이프 문자인 백슬래시를 삽입하면 됩니다. 이스케이프 문자는 뒤에 오는 문자가 변경되지 않은 상태로 결과 문자열에 포함되어야 하는 문자 리터럴임을 나타냅니다.

결과 문자열에 백슬래시를 포함하려면`\\`처럼 두 개의 백슬래시를 연속해서 입력해야 합니다.

> [!NOTE]
> C++ 및 C# 컴파일러 같은 일부 컴파일러에서는 하나의 백슬래시 문자가 이스케이프 문자로 해석될 수도 있습니다. 형식을 지정할 때 문자열이 올바로 해석되도록 하려면 해당 문자열 앞에 축자 문자열 리터럴 문자(@ 문자)를 사용하거나(C#의 경우) 각 백슬래시 앞에 또 다른 백슬래시를 추가하면 됩니다(C# 및 C++의 경우). 다음 C# 예제에서는 이 두 가지 방법을 모두 보여 줍니다.

다음 예제에서는 이스케이프 문자를 사용하여 서식 지정 작업에서 “#”, “0” 및 “\\” 문자가 이스케이프 문자나 형식 지정자로 해석되지 않도록 합니다. 이 C# 예제에서는 추가 백슬래시를 사용하여 백슬래시가 리터럴 문자로 해석되도록 합니다.

[!code-cpp[Formatting.Numeric.Custom#11](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/escape1.cpp#11)]
[!code-csharp-interactive[Formatting.Numeric.Custom#11](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/escape1.cs#11)]
[!code-vb[Formatting.Numeric.Custom#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/escape1.vb#11)]

[표로 이동](#table)

<a name="SectionSeparator"></a>

## <a name="the--section-separator"></a>";" 섹션 구분 기호

세미콜론(;)은 해당 값이 양수인지 여부에 따라 서로 다른 서식을 숫자에 적용하는 조건부 서식 지정자입니다. 이렇게 하려면 사용자 지정 서식 문자열에 세미콜론으로 구분된 최대 세 개의 섹션이 포함되어야 합니다. 다음 표에서는 이러한 섹션에 대해 설명합니다.

|섹션 수|설명|
|------------------------|-----------------|
|한 섹션|형식 문자열이 모든 값에 적용됩니다.|
|두 섹션|첫째 섹션은 양수 값과 0에 적용되고, 둘째 섹션은 음수 값에 적용됩니다.<br /><br /> 서식을 지정할 수가 음수였는데 둘째 섹션의 서식에 따라 반올림한 후에 0이 된 경우, 결과값 0은 첫째 섹션에 따라 서식이 지정됩니다.|
|세 섹션|첫째 섹션은 양수 값에 적용되고, 둘째 섹션은 음수 값에 적용되며, 셋째 섹션은 0에 적용됩니다.<br /><br /> 세미콜론 사이에 아무 것도 없어서 둘째 섹션이 비어 있는 경우에는 첫째 섹션을 0이 아닌 모든 값에 적용합니다.<br /><br /> 서식을 지정할 수가 0이 아니었는데 첫째 또는 둘째 섹션의 서식에 따라 반올림한 후에 0이 된 경우, 결과값 0은 셋째 섹션에 따라 서식이 지정됩니다.|

섹션 구분 기호는 마지막 값의 서식을 지정할 때 숫자와 연관된 기존 서식을 무시합니다. 예를 들어, 섹션 구분 기호가 사용되면 음수 값은 항상 빼기 기호 없이 표시됩니다. 마지막에 서식을 지정한 값에 빼기 기호를 붙이려면 빼기 기호를 사용자 지정 서식 지정자의 일부로 명시적으로 포함시켜야 합니다.

다음 예제에서는 ";" 서식 지정자를 사용하여 양수, 음수 및 0의 서식을 각각 다르게 지정합니다.

[!code-cpp[Formatting.Numeric.Custom#8](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/custom.cpp#8)]
[!code-csharp-interactive[Formatting.Numeric.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/custom.cs#8)]
[!code-vb[Formatting.Numeric.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/Custom.vb#8)]

[표로 이동](#table)

## <a name="character-literals"></a>문자 리터럴

사용자 지정 숫자 서식 문자열에서 나타나는 서식 지정자는 리터럴 문자가 아닌 서식 지정 문자로 해석됩니다. 여기에는 다음과 같은 문자가 포함됩니다.

- [0](#Specifier0)
- [\#](#SpecifierD)
- [%](#SpecifierPct)
- [‰](#SpecifierPerMille)
- '
- [\\](#SpecifierEscape)
- [.](#SpecifierPt)
- [,](#SpecifierTh)
- 서식 문자열의 해당 위치에 따라 [E 또는 e](#SpecifierExponent)

다른 모든 문자는 항상 문자 리터럴로 해석되며, 형식 지정 작업에서 변경되지 않고 결과 문자열에 포함됩니다.  구문 분석 작업에서는 입력 문자열의 문자와 정확히 일치해야 하며, 비교 시 대/소문자를 구분합니다.

다음 예제에서는 리터럴 문자 단위(이 경우에는 천)의 일반적인 사용을 한 가지 보여줍니다.

[!code-csharp-interactive[literal characters](~/samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/literal2.cs#1)]
[!code-vb[literal characters](~/samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/literal2.vb#1)]

문자가 결과 문자열에 포함되거나 입력 문자열에서 성공적으로 구문 분석될 수 있도록 하기 위해 문자를 서식 지정 문자가 아니라 리터럴 문자로 해석되도록 지정하는 두 가지 방법이 있습니다.

- 서식 지정 문자를 이스케이프하는 방법입니다. 자세한 내용은 ["\\" 이스케이프 문자](#SpecifierEscape)를 참조하세요.

- 전체 리터럴 문자열을 따옴표 아포스트로피로 묶습니다.

다음 예제에서는 사용자 지정 숫자 서식 문자열에서 예약된 문자를 포함하는 두 가지 방법을 사용합니다.

[!code-csharp-interactive[including reserved characters](~/samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/literal1.cs#1)]
[!code-vb[including reserved characters](~/samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/literal1.vb#1)]

<a name="NotesCustomFormatting"></a>

## <a name="notes"></a>참고 사항

### <a name="floating-point-infinities-and-nan"></a>부동 소수점 무한대 및 NaN

서식 문자열에 관계없이 <xref:System.Single> 또는 <xref:System.Double> 부동 소수점 형식의 값이 양의 무한대, 음의 무한대 또는 NaN(Not a Number)이면 서식이 지정된 문자열은 각각 현재 적용 가능한 <xref:System.Globalization.NumberFormatInfo.PositiveInfinitySymbol%2A>개체에서 지정하는 해당 <xref:System.Globalization.NumberFormatInfo.NegativeInfinitySymbol%2A>, <xref:System.Globalization.NumberFormatInfo.NaNSymbol%2A> 또는 <xref:System.Globalization.NumberFormatInfo> 속성의 값입니다.

### <a name="control-panel-settings"></a>제어판 설정

제어판에 있는 **국가 및 언어 옵션** 항목의 설정은 서식 지정 작업으로 생성되는 결과 문자열에 영향을 줍니다. 이러한 설정은 현재 스레드 문화권과 연결된 <xref:System.Globalization.NumberFormatInfo> 개체를 초기화하는 데 사용됩니다. 현재 스레드 문화권은 서식을 제어하는 데 사용되는 값을 제공합니다. 다른 설정을 사용하는 컴퓨터는 다른 결과 문자열을 생성합니다.

또한 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%29?displayProperty=nameWithType> 생성자를 사용하여 현재 시스템 문화권과 동일한 문화권을 나타내는 새 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화하는 경우 제어판의 **국가 및 언어 옵션** 항목을 통해 설정된 사용자 지정 내용이 새 <xref:System.Globalization.CultureInfo> 개체에도 적용됩니다. <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 생성자를 사용하면 시스템의 사용자 지정 내용이 반영되지 않는 <xref:System.Globalization.CultureInfo> 개체를 만들 수 있습니다.

### <a name="rounding-and-fixed-point-format-strings"></a>반올림 및 고정 소수점 서식 문자열

고정 소수점 서식 문자열, 즉 과학적 표기법 서식 문자가 들어 있지 않은 서식 문자열의 경우 소수점 오른쪽에 있는 10진수 자리 표시자와 같은 개수의 소수 자릿수만큼 숫자가 반올림됩니다. 서식 문자열에 소수점이 없으면 숫자는 가장 근접한 정수로 반올림됩니다. 숫자의 자릿수가 소수점 왼쪽의 10진수 자리 표시자보다 많으면, 초과 숫자가 결과 문자열의 첫째 10진수 자리 표시자 바로 앞에 복사됩니다.

[표로 이동](#table)

<a name="example"></a>

## <a name="example"></a>예

다음 예제에서는 두 개의 사용자 지정 숫자 서식 문자열을 보여 줍니다. 두 경우 모두에서 숫자 자리 표시자(`#`)는 숫자 데이터를 표시하며, 다른 모든 문자는 결과 문자열에 복사됩니다.

[!code-cpp[Formatting.Numeric.Custom#10](../../../samples/snippets/cpp/VS_Snippets_CLR/formatting.numeric.custom/cpp/example1.cpp#10)]
[!code-csharp-interactive[Formatting.Numeric.Custom#10](../../../samples/snippets/csharp/VS_Snippets_CLR/formatting.numeric.custom/cs/example1.cs#10)]
[!code-vb[Formatting.Numeric.Custom#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/formatting.numeric.custom/vb/example1.vb#10)]

[표로 이동](#table)

## <a name="see-also"></a>참고 항목

- <xref:System.Globalization.NumberFormatInfo?displayProperty=nameWithType>
- [형식 서식 지정](../../../docs/standard/base-types/formatting-types.md)
- [Standard Numeric Format Strings](../../../docs/standard/base-types/standard-numeric-format-strings.md)
- [방법: 숫자 앞에 0으로 채우기](../../../docs/standard/base-types/how-to-pad-a-number-with-leading-zeros.md)
- [샘플: .NET Core WinForms 서식 유틸리티(C#)](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-cs)
- [샘플: .NET Core WinForms 서식 유틸리티(Visual Basic)](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-vb)
