---
title: '방법: 그레고리오력이 아닌 달력으로 날짜 표시'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [.NET Framework], dates
- dates [.NET Framework], formatting
- calendars [.NET Framework], displaying dates
- displaying date and time data
ms.assetid: ed324eff-4aff-4a76-b6c0-04e6c0d8f5a9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cdd500d8eda81708d67254cbc5dc8da701ae4e09
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963349"
---
# <a name="how-to-display-dates-in-non-gregorian-calendars"></a>방법: 그레고리오력이 아닌 달력으로 날짜 표시
<xref:System.DateTime> 및 <xref:System.DateTimeOffset> 형식은 양력을 기본 달력으로 사용합니다. 즉, 날짜 및 시간 값의 `ToString` 메서드를 호출하면 해당 날짜 및 시간이 다른 달력을 사용하여 생성된 경우에도 해당 날짜 및 시간의 문자열 표현을 양력 달력으로 표시합니다. 이 내용은 두 가지 방법을 사용하여 페르시아력으로 날짜 및 시간 값을 만들지만 <xref:System.DateTime.ToString%2A> 메서드를 호출할 때 해당 날짜 및 시간 값을 여전히 양력으로 표시하는 다음 예제에 설명되어 있습니다. 이 예제에서는 특정 달력의 날짜를 표시하기 위해 자주 사용되지만 잘못된 두 가지 방법을 보여 줍니다.  
  
 [!code-csharp[Formatting.HowTo.Calendar#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Calendar/cs/Calendar1.cs#1)]
 [!code-vb[Formatting.HowTo.Calendar#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Calendar/vb/Calendar1.vb#1)]  
  
 두 가지 방법을 사용하여 특정 달력의 날짜를 표시할 수 있습니다. 첫 번째 방법에서는 달력이 특정 문화권의 기본 달력이어야 합니다. 두 번째 방법은 모든 달력에 사용할 수 있습니다.  
  
### <a name="to-display-the-date-for-a-cultures-default-calendar"></a>문화권의 기본 달력으로 날짜를 표시하려면  
  
1. 사용할 달력을 나타내는 <xref:System.Globalization.Calendar> 클래스에서 파생된 달력 개체를 인스턴스화합니다.  
  
2. 서식 지정을 사용하여 날짜를 표시할 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화합니다.  
  
3. <xref:System.Array.Exists%2A?displayProperty=nameWithType> 메서드를 호출하여 달력 개체가 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 속성에서 반환한 배열의 멤버인지 여부를 확인합니다. 이는 달력이 <xref:System.Globalization.CultureInfo> 개체의 기본 달력으로 사용될 수 있음을 나타냅니다. 배열의 멤버가 아닌 경우 "임의 달력의 날짜를 표시하려면" 섹션의 지침을 따르세요.  
  
4. <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType> 속성에서 반환한 <xref:System.Globalization.DateTimeFormatInfo> 개체의 <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A> 속성에 달력 개체를 할당합니다.  
  
    > [!NOTE]
    > <xref:System.Globalization.CultureInfo> 클래스에는 <xref:System.Globalization.CultureInfo.Calendar%2A> 속성도 있습니다. 그러나 이 클래스는 읽기 전용이며 상수이므로 <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=nameWithType> 속성에 할당된 새 기본 달력을 반영하도록 변경되지 않습니다.  
  
5. <xref:System.DateTime.ToString%2A> 또는 <xref:System.DateTime.ToString%2A> 메서드를 호출하여 이전 단계에서 기본 달력을 수정한 <xref:System.Globalization.CultureInfo> 개체를 전달합니다.  
  
### <a name="to-display-the-date-in-any-calendar"></a>임의 달력의 날짜를 표시하려면  
  
1. 사용할 달력을 나타내는 <xref:System.Globalization.Calendar> 클래스에서 파생된 달력 개체를 인스턴스화합니다.  
  
2. 날짜 및 시간 값의 문자열 표현에 표시할 날짜 및 시간 요소를 결정합니다.  
  
3. 표시할 각 날짜 및 시간 요소에 대해 달력 개체의 `Get` 메서드를 호출합니다. 메서드를 재정의합니다. 다음 메서드를 사용할 수 있습니다.  
  
    - <xref:System.Globalization.Calendar.GetYear%2A> - 해당 달력의 연도를 표시합니다.  
  
    - <xref:System.Globalization.Calendar.GetMonth%2A> - 해당 달력의 월을 표시합니다.  
  
    - <xref:System.Globalization.Calendar.GetDayOfMonth%2A> - 해당 달력의 일을 표시합니다.  
  
    - <xref:System.Globalization.Calendar.GetHour%2A> - 해당 달력의 시간을 표시합니다.  
  
    - <xref:System.Globalization.Calendar.GetMinute%2A> - 해당 달력의 분을 표시합니다.  
  
    - <xref:System.Globalization.Calendar.GetSecond%2A> - 해당 달력의 초를 표시합니다.  
  
    - <xref:System.Globalization.Calendar.GetMilliseconds%2A> - 해당 달력의 밀리초를 표시합니다.  
  
## <a name="example"></a>예  
 예제에서는 두 가지 달력을 사용하여 날짜를 표시합니다. 회교식 달력을 ar-JO 문화권의 기본 달력으로 정의한 후 날짜를 표시하고, fa-IR 문화권에서 선택적 달력으로 지원되지 않는 페르시아력을 사용하여 날짜를 표시합니다.  
  
 [!code-csharp[Formatting.HowTo.Calendar#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Calendar/cs/Calendar1.cs#2)]
 [!code-vb[Formatting.HowTo.Calendar#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Calendar/vb/Calendar1.vb#2)]  
  
 각 <xref:System.Globalization.CultureInfo> 개체는 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A> 속성에 표시된 하나 이상의 달력을 지원할 수 있습니다. 이러한 달력 중 하나가 문화권의 기본 달력으로 지정되며 읽기 전용 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType> 속성에 의해 반환됩니다. <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType> 속성에서 반환한 <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=nameWithType> 속성에 해당 달력을 나타내는 <xref:System.Globalization.Calendar> 개체를 할당하여 다른 선택적 달력을 기본값으로 지정할 수 있습니다. 그러나 <xref:System.Globalization.PersianCalendar> 클래스가 나타내는 페르시아력과 같은 일부 달력은 특정 문화권의 선택적 달력으로 사용되지 않습니다.  
  
 예제에서는 다시 사용할 수 있는 달력 유틸리티 클래스인 `CalendarUtility`를 정의하여 날짜의 문자열 표현을 특정 달력으로 생성하는 작업의 많은 세부 정보를 처리합니다. `CalendarUtility` 클래스의 멤버는 다음과 같습니다.  
  
- 하나의 매개 변수가 날짜를 나타내는 <xref:System.Globalization.Calendar> 개체를 매개 변수로 사용하는 생성자 - 클래스의 전용 필드에 할당됩니다.  
  
- `CalendarExists` - `CalendarUtility` 개체가 나타내는 달력이 메서드에 매개 변수로 전달되는 <xref:System.Globalization.CultureInfo> 개체에서 지원되는지 여부를 나타내는 부울 값을 반환하는 전용 메서드입니다. 이 메서드는 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 배열을 전달할 대상인 <xref:System.Array.Exists%2A?displayProperty=nameWithType> 메서드에 대한 호출을 래핑합니다.  
  
- `HasSameName` - <xref:System.Array.Exists%2A?displayProperty=nameWithType> 메서드에 매개 변수로 전달되는 <xref:System.Predicate%601> 대리자에 할당된 전용 메서드입니다. 메서드에서 `true`가 반환될 때까지 배열의 각 멤버가 메서드에 전달됩니다. 이 메서드는 선택적 달력의 이름이 `CalendarUtility` 개체가 나타내는 달력과 같은지 여부를 확인합니다.  
  
- `DisplayDate` - 두 매개 변수 즉, `CalendarUtility` 개체가 나타내는 달력에 표시할 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 값 및 서식 지정 규칙을 사용할 문화권이 전달되는 오버로드된 공용 메서드입니다. 날짜의 문자열 표현을 반환할 때의 해당 동작은 대상 달력이 사용할 형식 지정 규칙의 문화권에서 지원되는지 여부에 따라 달라집니다.  
  
 이 예제에서 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 값을 만드는 데 사용된 달력과 관계없이 해당 값은 일반적으로 양력 날짜로 표시됩니다. 이는 <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 형식이 달력 정보를 유지하지 않기 때문입니다. 내부적으로 두 값은 0001년 1월 1일 자정 이후에 경과된 틱 수로 표시됩니다. 해당 숫자의 해석은 달력에 따라 달라집니다. 대부분의 문화권에서 기본 달력은 양력입니다.  
  
## <a name="see-also"></a>참고 항목

- [서식 지정 작업 수행](../../../docs/standard/base-types/performing-formatting-operations.md)
