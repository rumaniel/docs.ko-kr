---
title: -.Net을 사용 하 여 C# JSON을 serialize 및 deserialize 하는 방법
author: tdykstra
ms.author: tdykstra
ms.date: 09/16/2019
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 22c2fd5fc5eaf7a5dc9b71a7335b0b844fa92b51
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291612"
---
# <a name="how-to-serialize-and-deserialize-json-in-net"></a>.NET에서 JSON을 serialize 및 deserialize 하는 방법

> [!IMPORTANT]
> JSON serialization 설명서는 생성 중입니다. 이 문서에서는 모든 시나리오를 다루지 않습니다. 자세한 내용은 GitHub의 dotnet/corefx 리포지토리, 특히 [json 기능-doc](https://github.com/dotnet/corefx/labels/json-functionality-doc)에서 발생 하는 system.servicemodel [문제](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-System.Text.Json) 를 검사 합니다.

이 문서에서는 <xref:System.Text.Json> 네임 스페이스를 사용 하 여 JSON (JavaScript Object Notation)으로 serialize 및 deserialize 하는 방법을 보여 줍니다. 지침 및 샘플 코드는 [ASP.NET Core](/aspnet/core/)와 같은 프레임 워크가 아닌 라이브러리를 직접 사용 합니다.

## <a name="namespaces"></a>네임스페이스

@No__t-0 네임 스페이스는 모든 진입점과 기본 유형을 포함 합니다. @No__t-0 네임 스페이스에는 serialization 및 deserialization과 관련 된 고급 시나리오 및 사용자 지정을 위한 특성 및 Api가 포함 되어 있습니다. 따라서이 문서에 표시 된 코드 예제에는 다음 `using` 지시문 중 하나 또는 둘 다가 필요 합니다.

```csharp
using System.Text.Json;
using System.Text.Json.Serialization;
```

@No__t-0 네임 스페이스의 특성은 현재 `System.Text.Json`에서 지원 되지 않습니다.

## <a name="how-to-write-net-objects-to-json-serialize"></a>JSON에 .NET 개체를 작성 하는 방법 (직렬화)

JSON을 문자열에 쓰려면 <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> 메서드를 호출 합니다. 다음 예제에서는 제네릭 형식 매개 변수를 포함 하는 오버 로드를 사용 합니다.

```csharp
WeatherForecast weatherForecast;
//...
string json = JsonSerializer.Serialize<WeatherForecast>(weatherForecast);
```

제네릭 형식 매개 변수를 생략 하 고 제네릭 형식 유추를 대신 사용할 수 있습니다.

```csharp
WeatherForecast weatherForecast;
//...
string json = JsonSerializer.Serialize(weatherForecast);
```

다음은 컬렉션 및 중첩 클래스를 포함 하는 serialize 되는 예제 형식입니다.

```csharp
public class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    public IList<DateTimeOffset> DatesAvailable { get; set;}
    public Dictionary<string, HighLowTemperatures> TemperatureRanges { get; set; }
    public string [] SummaryWords { get; set; }
}

public class HighLowTemperatures
{
    public Temperature High { get; set; }
    public Temperature Low { get; set; }
}

public class Temperature
{
    public int DegreesCelsius { get; set; }
}
```

JSON 출력은 기본적으로 축소 되어 있습니다. 

```json
{"Date":"2019-08-01T00:00:00-07:00","TemperatureC":25,"Summary":"Hot","DatesAvailable":["2019-08-01T00:00:00-07:00","2019-08-02T00:00:00-07:00"],"TemperatureRanges":{"Cold":{"High":{"DegreesCelsius":20},"Low":{"DegreesCelsius":-10}},"Hot":{"High":{"DegreesCelsius":60},"Low":{"DegreesCelsius":20}}},"SummaryWords":["Cool","Windy","Humid"]}
```

다음 예제에서는 동일한 JSON (공백 및 들여쓰기를 사용 하 여 잘 인쇄 됨)을 보여 줍니다.

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "TemperatureRanges": {
    "Cold": {
      "High": {
        "DegreesCelsius": 20
      },
      "Low": {
        "DegreesCelsius": -10
      }
    },
    "Hot": {
      "High": {
        "DegreesCelsius": 60
      },
      "Low": {
        "DegreesCelsius": 20
      }
    }
  },
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

@No__t-0의 오버 로드를 사용 하면 <xref:System.IO.Stream>로 serialize 할 수 있습니다. 비동기 버전의 `Stream` 오버 로드를 사용할 수 있습니다.

### <a name="serialize-to-utf-8"></a>U t f-8로 직렬화

U t f-8로 serialize 하려면 <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> 메서드를 호출 합니다.

```csharp
byte[] utf8Json = JsonSerializer.SerializeToUtf8Bytes<WeatherForecast>(weatherForecast);
```

또는 <xref:System.Text.Json.Utf8JsonWriter>을 사용 하는 @no__t 0 오버 로드를 사용할 수 있습니다.

U t f-8로 serialize 하는 것은 문자열 기반 메서드를 사용 하는 것 보다 약 5-10% 더 빠릅니다. 차이점은 바이트 (u t f-8)를 문자열 (UTF-16)로 변환할 필요가 없기 때문입니다.

## <a name="serialization-behavior"></a>Serialization 동작

* 기본적으로 모든 public 속성이 직렬화 됩니다. [제외할 속성을 지정할](#exclude-properties)수 있습니다.
* [기본 인코더](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) 는 ascii가 아닌 문자, ascii 범위 내의 HTML 구분 문자 및 [JSON 사양](https://tools.ietf.org/html/rfc8259#section-7)에 따라 이스케이프 되어야 하는 문자를 이스케이프 합니다.
* 기본적으로 JSON은 축소 되어 있습니다. [JSON을 잘 인쇄할](#serialize-to-formatted-json)수 있습니다.
* 기본적으로 JSON 이름의 대/소문자는 .NET 이름과 일치 합니다. [JSON 이름 대/소문자를 사용자 지정할](#customize-json-names)수 있습니다.
* 순환 참조가 감지 되 고 예외가 throw 됩니다. 자세한 내용은 GitHub의 dotnet/corefx 리포지토리에서 [순환 참조에 대 한 문제](https://github.com/dotnet/corefx/issues/38579) 를 참조 하세요.
* 현재는 필드가 제외 됩니다.

지원 되는 형식은 다음과 같습니다.

* 숫자 형식, 문자열, 부울 등 JavaScript 기본 형식에 매핑되는 .NET 기본 형식입니다.
* 사용자 정의 [일반 이전 CLR 개체 (POCOs)](https://stackoverflow.com/questions/250001/poco-definition).
* 1 차원 및 가변 배열 (`ArrayName[][]`)
* `TValue` @no__t `object`, `JsonElement` 또는 POCO입니다.
* 다음 네임 스페이스의 컬렉션입니다. 자세한 내용은 GitHub의 dotnet/corefx 리포지토리에서 [컬렉션 지원에 대 한 문제](https://github.com/dotnet/corefx/issues/36643) 를 참조 하세요.
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>

## <a name="how-to-read-json-into-net-objects-deserialize"></a>JSON을 .NET 개체로 읽는 방법 (deserialize)

문자열에서 deserialize 하려면 다음 예제와 같이 <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> 메서드를 호출 합니다.

```csharp
string json = ... ;

var weatherForecast = JsonSerializer.Deserialize<WeatherForecast>(json);
```

예제는 [직렬화](#how-to-write-net-objects-to-json-serialize) 섹션을 참조 하세요. JSON 및 .NET 개체는 동일 하지만 방향이 반대입니다.

@No__t-0의 오버 로드를 사용 하면 `Stream`에서 deserialize 할 수 있습니다.  비동기 버전의 `Stream` 오버 로드를 사용할 수 있습니다.

### <a name="deserialize-from-utf-8"></a>U t f-8에서 Deserialize

U t f-8에서 deserialize 하려면 다음 예제와 같이 `Utf8JsonReader` 또는 `ReadOnlySpan<byte>`를 사용 하는 <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> 오버 로드를 호출 합니다.

```csharp
byte[] utf8Json;
//...
var readOnlySpan = new ReadOnlySpan<byte>(utf8Json);
weatherForecast = JsonSerializer.Deserialize<WeatherForecastMin>(readOnlySpan);
```

```csharp
byte[] utf8Json;
//...
var utf8Reader = new Utf8JsonReader(utf8Json);
weatherForecast = JsonSerializer.Deserialize<WeatherForecastMin>(ref utf8Reader);
```

## <a name="deserialization-behavior"></a>Deserialization 동작

* 기본적으로 속성 이름 일치는 대/소문자를 구분 합니다. [대/소문자](#case-insensitive-property-matching)를 구분 하지 않도록 지정할 수 있습니다.
* JSON에 읽기 전용 속성에 대 한 값이 포함 된 경우에는이 값이 무시 되 고 예외가 throw 되지 않습니다.
* 매개 변수가 없는 생성자가 없는 참조 형식으로의 Deserialization은 지원 되지 않습니다.
* 변경할 수 없는 개체 또는 읽기 전용 속성에 대 한 Deserialization은 지원 되지 않습니다. 자세한 내용은 github의 dotnet/corefx 리포지토리에서 [변경 불가능 한 개체 지원](https://github.com/dotnet/corefx/issues/38569) 및 [읽기 전용 속성 지원 문제](https://github.com/dotnet/corefx/issues/38163) 에 대 한 github 문제를 참조 하세요.
* 기본적으로 열거형은 숫자로 지원 됩니다.
* 필드는 지원 되지 않습니다.
* 기본적으로 JSON의 주석이 나 후행 쉼표는 예외를 throw 합니다. 필요한 경우 [주석과 후행 쉼표를 허용할](#allow-comments-and-trailing-commas) 수 있습니다.
* [기본 최대 깊이](xref:System.Text.Json.JsonReaderOptions.MaxDepth) 는 64입니다.

## <a name="serialize-to-formatted-json"></a>형식이 지정 된 JSON으로 직렬화

JSON 출력을 잘 인쇄 하려면 <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType>을 `true`로 설정 합니다.

```csharp
var options = new JsonSerializerOptions
{
    WriteIndented = true,
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

직렬화 및 JSON 출력의 예제 유형은 다음과 같습니다.

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
}
```

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot"
}
```

## <a name="allow-comments-and-trailing-commas"></a>주석과 후행 쉼표 허용

JSON에서는 기본적으로 주석과 후행 쉼표를 사용할 수 없습니다. JSON에서 주석을 허용 하려면 <xref:System.Text.Json.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> 속성을 `JsonCommentHandling.Skip`로 설정 합니다. 후행 쉼표를 허용 하려면 <xref:System.Text.Json.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> 속성을 `true`로 설정 합니다. 다음 예제에서는 두 가지를 모두 허용 하는 방법을 보여 줍니다.

```csharp
var options = new JsonSerializerOptions
{
    ReadCommentHandling = JsonCommentHandling.Skip,
    AllowTrailingCommas = true
};
var weatherForecast = JsonSerializer.Deserialize<WeatherForecast>(json, options);
```

다음은 주석과 후행 쉼표를 사용 하는 JSON 예제입니다.

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25, // Fahrenheit 77
  "Summary": "Hot", /* Zharko */
}
```

## <a name="customize-json-names"></a>JSON 이름 사용자 지정

기본적으로 속성 이름 및 사전 키는 대/소문자를 포함 하 여 JSON 출력에서 변경 되지 않습니다. 이 섹션에서는 다음을 수행 하는 방법을 설명 합니다.

* 개별 속성 이름 사용자 지정
* 모든 속성 이름을 카멜식 대/소문자로 변환
* 사용자 지정 속성 명명 정책 구현
* 사전 키를 카멜식 대/소문자로 변환

현재는 열거형을 카멜식 대/소문자로 자동 변환 하는 기능이 지원 되지 않습니다. 자세한 내용은 GitHub의 dotnet/corefx 리포지토리에서 [카멜식 대/소문자 지원 열거 문제](https://github.com/dotnet/corefx/issues/37725) 를 참조 하세요.

### <a name="customize-individual-property-names"></a>개별 속성 이름 사용자 지정

개별 속성의 이름을 설정 하려면 [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) 특성을 사용 합니다.

직렬화 및 결과 JSON의 예는 다음과 같습니다.

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonPropertyName("Wind")]
    public int WindSpeed { get; set; }
}
```

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
  "Wind": 35
}
```

이 특성에 의해 설정 된 속성 이름:

* Serialization 및 deserialization을 위해 양방향으로 적용 됩니다.
* 속성 명명 정책 보다 우선 합니다.

### <a name="use-camel-case-for-all-json-property-names"></a>모든 JSON 속성 이름에 카멜식 대/소문자 사용

모든 JSON 속성 이름에 카멜식 대/소문자를 사용 하려면 다음 예제와 같이 <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType>을 `JsonNamingPolicy.CamelCase`로 설정 합니다.

```csharp
var options = new JsonSerializerOptions
{
    PropertyNamingPolicy = JsonNamingPolicy.CamelCase
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

직렬화 및 JSON 출력에 대 한 예제 클래스는 다음과 같습니다.

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonPropertyName("Wind")]
    public int WindSpeed { get; set; }
}
```

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureC": 25,
  "summary": "Hot",
  "Wind": 35
}
```

카멜식 대/소문자 속성 명명 정책:

* Serialization 및 deserialization에 적용 됩니다.
* @No__t-0 특성에 의해 재정의 됩니다.

### <a name="use-a-custom-json-property-naming-policy"></a>사용자 지정 JSON 속성 명명 정책 사용

사용자 지정 JSON 속성 명명 정책을 사용 하려면 다음 예제와 같이 <xref:System.Text.Json.JsonNamingPolicy>에서 파생 되는 클래스를 만들고 <xref:System.Text.Json.JsonNamingPolicy.ConvertName%2A> 메서드를 재정의 합니다.

```csharp
class UpperCaseNamingPolicy : JsonNamingPolicy
{
    public override string ConvertName(string name)
    {
        return name.ToUpper();
    }
}
```

그런 다음 <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> 속성을 명명 정책 클래스의 인스턴스로 설정 합니다.

```csharp
var options = new JsonSerializerOptions
{
    PropertyNamingPolicy = new UpperCaseNamingPolicy()
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

직렬화 및 JSON 출력에 대 한 예제 클래스는 다음과 같습니다.

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonPropertyName("Wind")]
    public int WindSpeed { get; set; }
}
```

```json
{
  "DATE": "2019-08-01T00:00:00-07:00",
  "TEMPERATUREC": 25,
  "SUMMARY": "Hot",
  "Wind": 35
}
```

JSON 속성 명명 정책:

* Serialization 및 deserialization에 적용 됩니다.
* @No__t-0 특성에 의해 재정의 됩니다.

### <a name="camel-case-dictionary-keys"></a>카멜식 대/소문자 사전 키

Serialize 할 개체의 속성 형식이 `Dictionary<string,TValue>` 인 경우 `string` 키를 카멜식 대/소문자로 변환할 수 있습니다. 이렇게 하려면 다음 예제와 같이 <xref:System.Text.Json.JsonSerializerOptions.DictionaryKeyPolicy>을 `JsonNamingPolicy.CamelCase`로 설정 합니다.

```csharp
var options = new JsonSerializerOptions
{
    DictionaryKeyPolicy = JsonNamingPolicy.CamelCase
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

직렬화 및 JSON 출력에 대 한 예제 개체는 다음과 같습니다.

|속성 |값  |
|---------|---------|
| Date    | 오전 8/1/2019 12:00:00-07:00|
| TemperatureC| 25 |
| 요약| 핫스폿을|
| TemperatureRanges | 콜드, 20<br>핫, 40|

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "cold": 20,
    "hot": 40
  }
}
```

카멜식 대/소문자 명명 정책은 serialization에만 적용 됩니다.

## <a name="exclude-properties"></a>제외 속성

기본적으로 모든 public 속성이 직렬화 됩니다. JSON 출력에 표시 하지 않으려는 경우 몇 가지 옵션이 있습니다. 이 섹션에서는 다음을 제외 하는 방법을 설명 합니다.

* 개별 속성
* 모든 읽기 전용 속성
* 모든 null 값 속성 

### <a name="exclude-individual-properties"></a>개별 속성 제외

개별 속성을 무시 하려면 [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) 특성을 사용 합니다.

다음은 serialize 및 JSON 출력에 대 한 예제 형식입니다.

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonIgnore]
    public int WindSpeed { get; set; }
}
```

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot"
}
```

### <a name="exclude-all-read-only-properties"></a>모든 읽기 전용 속성을 제외 합니다.

모든 읽기 전용 속성을 제외 하려면 다음 예제와 같이 <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType>을 `true`로 설정 합니다.

```csharp
var options = new JsonSerializerOptions
{
    IgnoreReadOnlyProperties = true
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

다음은 serialize 및 JSON 출력에 대 한 예제 형식입니다.

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    public int WindSpeed { get; private set; }
}
```

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
}
```

이 옵션은 serialization에만 적용 됩니다. Deserialization을 수행 하는 동안 읽기 전용 속성은 기본적으로 무시 됩니다. 공용 setter가 아닌 공용 getter가 포함 된 속성은 읽기 전용입니다.

### <a name="exclude-all-null-value-properties"></a>모든 null 값 속성 제외

모든 null 값 속성을 제외 하려면 다음 예제와 같이 <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues> 속성을 `true`로 설정 합니다.

```csharp
var options = new JsonSerializerOptions
{
    IgnoreNullValues = true
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

직렬화 및 JSON 출력에 대 한 예제 개체는 다음과 같습니다.

|속성 |값  |
|---------|---------|
| Date    | 오전 8/1/2019 12:00:00-07:00|
| TemperatureC| 25 |
| 요약| null|

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25
}
```

이 설정은 serialization 및 deserialization에 적용 됩니다. Deserialization을 수행 하는 동안 JSON의 null 값은 유효한 경우에만 무시 됩니다. Null을 허용 하지 않는 값 형식에 대 한 Null 값은 예외를 발생 시킵니다. 자세한 내용은 GitHub의 dotnet/corefx 리포지토리에서 [nullable이 아닌 값 형식에 대 한 문제](https://github.com/dotnet/corefx/issues/40922) 를 참조 하세요.

## <a name="case-insensitive-property-matching"></a>대/소문자를 구분 하지 않는 속성 일치

기본적으로 deserialization은 JSON과 대상 개체 속성 간에 일치 하는 대/소문자를 구분 하는 속성 이름을 찾습니다. 이 동작을 변경 하려면 <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType>을 `true`로 설정 합니다.

```csharp
var options = new JsonSerializerOptions
{
    PropertyNameCaseInsensitive = true,
};
var weatherForecast = JsonSerializer.Deserialize<WeatherForecast>(weatherForecast, options);
```

카멜식 대/소문자 속성 이름을 사용 하는 JSON 예제는 다음과 같습니다. 파스칼식 대/소문자 속성 이름을 포함 하는 다음 형식으로 deserialize 할 수 있습니다.

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureC": 25,
  "summary": "Hot",
}
```

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
}
```

## <a name="include-properties-of-derived-classes"></a>파생 클래스의 속성 포함

컴파일 시간에 serialize 할 형식을 지정 하는 경우 다형성 serialization이 지원 되지 않습니다. 예를 들어 `WeatherForecast` 클래스와 파생 클래스 `WeatherForecastWithWind` 인 경우를 가정 합니다.

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
}
class WeatherForecastWithWind : WeatherForecast
{
    public int WindSpeed { get; set; }
}
```

컴파일 시간에 `Serialize` 메서드를 통해 전달 되거나 유추 된 형식이 `WeatherForecast` 인 경우

```csharp
string json = JsonSerializer.Serialize<WeatherForecast>(weatherForecast);
```

```csharp
WeatherForecast weatherForecast;
//...
json = JsonSerializer.Serialize(weatherForecast);
```

이 시나리오에서는 `weatherForecast` 개체가 실제로 `WeatherForecastWithWind` 개체인 경우에도 `WindSpeed` 속성이 serialize 되지 않습니다. 기본 클래스 속성만 직렬화 됩니다.

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot"
}
```

이 동작은 파생 된 런타임 생성 형식에서 실수로 데이터가 노출 되는 것을 방지 하는 데 사용 됩니다.

파생 형식의 속성을 serialize 하려면 다음 방법 중 하나를 사용 합니다.

* 런타임에 형식을 지정할 수 있는 <xref:System.Text.Json.JsonSerializer.Serialize%2A>의 오버 로드를 호출 합니다.

  ```csharp
  json = JsonSerializer.Serialize(weatherForecast, weatherForecast.GetType());
  ```

* @No__t-0으로 serialize 될 개체를 선언 합니다.

  ```csharp
  json = JsonSerializer.Serialize<object>(weatherForecast);
  ```

위의 예제 시나리오에서 두 가지 방법 모두 `WindSpeed` 속성이 JSON 출력에 포함 됩니다.

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
  "WindSpeed": 35
}
```

## <a name="handle-overflow-json"></a>오버플로 JSON 처리

Deserialize 하는 동안 대상 형식의 속성으로 표시 되지 않는 데이터를 JSON에 받을 수 있습니다. 예를 들어 대상 형식이 다음과 같다고 가정 합니다.

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
}
```

Deserialize 할 JSON은 다음과 같습니다.

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "temperatureC": 25,
  "Summary": "Hot",
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

표시 된 형식에 표시 된 JSON을 deserialize 하는 경우 `DatesAvailable` 및 `SummaryWords` 속성은 이동 하지 않으며 손실 됩니다. 이러한 속성과 같은 추가 데이터를 캡처하려면 [JsonExtensionData](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) 특성을 `Dictionary<string,object>` 또는 `Dictionary<string,JsonElement>` 형식의 속성에 적용 합니다.

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonExtensionData]
    public Dictionary<string, object> ExtensionData { get; set; }
}
```

앞에서 설명한 JSON을이 샘플 형식으로 deserialize 하는 경우 추가 데이터는 `ExtensionData` 속성의 키-값 쌍이 됩니다.

|속성 |값  |참고  |
|---------|---------|---------|
| Date    | 오전 8/1/2019 12:00:00-07:00||
| TemperatureC| 0 | 대/소문자를 구분 하는 불일치 (JSON의 `temperatureC`). 따라서 속성은 설정 되지 않습니다. |
| 요약 | 핫스폿을 ||
| ExtensionData | temperatureC: 25 |Case가 일치 하지 않기 때문에이 JSON 속성은 추가 이며 사전에서 키-값 쌍이 됩니다.|
|| DatesAvailable:<br>  오전 8/1/2019 12:00:00-07:00<br>오전 8/2/2019 12:00:00-07:00 |JSON의 추가 속성은 키-값 쌍이 되며 배열은 값 개체로 사용 됩니다.|
| |요약 단어:<br>표<br>바람<br>Humid |JSON의 추가 속성은 키-값 쌍이 되며 배열은 값 개체로 사용 됩니다.|

대상 개체가 serialize 되 면 확장 데이터 키 값 쌍은 수신 JSON에 있는 것 처럼 JSON 속성이 됩니다.

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 0,
  "Summary": "Hot",
  "temperatureC": 25,
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

@No__t-0 속성 이름은 JSON에 표시 되지 않습니다. 이 동작을 통해 JSON은 deserialize 되지 않는 추가 데이터를 잃지 않고도 라운드트립을 수행할 수 있습니다.

## <a name="use-utf8jsonwriter-directly"></a>Utf8JsonWriter 직접 사용

다음 예제에서는 <xref:System.Text.Json.Utf8JsonWriter> 클래스를 직접 사용 하는 방법을 보여 줍니다.

```csharp
var options = new JsonWriterOptions
{
    Indented = true
};

using (var stream = new MemoryStream())
{
    using (var writer = new Utf8JsonWriter(stream, options))
    {
        writer.WriteStartObject();
        writer.WriteString("date", DateTimeOffset.UtcNow);
        writer.WriteNumber("temp", 42);
        writer.WriteEndObject();
    }

    string json = Encoding.UTF8.GetString(stream.ToArray());
    Console.WriteLine(json);
}
```

## <a name="use-utf8jsonreader-directly"></a>Utf8JsonReader 직접 사용

다음 예제에서는 <xref:System.Text.Json.Utf8JsonReader> 클래스를 직접 사용 하는 방법을 보여 줍니다. 이 코드에서는 `jsonUtf8` 변수가 u t f-8로 인코딩된 유효한 JSON을 포함 하는 바이트 배열 이라고 가정 합니다.

```csharp
var options = new JsonReaderOptions
{
    AllowTrailingCommas = true,
    CommentHandling = JsonCommentHandling.Skip
};
Utf8JsonReader reader = new Utf8JsonReader(jsonUtf8, options);

while (reader.Read())
{
    Console.Write(reader.TokenType);

    switch (reader.TokenType)
    {
        case JsonTokenType.PropertyName:
        case JsonTokenType.String:
            {
                string text = reader.GetString();
                Console.Write(" ");
                Console.Write(text);
                break;
            }

        case JsonTokenType.Number:
            {
                int value = reader.GetInt32();
                Console.Write(" ");
                Console.Write(value);
                break;
            }

            // Other token types elided for brevity
    }

    Console.WriteLine();
}
```

## <a name="additional-resources"></a>추가 자료

* [System.object 개요](system-text-json-overview.md)
* [System.object API 참조](xref:System.Text.Json)
* [System.object의 DateTime 및 DateTimeOffset 지원](../datetime/system-text-json-support.md)
