---
title: .NET에서 숫자 문자열 구문 분석
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parsing strings, numeric strings
- numeric strings
- enumerations [.NET Framework], parsing strings
- base types, parsing strings
ms.assetid: e39324ee-72e5-42d4-a80d-bf3ee7fc6c59
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 07ad8b278f6a44fce78bccc980acdc0dc93b1a7a
ms.sourcegitcommit: 700b9003ea6bdd83a53458bbc436c9b5778344f1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48261461"
---
# <a name="parsing-numeric-strings-in-net"></a>.NET에서 숫자 문자열 구문 분석
모든 숫자 형식에는 두 개의 정적 구문 분석 메서드인 `Parse` 및 `TryParse`가 있습니다. 이를 사용하여 숫자의 문자열 표현을 숫자 형식으로 변환할 수 있습니다. 이러한 메서드를 사용하면 [표준 숫자 서식 문자열](../../../docs/standard/base-types/standard-numeric-format-strings.md) 및 [사용자 지정 숫자 서식 문자열](../../../docs/standard/base-types/custom-numeric-format-strings.md)에서 설명하는 서식 문자열을 사용하여 생성된 문자열을 구문 분석할 수 있습니다. 기본적으로 `Parse` 및 `TryParse` 메서드는 정수 소수 자릿수를 포함하는 문자열을 정수 값으로 변환할 수 있습니다. 정수 및 소수 10진수 숫자, 그룹 구분 기호 및 소수 구분 기호를 포함하는 문자열을 부동 소수점 값으로 성공적으로 변환할 수 있습니다. 작업에 실패하면 `Parse` 메서드는 예외를 throw하지만 `TryParse` 메서드는 `false`를 반환합니다.  
  
## <a name="parsing-and-format-providers"></a>구문 분석 및 서식 공급자  
 일반적으로 숫자 값의 문자열 표현은 문화권마다 다릅니다. 통화 기호, 그룹(또는 천 단위 자리) 구분 기호 및 소수 구분 기호와 같은 숫자 문자열의 요소는 모두 문화권마다 다릅니다. 구문 분석 메서드는 이러한 문화권별 차이를 인식하는 서식 공급자를 암시적 또는 명시적으로 사용합니다. 형식 공급자가 `Parse` 또는 `TryParse` 메서드에 대한 호출에서 지정되지 않은 경우 현재 스레드 문화권과 연결된 형식 공급자(<xref:System.Globalization.NumberFormatInfo.CurrentInfo%2A?displayProperty=nameWithType> 속성에서 반환한 <xref:System.Globalization.NumberFormatInfo> 개체)가 사용됩니다.  
  
 형식 공급자는 <xref:System.IFormatProvider> 구현으로 나타납니다. 이 인터페이스에는 단일 멤버인 <xref:System.IFormatProvider.GetFormat%2A> 메서드가 있으며, 이 메서드의 단일 매개 변수는 서식을 지정할 형식을 나타내는 <xref:System.Type> 개체입니다. 이 메서드는 서식 지정 정보를 제공하는 개체를 반환합니다. .NET에서는 숫자 문자열을 구문 분석하기 위해 다음과 같은 두 가지 <xref:System.IFormatProvider> 구현을 지원합니다.  
  
-   <xref:System.Globalization.CultureInfo.GetFormat%2A?displayProperty=nameWithType> 메서드가 문화권별 서식 지정 정보를 제공하는 <xref:System.Globalization.NumberFormatInfo> 개체를 반환하는 <xref:System.Globalization.CultureInfo> 개체.  
  
-   <xref:System.Globalization.NumberFormatInfo.GetFormat%2A?displayProperty=nameWithType> 메서드가 그 자체를 반환하는 <xref:System.Globalization.NumberFormatInfo> 개체.  
  
 다음 예제에서는 배열의 각 문자열을 <xref:System.Double> 값으로 변환하려고 합니다. 먼저 영어(미국) 문화권의 규칙을 반영하는 서식 공급자를 사용하여 문자열을 구문 분석하려고 합니다. 이 작업에서 <xref:System.FormatException>을 throw하는 경우 프랑스어(프랑스) 문화권의 규칙을 반영하는 형식 공급자를 사용하여 문자열을 구문 분석하려고 합니다.  
  
 [!code-csharp[Parsing.Numbers#1](../../../samples/snippets/csharp/VS_Snippets_CLR/parsing.numbers/cs/formatproviders1.cs#1)]
 [!code-vb[Parsing.Numbers#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/parsing.numbers/vb/formatproviders1.vb#1)]  
  
## <a name="parsing-and-numberstyles-values"></a>구문 분석 및 NumberStyles 값  
 구문 분석 작업이 처리할 수 있는 스타일 요소(예: 공백, 그룹 구분 기호 및 소수 구분 기호)는 <xref:System.Globalization.NumberStyles> 열거형 값으로 정의됩니다. 기본적으로 정수 값을 나타내는 문자열은 숫자, 선행 및 후행 공백 및 선행 기호만을 허용하는 <xref:System.Globalization.NumberStyles.Integer?displayProperty=nameWithType> 값을 사용하여 구문 분석됩니다. 부동 소수점 값을 나타내는 문자열은 <xref:System.Globalization.NumberStyles.Float?displayProperty=nameWithType> 및 <xref:System.Globalization.NumberStyles.AllowThousands?displayProperty=nameWithType> 값의 조합을 사용하여 구문 분석됩니다. 이 복합 스타일은 선행 및 후행 공백, 선행 기호, 소수 구분 기호, 그룹 구분 기호 및 지수와 함께 10진수 숫자를 허용합니다. 구문 분석 작업에 성공하기 위해 <xref:System.Globalization.NumberStyles> 형식의 매개 변수를 포함하는 `Parse` 또는 `TryParse` 메서드의 오버로드를 호출하고 <xref:System.Globalization.NumberStyles> 플래그를 하나 이상 설정하여 문자열에 나타낼 수 있는 스타일 요소를 제어할 수 있습니다.  
  
 예를 들어 그룹 구분 기호를 포함하는 문자열은 <xref:System.Int32> 메서드를 사용하여 <xref:System.Int32.Parse%28System.String%29?displayProperty=nameWithType> 값으로 변환할 수 없지만, 다음 예제에서 설명하는 것처럼 <xref:System.Globalization.NumberStyles.AllowThousands?displayProperty=nameWithType> 플래그를 사용할 경우 변환이 성공합니다.  
  
 [!code-csharp[Parsing.Numbers#2](../../../samples/snippets/csharp/VS_Snippets_CLR/parsing.numbers/cs/styles1.cs#2)]
 [!code-vb[Parsing.Numbers#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/parsing.numbers/vb/styles1.vb#2)]  
  
> [!WARNING]
>  구문 분석 작업은 항상 특정 문화권의 서식 지정 규칙을 사용합니다. <xref:System.Globalization.CultureInfo> 또는 <xref:System.Globalization.NumberFormatInfo> 개체를 전달하여 문화권을 지정하지 않는 경우 현재 스레드와 관련된 문화권이 사용됩니다.  
  
 다음 표에서는 <xref:System.Globalization.NumberStyles> 열거형의 멤버를 나열하고 구문 분석 작업에 미치는 영향에 대해 설명합니다.  
  
|NumberStyles 값|구문 분석할 문자열에 미치는 영향|  
|------------------------|---------------------------------------|  
|<xref:System.Globalization.NumberStyles.None?displayProperty=nameWithType>|숫자만 허용됩니다.|  
|<xref:System.Globalization.NumberStyles.AllowDecimalPoint?displayProperty=nameWithType>|소수 구분 기호 및 소수 자릿수가 허용됩니다. 정수 값의 경우 소수 자릿수로 0만 허용됩니다. 유효한 소수 구분 기호는 <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A?displayProperty=nameWithType> 또는 <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator%2A?displayProperty=nameWithType> 속성으로 결정됩니다.|  
|<xref:System.Globalization.NumberStyles.AllowExponent?displayProperty=nameWithType>|지수 표기법을 나타내기 위해 "e" 또는 "E" 문자를 사용할 수 있습니다. 자세한 내용은 <xref:System.Globalization.NumberStyles>를 참조하세요.|  
|<xref:System.Globalization.NumberStyles.AllowLeadingWhite?displayProperty=nameWithType>|선행 공백이 허용됩니다.|  
|<xref:System.Globalization.NumberStyles.AllowTrailingWhite?displayProperty=nameWithType>|후행 공백이 허용됩니다.|  
|<xref:System.Globalization.NumberStyles.AllowLeadingSign?displayProperty=nameWithType>|양수 또는 음수 기호를 숫자 앞에 둘 수 있습니다.|  
|<xref:System.Globalization.NumberStyles.AllowTrailingSign?displayProperty=nameWithType>|양수 또는 음수 기호를 숫자 뒤에 둘 수 있습니다.|  
|<xref:System.Globalization.NumberStyles.AllowParentheses?displayProperty=nameWithType>|괄호는 음수 값을 나타내는 데 사용될 수 있습니다.|  
|<xref:System.Globalization.NumberStyles.AllowThousands?displayProperty=nameWithType>|그룹 구분 기호가 허용됩니다. 그룹 구분 문자는 <xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator%2A?displayProperty=nameWithType> 또는 <xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator%2A?displayProperty=nameWithType> 속성으로 결정됩니다.|  
|<xref:System.Globalization.NumberStyles.AllowCurrencySymbol?displayProperty=nameWithType>|통화 기호가 허용됩니다. 통화 기호는 <xref:System.Globalization.NumberFormatInfo.CurrencySymbol%2A?displayProperty=nameWithType> 속성으로 정의됩니다.|  
|<xref:System.Globalization.NumberStyles.AllowHexSpecifier?displayProperty=nameWithType>|구문 분석될 문자열은 16진수 숫자로 해석됩니다. 16진수인 0-9, A-F 및 a-f를 포함할 수 있습니다. 이 플래그는 정수 값을 구문 분석하는 데 사용할 수 있습니다.|  
  
 또한 <xref:System.Globalization.NumberStyles> 열거형은 다중 <xref:System.Globalization.NumberStyles> 플래그를 포함하는 다음과 같은 복합 스타일을 제공합니다.  
  
|복합 NumberStyles 값|구성원 포함|  
|----------------------------------|----------------------|  
|<xref:System.Globalization.NumberStyles.Integer?displayProperty=nameWithType>|<xref:System.Globalization.NumberStyles.AllowLeadingWhite?displayProperty=nameWithType>, <xref:System.Globalization.NumberStyles.AllowTrailingWhite?displayProperty=nameWithType> 및 <xref:System.Globalization.NumberStyles.AllowLeadingSign?displayProperty=nameWithType> 스타일을 포함합니다. 정수 값을 구문 분석하는 데 사용되는 기본 스타일입니다.|  
|<xref:System.Globalization.NumberStyles.Number?displayProperty=nameWithType>|<xref:System.Globalization.NumberStyles.AllowLeadingWhite?displayProperty=nameWithType>, <xref:System.Globalization.NumberStyles.AllowTrailingWhite?displayProperty=nameWithType>, <xref:System.Globalization.NumberStyles.AllowLeadingSign?displayProperty=nameWithType>, <xref:System.Globalization.NumberStyles.AllowTrailingSign?displayProperty=nameWithType>, <xref:System.Globalization.NumberStyles.AllowDecimalPoint?displayProperty=nameWithType> 및 <xref:System.Globalization.NumberStyles.AllowThousands?displayProperty=nameWithType> 스타일을 포함합니다.|  
|<xref:System.Globalization.NumberStyles.Float?displayProperty=nameWithType>|<xref:System.Globalization.NumberStyles.AllowLeadingWhite?displayProperty=nameWithType>, <xref:System.Globalization.NumberStyles.AllowTrailingWhite?displayProperty=nameWithType>, <xref:System.Globalization.NumberStyles.AllowLeadingSign?displayProperty=nameWithType>, <xref:System.Globalization.NumberStyles.AllowDecimalPoint?displayProperty=nameWithType> 및 <xref:System.Globalization.NumberStyles.AllowExponent?displayProperty=nameWithType> 스타일을 포함합니다.|  
|<xref:System.Globalization.NumberStyles.Currency?displayProperty=nameWithType>|<xref:System.Globalization.NumberStyles.AllowExponent?displayProperty=nameWithType> 및 <xref:System.Globalization.NumberStyles.AllowHexSpecifier?displayProperty=nameWithType>를 제외한 모든 스타일을 포함합니다.|  
|<xref:System.Globalization.NumberStyles.Any?displayProperty=nameWithType>|<xref:System.Globalization.NumberStyles.AllowHexSpecifier?displayProperty=nameWithType>를 제외한 모든 스타일을 포함합니다.|  
|<xref:System.Globalization.NumberStyles.HexNumber?displayProperty=nameWithType>|<xref:System.Globalization.NumberStyles.AllowLeadingWhite?displayProperty=nameWithType>, <xref:System.Globalization.NumberStyles.AllowTrailingWhite?displayProperty=nameWithType> 및 <xref:System.Globalization.NumberStyles.AllowHexSpecifier?displayProperty=nameWithType> 스타일을 포함합니다.|  
  
## <a name="parsing-and-unicode-digits"></a>구문 분석 및 유니코드 숫자  
 유니코드 표준은 다양한 문자 체계의 숫자에 대한 코드 포인트를 정의합니다. 예를 들어 U+0030에서 U+0039의 코드 포인트는 기본 라틴어 숫자 0부터 9까지를 나타내며, U+09E6에서 U+09EF의 코드 포인트는 벵골어 숫자 0부터 9까지, U+FF10에서 U+FF19의 코드 포인트는 전자 숫자 0부터 9까지를 나타냅니다. 그러나 메서드를 구문 분석하여 인식되는 숫자 자릿수는 U +0030에서 U +0039까지의 코드 포인트를 가진 기본 라틴어 숫자 0-9입니다. 숫자 구문 분석 메서드가 여타의 숫자가 포함된 문자열을 전달받은 경우 이 메서드는 <xref:System.FormatException>을 throw합니다.  
  
 다음 예제에서는 <xref:System.Int32.Parse%2A?displayProperty=nameWithType> 메서드를 사용하여 다양한 표기 체계의 숫자로 구성된 문자열을 구문 분석합니다. 이 예제의 결과에서와 같이 기본 라틴어 숫자에 대한 구문 분석 시도는 성공하지만 전자, 아랍어-인도어, 벵골어 숫자에 대한 구문 분석 시도는 실패합니다.  
  
 [!code-csharp[Parsing.Numbers#3](../../../samples/snippets/csharp/VS_Snippets_CLR/parsing.numbers/cs/unicode1.cs#3)]
 [!code-vb[Parsing.Numbers#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/parsing.numbers/vb/unicode1.vb#3)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Globalization.NumberStyles>  
- [Parsing Strings](../../../docs/standard/base-types/parsing-strings.md)  
- [형식 서식 지정](../../../docs/standard/base-types/formatting-types.md)
