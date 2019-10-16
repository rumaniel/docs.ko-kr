---
title: '방법: 문자열을 DateTime으로 변환'
description: 날짜 및 시간을 나타내는 문자열을 구문 분석하여 날짜 및 시간 문자열에서 DateTime을 만드는 기술을 알아봅니다.
ms.date: 02/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parsing strings, date and time strings
- date and time strings
- ParseExact method
- enumerations [.NET Framework], parsing strings
- base types, parsing strings
- DateTime object
- time strings
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b4217221cc5199b9d8904be1ca3073878378b4e9
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268175"
---
# <a name="parsing-date-and-time-strings-in-net"></a>.NET에서 날짜 및 시간 문자열 구문 분석

문자열을 구문 분석하여 <xref:System.DateTime> 개체로 변환하려면 날짜 및 시간을 텍스트로 나타내는 방법에 대한 정보를 지정해야 합니다. 문화권에 따라 일, 월 및 연도의 순서를 다르게 사용합니다. 시간 표현에서는 24시간제를 사용하는 경우도 있고 “AM”과 “PM”을 지정하기도 합니다. 애플리케이션에 따라서는 날짜만 필요하거나 시간만 필요한 경우도 있고, 날짜와 시간을 모두 지정해야 하는 경우도 있습니다. 문자열을 <xref:System.DateTime> 개체로 변환하는 방법을 통해 필요한 형식과 애플리케이션에 필요한 날짜 및 시간의 요소에 대한 자세한 정보를 제공할 수 있습니다. 텍스트를 <xref:System.DateTime>으로 올바로 변환하려면 다음 세 가지 하위 작업을 수행해야 합니다.

1. 날짜 및 시간을 나타내는 텍스트에 필요한 형식을 지정해야 합니다.
1. 날짜 시간 형식의 문화권을 지정할 수 있습니다.
1. 텍스트 표현에서 누락된 구성 요소를 날짜 및 시간으로 설정하는 방법을 지정할 수 있습니다.

<xref:System.DateTime.Parse%2A> 및 <xref:System.DateTime.TryParse%2A> 메서드는 날짜 및 시간의 여러 공통된 표현을 변환합니다. <xref:System.DateTime.ParseExact%2A> 및 <xref:System.DateTime.TryParseExact%2A> 메서드는 날짜 및 시간 형식 문자열에 지정된 패턴을 따르는 문자열 표현을 변환합니다. 자세한 내용은 [표준 날짜 및 시간 형식 문자열](standard-date-and-time-format-strings.md) 및 [사용자 지정 날짜 및 시간 형식 문자열](custom-date-and-time-format-strings.md)의 문서를 참조하세요.

현재 <xref:System.Globalization.DateTimeFormatInfo> 개체를 사용하면 텍스트를 날짜 및 시간으로 해석하는 방법을 더 세밀하게 제어할 수 있습니다. <xref:System.Globalization.DateTimeFormatInfo>의 속성은 날짜 및 시간 구분 기호, 월, 일 및 연대의 이름, “AM” 및 “PM” 지정의 형식을 설명합니다. 현재 스레드 문화권에서는 현재 문화권을 나타내는 <xref:System.Globalization.DateTimeFormatInfo>를 제공합니다. 특정 문화권 또는 사용자 지정 설정이 필요한 경우 구문 분석 메서드의 <xref:System.IFormatProvider> 매개 변수를 지정합니다. <xref:System.IFormatProvider> 매개 변수의 경우 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체나 <xref:System.Globalization.DateTimeFormatInfo> 개체를 지정해야 합니다.

날짜 또는 시간을 나타내는 텍스트에 일부 정보가 누락될 수 있습니다. 예를 들어 대부분의 사람은 날짜 “3월 12일”이 현재 연도를 나타낸다고 간주합니다. 마찬가지로 “2018년 3월”은 2018년의 3월을 나타냅니다. 시간을 나타내는 텍스트는 시간, 분 및 AM/PM 지정만 포함하는 경우가 많습니다.  구문 분석 메서드는 적절한 기본값을 사용하여 이러한 누락된 정보를 처리합니다.

- 시간만 있으면 날짜 부분은 현재 날짜를 사용합니다.
- 날짜만 있으면 시간 부분은 자정입니다.
- 날짜에서 연도를 지정하지 않으면 현재 연도가 사용됩니다.
- 일을 지정하지 않으면 해당 월의 1일이 사용됩니다.

문자열에 날짜가 있으면 월과 일 또는 연도 중 하나를 포함해야 합니다. 시간이 있으면 시와 분 또는 AM/PM 지정자 중 하나를 포함해야 합니다.

<xref:System.Globalization.DateTimeStyles.NoCurrentDateDefault> 상수를 지정하여 이러한 기본값을 재정의할 수 있습니다. 이 상수를 사용하면 누락된 연도, 월 또는 일 속성이 값 `1`로 설정됩니다. <xref:System.DateTime.Parse%2A>를 사용하는 [마지막 예제](#styles-example)에서 이 동작을 보여줍니다.

날짜 및 시간 구성 요소 외에도 날짜 및 시간의 문자열 표현은 시간이 UTC(협정 세계시)와 얼마나 다른지를 나타내는 오프셋을 포함할 수 있습니다. 예를 들어, 문자열 "2/14/2007 5:32:00 -7:00"는 UTC보다 7시간 이전인 시간을 가리킵니다. 시간의 문자열 표현에서 오프셋을 생략하면 구문 분석은 해당 <xref:System.DateTime.Kind%2A> 속성이 <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>로 설정된 <xref:System.DateTime> 개체를 반환합니다. 오프셋을 지정하면 구문 분석은 <xref:System.DateTime.Kind%2A> 속성이 <xref:System.DateTimeKind.Local?displayProperty=nameWithType>로 설정되고 해당 값이 컴퓨터의 로컬 표준 시간대로 조정된 <xref:System.DateTime> 개체를 반환합니다. 구문 분석 메서드에서 <xref:System.Globalization.DateTimeStyles> 값을 사용하여 이 동작을 수정할 수 있습니다.
  
서식 공급자는 모호한 날짜를 해석하는 데에도 사용됩니다. “02/03/04” 문자열에서 나타내는 날짜의 구성 요소 중 무엇이 월, 일 및 연도인지가 명확하지 않습니다. 이들 구성 요소는 형식 공급자에서 비슷한 날짜 형식의 순서에 따라 해석됩니다.

## <a name="parse"></a>Parse

다음 예제에서는 <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 메서드를 사용하여 `string`을 <xref:System.DateTime>으로 변환하는 방법을 설명합니다. 이 예제는 현재 스레드와 연결된 문화권을 사용합니다. 현재 문화권과 연결된 <xref:System.Globalization.CultureInfo>가 입력 문자열을 구문 분석할 수 없는 경우 <xref:System.FormatException>이 throw됩니다.

> [!TIP]
> 이 문서의 모든 C# 샘플은 브라우저에서 실행됩니다. **실행** 단추를 눌러 출력을 볼 수 있습니다. 편집해서 직접 실험할 수도 있습니다.

> [!NOTE]
> 이러한 예제는 GitHub 문서 리포지토리에서 [C#](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/conversions) 및 [VB](https://github.com/dotnet/samples/tree/master/snippets/visualbasic/how-to/conversions)용으로 제공됩니다. 또는 [C#](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/conversions.zip) 또는 [VB](https://github.com/dotnet/samples/raw/master/snippets/visualbasic/how-to/conversions.zip)용 zip 파일로 프로젝트를 다운로드할 수 있습니다.

[!code-csharp-interactive[Parsing.DateAndTime#1](../../../samples/snippets/csharp/how-to/conversions/StringToDateTime.cs#1)]
[!code-vb[Parsing.DateAndTime#1](../../../samples/snippets/visualbasic/how-to/conversions/Program.vb#1)]

문자열을 구문 분석할 때 어느 문화권의 서식 규칙을 사용할지 명시적으로 정의할 수도 있습니다. 즉, <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType> 속성에서 반환하는 표준 <xref:System.Globalization.DateTimeFormatInfo> 개체 중 하나를 지정합니다. 다음 예제에서는 형식 공급자를 사용하여 독일어 문자열을 <xref:System.DateTime>으로 구문 분석합니다. 여기서는 `de-DE` 문화권을 나타내는 <xref:System.Globalization.CultureInfo>를 만듭니다. 이 `CultureInfo` 개체는 이 특정 문자열이 성공적으로 구문 분석되도록 합니다. 그러면 <xref:System.Threading.Thread.CurrentThread>의 <xref:System.Threading.Thread.CurrentCulture>에 있는 모든 설정이 불가능합니다.  
  
[!code-csharp[Parsing.DateAndTime#2](../../../samples/snippets/csharp/how-to/conversions/StringToDateTime.cs#2)]
[!code-vb[Parsing.DateAndTime#2](../../../samples/snippets/visualbasic/how-to/conversions/Program.vb#2)]

그러나 <xref:System.DateTime.Parse%2A> 메서드의 오버로드를 사용하여 사용자 지정 형식 공급자를 지정할 수는 있지만, 이 메서드는 비표준 형식의 구문 분석을 지원하지 않습니다. 비표준 서식으로 표현된 날짜 및 시간을 구문 분석하려면 대신 <xref:System.DateTime.ParseExact%2A> 메서드를 사용합니다.  

<a name="styles-example"></a>다음 예제에서는 <xref:System.Globalization.DateTimeStyles> 열거형을 사용하여 지정되지 않은 필드의 <xref:System.DateTime>에 현재 날짜 및 시간 정보를 추가하지 않도록 지정합니다.  

[!code-csharp[Parsing.DateAndTime#3](../../../samples/snippets/csharp/how-to/conversions/StringToDateTime.cs#3)]
[!code-vb[Parsing.DateAndTime#3](../../../samples/snippets/visualbasic/how-to/conversions/Program.vb#3)]
 
## <a name="parseexact"></a>ParseExact

<xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType> 메서드는 지정된 문자열 패턴 중 하나를 따르는 문자열을 <xref:System.DateTime> 개체로 변환합니다. 지정된 형식 중 하나가 아닌 문자열을 이 메서드에 전달하면 <xref:System.FormatException>이 throw됩니다. 표준 날짜 및 시간 형식 지정자 또는 사용자 지정 형식 지정자의 조합 중 하나를 지정할 수 있습니다. 사용자 지정 서식 지정자를 사용하면 사용자 지정 문자열을 생성할 수 있습니다. 지정자에 대한 설명은 [표준 날짜 및 시간 서식 문자열](standard-date-and-time-format-strings.md) 및 [사용자 지정 날짜 및 시간 서식 문자열](custom-date-and-time-format-strings.md)의 항목을 참조하세요.  

다음 예제에서 <xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType> 메서드는 구문 분석할 문자열 개체 뒤에 형식 지정자와 <xref:System.Globalization.CultureInfo> 개체를 전달합니다. 이 <xref:System.DateTime.ParseExact%2A> 메서드는 `en-US` 문화권의 자세한 날짜 패턴을 따라는 문자열만 구문 분석할 수 있습니다.  

[!code-csharp[Parsing.DateAndTime#4](../../../samples/snippets/csharp/how-to/conversions/StringToDateTime.cs#4)]
[!code-vb[Parsing.DateAndTime#4](../../../samples/snippets/visualbasic/how-to/conversions/Program.vb#4)]

<xref:System.DateTime.Parse%2A> 및 <xref:System.DateTime.ParseExact%2A> 메서드의 각 오버로드에는 문자열의 서식 지정에 대한 문화권별 정보를 제공하는 <xref:System.IFormatProvider> 매개 변수도 있습니다. 이 <xref:System.IFormatProvider> 개체는 표준 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체이거나 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType> 속성에서 반환하는 <xref:System.Globalization.DateTimeFormatInfo> 개체입니다.  <xref:System.DateTime.ParseExact%2A>는 하나 이상의 사용자 지정 날짜 및 시간 형식을 정의하는 추가 문자열이나 문자열 배열 인수도 사용합니다.  

## <a name="see-also"></a>참고 항목

- [Parsing Strings](parsing-strings.md)
- [형식 서식 지정](formatting-types.md)
- [.NET에서 형식 변환](type-conversion.md)
- [표준 날짜 및 시간 형식](standard-date-and-time-format-strings.md)
- [사용자 지정 날짜 및 시간 형식 문자열](custom-date-and-time-format-strings.md)
