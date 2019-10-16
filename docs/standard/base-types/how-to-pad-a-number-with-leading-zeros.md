---
title: '방법: 숫자 앞에 0으로 채우기'
ms.date: 02/25/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- numeric format strings [.NET Framework]
- formatting [.NET Framework], numbers
- number formatting [.NET Framework]
- numbers [.NET Framework], format strings
ms.assetid: 0b2c2cb5-c580-4891-8d81-cb632f5ec384
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 54c3eb734184adf5168607cfc8bcbf6c17ea493a
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57678895"
---
# <a name="how-to-pad-a-number-with-leading-zeros"></a>방법: 숫자 앞에 0으로 채우기

"D" [표준 숫자 서식 문자열](../../../docs/standard/base-types/standard-numeric-format-strings.md)과 함께 전체 자릿수 지정자를 사용하여 앞에 오는 0을 정수에 추가할 수 있습니다. [사용자 지정 숫자 서식 문자열](../../../docs/standard/base-types/custom-numeric-format-strings.md)을 사용하여 정수와 부동 소수점 숫자 둘 다에 앞에 오는 0을 추가할 수 있습니다. 이 문서에서는 두 개의 메서드를 사용하여 앞에 오는 0으로 숫자를 채우는 방법을 보여줍니다.

## <a name="to-pad-an-integer-with-leading-zeros-to-a-specific-length"></a>앞에 오는 0으로 특정 길이까지 정수를 채우려면

1. 표시할 정수 값의 최소 자릿수를 결정합니다. 이 숫자에 원하는 선행 자릿수를 포함합니다.

1. 정수를 10진수 값으로 표시할지 아니면 16진수 값으로 표시할지를 결정합니다.

    - 정수를 10진수 값으로 표시하려면 해당 `ToString(String)` 메서드를 호출하고 문자열 "D*n*"을 `format` 매개 변수의 값으로 전달합니다. 여기서 *n*은 문자열의 최소 길이를 나타냅니다.

    - 정수를 16진수 값으로 표시하려면 해당 `ToString(String)` 메서드를 호출하고 문자열 "X*n*"을 서식 매개 변수의 값으로 전달합니다. 여기서 *n*은 문자열의 최소 길이를 나타냅니다.

[C#](../../csharp/language-reference/tokens/interpolated.md) 및 [Visual Basic](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md) 모두의 보간된 문자열에서 형식 문자열을 사용할 수도 있습니다. 또는 [복합 서식 지정](../../../docs/standard/base-types/composite-formatting.md)을 사용하는 <xref:System.String.Format%2A?displayProperty=nameWithType> 또는 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType>과 같은 메서드를 호출할 수 있습니다.

다음 예제에서는 서식이 지정된 숫자의 전체 길이가 8자 이상이 되도록 앞에 오는 0으로 여러 정수 값의 서식을 지정합니다.

[!code-csharp[Formatting.HowTo.PadNumber#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#1)]
[!code-vb[Formatting.HowTo.PadNumber#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#1)]

## <a name="to-pad-an-integer-with-a-specific-number-of-leading-zeros"></a>특정 수의 앞에 오는 0으로 정수를 채우려면

1. 정수 값을 표시하는 데 사용할 앞에 오는 0의 수를 결정합니다.

1. 정수를 10진수 값으로 표시할지 아니면 16진수 값으로 표시할지를 결정합니다.

    - 10진수 값으로 서식을 지정하려면 "D" 표준 서식 지정자를 사용해야 합니다.

    - 16진수 값으로 서식을 지정하려면 "X" 표준 서식 지정자를 사용해야 합니다.

1. 정수 값의 `ToString("D").Length` 또는 `ToString("X").Length` 메서드를 호출하여 채워지지 않은 숫자 문자열의 길이를 확인합니다.

1. 서식이 지정된 문자열에 포함할 앞에 오는 0의 수를 채워지지 않은 숫자 문자열의 길이에 추가합니다. 앞에 오는 0의 개수를 추가하면 채워진 문자열의 전체 길이를 정의합니다.

1. 정수 값의 `ToString(String)` 메서드를 호출하고, 10진수 문자열의 경우 문자열 "D*n*"을 전달하고 16진수 문자열의 경우 "X*n*"을 전달합니다. 여기서 *n*은 채워진 문자열의 전체 길이를 나타냅니다. 또한 합성 서식 지정을 지원하는 메서드에 "D*n*" 또는 "X*n*" 서식 문자열을 사용할 수 있습니다.

다음 예제에서는 5개의 앞에 오는 0으로 정수 값을 채웁니다.

[!code-csharp[Formatting.HowTo.PadNumber#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#2)]
[!code-vb[Formatting.HowTo.PadNumber#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#2)]

## <a name="to-pad-a-numeric-value-with-leading-zeros-to-a-specific-length"></a>앞에 오는 0으로 특정 길이까지 숫자 값을 채우려면

1. 숫자의 문자열 표현에서 정수 부분을 표시하는 데 사용할 자릿수를 결정합니다. 이 숫자의 전체 자릿수에 원하는 수의 앞에 오는 0을 포함합니다.

1. 0 자리 표시자("0")를 사용하여 0의 최소 개수를 나타내는 사용자 지정 숫자 서식 문자열을 정의합니다.

1. 숫자의 `ToString(String)` 메서드를 호출하여 사용자 지정 서식 문자열에 전달합니다. 합성 서식 지정을 지원하는 문자열 보간 또는 메서드에서 사용자 지정 서식 문자열을 사용할 수도 있습니다.

다음 예제에서는 앞에 오는 0으로 여러 숫자 값의 형식을 지정합니다. 결과적으로 서식이 지정된 숫자의 전체 길이는 10진수의 왼쪽으로 최소한 8자리입니다.

[!code-csharp[Formatting.HowTo.PadNumber#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#3)]
[!code-vb[Formatting.HowTo.PadNumber#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#3)]

## <a name="to-pad-a-numeric-value-with-a-specific-number-of-leading-zeros"></a>특정 수의 앞에 오는 0으로 숫자 값을 채우려면

1. 숫자 값을 표시하는 데 사용할 앞에 오는 0의 수를 결정합니다.

1. 채워지지 않은 숫자 문자열에서 정수 부분의 자릿수를 확인합니다.

    1. 숫자의 문자열 표현에 소수점 기호가 포함되어 있는지 확인합니다.

    1. 소수점 기호가 포함되어 있으면 정수 부분에 있는 문자 수를 확인합니다.

         또는

         소수점 기호가 포함되어 있지 않으면 문자열의 길이를 확인합니다.

1. 다음을 사용하는 사용자 지정 형식 문자열을 만듭니다.

    - 문자열에 표시할 앞에 오는 0 각각에 대한 0 자리 표시자("0").

    - 기본 문자열의 각 숫자를 나타내는 0 자리 표시자 또는 10진수 자리 표시자("#").

1. 사용자 지정 서식 문자열을 숫자의 `ToString(String)` 메서드에 대한 매개 변수 또는 합성 서식 지정을 지원하는 메서드에 대한 매개 변수로 제공합니다.

다음 예제에서는 5개의 앞에 오는 0으로 두 개의 <xref:System.Double> 값을 채웁니다.

[!code-csharp[Formatting.HowTo.PadNumber#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#4)]
[!code-vb[Formatting.HowTo.PadNumber#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#4)]

## <a name="see-also"></a>참고 항목

- [Custom Numeric Format Strings](../../../docs/standard/base-types/custom-numeric-format-strings.md)
- [Standard Numeric Format Strings](../../../docs/standard/base-types/standard-numeric-format-strings.md)
- [복합 형식 지정](../../../docs/standard/base-types/composite-formatting.md)
