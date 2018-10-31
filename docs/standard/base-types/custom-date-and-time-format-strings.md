---
title: 사용자 지정 날짜 및 시간 형식 문자열
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
ms.assetid: 98b374e3-0cc2-4c78-ab44-efb671d71984
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f51e3f36594a6f66c5fad32214d84a11b78726a4
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48582881"
---
# <a name="custom-date-and-time-format-strings"></a>사용자 지정 날짜 및 시간 형식 문자열

날짜 및 시간 형식 문자열은 형식 지정 작업에서 생성되는 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 값의 텍스트 표현을 정의합니다. 또한 문자열을 날짜 및 시간으로 성공적으로 변환하기 위해 구문 분석 작업에 필요한 날짜 및 시간 값의 표현을 정의할 수 있습니다. 사용자 지정 형식 문자열은 하나 이상의 사용자 지정 날짜 및 시간 형식 지정자로 구성됩니다. [표준 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)이 아닌 문자열은 사용자 지정 날짜 및 시간 형식 문자열로 해석됩니다.

> [!TIP]
> 서식 문자열을 숫자 또는 날짜 및 시간 값에 적용할 수 있도록 지원하고 결과 문자열을 표시하는 응용 프로그램인 [서식 유틸리티](https://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)를 다운로드할 수 있습니다.

 사용자 지정 날짜 및 시간 형식 문자열은 <xref:System.DateTime>과 <xref:System.DateTimeOffset> 값 모두에 사용할 수 있습니다.

[!INCLUDE[C# interactive-note](~/includes/csharp-interactive-with-utc-partial-note.md)] 

<a name="table"></a> 형식 작업에서 사용자 지정 날짜 및 시간 형식 문자열은 날짜 및 시간 인스턴스의 `ToString` 메서드 또는 복합 형식을 지원하는 메서드에서 사용할 수 있습니다. 다음 예제에서는 두 가지 사용 방법을 모두 보여 줍니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#17](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/custandformatting1.cs#17)]
 [!code-vb[Formatting.DateAndTime.Custom#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/custandformatting1.vb#17)]

 구문 분석 작업에서 사용자 지정 날짜 및 시간 형식 문자열은 <xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType>, <xref:System.DateTime.TryParseExact%2A?displayProperty=nameWithType>, <xref:System.DateTimeOffset.ParseExact%2A?displayProperty=nameWithType> 및 <xref:System.DateTimeOffset.TryParseExact%2A?displayProperty=nameWithType> 메서드에서 사용할 수 있습니다. 이러한 메서드를 사용하려면 구문 분석 작업을 성공하기 위해 입력 문자열이 특정 패턴을 정확하게 따라야 합니다. 다음 예제에서는 <xref:System.DateTimeOffset.ParseExact%28System.String%2CSystem.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 메서드를 호출하여 일, 월 및 두 자릿수 연도를 포함해야 하는 날짜를 구문 분석하는 방법을 보여 줍니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#18](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/custandparsing1.cs#18)]
 [!code-vb[Formatting.DateAndTime.Custom#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/custandparsing1.vb#18)]

 다음 표에서는 사용자 지정 날짜 및 시간 형식 지정자 및 각 형식 지정자에 따라 생성되는 결과 문자열을 보여 줍니다. 기본적으로 결과 문자열은 en-US 문화권의 형식 규칙을 반영합니다. 특정 형식 지정자가 지역화된 결과 문자열을 생성하는 경우 결과 문자열에 적용되는 문화권의 예도 보여 줍니다. 사용자 지정 날짜 및 시간 형식 문자열을 사용하는 방법에 대한 자세한 내용은 참고 단원을 참조하세요.

| 형식 지정자 | 설명 | 예제 |
| ---------------------- | ----------------- | -------------- |
|"d"|1부터 31까지의 일(월 기준)입니다.<br /><br /> 추가 정보: ["d" 사용자 지정 형식 지정자](#dSpecifier)|2009-06-01T13:45:30 -> 1<br /><br /> 2009-06-15T13:45:30 -> 15|
|"dd"|01부터 31까지의 일(월 기준)입니다.<br /><br /> 추가 정보: ["dd" 사용자 지정 형식 지정자](#ddSpecifier)|2009-06-01T13:45:30 -> 01<br /><br /> 2009-06-15T13:45:30 -> 15|
|"ddd"|요일의 약식 이름입니다.<br /><br /> 추가 정보: ["ddd" 사용자 지정 형식 지정자](#dddSpecifier)|2009-06-15T13:45:30 -> Mon (en-US)<br /><br /> 2009-06-15T13:45:30 -> Пн (ru-RU)<br /><br /> 2009-06-15T13:45:30 -> lun. (fr-FR)|
|"dddd"|요일의 전체 이름입니다.<br /><br /> 추가 정보: ["dddd" 사용자 지정 형식 지정자](#ddddSpecifier)|2009-06-15T13:45:30 -> Monday (en-US)<br /><br /> 2009-06-15T13:45:30 -> понедельник (ru-RU)<br /><br /> 2009-06-15T13:45:30 -> lundi (fr-FR)|
|"f"|날짜 및 시간 값에서 1/10초입니다.<br /><br /> 추가 정보: ["F" 사용자 지정 형식 지정자](#fSpecifier)|2009-06-15T13:45:30.6170000 -> 6<br /><br /> 2009-06-15T13:45:30.05 -> 0|
|"ff"|날짜 및 시간 값의 1/100초입니다.<br /><br /> 추가 정보: ["FF" 사용자 지정 형식 지정자](#ffSpecifier)|2009-06-15T13:45:30.6170000 -> 61<br /><br /> 2009-06-15T13:45:30.0050000 -> 00|
|"fff"|날짜 및 시간 값의 1/1000초입니다.<br /><br /> 추가 정보: ["FFF" 사용자 지정 형식 지정자](#fffSpecifier)|6/15/2009 13:45:30.617 -> 617<br /><br /> 6/15/2009 13:45:30.0005 -> 000|
|"ffff"|날짜 및 시간 값의 1/10000초입니다.<br /><br /> 추가 정보: ["FFFF" 사용자 지정 형식 지정자](#ffffSpecifier)|2009-06-15T13:45:30.6175000 -> 6175<br /><br /> 2009-06-15T13:45:30.0000500  -> 0000|
|"fffff"|날짜 및 시간 값의 1/100000초입니다.<br /><br /> 추가 정보: ["FFFFF" 사용자 지정 형식 지정자](#fffffSpecifier)|2009-06-15T13:45:30.6175400 -> 61754<br /><br /> 6/15/2009 13:45:30.000005 -> 00000|
|"ffffff"|날짜 및 시간 값의 1/1000000초입니다.<br /><br /> 추가 정보: ["FFFFFF" 사용자 지정 형식 지정자](#ffffffSpecifier)|2009-06-15T13:45:30.6175420 -> 617542<br /><br /> 2009-06-15T13:45:30.0000005 -> 000000|
|"fffffff"|날짜 및 시간 값의 1/10000000초입니다.<br /><br /> 추가 정보: ["FFFFFFF" 사용자 지정 형식 지정자](#fffffffSpecifier)|2009-06-15T13:45:30.6175425 -> 6175425<br /><br /> 2009-06-15T13:45:30.0001150 -> 0001150|
|"F"|0이 아닌 경우 날짜 및 시간 값의 1/10초입니다.<br /><br /> 추가 정보: ["F" 사용자 지정 형식 지정자](#F_Specifier)|2009-06-15T13:45:30.6170000 -> 6<br /><br /> 2009-06-15T13:45:30.0500000 -> (출력 없음)|
|"FF"|0이 아닌 경우 날짜 및 시간 값의 1/100초입니다.<br /><br /> 추가 정보: ["FF" 사용자 지정 형식 지정자](#FF_Specifier)|2009-06-15T13:45:30.6170000 -> 61<br /><br /> 2009-06-15T13:45:30.0050000 -> (출력 없음)|
|"FFF"|0이 아닌 경우 날짜 및 시간 값의 1/1000초입니다.<br /><br /> 추가 정보: ["FFF" 사용자 지정 형식 지정자](#FFF_Specifier)|2009-06-15T13:45:30.6170000 -> 617<br /><br /> 2009-06-15T13:45:30.0005000 -> (출력 없음)|
|"FFFF"|0이 아닌 경우 날짜 및 시간 값의 1/10000초입니다.<br /><br /> 추가 정보: ["FFFF" 사용자 지정 형식 지정자](#FFFF_Specifier)|2009-06-15T13:45:30.5275000 -> 5275<br /><br /> 2009-06-15T13:45:30.0000500 -> (출력 없음)|
|"FFFFF"|0이 아닌 경우 날짜 및 시간 값의 1/100000초입니다.<br /><br /> 추가 정보: ["FFFFF" 사용자 지정 형식 지정자](#FFFFF_Specifier)|2009-06-15T13:45:30.6175400 -> 61754<br /><br /> 2009-06-15T13:45:30.0000050 -> (출력 없음)|
|"FFFFFF"|0이 아닌 경우 날짜 및 시간 값의 1/1000000초입니다.<br /><br /> 추가 정보: ["FFFFFF" 사용자 지정 형식 지정자](#FFFFFF_Specifier)|2009-06-15T13:45:30.6175420 -> 617542<br /><br /> 2009-06-15T13:45:30.0000005 -> (출력 없음)|
|"FFFFFFF"|0이 아닌 경우 날짜 및 시간 값의 1/10000000초입니다.<br /><br /> 추가 정보: ["FFFFFFF" 사용자 지정 형식 지정자](#FFFFFFF_Specifier)|2009-06-15T13:45:30.6175425 -> 6175425<br /><br /> 2009-06-15T13:45:30.0001150 -> 000115|
|"g", "gg"|서기 또는 연대입니다.<br /><br /> 추가 정보: ["g" 또는 "gg" 사용자 지정 형식 지정자](#gSpecifier)|2009-06-15T13:45:30.6170000 -> A.D.|
|"h"|12시간 형식을 사용하는 1부터 12까지의 시간입니다.<br /><br /> 추가 정보: ["H" 사용자 지정 형식 지정자](#hSpecifier)|2009-06-15T01:45:30 -> 1<br /><br /> 2009-06-15T13:45:30 -> 1|
|"hh"|12시간 형식을 사용하는 01부터 12까지의 시간입니다.<br /><br /> 추가 정보: ["HH" 사용자 지정 형식 지정자](#hhSpecifier)|2009-06-15T01:45:30 -> 01<br /><br /> 2009-06-15T13:45:30 -> 01|
|"H"|24시간 형식을 사용하는 0부터 23까지의 시간입니다.<br /><br /> 추가 정보: ["H" 사용자 지정 형식 지정자](#H_Specifier)|2009-06-15T01:45:30 -> 1<br /><br /> 2009-06-15T13:45:30 -> 13|
|"HH"|24시간 형식을 사용하는 00부터 23까지의 시간입니다.<br /><br /> 추가 정보: ["HH" 사용자 지정 형식 지정자](#HH_Specifier)|2009-06-15T01:45:30 -> 01<br /><br /> 2009-06-15T13:45:30 -> 13|
|"K"|표준 시간대 정보입니다.<br /><br /> 추가 정보: ["K" 사용자 지정 형식 지정자](#KSpecifier)|<xref:System.DateTime> 값과 함께 사용하는 경우<br /><br /> 2009-06-15T13:45:30, Kind Unspecified -><br /><br /> 2009-06-15T13:45:30, Kind Utc -> Z<br /><br /> 2009-06-15T13:45:30, Kind Local -> -07:00(로컬 컴퓨터 설정에 따라 달라짐)<br /><br /> <xref:System.DateTimeOffset> 값과 함께 사용하는 경우<br /><br /> 2009-06-15T01:45:30-07:00 --> -07:00<br /><br /> 2009-06-15T08:45:30+00:00 --> +00:00|
|"m"|0부터 59까지의 분입니다.<br /><br /> 추가 정보: ["m" 사용자 지정 형식 지정자](#mSpecifier)|2009-06-15T01:09:30 -> 9<br /><br /> 2009-06-15T13:29:30 -> 29|
|"mm"|00부터 59까지의 분입니다.<br /><br /> 추가 정보: ["MM" 사용자 지정 형식 지정자](#mmSpecifier)|2009-06-15T01:09:30 -> 09<br /><br /> 2009-06-15T01:45:30 -> 45|
|"M"|1부터 12까지의 월입니다.<br /><br /> 추가 정보: ["m" 사용자 지정 형식 지정자](#M_Specifier)|2009-06-15T13:45:30 -> 6|
|"MM"|01부터 12까지의 월입니다.<br /><br /> 추가 정보: ["MM" 사용자 지정 형식 지정자](#MM_Specifier)|2009-06-15T13:45:30 -> 06|
|"MMM"|월의 약식 이름입니다.<br /><br /> 추가 정보: ["MMM" 사용자 지정 형식 지정자](#MMM_Specifier)|2009-06-15T13:45:30 -> Jun (en-US)<br /><br /> 2009-06-15T13:45:30 -> juin (fr-FR)<br /><br /> 2009-06-15T13:45:30 -> Jun (zu-ZA)|
|"MMMM"|월의 전체 이름입니다.<br /><br /> 추가 정보: ["MMMM" 사용자 지정 형식 지정자](#MMMM_Specifier)|2009-06-15T13:45:30 -> June (en-US)<br /><br /> 2009-06-15T13:45:30 -> juni (da-DK)<br /><br /> 2009-06-15T13:45:30 -> uJuni (zu-ZA)|
|"s"|0부터 59까지의 초입니다.<br /><br /> 추가 정보: ["s" 사용자 지정 형식 지정자](#sSpecifier)|2009-06-15T13:45:09 -> 9|
|"ss"|00부터 59까지의 초입니다.<br /><br /> 추가 정보: ["ss" 사용자 지정 형식 지정자](#ssSpecifier)|2009-06-15T13:45:09 -> 09|
|"t"|AM/PM 지정자의 첫 문자입니다.<br /><br /> 추가 정보: ["t" 사용자 지정 형식 지정자](#tSpecifier)|2009-06-15T13:45:30 -> P (en-US)<br /><br /> 2009-06-15T13:45:30 -> 午 (ja-JP)<br /><br /> 2009-06-15T13:45:30 ->  (fr-FR)|
|"tt"|AM/PM 지정자입니다.<br /><br /> 추가 정보: ["tt" 사용자 지정 형식 지정자](#ttSpecifier)|2009-06-15T13:45:30 -> PM (en-US)<br /><br /> 2009-06-15T13:45:30 -> 午後 (ja-JP)<br /><br /> 2009-06-15T13:45:30 ->  (fr-FR)|
|"y"|0부터 99까지의 연도입니다.<br /><br /> 추가 정보: ["y" 사용자 지정 형식 지정자](#ySpecifier)|0001-01-01T00:00:00 -> 1<br /><br /> 0900-01-01T00:00:00 -> 0<br /><br /> 1900-01-01T00:00:00 -> 0<br /><br /> 2009-06-15T13:45:30 -> 9<br /><br /> 2019-06-15T13:45:30 -> 19|
|"yy"|00부터 99까지의 연도입니다.<br /><br /> 추가 정보: ["yy" 사용자 지정 형식 지정자](#yySpecifier)|0001-01-01T00:00:00 -> 01<br /><br /> 0900-01-01T00:00:00 -> 00<br /><br /> 1900-01-01T00:00:00 -> 00<br /><br /> 2019-06-15T13:45:30 -> 19|
|"yyy"|최소 세 자리 숫자로 된 연도입니다.<br /><br /> 추가 정보: ["yyy" 사용자 지정 형식 지정자](#yyySpecifier)|0001-01-01T00:00:00 -> 001<br /><br /> 0900-01-01T00:00:00 -> 900<br /><br /> 1900-01-01T00:00:00 -> 1900<br /><br /> 2009-06-15T13:45:30 -> 2009|
|"yyyy"|네 자리 숫자로 된 연도입니다.<br /><br /> 추가 정보: ["yyyy" 사용자 지정 형식 지정자](#yyyySpecifier)|0001-01-01T00:00:00 -> 0001<br /><br /> 0900-01-01T00:00:00 -> 0900<br /><br /> 1900-01-01T00:00:00 -> 1900<br /><br /> 2009-06-15T13:45:30 -> 2009|
|"yyyyy"|다섯 자리 숫자로 된 연도입니다.<br /><br /> 추가 정보: ["yyyyy" 사용자 지정 형식 지정자](#yyyyySpecifier)|0001-01-01T00:00:00 -> 00001<br /><br /> 2009-06-15T13:45:30 -> 02009|
|"z"|앞에 0이 표시되지 않는 UTC에서의 시간 오프셋입니다.<br /><br /> 추가 정보: ["z" 사용자 지정 형식 지정자](#zSpecifier)|2009-06-15T13:45:30-07:00 -> -7|
|"zz"|한 자리 값의 경우 앞에 0이 표시되는 UTC에서의 시간 오프셋입니다.<br /><br /> 추가 정보: ["zz" 사용자 지정 형식 지정자](#zzSpecifier)|2009-06-15T13:45:30-07:00 -> -07|
|"zzz"|UTC에서의 시간 및 분 오프셋입니다.<br /><br /> 추가 정보: ["zzz" 사용자 지정 형식 지정자](#zzzSpecifier)|2009-06-15T13:45:30-07:00 -> -07:00|
|":"|시간 구분 기호입니다.<br /><br /> 추가 정보: [":" 사용자 지정 형식 지정자](#timeSeparator)|2009-06-15T13:45:30 -> : (en-US)<br /><br /> 2009-06-15T13:45:30 -> . (it-IT)<br /><br /> 2009-06-15T13:45:30 -> : (ja-JP)|
|"/"|날짜 구분 기호입니다.<br /><br /> 추가 정보: ["/" 사용자 지정 형식 지정자](#dateSeparator)|2009-06-15T13:45:30 -> / (en-US)<br /><br /> 2009-06-15T13:45:30 -> - (ar-DZ)<br /><br /> 2009-06-15T13:45:30 -> . (tr-TR)|
|"*string*"<br /><br /> '*string*'|리터럴 문자열 구분 기호입니다.<br /><br /> 추가 정보: [리터럴 문자](#Literals)|2009-06-15T13:45:30 ("arr:" h:m t) -> arr: 1:45 P<br /><br /> 2009-06-15T13:45:30 ('arr:' h:m t) -> arr: 1:45 P|
|%|뒤에 오는 문자를 사용자 지정 형식 지정자로 정의합니다.<br /><br /> 추가 정보: [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)|2009-06-15T13:45:30 (%h) -> 1|
|\\|이스케이프 문자입니다.<br /><br /> 추가 정보: [문자 리터럴](#Literals) 및 [이스케이프 문자 사용](#escape).|2009-06-15T13:45:30 (h \h) -> 1 h|
|기타 문자|문자가 변경되지 않은 상태로 결과 문자열에 복사됩니다.<br /><br /> 추가 정보: [리터럴 문자](#Literals)|2009-06-15T01:45:30 (arr hh:mm t) -> arr 01:45 A|

 다음 단원에서는 각 사용자 지정 날짜 및 시간 형식 지정자에 대한 추가 정보를 제공합니다. 다른 설명이 없는 각 지정자는 <xref:System.DateTime> 값에 사용할 때와 <xref:System.DateTimeOffset> 값에 사용할 때 동일한 문자열을 생성합니다.

<a name="dSpecifier"></a> 

## <a name="the-d-custom-format-specifier"></a>"d" 사용자 지정 형식 지정자
 "d" 사용자 지정 형식 지정자는 일(월 기준)을 1부터 31까지의 숫자로 나타냅니다. 한 자리 일의 경우 앞에 0이 표시되지 않습니다.

 다른 사용자 지정 형식 지정자 없이 "d" 형식 지정자만 사용되면 "d" 표준 날짜 및 시간 형식 지정자로 해석됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 여러 개의 형식 문자열에 "d" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#1)]
 [!code-vb[Formatting.DateAndTime.Custom#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#1)]

 [표로 이동](#table)

<a name="ddSpecifier"></a> 

## <a name="the-dd-custom-format-specifier"></a>"dd" 사용자 지정 형식 지정자
 "dd" 사용자 지정 형식 문자열은 일(월 기준)을 01부터 31까지의 숫자로 나타냅니다. 한 자리 일의 경우 앞에 0이 표시됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "dd" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#2)]
 [!code-vb[Formatting.DateAndTime.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#2)]

 [표로 이동](#table)

<a name="dddSpecifier"></a> 

## <a name="the-ddd-custom-format-specifier"></a>"ddd" 사용자 지정 형식 지정자
 "ddd" 사용자 지정 형식 지정자는 요일의 약식 이름을 나타냅니다. 요일의 지역화된 약식 이름은 현재 또는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames%2A?displayProperty=nameWithType> 속성에서 검색됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "ddd" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#3)]
 [!code-vb[Formatting.DateAndTime.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#3)]

 [표로 이동](#table)

<a name="ddddSpecifier"></a> 

## <a name="the-dddd-custom-format-specifier"></a>"dddd" 사용자 지정 형식 지정자
 "dddd" 사용자 지정 형식 지정자는 임의 개수의 추가 "d" 지정자와 함께 요일의 전체 이름을 나타냅니다. 지역화된 요일 이름은 현재 또는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.DayNames%2A?displayProperty=nameWithType> 속성에서 검색됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "dddd" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#4)]
 [!code-vb[Formatting.DateAndTime.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#4)]

 [표로 이동](#table)

<a name="fSpecifier"></a> 

## <a name="the-f-custom-format-specifier"></a>"f" 사용자 지정 형식 지정자
 "f" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수를 나타냅니다. 즉, 날짜 및 시간 값에서 1/10초까지 표시합니다.

 다른 형식 지정자 없이 "f" 형식 지정자만 사용되면 "f" 표준 날짜 및 시간 형식 지정자로 해석됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 "f" 형식 지정자를 <xref:System.DateTime.ParseExact%2A>, <xref:System.DateTime.TryParseExact%2A>, <xref:System.DateTimeOffset.ParseExact%2A> 또는 <xref:System.DateTimeOffset.TryParseExact%2A> 메서드에 형식 문자열의 일부로 제공하여 사용할 경우, 사용하는 "f" 형식 지정자의 수는 문자열을 구문 분석하는 데 필요한 초의 소수 부분에 대한 최대 유효 자릿수를 나타냅니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "f" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]

 [표로 이동](#table)

<a name="ffSpecifier"></a> 

## <a name="the-ff-custom-format-specifier"></a>"ff" 사용자 지정 형식 지정자
 "ff" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 2개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/100초까지 표시합니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "ff" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]

 [표로 이동](#table)

<a name="fffSpecifier"></a> 

## <a name="the-fff-custom-format-specifier"></a>"fff" 사용자 지정 형식 지정자
 "fff" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 3개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/1000초까지 표시합니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "fff" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]

 [표로 이동](#table)

<a name="ffffSpecifier"></a> 

## <a name="the-ffff-custom-format-specifier"></a>"ffff" 사용자 지정 형식 지정자
 "ffff" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 4개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/10000초까지 표시합니다.

 1/10000초까지 표시하는 것이 가능하기는 하지만 이 값은 의미가 없을 수도 있습니다. 날짜 및 시간 값의 자릿수는 시스템 시계의 정밀도에 따라 달라집니다. Windows NT 3.5 이상 버전과 Windows Vista 운영 체제의 경우 시계의 정밀도는 약 10-15밀리초입니다.

 [표로 이동](#table)

<a name="fffffSpecifier"></a> 

## <a name="the-fffff-custom-format-specifier"></a>"fffff" 사용자 지정 형식 지정자
 "fffff" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 다섯 개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/100000초까지 표시합니다.

 1/100000초까지 표시하는 것이 가능하기는 하지만 이 값은 의미가 없을 수도 있습니다. 날짜 및 시간 값의 자릿수는 시스템 시계의 정밀도에 따라 달라집니다. Windows NT 3.5 이상 버전과 Windows Vista 운영 체제의 경우 시계의 정밀도는 약 10-15밀리초입니다.

 [표로 이동](#table)

<a name="ffffffSpecifier"></a> 

## <a name="the-ffffff-custom-format-specifier"></a>"ffffff" 사용자 지정 형식 지정자
 "ffffff" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 6개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/1000000초까지 표시합니다.

 1/1000000초까지 표시하는 것이 가능하기는 하지만 이 값은 의미가 없을 수도 있습니다. 날짜 및 시간 값의 자릿수는 시스템 시계의 정밀도에 따라 달라집니다. Windows NT 3.5 이상 버전과 Windows Vista 운영 체제의 경우 시계의 정밀도는 약 10-15밀리초입니다.

 [표로 이동](#table)

<a name="fffffffSpecifier"></a> 

## <a name="the-fffffff-custom-format-specifier"></a>"fffffff" 사용자 지정 형식 지정자
 "fffffff" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 7개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/10000000초까지 표시합니다.

 1/10000000초까지 표시하는 것이 가능하기는 하지만 이 값은 의미가 없을 수도 있습니다. 날짜 및 시간 값의 자릿수는 시스템 시계의 정밀도에 따라 달라집니다. Windows NT 3.5 이상 버전과 Windows Vista 운영 체제의 경우 시계의 정밀도는 약 10-15밀리초입니다.

 [표로 이동](#table)

<a name="F_Specifier"></a> 

## <a name="the-f-custom-format-specifier"></a>"F" 사용자 지정 형식 지정자
 "F" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수를 나타냅니다. 즉, 날짜 및 시간 값에서 1/10초까지 표시합니다. 이 자릿수가 0이면 아무 것도 표시되지 않습니다.

 다른 형식 지정자 없이 "F" 형식 지정자만 사용되면 "F" 표준 날짜 및 시간 형식 지정자로 해석됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 <xref:System.DateTime.ParseExact%2A>, <xref:System.DateTime.TryParseExact%2A>, <xref:System.DateTimeOffset.ParseExact%2A> 또는 <xref:System.DateTimeOffset.TryParseExact%2A> 메서드와 함께 F 형식 지정자를 사용할 경우, 사용하는 "F" 형식 지정자의 수는 문자열을 구문 분석하는 데 사용할 수 있는 시간(초)의 최대 유효 자릿수에 대한 최대 개수를 나타냅니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "F" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]

 [표로 이동](#table)

<a name="FF_Specifier"></a> 

## <a name="the-ff-custom-format-specifier"></a>"FF" 사용자 지정 형식 지정자
 "FF" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 2개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/100초까지 표시합니다. 그러나 뒤에 0이 오거나 두 숫자가 0이면 표시되지 않습니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "FF" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]

 [표로 이동](#table)

<a name="FFF_Specifier"></a> 

## <a name="the-fff-custom-format-specifier"></a>"FFF" 사용자 지정 형식 지정자
 "FFF" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 3개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/1000초까지 표시합니다. 그러나 뒤에 0이 오거나 세 숫자가 0이면 표시되지 않습니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "FFF" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]

 [표로 이동](#table)

<a name="FFFF_Specifier"></a> 

## <a name="the-ffff-custom-format-specifier"></a>"FFFF" 사용자 지정 형식 지정자
 "FFFF" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 4개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/10000초까지 표시합니다. 그러나 뒤에 0이 오거나 네 숫자가 0이면 표시되지 않습니다.

 1/10000초까지 표시하는 것이 가능하기는 하지만 이 값은 의미가 없을 수도 있습니다. 날짜 및 시간 값의 자릿수는 시스템 시계의 정밀도에 따라 달라집니다. Windows NT 3.5 이상 버전과 Windows Vista 운영 체제의 경우 시계의 정밀도는 약 10-15밀리초입니다.

 [표로 이동](#table)

<a name="FFFFF_Specifier"></a> 

## <a name="the-fffff-custom-format-specifier"></a>"FFFFF" 사용자 지정 형식 지정자
 "FFFFF" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 5개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/100000초까지 표시합니다. 그러나 뒤에 0이 오거나 다섯 숫자가 0이면 표시되지 않습니다.

 1/100000초까지 표시하는 것이 가능하기는 하지만 이 값은 의미가 없을 수도 있습니다. 날짜 및 시간 값의 자릿수는 시스템 시계의 정밀도에 따라 달라집니다. Windows NT 3.5 이상 버전과 Windows Vista 운영 체제의 경우 시계의 정밀도는 약 10-15밀리초입니다.

 [표로 이동](#table)

<a name="FFFFFF_Specifier"></a> 

## <a name="the-ffffff-custom-format-specifier"></a>"FFFFFF" 사용자 지정 형식 지정자
 "FFFFFF" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 6개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/1000000초까지 표시합니다. 그러나 뒤에 0이 오거나 여섯 숫자가 0이면 표시되지 않습니다.

 1/1000000초까지 표시하는 것이 가능하기는 하지만 이 값은 의미가 없을 수도 있습니다. 날짜 및 시간 값의 자릿수는 시스템 시계의 정밀도에 따라 달라집니다. Windows NT 3.5 이상 버전과 Windows Vista 운영 체제의 경우 시계의 정밀도는 약 10-15밀리초입니다.

 [표로 이동](#table)

<a name="FFFFFFF_Specifier"></a> 

## <a name="the-fffffff-custom-format-specifier"></a>"FFFFFFF" 사용자 지정 형식 지정자
 "FFFFFFF" 사용자 지정 형식 지정자는 초의 소수 부분에 대한 최대 유효 자릿수 7개를 나타냅니다. 즉, 날짜 및 시간 값에서 1/10000000초까지 표시합니다. 그러나 뒤에 0이 오거나 일곱 숫자가 0이면 표시되지 않습니다.

 1/10000000초까지 표시하는 것이 가능하기는 하지만 이 값은 의미가 없을 수도 있습니다. 날짜 및 시간 값의 자릿수는 시스템 시계의 정밀도에 따라 달라집니다. Windows NT 3.5 이상 버전과 Windows Vista 운영 체제의 경우 시계의 정밀도는 약 10-15밀리초입니다.

 [표로 이동](#table)

<a name="gSpecifier"></a> 

## <a name="the-g-or-gg-custom-format-specifier"></a>"g" 또는 "gg" 사용자 지정 형식 지정자
 "g" 또는 "gg" 사용자 지정 형식 지정자는 임의 개수의 추가 "g" 지정자와 함께 A.D. 같은 시대 또는 연대를 나타냅니다. 형식을 지정할 날짜에 연관된 시대 또는 연대 문자열이 없으면 이 지정자는 무시됩니다.

 다른 사용자 지정 형식 지정자 없이 "g" 형식 지정자만 사용되면 "g" 표준 날짜 및 시간 형식 지정자로 해석됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 사용자 지정 형식 문자열에 "g" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#6)]
 [!code-vb[Formatting.DateAndTime.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#6)]

 [표로 이동](#table)

<a name="hSpecifier"></a> 

## <a name="the-h-custom-format-specifier"></a>"h" 사용자 지정 형식 지정자
 "h" 사용자 지정 형식 지정자는 시간을 1부터 12까지의 숫자로 나타냅니다. 즉, 자정 또는 정오 이후의 총 시간을 계산하는 12시간 형식으로 나타냅니다. 자정 이후의 시간과 정오 이후의 같은 시간을 구별할 수 없습니다. 시간은 반올림되지 않으며 한 자리 시간의 경우 앞에 0이 표시되지 않습니다. 예를 들어, 시간이 오전 또는 오후 5:43일 경우 이 사용자 지정 형식 지정자는 "5"를 표시합니다.

 다른 사용자 지정 형식 지정자 없이 "h" 형식 지정자만 사용되면 표준 날짜 및 시간 형식 지정자로 해석되고 <xref:System.FormatException>이 throw됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 사용자 지정 형식 문자열에 "h" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#7)]

 [표로 이동](#table)

<a name="hhSpecifier"></a> 

## <a name="the-hh-custom-format-specifier"></a>"hh" 사용자 지정 형식 지정자
 "hh" 사용자 지정 형식 지정자는 임의 개수의 추가 "h" 지정자와 함께 시간을 1부터 12까지의 숫자로 나타냅니다. 즉, 자정 또는 정오 이후의 총 시간을 계산하는 12시간 형식으로 나타냅니다. 자정 이후의 시간과 정오 이후의 같은 시간을 구별할 수 없습니다. 시간은 반올림되지 않으며 한 자리 시간의 경우 앞에 0이 표시됩니다. 예를 들어, 시간이 오전 또는 오후 5:43일 경우 이 형식 지정자는 "05"를 표시합니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "hh" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#8)]

 [표로 이동](#table)

<a name="H_Specifier"></a> 

## <a name="the-h-custom-format-specifier"></a>"H" 사용자 지정 형식 지정자
 "H" 사용자 지정 형식 지정자는 시간을 0부터 23까지의 숫자로 나타냅니다. 즉, 자정 이후의 시간을 계산하는 24시간(0부터 시작) 형식으로 나타냅니다. 한 자리 시간의 경우 앞에 0이 표시되지 않습니다.

 다른 사용자 지정 형식 지정자 없이 "H" 형식 지정자만 사용되면 표준 날짜 및 시간 형식 지정자로 해석되고 <xref:System.FormatException>이 throw됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 사용자 지정 형식 문자열에 "H" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#9)]
 [!code-vb[Formatting.DateAndTime.Custom#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#9)]

 [표로 이동](#table)

<a name="HH_Specifier"></a> 

## <a name="the-hh-custom-format-specifier"></a>"HH" 사용자 지정 형식 지정자
 "HH" 사용자 지정 형식 지정자는 임의 개수의 추가 "H" 지정자와 함께 시간을 00부터 23까지의 숫자로 나타냅니다. 즉, 자정 이후의 시간을 계산하는 24시간(0부터 시작) 형식으로 나타냅니다. 한 자리 시간의 경우 앞에 0이 표시됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "HH" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#10)]
 [!code-vb[Formatting.DateAndTime.Custom#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#10)]

 [표로 이동](#table)

<a name="KSpecifier"></a> 

## <a name="the-k-custom-format-specifier"></a>"K" 사용자 지정 형식 지정자
 "K" 사용자 지정 형식 지정자는 날짜 및 시간 값의 표준 시간대 정보를 나타냅니다. 이 형식 지정자를 <xref:System.DateTime> 값과 함께 사용할 경우 결과 문자열은 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성 값에 의해 정의됩니다.

-   현지 표준 시간대(<xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성 값이 <xref:System.DateTimeKind.Local?displayProperty=nameWithType>임)의 경우 이 지정자는 "zzz" 지정자와 같으며 UTC(Coordinated Universal Time)에서의 로컬 오프셋(예: "-07:00")이 포함된 결과 문자열을 생성합니다.

-   UTC 시간(<xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성 값이 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType>임)의 경우 결과 문자열에 UTC 날짜를 나타내는 "Z" 문자가 포함됩니다.

-   지정되지 않은 표준 시간대(시간의 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성이 <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>임)의 경우 결과가 <xref:System.String.Empty?displayProperty=nameWithType>와 같습니다.

 <xref:System.DateTimeOffset> 값의 경우 “K” 형식 지정자는 “zz” 형식 지정자와 같으며 UTC에서의 <xref:System.DateTimeOffset> 값 오프셋이 포함된 결과 문자열을 생성합니다.

 다른 사용자 지정 형식 지정자 없이 "K" 형식 지정자만 사용되면 표준 날짜 및 시간 형식 지정자로 해석되고 <xref:System.FormatException>이 throw됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 미국 태평양 표준 시간대에 있는 시스템의 다양한 <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 값에 "K" 사용자 지정 형식 지정자를 사용하여 생성된 문자열을 표시합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#12)]
 [!code-vb[Formatting.DateAndTime.Custom#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#12)]

 [표로 이동](#table)

<a name="mSpecifier"></a> 

## <a name="the-m-custom-format-specifier"></a>"m" 사용자 지정 형식 지정자
 "m" 사용자 지정 형식 지정자는 분을 0부터 59까지의 숫자로 나타냅니다. 분은 마지막 시간 이후 경과한 총 분 수를 나타냅니다. 한 자리 분의 경우 앞에 0이 표시되지 않습니다.

 다른 사용자 지정 형식 지정자 없이 "m" 형식 지정자만 사용되면 "m" 표준 날짜 및 시간 형식 지정자로 해석됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 사용자 지정 형식 문자열에 "m" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#7)]

 [표로 이동](#table)

<a name="mmSpecifier"></a> 

## <a name="the-mm-custom-format-specifier"></a>"mm" 사용자 지정 형식 지정자
 "mm" 사용자 지정 형식 지정자는 임의 개수의 추가 "m" 지정자와 함께 분을 00부터 59까지의 숫자로 나타냅니다. 분은 마지막 시간 이후 경과한 총 분 수를 나타냅니다. 한 자리 분의 경우 앞에 0이 표시됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "mm" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#8)]

 [표로 이동](#table)

<a name="M_Specifier"></a> 

## <a name="the-m-custom-format-specifier"></a>"M" 사용자 지정 형식 지정자
 "M" 사용자 지정 형식 지정자는 월을 1부터 12까지의 숫자(또는 13월까지 있는 역법의 경우 1부터 13까지의 숫자)로 표현합니다. 한 자리 월의 경우 앞에 0이 표시되지 않습니다.

 다른 사용자 지정 형식 지정자 없이 "M" 형식 지정자만 사용되면 "M" 표준 날짜 및 시간 형식 지정자로 해석됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 사용자 지정 형식 문자열에 "M" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#11)]
 [!code-vb[Formatting.DateAndTime.Custom#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#11)]

 [표로 이동](#table)

<a name="MM_Specifier"></a> 

## <a name="the-mm-custom-format-specifier"></a>"MM" 사용자 지정 형식 지정자
 "MM" 사용자 지정 형식 지정자는 월을 01부터 12까지의 숫자(또는 13월까지 있는 역법의 경우 01부터 13까지의 숫자)로 표현합니다. 한 자리 월의 경우 앞에 0이 표시됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "MM" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#2)]
 [!code-vb[Formatting.DateAndTime.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#2)]

 [표로 이동](#table)

<a name="MMM_Specifier"></a> 

## <a name="the-mmm-custom-format-specifier"></a>"MMM" 사용자 지정 형식 지정자
 "MMM" 사용자 지정 형식 지정자는 월의 약식 이름을 나타냅니다. 월의 지역화된 약식 이름은 현재 또는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.AbbreviatedMonthNames%2A?displayProperty=nameWithType> 속성에서 검색됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "MMM" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#3)]
 [!code-vb[Formatting.DateAndTime.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#3)]

 [표로 이동](#table)

<a name="MMMM_Specifier"></a> 

## <a name="the-mmmm-custom-format-specifier"></a>"MMMM" 사용자 지정 형식 지정자
 "MMMM" 사용자 지정 형식 지정자는 월의 전체 이름을 나타냅니다. 월의 지역화된 이름은 현재 또는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A?displayProperty=nameWithType> 속성에서 검색됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "MMMM" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#4)]
 [!code-vb[Formatting.DateAndTime.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#4)]

 [표로 이동](#table)

<a name="sSpecifier"></a> 

## <a name="the-s-custom-format-specifier"></a>"s" 사용자 지정 형식 지정자
 "s" 사용자 지정 형식 지정자는 초를 0부터 59까지의 숫자로 나타냅니다. 결과는 마지막 분 이후 경과한 총 초 수를 나타냅니다. 한 자리 초의 경우 앞에 0이 표시되지 않습니다.

 다른 사용자 지정 형식 지정자 없이 "s" 형식 지정자만 사용되면 "s" 표준 날짜 및 시간 형식 지정자로 해석됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 사용자 지정 형식 문자열에 "s" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#7)]

 [표로 이동](#table)

<a name="ssSpecifier"></a> 

## <a name="the-ss-custom-format-specifier"></a>"ss" 사용자 지정 형식 지정자
 "ss" 사용자 지정 형식 지정자는 임의 개수의 추가 "s" 지정자와 함께 초를 00부터 59까지의 숫자로 나타냅니다. 결과는 마지막 분 이후 경과한 총 초 수를 나타냅니다. 한 자리 초의 경우 앞에 0이 표시됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "ss" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#8)]

 [표로 이동](#table)

<a name="tSpecifier"></a> 

## <a name="the-t-custom-format-specifier"></a>"t" 사용자 지정 형식 지정자
 "t" 사용자 지정 형식 지정자는 AM/PM 지정자의 첫 문자를 나타냅니다. 적절한 지역화된 지정자는 현재 또는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A?displayProperty=nameWithType> 또는 <xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A?displayProperty=nameWithType> 속성에서 검색됩니다. AM 지정자는 0:00:00(자정)부터 11:59:59.999까지의 모든 시간에 사용되고 PM 지정자는 12:00:00(정오)부터 23:59:59.999까지의 모든 시간에 사용됩니다.

 다른 사용자 지정 형식 지정자 없이 "t" 형식 지정자만 사용되면 "t" 표준 날짜 및 시간 형식 지정자로 해석됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 사용자 지정 형식 문자열에 "t" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#7)]

 [표로 이동](#table)

<a name="ttSpecifier"></a> 

## <a name="the-tt-custom-format-specifier"></a>"tt" 사용자 지정 형식 지정자
 "tt" 사용자 지정 형식 지정자는 임의 개수의 추가 "t" 지정자와 함께 전체 AM/PM 지정자를 나타냅니다. 적절한 지역화된 지정자는 현재 또는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A?displayProperty=nameWithType> 또는 <xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A?displayProperty=nameWithType> 속성에서 검색됩니다. AM 지정자는 0:00:00(자정)부터 11:59:59.999까지의 모든 시간에 사용되고 PM 지정자는 12:00:00(정오)부터 23:59:59.999까지의 모든 시간에 사용됩니다.

 "tt" 지정자는 AM과 PM을 구분해야 하는 언어에만 사용해야 합니다. 예를 들어, 일본어 AM/PM 지정자의 경우 첫 번째 문자가 아니라 두 번째 문자가 서로 다릅니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "tt" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp[Formatting.DateAndTime.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#8)]

 [표로 이동](#table)

<a name="ySpecifier"></a> 

## <a name="the-y-custom-format-specifier"></a>"y" 사용자 지정 형식 지정자
 "y" 사용자 지정 형식 지정자는 연도를 한 자리 또는 두 자리 숫자로 나타냅니다. 연도가 두 자리를 넘으면 마지막 두 자리 숫자만 결과에 나타납니다. 2008과 같이 두 자리 연도의 첫 번째 숫자가 0으로 시작하면 앞에 0이 표시되지 않습니다.

 다른 사용자 지정 형식 지정자 없이 "y" 형식 지정자만 사용되면 "y" 표준 날짜 및 시간 형식 지정자로 해석됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 사용자 지정 형식 문자열에 "y" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]

 [표로 이동](#table)

<a name="yySpecifier"></a> 

## <a name="the-yy-custom-format-specifier"></a>"yy" 사용자 지정 형식 지정자
 "yy" 사용자 지정 형식 지정자는 연도를 두 자리 숫자로 나타냅니다. 연도가 두 자리를 넘으면 마지막 두 자리 숫자만 결과에 나타납니다. 두 자리 연도의 유효 자릿수가 두 자리 미만인 경우 두 자리가 되도록 앞에 0이 채워집니다.

 구문 분석 작업에서 "yy" 사용자 지정 형식 지정자를 사용하여 구문 분석되는 2자리 년도는 형식 공급자의 현재 달력의 <xref:System.Globalization.Calendar.TwoDigitYearMax%2A?displayProperty=nameWithType> 속성을 기준으로 해석됩니다. 다음 예제에서는 en-US 문화권(이 경우 현재 문화권)의 기본 양력을 사용하여 두 자리 년도를 갖는 날짜의 문자열 표현을 구문 분석합니다. 그런 다음 <xref:System.Globalization.CultureInfo> 속성이 수정된 <xref:System.Globalization.GregorianCalendar> 개체를 사용하도록 현재 문화권의 <xref:System.Globalization.GregorianCalendar.TwoDigitYearMax%2A> 개체를 변경합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#19](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/parseexact2digityear1.cs#19)]
 [!code-vb[Formatting.DateAndTime.Custom#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/parseexact2digityear1.vb#19)]

 다음 예제에서는 사용자 지정 형식 문자열에 "yy" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]

 [표로 이동](#table)

<a name="yyySpecifier"></a> 

## <a name="the-yyy-custom-format-specifier"></a>"yyy" 사용자 지정 형식 지정자
 "yyy" 사용자 지정 형식 지정자는 연도를 최소 세 자리 숫자로 나타냅니다. 연도의 유효 자릿수가 세 자리보다 많더라도 결과 문자열에 포함됩니다. 연도가 세 자리 미만인 경우 세 자리가 되도록 앞에 0이 채워집니다.

> [!NOTE]
>  연도를 다섯 자리까지 표시할 수 있는 태국 불교식 달력의 경우 이 형식 지정자는 유효 자릿수를 모두 표시합니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "yyy" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]

 [표로 이동](#table)

<a name="yyyySpecifier"></a> 

## <a name="the-yyyy-custom-format-specifier"></a>"yyyy" 사용자 지정 형식 지정자
 "yyyy" 사용자 지정 형식 지정자는 연도를 최소 네 자리 숫자로 나타냅니다. 연도의 유효 자릿수가 네 자리보다 많더라도 결과 문자열에 포함됩니다. 연도가 네 자리 미만인 경우 네 자리가 되도록 앞에 0이 채워집니다.

> [!NOTE]
>  연도를 다섯 자리까지 표시할 수 있는 태국 불교식 달력의 경우 이 형식 지정자는 최소 네 자리 숫자를 표시합니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "yyyy" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]

 [표로 이동](#table)

<a name="yyyyySpecifier"></a> 

## <a name="the-yyyyy-custom-format-specifier"></a>"yyyyy" 사용자 지정 형식 지정자
 "yyyyy" 사용자 지정 형식 지정자는 임의 개수의 추가 "y" 지정자와 함께 연도를 최소 다섯 자리 숫자로 나타냅니다. 연도의 유효 자릿수가 다섯 자리보다 많더라도 결과 문자열에 포함됩니다. 연도가 다섯 자리 미만인 경우 다섯 자리가 되도록 앞에 0이 채워집니다.

 추가 "y" 지정자가 있는 경우 "y" 지정자의 수에 맞도록 앞에 0이 필요한 만큼 채워집니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "yyyyy" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]

 [표로 이동](#table)

<a name="zSpecifier"></a> 

## <a name="the-z-custom-format-specifier"></a>"z" 사용자 지정 형식 지정자
 <xref:System.DateTime> 값에 사용할 경우 "z" 사용자 지정 형식 지정자는 시간 단위로 측정된 UTC(Coordinated Universal Time)에서 로컬 운영 체제의 부호 있는 표준 시간대 오프셋을 나타냅니다. 이 형식 지정자는 인스턴스의 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성 값은 반영하지 않습니다. 따라서 <xref:System.DateTime> 값에는 "z" 형식 지정자를 사용하지 않는 것이 좋습니다.

 <xref:System.DateTimeOffset> 값에 사용할 경우 이 형식 지정자는 시간 단위로 측정된 UTC에서의 <xref:System.DateTimeOffset> 값 오프셋을 나타냅니다.

 오프셋은 항상 앞에 부호가 표시됩니다. 더하기 기호(+)는 UTC보다 앞선 시간을 나타내고 빼기 기호(-)는 UTC보다 늦은 시간을 나타냅니다. 한 자리 오프셋의 경우 앞에 0이 표시되지 않습니다.

 다른 사용자 지정 형식 지정자 없이 "z" 형식 지정자만 사용되면 표준 날짜 및 시간 형식 지정자로 해석되고 <xref:System.FormatException>이 throw됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 다음 예제에서는 사용자 지정 형식 문자열에 "z" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#14)]
 [!code-vb[Formatting.DateAndTime.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#14)]

 [표로 이동](#table)

<a name="zzSpecifier"></a> 

## <a name="the-zz-custom-format-specifier"></a>"zz" 사용자 지정 형식 지정자
 <xref:System.DateTime> 값에 사용할 경우 "zz" 사용자 지정 형식 지정자는 시간 단위로 측정된 UTC에서 로컬 운영 체제의 부호 있는 표준 시간대 오프셋을 나타냅니다. 이 형식 지정자는 인스턴스의 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성 값은 반영하지 않습니다. 따라서 <xref:System.DateTime> 값에는 "zz" 형식 지정자를 사용하지 않는 것이 좋습니다.

 <xref:System.DateTimeOffset> 값에 사용할 경우 이 형식 지정자는 시간 단위로 측정된 UTC에서의 <xref:System.DateTimeOffset> 값 오프셋을 나타냅니다.

 오프셋은 항상 앞에 부호가 표시됩니다. 더하기 기호(+)는 UTC보다 앞선 시간을 나타내고 빼기 기호(-)는 UTC보다 늦은 시간을 나타냅니다. 한 자리 오프셋의 경우 앞에 0이 표시됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "zz" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#14)]
 [!code-vb[Formatting.DateAndTime.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#14)]

 [표로 이동](#table)

<a name="zzzSpecifier"></a> 

## <a name="the-zzz-custom-format-specifier"></a>"zzz" 사용자 지정 형식 지정자
 <xref:System.DateTime> 값에 사용할 경우 "zzz" 사용자 지정 형식 지정자는 시간 및 분 단위로 측정된 UTC에서 로컬 운영 체제의 부호 있는 표준 시간대 오프셋을 나타냅니다. 이 형식 지정자는 인스턴스의 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성 값은 반영하지 않습니다. 따라서 <xref:System.DateTime> 값에는 "zzz" 형식 지정자를 사용하지 않는 것이 좋습니다.

 <xref:System.DateTimeOffset> 값에 사용할 경우 이 형식 지정자는 시간 및 분 단위로 측정된 UTC에서의 <xref:System.DateTimeOffset> 값 오프셋을 나타냅니다.

 오프셋은 항상 앞에 부호가 표시됩니다. 더하기 기호(+)는 UTC보다 앞선 시간을 나타내고 빼기 기호(-)는 UTC보다 늦은 시간을 나타냅니다. 한 자리 오프셋의 경우 앞에 0이 표시됩니다.

 다음 예제에서는 사용자 지정 형식 문자열에 "zzz" 사용자 지정 형식 지정자를 포함합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#14)]
 [!code-vb[Formatting.DateAndTime.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#14)]

 [표로 이동](#table)

<a name="timeSeparator"></a> 

## <a name="the--custom-format-specifier"></a>":" 사용자 지정 형식 지정자
 ":" 사용자 지정 형식 지정자는 시, 분, 초를 구분하는 데 사용되는 시간 구분 기호를 나타냅니다. 적절한 지역화된 시간 구분 기호는 현재 또는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A?displayProperty=nameWithType> 속성에서 검색됩니다.

> [!NOTE]
>  특정 날짜 및 시간 문자열의 시간 구분 기호를 변경하려면 리터럴 문자열 구분 기호 내에서 구분 기호 문자를 지정합니다. 예를 들어 사용자 지정 형식 문자열 `hh'_'dd'_'ss`는 "\_"(밑줄)이 항상 시간 구분 기호로 사용되는 결과 문자열을 생성합니다. 특정 문화권의 모든 날짜에 대한 시간 구분 기호를 변경하려면 현재 문화권의 <xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A?displayProperty=nameWithType> 속성 값을 변경하거나 <xref:System.Globalization.DateTimeFormatInfo> 개체를 인스턴스화하고 해당 <xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A> 속성에 문자를 할당한 다음 <xref:System.IFormatProvider> 매개 변수를 포함하는 서식 지정 메서드의 오버로드를 호출합니다.

 다른 사용자 지정 형식 지정자 없이 ":" 형식 지정자만 사용되면 표준 날짜 및 시간 형식 지정자로 해석되고 <xref:System.FormatException>이 throw됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 [표로 이동](#table)

<a name="dateSeparator"></a> 

## <a name="the--custom-format-specifier"></a>"/" 사용자 지정 형식 지정자
 "/" 사용자 지정 형식 지정자는 년, 월, 일을 구분하는 데 사용되는 날짜 구분 기호를 나타냅니다. 적절한 지역화된 날짜 구분 기호는 현재 또는 지정된 문화권의 <xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A?displayProperty=nameWithType> 속성에서 검색됩니다.

> [!NOTE]
>  특정 날짜 및 시간 문자열의 날짜 구분 기호를 변경하려면 리터럴 문자열 구분 기호 내에서 구분 기호 문자를 지정합니다. 예를 들어 사용자 지정 형식 문자열 `mm'/'dd'/'yyyy`는 "/"를 항상 날짜 구분 기호로 사용하는 결과 문자열을 생성합니다. 특정 문화권의 모든 날짜에 대한 날짜 구분 기호를 변경하려면 현재 문화권의 <xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A?displayProperty=nameWithType> 속성 값을 변경하거나 <xref:System.Globalization.DateTimeFormatInfo> 개체를 인스턴스화하고 해당 <xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A> 속성에 문자를 할당한 다음 <xref:System.IFormatProvider> 매개 변수를 포함하는 서식 지정 메서드의 오버로드를 호출합니다.

 다른 사용자 지정 형식 지정자 없이 "/" 형식 지정자만 사용되면 표준 날짜 및 시간 형식 지정자로 해석되고 <xref:System.FormatException>이 throw됩니다. 단일 형식 지정자를 사용하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [단일 사용자 지정 형식 지정자 사용](#UsingSingleSpecifiers)을 참조하세요.

 [표로 이동](#table)

<a name="Literals"></a> 

## <a name="character-literals"></a>문자 리터럴
 사용자 지정 날짜 및 시간 형식 문자열에서 다음 문자는 예약되었으며 항상 형식 지정 문자 또는 ", ', / 및 \\의 경우 특수 문자로 해석됩니다.

||||||
|-|-|-|-|-|
|F|H|K|M|일|
|f|g|h|분|s|
|t|y|z|%|:|
|/|"|'|\||

 다른 모든 문자는 항상 문자 리터럴로 해석되며, 형식 지정 작업에서 변경되지 않고 결과 문자열에 포함됩니다.  구문 분석 작업에서는 입력 문자열의 문자와 정확히 일치해야 하며, 비교 시 대/소문자를 구분합니다.

 다음 예제에는 형식 문자열에서 현지 표준 시간대를 나타내는 리터럴 문자 "PST"(태평양 표준시) 및 "PDT"(태평양 일광 절약 시간)가 포함되어 있습니다. 문자열이 결과 문자열에 포함되고, 현지 표준 시간대 문자열을 포함하는 문자열도 성공적으로 구문 분석되는 것을 확인합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#20](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/LiteralsEx1.cs#20)]
 [!code-vb[Formatting.DateAndTime.Custom#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/LiteralsEx1.vb#20)]

 문자가 결과 문자열에 포함되거나 입력 문자열에서 성공적으로 구문 분석될 수 있도록 하기 위해 문자를 예약 문자가 아니라 리터럴 문자로 해석되도록 지정하는 두 가지 방법이 있습니다.

- 각 예약된 문자를 이스케이프합니다. 자세한 내용은 [이스케이프 문자 사용](#escape)을 참조하세요.
  
  다음 예제에는 형식 문자열에서 현지 표준 시간대를 나타내는 리터럴 문자 "pst"(태평양 표준시)가 포함되어 있습니다. "s"와 "t"는 둘 다 사용자 지정 형식 문자열이므로 두 문자를 문자 리터럴로 해석되도록 이스케이프해야 합니다.
  
  [!code-csharp-interactive[Formatting.DateAndTime.Custom#21](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/LiteralsEx2.cs#21)]
  [!code-vb[Formatting.DateAndTime.Custom#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/LiteralsEx2.vb#21)]

- 전체 리터럴 문자열을 따옴표나 아포스트로피로 묶습니다. 다음 예제는 "pst"가 따옴표로 묶여 구분된 전체 문자열을 문자 리터럴로 해석해야 한다는 점을 제외하고 이전 예제와 같습니다.
  
  [!code-csharp-interactive[Formatting.DateAndTime.Custom#22](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/LiteralsEx3.cs#22)]
  [!code-vb[Formatting.DateAndTime.Custom#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/LiteralsEx3.vb#22)]

<a name="Notes"></a> 

## <a name="notes"></a>노트

<a name="UsingSingleSpecifiers"></a> 

### <a name="using-single-custom-format-specifiers"></a>단일 사용자 지정 형식 지정자 사용
 사용자 지정 날짜 및 시간 형식 문자열은 둘 이상의 문자로 구성됩니다. 날짜 및 시간 형식 지정 메서드는 단일 문자 문자열을 표준 날짜 및 시간 형식 문자열로 해석합니다. 날짜 및 시간 형식 지정 메서드가 문자를 올바른 형식 지정자로 인식하지 못하면 <xref:System.FormatException>이 throw됩니다. 예를 들어, "h" 지정자로만 구성된 형식 문자열은 표준 날짜 및 시간 형식 문자열로 해석됩니다. 그러나 이 경우 "h" 표준 날짜 및 시간형식 지정자가 없으므로 예외가 발생합니다.

 사용자 지정 날짜 및 시간 형식 지정자 중 하나를 형식 문자열의 유일한 지정자로 사용하려면(즉, "d", "f", "F", "g", "h", "H", "K", "m", "M", "s", "t", "y", "z", ":" 또는 "/" 사용자 지정 형식 지정자를 단독으로 사용하려면) 지정자 앞이나 뒤에 공백을 포함하거나 단일 사용자 지정 날짜 및 시간 지정자 앞에 백분율("%") 형식 지정자를 포함합니다.

 예를 들어, "`%h"`는 현재 날짜 및 시간 값이 나타내는 시간을 표시하는 사용자 지정 날짜 및 시간 형식 문자열로 해석됩니다. 결과 문자열에 시간 외에 공백이 포함되기는 하지만 " h" 또는 "h " 형식 지정자를 사용할 수도 있습니다. 다음 예제에서는 이러한 세 가지 형식 문자열을 보여 줍니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#16](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/literal1.cs#16)]
 [!code-vb[Formatting.DateAndTime.Custom#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/literal1.vb#16)]

<a name="escape"></a> 

### <a name="using-the-escape-character"></a>이스케이프 문자 사용
 형식 문자열의 "d", "f", "F", "g", "h", "H", "K", "m", "M", "s", "t", "y", "z", ":" 또는 "/" 문자는 리터럴 문자가 아닌 사용자 지정 형식 지정자로 해석됩니다. 문자가 형식 지정자로 해석되지 않도록 하려면 해당 문자 앞에 이스케이프 문자인 백슬래시(\\)를 삽입하면 됩니다. 이스케이프 문자는 뒤에 오는 문자가 변경되지 않은 상태로 결과 문자열에 포함되어야 하는 문자 리터럴임을 나타냅니다.

 결과 문자열에 백슬래시를 포함하려면`\\`처럼 두 개의 백슬래시를 연속해서 입력해야 합니다.

> [!NOTE]
>  C++ 및 C# 컴파일러 같은 일부 컴파일러에서는 하나의 백슬래시 문자가 이스케이프 문자로 해석될 수도 있습니다. 형식을 지정할 때 문자열이 올바로 해석되도록 하려면 해당 문자열 앞에 축자 문자열 리터럴 문자(@ 문자)를 사용하거나(C#의 경우) 각 백슬래시 앞에 또 다른 백슬래시를 추가하면 됩니다(C# 및 C++의 경우). 다음 C# 예제에서는 이 두 가지 방법을 모두 보여 줍니다.

 다음 예제에서는 이스케이프 문자를 사용하여 형식 지정 작업에서 "h" 및 "m" 문자가 형식 지정자로 해석되지 않도록 합니다.

 [!code-csharp-interactive[Formatting.DateAndTime.Custom#15](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/escape1.cs#15)]
 [!code-vb[Formatting.DateAndTime.Custom#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/escape1.vb#15)]

### <a name="control-panel-settings"></a>제어판 설정
 제어판의 **국가 및 언어 옵션** 설정은 많은 사용자 지정 날짜 및 시간 형식 지정자를 사용한 형식 지정 작업으로 생성되는 결과 문자열에 영향을 줍니다. 이러한 설정은 형식을 제어하는 데 사용되는 값을 제공하는 현재 스레드 문화권과 연결된 <xref:System.Globalization.DateTimeFormatInfo> 개체를 초기화하는 데 사용됩니다. 다른 설정을 사용하는 컴퓨터는 다른 결과 문자열을 생성합니다.

 또한 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%29?displayProperty=nameWithType> 생성자를 사용하여 현재 시스템 문화권과 동일한 문화권을 나타내는 새 <xref:System.Globalization.CultureInfo> 개체를 인스턴스화하는 경우 제어판의 **국가 및 언어 옵션** 항목을 통해 설정된 사용자 지정 내용이 새 <xref:System.Globalization.CultureInfo> 개체에도 적용됩니다. <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 생성자를 사용하면 시스템의 사용자 지정 내용이 반영되지 않는 <xref:System.Globalization.CultureInfo> 개체를 만들 수 있습니다.

### <a name="datetimeformatinfo-properties"></a>DateTimeFormatInfo 속성
 형식은 현재 스레드 문화권에 의해 암시적으로 제공되거나 형식 지정 작업을 호출하는 메서드의 <xref:System.Globalization.DateTimeFormatInfo> 매개 변수에 의해 명시적으로 제공되는 현재 <xref:System.IFormatProvider> 개체의 속성에 따라 영향을 받습니다. <xref:System.IFormatProvider> 매개 변수의 경우 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체나 <xref:System.Globalization.DateTimeFormatInfo> 개체를 지정해야 합니다.

 대부분의 사용자 지정 날짜 및 시간 형식 지정자로 생성되는 결과 문자열도 현재 <xref:System.Globalization.DateTimeFormatInfo> 개체의 속성에 따라 달라집니다. 따라서 응용 프로그램에서는 해당 <xref:System.Globalization.DateTimeFormatInfo> 속성을 변경하여 일부 사용자 지정 날짜 및 시간 형식 지정자에서 생성된 결과를 변경할 수 있습니다. 예를 들어, "ddd" 형식 지정자는 <xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames%2A> 문자열 배열에서 찾은 약식 요일 이름을 결과 문자열에 추가합니다. 마찬가지로 "MMMM" 형식 지정자는 <xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A> 문자열 배열에서 찾은 전체 월 이름을 결과 문자열에 추가합니다.

## <a name="see-also"></a>참고 항목

- <xref:System.DateTime?displayProperty=nameWithType>
- <xref:System.IFormatProvider?displayProperty=nameWithType>
- [형식 서식 지정](../../../docs/standard/base-types/formatting-types.md)
- [표준 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)
- [샘플: .NET Framework 4 서식 유틸리티](https://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)
