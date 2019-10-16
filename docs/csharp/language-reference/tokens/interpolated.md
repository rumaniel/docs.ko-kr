---
title: $ - 문자열 보간 - C# 참조
ms.custom: seodec18
description: 문자열 보간을 이용한 구문으로 기존의 문자열 합성보다 읽기 쉽고 편리하게 문자열 출력의 서식을 지정할 수 있습니다.
ms.date: 09/02/2019
f1_keywords:
- $_CSharpKeyword
- $
helpviewer_keywords:
- $ special character [C#]
- string interpolation [C#]
- interpolated string [C#]
author: pkulikov
ms.author: ronpet
ms.openlocfilehash: 53a8938a373136df65e23c162b94c4d8dc1f30b4
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253859"
---
# <a name="---string-interpolation-c-reference"></a>$ - 문자열 보간(C# 참조)

`$`특수 문자는 문자열 리터럴을 *보간된 문자열*로 식별합니다. 보간된 문자열은 *보간 식*이 포함될 수 있는 문자열 리터럴입니다. 보간된 문자열이 결과 문자열로 해석되면 보간 식이 있는 항목이 식 결과의 문자열 표현으로 바뀝니다. 이 기능은 C# 6부터 사용할 수 있습니다.

문자열 보간은 [문자열 합성 서식 지정](../../../standard/base-types/composite-formatting.md) 기능보다 읽기 쉽고 편리하게 서식이 지정된 문자열을 만들 수 있는 구문을 제공합니다. 다음 예제에서는 두 기능을 사용하여 동일한 출력을 생성합니다.

[!code-csharp-interactive[compare with composite formatting](~/samples/snippets/csharp/language-reference/tokens/string-interpolation.cs#1)]

## <a name="structure-of-an-interpolated-string"></a>보간된 문자열의 구조

문자열 리터럴을 보간된 문자열로 식별하려면 `$` 기호를 사용하여 추가합니다. 문자열 리터럴을 시작하는 `$` 및 `"` 사이에 공백이 없어야 합니다.

보간 식이 있는 항목의 구조는 다음과 같습니다.

```csharp
{<interpolationExpression>[,<alignment>][:<formatString>]}
```

대괄호 안의 요소는 선택 사항입니다. 다음 표에서는 각 요소에 대해 설명합니다.

|요소|설명|
|-------------|-----------------|
|`interpolationExpression`|서식을 지정할 결과를 생성하는 식입니다. `null`의 문자열 표현은 <xref:System.String.Empty?displayProperty=nameWithType>입니다.|
|`alignment`|식 결과의 문자열 표현에 최소 문자 수를 정의하는 값을 갖는 상수 식입니다. 양수이면 문자열 표현이 오른쪽에 맞춰지며, 음수이면 왼쪽에 맞춰집니다. 자세한 내용은 [맞춤 구성 요소](../../../standard/base-types/composite-formatting.md#alignment-component)를 참조하세요.|
|`formatString`|식 결과의 형식을 기준으로 지원되는 서식 문자열입니다. 자세한 내용은 [서식 문자열 구성 요소](../../../standard/base-types/composite-formatting.md#format-string-component)를 참조하세요.|

다음 예제에서는 위에 설명된 선택적 서식 지정 구성 요소를 사용합니다.

[!code-csharp-interactive[specify alignment and format string](~/samples/snippets/csharp/language-reference/tokens/string-interpolation.cs#2)]

## <a name="special-characters"></a>특수 문자

보간된 문자열로 생성된 문자에 중괄호("{" 또는 "}")를 포함하려면 두 개의 중괄호("{{" 또는 "}}")를 사용합니다. 자세한 내용은 [중괄호 이스케이프](../../../standard/base-types/composite-formatting.md#escaping-braces)를 참조하세요.

콜론(":")은 보간 식 항목에서 특별한 의미가 있으므로, 보간 식에서 [조건부 연산자](../operators/conditional-operator.md)를 사용하려면 해당 식을 괄호로 묶습니다.

다음 예제에서는 중괄호를 결과 문자열에 포함하는 방법과 보간 식에서 조건부 연산자를 사용하는 방법을 보여줍니다.

[!code-csharp-interactive[example with ternary conditional operator](~/samples/snippets/csharp/language-reference/tokens/string-interpolation.cs#3)]

보간된 약어 문자열은 `@` 문자가 뒤에 오는 `$` 문자로 시작합니다. 약어 문자열에 대한 자세한 내용은 [문자열](../keywords/string.md) 및 [약어 식별자](verbatim.md) 항목을 참조하세요.

> [!NOTE]
> C# 8.0부터는 `$` 및 `@` 토큰을 순서에 관계없이 사용할 수 있습니다. `$@"..."` 및 `@$"..."`는 모두 유효한 보간된 약어 문자열입니다. 이전 C# 버전에서는 `$` 토큰이 `@` 토큰 앞에 나타나야 했습니다.

## <a name="implicit-conversions-and-how-to-specify-iformatprovider-implementation"></a>암시적 변환 및 `IFormatProvider` 구현 지정 방법

보간된 문자열에서 다음과 같은 세 가지 암시적 변환을 수행할 수 있습니다.

1. 보간된 문자열을 <xref:System.String> 인스턴스로 변환. 보간 식 항목을 사용하여 보간된 문자열을 확인한 결과를 올바르게 서식이 지정된 문자열 표현으로 바꾼 것입니다. 이 변환에서는 <xref:System.Globalization.CultureInfo.CurrentCulture>를 사용하여 식 결과의 형식을 지정합니다.

1. 보간된 문자열을 서식을 지정할 식 결과와 함께 복합 서식 문자열을 나타내는 <xref:System.FormattableString> 인스턴스로 변환. 이 변수를 사용하면 단일 <xref:System.FormattableString> 인스턴스에서 문화권별 콘텐츠가 포함된 여러 결과 문자열을 만들 수 있습니다. 이렇게 하려면 다음 메서드 중 하나를 호출합니다.

      - <xref:System.Globalization.CultureInfo.CurrentCulture>에 대한 결과 문자열을 생성하는 <xref:System.FormattableString.ToString> 오버로드.
      - <xref:System.Globalization.CultureInfo.InvariantCulture>에 대한 결과 문자열을 생성하는 <xref:System.FormattableString.Invariant%2A> 메서드.
      - 지정된 문화에 대한 결과 문자열을 생성하는 <xref:System.FormattableString.ToString(System.IFormatProvider)> 메서드.

    <xref:System.FormattableString.ToString(System.IFormatProvider)> 메서드를 사용하여 사용자 지정 형식을 지원하는 <xref:System.IFormatProvider> 인터페이스의 사용자 정의 구현을 제공할 수도 있습니다. 자세한 내용은 [.NET의 형식 서식 지정](../../../standard/base-types/formatting-types.md) 문서의 [ICustomFormatter를 사용하여 사용자 지정 형식 지정](../../../standard/base-types/formatting-types.md#custom-formatting-with-icustomformatter) 섹션을 참조하세요.

1. 보간된 문자열을 <xref:System.IFormattable> 인스턴스로 변환. 또한 이 인스턴스를 사용하면 단일 <xref:System.IFormattable> 인스턴스의 문화권별 콘텐츠로 여러 결과 문자열을 만들 수 있습니다.

다음 예제에서는 <xref:System.FormattableString>에 대한 암시적 변환을 사용하여 문화권별 결과 문자열을 만듭니다.

[!code-csharp-interactive[create culture-specific result strings](~/samples/snippets/csharp/language-reference/tokens/string-interpolation.cs#4)]

## <a name="additional-resources"></a>추가 자료

문자열 보간을 처음 접하는 경우 [C#의 문자열 보간](../../tutorials/exploration/interpolated-strings.yml) 대화형 자습서를 참조하세요. 보간된 문자열을 사용하여 서식화된 문자열을 생성하는 방법을 보여 주는 다른 [C#의 문자열 보간](../../tutorials/string-interpolation.md) 자습서도 확인할 수 있습니다.

## <a name="compilation-of-interpolated-strings"></a>보간된 문자열의 컴파일

보간된 문자열이 `string` 형식이면 일반적으로 <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드 호출로 변환됩니다. 컴파일러는 분석된 동작이 연결에 해당하는 경우 <xref:System.String.Format%2A?displayProperty=nameWithType>을 <xref:System.String.Concat%2A?displayProperty=nameWithType>으로 바꿀 수 있습니다.

보간된 문자열 형식이 <xref:System.IFormattable> 또는 <xref:System.FormattableString>이면 컴파일러가 <xref:System.Runtime.CompilerServices.FormattableStringFactory.Create%2A?displayProperty=nameWithType> 메서드에 대한 호출을 생성합니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [보간된 문자열](~/_csharplang/spec/expressions.md#interpolated-strings) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 특수 문자](index.md)
- [문자열](../../programming-guide/strings/index.md)
- [숫자 결과 형식 지정 표](../keywords/formatting-numeric-results-table.md)
- [복합 형식 지정](../../../standard/base-types/composite-formatting.md)
- <xref:System.String.Format%2A?displayProperty=nameWithType>
