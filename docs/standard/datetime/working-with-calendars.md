---
title: 달력 작업
ms.date: 04/01/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- globalization [.NET], calendars
- calendars, global applications
- global applications, calendars
- world-ready applications, calendars
- international applications [.NET], calendars
- culture, calendars
ms.assetid: 0c1534e5-979b-4c8a-a588-1c24301aefb3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dafa7cdaa38180e458a34fd34316f134aa443040
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929126"
---
# <a name="working-with-calendars"></a>달력 작업

날짜 및 시간 값은 시간에서 변하지 않는 어느 한 시점을 나타내지만 이에 대한 문자열 표현은 문화권에 따라 달라지며 특정 문화권에서 날짜 및 시간 값을 표시하는 데 사용되는 규칙과 해당 문화권에서 사용하는 달력에 따라 달라집니다. 이 항목에서는 .NET의 달력 지원에 대해 설명 하 고 날짜 값으로 작업할 때 달력 클래스를 사용 하는 방법을 설명 합니다.

## <a name="calendars-in-net"></a>.NET의 일정

.Net의 모든 달력은 기본 달력 <xref:System.Globalization.Calendar?displayProperty=nameWithType> 구현을 제공 하는 클래스에서 파생 됩니다. <xref:System.Globalization.Calendar> 클래스로부터 상속되는 클래스 중 하나는 모든 음력 달력의 기본 클래스인 <xref:System.Globalization.EastAsianLunisolarCalendar> 클래스입니다. .NET에는 다음과 같은 달력 구현이 포함 됩니다.

- <xref:System.Globalization.ChineseLunisolarCalendar>는 중국식 음력 달력을 나타냅니다.

- <xref:System.Globalization.GregorianCalendar>는 그레고리오력을 나타냅니다. 이 달력은 다시 <xref:System.Globalization.GregorianCalendarTypes?displayProperty=nameWithType> 열거형으로 정의되는 하위 유형으로 세분화됩니다(예: 아랍어 및 중동 프랑스어). <xref:System.Globalization.GregorianCalendar.CalendarType%2A?displayProperty=nameWithType> 속성은 그레고리오력 달력의 하위 유형을 지정합니다.

- <xref:System.Globalization.HebrewCalendar>는 히브리어 달력을 나타냅니다.

- <xref:System.Globalization.HijriCalendar>는 회교식 달력을 나타냅니다.

- <xref:System.Globalization.JapaneseCalendar>는 일본식 달력을 나타냅니다.

- <xref:System.Globalization.JapaneseLunisolarCalendar>는 일본식 음력 달력을 나타냅니다.

- <xref:System.Globalization.JulianCalendar>는 율리우스력을 나타냅니다.

- <xref:System.Globalization.KoreanCalendar>는 한국식 달력을 나타냅니다.

- <xref:System.Globalization.KoreanLunisolarCalendar>는 한국식 음력 달력을 나타냅니다.

- <xref:System.Globalization.PersianCalendar>는 페르시아력을 나타냅니다.

- <xref:System.Globalization.TaiwanCalendar>는 대만식 달력을 나타냅니다.

- <xref:System.Globalization.TaiwanLunisolarCalendar>는 대만식 음력 달력을 나타냅니다.

- <xref:System.Globalization.ThaiBuddhistCalendar>는 태국 불교식 달력을 나타냅니다.

- <xref:System.Globalization.UmAlQuraCalendar>는 사우디아라비아 회교식(Um Al Qura) 달력을 나타냅니다.

달력은 다음 두 가지 방법 중 하나로 사용할 수 있습니다.

- 특정 문화권에서 사용되는 달력. 각 <xref:System.Globalization.CultureInfo> 개체에는 해당 개체가 현재 사용 중인 달력인 현재 달력이 포함됩니다. 모든 날짜 및 시간 값에 대한 문자열 표현에는 자동으로 현재 문화권과 현재 달력이 반영됩니다. 일반적으로 현재 달력은 해당 문화권의 기본 달력입니다. <xref:System.Globalization.CultureInfo>개체에는 문화권에서 사용할 수 있는 추가 달력을 포함 하는 선택적 달력도 있습니다.

- 특정 문화권과 관계가 없는 독립 실행형 달력. 이 경우에는 달력을 반영한 값으로 날짜를 표시하기 위해 <xref:System.Globalization.Calendar> 메서드가 사용됩니다.

6개의 달력 클래스 <xref:System.Globalization.ChineseLunisolarCalendar>, <xref:System.Globalization.JapaneseLunisolarCalendar>, <xref:System.Globalization.JulianCalendar>, <xref:System.Globalization.KoreanLunisolarCalendar>, <xref:System.Globalization.PersianCalendar> 및 <xref:System.Globalization.TaiwanLunisolarCalendar>는 독립 실행형 달력으로만 사용할 수 있습니다. 이러한 달력은 어떤 문화권에서도 기본 달력이나 선택적인 달력으로 사용되지 않습니다.

## <a name="calendars-and-cultures"></a>달력 및 문화권

각 문화권에는 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType> 속성으로 정의되는 기본 달력이 포함됩니다. <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 속성은 특정 문화권의 기본 달력을 포함하여 해당 문화권에서 지원되는 모든 달력을 지정하는 <xref:System.Globalization.Calendar> 개체의 배열을 반환합니다.

다음 예제에서는 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 속성에 대해 설명합니다. 이 예제에서는 태국어(태국) 및 일본어(일본) 문화권에 대해 `CultureInfo` 개체를 만들고 기본 달력과 선택적인 달력을 표시합니다. 두 경우 모두 해당 문화권의 기본 달력이 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 컬렉션에도 포함됩니다.

[!code-csharp[Conceptual.Calendars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/calendarinfo1.cs#1)]
[!code-vb[Conceptual.Calendars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/calendarinfo1.vb#1)]

특정 <xref:System.Globalization.CultureInfo> 개체에서 현재 사용되는 달력은 해당 문화권의 <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=nameWithType> 속성에 의해 정의됩니다. 문화권의 <xref:System.Globalization.DateTimeFormatInfo> 개체는 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType> 속성에 의해 반환됩니다. 문화권을 만들 때 기본값은 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType> 속성의 값과 동일합니다. 하지만 문화권의 현재 달력을 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 속성으로 반환된 배열에 포함된 임의의 달력으로 변경할 수 있습니다. 현재 달력을 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 속성 값에 포함되지 않은 달력으로 설정하려고 하면 <xref:System.ArgumentException>이 throw됩니다.

다음 예제에서는 아랍어(사우디아라비아) 문화권에서 사용되는 달력을 변경합니다. 먼저 <xref:System.DateTime> 값을 인스턴스화하고 현재 문화권(이 경우에는 영어(미국))과 현재 문화권의 달력(그레고리오력)을 사용하여 표시합니다. 그런 다음 현재 문화권을 아랍어(사우디아라비아)로 변경하고 기본값인 우말쿠라 달력을 사용하여 날짜를 표시합니다. 그런 다음 `CalendarExists` 메서드를 호출하여 회교식 달력이 아랍어(사우디아라비아) 문화권에서 지원되는지 확인합니다. 이 달력이 지원되므로 현재 달력을 회교식 달력으로 변경하고 다시 날짜를 표시합니다. 각각의 경우에 날짜는 현재 문화권의 현재 달력을 사용하여 표시됩니다.

[!code-csharp[Conceptual.Calendars#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/changecalendar2.cs#2)]
[!code-vb[Conceptual.Calendars#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/changecalendar2.vb#2)]

## <a name="dates-and-calendars"></a>날짜 및 달력

<xref:System.Globalization.Calendar> 형식의 매개 변수를 포함하고 날짜 요소(즉, 월, 일 및 연도)가 지정된 달력의 값을 반영하도록 허용하는 생성자를 제외하면 <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 값 모두 항상 그레고리오력을 기반으로 합니다. 예를 들어 <xref:System.DateTime.Year%2A?displayProperty=nameWithType> 속성은 그레고리오력으로 연도를 반환하고 <xref:System.DateTime.Day%2A?displayProperty=nameWithType> 속성은 그레고리오력에서 특정 월의 일을 반환합니다.

> [!IMPORTANT]
> 날짜 값과 날짜 값의 문자열 표현은 서로 다르다는 점에 주의해야 합니다. 날짜 값은 그레고리오력을 기반으로 하지만 날짜 값의 표현은 특정 문화권의 현재 달력을 기반으로 합니다.

다음 예제에서는 <xref:System.DateTime> 속성과 이러한 속성의 해당 <xref:System.Globalization.Calendar> 메서드 간의 차이점을 보여 줍니다. 이 예제에서 문화권은 아랍어(이집트)이고 현재 달력은 우말쿠라입니다. <xref:System.DateTime> 값은 2011년의 7번째 월에서 15번째 일로 설정되어 있습니다. 변하지 않는 문화권의 규칙을 사용할 경우 동일한 값이 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 메서드로 반환되기 때문에 이 값은 그레고리오력 날짜로 해석되는 것이 분명합니다. 현재 문화권의 규칙을 사용하여 서식이 지정된 날짜의 문자열 표현은 우말쿠라 달력의 날짜와 동일한 14/08/32입니다. 그런 다음 `DateTime` 및 `Calendar`의 멤버를 사용하여 <xref:System.DateTime> 값의 일, 월 및 연도를 반환합니다. 각각의 경우에 <xref:System.DateTime> 멤버로 반환되는 값에는 그레고리오력의 값이 반영되지만 <xref:System.Globalization.UmAlQuraCalendar> 멤버로 반환되는 값에는 우말쿠라 달력의 값이 반영됩니다.

[!code-csharp[Conceptual.Calendars#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/datesandcalendars2.cs#3)]
[!code-vb[Conceptual.Calendars#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/datesandcalendars2.vb#3)]

### <a name="instantiating-dates-based-on-a-calendar"></a>달력을 기반으로 날짜 인스턴스화

<xref:System.DateTime> 및 <xref:System.DateTimeOffset> 값은 그레고리오력을 기반으로 하기 때문에 다른 달력에서 일, 월 또는 연도 값을 사용하려면 <xref:System.Globalization.Calendar> 형식의 매개 변수를 포함하는 오버로드된 생성자를 호출하여 날짜 값을 인스턴스화해야 합니다. 특정 달력의 <xref:System.Globalization.Calendar.ToDateTime%2A?displayProperty=nameWithType> 메서드의 오버로드 중 하나를 호출하여 특정 달력의 값을 기반으로 <xref:System.DateTime> 개체를 인스턴스화할 수도 있습니다.

다음 예제에서는 <xref:System.DateTime> 개체를 <xref:System.Globalization.HebrewCalendar> 생성자에 전달하여 하나의 <xref:System.DateTime> 값을 인스턴스화하고 <xref:System.DateTime> 메서드를 호출하여 두 번째 <xref:System.Globalization.HebrewCalendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType> 값을 인스턴스화합니다. 두 값은 히브리식 달력에서 동일한 값을 사용하여 만들어졌기 때문에 <xref:System.DateTime.Equals%2A?displayProperty=nameWithType> 메서드를 호출하면 두 <xref:System.DateTime> 값이 동일한 것으로 표시됩니다.

[!code-csharp[Conceptual.Calendars#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatehcdate1.cs#4)]
[!code-vb[Conceptual.Calendars#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatehcdate1.vb#4)]

### <a name="representing-dates-in-the-current-calendar"></a>현재 달력의 날짜 표시

날짜 및 시간 서식을 지정하는 메서드는 날짜를 문자열로 변환할 때 항상 현재 달력을 사용합니다. 즉, 연도, 월 및 월의 일에 대한 문자열 표현에는 현재 달력이 반영되며, 그레고리오력이 반드시 반영되지는 않습니다.

다음 예제에서는 현재 달력이 날짜의 문자열 표현에 어떤 영향을 주는지 보여 줍니다. 여기에서는 현재 문화권을 중국어(번체, 대만)로 변경하고 날짜 값을 인스턴스화합니다. 그런 다음 현재 달력과 날짜를 표시하고, 현재 달력을 <xref:System.Globalization.TaiwanCalendar>로 변경한 후 현재 달력 및 날짜를 다시 한 번 표시합니다. 날짜가 처음 표시될 때는 그레고리오력의 날짜로 표시됩니다. 두 번째 표시될 때는 대만 달력의 날짜로 표시됩니다.

[!code-csharp[Conceptual.Calendars#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/currentcalendar1.cs#5)]
[!code-vb[Conceptual.Calendars#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/currentcalendar1.vb#5)]

### <a name="representing-dates-in-a-non-current-calendar"></a>현재이 아닌 달력의 날짜 표시

특정 문화권의 현재 달력이 아닌 달력을 사용하여 날짜를 표시하려면 해당 <xref:System.Globalization.Calendar> 개체의 메서드를 호출해야 합니다. 예를 들어 <xref:System.Globalization.Calendar.GetYear%2A?displayProperty=nameWithType>, <xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=nameWithType> 메서드는 연도, 월 및 일을 특정 달력을 반영하는 값으로 변환합니다.

> [!WARNING]
> 일부 달력은 특정 문화권에서 선택적인 달력이 아니기 때문에 이러한 달력으로 날짜를 표시하려면 항상 달력 메서드를 호출해야 합니다. 이러한 제한은 <xref:System.Globalization.EastAsianLunisolarCalendar>, <xref:System.Globalization.JulianCalendar> 및 <xref:System.Globalization.PersianCalendar> 클래스에서 파생되는 모든 달력에 적용됩니다.

다음 예제에서는 <xref:System.Globalization.JulianCalendar> 개체를 사용하여 율리우스력의 1905년 1월 9일 날짜를 인스턴스화합니다. 이 날짜를 기본(그레고리오력) 달력을 사용하여 표시하면 1905년 1월 22일로 표시됩니다. 개별 <xref:System.Globalization.JulianCalendar> 메서드를 호출하면 날짜를 율리우스력으로 표시할 수 있습니다.

[!code-csharp[Conceptual.Calendars#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/noncurrentcalendar1.cs#6)]
[!code-vb[Conceptual.Calendars#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/noncurrentcalendar1.vb#6)]

### <a name="calendars-and-date-ranges"></a>달력 및 날짜 범위

달력에서 지원하는 가장 빠른 날짜는 그 달력의 <xref:System.Globalization.Calendar.MinSupportedDateTime%2A?displayProperty=nameWithType> 속성에 의해 표시됩니다. <xref:System.Globalization.GregorianCalendar> 클래스의 경우 그 날짜는 서기 0001년 1월 1일입니다. .NET의 다른 모든 달력은 이후 날짜를 지원 합니다. 달력에서 지원하는 가장 빠른 날짜에 앞서는 날짜 및 시간 값을 사용하려고 하면 <xref:System.ArgumentOutOfRangeException> 예외가 발생합니다.

그러나 한 가지 중요한 예외가 있습니다. <xref:System.DateTime> 개체와 <xref:System.DateTimeOffset> 개체의 (초기화되지 않은) 기본값은 <xref:System.Globalization.GregorianCalendar.MinSupportedDateTime%2A?displayProperty=nameWithType> 값과 같습니다. 서 기 0001 년 1 월 1 일을 지원 하지 않는 달력에서이 날짜의 형식을 지정 하려고 하는 경우 형식 지정자를 제공 하지 않습니다. 서식 지정 메서드는 "G" (일반 날짜/시간 패턴) 서식 지정자 대신 "s" (정렬 가능한 날짜/시간 패턴) 서식 지정자를 사용 합니다. 따라서 형식 지정 작업에서 <xref:System.ArgumentOutOfRangeException> 예외가 발생하지 않습니다. 대신, 지원되지 않는 날짜를 반환합니다. 이 점은 다음 예제에 설명되어 있습니다. 즉, 현재 문화권이 일본식 달력을 사용하는 일본어(일본)와 우말쿠라 달력을 사용하는 아랍어(이집트)로 설정되어 있을 때 <xref:System.DateTime.MinValue?displayProperty=nameWithType>의 값을 표시합니다. 현재 문화권을 영어(미국)로도 설정하고 이런 각각의 <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=nameWithType> 개체와 함께 <xref:System.Globalization.CultureInfo> 메서드를 호출합니다. 각각의 경우, 날짜는 정렬 가능한 날짜/시간 패턴을 사용하여 표시됩니다.

[!code-csharp[Conceptual.Calendars#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/minsupporteddatetime1.cs#11)]
[!code-vb[Conceptual.Calendars#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/minsupporteddatetime1.vb#11)]

## <a name="working-with-eras"></a>연대 작업

달력에서 날짜는 일반적으로 연대로 구분됩니다. 그러나 .net의 <xref:System.Globalization.Calendar> 클래스는 달력에 정의 된 모든 연대를 지원 하지 않으며 대부분 <xref:System.Globalization.Calendar> 의 클래스는 단일 연대만 지원 합니다. <xref:System.Globalization.JapaneseCalendar> 및 <xref:System.Globalization.JapaneseLunisolarCalendar> 클래스에서만 여러 연대가 지원됩니다.

> [!IMPORTANT]
> <xref:System.Globalization.JapaneseCalendar> 및<xref:System.Globalization.JapaneseLunisolarCalendar>의 새 연대 인 Reiwa 연대는 2019 년 5 월 1 일에 시작 됩니다. 이번 변경 내용은 달력을 사용하는 모든 애플리케이션에 영향을 줍니다. 자세한 내용은 다음 문서를 참조 하세요.
>
> - [.Net의 일본어 달력에서 새 연대를 처리](https://devblogs.microsoft.com/dotnet/handling-a-new-era-in-the-japanese-calendar-in-net/)하 고 여러 연대를 사용 하 여 달력을 지원 하 고 여러 연대 달력을 처리할 때 사용할 모범 사례를 설명 하는 .net에 추가 된 기능을 설명 합니다.
> - Windows에서 응용 프로그램을 테스트 하는 방법에 대 한 정보를 제공 하 여 era 변경에 대 한 준비를 하도록 [응용 프로그램을 준비](/windows/uwp/design/globalizing/japanese-era-change)합니다.
> - 새 일본어 달력 연대와 관련 된 개별 Windows 버전에 대 한 .NET Framework 업데이트를 나열 하는 [.NET Framework에 대 한 새 일본 Era 업데이트 요약](https://support.microsoft.com/help/4477957/new-japanese-era-updates-for-net-framework), multi-factor support에 대 한 새로운 .NET Framework 기능에 대 한 정보 및 다음 항목 포함 응용 프로그램 테스트에서를 찾습니다.

대부분의 달력에서 연대는 매우 긴 기간을 나타냅니다. 예를 들어 양력 달력에서 현재 연대는 세 개 이상의 millennia 범위에 포함 됩니다. <xref:System.Globalization.JapaneseCalendar> 및의경우여러연대를지원하는두개의<xref:System.Globalization.JapaneseLunisolarCalendar>달력은 그렇지 않습니다. 연대는 황제 reign의 기간에 해당 합니다. 여러 연대 지원. 특히 현재 연대의 상한 값을 알 수 없는 경우 특별 한 과제가 발생 합니다.

### <a name="eras-and-era-names"></a>연대 및 연대 이름

.Net에서 특정 달력 구현에서 지 원하는 연대를 나타내는 정수는 <xref:System.Globalization.Calendar.Eras%2A?displayProperty=nameWithType> 배열에서 역순으로 저장 됩니다. 현재 연대 (최신 시간 범위의 연대)는 인덱스 0에 있고 여러 연대를 지 원하는 클래스의 <xref:System.Globalization.Calendar> 경우 각 연속 인덱스는 이전 연대를 반영 합니다. 정적 <xref:System.Globalization.Calendar.CurrentEra?displayProperty=nameWithType> 속성은 <xref:System.Globalization.Calendar.Eras%2A?displayProperty=nameWithType> 배열에서 현재 연대의 인덱스를 정의하며 값이 항상 0인 상수입니다. 개별 <xref:System.Globalization.Calendar> 클래스에는 또한 현재 연대의 값을 반환하는 정적 필드가 포함됩니다. 이러한 필드는 다음 표에 나열되어 있습니다.

| 달력 클래스                                        | 현재 연대 필드                                                 |
| ----------------------------------------------------- | ----------------------------------------------------------------- |
| <xref:System.Globalization.ChineseLunisolarCalendar>  | <xref:System.Globalization.ChineseLunisolarCalendar.ChineseEra>   |
| <xref:System.Globalization.GregorianCalendar>         | <xref:System.Globalization.GregorianCalendar.ADEra>               |
| <xref:System.Globalization.HebrewCalendar>            | <xref:System.Globalization.HebrewCalendar.HebrewEra>              |
| <xref:System.Globalization.HijriCalendar>             | <xref:System.Globalization.HijriCalendar.HijriEra>                |
| <xref:System.Globalization.JapaneseLunisolarCalendar> | <xref:System.Globalization.JapaneseLunisolarCalendar.JapaneseEra> |
| <xref:System.Globalization.JulianCalendar>            | <xref:System.Globalization.JulianCalendar.JulianEra>              |
| <xref:System.Globalization.KoreanCalendar>            | <xref:System.Globalization.KoreanCalendar.KoreanEra>              |
| <xref:System.Globalization.KoreanLunisolarCalendar>   | <xref:System.Globalization.KoreanLunisolarCalendar.GregorianEra>  |
| <xref:System.Globalization.PersianCalendar>           | <xref:System.Globalization.PersianCalendar.PersianEra>            |
| <xref:System.Globalization.ThaiBuddhistCalendar>      | <xref:System.Globalization.ThaiBuddhistCalendar.ThaiBuddhistEra>  |
| <xref:System.Globalization.UmAlQuraCalendar>          | <xref:System.Globalization.UmAlQuraCalendar.UmAlQuraEra>          |

특정 연대 번호에 해당하는 이름은 연대 번호를 <xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=nameWithType> 또는 <xref:System.Globalization.DateTimeFormatInfo.GetAbbreviatedEraName%2A?displayProperty=nameWithType> 메서드에 전달하여 검색할 수 있습니다. 다음 예제에서는 이러한 메서드를 호출하여 <xref:System.Globalization.GregorianCalendar> 클래스에서 연대 지원에 대한 정보를 검색합니다. 현재 연대의 두 번째 연도의 1 월 1 일에 해당 하는 양력 날짜 뿐만 아니라 지원 되는 각 일본식 달력 연대의 두 번째 연도의 1 월 1 일에 해당 하는 양력 날짜를 표시 합니다.

[!code-csharp[Conceptual.Calendars#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatewithera1.cs)]
[!code-vb[Conceptual.Calendars#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatewithera1.vb)]

또한 "g" 사용자 지정 날짜 및 시간 서식 문자열에는 날짜 및 시간의 문자열 표현으로 달력의 연대 이름이 포함됩니다. 자세한 내용은 [사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)을 참조 하세요.

### <a name="instantiating-a-date-with-an-era"></a>연대를 사용 하 여 날짜 인스턴스화

여러 연대를 <xref:System.Globalization.Calendar> 지 원하는 두 클래스의 경우 특정 연도, 월 및 월 값의 일로 구성 된 날짜는 모호할 수 있습니다. 예를 들어에서 지 원하는 <xref:System.Globalization.JapaneseCalendar> 모든 연대에는 숫자가 1 인 연도가 있습니다. 일반적으로 연대가 지정되지 않으면 날짜 및 시간과 달력 메서드에서는 모두 값이 현재 연대에 속하는 것으로 가정합니다. 이는 형식의 매개 변수<xref:System.DateTime.%23ctor%2A>와<xref:System.DateTimeOffset.%23ctor%2A> JapaneseCalendar system.xml.xmlconvert.todatetime <xref:System.Globalization.Calendar>및[ JapaneseLunisolarCalendar 메서드를 포함하는 ](xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32))및[ 생성자에 적용됩니다.](xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)) 다음 예제에서는 지정 되지 않은 연대의 두 번째 연도의 1 월 1 일을 나타내는 날짜를 인스턴스화합니다. Reiwa era가 현재 연대 인 경우 예제를 실행 하는 경우 날짜는 Reiwa 연대의 두 번째 연도로 해석 됩니다. 令和는 <xref:System.DateTime.ToString(System.String,System.IFormatProvider)?displayProperty=nameWithType> 메서드에서 반환 된 문자열의 연도 앞에 오고 양력에서 1 월 1 일에 해당 하는 2020에 해당 합니다. (Reiwa 연대는 양력 년 2019 년에 시작 됩니다.)

[!code-csharp[A date in the current era](~/samples/snippets/standard/datetime/calendars/current-era/cs/program.cs)]
[!code-vb[A date in the current era](~/samples/snippets/standard/datetime/calendars/current-era/vb/program.vb)]

그러나 연대가 변경 되 면이 코드의 의도는 모호 합니다. 현재 연대의 두 번째 연도를 나타내는 날짜 이거나 서 연대의 두 번째 연도를 나타내기 위한 것 입니까? 이러한 모호성을 방지 하는 방법에는 두 가지가 있습니다.

- 기본 <xref:System.Globalization.GregorianCalendar> 클래스를 사용 하 여 날짜 및 시간 값을 인스턴스화합니다. 그러면 다음 예제와 같이 날짜의 문자열 표현에 일본어 달력 또는 일본어 음 양력을 사용할 수 있습니다.

  [!code-csharp[Insantiating a Gregorian date](~/samples/snippets/standard/datetime/calendars/gregorian/cs/program.cs)]
  [!code-vb[Instantiating a Gregorian date](~/samples/snippets/standard/datetime/calendars/gregorian/vb/program.vb)]

- 연대를 명시적으로 지정 하는 날짜 및 시간 메서드를 호출 합니다. 여기에는 다음 메서드가 포함됩니다.

  - <xref:System.Globalization.JapaneseCalendar> <xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)> 또는 클래스<xref:System.Globalization.JapaneseLunisolarCalendar> 의 메서드입니다.

  - <xref:System.DateTimeOffset> <xref:System.DateTime.Parse%2A> 구문분석할<xref:System.DateTime.TryParse%2A>문자열이 포함 된, <xref:System.Globalization.DateTimeStyles>,또는 와 같은 또는 구문 분석 메서드 (현재 문화권이 일본어-일본 (") 인 경우 선택적으로 인수) <xref:System.DateTime> <xref:System.DateTime.ParseExact%2A> <xref:System.DateTime.TryParseExact%2A> ja-jp ")이 고 해당 문화권의 일정은 <xref:System.Globalization.JapaneseCalendar>입니다. 구문 분석할 문자열은 연대를 포함 해야 합니다.

  - `provider` <xref:System.DateTimeOffset> 형식의 <xref:System.DateTime> 매개변수를포함하는또는<xref:System.IFormatProvider>구문 분석 메서드입니다. `provider`<xref:System.Globalization.CultureInfo> 는 현재 <xref:System.Globalization.JapaneseCalendar> <xref:System.Globalization.DateTimeFormatInfo.Calendar> 달력이<xref:System.Globalization.DateTimeFormatInfo> 인 일본-일본 ("ja-jp") 문화권을 나타내는 개체 이거나 속성이 인 개체 여야 합니다. <xref:System.Globalization.JapaneseCalendar> 구문 분석할 문자열은 연대를 포함 해야 합니다.

  다음 예제에서는 이러한 메서드 중 세 가지를 사용 하 여 1868 년 9 월 8 일에 시작 되 고 1912 년 7 월 29 일에 종료 된 Meiji 연대의 날짜 및 시간을 인스턴스화합니다.

  [!code-csharp[A date in a specified era](~/samples/snippets/standard/datetime/calendars/specify-era/cs/program.cs)]
  [!code-vb[A date in a specified era](~/samples/snippets/standard/datetime/calendars/specify-era/vb/program.vb)]

> [!TIP]
> 여러 연대를 지 원하는 달력으로 작업 하는 경우 *항상* 양력 날짜를 사용 하 여 날짜를 인스턴스화하거나 해당 달력을 기반으로 날짜와 시간을 인스턴스화할 때 연대를 지정 합니다.

<xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)> 메서드에 연대를 지정 하는 경우 <xref:System.Globalization.Calendar.Eras> 달력의 속성에 연대의 인덱스를 제공 합니다. 그러나 연대에 변경 내용이 적용 되는 달력의 경우 이러한 인덱스는 상수 값이 아닙니다. 현재 연대의 인덱스는 0이 고 가장 오래 된 연대는 인덱스 `Eras.Length - 1`에 있습니다. 새 연대를 달력에 추가 하면 이전 연대 인덱스는 1 씩 증가 합니다. 다음과 같이 적절 한 연대 인덱스를 제공할 수 있습니다.

- 현재 연대의 날짜의 경우 항상 달력의 <xref:System.Globalization.Calendar.CurrentEra> 속성을 사용 합니다.

- 지정 된 연대의 날짜에 대해 <xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=nameWithType> 메서드를 사용 하 여 지정 된 연대 이름에 해당 하는 인덱스를 검색 합니다. 이렇게 하려면가 <xref:System.Globalization.JapaneseCalendar> ja-jp 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체의 현재 달력 이어야 합니다.  이 기법은와 동일한 연대 <xref:System.Globalization.JapaneseLunisolarCalendar> <xref:System.Globalization.JapaneseCalendar>를 지원 하기 때문에 에서도 작동 합니다. 이전 예제에서는이 방법을 보여 줍니다.

### <a name="calendars-eras-and-date-ranges-relaxed-range-checks"></a>달력, 연대 및 날짜 범위: 완화 범위 검사

개별 달력과 매우 유사 하 게 날짜 범위가 지원 되며 및 <xref:System.Globalization.JapaneseCalendar> <xref:System.Globalization.JapaneseLunisolarCalendar> 클래스의 연대에도 지원 되는 범위가 있습니다. 이전에는 .NET에서 엄격한 연대 범위를 사용 하 여 연대 특정 날짜가 해당 연대의 범위 내에 있는지 확인 했습니다. 즉, 날짜가 지정 된 연대의 범위를 벗어나면 메서드는을 throw <xref:System.ArgumentOutOfRangeException>합니다. 현재 .NET에서는 기본적으로 완화 된 원거리 검사를 사용 합니다. 모든 버전의 .NET에 대 한 업데이트는 완화 된 연대 범위 검사를 도입 했습니다. 지정 된 연대의 범위를 벗어나는 연대 특정 날짜를 인스턴스화하 려는 시도는 다음 연대로 "오버플로" 되 고 예외가 throw 되지 않습니다.

다음 예제에서는 1926 년 12 월 25 일에 시작 되 고 1989 년 1 월 7 일에 종료 되는 Showa 연대의 65th 연도에서 날짜를 인스턴스화합니다. 이 날짜는의 Showa 연대 <xref:System.Globalization.JapaneseCalendar>범위를 벗어나는 1990 년 1 월 9 일에 해당 합니다. 예제의 출력에서 보여 주는 것 처럼 예제에서 표시 되는 날짜는 서 연대의 두 번째 연도의 1 월 9 일 1990입니다.

  [!code-csharp[Relaxed range checks](~/samples/snippets/standard/datetime/calendars/relaxed-range/cs/program.cs)]
  [!code-vb[Relaxed range checks](~/samples/snippets/standard/datetime/calendars/relaxed-range/vb/program.vb)]

완화 된 범위 검사가 바람직하지 않은 경우 응용 프로그램이 실행 되 고 있는 .NET 버전에 따라 여러 가지 방법으로 엄격한 범위 검사를 복원할 수 있습니다.

- **.NET Core:** 다음을. n e t *core.* c p.

  ```json
  "runtimeOptions": {
    "configProperties": {
        "Switch.System.Globalization.EnforceJapaneseEraYearRanges": true
    }
  }
  ```

- **.NET Framework 4.6 이상:** 다음 AppContext 스위치를 설정할 수 있습니다.

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.EnforceJapaneseEraYearRanges=true" />
    </runtime>
  </configuration>
  ```

- **.NET Framework 4.5.2 이전:** 다음 레지스트리 값을 설정할 수 있습니다.

   |  |  |
   |--|--|
   |Key | HKEY_LOCAL_MACHINE\Software\Microsoft\.NETFramework\AppContext |
   |이름 | Switch.System.Globalization.EnforceJapaneseEraYearRanges |
   |형식 | REG_SZ |
   |값 | true |

엄격한 범위 검사를 사용 하도록 설정 하면 이전 예제에서 <xref:System.ArgumentOutOfRangeException> 을 throw 하 고 다음과 같은 출력을 표시 합니다.

```console
Unhandled Exception: System.ArgumentOutOfRangeException: Valid values are between 1 and 64, inclusive.
Parameter name: year
   at System.Globalization.GregorianCalendarHelper.GetYearOffset(Int32 year, Int32 era, Boolean throwOnError)
   at System.Globalization.GregorianCalendarHelper.ToDateTime(Int32 year, Int32 month, Int32 day, Int32 hour, Int32 minute, Int32 second, Int32 millisecond, Int32 era)
   at Example.Main()
```

### <a name="representing-dates-in-calendars-with-multiple-eras"></a>여러 연대를 사용 하 여 달력의 날짜 표시

<xref:System.Globalization.Calendar> 개체가 연대를 지원하고 <xref:System.Globalization.CultureInfo> 개체의 현재 달력인 경우 전체 날짜 및 시간, 긴 날짜 및 간단한 날짜 패턴에 대한 날짜 및 시간 값의 문자열 표현에 연대가 포함됩니다. 다음 예제에서는 현재 문화권이 일본(일본어)이고 현재 달력이 일본식 달력일 때 이러한 날짜를 표시합니다.

[!code-csharp[Conceptual.Calendars#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings1.cs#8)]
[!code-vb[Conceptual.Calendars#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings1.vb#8)]

> [!WARNING]
> 클래스는 둘 이상의 연대에서 날짜를 지원 하 고, <xref:System.Globalization.CultureInfo> 개체의 현재 달력 일 수 있는 .net의 유일한 달력 클래스입니다 .이 클래스는 일본어 (일본) <xref:System.Globalization.CultureInfo> 문화권을 나타내는 개체입니다. <xref:System.Globalization.JapaneseCalendar>

모든 달력에서 "g" 사용자 지정 서식 지정자는 결과 문자열에 연대를 포함합니다. 다음 예제에서는 현재 달력이 그레고리오력일 때 "MM-dd-yyyy g" 사용자 지정 서식 문자열을 사용하여 결과 문자열에 연대를 포함합니다.

[!code-csharp[Conceptual.Calendars#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings2.cs#9)]
[!code-vb[Conceptual.Calendars#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings2.vb#9)]

날짜의 문자열 표현이 현재 달력이 아닌 달력으로 표현될 경우 <xref:System.Globalization.Calendar> 클래스에는 <xref:System.Globalization.Calendar.GetEra%2A?displayProperty=nameWithType>, <xref:System.Globalization.Calendar.GetYear%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=nameWithType> 메서드와 함께 사용할 수 있는 <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=nameWithType> 메서드가 포함되어 날짜가 속하는 연대뿐만 아니라 날짜 자체를 모호하게 표시합니다. 다음 예제에서는 <xref:System.Globalization.JapaneseLunisolarCalendar> 클래스를 사용하여 설명을 제공합니다. 하지만 결과 문자열에 연대에 대해 정수 대신 의미 있는 이름이나 약어를 포함하기 위해서는 <xref:System.Globalization.DateTimeFormatInfo> 개체를 인스턴스화하고 <xref:System.Globalization.JapaneseCalendar>를 현재 달력으로 지정해야 합니다. <xref:System.Globalization.JapaneseLunisolarCalendar> 달력은 특정 문화권의 현재 달력이 될 수 없지만 이 경우 두 달력이 동일한 연대를 공유합니다.

[!code-csharp[Conceptual.Calendars#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings3.cs#10)]
[!code-vb[Conceptual.Calendars#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings3.vb#10)]

일본 달력에서 연대의 첫 번째 연도를 Gannen (元年) 라고 합니다. 예를 들어 서 1 대신 서 연대의 첫 번째 연도를 서 Gannen로 설명할 수 있습니다. .Net에서는 다음 표준 또는 사용자 지정 날짜 및 시간 형식 문자열로 <xref:System.Globalization.CultureInfo> 형식이지정된날짜및시간에대한서식지정작업에서이규칙을사용합니다.<xref:System.Globalization.JapaneseCalendar> 클래스:

- "D" 표준 날짜 및 시간 형식 문자열로 표시 되는 [자세한 날짜 패턴](../base-types/standard-date-and-time-format-strings.md#LongDate)입니다.
- "F" 표준 날짜 및 시간 형식 문자열로 표시 되는 [전체 날짜의 자세한 시간 패턴](../base-types/standard-date-and-time-format-strings.md#FullDateLongTime)입니다.
- "F" 표준 날짜 및 시간 형식 문자열로 표시 되는 [전체 날짜 간단한 시간 패턴](../base-types/standard-date-and-time-format-strings.md#FullDateShortTime)입니다.
- Y "또는" y "표준 날짜 및 시간 형식 문자열로 표시 되는 [연도/월 패턴](../base-types/standard-date-and-time-format-strings.md#YearMonth)입니다.
- ["Ggy ' 年 '" 또는 "ggy年" [사용자 지정 날짜 및 시간 서식 문자열](../base-types/custom-date-and-time-format-strings.md)입니다.

예를 들어 다음 예에서는에서 <xref:System.Globalization.JapaneseCalendar> 서 연대의 첫 번째 연도의 날짜를 표시 합니다.

  [!code-csharp[gannen](~/samples/snippets/standard/datetime/calendars/gannen/cs/program.cs)]
  [!code-vb[gannen](~/samples/snippets/standard/datetime/calendars/gannen/vb/gannen-fmt.vb)]

서식 지정 작업에이 동작이 원치 않는 경우 .NET의 버전에 따라 다음 작업을 수행 하 여 "Gannen"가 아닌 연대의 첫 번째 연도를 항상 "1"로 나타내는 이전 동작을 복원할 수 있습니다.

- **.NET Core:** 다음을. n e t *core.* c p.

  ```json
  "runtimeOptions": {
    "configProperties": {
        "Switch.System.Globalization.FormatJapaneseFirstYearAsANumber": true
    }
  }
  ```

- **.NET Framework 4.6 이상:** 다음 AppContext 스위치를 설정할 수 있습니다.

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.FormatJapaneseFirstYearAsANumber=true" />
    </runtime>
  </configuration>
  ```

- **.NET Framework 4.5.2 이전:** 다음 레지스트리 값을 설정할 수 있습니다.

   |  |  |
   |--|--|
   |Key | HKEY_LOCAL_MACHINE\Software\Microsoft\.NETFramework\AppContext |
   |이름 | Switch.System.Globalization.FormatJapaneseFirstYearAsANumber |
   |형식 | REG_SZ |
   |값 | true |

서식 지정 작업에서 gannen 지원을 사용 하지 않도록 설정 하면 이전 예제에서 다음과 같은 출력을 표시 합니다.

```console
Japanese calendar date: 平成1年8月18日 (Gregorian: Friday, August 18, 1989)
```

날짜 및 시간 구문 분석 작업에서 "1" 또는 Gannen로 표시 된 연도가 포함 된 문자열을 지원 하도록 .NET도 업데이트 되었습니다. 이 작업을 수행할 필요는 없지만 이전 동작을 복원 하 여 연대의 첫 해에 "1"만 인식 하도록 할 수 있습니다. .NET의 버전에 따라 다음과 같이이 작업을 수행할 수 있습니다.

- **.NET Core:** 다음을. n e t *core.* c p.

  ```json
  "runtimeOptions": {
    "configProperties": {
        "Switch.System.Globalization.EnforceLegacyJapaneseDateParsing": true
    }
  }
  ```

- **.NET Framework 4.6 이상:** 다음 AppContext 스위치를 설정할 수 있습니다.

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.EnforceLegacyJapaneseDateParsing=true" />
    </runtime>
  </configuration>
  ```

- **.NET Framework 4.5.2 이전:** 다음 레지스트리 값을 설정할 수 있습니다.

   |  |  |
   |--|--|  
   |Key | HKEY_LOCAL_MACHINE\Software\Microsoft\.NETFramework\AppContext |
   |이름 | Switch.System.Globalization.EnforceLegacyJapaneseDateParsing |
   |형식 | REG_SZ |
   |값 | true | 

## <a name="see-also"></a>참고자료

- [방법: 그레고리오 력이 아닌 달력의 날짜 표시](../../../docs/standard/base-types/how-to-display-dates-in-non-gregorian-calendars.md)
- [샘플: 달력 주 범위 유틸리티](https://code.msdn.microsoft.com/NET-Framework-4-Calendar-3360a84a)
- [Calendar 클래스](xref:System.Globalization.Calendar)
