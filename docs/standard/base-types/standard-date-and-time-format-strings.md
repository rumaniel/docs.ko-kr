---
title: 표준 날짜 및 시간 형식 문자열
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [.NET Framework], dates
- custom DateTime format string
- format specifiers, custom date and time
- format strings
- custom date and time format strings
- formatting [.NET Framework], time
- date and time strings
ms.assetid: bb79761a-ca08-44ee-b142-b06b3e2fc22b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4ca6109a61fb32cd148e69081da0772277743b6e
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48873734"
---
# <a name="standard-date-and-time-format-strings"></a>표준 날짜 및 시간 형식 문자열
표준 날짜 및 시간 서식 문자열은 단일 서식 지정자를 사용하여 날짜 및 시간 값의 텍스트 표현을 정의합니다. 공백을 포함하여 문자가 두 개 이상 포함된 날짜 및 시간 서식 문자열은 사용자 지정 날짜 및 시간 서식 문자열로 해석됩니다. 자세한 내용은 [사용자 지정 날짜 및 시간 서식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)을 참조하세요. 표준 또는 사용자 지정 서식 문자열은 다음 두 가지 방법으로 사용할 수 있습니다.  
  
-   서식 지정 작업의 결과로 생성되는 문자열을 정의합니다.  
  
-   구문 분석 작업을 통해 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 값으로 변환할 수 있는 날짜 및 시간 값의 텍스트 표현을 정의합니다.  

> [!TIP]
>  서식 문자열을 숫자 또는 날짜 및 시간 값에 적용할 수 있도록 지원하고 결과 문자열을 표시하는 응용 프로그램인 [서식 유틸리티](https://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)를 다운로드할 수 있습니다.  

표준 날짜 및 시간 서식 문자열은 <xref:System.DateTime>과 <xref:System.DateTimeOffset> 값 모두에 사용할 수 있습니다.  
  
[!INCLUDE[C# interactive-note](~/includes/csharp-interactive-with-utc-partial-note.md)] 

<a name="table"></a> 다음 표에서는 표준 날짜 및 시간 서식 지정자에 대해 설명합니다. 다른 설명이 없는 한 특정 표준 날짜 및 시간 서식 지정자는 <xref:System.DateTime> 값에 사용할 때와 <xref:System.DateTimeOffset> 값에 사용할 때 동일한 문자열을 생성합니다. 표준 날짜 및 시간 서식 문자열을 사용하는 방법에 대한 자세한 내용은 [참고](#Notes) 섹션을 참조하세요.  
  
|형식 지정자|설명|예제|  
|----------------------|-----------------|--------------|  
|"d"|간단한 날짜 패턴입니다.<br /><br /> 추가 정보: [간단한 날짜("d") 서식 지정자](#ShortDate)|2009-06-15T13:45:30 -> 6/15/2009 (en-US)<br /><br /> 2009-06-15T13:45:30 -> 15/06/2009 (fr-FR)<br /><br /> 2009-06-15T13:45:30 -> 2009/06/15 (ja-JP)|  
|"D"|자세한 날짜 패턴입니다.<br /><br /> 추가 정보: [자세한 날짜("D") 서식 지정자](#LongDate)|2009-06-15T13:45:30 -> Monday, June 15, 2009 (en-US)<br /><br /> 2009-06-15T13:45:30 -> 15 июня 2009 г. (ru-RU)<br /><br /> 2009-06-15T13:45:30 -> Montag, 15. Juni 2009 (de-DE)|  
|"f"|전체 날짜/시간 패턴(간단한 시간)입니다.<br /><br /> 추가 정보: [전체 날짜, 간단한 시간("f") 서식 지정자](#FullDateShortTime)|2009-06-15T13:45:30 -> Monday, June 15, 2009 1:45 PM (en-US)<br /><br /> 2009-06-15T13:45:30 -> den 15 juni 2009 13:45 (sv-SE)<br /><br /> 2009-06-15T13:45:30 -> Δευτέρα, 15 Ιουνίου 2009 1:45 μμ (el-GR)|  
|"F"|전체 날짜/시간 패턴(자세한 시간)<br /><br /> 추가 정보: [전체 날짜 자세한 시간("F") 서식 지정자](#FullDateLongTime)|2009-06-15T13:45:30 -> Monday, June 15, 2009 1:45:30 PM (en-US)<br /><br /> 2009-06-15T13:45:30 -> den 15 juni 2009 13:45:30 (sv-SE)<br /><br /> 2009-06-15T13:45:30 -> Δευτέρα, 15 Ιουνίου 2009 1:45:30 μμ (el-GR)|  
|"g"|일반 날짜/시간 패턴(간단한 시간)<br /><br /> 추가 정보: [일반 날짜 간단한 시간("g") 서식 지정자](#GeneralDateShortTime)|2009-06-15T13:45:30 -> 6/15/2009 1:45 PM (en-US)<br /><br /> 2009-06-15T13:45:30 -> 15/06/2009 13:45 (es-ES)<br /><br /> 2009-06-15T13:45:30 -> 2009/6/15 13:45 (zh-CN)|  
|"G"|일반 날짜/시간 패턴(자세한 시간)입니다.<br /><br /> 추가 정보: [일반 날짜, 자세한 시간("G") 서식 지정자](#GeneralDateLongTime)|2009-06-15T13:45:30 -> 6/15/2009 1:45:30 PM (en-US)<br /><br /> 2009-06-15T13:45:30 -> 15/06/2009 13:45:30 (es-ES)<br /><br /> 2009-06-15T13:45:30 -> 2009/6/15 13:45:30 (zh-CN)|  
|"M", "m"|월/일 패턴입니다.<br /><br /> 추가 정보: [월("M", "m") 서식 지정자](#MonthDay)|2009-06-15T13:45:30 -> June 15 (en-US)<br /><br /> 2009-06-15T13:45:30 -> 15. juni (da-DK)<br /><br /> 2009-06-15T13:45:30 -> 15 Juni (id-ID)|  
|"O", "o"|라운드트립 날짜/시간 패턴입니다.<br /><br /> 추가 정보: [라운드트립("O", "o") 서식 지정자](#Roundtrip)|<xref:System.DateTime> 값:<br /><br /> 2009-06-15T13:45:30 (DateTimeKind.Local) --> 2009-06-15T13:45:30.0000000-07:00<br /><br /> 2009-06-15T13:45:30 (DateTimeKind.Utc) --> 2009-06-15T13:45:30.0000000Z<br /><br /> 2009-06-15T13:45:30 (DateTimeKind.Unspecified) --> 2009-06-15T13:45:30.0000000<br /><br /> <xref:System.DateTimeOffset> 값:<br /><br /> 2009-06-15T13:45:30-07:00 --> 2009-06-15T13:45:30.0000000-07:00|  
|"R", "r"|RFC1123 패턴입니다.<br /><br /> 추가 정보: [RFC1123("R", "r") 서식 지정자](#RFC1123)|2009-06-15T13:45:30 -> Mon, 15 Jun 2009 20:45:30 GMT|  
|"s"|정렬 가능한 날짜/시간 패턴입니다.<br /><br /> 추가 정보: [정렬 가능한("s") 서식 지정자](#Sortable)|2009-06-15T13:45:30 (DateTimeKind.Local) -> 2009-06-15T13:45:30<br /><br /> 2009-06-15T13:45:30 (DateTimeKind.Utc) -> 2009-06-15T13:45:30|  
|"t"|간단한 시간 패턴입니다.<br /><br /> 추가 정보: [간단한 시간("t") 서식 지정자](#ShortTime)|2009-06-15T13:45:30 -> 1:45 PM (en-US)<br /><br /> 2009-06-15T13:45:30 -> 13:45 (hr-HR)<br /><br /> 2009-06-15T13:45:30 -> 01:45 م (ar-EG)|  
|"T"|자세한 시간 패턴<br /><br /> 추가 정보: [자세한 시간("T") 서식 지정자](#LongTime)|2009-06-15T13:45:30 -> 1:45:30 PM (en-US)<br /><br /> 2009-06-15T13:45:30 -> 13:45:30 (hr-HR)<br /><br /> 2009-06-15T13:45:30 -> 01:45:30 م (ar-EG)|  
|"u"|정렬 가능한 유니버설 날짜/시간 패턴<br /><br /> 추가 정보: [정렬 가능한 유니버설("u") 서식 지정자](#UniversalSortable)|<xref:System.DateTime> 값 사용: 2009-06-15T13:45:30 -> 2009-06-15 13:45:30Z<br /><br /> <xref:System.DateTimeOffset> 값 사용: 2009-06-15T13:45:30 -> 2009-06-15 20:45:30Z|  
|"U"|유니버설 전체 날짜/시간 패턴입니다.<br /><br /> 추가 정보: [유니버설 전체("U") 서식 지정자](#UniversalFull)|2009-06-15T13:45:30 -> Monday, June 15, 2009 8:45:30 PM (en-US)<br /><br /> 2009-06-15T13:45:30 -> den 15 juni 2009 20:45:30 (sv-SE)<br /><br /> 2009-06-15T13:45:30 -> Δευτέρα, 15 Ιουνίου 2009 8:45:30 μμ (el-GR)|  
|"Y", "y"|연도 월 패턴<br /><br /> 추가 정보: [연도 월("Y") 서식 지정자](#YearMonth)|2009-06-15T13:45:30 -> June, 2009 (en-US)<br /><br /> 2009-06-15T13:45:30 -> juni 2009 (da-DK)<br /><br /> 2009-06-15T13:45:30 -> Juni 2009 (id-ID)|  
|기타 모든 단일 문자|알 수 없는 지정자입니다.|런타임 <xref:System.FormatException>을 throw합니다.|  
  
## <a name="how-standard-format-strings-work"></a>표준 서식 문자열의 작동 방법  
 서식 지정 작업에서 표준 서식 문자열은 단순히 사용자 지정 서식 문자열에 대한 별칭입니다. 별칭을 사용하여 사용자 지정 서식 문자열을 참조할 경우 별칭은 변하지 않지만 사용자 지정 서식 문자열 자체는 변경될 수 있다는 장점이 있습니다. 이는 날짜 및 시간 값에 대한 문자열 표현이 일반적으로 문화권마다 다르다는 점을 감안했을 때 매우 중요한 기능입니다. 예를 들어, "d" 표준 서식 문자열은 날짜 및 시간 값을 간단한 날짜 패턴을 사용하여 표시함을 나타냅니다. 고정 문화권의 경우 이 패턴이 "MM/dd/yyyy"이고 fr-FR 문화권의 경우 "dd/MM/yyyy"이며 ja-JP 문화권의 경우 "yyyy/MM/dd"입니다.  
  
 서식 지정 작업에서 표준 서식 문자열이 특정 문화권의 사용자 지정 서식 문자열에 매핑되는 경우 응용 프로그램에서는 다음 방법 중 하나로 사용할 사용자 지정 서식 문자열이 포함된 특정 문화권을 정의할 수 있습니다.  
  
-   기본 또는 현재 문화권을 사용할 수 있습니다. 다음 예제에서는 현재 문화권의 간단한 날짜 서식을 사용하여 날짜를 표시합니다. 이 예제의 경우 현재 문화권이 en-US입니다.  
  
     [!code-csharp-interactive[System.DateTime.Conceptual.Formatting#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/cs/StandardFormats1.cs#1)]
     [!code-vb[System.DateTime.Conceptual.Formatting#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/vb/StandardFormats1.vb#1)]  
  
-   사용할 서식 지정과 관련된 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체를 <xref:System.IFormatProvider> 매개 변수가 있는 메서드에 전달할 수 있습니다. 다음 예제에서는 pt-BR 문화권의 간단한 날짜 서식을 사용하여 날짜를 표시합니다.  
  
     [!code-csharp[System.DateTime.Conceptual.Formatting#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/cs/StandardFormats1.cs#2)]
     [!code-vb[System.DateTime.Conceptual.Formatting#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/vb/StandardFormats1.vb#2)]  
  
-   서식 지정 정보를 제공하는 <xref:System.Globalization.DateTimeFormatInfo> 개체를 <xref:System.IFormatProvider> 매개 변수가 있는 메서드에 전달할 수 있습니다. 다음 예제에서는 hr-HR 문화권의 <xref:System.Globalization.DateTimeFormatInfo> 개체가 제공하는 간단한 날짜 서식을 사용하여 날짜를 표시합니다.  
  
     [!code-csharp[System.DateTime.Conceptual.Formatting#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/cs/StandardFormats1.cs#3)]
     [!code-vb[System.DateTime.Conceptual.Formatting#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/vb/StandardFormats1.vb#3)]  
  
> [!NOTE]
>  날짜와 시간 값 서식 지정에 사용되는 패턴 또는 문자열에 대한 자세한 내용은 <xref:System.Globalization.NumberFormatInfo> 클래스 항목을 참조하세요.  
  
 표준 서식 문자열을 보다 긴 고정 사용자 지정 서식 문자열에 대한 약식 표현으로 사용하는 경우도 있습니다. 표준 서식 문자열은 "O"(또는 "o"), "R"(또는 "r"), "s" 및 "u"라는 네 범주로 나뉩니다. 이 문자열은 고정 문화권에 정의된 사용자 지정 서식 문자열에 대응되며, 문화권마다 동일하게 인식되는 날짜 및 시간 값에 대한 문자열 표현을 생성합니다. 다음 표에서는 이러한 네 가지 표준 날짜 및 시간 서식 문자열에 대해 설명합니다.  
  
|표준 서식 문자열|DateTimeFormatInfo.InvariantInfo 속성으로 정의된 문자열|사용자 지정 서식 문자열|  
|----------------------------|----------------------------------------------------------|--------------------------|  
|"O" 또는 "o"|없음|yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffzz|  
|"R" 또는 "r"|<xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern%2A>|ddd, dd MMM yyyy HH':'mm':'ss 'GMT'|  
|"s"|<xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern%2A>|yyyy'-'MM'-'dd'T'HH':'mm':'ss|  
|"u"|<xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern%2A>|yyyy'-'MM'-'dd HH':'mm':'ss'Z'|  
  
 표준 서식 문자열은 입력 문자열이 특정 패턴을 정확하게 따라야 구문 분석 작업이 성공하는 <xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.ParseExact%2A?displayProperty=nameWithType> 메서드의 구문 분석 작업에서도 사용할 수 있습니다. 많은 표준 서식 문자열은 여러 사용자 지정 서식 문자열로 매핑되므로 날짜 및 시간 값을 여러 서식으로 표현할 수 있으며 그래도 구문 분석 작업이 성공합니다. <xref:System.Globalization.DateTimeFormatInfo.GetAllDateTimePatterns%28System.Char%29?displayProperty=nameWithType> 메서드를 호출하면 표준 서식 문자열에 해당하는 사용자 지정 서식 문자열을 확인할 수 있습니다. 다음 예제에서는 "d"(간단한 날짜 패턴) 표준 서식 문자열로 매핑되는 사용자 지정 서식 문자열을 보여 줍니다.  
  
 [!code-csharp-interactive[Formatting.DateAndTime.Standard#17](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/stdandparsing1.cs#17)]
 [!code-vb[Formatting.DateAndTime.Standard#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/stdandparsing1.vb#17)]  
  
 다음 단원에서는 <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 값에 대한 표준 서식 지정자에 대해 설명합니다.  
  
<a name="ShortDate"></a>   
## <a name="the-short-date-d-format-specifier"></a>간단한 날짜("d") 서식 지정자  
 "d" 표준 서식 지정자는 특정 문화권의 <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 예를 들어, 고정 문화권의 <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A> 속성이 반환하는 사용자 지정 서식 문자열은 "MM/dd/yyyy"입니다.  
  
 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체의 속성을 보여 줍니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A>|결과 문자열의 전체 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A>|날짜의 연도, 월 및 일 구성 요소를 구분하는 문자열을 정의합니다.|  
  
 다음 예제에서는 "d" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#1)]
 [!code-vb[Formatting.DateAndTime.Standard#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#1)]  
  
 [표로 이동](#table)  
  
<a name="LongDate"></a>   
## <a name="the-long-date-d-format-specifier"></a>자세한 날짜("D") 서식 지정자  
 "D" 표준 서식 지정자는 현재 <xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 예를 들어, 고정 문화권에 대한 사용자 지정 서식 문자열은 "dddd, dd MMMM yyyy"입니다.  
  
 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체의 속성을 보여 줍니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A>|결과 문자열의 전체 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|결과 문자열에 나타날 수 있는 지역화된 요일 이름을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|결과 문자열에 나타날 수 있는 지역화된 월 이름을 정의합니다.|  
  
 다음 예제에서는 "D" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#2)]
 [!code-vb[Formatting.DateAndTime.Standard#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#2)]  
  
 [표로 이동](#table)  
  
<a name="FullDateShortTime"></a>   
## <a name="the-full-date-short-time-f-format-specifier"></a>전체 날짜, 간단한 시간("f") 서식 지정자  
 "f" 표준 서식 지정자는 공백으로 구분된 자세한 날짜("D")와 간단한 시간("t") 패턴의 조합입니다.  
  
 결과 문자열은 특정 <xref:System.Globalization.DateTimeFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체 속성을 보여 줍니다. 일부 문화권의 <xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=nameWithType> 속성에서 반환하는 사용자 지정 서식 지정자는 일부 속성을 사용하지 못할 수 있습니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A>|결과 문자열의 날짜 구성 요소 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A>|결과 문자열의 시간 구성 요소 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|결과 문자열에 나타날 수 있는 지역화된 요일 이름을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|결과 문자열에 나타날 수 있는 지역화된 월 이름을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|시간의 시, 분 및 초 구성 요소를 구분하는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|12시간 서식으로 자정부터 정오까지의 시간을 나타내는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|12시간 서식으로 정오부터 자정까지의 시간을 나타내는 문자열을 정의합니다.|  
  
 다음 예제에서는 "f" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#3)]
 [!code-vb[Formatting.DateAndTime.Standard#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#3)]  
  
 [표로 이동](#table)  
  
<a name="FullDateLongTime"></a>   
## <a name="the-full-date-long-time-f-format-specifier"></a>전체 날짜, 자세한 시간("F") 서식 지정자  
 "F" 표준 서식 지정자는 현재 <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 예를 들어, 고정 문화권에 대한 사용자 지정 서식 문자열은 "dddd, dd MMMM yyyy HH:mm:ss"입니다.  
  
 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체 속성을 보여 줍니다. 일부 문화권의 <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A> 속성에서 반환하는 사용자 지정 서식 지정자는 일부 속성을 사용하지 못할 수 있습니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A>|결과 문자열의 전체 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|결과 문자열에 나타날 수 있는 지역화된 요일 이름을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|결과 문자열에 나타날 수 있는 지역화된 월 이름을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|시간의 시, 분 및 초 구성 요소를 구분하는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|12시간 서식으로 자정부터 정오까지의 시간을 나타내는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|12시간 서식으로 정오부터 자정까지의 시간을 나타내는 문자열을 정의합니다.|  
  
 다음 예제에서는 "F" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#4)]
 [!code-vb[Formatting.DateAndTime.Standard#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#4)]  
  
 [표로 이동](#table)  
  
<a name="GeneralDateShortTime"></a>   
## <a name="the-general-date-short-time-g-format-specifier"></a>일반 날짜, 간단한 시간("g") 서식 지정자  
 "g" 표준 서식 지정자는 공백으로 구분된 간단한 날짜("d")와 간단한 시간("t") 패턴의 조합입니다.  
  
 결과 문자열은 특정 <xref:System.Globalization.DateTimeFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체 속성을 보여 줍니다. 일부 문화권의 <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=nameWithType> 속성에서 반환하는 사용자 지정 서식 지정자는 일부 속성을 사용하지 못할 수 있습니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A>|결과 문자열의 날짜 구성 요소 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A>|결과 문자열의 시간 구성 요소 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A>|날짜의 연도, 월 및 일 구성 요소를 구분하는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|시간의 시, 분 및 초 구성 요소를 구분하는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|12시간 서식으로 자정부터 정오까지의 시간을 나타내는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|12시간 서식으로 정오부터 자정까지의 시간을 나타내는 문자열을 정의합니다.|  
  
 다음 예제에서는 "g" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Standard#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#5)]  
  
 [표로 이동](#table)  
  
<a name="GeneralDateLongTime"></a>   
## <a name="the-general-date-long-time-g-format-specifier"></a>일반 날짜, 자세한 시간("G") 서식 지정자  
 "G" 표준 서식 지정자는 공백으로 구분된 간단한 날짜("d")와 자세한 시간("T") 패턴의 조합입니다.  
  
 결과 문자열은 특정 <xref:System.Globalization.DateTimeFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체 속성을 보여 줍니다. 일부 문화권의 <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A?displayProperty=nameWithType> 속성에서 반환하는 사용자 지정 서식 지정자는 일부 속성을 사용하지 못할 수 있습니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A>|결과 문자열의 날짜 구성 요소 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A>|결과 문자열의 시간 구성 요소 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A>|날짜의 연도, 월 및 일 구성 요소를 구분하는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|시간의 시, 분 및 초 구성 요소를 구분하는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|12시간 서식으로 자정부터 정오까지의 시간을 나타내는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|12시간 서식으로 정오부터 자정까지의 시간을 나타내는 문자열을 정의합니다.|  
  
 다음 예제에서는 "G" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#6)]
 [!code-vb[Formatting.DateAndTime.Standard#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#6)]  
  
 [표로 이동](#table)  
  
<a name="MonthDay"></a>   
## <a name="the-month-m-m-format-specifier"></a>월("M", "m") 서식 지정자  
 "M" 또는 "m" 표준 서식 지정자는 현재 <xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 예를 들어, 고정 문화권에 대한 사용자 지정 서식 문자열은 "MMMM dd"입니다.  
  
 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체의 속성을 보여 줍니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern%2A>|결과 문자열의 전체 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|결과 문자열에 나타날 수 있는 지역화된 월 이름을 정의합니다.|  
  
 다음 예제에서는 "m" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Standard#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#7)]  
  
 [표로 이동](#table)  
  
<a name="Roundtrip"></a>   
## <a name="the-round-trip-o-o-format-specifier"></a>라운드트립("O", "o") 서식 지정자  
 "O" 또는 "o" 표준 서식 지정자는 표준 시간대 정보를 유지하는 패턴을 사용하여 사용자 지정 날짜 및 시간 서식 문자열을 나타내고 ISO 8601을 준수하는 결과 문자열을 생략합니다. <xref:System.DateTime> 값의 경우 이 서식 지정자는 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성과 함께 날짜 및 시간 값을 텍스트로 유지합니다. 서식이 지정된 문자열은 <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> 매개 변수가 <xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType>로 설정된 경우 `styles` 또는 <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> 메서드를 사용하여 다시 구문 분석할 수 있습니다.  
  
 "O" 또는 "o" 표준 서식 지정자는 <xref:System.DateTime> 값에 대한 "yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffK" 사용자 지정 서식 문자열과 <xref:System.DateTimeOffset> 값에 대한 "yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffzzz" 사용자 지정 문자열에 해당합니다. 이 문자열에서 하이픈, 콜론, 문자 "T" 등의 개별 문자를 구분하는 작은따옴표 쌍은 변경할 수 없는 리터럴입니다. 아포스트로피는 출력 문자열에 표시되지 않습니다.  
  
 “O” 또는 “o” 표준 형식 지정자(및 “yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffK” 사용자 지정 형식 문자열)는 ISO 8601에서 <xref:System.DateTime> 값의 <xref:System.DateTime.Kind%2A> 속성을 유지하기 위해 표준 시간대 정보를 나타내는 세 가지 방법을 이용합니다.  
  
-   <xref:System.DateTimeKind.Local?displayProperty=nameWithType> 날짜 및 시간 값의 표준 시간대 구성 요소는 UTC의 오프셋입니다(예: +01:00, -07:00). 모든 <xref:System.DateTimeOffset> 값은 이 형식으로도 표현됩니다.  
  
-   <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> 날짜 및 시간 값의 표준 시간대 구성 요소는 "Z"(0 오프셋을 의미함)를 사용하여 UTC를 나타냅니다.  
  
-   <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> 날짜 및 시간 값은 표준 시간대 정보를 포함하지 않습니다.  
  
 "O" 또는 "o" 표준 서식 지정자는 국제 표준을 준수하므로, 이 지정자를 사용하는 서식 지정 또는 구문 분석 작업에서는 항상 고정 문화권 및 양력을 사용합니다.  
  
 `Parse` 및 `TryParse`의 `ParseExact`, `TryParseExact`, <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 메서드에 전달되는 문자열은 이러한 형식 중 하나인 경우 "O" 또는 "o" 서식 지정자를 사용하여 구문 분석할 수 있습니다. <xref:System.DateTime> 개체의 경우 호출하는 구문 분석 오버로드는 값이 `styles`인 <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType> 매개 변수도 포함해야 합니다. "O" 또는 "o" 서식 지정자에 해당하는 사용자 지정 서식 문자열로 구문 분석 메서드를 호출하는 경우 "O" 또는 "o"와 동일한 결과를 얻지 못합니다. 사용자 지정 서식 문자열을 사용하는 구문 분석 메서드는 표준 시간대 구성 요소가 없거나 "Z"를 사용하여 UTC를 나타내는 날짜 및 시간 값의 문자열 표현을 구문 분석할 수 없기 때문입니다.  
  
 다음 예제에서는 "o" 서식 지정자를 사용하여 미국 태평양 표준 시간대에 있는 시스템의 일련의 <xref:System.DateTime> 값 및 <xref:System.DateTimeOffset> 값을 표시합니다.  
  
 [!code-csharp-interactive[Formatting.DateAndTime.Standard#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/o1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Standard#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/o1.vb#8)]  
  
 다음 예제에서는 "o" 서식 지정자를 사용하여 서식이 지정된 문자열을 만든 다음 날짜 및 시간 `Parse` 메서드를 호출하여 원래 날짜 및 시간 값을 복원합니다.  
  
 [!code-csharp[Formatting.DateandTime.Standard#16](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Roundtrip1.cs#16)]
 [!code-vb[Formatting.DateandTime.Standard#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/RoundTrip1.vb#16)]  
  
 [표로 이동](#table)  
  
<a name="RFC1123"></a>   
## <a name="the-rfc1123-r-r-format-specifier"></a>RFC1123("R", "r") 서식 지정자  
 "R" 또는 "r" 표준 서식 지정자는 <xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 이 패턴은 정의된 표준을 반영하며 해당 속성은 읽기 전용입니다. 따라서 이 패턴은 사용된 문화권이나 제공된 서식 공급자에 관계없이 항상 같습니다. 사용자 지정 서식 문자열은 "ddd, dd MMM yyyy HH':'mm':'ss 'GMT'"입니다. 이 표준 서식 지정자를 사용할 경우 서식 지정 또는 구문 분석 작업에서 항상 고정 문화권이 사용됩니다.  
  
 결과 문자열은 고정 문화권을 나타내는 <xref:System.Globalization.DateTimeFormatInfo> 속성에서 반환하는 다음과 같은 <xref:System.Globalization.DateTimeFormatInfo.InvariantInfo%2A?displayProperty=nameWithType> 개체 속성의 영향을 받습니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern%2A>|결과 문자열의 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames%2A>|결과 문자열에 나타날 수 있는 약식 요일 이름을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.AbbreviatedMonthNames%2A>|결과 문자열에 나타날 수 있는 약식 월 이름을 정의합니다.|  
  
 RFC 1123 표준에 따라 시간이 UTC(Coordinated Universal Time)로 표시되지만 서식 지정 작업 중에 <xref:System.DateTime> 또는 개체의 값이 수정되지 않습니다. 따라서 서식 지정 작업을 수행하기 전에 <xref:System.DateTime> 메서드를 호출하여 <xref:System.DateTime.ToUniversalTime%2A?displayProperty=nameWithType> 값을 UTC로 변환해야 합니다. 반면에 <xref:System.DateTimeOffset> 값은 이 변환을 자동으로 수행하므로, 서식 지정 작업 전에 <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> 메서드를 호출할 필요가 없습니다.  
  
 다음 예제에서는 "r" 서식 지정자를 사용하여 미국 태평양 표준 시간대에 있는 시스템의 <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 값을 표시합니다.  
  
 [!code-csharp-interactive[Formatting.DateAndTime.Standard#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#9)]
 [!code-vb[Formatting.DateAndTime.Standard#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#9)]  
  
 [표로 이동](#table)  
  
<a name="Sortable"></a>   
## <a name="the-sortable-s-format-specifier"></a>정렬 가능한("s") 서식 지정자  
 "s" 표준 서식 지정자는 <xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 이 패턴은 정의된 표준(ISO 8601)을 반영하며 해당 속성은 읽기 전용입니다. 따라서 이 패턴은 사용된 문화권이나 제공된 서식 공급자에 관계없이 항상 같습니다. 사용자 지정 서식 문자열은 "yyyy'-'MM'-'dd'T'HH':'mm':'ss"입니다.  
  
 "s" 형식 지정자는 날짜 및 시간 값에 따라 오름차순 또는 내림차순으로 일관되게 정렬되는 결과 문자열을 생성하기 위한 것입니다. 따라서, "s" 표준 형식 지정자는 날짜 및 시간 값을 일관된 형식으로 나타내지만 형식 지정 작업에서 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성이나 해당 <xref:System.DateTimeOffset.Offset%2A?displayProperty=nameWithType> 값을 반영하도록 형식이 지정되는 날짜 및 시간 개체의 값을 수정하지는 않습니다. 예를 들어 날짜 및 시간 값 2014-11-15T18:32:17+00:00 및 2014-11-15T18:32:17+08:00의 형식을 지정하여 생성된 결과 문자열은 같습니다.  
  
 이 표준 서식 지정자를 사용할 경우 서식 지정 또는 구문 분석 작업에서 항상 고정 문화권이 사용됩니다.  
  
 다음 예제에서는 "s" 서식 지정자를 사용하여 미국 태평양 표준 시간대에 있는 시스템의 <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 값을 표시합니다.  
  
 [!code-csharp-interactive[Formatting.DateAndTime.Standard#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#10)]
 [!code-vb[Formatting.DateAndTime.Standard#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#10)]  
  
 [표로 이동](#table)  
  
<a name="ShortTime"></a>   
## <a name="the-short-time-t-format-specifier"></a>간단한 시간("t") 서식 지정자  
 "t" 표준 서식 지정자는 현재 <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 예를 들어, 고정 문화권에 대한 사용자 지정 서식 문자열은 "HH:mm"입니다.  
  
 결과 문자열은 특정 <xref:System.Globalization.DateTimeFormatInfo> 개체의 서식 지정 정보에 영향을 받습니다. 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체 속성을 보여 줍니다. 일부 문화권의 <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=nameWithType> 속성에서 반환하는 사용자 지정 서식 지정자는 일부 속성을 사용하지 못할 수 있습니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A>|결과 문자열의 시간 구성 요소 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|시간의 시, 분 및 초 구성 요소를 구분하는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|12시간 서식으로 자정부터 정오까지의 시간을 나타내는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|12시간 서식으로 정오부터 자정까지의 시간을 나타내는 문자열을 정의합니다.|  
  
 다음 예제에서는 "t" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#11)]
 [!code-vb[Formatting.DateAndTime.Standard#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#11)]  
  
 [표로 이동](#table)  
  
<a name="LongTime"></a>   
## <a name="the-long-time-t-format-specifier"></a>자세한 시간("T") 서식 지정자  
 "T" 표준 서식 지정자는 특정 문화권의 <xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 예를 들어, 고정 문화권에 대한 사용자 지정 서식 문자열은 "HH:mm:ss"입니다.  
  
 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체 속성을 보여 줍니다. 일부 문화권의 <xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A?displayProperty=nameWithType> 속성에서 반환하는 사용자 지정 서식 지정자는 일부 속성을 사용하지 못할 수 있습니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A>|결과 문자열의 시간 구성 요소 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|시간의 시, 분 및 초 구성 요소를 구분하는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|12시간 서식으로 자정부터 정오까지의 시간을 나타내는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|12시간 서식으로 정오부터 자정까지의 시간을 나타내는 문자열을 정의합니다.|  
  
 다음 예제에서는 "T" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#12)]
 [!code-vb[Formatting.DateAndTime.Standard#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#12)]  
  
 [표로 이동](#table)  
  
<a name="UniversalSortable"></a>   
## <a name="the-universal-sortable-u-format-specifier"></a>정렬 가능한 유니버설("u") 서식 지정자  
 "u" 표준 서식 지정자는 <xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 이 패턴은 정의된 표준을 반영하며 해당 속성은 읽기 전용입니다. 따라서 이 패턴은 사용된 문화권이나 제공된 서식 공급자에 관계없이 항상 같습니다. 사용자 지정 서식 문자열은 "yyyy'-'MM'-'dd HH':'mm':'ss'Z"입니다. 이 표준 서식 지정자를 사용할 경우 서식 지정 또는 구문 분석 작업에서 항상 고정 문화권이 사용됩니다.  
  
 결과 문자열에 시간이 UTC(Coordinated Universal Time)로 표시되어야 하지만 서식 지정 작업 중에 원래 <xref:System.DateTime> 값의 변환이 전혀 수행되지 않습니다. 따라서 서식 지정하기 전에 <xref:System.DateTime> 메서드를 호출하여 <xref:System.DateTime.ToUniversalTime%2A?displayProperty=nameWithType> 값을 UTC로 변환해야 합니다.  반면에 <xref:System.DateTimeOffset> 값은 이 변환을 자동으로 수행하므로, 서식 지정 작업 전에 <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> 메서드를 호출할 필요가 없습니다.  
  
 다음 예제에서는 "u" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp-interactive[Formatting.DateAndTime.Standard#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Standard#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#13)]  
  
 [표로 이동](#table)  
  
<a name="UniversalFull"></a>   
## <a name="the-universal-full-u-format-specifier"></a>유니버설 전체("U") 서식 지정자  
 "U" 표준 서식 지정자는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 이 패턴은 "F" 패턴과 동일합니다. 그러나 서식 지정 작업을 수행하기 전에 <xref:System.DateTime> 값이 자동으로 UTC로 변환됩니다.  
  
 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체 속성을 보여 줍니다. 일부 문화권의 <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A> 속성에서 반환하는 사용자 지정 서식 지정자는 일부 속성을 사용하지 못할 수 있습니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A>|결과 문자열의 전체 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|결과 문자열에 나타날 수 있는 지역화된 요일 이름을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|결과 문자열에 나타날 수 있는 지역화된 월 이름을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|시간의 시, 분 및 초 구성 요소를 구분하는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|12시간 서식으로 자정부터 정오까지의 시간을 나타내는 문자열을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|12시간 서식으로 정오부터 자정까지의 시간을 나타내는 문자열을 정의합니다.|  
  
 "U" 서식 지정자는 <xref:System.DateTimeOffset> 형식에는 지원되지 않으므로 "U" 서식 지정자를 사용하여 <xref:System.FormatException> 값의 서식을 지정하려고 하면 <xref:System.DateTimeOffset>이 throw됩니다.  
  
 다음 예제에서는 "U" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#14)]
 [!code-vb[Formatting.DateAndTime.Standard#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#14)]  
  
 [표로 이동](#table)  
  
<a name="YearMonth"></a>   
## <a name="the-year-month-y-y-format-specifier"></a>년 월("Y", "y") 서식 지정자  
 "Y" 또는 "y" 표준 서식 지정자는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern%2A?displayProperty=nameWithType> 속성에 의해 정의되는 사용자 지정 날짜 및 시간 서식 문자열을 나타냅니다. 예를 들어, 고정 문화권에 대한 사용자 지정 서식 문자열은 "yyyy MMMM"입니다.  
  
 다음 표에서는 반환된 문자열의 서식을 제어하는 <xref:System.Globalization.DateTimeFormatInfo> 개체의 속성을 보여 줍니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern%2A>|결과 문자열의 전체 서식을 정의합니다.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|결과 문자열에 나타날 수 있는 지역화된 월 이름을 정의합니다.|  
  
 다음 예제에서는 "y" 서식 지정자를 사용하여 날짜 및 시간 값을 표시합니다.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#15](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#15)]
 [!code-vb[Formatting.DateAndTime.Standard#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#15)]  
  
 [표로 이동](#table)  
  
<a name="Notes"></a>   
## <a name="notes"></a>노트  
  
### <a name="control-panel-settings"></a>제어판 설정  
 제어판에 있는 **국가 및 언어 옵션** 항목의 설정은 서식 지정 작업으로 생성되는 결과 문자열에 영향을 줍니다. 이러한 설정은 형식을 제어하는 데 사용되는 값을 제공하는 현재 스레드 문화권과 연결된 <xref:System.Globalization.DateTimeFormatInfo> 개체를 초기화하는 데 사용됩니다. 다른 설정을 사용하는 컴퓨터는 다른 결과 문자열을 생성합니다.  
  
 또한 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%29?displayProperty=nameWithType> 생성자를 사용하여 현재 시스템 문화권과 동일한 문화권을 나타내는 새 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화하는 경우 제어판의 **국가 및 언어 옵션** 항목을 통해 설정된 사용자 지정 내용이 새 <xref:System.Globalization.CultureInfo> 개체에도 적용됩니다. <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 생성자를 사용하면 시스템의 사용자 지정 내용이 반영되지 않는 <xref:System.Globalization.CultureInfo> 개체를 만들 수 있습니다.  
  
### <a name="datetimeformatinfo-properties"></a>DateTimeFormatInfo 속성  
 형식은 현재 스레드 문화권에 의해 암시적으로 제공되거나 형식 지정 작업을 호출하는 메서드의 <xref:System.Globalization.DateTimeFormatInfo> 매개 변수에 의해 명시적으로 제공되는 현재 <xref:System.IFormatProvider> 개체의 속성에 따라 영향을 받습니다. <xref:System.IFormatProvider> 매개 변수에 대해 응용 프로그램에서는 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체를 지정하거나 특정 문화권의 날짜 및 시간 서식 지정 규칙을 나타내는 <xref:System.Globalization.DateTimeFormatInfo> 개체를 지정해야 합니다. 대부분의 표준 날짜 및 시간 서식 지정자는 현재 <xref:System.Globalization.DateTimeFormatInfo> 개체의 속성으로 정의된 서식 지정 패턴의 별칭입니다. 따라서 응용 프로그램에서는 해당 <xref:System.Globalization.DateTimeFormatInfo> 속성의 날짜 및 시간 서식 패턴을 변경하여 일부 표준 날짜 및 시간 서식 지정자로 생성되는 결과를 변경할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.DateTime?displayProperty=nameWithType>  
- <xref:System.DateTimeOffset?displayProperty=nameWithType>  
- [형식 서식 지정](../../../docs/standard/base-types/formatting-types.md)  
- [사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)  
- [샘플: .NET Framework 4 서식 유틸리티](https://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)
