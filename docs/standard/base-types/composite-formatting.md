---
title: 복합 형식 지정
ms.date: 10/26/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parameter specifiers
- strings [.NET Framework], alignment
- format specifiers, composite formatting
- strings [.NET Framework], composite
- composite formatting
- objects [.NET Framework], formatting multiple objects
ms.assetid: 87b7d528-73f6-43c6-b71a-f23043039a49
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8d0574c7e0910a658f1dc80d8394f55b472c31a3
ms.sourcegitcommit: 46c68557bf6395f0ab9915f7558f2faae0097695
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/12/2019
ms.locfileid: "64634566"
---
# <a name="composite-formatting"></a>복합 형식 지정

.NET의 복합 형식 지정 기능에는 개체 목록과 복합 형식 문자열이 입력으로 사용됩니다. 합성 서식 문자열은 고정 텍스트와 목록의 개체에 해당하는 인덱싱된 자리 표시자(서식 항목이라고 함)가 결합된 형태로 구성됩니다. 서식 지정 작업을 통해 원래의 고정 텍스트와 목록에 있는 개체의 문자열 표현이 결합된 형태의 결과 문자열을 얻을 수 있습니다.  
  
> [!IMPORTANT]
> 복합 형식 문자열을 사용하는 대신 사용 중인 언어 및 언어 버전에서 지원하는 경우 *보간된 문자열*을 사용할 수 있습니다. 보간된 문자열은 *보간된 식*이 포함된 문자열입니다. 각 보간된 표현식은 표현식의 값으로 해석되고 문자열이 할당될 때 결과 문자열에 포함됩니다. 자세한 내용은 [문자열 보간(C# 참조)](../../csharp/language-reference/tokens/interpolated.md) 및 [문자열 보간(Visual Basic 참조)](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md)을 참조하세요.

다음과 같은 메서드에서 합성 형식 지정 기능을 지원합니다.  
  
- 서식이 지정된 결과 문자열을 반환하는 <xref:System.String.Format%2A?displayProperty=nameWithType>.  
  
- 서식이 지정된 결과 문자열을 <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType> 개체에 추가하는 <xref:System.Text.StringBuilder>.   
- 콘솔에 서식이 지정된 결과 문자열을 표시하는 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> 메서드의 과부하.  
  
- 스트림 또는 파일에 서식이 지정된 결과 문자열을 쓰는 <xref:System.IO.TextWriter.WriteLine%2A?displayProperty=nameWithType> 메서드의 과부하. <xref:System.IO.TextWriter> 및 <xref:System.IO.StreamWriter>와 같은 <xref:System.Web.UI.HtmlTextWriter>에서 파생된 클래스도 이 기능을 공유합니다.  
  
- 추적 수신기로 서식이 지정된 메시지를 출력하는 <xref:System.Diagnostics.Debug.WriteLine%28System.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType>.  
  
- 추적 수신기로 서식이 지정된 메시지를 출력하는 <xref:System.Diagnostics.Trace.TraceError%28System.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType>, <xref:System.Diagnostics.Trace.TraceInformation%28System.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 및 <xref:System.Diagnostics.Trace.TraceWarning%28System.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 메서드.  
  
- 추적 수신기에 정보 메서드를 쓰는 <xref:System.Diagnostics.TraceSource.TraceInformation%28System.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 메서드.  
  
## <a name="composite-format-string"></a>합성 서식 문자열  
 합성 서식 문자열과 개체 목록은 합성 서식 지정 기능을 지원하는 메서드의 인수로 사용됩니다. 합성 서식 문자열은 0개 이상의 고정 텍스트가 하나 이상의 서식 항목과 결합된 형태로 구성됩니다. 고정 텍스트는 사용자가 선택하는 임의의 문자열이고, 각 서식 항목은 목록의 개체나 boxed 구조체에 해당합니다. 합성 서식 지정 기능은 각 서식 항목을 목록에 있는 해당 개체의 문자열 표현으로 바꿔 새로운 결과 문자열을 반환합니다.  
  
 다음은 이 기능을 보여 주는 <xref:System.String.Format%2A> 코드 조각입니다.  
  
 [!code-csharp[Formatting.Composite#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#1)]
 [!code-vb[Formatting.Composite#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#1)]  
  
 고정 텍스트는 “`Name =`” 및 “`, hours =`”입니다. 형식 항목은 인덱스가 0이고 `name` 개체에 해당하는 “`{0}`”과(와) 인덱스가 1이고 `DateTime.Now` 개체에 해당하는 “`{1:hh}`”입니다.  
  
## <a name="format-item-syntax"></a>서식 항목 구문  
 각 서식 항목의 형태와 구성 요소는 다음과 같습니다.  
  
 `{` *index*[`,`*alignment*][`:`*formatString*]`}`  
  
 여기서 중괄호("{"와 "}")의 짝이 반드시 맞아야 합니다.  
  
### <a name="index-component"></a>Index 구성 요소  
 매개 변수 지정자라고도 하는 필수 *index* 구성 요소는 0부터 시작하는 숫자로, 개체 목록에서 해당하는 항목을 식별합니다. 즉, 매개 변수 지정자가 0인 서식 항목은 목록에 있는 첫째 개체의 서식을 지정하고 매개 변수 지정자가 1인 서식 항목은 목록에 있는 둘째 개체의 서식을 지정하는 식으로 적용됩니다. 다음 예제에는 10보다 작은 소수를 나타내고 0부터 3까지 번호가 매겨진 4개의 매개 변수 지정자가 포함되어 있습니다.  
  
 [!code-csharp[Formatting.Composite#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/index1.cs#7)]
 [!code-vb[Formatting.Composite#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/index1.vb#7)]  
  
 동일한 매개 변수 지정자를 지정하여 여러 서식 항목이 개체 목록의 동일한 요소를 참조하도록 할 수 있습니다. 예를 들어, 복합 서식 문자열을 다음과 같이 지정하여 동일한 숫자 값을 16진수, 지수 및 숫자 서식으로 지정할 수 있습니다. 다음 예제와 같이 "0x{0:X} {0:E} {0:N}"가 표시됩니다.  
  
 [!code-csharp[Formatting.Composite#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/index1.cs#10)]
 [!code-vb[Formatting.Composite#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/index1.vb#10)]  
  
 각 서식 항목은 목록의 어떤 개체나 참조할 수 있습니다. 예를 들어, 세 개의 개체가 있을 경우 “{1} {0} {2}”와 같이 복합 형식 문자열을 지정하여 둘째, 첫째, 셋째 개체의 서식을 지정할 수 있습니다. 서식 항목에서 참조하지 않는 개체는 무시됩니다. 매개 변수 지정자가 개체 목록 범위를 벗어나는 항목을 지정하면 런타임에 <xref:System.FormatException>이 발생합니다.  
  
### <a name="alignment-component"></a>Alignment 구성 요소  
 선택적인 *alignment* 구성 요소는 기본 형식의 필드 너비를 나타내는 부호 있는 정수입니다. *alignment* 값이 형식이 지정된 문자열보다 작으면 *alignment*는 무시되고 형식이 지정된 문자열의 길이가 필드 너비로 사용됩니다. *alignment*가 양수이면 필드에서 형식이 지정된 데이터가 오른쪽 맞춤되고 *alignment*가 음수이면 왼쪽 맞춤됩니다. 채우기가 필요하면 공백이 사용됩니다. *alignment*를 지정하는 경우 쉼표가 필요합니다.  
  
 다음 예제에서는 두 배열, 즉 직원의 이름을 포함하는 배열과 2주 동안의 작업 시간을 포함하는 배열을 정의합니다. 복합 형식 문자열은 20자 필드에 이름을 왼쪽 맞춤하고 5자 필드에 해당 시간을 오른쪽 맞춤합니다. 소수 1자리로 시간 형식을 지정하기 위해 "N1" 표준 형식 문자열도 사용됩니다.  
  
 [!code-csharp[Formatting.Composite#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/alignment1.cs#8)]
 [!code-vb[Formatting.Composite#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/alignment1.vb#8)]  
  
### <a name="format-string-component"></a>Format String 구성 요소  
 선택적 *formatString* 구성 요소는 서식을 지정할 개체 형식에 적절한 형식 문자열입니다. 해당 개체가 숫자 값이면 표준 또는 사용자 지정 숫자 형식 문자열을, <xref:System.DateTime> 개체이면 표준 또는 사용자 지정 날짜 및 시간 형식 문자열을, 열거형 값이면 [열거형 서식 문자열](../../../docs/standard/base-types/enumeration-format-strings.md)을 지정합니다. *formatString*을 지정하지 않으면 숫자, 날짜 및 시간, 또는 열거형 형식에 대해 일반("G") 형식 지정자가 사용됩니다. *formatString*을 지정하는 경우 콜론이 필요합니다.  
  
 다음 표에는 미리 정의된 서식 문자열 집합을 지원하는 .NET Framework 클래스 라이브러리의 형식 또는 형식 범주와 지원되는 서식 문자열을 나열하는 항목에 대한 링크가 나와 있습니다. 문자열 서식 지정은 애플리케이션 정의 형식에서 지원하는 형식 문자열 집합을 정의하는, 모든 기존 형식을 위한 새 형식 문자열을 정의하는 확장 가능한 메커니즘입니다. 자세한 내용은 <xref:System.IFormattable> 및 <xref:System.ICustomFormatter> 인터페이스 항목을 참조하세요.  
  
|형식 또는 형식 범주|참조|  
|---------------------------|---------|  
|날짜 및 시간 형식(<xref:System.DateTime>, <xref:System.DateTimeOffset>)|[표준 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)<br /><br /> [사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)|  
|열거형 형식(<xref:System.Enum?displayProperty=nameWithType>에서 파생되는 모든 형식)|[Enumeration Format Strings](../../../docs/standard/base-types/enumeration-format-strings.md)|  
|숫자 형식(<xref:System.Numerics.BigInteger>, <xref:System.Byte>, <xref:System.Decimal>, <xref:System.Double>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.Single>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64>)|[Standard Numeric Format Strings](../../../docs/standard/base-types/standard-numeric-format-strings.md)<br /><br /> [Custom Numeric Format Strings](../../../docs/standard/base-types/custom-numeric-format-strings.md)|  
|<xref:System.Guid>|<xref:System.Guid.ToString%28System.String%29?displayProperty=nameWithType>|  
|<xref:System.TimeSpan>|[표준 TimeSpan 서식 문자열](../../../docs/standard/base-types/standard-timespan-format-strings.md)<br /><br /> [사용자 지정 TimeSpan 서식 문자열](../../../docs/standard/base-types/custom-timespan-format-strings.md)|  
  
### <a name="escaping-braces"></a>이스케이프 중괄호  
 여는 중괄호와 닫는 중괄호는 서식 항목의 시작과 끝으로 해석됩니다. 따라서 리터럴 여는 중괄호나 닫는 중괄호를 표시하려면 이스케이프 시퀀스를 사용해야 합니다. 고정 텍스트에서 여는 중괄호 2개("{{")를 사용하면 여는 중괄호 1개("{")가, 닫는 중괄호 2개("}}")를 사용하면 닫는 중괄호 1개("}")가 표시됩니다. 서식 항목에서 중괄호는 나타나는 순서대로 해석됩니다. 중첩 중괄호 해석은 지원되지 않습니다.  
  
 이스케이프된 중괄호가 해석되는 방식에 따라 예기치 않은 결과가 나올 수도 있습니다. 예를 들어 여는 중괄호, 10진수로 서식 지정된 숫자 값 및 닫는 중괄호를 표시하기 위해 서식 항목 “{{{0:D}}}”를 사용했다고 가정해 봅시다. 그러나 이 서식 항목은 다음과 같이 해석됩니다.  
  
1. 맨 처음 여는 중괄호 2개("{{")는 이스케이프되어 여는 중괄호 1개가 됩니다.  
  
2. 그 다음 3개의 문자("{0:")는 서식 항목의 시작으로 해석됩니다.  
  
3. 다음 문자("D")는 10진 표준 숫자 서식 지정자로 해석되지만, 그 다음 이스케이프된 중괄호 2개("}}")는 중괄호 1개로 인식됩니다. 결과 문자열("D}")은 표준 숫자 서식 지정자가 아니므로 리터럴 문자열 "D}"를 표시하는 사용자 지정 서식 문자열로 해석됩니다.  
  
4. 마지막 중괄호("}")는 서식 항목의 끝으로 해석됩니다.  
  
5. 표시되는 최종 결과는 리터럴 문자열 "{D}"입니다. 서식 지정 시 의도했던 숫자 값이 표시되지 않습니다.  
  
 이스케이프된 중괄호 및 서식 항목이 잘못 해석되지 않도록 코드를 작성하는 방법 중 하나는 중괄호와 서식 항목의 서식을 따로 지정하는 것입니다. 즉, 첫째 서식 작업에서 리터럴 여는 중괄호를 표시하고 다음 작업에서 서식 항목의 결과를 표시한 다음 마지막 작업에서 리터럴 닫는 괄호를 표시합니다. 다음 예제에서 이 방법을 보여 줍니다.  
  
 [!code-csharp[Formatting.Composite#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Escaping1.cs#2)]
 [!code-vb[Formatting.Composite#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Escaping1.vb#2)]  
  
### <a name="processing-order"></a>처리 순서  
 합성 서식 지정 메서드에 대한 호출에 값이 <xref:System.IFormatProvider>이 아닌 `null` 인수가 포함되는 경우, 런타임은 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 메서드를 호출하여 <xref:System.ICustomFormatter> 구현을 요청합니다. 메서드가 <xref:System.ICustomFormatter> 구현을 반환할 수 있는 경우 복합 서식 지정 메서드의 호출 기간 동안 캐시됩니다.
  
 다음과 같이 서식 항목에 상응하는 매개 변수 목록의 각 값이 문자열로 변환됩니다.  
  
1. 서식을 지정할 값이 `null`이면 빈 문자열 <xref:System.String.Empty?displayProperty=nameWithType>이 반환됩니다.  
  
2. <xref:System.ICustomFormatter> 구현을 사용할 수 있는 경우 런타임은 <xref:System.ICustomFormatter.Format%2A> 메서드를 호출합니다. <xref:System.IFormatProvider> 구현과 함께, 형식 항목의 *formatString* 값이 있는 경우 메서드에 이 값을 전달하고, 값이 없는 경우에는 `null`을 전달합니다. <xref:System.ICustomFormatter.Format%2A?displayProperty=nameWithType> 메서드에 대한 호출이 `null`을 반환하는 경우 실행은 다음 단계로 진행합니다. 그렇지 않은 경우 <xref:System.ICustomFormatter.Format%2A?displayProperty=nameWithType> 호출의 결과가 반환됩니다.
  
3. 값이 <xref:System.IFormattable> 인터페이스를 구현하면 인터페이스의 <xref:System.IFormattable.ToString%28System.String%2CSystem.IFormatProvider%29> 메서드가 호출됩니다. *formatString* 값(형식 항목에 있는 경우) 또는 `null`(없는 경우)이 메서드에 전달됩니다. <xref:System.IFormatProvider> 인수는 다음과 같이 결정됩니다.  
  
    - 숫자 값의 경우, null이 아닌 <xref:System.IFormatProvider> 인수가 있는 합성 서식 지정 메서드가 호출되면 런타임이 <xref:System.Globalization.NumberFormatInfo> 메서드에서 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 개체를 요청합니다. 값을 제공할 수 없거나, 인수 값이 `null`이거나, 합성 서식 지정 메서드에 <xref:System.IFormatProvider> 매개 변수가 없는 경우, 현재 스레드 문화권에 대한 <xref:System.Globalization.NumberFormatInfo> 개체가 사용됩니다.  
  
    - 날짜 및 시간 값의 경우, null이 아닌 <xref:System.IFormatProvider> 인수가 있는 합성 서식 지정 메서드가 호출되면 런타임이 <xref:System.Globalization.DateTimeFormatInfo> 메서드에서 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 개체를 요청합니다. 값을 제공할 수 없거나, 인수 값이 `null`이거나, 합성 서식 지정 메서드에 <xref:System.IFormatProvider> 매개 변수가 없는 경우, 현재 스레드 문화권에 대한 <xref:System.Globalization.DateTimeFormatInfo> 개체가 사용됩니다.  
  
    - 다른 형식의 개체에 대해, 복합 형식 지정 메서드가 <xref:System.IFormatProvider> 인수와 함께 호출되는 경우 그 값은 <xref:System.IFormattable.ToString%2A?displayProperty=nameWithType> 구현으로 직접 전달됩니다. 그렇지 않으면 `null`이 <xref:System.IFormattable.ToString%2A?displayProperty=nameWithType> 구현으로 전달됩니다.  
  
4. `ToString`을 재정의하거나 기본 클래스의 동작을 상속하는, 형식의 매개 변수 없는 <xref:System.Object.ToString?displayProperty=nameWithType> 메서드가 호출됩니다. 이 경우, 형식 항목에서 *formatString* 구성 요소로 지정된 형식 문자열(있는 경우)은 무시됩니다.  
  
 앞의 단계가 수행된 후에 맞춤이 적용됩니다.  
  
## <a name="code-examples"></a>코드 예제  
 다음 예제에서는 합성 서식 지정을 사용하여 만든 문자열과 개체의 `ToString` 메서드를 사용하여 만든 문자열을 보여 줍니다. 두 형식의 서식을 지정한 결과는 같습니다.  
  
 [!code-csharp[Formatting.Composite#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#3)]
 [!code-vb[Formatting.Composite#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#3)]  
  
 오늘이 5월의 목요일이라고 가정할 때 앞의 예제에서 두 문자열의 값은 미국 영어 문화권에서 `Thursday May` 입니다.  
  
 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType>은 <xref:System.String.Format%2A?displayProperty=nameWithType>과 동일한 기능을 제공합니다. 두 메서드가 유일하게 다른 점은 <xref:System.String.Format%2A?displayProperty=nameWithType>은 결과를 문자열로 반환하는 반면 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType>은 <xref:System.Console> 개체와 연결된 출력 스트림에 결과를 쓴다는 것입니다. 다음 예제에서는 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> 메서드를 사용하여 `MyInt` 값의 서식을 통화 값으로 지정합니다.  
  
 [!code-csharp[Formatting.Composite#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#4)]
 [!code-vb[Formatting.Composite#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#4)]  
  
 다음 예제에서는 하나의 개체 서식을 두 가지 다른 방법으로 지정하는 경우를 비롯하여 여러 개체의 서식을 지정하는 방법을 보여 줍니다.  
  
 [!code-csharp[Formatting.Composite#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#5)]
 [!code-vb[Formatting.Composite#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#5)]  
  
 다음 예제에서는 서식 지정에서 맞춤을 사용하는 방법을 보여 줍니다. 서식 지정되는 인수가 세로줄 문자(&#124;) 사이에 위치하면서 결과 맞춤이 강조됩니다.  
  
 [!code-csharp[Formatting.Composite#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#6)]
 [!code-vb[Formatting.Composite#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#6)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Console.WriteLine%2A>
- <xref:System.String.Format%2A?displayProperty=nameWithType>
- [문자열 보간(C#)](../../csharp/language-reference/tokens/interpolated.md)
- [문자열 보간(Visual Basic)](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md)
- [형식 서식 지정](../../../docs/standard/base-types/formatting-types.md)
- [표준 숫자 형식 문자열](../../../docs/standard/base-types/standard-numeric-format-strings.md)
- [사용자 지정 숫자 형식 문자열](../../../docs/standard/base-types/custom-numeric-format-strings.md)
- [표준 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)
- [사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)
- [표준 TimeSpan 서식 문자열](../../../docs/standard/base-types/standard-timespan-format-strings.md)
- [사용자 지정 TimeSpan 서식 문자열](../../../docs/standard/base-types/custom-timespan-format-strings.md)
- [Enumeration Format Strings](../../../docs/standard/base-types/enumeration-format-strings.md)
