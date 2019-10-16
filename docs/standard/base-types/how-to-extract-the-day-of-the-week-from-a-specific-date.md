---
title: '방법: 특정 날짜의 요일 추출'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [.NET Framework], dates
- DateTime.DayOfWeek property
- DateTime.ToString method
- dates [.NET Framework], retrieving week information
- DateTimeOffset.DayOfWeek property
- dates [.NET Framework], day of week
- Weekday function
- day of week [.NET Framework]
- extracting day of week
- weekday names
- WeekdayName function
- numbers [.NET Framework], day of week
- formatting [.NET Framework], time
- DateTimeOffset.ToString method
- full weekday names
ms.assetid: 1c9bef76-5634-46cf-b91c-9b9eb72091d7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 55bdf4cf589bd912dbfc85777542150696aaa436
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65589784"
---
# <a name="how-to-extract-the-day-of-the-week-from-a-specific-date"></a>방법: 특정 날짜의 요일 추출
.NET Framework를 사용하면 쉽게 특정 날짜가 일주일 중 몇 번째 날인지 확인하고, 특정 날짜의 지역화된 요일 이름을 표시할 수 있습니다. 특정 날짜에 해당하는 요일을 나타내는 열거형 값은 <xref:System.DateTime.DayOfWeek%2A> 또는 <xref:System.DateTimeOffset.DayOfWeek%2A> 속성에서 제공합니다. 이와 대조적으로 요일 이름을 검색하는 것은 날짜 및 시간 값의 `ToString` 메서드 또는 <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드와 같은 서식 지정 메서드를 호출하여 수행할 수 있는 서식 지정 작업입니다. 이 항목에서는 이러한 서식 지정 작업을 수행하는 방법을 보여 줍니다.  
  
### <a name="to-extract-a-number-indicating-the-day-of-the-week-from-a-specific-date"></a>특정 날짜에서 요일을 나타내는 숫자를 추출하려면  
  
1. 날짜의 문자열 표현에 대한 작업을 하는 경우에는 정적 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 메서드를 사용하여 해당 표현을 <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType> 값으로 변환합니다.  
  
2. <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=nameWithType> 속성을 사용하여 요일을 나타내는 <xref:System.DayOfWeek> 값을 검색합니다.  
  
3. 필요한 경우 <xref:System.DayOfWeek> 값을 정수로 캐스팅(C#의 경우) 또는 변환(Visual Basic의 경우)합니다.  
  
 다음 예제에서는 특정 날짜의 요일을 나타내는 정수를 표시합니다.  
  
 [!code-csharp[Formatting.Howto.WeekdayName#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/weekdaynumber7.cs#7)]
 [!code-vb[Formatting.Howto.WeekdayName#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/weekdaynumber7.vb#7)]  
  
### <a name="to-extract-the-abbreviated-weekday-name-from-a-specific-date"></a>특정 날짜에서 간략화된 요일 이름을 추출하려면  
  
1. 날짜의 문자열 표현에 대한 작업을 하는 경우에는 정적 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 메서드를 사용하여 해당 표현을 <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType> 값으로 변환합니다.  
  
2. 현재 문화권 또는 특정 문화권의 간략화된 요일 이름을 추출할 수 있습니다.  
  
    1. 현재 문화권의 간략화된 요일 이름을 추출하려면 날짜 및 시간 값의 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> 인스턴스 메서드를 호출하고 문자열 "ddd"를 `format` 매개 변수로 전달합니다. 다음 예제에서는 <xref:System.DateTime.ToString%28System.String%29> 메서드를 호출하는 방법을 보여 줍니다.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname1.cs#1)]
         [!code-vb[Formatting.Howto.WeekdayName#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname1.vb#1)]  
  
    2. 특정 문화권의 간략화된 요일 이름을 추출하려면 날짜 및 시간 값의 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 인스턴스 메서드를 호출합니다. 문자열 "ddd"를 `format` 매개 변수로 전달합니다. <xref:System.Globalization.CultureInfo> 또는 요일 이름을 <xref:System.Globalization.DateTimeFormatInfo> 매개 변수로 검색하려는 문화권을 나타내는 `provider` 개체를 전달합니다. 다음 코드에서는 fr-FR 문화권을 나타내는 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> 개체를 사용하여 <xref:System.Globalization.CultureInfo> 메서드에 대한 호출을 보여 줍니다.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname2.cs#2)]
         [!code-vb[Formatting.Howto.WeekdayName#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname2.vb#2)]  
  
### <a name="to-extract-the-full-weekday-name-from-a-specific-date"></a>특정 날짜에서 전체 요일 이름을 추출하려면  
  
1. 날짜의 문자열 표현에 대한 작업을 하는 경우에는 정적 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 메서드를 사용하여 해당 표현을 <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType> 값으로 변환합니다.  
  
2. 현재 문화권 또는 특정 문화권의 전체 요일 이름을 추출할 수 있습니다.  
  
    1. 현재 문화권의 요일 이름을 추출하려면 날짜 및 시간 값의 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> 인스턴스 메서드를 호출하고 문자열 "dddd"를 `format` 매개 변수로 전달합니다. 다음 예제에서는 <xref:System.DateTime.ToString%28System.String%29> 메서드를 호출하는 방법을 보여 줍니다.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname4.cs#4)]
         [!code-vb[Formatting.Howto.WeekdayName#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname4.vb#4)]  
  
    2. 특정 문화권의 요일 이름을 추출하려면 날짜 및 시간 값의 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 인스턴스 메서드를 호출합니다. 문자열 "dddd"를 `format` 매개 변수로 전달합니다. <xref:System.Globalization.CultureInfo> 또는 요일 이름을 <xref:System.Globalization.DateTimeFormatInfo> 매개 변수로 검색하려는 문화권을 나타내는 `provider` 개체를 전달합니다. 다음 코드에서는 es-ES 문화권을 나타내는 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> 개체를 사용하여 <xref:System.Globalization.CultureInfo> 메서드에 대한 호출을 보여 줍니다.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname5.cs#5)]
         [!code-vb[Formatting.Howto.WeekdayName#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname5.vb#5)]  
  
## <a name="example"></a>예제  
 이 예제에서는 특정 날짜의 요일, 간략화된 요일 이름 및 전체 요일 이름을 나타내는 숫자를 검색하기 위해 <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> 및 <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=nameWithType> 속성과 <xref:System.DateTime.ToString%2A?displayProperty=nameWithType> 및 <xref:System.DateTimeOffset.ToString%2A?displayProperty=nameWithType> 메서드에 대한 호출을 보여 줍니다.  
  
 [!code-csharp[Formatting.Howto.WeekdayName#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/example6.cs#6)]
 [!code-vb[Formatting.Howto.WeekdayName#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example6.vb#6)]  
  
 개별 언어는 .NET Framework에서 제공하는 기능과 중복되거나 이러한 기능을 보완하는 기능을 제공할 수 있습니다. 예를 들어, Visual Basic에는 다음과 같은 두 가지 함수가 포함되어 있습니다.  
  
- `Weekday`: 특정 날짜의 요일을 나타내는 숫자를 반환합니다. 이 함수는 요일의 첫날 서수 값을 1로 간주하는 반면, <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> 속성은 이를 0으로 간주합니다.  
  
- `WeekdayName`: 현재 문화권에서 특정 요일 숫자에 해당하는 요일 이름을 반환합니다.  
  
 다음 예제에서는 Visual Basic `Weekday` 및 `WeekdayName` 함수의 사용 방법을 보여 줍니다.  
  
 [!code-vb[Formatting.HowTo.WeekdayName#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example9.vb#9)]  
  
 또한 <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> 속성에서 반환하는 값을 사용하여 특정 날짜의 요일 이름을 검색할 수 있습니다. 이렇게 하려면 속성에서 반환하는 <xref:System.Enum.ToString%2A> 값에 대해 <xref:System.DayOfWeek> 메서드를 호출하기만 하면 됩니다. 그러나 이 방법은 다음 예제에 나와 있는 것처럼 현재 문화권의 지역화된 요일 이름을 생성하지 않습니다.  
  
 [!code-csharp[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/Howto1.cs#8)]
 [!code-vb[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/Howto1.vb#8)]  
  
## <a name="see-also"></a>참고 항목

- [서식 지정 작업 수행](../../../docs/standard/base-types/performing-formatting-operations.md)
- [표준 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)
- [사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)
