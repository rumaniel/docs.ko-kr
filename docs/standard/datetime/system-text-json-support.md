---
title: System.Text.Json의 DateTime 및 DateTimeOffset 지원
description: DateTime 및 DateTimeOffset 형식이 System.object 라이브러리에서 지원 되는 방법에 대 한 개요입니다.
ms.technology: dotnet-standard
author: layomia
ms.author: laakinri
ms.date: 07/22/2019
helpviewer_keywords:
- JSON, Serializer, Utf8
- JSON DateTime, JSON DateTimeOffset
- DateTime, DateTimeOffset
- JsonSerializer, Utf8JsonReader, Utf8JsonWriter, JsonElement, JsonDocument
- JSON Serializer, JSON Reader, JSON Writer
- Converter, JSON Converter, DateTime Converter
- ISO, ISO 8601, ISO 8601-1:2019
ms.openlocfilehash: 000a6b6dc892e65b50ae413ab3cb95d2a73ef0ef
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182580"
---
# <a name="datetime-and-datetimeoffset-support-in-systemtextjson"></a>System.Text.Json의 DateTime 및 DateTimeOffset 지원

System.string 라이브러리는 ISO 8601:-2019 확장 프로필에 따라 및 <xref:System.DateTime> <xref:System.DateTimeOffset> 값을 구문 분석 하 고 기록 합니다.
[변환기](xref:System.Text.Json.Serialization.JsonConverter%601) 는로 serialize 및 deserialize 할 수 있는 <xref:System.Text.Json.JsonSerializer>사용자 지정 지원을 제공 합니다.
및를 <xref:System.Text.Json.Utf8JsonReader> <xref:System.Text.Json.Utf8JsonWriter>사용 하는 경우에도 사용자 지정 지원을 구현할 수 있습니다.

## <a name="support-for-the-iso-8601-12019-format"></a>ISO 8601-1:2019 형식에 대 한 지원

<xref:System.DateTime> <xref:System.Text.Json.Utf8JsonReader> ,,및<xref:System.Text.Json.JsonElement> 형식은 ISO 8601-1:2019 형식의 확장 프로필 ( <xref:System.DateTimeOffset> 예: 2019-07-26t16)에 따라 구문 분석 되 고텍스트표현을작성합니다.<xref:System.Text.Json.Utf8JsonWriter> <xref:System.Text.Json.JsonSerializer> : 59:57-05:00.

<xref:System.DateTime>다음 <xref:System.DateTimeOffset> 을 사용 하 여 <xref:System.Text.Json.JsonSerializer>및 데이터를 직렬화 할 수 있습니다.

[!code-csharp[example-serializing-with-jsonserializer](~/samples/snippets/standard/datetime/json/csharp/serializing-with-jsonserializer/Program.cs)]

다음을 사용 하 여 <xref:System.Text.Json.JsonSerializer>deserialize 할 수도 있습니다.

[!code-csharp[example-deserializing-with-jsonserializer-valid](~/samples/snippets/standard/datetime/json/csharp/deserializing-with-jsonserializer-valid/Program.cs)]

기본 옵션을 사용 하 <xref:System.DateTime> 여 <xref:System.DateTimeOffset> 입력 및 텍스트 표현은 확장 된 ISO 8601-1:2019 프로필을 준수 해야 합니다.
프로필에 맞지 않는 표현을 deserialize 하려고 하면이 <xref:System.Text.Json.JsonSerializer> <xref:System.Text.Json.JsonException>throw 됩니다.

[!code-csharp[example-deserializing-with-jsonserializer-error](~/samples/snippets/standard/datetime/json/csharp/deserializing-with-jsonserializer-error/Program.cs)]

는 <xref:System.Text.Json.JsonDocument> <xref:System.DateTime> 및 표현을<xref:System.DateTimeOffset> 포함 하 여 JSON 페이로드의 내용에 대 한 구조적 액세스를 제공 합니다. 아래 예제에서는 온도 수집이 지정 된 경우 월요일의 평균 온도를 계산할 수 있는 방법을 보여 줍니다.

[!code-csharp[example-computing-with-jsondocument-valid](~/samples/snippets/standard/datetime/json/csharp/computing-with-jsondocument-valid/Program.cs)]

비준수 <xref:System.DateTime> 표현이 포함 된 페이로드에 대해 평균 온도를 계산 하려고 시도 하면 <xref:System.Text.Json.JsonDocument> 이 throw <xref:System.FormatException>됩니다.

[!code-csharp[example-computing-with-jsondocument-error](~/samples/snippets/standard/datetime/json/csharp/computing-with-jsondocument-error/Program.cs)]

낮은 수준 <xref:System.Text.Json.Utf8JsonWriter> 에서 및 <xref:System.DateTime> <xref:System.DateTimeOffset> 데이터를 기록 합니다.

[!code-csharp[example-writing-with-utf8jsonwriter](~/samples/snippets/standard/datetime/json/csharp/writing-with-utf8jsonwriter/Program.cs)]

<xref:System.Text.Json.Utf8JsonReader>구문 <xref:System.DateTime> 분석 <xref:System.DateTimeOffset> 및 데이터:

[!code-csharp[example-reading-with-utf8jsonreader-valid](~/samples/snippets/standard/datetime/json/csharp/reading-with-utf8jsonreader-valid/Program.cs)]

호환 되지 않는 형식을로 <xref:System.Text.Json.Utf8JsonReader> 읽으려고 하면이 <xref:System.FormatException>throw 됩니다.

[!code-csharp[example-reading-with-utf8jsonreader-error](~/samples/snippets/standard/datetime/json/csharp/reading-with-utf8jsonreader-error/Program.cs)]

## <a name="custom-support-for-xrefsystemdatetime-and-xrefsystemdatetimeoffset"></a>및에 대 <xref:System.DateTime> 한 사용자 지정 지원<xref:System.DateTimeOffset>

### <a name="when-using-xrefsystemtextjsonjsonserializer"></a>사용 하는 경우<xref:System.Text.Json.JsonSerializer>

Serializer에서 사용자 지정 구문 분석 또는 서식 지정을 수행 하려는 경우 [사용자 지정 변환기](xref:System.Text.Json.Serialization.JsonConverter%601)를 구현할 수 있습니다.
다음은 몇 가지 예입니다.

#### <a name="using-datetimeoffsetparse-and-datetimeoffsettostring"></a>및 `DateTime(Offset).Parse` 사용`DateTime(Offset).ToString`

입력 <xref:System.DateTime> `DateTime(Offset).Parse` 또는 <xref:System.DateTimeOffset> 텍스트 표현의 형식을 확인할 수 없는 경우 변환기의 읽기 논리에서 메서드를 사용할 수 있습니다. 이렇게 하면를 사용할 수 있습니다. Iso 8601 문자열 및 확장 된 iso <xref:System.DateTime> 8601-1:2019 <xref:System.DateTimeOffset> 프로필을 준수 하지 않는 iso 8601 형식을 비롯 한 다양 한 텍스트 형식 구문 분석을 위한 광범위 한 기능을 제공 합니다. 이 방법은 serializer의 기본 구현을 사용 하는 것 보다 성능이 훨씬 낮습니다.

Serialize를 위해 변환기 쓰기 논리에서 `DateTime(Offset).ToString` 메서드를 사용할 수 있습니다. <xref:System.DateTime> 이를 통해 [표준 날짜 및 시간 형식](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings)및 [사용자 지정 날짜 및 시간 형식을](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings)사용 하 여 및 <xref:System.DateTimeOffset> 값을 작성할 수 있습니다.
이는 serializer의 기본 구현을 사용 하는 것 보다 성능이 훨씬 낮습니다.

[!code-csharp[example-showing-datetime-parse](~/samples/snippets/standard/datetime/json/csharp/datetime-converter-examples/example1/Program.cs)]

> [!NOTE]
> 을 구현 <xref:System.Text.Json.Serialization.JsonConverter%601>하 고 `T` 가 <xref:System.DateTime>인 경우 `typeToConvert` 매개 변수는 항상 `typeof(DateTime)`입니다.
매개 변수는 다형성 사례를 처리 하 고 제네릭을 사용 하 여 성능을 `typeof(T)` 향상 시킬 때 유용 합니다.

#### <a name="using-xrefsystembufferstextutf8parser-and-xrefsystembufferstextutf8formatter"></a>및 <xref:System.Buffers.Text.Utf8Parser> 사용<xref:System.Buffers.Text.Utf8Formatter>

입력 <xref:System.DateTime> 또는<xref:System.DateTimeOffset> 텍스트 표현이 "R", "l", "O" 또는 "G" [표준 날짜 및 시간 형식 문자열](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings)중 하나를 준수 하는 경우 변환기 논리에서 빠른 utf-8 기반 구문 분석 및 형식 지정 메서드를 사용할 수 있습니다. 다음 형식 중 하나에 따라 씁니다. 이는 및 `DateTime(Offset).ToString`을 사용 하 `DateTime(Offset).Parse` 는 것 보다 훨씬 빠릅니다.

이 예제에서는 ["R" 표준 형식](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings#the-rfc1123-r-r-format-specifier)에 따라 <xref:System.DateTime> 값을 serialize 및 deserialize 하는 사용자 지정 변환기를 보여 줍니다.

[!code-csharp[example-showing-utf8-parser-and-formatter](~/samples/snippets/standard/datetime/json/csharp/datetime-converter-examples/example2/Program.cs)]

> [!NOTE]
> "R" 표준 형식은 항상 29 자 길이입니다.

#### <a name="using-datetimeoffsetparse-as-a-fallback-to-the-serializers-native-parsing"></a>Serializer `DateTime(Offset).Parse` 의 네이티브 구문 분석에 대 한 대체로를 사용 합니다.

일반적으로 입력 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 데이터가 확장 된 ISO 8601-1:2019 프로필을 따르도록 하려면 serializer의 네이티브 구문 분석 논리를 사용할 수 있습니다. 경우에만 대체 메커니즘을 구현할 수도 있습니다.
이 예제에서는를 사용 하 여 <xref:System.DateTime> <xref:System.Text.Json.Utf8JsonReader.TryGetDateTime(System.DateTime@)>텍스트 표현의 구문 분석에 실패 한 후 변환기에서를 사용 하 여 <xref:System.DateTime.Parse(System.String)>데이터를 성공적으로 구문 분석 함을 보여 줍니다.

[!code-csharp[example-showing-datetime-parse-as-fallback](~/samples/snippets/standard/datetime/json/csharp/datetime-converter-examples/example3/Program.cs)]

### <a name="when-writing-with-xrefsystemtextjsonutf8jsonwriter"></a>을 사용 하 여 작성 하는 경우<xref:System.Text.Json.Utf8JsonWriter>

<xref:System.DateTime> 를 사용 하 여 `ReadOnlySpan<Byte>` `ReadOnlySpan<Char>` <xref:System.String> <xref:System.DateTimeOffset> <xref:System.Text.Json.Utf8JsonWriter>사용자 지정 또는 텍스트 표현을 작성 하려는 경우 사용자 지정 표현의 형식을,, 또는 <xref:System.Text.Json.JsonEncodedText>로 지정 하 고 해당 하는 [Utf8JsonWriter WriteStringValue](https://docs.microsoft.com/dotnet/api/system.text.json.utf8jsonwriter.writestringvalue?view=netcore-3.0) 또는 [Utf8JsonWriter](https://docs.microsoft.com/dotnet/api/system.text.json.utf8jsonwriter.writestring?view=netcore-3.0) .

다음 예제에서는 <xref:System.DateTime> <xref:System.DateTime.ToString(System.String,System.IFormatProvider)>를사용하 여 사용자 지정 형식을 만든 다음 메서드를사용하여작성하는방법을보여줍니다.<xref:System.Text.Json.Utf8JsonWriter.WriteStringValue(System.String)>

[!code-csharp[example-custom-writing-with-utf8jsonwriter](~/samples/snippets/standard/datetime/json/csharp/custom-writing-with-utf8jsonwriter/Program.cs)]

### <a name="when-reading-with-xrefsystemtextjsonutf8jsonreader"></a>읽을 때<xref:System.Text.Json.Utf8JsonReader>

를 사용 하 여 사용자 지정 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 텍스트 표현을 <xref:System.Text.Json.Utf8JsonReader>읽으려면를 <xref:System.String> 사용 <xref:System.Text.Json.Utf8JsonReader.GetString>하 여 현재 JSON 토큰의 값을 가져온 다음 사용자 지정 논리를 사용 하 여 값을 구문 분석할 수 있습니다.

다음 예제에서는를 사용 <xref:System.DateTimeOffset> <xref:System.Text.Json.Utf8JsonReader.GetString>하 여 사용자 지정 텍스트 표현을 검색 한 다음를 사용 하 <xref:System.DateTimeOffset.ParseExact(System.String,System.String,System.IFormatProvider)>여 구문 분석 하는 방법을 보여 줍니다.

[!code-csharp[example-custom-reading-with-utf8jsonreader](~/samples/snippets/standard/datetime/json/csharp/custom-reading-with-utf8jsonreader/Program.cs)]

## <a name="the-extended-iso-8601-12019-profile-in-systemtextjson"></a>System.object의 확장 된 ISO 8601-1:2019 프로필

### <a name="date-and-time-components"></a>날짜 및 시간 구성 요소

에 <xref:System.Text.Json> 구현 된 확장 ISO 8601-1:2019 프로필은 날짜 및 시간 표현에 대해 다음과 같은 구성 요소를 정의 합니다. 이러한 구성 요소는 구문 분석 및 형식 지정 <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 표현을 할 때 지원 되는 다양 한 수준의 세분성을 정의 하는 데 사용 됩니다.

| 구성 요소       | 서식                      | 설명                                                                     |
|-----------------|-----------------------------|---------------------------------------------------------------------------------|
| Year            | "yyyy"                      | 0001-9999                                                                       |
| 월           | "MM"                        | 01-12                                                                           |
| Day             | "dd"                        | 월/연도를 기준으로 하는 01-28, 01-29, 01-30, 01-31                                  |
| Hour            | "HH"                        | 00-23                                                                           |
| Minute          | "mm"                        | 00-59                                                                           |
| Second          | "ss"                        | 00-59                                                                           |
| 초 분수 | "FFFFFFF"                   | 최소 1 자리 숫자, 최대 16 자리                                      |
| 시간 오프셋     | "K"                         | "Z" 또는 "(' + '/'-') HH ': ' mm"                                                |
| 부분 시간    | "HH ': ' mm ': ' ss [FFFFFFF]"     | UTC 오프셋 정보가 없는 시간                                             |
| 전체 날짜       | "yyyy'-'mm'-'dd't'hh-'MM'-'dd"            | 달력 날짜                                                                   |
| 전체 시간       | "' Partial time'K"           | 현지 시간과 UTC 사이의 시간 오프셋을 사용한 하루 또는 현지 시간 (UTC) |
| 날짜 시간       | "' 전체 날짜 ' ' ' ' 전체 시간 '" | 달력 날짜 및 시간 (예: 2019-07-26T16:59:57-05:00)                   |

### <a name="support-for-parsing"></a>구문 분석 지원

구문 분석에 대해 정의 되는 세분성 수준은 다음과 같습니다.

1. ' 전체 날짜 '
    1. "yyyy'-'mm'-'dd't'hh-'MM'-'dd"

2. "' 전체 날짜 ' ' ' ' ' 시간 ' ': ' ' Minute '"
    1. "yyyy'-'mm'-'dd't'hh-'MM'-' m ': ' MM '

3. "' 전체 날짜 ' ' ' ' ' 부분 시간 '"
    1. "yyyy'-'mm'-'dd't'hh-'MM'-% Ddu: ' MM ': ' ss ' ([정렬 가능한 (" s ") 서식 지정자](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings#the-sortable-s-format-specifier))
    2. "yyyy'-'mm'-'dd't'hh-'MM'-% n이 (가): ' MM ': ' ss '. ' FFFFFFF

4. "' 전체 날짜 ' ' ' ' 시간 시간 ' ': ' ' Minute ' ' 시간 오프셋 '"
    1. "yyyy'-'mm'-'dd't'hh-'MM'-% n n e t ': ' mmZ '
    2. "yyyy'-'mm'-'dd't'hh-'MM'-% Ddn ': ' mm (' + '/'-') HH ': ' mm"

5. ' 날짜 시간 '
    1. "yyyy'-'mm'-'dd't'hh-'MM'-% n이 (가): ' MM ': ' ssZ '
    2. "yyyy'-'mm'-'dd't'hh-'MM'-% n이 (가): ' MM ': ' ss '. ' FFFFFFFZ "
    3. "yyyy'-'mm'-'dd't'hh-'MM'-% n n e t ': ' mm ': ' ss (' + '/'-') HH ': ' mm '
    4. "yyyy'-'mm'-'dd't'hh-'MM'-% n이 (가): ' MM ': ' ss '. ' FFFFFFF (' + '/'-') HH ': ' mm '

초에 소수 자릿수가 있으면 숫자가 하나 이상 있어야 합니다. `2019-07-26T00:00:00.` 허용 되지 않습니다.
최대 16 개의 소수 자릿수가 허용 되지만 처음 7 개만 구문 분석 됩니다. 그 외의 모든 항목은 0으로 간주 됩니다.
예 `2019-07-26T00:00:00.1234567890` 를 들어는 `2019-07-26T00:00:00.1234567`인 것 처럼 구문 분석 됩니다.
이는이 해상도로 제한 되 <xref:System.DateTime> 는 구현과의 호환성을 유지 하기 위한 것입니다.

윤 초는 지원 되지 않습니다.

### <a name="support-for-formatting"></a>서식 지정 지원

서식 지정에 대해 정의 된 세분성 수준은 다음과 같습니다.

1. "' 전체 날짜 ' ' ' ' ' 부분 시간 '"
    1. "yyyy'-'mm'-'dd't'hh-'MM'-% Ddu: ' MM ': ' ss ' ([정렬 가능한 (" s ") 서식 지정자](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings#the-sortable-s-format-specifier))

        오프셋 정보 없이 소수 <xref:System.DateTime> 자릿수 초 없이의 형식을 지정 하는 데 사용 됩니다.

    2. "yyyy'-'mm'-'dd't'hh-'MM'-% n이 (가): ' MM ': ' ss '. ' FFFFFFF

        오프셋 정보 없이 소수 <xref:System.DateTime> 자릿수 초를 사용 하 여의 형식을 지정 하는 데 사용 됩니다.

2. ' 날짜 시간 '
    1. "yyyy'-'mm'-'dd't'hh-'MM'-% n이 (가): ' MM ': ' ssZ '

        소수 자릿수 초를 <xref:System.DateTime> 제외 <xref:System.DateTimeOffset> 하 고 UTC 오프셋을 사용 하 여의 형식을 지정 하는 데 사용 됩니다.

    2. "yyyy'-'mm'-'dd't'hh-'MM'-% n이 (가): ' MM ': ' ss '. ' FFFFFFFZ "

        UTC 오프셋을 사용 <xref:System.DateTime> 하 <xref:System.DateTimeOffset> 여 또는 소수 자릿수 초를 지정 하는 데 사용 됩니다.

    3. "yyyy'-'mm'-'dd't'hh-'MM'-% n n e t ': ' mm ': ' ss (' + '/'-') HH ': ' mm '

        소수 자릿수 초를 <xref:System.DateTime> 제외 <xref:System.DateTimeOffset> 하 고 로컬 오프셋을 사용 하 여의 형식을 지정 하는 데 사용 됩니다.

    4. "yyyy'-'mm'-'dd't'hh-'MM'-% n이 (가): ' MM ': ' ss '. ' FFFFFFF (' + '/'-') HH ': ' mm '

        현지 오프셋으로 또는 <xref:System.DateTime> <xref:System.DateTimeOffset> 소수 자릿수 초를 사용 하 여의 형식을 지정 하는 데 사용 됩니다.

있는 경우 최대 7 개의 소수 자릿수가 기록 됩니다. 이는이 해상도로 제한 되는 구현과일치합니다.<xref:System.DateTime>
