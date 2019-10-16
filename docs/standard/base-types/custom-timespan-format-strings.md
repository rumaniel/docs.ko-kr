---
title: 사용자 지정 TimeSpan 형식 문자열 - .NET
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- format specifiers, custom time interval
- format strings
- formatting [.NET Framework], time interval
- custom time interval format strings
- formatting [.NET Framework], time
- custom TimeSpan format strings
ms.assetid: a63ebf55-7269-416b-b4f5-286f6c03bf0e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 14fbcbbd2e4042fa4f25b3c8993cf47fefd95052
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65644992"
---
# <a name="custom-timespan-format-strings"></a>사용자 지정 TimeSpan 형식 문자열

<xref:System.TimeSpan> 형식 문자열은 서식 지정 작업에서 생성되는 <xref:System.TimeSpan> 값의 텍스트 표현을 정의합니다. 사용자 지정 형식 문자열은 하나 이상의 사용자 지정 <xref:System.TimeSpan> 형식 지정자와 임의 개수의 리터럴 문자로 구성됩니다. [표준 TimeSpan 형식 문자열](standard-timespan-format-strings.md)이 아닌 문자열은 사용자 지정 <xref:System.TimeSpan> 형식 문자열로 해석됩니다.

> [!IMPORTANT]
> 사용자 지정 <xref:System.TimeSpan> 형식 지정자는 일과 시간, 시간과 분 또는 초와 소수 자릿수 초를 구분하는 기호 등의 자리 표시자 구분 기호를 포함하지 않습니다. 대신, 이러한 기호는 사용자 지정 형식 문자열에 문자열 리터럴로 포함되어야 합니다. 예를 들어 `"dd\.hh\:mm"`은 일과 시간의 구분 기호로 마침표(.)를 정의하고 시간과 분의 구분 기호로 콜론(:)을 정의합니다.
>
> 사용자 지정 <xref:System.TimeSpan> 형식 지정자도 음수 및 양수 시간 간격을 구분할 수 있도록 하는 부호 기호를 포함하지 않습니다. 부호 기호를 포함하려면 조건부 논리를 사용하여 서식 문자열을 생성해야 합니다. [기타 문자](#other-characters) 섹션에 예제가 포함되어 있습니다.

<xref:System.TimeSpan> 값의 문자열 표현은 <xref:System.TimeSpan.ToString%2A?displayProperty=nameWithType> 메서드의 오버로드 호출을 통해 그리고 <xref:System.String.Format%2A?displayProperty=nameWithType>과 같이 복합 서식 지정을 지원하는 메서드에 의해 생성됩니다. 자세한 내용은 [서식 지정 형식](formatting-types.md) 및 [복합 서식 지정](composite-formatting.md)을 참조하세요. 다음 예제에서는 서식 지정 작업에서 사용자 지정 형식 문자열을 사용하는 방법을 보여줍니다.

[!code-csharp[Conceptual.TimeSpan.Custom#1](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customformatexample1.cs#1)]
[!code-vb[Conceptual.TimeSpan.Custom#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customformatexample1.vb#1)]

사용자 지정 <xref:System.TimeSpan> 형식 문자열은 <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 및 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드에서도 구문 분석 작업에 필요한 입력 문자열 서식을 정의하는 데 사용합니다. 구문 분석 시에는 값의 문자열 표현이 해당 값으로 변환됩니다. 다음 예제에서는 구문 분석 작업에 표준 형식 문자열을 사용하는 방법을 보여 줍니다.

[!code-csharp[Conceptual.TimeSpan.Custom#2](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customparseexample1.cs#2)]
[!code-vb[Conceptual.TimeSpan.Custom#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customparseexample1.vb#2)]

<a name="table"></a> 다음 표에서는 사용자 지정 날짜 및 시간 형식 지정자에 대해 설명합니다.

| 형식 지정자 | 설명 | 예제 |
|----------------------|-----------------|-------------|
|"d", "%d"|시간 간격의 전체 일 수입니다.<br /><br /> 추가 정보: [“d” 사용자 지정 형식 지정자](#dSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%d` --> "6"<br /><br /> `d\.hh\:mm` --> "6.14:32"|
|“dd”-“dddddddd”|시간 간격의 전체 일 수로, 필요에 따라 앞에 0으로 채워집니다.<br /><br /> 추가 정보: [“dd”-”dddddddd” 사용자 지정 형식 지정자](#ddSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `ddd` --> "006"<br /><br /> `dd\.hh\:mm` --> "06.14:32"|
|"h", "%h"|일 수로 계산되지 않은 시간 간격의 전체 시간 수입니다. 한 자리 시간의 경우 앞에 0이 없습니다.<br /><br /> 추가 정보: [“h” 사용자 지정 형식 지정자](#hSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `%h` --> "14"<br /><br /> `hh\:mm` --> "14:32"|
|"hh"|일 수로 계산되지 않은 시간 간격의 전체 시간 수입니다. 한 자리 시간의 경우 앞에 0이 있습니다.<br /><br /> 추가 정보: [“hh” 사용자 지정 형식 지정자](#hhSpecifier).|`new TimeSpan(6, 14, 32, 17, 685):`<br /><br /> `hh` --> "14"<br /><br /> `new TimeSpan(6, 8, 32, 17, 685):`<br /><br /> `hh` --> 08|
|"m", "%m"|시간 또는 일 수로 계산되지 않은 시간 간격의 전체 분 수입니다. 한 자리 분의 경우 앞에 0이 없습니다.<br /><br /> 추가 정보: [“m” 사용자 지정 형식 지정자](#mSpecifier).|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `%m` --> "8"<br /><br /> `h\:m` --> "14:8"|
|"mm"|시간 또는 일 수로 계산되지 않은 시간 간격의 전체 분 수입니다. 한 자리 분의 경우 앞에 0이 있습니다.<br /><br /> 추가 정보: [“mm” 사용자 지정 형식 지정자](#mmSpecifier).|`new TimeSpan(6, 14, 8, 17, 685):`<br /><br /> `mm` --> "08"<br /><br /> `new TimeSpan(6, 8, 5, 17, 685):`<br /><br /> `d\.hh\:mm\:ss` --> 6.08:05:17|
|"s", "%s"|시간, 일 또는 분 수로 계산되지 않은 시간 간격의 전체 초 수입니다. 한 자리 초의 경우 앞에 0이 없습니다.<br /><br /> 추가 정보: [“s” 사용자 지정 형식 지정자](#sSpecifier).|`TimeSpan.FromSeconds(12.965)`:<br /><br /> `%s` --> 12<br /><br /> `s\.fff` --> 12.965|
|"ss"|시간, 일 또는 분 수로 계산되지 않은 시간 간격의 전체 초 수입니다.  한 자리 초의 경우 앞에 0이 있습니다.<br /><br /> 추가 정보: [“ss” 사용자 지정 형식 지정자](#ssSpecifier).|`TimeSpan.FromSeconds(6.965)`:<br /><br /> `ss` --> 06<br /><br /> `ss\.fff` --> 06.965|
|"f", "%f"|시간 간격의 1/10초입니다.<br /><br /> 추가 정보: [“f” 사용자 지정 형식 지정자](#fSpecifier).|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `f` --> 8<br /><br /> `ss\.f` --> 06.8|
|"ff"|시간 간격의 1/100초입니다.<br /><br /> 추가 정보: [“ff” 사용자 지정 형식 지정자](#ffSpecifier).|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `ff` --> 89<br /><br /> `ss\.ff` --> 06.89|
|"fff"|시간 간격의 밀리초입니다.<br /><br /> 추가 정보: [“fff” 사용자 지정 형식 지정자](#f3Specifier).|`TimeSpan.FromSeconds(6.895)`:<br /><br /> `fff` --> 895<br /><br /> `ss\.fff` --> 06.895|
|"ffff"|시간 간격의 1/10000초입니다.<br /><br /> 추가 정보: [“ffff” 사용자 지정 형식 지정자](#f4Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `ffff` --> 8954<br /><br /> `ss\.ffff` --> 06.8954|
|"fffff"|시간 간격의 1/100000초입니다.<br /><br /> 추가 정보: [“fffff” 사용자 지정 형식 지정자](#f5Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `fffff` --> 89543<br /><br /> `ss\.fffff` --> 06.89543|
|"ffffff"|시간 간격의 1/1000000초입니다.<br /><br /> 추가 정보: [“ffffff” 사용자 지정 형식 지정자](#f6Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `ffffff` --> 895432<br /><br /> `ss\.ffffff` --> 06.895432|
|"fffffff"|시간 간격의 1/10000000초(또는 소수 자릿수 틱)입니다.<br /><br /> 추가 정보: [“fffffff” 사용자 지정 형식 지정자](#f7Specifier).|`TimeSpan.Parse("0:0:6.8954321")`:<br /><br /> `fffffff` --> 8954321<br /><br /> `ss\.fffffff` --> 06.8954321|
|"F", "%F"|시간 간격의 1/10초입니다. 이 자릿수가 0이면 아무 것도 표시되지 않습니다.<br /><br /> 추가 정보: [“F” 사용자 지정 형식 지정자](#F_Specifier).|`TimeSpan.Parse("00:00:06.32")`:<br /><br /> `%F`: 3<br /><br /> `TimeSpan.Parse("0:0:3.091")`:<br /><br /> `ss\.F`: 03.|
|"FF"|시간 간격의 1/100초입니다. 뒤에 오는 소수 자릿수 0이나 연속 두 자리 0은 포함되지 않습니다.<br /><br /> 추가 정보: [“FF” 사용자 지정 형식 지정자](#FF_Specifier).|`TimeSpan.Parse("00:00:06.329")`:<br /><br /> `FF`: 32<br /><br /> `TimeSpan.Parse("0:0:3.101")`:<br /><br /> `ss\.FF`: 03.1|
|"FFF"|시간 간격의 밀리초입니다. 뒤에 오는 소수 자릿수 0은 포함되지 않습니다.<br /><br /> 추가 정보:|`TimeSpan.Parse("00:00:06.3291")`:<br /><br /> `FFF`: 329<br /><br /> `TimeSpan.Parse("0:0:3.1009")`:<br /><br /> `ss\.FFF`: 03.1|
|"FFFF"|시간 간격의 1/10000초입니다. 뒤에 오는 소수 자릿수 0은 포함되지 않습니다.<br /><br /> 추가 정보: [“FFFF” 사용자 지정 형식 지정자](#F4_Specifier).|`TimeSpan.Parse("00:00:06.32917")`:<br /><br /> `FFFFF`: 3291<br /><br /> `TimeSpan.Parse("0:0:3.10009")`:<br /><br /> `ss\.FFFF`: 03.1|
|"FFFFF"|시간 간격의 1/100000초입니다. 뒤에 오는 소수 자릿수 0은 포함되지 않습니다.<br /><br /> 추가 정보: [“FFFFF” 사용자 지정 형식 지정자](#F5_Specifier).|`TimeSpan.Parse("00:00:06.329179")`:<br /><br /> `FFFFF`: 32917<br /><br /> `TimeSpan.Parse("0:0:3.100009")`:<br /><br /> `ss\.FFFFF`: 03.1|
|"FFFFFF"|시간 간격의 1/1000000초입니다. 뒤에 오는 소수 자릿수 0은 표시되지 않습니다.<br /><br /> 추가 정보: [“FFFFFF” 사용자 지정 형식 지정자](#F6_Specifier).|`TimeSpan.Parse("00:00:06.3291791")`:<br /><br /> `FFFFFF`: 329179<br /><br /> `TimeSpan.Parse("0:0:3.1000009")`:<br /><br /> `ss\.FFFFFF`: 03.1|
|"FFFFFFF"|시간 간격의 1/10000000초입니다. 뒤에 오는 소수 자릿수 0이나 연속 일곱 자리 0은 표시되지 않습니다.<br /><br /> 추가 정보: [“FFFFFFF” 사용자 지정 형식 지정자](#F7_Specifier).|`TimeSpan.Parse("00:00:06.3291791")`:<br /><br /> `FFFFFF`: 3291791<br /><br /> `TimeSpan.Parse("0:0:3.1900000")`:<br /><br /> `ss\.FFFFFF`: 03.19|
|'*string*'|리터럴 문자열 구분 기호입니다.<br /><br /> 추가 정보: [기타 문자](#other-characters).|`new TimeSpan(14, 32, 17):`<br /><br /> `hh':'mm':'ss` --> "14:32:17"|
|&#92;|이스케이프 문자입니다.<br /><br /> 추가 정보: [기타 문자](#other-characters).|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` --> "14:32:17"|
|기타 문자|이스케이프되지 않은 다른 모든 문자는 사용자 지정 형식 지정자로 해석됩니다.<br /><br /> 추가 정보: [기타 문자](#other-characters).|`new TimeSpan(14, 32, 17):`<br /><br /> `hh\:mm\:ss` --> "14:32:17"|

## <a name="dSpecifier"></a> “d” 사용자 지정 형식 지정자

“d” 사용자 지정 형식 지정자는 시간 간격의 전체 일 수를 나타내는 <xref:System.TimeSpan.Days%2A?displayProperty=nameWithType> 속성 값을 출력합니다. 값이 두 자리 이상인 경우에도 <xref:System.TimeSpan> 값에 전체 일 수를 출력합니다. <xref:System.TimeSpan.Days%2A?displayProperty=nameWithType> 속성 값이 0이면 지정자는 “0”을 출력합니다.

“d” 사용자 지정 형식 지정자만 단독으로 사용하는 경우 표준 형식 문자열로 잘못 해석되지 않도록 “%d”를 지정합니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#3](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#3)]
[!code-vb[Conceptual.TimeSpan.Custom#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#3)]

다음 예제에서는 "d" 사용자 지정 형식 지정자를 사용하는 방법을 보여 줍니다.

[!code-csharp[Conceptual.TimeSpan.Custom#4](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#4)]
[!code-vb[Conceptual.TimeSpan.Custom#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#4)]

[표로 이동](#table)

## <a name="ddSpecifier"></a> “dd”-”dddddddd” 사용자 지정 형식 지정자

“dd”, “ddd”, “dddd”, “ddddd”, “dddddd”, “ddddddd” 및 “dddddddd” 사용자 지정 형식 지정자는 시간 간격의 전체 일 수를 나타내는 <xref:System.TimeSpan.Days%2A?displayProperty=nameWithType> 속성 값을 출력합니다.

출력 문자열에는 형식 지정자에 “d” 문자 수로 지정된 최소 자릿수가 포함되며 필요에 따라 앞에 0으로 채워집니다. 일 수의 자릿수가 형식 지정자의 "d" 문자 수를 초과할 경우 전체 일 수가 결과 문자열에 출력됩니다.

다음 예제에서는 이러한 형식 지정자를 사용하여 두 <xref:System.TimeSpan> 값의 문자열 표현을 표시합니다. 첫 번째 시간 간격의 일 구성 요소 값은 0입니다. 두 번째 시간 간격의 일 구성 요소 값은 365입니다.

[!code-csharp[Conceptual.TimeSpan.Custom#5](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#5)]
[!code-vb[Conceptual.TimeSpan.Custom#5](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#5)]

[표로 이동](#table)

## <a name="hSpecifier"></a> “h” 사용자 지정 형식 지정자

“h” 사용자 지정 형식 지정자는 일 구성 요소의 일부로 계산되지 않은 시간 간격의 전체 시간 수를 나타내는 <xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType> 속성 값을 출력합니다. <xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType> 속성 값이 0-9이면 한 자리 문자열 값을 반환하고, <xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType> 속성 값이 10-23이면 두 자리 문자열 값을 반환합니다.

“h” 사용자 지정 형식 지정자만 단독으로 사용하는 경우 표준 형식 문자열로 잘못 해석되지 않도록 “%h”를 지정합니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#6](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
[!code-vb[Conceptual.TimeSpan.Custom#6](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]

일반적으로 구문 분석 작업에서 하나의 숫자만 포함하는 입력 문자열은 일 수로 해석됩니다. "%h" 사용자 지정 형식 지정자를 대신 사용하여 숫자 문자열을 시간 수로 해석할 수 있습니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#8](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#8)]
[!code-vb[Conceptual.TimeSpan.Custom#8](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#8)]

다음 예제에서는 "h" 사용자 지정 형식 지정자를 사용하는 방법을 보여 줍니다.

[!code-csharp[Conceptual.TimeSpan.Custom#7](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#7)]
[!code-vb[Conceptual.TimeSpan.Custom#7](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#7)]

[표로 이동](#table)

## <a name="hhSpecifier"></a> “hh” 사용자 지정 형식 지정자

“hh” 사용자 지정 형식 지정자는 일 구성 요소의 일부로 계산되지 않은 시간 간격의 전체 시간 수를 나타내는 <xref:System.TimeSpan.Hours%2A?displayProperty=nameWithType> 속성 값을 출력합니다. 0-9 값의 경우 출력 문자열 앞에 0이 포함됩니다.

일반적으로 구문 분석 작업에서 하나의 숫자만 포함하는 입력 문자열은 일 수로 해석됩니다. "hh" 사용자 지정 형식 지정자를 대신 사용하여 숫자 문자열을 시간 수로 해석할 수 있습니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#9](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#9)]
[!code-vb[Conceptual.TimeSpan.Custom#9](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#9)]

다음 예제에서는 "hh" 사용자 지정 형식 지정자를 사용하는 방법을 보여 줍니다.

[!code-csharp[Conceptual.TimeSpan.Custom#10](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#10)]
[!code-vb[Conceptual.TimeSpan.Custom#10](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#10)]

[표로 이동](#table)

## <a name="mSpecifier"></a> “m” 사용자 지정 형식 지정자

“m” 사용자 지정 형식 지정자는 일 구성 요소의 일부로 계산되지 않은 시간 간격의 전체 시간 수를 나타내는 <xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType> 속성 값을 출력합니다. <xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType> 속성 값이 0-9이면 한 자리 문자열 값을 반환하고, <xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType> 속성 값이 10-59이면 두 자리 문자열 값을 반환합니다.

“m” 사용자 지정 형식 지정자만 단독으로 사용하는 경우 표준 형식 문자열로 잘못 해석되지 않도록 “%m”을 지정합니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#6](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#6)]
[!code-vb[Conceptual.TimeSpan.Custom#6](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#6)]

일반적으로 구문 분석 작업에서 하나의 숫자만 포함하는 입력 문자열은 일 수로 해석됩니다. "%m" 사용자 지정 형식 지정자를 대신 사용하여 숫자 문자열을 분 수로 해석할 수 있습니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#11](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#11)]
[!code-vb[Conceptual.TimeSpan.Custom#11](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#11)]

다음 예제에서는 "m" 사용자 지정 형식 지정자를 사용하는 방법을 보여 줍니다.

[!code-csharp[Conceptual.TimeSpan.Custom#12](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#12)]
[!code-vb[Conceptual.TimeSpan.Custom#12](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#12)]

[표로 이동](#table)

## <a name="mmSpecifier"></a> “mm” 사용자 지정 형식 지정자

“mm” 사용자 지정 형식 지정자는 시간 또는 일 구성 요소의 일부로 포함되지 않은 시간 간격의 전체 분 수를 나타내는 <xref:System.TimeSpan.Minutes%2A?displayProperty=nameWithType> 속성 값을 출력합니다. 0-9 값의 경우 출력 문자열 앞에 0이 포함됩니다.

일반적으로 구문 분석 작업에서 하나의 숫자만 포함하는 입력 문자열은 일 수로 해석됩니다. "mm" 사용자 지정 형식 지정자를 대신 사용하여 숫자 문자열을 분 수로 해석할 수 있습니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#13](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#13)]
[!code-vb[Conceptual.TimeSpan.Custom#13](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#13)]

다음 예제에서는 "mm" 사용자 지정 형식 지정자를 사용하는 방법을 보여 줍니다.

[!code-csharp[Conceptual.TimeSpan.Custom#14](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#14)]
[!code-vb[Conceptual.TimeSpan.Custom#14](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#14)]

[표로 이동](#table)

## <a name="sSpecifier"></a> “s” 사용자 지정 형식 지정자

“s” 사용자 지정 형식 지정자는 시간, 일 또는 분 구성 요소의 일부로 포함되지 않은 시간 간격의 전체 초 수를 나타내는 <xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType> 속성 값을 출력합니다. <xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType> 속성 값이 0-9이면 한 자리 문자열 값을 반환하고, <xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType> 속성 값이 10-59이면 두 자리 문자열 값을 반환합니다.

“s” 사용자 지정 형식 지정자만 단독으로 사용하는 경우 표준 형식 문자열로 잘못 해석되지 않도록 “%s”를 지정합니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#15](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#15)]
[!code-vb[Conceptual.TimeSpan.Custom#15](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#15)]

일반적으로 구문 분석 작업에서 하나의 숫자만 포함하는 입력 문자열은 일 수로 해석됩니다. "%s" 사용자 지정 형식 지정자를 대신 사용하여 숫자 문자열을 초 수로 해석할 수 있습니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#17](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#17)]
[!code-vb[Conceptual.TimeSpan.Custom#17](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#17)]

다음 예제에서는 "s" 사용자 지정 형식 지정자를 사용하는 방법을 보여 줍니다.

[!code-csharp[Conceptual.TimeSpan.Custom#16](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#16)]
[!code-vb[Conceptual.TimeSpan.Custom#16](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#16)]

[표로 이동](#table)

## <a name="ssSpecifier"></a> “ss” 사용자 지정 형식 지정자

“ss” 사용자 지정 형식 지정자는 시간, 일 또는 분 구성 요소의 일부로 포함되지 않은 시간 간격의 전체 초 수를 나타내는 <xref:System.TimeSpan.Seconds%2A?displayProperty=nameWithType> 속성 값을 출력합니다. 0-9 값의 경우 출력 문자열 앞에 0이 포함됩니다.

일반적으로 구문 분석 작업에서 하나의 숫자만 포함하는 입력 문자열은 일 수로 해석됩니다. "ss" 사용자 지정 형식 지정자를 대신 사용하여 숫자 문자열을 초 수로 해석할 수 있습니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#18](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#18)]
[!code-vb[Conceptual.TimeSpan.Custom#18](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#18)]

다음 예제에서는 "ss" 사용자 지정 형식 지정자를 사용하는 방법을 보여 줍니다.

[!code-csharp[Conceptual.TimeSpan.Custom#19](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/customexamples1.cs#19)]
[!code-vb[Conceptual.TimeSpan.Custom#19](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/customexamples1.vb#19)]

[표로 이동](#table)

## <a name="fSpecifier"></a> “f” 사용자 지정 형식 지정자

"f" 사용자 지정 형식 지정자는 시간 간격의 1/10초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 입력 문자열에는 정확히 소수 한 자리가 포함되어야 합니다.

“f” 사용자 지정 형식 지정자만 단독으로 사용하는 경우 표준 형식 문자열로 잘못 해석되지 않도록 “%f”를 지정합니다.

다음 예제에서는 “f” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/10초를 표시합니다. "f"가 먼저 유일한 형식 지정자로 사용된 다음 사용자 지정 형식 문자열에서 "s" 지정자와 함께 사용됩니다.

[!code-csharp[Conceptual.TimeSpan.Custom#20](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
[!code-vb[Conceptual.TimeSpan.Custom#20](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]

[표로 이동](#table)

## <a name="ffSpecifier"></a> “ff” 사용자 지정 형식 지정자

"ff" 사용자 지정 형식 지정자는 시간 간격의 1/100초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 입력 문자열에는 정확히 소수 두 자리가 포함되어야 합니다.

다음 예제에서는 “ff” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/100초를 표시합니다. "ff"가 먼저 유일한 형식 지정자로 사용된 다음 사용자 지정 형식 문자열에서 "s" 지정자와 함께 사용됩니다.

[!code-csharp[Conceptual.TimeSpan.Custom#20](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
[!code-vb[Conceptual.TimeSpan.Custom#20](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]

[표로 이동](#table)

## <a name="f3Specifier"></a> “fff” 사용자 지정 형식 지정자

"fff" 사용자 지정 형식 지정자(세 개의 "f" 문자 포함)는 시간 간격의 밀리초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 입력 문자열에는 정확히 소수 세 자리가 포함되어야 합니다.

다음 예제에서는 “fff” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 밀리초를 표시합니다. "fff"가 먼저 유일한 형식 지정자로 사용된 다음 사용자 지정 형식 문자열에서 "s" 지정자와 함께 사용됩니다.

[!code-csharp[Conceptual.TimeSpan.Custom#20](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
[!code-vb[Conceptual.TimeSpan.Custom#20](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]

[표로 이동](#table)

## <a name="f4Specifier"></a> “ffff” 사용자 지정 형식 지정자

"ffff" 사용자 지정 형식 지정자(네 개의 "f" 문자 포함)는 시간 간격의 1/10000초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 입력 문자열에는 정확히 소수 네 자리가 포함되어야 합니다.

다음 예제에서는 “ffff” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/10000초를 표시합니다. "ffff"가 먼저 유일한 형식 지정자로 사용된 다음 사용자 지정 형식 문자열에서 "s" 지정자와 함께 사용됩니다.

[!code-csharp[Conceptual.TimeSpan.Custom#20](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
[!code-vb[Conceptual.TimeSpan.Custom#20](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]

[표로 이동](#table)

## <a name="f5Specifier"></a> “fffff” 사용자 지정 형식 지정자

"fffff" 사용자 지정 형식 지정자(다섯 개의 "f" 문자 포함)는 시간 간격의 1/100000초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 입력 문자열에는 정확히 소수 다섯 자리가 포함되어야 합니다.

다음 예제에서는 “fffff” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/100000초를 표시합니다. "fffff"가 먼저 유일한 형식 지정자로 사용된 다음 사용자 지정 형식 문자열에서 "s" 지정자와 함께 사용됩니다.

[!code-csharp[Conceptual.TimeSpan.Custom#20](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
[!code-vb[Conceptual.TimeSpan.Custom#20](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]

[표로 이동](#table)

## <a name="f6Specifier"></a> “ffffff” 사용자 지정 형식 지정자

"ffffff" 사용자 지정 형식 지정자(여섯 개의 "f" 문자 포함)는 시간 간격의 1/1000000초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 입력 문자열에는 정확히 소수 여섯 자리가 포함되어야 합니다.

다음 예제에서는 “ffffff” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/1000000초를 표시합니다. 먼저 유일한 형식 지정자로 사용된 다음 사용자 지정 형식 문자열에서 "s" 지정자와 함께 사용됩니다.

[!code-csharp[Conceptual.TimeSpan.Custom#20](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
[!code-vb[Conceptual.TimeSpan.Custom#20](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]

[표로 이동](#table)

## <a name="f7Specifier"></a> “fffffff” 사용자 지정 형식 지정자

"fffffff" 사용자 지정 형식 지정자(일곱 개의 "f" 문자 포함)는 시간 간격의 1/10000000초(또는 소수 자릿수 틱)를 출력합니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 입력 문자열에는 정확히 소수 일곱 자리가 포함되어야 합니다.

다음 예제에서는 “fffffff” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 소수 자릿수 틱을 표시합니다. 먼저 유일한 형식 지정자로 사용된 다음 사용자 지정 형식 문자열에서 "s" 지정자와 함께 사용됩니다.

[!code-csharp[Conceptual.TimeSpan.Custom#20](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/fspecifiers1.cs#20)]
[!code-vb[Conceptual.TimeSpan.Custom#20](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/fspecifiers1.vb#20)]

[표로 이동](#table)

## <a name="F_Specifier"></a> “F” 사용자 지정 형식 지정자

"F" 사용자 지정 형식 지정자는 시간 간격의 1/10초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. 시간 간격의 1/10초 값이 0이면 결과 문자열에 포함되지 않습니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 1/10초 숫자 표시는 선택 사항입니다.

“F” 사용자 지정 형식 지정자만 단독으로 사용하는 경우 표준 형식 문자열로 잘못 해석되지 않도록 “%F”를 지정합니다.

다음 예제에서는 “F” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/10초를 표시합니다. 또한 구문 분석 작업에서 이 사용자 지정 형식 지정자를 사용합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#21](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#21)]
[!code-vb[Conceptual.TimeSpan.Custom#21](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#21)]

[표로 이동](#table)

## <a name="FF_Specifier"></a> “FF” 사용자 지정 형식 지정자

"FF" 사용자 지정 형식 지정자는 시간 간격의 1/100초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. 뒤에 오는 소수 자릿수 0이 있는 경우 결과 문자열에 포함되지 않습니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 1/10초 및 1/100초 숫자 표시는 선택 사항입니다.

다음 예제에서는 “FF” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/100초를 표시합니다. 또한 구문 분석 작업에서 이 사용자 지정 형식 지정자를 사용합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#22](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#22)]
[!code-vb[Conceptual.TimeSpan.Custom#22](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#22)]

[표로 이동](#table)

## <a name="F3_Specifier"></a> “FFF” 사용자 지정 형식 지정자

"FFF" 사용자 지정 형식 지정자(세 개의 "F" 문자 포함)는 시간 간격의 밀리초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. 뒤에 오는 소수 자릿수 0이 있는 경우 결과 문자열에 포함되지 않습니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 1/10초, 1/100초 및 1/1000초 숫자 표시는 선택 사항입니다.

다음 예제에서는 “FFF” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/1000초를 표시합니다. 또한 구문 분석 작업에서 이 사용자 지정 형식 지정자를 사용합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#23](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#23)]
[!code-vb[Conceptual.TimeSpan.Custom#23](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#23)]

[표로 이동](#table)

## <a name="F4_Specifier"></a> “FFFF” 사용자 지정 형식 지정자

"FFFF" 사용자 지정 형식 지정자(네 개의 "F" 문자 포함)는 시간 간격의 1/10000초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. 뒤에 오는 소수 자릿수 0이 있는 경우 결과 문자열에 포함되지 않습니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 1/10초, 1/100초, 1/1000초 및 1/10000초 숫자 표시는 선택 사항입니다.

다음 예제에서는 “FFFF” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/10000초를 표시합니다. 또한 구문 분석 작업에서 "FFFF" 사용자 지정 형식 지정자를 사용합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#24](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#24)]
[!code-vb[Conceptual.TimeSpan.Custom#24](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#24)]

[표로 이동](#table)

## <a name="F5_Specifier"></a> “FFFFF” 사용자 지정 형식 지정자

"FFFFF" 사용자 지정 형식 지정자(다섯 개의 "F" 문자 포함)는 시간 간격의 1/100000초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. 뒤에 오는 소수 자릿수 0이 있는 경우 결과 문자열에 포함되지 않습니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 1/10초, 1/100초, 1/1000초, 1/10000초 및 1/100000초 숫자 표시는 선택 사항입니다.

다음 예제에서는 “FFFFF” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/100000초를 표시합니다. 또한 구문 분석 작업에서 "FFFFF" 사용자 지정 형식 지정자를 사용합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#25](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#25)]
[!code-vb[Conceptual.TimeSpan.Custom#25](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#25)]

[표로 이동](#table)

## <a name="F6_Specifier"></a> “FFFFFF” 사용자 지정 형식 지정자

"FFFFFF" 사용자 지정 형식 지정자(여섯 개의 "F" 문자 포함)는 시간 간격의 1/1000000초를 출력합니다. 형식 지정 작업에서 나머지 소수 자릿수는 잘립니다. 뒤에 오는 소수 자릿수 0이 있는 경우 결과 문자열에 포함되지 않습니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 1/10초, 1/100초, 1/1000초, 1/10000초, 1/100000초 및 1/1000000초 숫자 표시는 선택 사항입니다.

다음 예제에서는 “FFFFFF” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1/1000000초를 표시합니다. 또한 구문 분석 작업에서 이 사용자 지정 형식 지정자를 사용합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#26](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#26)]
[!code-vb[Conceptual.TimeSpan.Custom#26](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#26)]

[표로 이동](#table)

## <a name="F7_Specifier"></a> “FFFFFFF” 사용자 지정 형식 지정자

"FFFFFFF" 사용자 지정 형식 지정자(일곱 개의 "F" 문자 포함)는 시간 간격의 1/10000000초(또는 소수 자릿수 틱)를 출력합니다. 뒤에 오는 소수 자릿수 0이 있는 경우 결과 문자열에 포함되지 않습니다. <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 또는 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드를 호출하는 구문 분석 작업에서 입력 문자열의 소수 일곱 자리 표시는 선택 사항입니다.

다음 예제에서는 “FFFFFFF” 사용자 지정 형식 지정자를 사용하여 <xref:System.TimeSpan> 값에 1초의 소수 자릿수 부분을 표시합니다. 또한 구문 분석 작업에서 이 사용자 지정 형식 지정자를 사용합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#27](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/f_specifiers1.cs#27)]
[!code-vb[Conceptual.TimeSpan.Custom#27](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/f_specifiers1.vb#27)]

[표로 이동](#table)

## <a name="other-characters"></a>기타 문자

공백 문자를 포함하여 형식 문자열에서 이스케이프되지 않은 다른 모든 문자는 사용자 지정 형식 지정자로 해석됩니다. 대부분의 경우 이스케이프되지 않은 다른 문자가 있으면 <xref:System.FormatException>이 발생합니다.

형식 문자열에 리터럴 문자를 포함하는 방법에는 다음 두 가지가 있습니다.

- 작은따옴표(리터럴 문자열 구분 기호)로 묶습니다.

- 이스케이프 문자로 해석되는 백슬래시(“\\”)를 앞에 추가합니다. 즉, C#에서는 서식 문자열이 @-quoted여야 하거나 리터럴 문자 앞에 백슬래시를 추가해야 합니다.

  경우에 따라 조건부 논리를 사용하여 서식 문자열에 이스케이프된 리터럴을 포함해야 할 수 있습니다. 다음 예제에서는 조건부 논리를 사용하여 음수 시간 간격에 대해 부호 기호를 포함합니다.

  [!code-csharp[Conceptual.TimeSpan.Custom#29](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/negativevalues1.cs#29)]
  [!code-vb[Conceptual.TimeSpan.Custom#29](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/negativevalues1.vb#29)]

.NET에서는 시간 간격의 구분 기호에 대한 문법을 정의하지 않습니다. 즉, 일과 시간, 시간과 분, 분과 초, 초와 1초의 소수 자릿수 간 구분 기호를 형식 문자열에서 모두 문자 리터럴로 처리해야 합니다.

다음 예제에서는 이스케이프 문자와 작은따옴표를 둘 다 사용하여 출력 문자열에서 "분" 단어가 포함된 사용자 지정 형식 문자열을 정의합니다.

[!code-csharp[Conceptual.TimeSpan.Custom#28](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.custom/cs/literal1.cs#28)]
[!code-vb[Conceptual.TimeSpan.Custom#28](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.custom/vb/literal1.vb#28)]

[표로 이동](#table)

## <a name="see-also"></a>참고 항목

- [형식 서식 지정](formatting-types.md)
- [표준 TimeSpan 서식 문자열](standard-timespan-format-strings.md)
