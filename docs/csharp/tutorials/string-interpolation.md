---
title: C#의 문자열 보간
description: 문자열 보간을 사용하여 C#으로 결과 문자열에 서식이 지정된 식 결과를 포함하는 방법을 알아봅니다.
author: pkulikov
ms.date: 09/02/2019
ms.openlocfilehash: d3a3a08d5911b5323aa61c571f05318d10380339
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252924"
---
# <a name="string-interpolation-in-c"></a>C\#의 문자열 보간

이 자습서에서는 [문자열 보간](../language-reference/tokens/interpolated.md)을 사용하여 결과 문자열에서 식 결과의 서식을 지정하고 포함하는 방법을 보여줍니다. 예제에서는 사용자가 기본 C# 개념 및 .NET 형식 서식 지정에 익숙하다고 가정합니다. 문자열 보간 또는 .NET 형식 서식 지정을 처음 접하는 경우 [대화형 문자열 보간 자습서](exploration/interpolated-strings.yml)을 먼저 체크 아웃합니다. .NET에서 형식 서식 지정하는 방법에 대한 자세한 내용은 [.NET의 형식 지정](../../standard/base-types/formatting-types.md) 항목을 참조하세요.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

## <a name="introduction"></a>소개

[문자열 보간](../language-reference/tokens/interpolated.md) 기능은 [복합 서식 지정](../../standard/base-types/composite-formatting.md) 기능을 기반으로 빌드되고 결과 문자열에 서식이 지정된 식 결과를 포함하는 읽기 쉽고 편리한 구문을 제공합니다.

문자열 리터럴을 보간된 문자열로 식별하려면 `$` 기호를 사용하여 추가합니다. 보간된 문자열에서 값을 반환하는 유효한 C# 식을 포함할 수 있습니다. 다음 예제에서는 식이 계산되는 즉시 결과가 문자열로 변환되고 결과 문자열에 포함됩니다.

[!code-csharp-interactive[string interpolation example](~/samples/snippets/csharp/tutorials/string-interpolation/Program.cs#1)]

이 예제에서 볼 수 있듯이 중괄호를 포함하여 보간된 문자열에 식을 포함합니다.

```csharp
{<interpolationExpression>}
```

보간된 문자열은 [문자열 복합 서식 지정](../../standard/base-types/composite-formatting.md) 기능의 모든 기능을 지원합니다. 따라서 <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드를 사용할 때 보다 읽기 쉬운 대안이 됩니다.

## <a name="how-to-specify-a-format-string-for-an-interpolation-expression"></a>보간 식에 대한 서식 문자열을 지정하는 방법

콜론(":")과 형식 문자열을 사용하여 보간 식에 따라 식 결과의 형식에서 지원하는 형식 문자열을 지정합니다.

```csharp
{<interpolationExpression>:<formatString>}
```

다음 예제에서는 날짜 및 시간 또는 숫자 결과를 생성하는 식의 표준 및 사용자 지정 서식 지정 문자열을 지정하는 방법을 보여줍니다.

[!code-csharp-interactive[format string example](~/samples/snippets/csharp/tutorials/string-interpolation/Program.cs#2)]

자세한 내용은 [복합 서식 지정](../../standard/base-types/composite-formatting.md) 항목의 [문자열 구성 요소 서식 지정](../../standard/base-types/composite-formatting.md#format-string-component) 섹션을 참조하세요. 해당 섹션에서는 .NET 기본 형식에서 지원하는 표준 및 사용자 지정 서식 지정 문자열을 설명하는 항목에 대한 링크를 제공합니다.

## <a name="how-to-control-the-field-width-and-alignment-of-the-formatted-interpolation-expression"></a>필드 너비와 서식이 지정된 보간 식의 맞춤을 제어하는 방법

쉼표(",") 및 상수 식을 포함한 보간 식에 따라 최소 필드 너비 및 서식이 지정된 식 결과의 맞춤을 지정합니다.

```csharp
{<interpolationExpression>,<alignment>}
```

*맞춤* 값이 양수이면 서식이 지정된 식 결과는 오른쪽 맞춤입니다. 값이 음수이면 왼쪽 맞춤입니다.

맞춤 및 서식 문자열을 모두 지정해야 할 경우 맞춤 구성 요소를 시작합니다.

```csharp
{<interpolationExpression>,<alignment>:<formatString>}
```

다음 예제에서는 맞춤을 지정하고 파이프 문자("|")를 사용하여 텍스트 필드를 구분하는 방법을 보여줍니다.

[!code-csharp-interactive[alignment example](~/samples/snippets/csharp/tutorials/string-interpolation/Program.cs#3)]

출력 표시 예제에서 볼 수 있듯이 서식이 지정된 식 결과의 길이가 지정된 필드 너비를 초과하는 경우 *맞춤* 값은 무시됩니다.

자세한 내용은 [복합 서식 지정](../../standard/base-types/composite-formatting.md) 항목의 [맞춤 구성 요소](../../standard/base-types/composite-formatting.md#alignment-component) 섹션을 참조하세요.

## <a name="how-to-use-escape-sequences-in-an-interpolated-string"></a>보간된 문자열에서 이스케이프 시퀀스를 사용하는 방법

보간된 문자열에서는 일반 문자열 리터럴을 사용할 수 있는 모든 이스케이프 시퀀스를 지원합니다. 자세한 내용은 [문자열 이스케이프 시퀀스](../programming-guide/strings/index.md#string-escape-sequences)를 참조하세요.

이스케이프 시퀀스를 문자 그대로 해석하려면 [약어](../language-reference/tokens/verbatim.md) 리터럴 문자열을 사용합니다. 보간된 약어 문자열은 `@` 문자가 뒤에 오는 `$` 문자로 시작합니다. C# 8.0부터는 `$` 및 `@` 토큰을 순서에 관계없이 사용할 수 있습니다. `$@"..."` 및 `@$"..."`는 모두 유효한 보간된 약어 문자열입니다.

중괄호("{" 또는 "}")를 포함하려면 결과 문자열에서 2개의 중괄호("{{" 또는 "}}")를 사용합니다. 자세한 내용은 [복합 서식 지정](../../standard/base-types/composite-formatting.md) 항목의 [중괄호 이스케이프 처리](../../standard/base-types/composite-formatting.md#escaping-braces) 섹션을 참조하세요.

다음 예제에서는 결과 문자열에 중괄호를 포함하고 약어 보간된 문자열을 만드는 방법을 보여줍니다.

[!code-csharp-interactive[escape sequence example](~/samples/snippets/csharp/tutorials/string-interpolation/Program.cs#4)]

## <a name="how-to-use-a-ternary-conditional-operator--in-an-interpolation-expression"></a>보간 식에서 3개로 구성된 `?:` 조건부 연산자를 사용하는 방법

보간 식에서 콜론(":")에 특별한 의미가 있으므로 식에서 [조건부 연산자](../language-reference/operators/conditional-operator.md)를 사용하기 위해 다음 예제에서 볼 수 있듯이 해당 식을 괄호로 묶습니다.

[!code-csharp-interactive[conditional operator example](~/samples/snippets/csharp/tutorials/string-interpolation/Program.cs#5)]

## <a name="how-to-create-a-culture-specific-result-string-with-string-interpolation"></a>문자열 보간을 사용하여 문화권별 결과 문자열을 만드는 방법

기본적으로는 보간된 문자열은 모든 서식 지정 작업에 대해 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=nameWithType> 속성에서 정의한 현재 문화권을 사용합니다. <xref:System.FormattableString?displayProperty=nameWithType> 인스턴스에 대한 보간된 문자열의 암시적 변환을 사용하고 해당 <xref:System.FormattableString.ToString(System.IFormatProvider)> 메서드를 호출하여 문화권별 결과 문자열을 만듭니다. 다음 예제에서는 해당 작업을 수행하는 방법을 보여줍니다.

[!code-csharp-interactive[specify different cultures](~/samples/snippets/csharp/tutorials/string-interpolation/Program.cs#6)]

이 예제에서 볼 수 있듯이 하나의 <xref:System.FormattableString> 인스턴스를 사용하여 다양한 문화권에 여러 결과 문자열을 생성할 수 있습니다.

## <a name="how-to-create-a-result-string-using-the-invariant-culture"></a>고정 문화권을 사용하여 결과 문자열을 만드는 방법

<xref:System.FormattableString.ToString(System.IFormatProvider)?displayProperty=nameWithType> 메서드와 함께 고정 <xref:System.FormattableString.Invariant%2A?displayProperty=nameWithType> 메서드를 사용하여 <xref:System.Globalization.CultureInfo.InvariantCulture>에서 보간된 문자열을 결과 문자열로 해결할 수 있습니다. 다음 예제에서는 해당 작업을 수행하는 방법을 보여줍니다.

[!code-csharp-interactive[format with invariant culture](~/samples/snippets/csharp/tutorials/string-interpolation/Program.cs#7)]

## <a name="conclusion"></a>결론

이 자습서에서는 문자열 보간 사용법의 일반적인 시나리오를 설명합니다. 문자열 보간에 대한 자세한 내용은 [문자열 보간](../language-reference/tokens/interpolated.md) 항목을 참조하세요. .NET에서 형식 서식 지정하는 방법에 대한 자세한 내용은 [.NET의 형식 지정](../../standard/base-types/formatting-types.md) 및 [복합 서식 지정](../../standard/base-types/composite-formatting.md) 항목을 참조하세요.

## <a name="see-also"></a>참고 항목

- <xref:System.String.Format%2A?displayProperty=nameWithType>
- <xref:System.FormattableString?displayProperty=nameWithType>
- <xref:System.IFormattable?displayProperty=nameWithType>
- [문자열](../programming-guide/strings/index.md)
