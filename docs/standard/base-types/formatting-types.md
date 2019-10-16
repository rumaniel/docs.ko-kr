---
title: .NET의 서식 지정 형식
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data formatting [.NET Framework]
- dates [.NET Framework], formatting
- date formatting [.NET Framework]
- number formatting [.NET Framework]
- ToString method
- custom cultural settings [.NET Framework]
- numbers [.NET Framework], formatting
- formatting strings [.NET Framework]
- time [.NET Framework], formatting
- currency [.NET Framework], formatting
- types [.NET Framework], formatting
- format specifiers [.NET Framework]
- times [.NET Framework], formatting
- culture [.NET Framework], formatting
- formatting [.NET Framework], types supported
- base types [.NET Framework], formatting
- custom formatting [.NET Framework]
- strings [.NET Framework], formatting
ms.assetid: 0d1364da-5b30-4d42-8e6b-03378343343f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 82dc1e36ae5a0eede7099c8e13ac9a2393bbb904
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253974"
---
# <a name="formatting-types-in-net"></a>.NET의 서식 지정 형식

형식 지정은 대개 결과 문자열을 사용자에게 표시하거나 deserialize하여 원본 데이터 형식으로 복원하기 위해 클래스, 구조체 또는 열거형 값의 인스턴스를 해당 문자열 표현으로 변환하는 프로세스입니다. 이 변환 프로세스에는 다음과 같은 여러 가지 문제점이 나타날 수 있습니다.

- 내부적으로 값을 저장하는 방식에 사용자가 원하는 표시 방식이 반영되지 않을 수 있습니다. 예를 들어, 전화 번호가 사용자에게 친숙하지 않은 8009999999 형태로 저장될 수 있습니다. 이 전화 번호는 800-999-9999로 표시되어야 합니다. 이러한 방식으로 숫자의 형식을 지정하는 예제는 [사용자 지정 형식 문자열](#customStrings) 단원을 참조하세요.

- 개체를 문자열 표현으로 변환하는 과정이 명확하지 않을 수 있습니다. 예를 들어, Temperature 또는 Person 개체의 문자열 표현이 어떻게 표시될지 명확하지 않습니다. 다양한 방식으로 Temperature 개체의 형식을 지정하는 예제는 [표준 형식 문자열](#standardStrings) 단원을 참조하세요.

- 값에 문화권별 형식 지정이 필요할 수 있습니다. 예를 들어, 숫자를 사용하여 통화 값을 나타내는 애플리케이션에서는 숫자 문자열에 현재 문화권의 통화 기호, 그룹 구분 기호(대부분의 경우 1000 단위 구분 기호임) 및 소수점 기호가 포함되어야 합니다. 예제는 [형식 공급자 및 IFormatProvider 인터페이스를 사용하여 문화권 구분 형식 지정](#FormatProviders) 단원을 참조하세요.

- 애플리케이션에서 같은 값을 여러 가지 방법으로 표시해야 하는 경우도 있을 수 있습니다. 예를 들어, 애플리케이션에서 해당 이름의 문자열 표현을 표시하거나 해당 내부 값을 표시하여 열거형 멤버를 나타낼 수 있습니다. 다양한 방식으로 <xref:System.DayOfWeek> 열거형 멤버의 형식을 지정하는 예제는 [표준 형식 문자열](#standardStrings) 단원을 참조하세요.

> [!NOTE]
> 형식 지정은 형식의 값을 문자열 표현으로 변환합니다. 구문 분석은 형식 지정과 반대 과정으로 진행됩니다. 구문 분석 작업은 해당 문자열 표현에서 데이터 형식의 인스턴스를 만듭니다. 문자열을 다른 데이터 형식으로 변환하는 방법에 대한 자세한 내용은 [Parsing Strings](../../../docs/standard/base-types/parsing-strings.md)을 참조하세요.

.NET에서는 개발자가 이러한 요구 사항을 처리할 수 있는 다양한 형식 지정을 지원합니다.

이 개요는 다음과 같은 단원으로 구성됩니다.

- [.NET의 서식 지정](#NetFormatting)

- [ToString 메서드를 사용한 기본 형식 지정](#DefaultToString)

- [ToString 메서드 재정의](#OverrideToString)

- [ToString 메서드 및 형식 문자열](#FormatStrings)

  - [표준 형식 문자열](#standardStrings)

  - [사용자 지정 형식 문자열](#customStrings)

  - [서식 문자열 및 .NET 클래스 라이브러리 형식](#stringRef)

- [형식 공급자 및 IFormatProvider 인터페이스를 사용하여 문화권 구분 형식 지정](#FormatProviders)

  - [숫자 값의 문화권 구분 서식 지정](#numericCulture)

  - [날짜 및 시간 값의 문화권 구분 서식 지정](#dateCulture)

- [IFormattable 인터페이스](#IFormattable)

- [복합 형식 지정](#CompositeFormatting)

- [ICustomFormatter를 사용한 사용자 지정 형식 지정](#Custom)

- [관련 항목](#RelatedTopics)

- [참조](#Reference)

<a name="NetFormatting"></a>

## <a name="formatting-in-net"></a>.NET의 형식 지정

서식 지정의 기본 메커니즘은 이 항목의 뒷부분에 나오는 [ToString 메서드를 사용한 기본 형식 지정](#DefaultToString) 섹션에서 설명하는 <xref:System.Object.ToString%2A?displayProperty=nameWithType> 메서드의 기본 구현입니다. 그러나 .NET에서는 기본 형식 지정 지원을 수정하고 확장할 수 있는 여러 가지 방법을 제공합니다. 이러한 요구 사항은 다음과 같습니다.

- <xref:System.Object.ToString%2A?displayProperty=nameWithType> 메서드를 재정의하여 개체의 값에 대한 사용자 지정 문자열 표현을 정의합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [ToString 메서드 재정의](#OverrideToString) 단원을 참조하세요.

- 개체의 값에 대한 문자열 표현에서 여러 형식을 사용할 수 있도록 형식 지정자를 정의합니다. 예를 들어, 다음 문의 "X" 형식 지정자는 정수를 16진수 값의 문자열 표현으로 변환합니다.

     [!code-csharp[Conceptual.Formatting.Overview#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/specifier1.cs#3)]
     [!code-vb[Conceptual.Formatting.Overview#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/specifier1.vb#3)]

     형식 지정자에 대한 자세한 내용은 [ToString 메서드 및 형식 문자열](#FormatStrings) 단원을 참조하세요.

- 형식 공급자를 사용하여 특정 문화권의 형식 지정 규칙을 사용합니다. 예를 들어, 다음 문은 en-US 문화권의 형식 지정 규칙을 사용하여 통화 값을 표시합니다.

     [!code-csharp[Conceptual.Formatting.Overview#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/specifier1.cs#10)]
     [!code-vb[Conceptual.Formatting.Overview#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/specifier1.vb#10)]

     형식 공급자를 사용하여 형식을 지정하는 방법에 대한 자세한 내용은 [형식 공급자 및 IFormatProvider 인터페이스](#FormatProviders) 단원을 참조하세요.

- <xref:System.IFormattable> 인터페이스를 구현하여 <xref:System.Convert> 클래스를 사용하여 문자열 변환과 복합 형식 지정을 지원합니다. 자세한 내용은 [IFormattable 인터페이스](#IFormattable) 단원을 참조하세요.

- 복합 형식 지정을 사용하여 값의 문자열 표현을 더 큰 문자열에 포함합니다. 자세한 내용은 [복합 형식 지정](#CompositeFormatting) 단원을 참조하세요.

- <xref:System.ICustomFormatter> 와 <xref:System.IFormatProvider> 를 구현하여 완벽한 사용자 지정 형식 지정 솔루션을 제공합니다. 자세한 내용은 [ICustomFormatter를 사용한 사용자 지정 형식 지정](#Custom) 단원을 참조하세요.

다음 단원에서는 개체를 문자열 표현으로 변환하는 데 대해 이러한 메서드를 검토합니다.

<a name="DefaultToString"></a>

## <a name="default-formatting-using-the-tostring-method"></a>ToString 메서드를 사용한 기본 형식 지정

<xref:System.Object?displayProperty=nameWithType> 에서 파생되는 모든 형식은 기본적으로 형식의 이름을 반환하는 매개 변수가 없는 `ToString` 메서드를 상속합니다. 다음 예제에서는 기본 `ToString` 메서드를 보여 줍니다. 이 예제에서는 구현이 없는 `Automobile` 이라는 클래스를 정의합니다. 클래스가 인스턴스화되고 `ToString` 메서드가 호출되면 해당 형식 이름이 표시됩니다. 예제에서는 `ToString` 메서드를 명시적으로 호출하지 않습니다. <xref:System.Console.WriteLine%28System.Object%29?displayProperty=nameWithType> 메서드는 인수로 전달되는 개체의 `ToString` 메서드를 암시적으로 호출합니다.

[!code-csharp[Conceptual.Formatting.Overview#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/default1.cs#1)]
[!code-vb[Conceptual.Formatting.Overview#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/default1.vb#1)]

> [!WARNING]
> [!INCLUDE[win81](../../../includes/win81-md.md)]부터 Windows Runtime에는 기본 형식 지원을 제공하는 단일 메서드([IStringable.ToString](xref:Windows.Foundation.IStringable.ToString%2A))를 사용하는 <xref:Windows.Foundation.IStringable> 인터페이스가 포함됩니다. 그러나 관리되는 형식은 `IStringable` 인터페이스를 구현하지 않는 것이 좋습니다. 자세한 내용은 <xref:System.Object.ToString%2A?displayProperty=nameWithType> 참조 페이지의 " Windows Runtime 및 `IStringable` 인터페이스" 섹션을 참조하세요.

인터페이스를 제외한 모든 형식이 <xref:System.Object>에서 파생되기 때문에 이 함수는 사용자 지정 클래스 또는 구조체에 자동으로 제공됩니다. 그러나 기본 `ToString` 메서드에서 제공하는 기능은 다음과 같이 제한됩니다. 형식을 식별하지만 형식의 인스턴스에 대한 정보를 제공하지 못합니다. 이 개체에 대한 정보를 제공하는 개체의 문자열 표현을 제공하려면 `ToString` 메서드를 재정의해야 합니다.

> [!NOTE]
> 구조체는 <xref:System.ValueType>에서 상속되며, 이 형식은 다시 <xref:System.Object>에서 파생됩니다. <xref:System.ValueType> 이 <xref:System.Object.ToString%2A?displayProperty=nameWithType>을 재정의해도 해당 구현은 동일합니다.

<a name="OverrideToString"></a>

## <a name="overriding-the-tostring-method"></a>ToString 메서드 재정의

형식 이름을 표시할 수 있는 경우가 종종 제한되어 형식의 사용자가 서로 다른 인스턴스를 구분할 수 없는 경우가 있습니다. 그러나 `ToString` 메서드를 재정의하여 개체 값을 더 유용하게 표현할 수 있습니다. 다음 예제에서는 `Temperature` 개체를 정의하고 `ToString` 메서드를 재정의하여 온도를 섭씨 단위로 표시합니다.

[!code-csharp[Conceptual.Formatting.Overview#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/overrides1.cs#2)]
[!code-vb[Conceptual.Formatting.Overview#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/overrides1.vb#2)]

.NET에서 각 기본 값 형식의 `ToString` 메서드는 개체의 이름 대신 개체의 값을 표시하도록 재정의되었습니다. 다음 표에는 각 기본 형식의 재정의가 나와 있습니다. 재정의된 메서드의 대부분은 `ToString` 메서드의 다른 오버로드를 호출하고 이를 해당 형식에 대한 일반적인 형식을 정의하는 "G" 형식 지정자와 현재 문화권을 나타내는 <xref:System.IFormatProvider> 개체에 전달합니다.

|형식|ToString 재정의|
|----------|-----------------------|
|<xref:System.Boolean>|<xref:System.Boolean.TrueString?displayProperty=nameWithType> 또는 <xref:System.Boolean.FalseString?displayProperty=nameWithType>을 반환합니다.|
|<xref:System.Byte>|`Byte.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.Byte> 값의 형식을 지정합니다.|
|<xref:System.Char>|문자를 문자열로 반환합니다.|
|<xref:System.DateTime>|`DateTime.ToString("G", DatetimeFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 날짜 및 시간 값의 형식을 지정합니다.|
|<xref:System.Decimal>|`Decimal.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.Decimal> 값의 형식을 지정합니다.|
|<xref:System.Double>|`Double.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.Double> 값의 형식을 지정합니다.|
|<xref:System.Int16>|`Int16.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.Int16> 값의 형식을 지정합니다.|
|<xref:System.Int32>|`Int32.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.Int32> 값의 형식을 지정합니다.|
|<xref:System.Int64>|`Int64.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.Int64> 값의 형식을 지정합니다.|
|<xref:System.SByte>|`SByte.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.SByte> 값의 형식을 지정합니다.|
|<xref:System.Single>|`Single.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.Single> 값의 형식을 지정합니다.|
|<xref:System.UInt16>|`UInt16.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.UInt16> 값의 형식을 지정합니다.|
|<xref:System.UInt32>|`UInt32.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.UInt32> 값의 형식을 지정합니다.|
|<xref:System.UInt64>|`UInt64.ToString("G", NumberFormatInfo.CurrentInfo)` 을 호출하여 현재 문화권에 대한 <xref:System.UInt64> 값의 형식을 지정합니다.|

<a name="FormatStrings"></a>

## <a name="the-tostring-method-and-format-strings"></a>ToString 메서드 및 형식 문자열

개체에 문자열 표현이 하나만 있는 경우에는 기본 `ToString` 메서드를 사용하거나 `ToString` 을 재정의합니다. 하지만 개체의 값에 여러 표현이 있는 경우가 자주 있습니다. 예를 들어 온도는 화씨, 섭씨 또는 캘빈으로 표시할 수 있습니다. 마찬가지로 정수 값 10도 10, 10.0, 1.0e01, $10.00 등과 같은 여러 가지 방식으로 표현될 수 있습니다.

하나의 값에 여러 문자열 표현을 허용하기 위해 .NET에서는 형식 문자열을 사용합니다. 형식 문자열은 하나 이상의 미리 정의된 형식 지정자가 들어 있는 문자열이며, 이러한 형식 지정자는 `ToString` 메서드가 해당 출력의 형식을 지정하는 방식을 정의한 단일 문자 또는 문자 그룹입니다. 형식 문자열은 개체의 `ToString` 메서드에 매개 변수로 전달되어 개체의 값에 대한 문자열 표현의 표시 방법을 결정합니다.

.NET의 모든 숫자 형식, 날짜/시간 형식 및 열거형 형식은 미리 정의된 형식 지정자 집합을 지원합니다. 형식 문자열을 사용하여 애플리케이션 정의 데이터 형식의 여러 문자열 표현도 정의할 수 있습니다.

<a name="standardStrings"></a>

### <a name="standard-format-strings"></a>표준 형식 문자열

표준 형식 문자열에는 개체의 문자열 표현을 정의하는 영문자인 단일 형식 지정자와 함께 결과 문자열을 표시하는 데 사용할 자릿수에 영향을 주는 선택적 전체 자릿수 지정자가 포함됩니다. 전체 자릿수 지정자가 생략되었거나 지원되지 않으면 표준 형식 지정자는 표준 형식 문자열과 같습니다.

.NET에서는 모든 숫자 형식, 날짜/시간 형식 및 열거형 형식에 대한 표준 형식 지정자 집합을 정의합니다. 예를 들어, 이러한 각 범주는 해당 형식 값에 대한 일반적인 문자열 표현을 정의하는 "G" 표준 형식 지정자를 지원합니다.

열거형 형식의 표준 형식 문자열은 값의 문자열 표현을 직접 제어합니다. 열거형 값의 `ToString` 메서드에 전달된 형식 문자열은 값이 문자열 이름("G" 및 "F" 형식 지정자), 내부 정수 값("D" 형식 지정자) 또는 16진수 값("X" 형식 지정자)을 사용하여 표시되는지 여부를 결정합니다. 다음 예제에서는 표준 형식 문자열을 사용하여 <xref:System.DayOfWeek> 열거형 값의 형식을 지정하는 방법을 보여 줍니다.

[!code-csharp[Conceptual.Formatting.Overview#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/standard1.cs#4)]
[!code-vb[Conceptual.Formatting.Overview#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/standard1.vb#4)]

열거형 형식 문자열에 대한 자세한 내용은 [Enumeration Format Strings](../../../docs/standard/base-types/enumeration-format-strings.md)을 참조하세요.

일반적으로 숫자 형식의 표준 형식 문자열은 정확한 모양이 하나 이상의 속성 값에 의해 제어되는 결과 문자열을 정의합니다. 예를 들어, "C" 형식 지정자는 숫자의 형식을 통화 값으로 지정합니다. "C" 형식 지정자를 유일한 매개 변수로 사용하여 `ToString` 메서드를 호출하면 현재 문화권의 <xref:System.Globalization.NumberFormatInfo> 개체에 있는 다음 속성 값이 숫자 값의 문자열 표현을 정의하는 데 사용됩니다.

- 현재 문화권의 통화 기호를 지정하는 <xref:System.Globalization.NumberFormatInfo.CurrencySymbol%2A> 속성

- 다음과 같은 사항을 결정하는 정수를 반환하는 <xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern%2A> 또는 <xref:System.Globalization.NumberFormatInfo.CurrencyPositivePattern%2A> 속성

  - 통화 기호의 위치

  - 음수 값이 선행 음수 기호, 후행 음수 기호 또는 괄호로 표시되는지 여부

  - 숫자 값과 통화 기호 사이에 공백이 표시되는지 여부

- 결과 문자열의 소수 자릿수를 정의하는 <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A> 속성

- 결과 문자열의 소수 구분 기호를 정의하는 <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator%2A> 속성

- 그룹 구분 기호를 정의하는 <xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator%2A> 속성

- 정수 부분의 각 그룹 자릿수를 정의하는 <xref:System.Globalization.NumberFormatInfo.CurrencyGroupSizes%2A> 속성

- 음수 값을 나타내는 데 괄호가 사용되지 않는 경우 결과 문자열에 사용되는 음수 기호를 결정하는 <xref:System.Globalization.NumberFormatInfo.NegativeSign%2A> 속성

이외에도 숫자 형식 문자열에는 전체 자릿수 지정자가 포함될 수도 있습니다. 이 지정자의 의미는 해당 지정자가 사용되는 형식 문자열에 따라 달라지지만 일반적으로 결과 문자열에 표시될 전체 자릿수나 소수 자릿수를 나타냅니다. 예를 들어, 다음 예제에서는 "X4" 표준 숫자 문자열과 전체 자릿수 지정자를 사용하여 네 자리의 16진수로 구성된 문자열 값을 만듭니다.

[!code-csharp[Conceptual.Formatting.Overview#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/precisionspecifier1.cs#6)]
[!code-vb[Conceptual.Formatting.Overview#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/precisionspecifier1.vb#6)]

표준 숫자 서식 지정 문자열에 대한 자세한 내용은 [Standard Numeric Format Strings](../../../docs/standard/base-types/standard-numeric-format-strings.md)을 참조하세요.

날짜 및 시간 값의 표준 형식 문자열은 특정 <xref:System.Globalization.DateTimeFormatInfo> 속성에 저장된 사용자 지정 형식 문자열의 별칭입니다. 예를 들어, "D" 형식 지정자를 사용하여 날짜 및 시간 값의 `ToString` 메서드를 호출하면 현재 문화권의 <xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A?displayProperty=nameWithType> 속성에 저장된 사용자 지정 형식 문자열을 사용하여 날짜 및 시간이 표시됩니다. (사용자 지정 서식 문자열에 대한 자세한 내용은 [다음 섹션](#customStrings)을 참조하세요.) 다음 예제에서는 이러한 관계를 보여 줍니다.

[!code-csharp[Conceptual.Formatting.Overview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/alias1.cs#5)]
[!code-vb[Conceptual.Formatting.Overview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/alias1.vb#5)]

표준 날짜 및 시간 형식 문자열에 대한 자세한 내용은 [Standard Date and Time Format Strings](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)을 참조하세요.

표준 형식 문자열을 사용하여 개체의 `ToString(String)` 메서드에 의해 생성되는 애플리케이션 정의 개체의 문자열 표현도 정의할 수 있습니다. 개체가 지원하는 특정 표준 형식 지정자를 정의하고 이러한 지정자가 대/소문자를 구분하는지 여부를 결정할 수 있습니다. `ToString(String)` 메서드의 구현에서는 다음을 지원해야 합니다.

- 개체의 사용자 지정 또는 일반 형식을 나타내는 "G" 형식 지정자. 개체의 `ToString` 메서드에 대한 매개 변수가 없는 오버로드는 해당 `ToString(String)` 오버로드를 호출하고 이를 "G" 표준 형식 문자열에 전달해야 합니다.

- null 참조(Visual Basic의 경우`Nothing` )와 동일한 형식 지정자에 대한 지원. null 참조와 동일한 형식 지정자는 "G" 형식 지정자와 같은 것으로 간주됩니다.

예를 들어 `Temperature` 클래스는 섭씨 온도를 내부적으로 저장하고 형식 지정자를 사용하여 `Temperature` 개체의 값을 섭씨, 화씨 및 캘빈으로 표시할 수 있습니다. 다음 예제에서 이에 대해 설명합니다.

[!code-csharp[Conceptual.Formatting.Overview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/appstandard1.cs#7)]
[!code-vb[Conceptual.Formatting.Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/appstandard1.vb#7)]

<a name="customStrings"></a>

### <a name="custom-format-strings"></a>사용자 지정 형식 문자열

표준 형식 문자열 외에도 .NET에서는 숫자 값과 날짜 및 시간 값에 대한 사용자 지정 형식 문자열을 정의합니다. 사용자 지정 형식 문자열은 값의 문자열 표현을 정의하는 하나 이상의 사용자 지정 형식 지정자로 구성됩니다. 예를 들어, en-US 문화권의 경우 사용자 지정 날짜 및 시간 형식 문자열 "yyyy/mm/dd hh:mm:ss t zzz"는 날짜를 "2008/11/15 07:45:00.0000 P -08:00" 형태의 문자열 표현으로 변환합니다. 마찬가지로 사용자 지정 형식 문자열 "0000"은 정수 값 12를 "0012"로 변환합니다. 사용자 지정 서식 문자열의 전체 목록은 [Custom Date and Time Format Strings](../../../docs/standard/base-types/custom-date-and-time-format-strings.md) 및 [Custom Numeric Format Strings](../../../docs/standard/base-types/custom-numeric-format-strings.md)을 참조하세요.

형식 문자열이 단일 사용자 지정 형식 지정자로 구성된 경우에는 표준 형식 지정자와 혼동되지 않도록 형식 지정자 앞에 백분율 기호(%)가 와야 합니다. 다음 예제에서는 "M" 사용자 지정 형식 지정자를 사용하여 특정 날짜의 월에 해당하는 한 자리 또는 두 자리 숫자를 표시합니다.

[!code-csharp[Conceptual.Formatting.Overview#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/singlecustom1.cs#8)]
[!code-vb[Conceptual.Formatting.Overview#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/singlecustom1.vb#8)]

많은 표준 형식 문자열은 <xref:System.Globalization.DateTimeFormatInfo> 개체의 속성에 정의된 사용자 지정 형식 문자열의 별칭입니다. 또한 사용자 지정 형식 문자열을 사용하면 상당히 융통성 있게 숫자 값 또는 날짜 및 시간 값에 대한 애플리케이션 정의 형식 지정 기능을 제공할 수 있습니다. 여러 사용자 지정 형식 지정자를 하나의 사용자 지정 형식 문자열로 결합하여 숫자 값과 날짜 및 시간 값에 대한 사용자 지정 결과 문자열을 정의할 수 있습니다. 다음 예제에서는 월 이름, 일, 연도 및 괄호로 묶은 요일을 차례로 표시하는 사용자 지정 형식 문자열을 정의합니다.

[!code-csharp[Conceptual.Formatting.Overview#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/custom1.cs#9)]
[!code-vb[Conceptual.Formatting.Overview#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/custom1.vb#9)]

다음 예제에서는 <xref:System.Int64> 값을 7자리 표준 미국 전화 번호로 지역 번호와 함께 표시하는 사용자 지정 서식 문자열을 정의합니다.

[!code-csharp[Conceptual.Formatting.Overview#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/telnumber1.cs#21)]
[!code-vb[Conceptual.Formatting.Overview#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/telnumber1.vb#21)]

일반적으로 표준 형식 문자열로 애플리케이션 정의 형식의 형식 지정 요구를 대부분 처리할 수 있지만 사용자 지정 형식 지정자를 정의하여 형식의 형식을 지정할 수도 있습니다.

<a name="stringRef"></a>

### <a name="format-strings-and-net-types"></a>형식 문자열 및 .NET 형식

모든 숫자 형식(즉, <xref:System.Byte>, <xref:System.Decimal>, <xref:System.Double>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.Single>, <xref:System.UInt16>, <xref:System.UInt32>,<xref:System.UInt64> 및 <xref:System.Numerics.BigInteger> 형식)과 <xref:System.DateTime>, <xref:System.DateTimeOffset>, <xref:System.TimeSpan>, <xref:System.Guid> 및 모든 열거형 형식은 서식 문자열을 사용한 서식 지정을 지원합니다. 각 형식에서 지원되는 형식 문자열에 대한 자세한 내용은 다음 항목을 참조하세요.

|제목|정의|
|-----------|----------------|
|[Standard Numeric Format Strings](../../../docs/standard/base-types/standard-numeric-format-strings.md)|숫자 값의 일반적으로 사용되는 문자열 표현을 만드는 표준 형식 문자열에 대해 설명합니다.|
|[Custom Numeric Format Strings](../../../docs/standard/base-types/custom-numeric-format-strings.md)|숫자 값의 애플리케이션별 형식을 만드는 사용자 지정 형식 문자열에 대해 설명합니다.|
|[표준 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)|<xref:System.DateTime> 및 <xref:System.DateTimeOffset> 값의 일반적으로 사용되는 문자열 표현을 만드는 표준 서식 문자열에 대해 설명합니다.|
|[사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)|<xref:System.DateTime> 및 <xref:System.DateTimeOffset> 값의 애플리케이션별 서식을 만드는 사용자 지정 서식 문자열에 대해 설명합니다.|
|[표준 TimeSpan 서식 문자열](../../../docs/standard/base-types/standard-timespan-format-strings.md)|시간 간격의 일반적으로 사용되는 문자열 표현을 만드는 표준 형식 문자열에 대해 설명합니다.|
|[사용자 지정 TimeSpan 서식 문자열](../../../docs/standard/base-types/custom-timespan-format-strings.md)|시간 간격의 애플리케이션별 형식을 만드는 사용자 지정 형식 문자열에 대해 설명합니다.|
|[Enumeration Format Strings](../../../docs/standard/base-types/enumeration-format-strings.md)|열거형 값의 문자열 표현을 만드는 데 사용되는 표준 형식 문자열에 대해 설명합니다.|
|<xref:System.Guid.ToString%28System.String%29?displayProperty=nameWithType>|<xref:System.Guid> 값에 대한 표준 형식 문자열에 대해 설명합니다.|

<a name="FormatProviders"></a>

## <a name="culture-sensitive-formatting-with-format-providers-and-the-iformatprovider-interface"></a>형식 공급자 및 IFormatProvider 인터페이스를 사용하여 문화권 구분 형식 지정

형식 지정자를 사용하여 개체의 형식 지정을 사용자 지정할 수 있기는 하지만 의미 있는 개체의 문자열 표현을 만들려면 추가 형식 지정 정보가 필요한 경우가 종종 있습니다. 예를 들어, C" 표준 형식 문자열이나 "$ #,#.00" 같은 사용자 지정 형식 문자열을 사용하여 숫자의 형식을 통화 값으로 지정하려면 최소한 올바른 통화 기호, 그룹 구분 기호 및 소수 구분 기호에 대한 정보를 형식 지정된 문자열에 포함할 수 있어야 합니다. .NET에서는 이러한 추가 서식 지정 정보를 <xref:System.IFormatProvider> 인터페이스를 통해 사용할 수 있습니다. 이러한 인터페이스는 숫자 형식과 날짜 및 시간 형식의 `ToString` 메서드에 대한 하나 이상의 오버로드에 매개 변수로 제공됩니다. <xref:System.IFormatProvider> 구현은 .NET에서 문화권별 서식 지정을 지원하는 데 사용됩니다. 다음 예제에서는 서로 다른 문화권을 나타내는 세 <xref:System.IFormatProvider> 개체를 사용하여 형식을 지정할 때 개체의 문자열 표현이 어떻게 바뀌는지 보여 줍니다.

[!code-csharp[Conceptual.Formatting.Overview#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/iformatprovider1.cs#11)]
[!code-vb[Conceptual.Formatting.Overview#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/iformatprovider1.vb#11)]

<xref:System.IFormatProvider> 인터페이스에는 <xref:System.IFormatProvider.GetFormat%28System.Type%29>메서드가 하나 있으며, 이 메서드에는 형식 지정 정보를 제공하는 개체의 형식을 지정하는 매개 변수가 하나 있습니다. 이 메서드는 해당 형식의 개체를 제공할 수 있는 경우 해당 형식의 개체를 반환합니다. 그러지 않으면 null 참조(Visual Basic의 경우`Nothing` )를 반환합니다.

<xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 은 콜백 메서드입니다. `ToString` 매개 변수가 포함된 <xref:System.IFormatProvider> 메서드 오버로드를 호출하면 해당 <xref:System.IFormatProvider.GetFormat%2A> 개체의 <xref:System.IFormatProvider> 메서드가 호출됩니다. <xref:System.IFormatProvider.GetFormat%2A> 메서드는 `formatType` 매개 변수에 지정된 대로 필요한 형식 지정 정보를 제공하는 개체를 `ToString` 메서드에 반환합니다.

<xref:System.IFormatProvider>형식의 매개 변수를 포함하는 형식 지정 또는 문자열 변환 메서드가 많이 있기는 하지만 대부분의 경우 메서드가 호출될 때 매개 변수의 값이 무시됩니다. 다음 표에서는 매개 변수를 사용하는 형식 지정 메서드와 이러한 메서드가 <xref:System.Type> 메서드로 전달하는 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 개체의 형식을 보여 줍니다.

|메서드|`formatType` 매개 변수의 형식|
|------------|------------------------------------|
|숫자 형식의`ToString` 메서드|<xref:System.Globalization.NumberFormatInfo?displayProperty=nameWithType>|
|날짜 및 시간 형식의`ToString` 메서드|<xref:System.Globalization.DateTimeFormatInfo?displayProperty=nameWithType>|
|<xref:System.String.Format%2A?displayProperty=nameWithType>|<xref:System.ICustomFormatter?displayProperty=nameWithType>|
|<xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType>|<xref:System.ICustomFormatter?displayProperty=nameWithType>|

> [!NOTE]
> 숫자 형식과 날짜 및 시간 형식의 `ToString` 메서드는 오버로드되며, 일부 오버로드에만 <xref:System.IFormatProvider> 매개 변수가 포함됩니다. 메서드에 <xref:System.IFormatProvider>형식의 매개 변수가 없으면 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 속성에 의해 반환되는 개체가 대신 전달됩니다. 예를 들어, 기본 <xref:System.Int32.ToString?displayProperty=nameWithType> 메서드를 호출하면 결과적으로 `Int32.ToString("G", System.Globalization.CultureInfo.CurrentCulture)`같은 메서드가 호출됩니다.

.NET에는 <xref:System.IFormatProvider>를 구현하는 세 가지 클래스가 있습니다.

- 특정 문화권의 날짜 및 시간 값에 대한 형식 지정 정보를 제공하는<xref:System.Globalization.DateTimeFormatInfo>클래스. 이 클래스에 대해 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 을 구현하면 해당 클래스의 인스턴스가 반환됩니다.

- 특정 문화권의 숫자 형식 지정 정보를 제공하는<xref:System.Globalization.NumberFormatInfo>클래스. 이 클래스에 대해 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 을 구현하면 해당 클래스의 인스턴스가 반환됩니다.

- <xref:System.Globalization.CultureInfo>. 이 클래스에 대해 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=nameWithType> 을 구현하면 숫자 형식 지정 정보를 제공하는 <xref:System.Globalization.NumberFormatInfo> 개체 또는 날짜 및 시간 값에 대한 형식 지정 정보를 제공하는 <xref:System.Globalization.DateTimeFormatInfo> 개체가 반환될 수 있습니다.

사용자 고유의 형식 공급자를 구현하여 이러한 클래스 중 하나를 대체할 수도 있습니다. 그러나 <xref:System.IFormatProvider.GetFormat%2A> 메서드에 형식 지정 정보를 제공해야 하는 경우에는 구현된 형식 공급자의 `ToString` 메서드에서 위의 표에 나와 있는 형식의 개체를 반환해야 합니다.

<a name="numericCulture"></a>

### <a name="culture-sensitive-formatting-of-numeric-values"></a>숫자 값의 문화권 구분 서식 지정

기본적으로 숫자 값의 형식은 문화권을 구분합니다. 형식 지정 메서드를 호출할 때 문화권을 지정하지 않으면 현재 스레드 문화권의 형식 규칙이 사용됩니다. 이는 현재 스레드 문화권을 4번 변경한 후 <xref:System.Decimal.ToString%28System.String%29?displayProperty=nameWithType> 메서드를 호출하는 다음 예제에 나와 있습니다. 각각의 경우 결과 문자열은 현재 문화권의 형식 규칙을 반영합니다. 이는 `ToString` 및 `ToString(String)` 메서드가 각 숫자 형식의 `ToString(String, IFormatProvider)` 메서드에 대한 호출을 래핑하기 때문입니다.

[!code-csharp[Conceptual.Formatting.Overview#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/culturespecific3.cs#19)]
[!code-vb[Conceptual.Formatting.Overview#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/culturespecific3.vb#19)]

`ToString` 매개 변수를 포함하는 `provider` 오버로드를 호출하고 여기에 다음 중 하나를 전달하여 특정 문화권에 대한 숫자 값의 형식을 지정할 수도 있습니다.

- 사용할 형식 규칙이 포함된 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체. 해당 <xref:System.Globalization.CultureInfo.GetFormat%2A?displayProperty=nameWithType> 메서드는 숫자 값에 대한 문화권별 형식 정보를 제공하는 <xref:System.Globalization.CultureInfo.NumberFormat%2A?displayProperty=nameWithType> 개체인 <xref:System.Globalization.NumberFormatInfo> 속성의 값을 반환합니다.

- 사용할 문화권별 형식 규칙을 정의하는 <xref:System.Globalization.NumberFormatInfo> 개체. 해당 <xref:System.Globalization.NumberFormatInfo.GetFormat%2A> 메서드는 자신의 인스턴스를 반환합니다.

다음 예제에서는 부동 소수점 수의 형식을 지정하기 위해 영어(미국) 및 영어(영국) 문화권과 프랑스어 및 러시아어 중립 문화권을 나타내는 <xref:System.Globalization.NumberFormatInfo> 개체를 사용합니다.

[!code-csharp[Conceptual.Formatting.Overview#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/culturespecific4.cs#20)]
[!code-vb[Conceptual.Formatting.Overview#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/culturespecific4.vb#20)]

<a name="dateCulture"></a>

### <a name="culture-sensitive-formatting-of-date-and-time-values"></a>날짜 및 시간 값의 문화권 구분 서식 지정

기본적으로 날짜 및 시간 값의 형식은 문화권을 구분합니다. 형식 지정 메서드를 호출할 때 문화권을 지정하지 않으면 현재 스레드 문화권의 형식 규칙이 사용됩니다. 이는 현재 스레드 문화권을 4번 변경한 후 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 메서드를 호출하는 다음 예제에 나와 있습니다. 각각의 경우 결과 문자열은 현재 문화권의 형식 규칙을 반영합니다. 이는 <xref:System.DateTime.ToString?displayProperty=nameWithType>, <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType>, <xref:System.DateTimeOffset.ToString?displayProperty=nameWithType>및 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> 메서드가 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 및 <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 메서드에 대한 호출을 래핑하기 때문입니다.

[!code-csharp[Conceptual.Formatting.Overview#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/culturespecific1.cs#17)]
[!code-vb[Conceptual.Formatting.Overview#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/culturespecific1.vb#17)]

<xref:System.DateTime.ToString%2A?displayProperty=nameWithType> 매개 변수를 포함하는 <xref:System.DateTimeOffset.ToString%2A?displayProperty=nameWithType> 또는 `provider` 오버로드를 호출하고 여기에 다음 중 하나를 전달하여 특정 문화권에 대한 날짜 및 시간 값의 형식을 지정할 수도 있습니다.

- 사용할 형식 규칙이 포함된 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체. 해당 <xref:System.Globalization.CultureInfo.GetFormat%2A?displayProperty=nameWithType> 메서드는 날짜 및 시간 값에 대한 문화권별 형식 정보를 제공하는 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType> 개체인 <xref:System.Globalization.DateTimeFormatInfo> 속성의 값을 반환합니다.

- 사용할 문화권별 형식 규칙을 정의하는 <xref:System.Globalization.DateTimeFormatInfo> 개체. 해당 <xref:System.Globalization.DateTimeFormatInfo.GetFormat%2A> 메서드는 자신의 인스턴스를 반환합니다.

다음 예제에서는 날짜의 형식을 지정하기 위해 영어(미국) 및 영어(영국) 문화권과 프랑스어 및 러시아어 중립 문화권을 나타내는 <xref:System.Globalization.DateTimeFormatInfo> 개체를 사용합니다.

[!code-csharp[Conceptual.Formatting.Overview#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/culturespecific2.cs#18)]
[!code-vb[Conceptual.Formatting.Overview#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/culturespecific2.vb#18)]

<a name="IFormattable"></a>

## <a name="the-iformattable-interface"></a>IFormattable 인터페이스

일반적으로 형식 문자열과 `ToString` 매개 변수로 <xref:System.IFormatProvider> 메서드를 오버로드하는 형식은 <xref:System.IFormattable> 인터페이스도 구현합니다. 이 인터페이스에는 형식 문자열과 형식 공급자가 매개 변수로 포함되어 있는 <xref:System.IFormattable.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType>이라는 단일 멤버가 있습니다.

애플리케이션 정의 클래스에 대해 <xref:System.IFormattable> 인터페이스를 구현하면 다음과 같은 두 가지 이점이 있습니다.

- <xref:System.Convert> 클래스를 사용한 문자열 변환을 지원합니다. <xref:System.Convert.ToString%28System.Object%29?displayProperty=nameWithType> 및 <xref:System.Convert.ToString%28System.Object%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 메서드를 호출하면 <xref:System.IFormattable> 구현이 자동으로 호출됩니다.

- 복합 형식 지정을 지원합니다. 형식 문자열을 포함한 형식 항목이 사용자 지정 형식의 형식을 지정하는 데 사용되면 공용 언어 런타임에서 자동으로 <xref:System.IFormattable> 구현을 호출하고 이를 형식 문자열에 전달합니다. <xref:System.String.Format%2A?displayProperty=nameWithType> 또는 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType>같은 메서드를 사용하는 복합 형식 지정에 대한 자세한 내용은 [복합 형식 지정](#CompositeFormatting) 단원을 참조하세요.

다음 예제에서는 `Temperature` 인터페이스를 구현하는 <xref:System.IFormattable> 클래스를 정의합니다. 이 클래스는 온도를 섭씨로 표시하는 "C" 또는 "G" 형식 지정자, 온도를 화씨로 표시하는 "F" 형식 지정자 또는 온도를 켈빈으로 표시하는 "K" 형식 지정자를 지원합니다.

[!code-csharp[Conceptual.Formatting.Overview#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/iformattable.cs#12)]
[!code-vb[Conceptual.Formatting.Overview#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/iformattable.vb#12)]

다음 예제에서는 `Temperature` 개체를 인스턴스화합니다. 그런 다음 <xref:System.Convert.ToString%2A> 메서드를 호출하고 여러 복합 형식 문자열을 사용하여 `Temperature` 개체의 다양한 문자열 표현을 얻습니다. 이 메서드를 호출할 때마다 자동으로 <xref:System.IFormattable> 클래스의 `Temperature` 구현도 호출됩니다.

[!code-csharp[Conceptual.Formatting.Overview#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/iformattable.cs#13)]
[!code-vb[Conceptual.Formatting.Overview#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/iformattable.vb#13)]

<a name="CompositeFormatting"></a>

## <a name="composite-formatting"></a>복합 형식 지정

<xref:System.String.Format%2A?displayProperty=nameWithType> 및 <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType>같은 일부 메서드는 복합 형식 지정을 지원합니다. 복합 형식 문자열은 0개 이상의 개체에 대한 문자열 표현이 통합된 단일 문자열을 반환하는 일종의 템플릿입니다. 복합 형식 문자열에서는 각 개체가 인덱싱된 형식 항목으로 표현됩니다. 형식 항목의 인덱스는 메서드의 매개 변수 목록에 표시되는 개체의 위치에 해당합니다. 인덱스는 0에서 시작합니다. 예를 들어 다음과 같은 <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드 호출에서 첫 번째 형식 항목인 `{0:D}`는 `thatDate`의 문자열 표현으로 바뀌고, 두 번째 형식 항목인 `{1}`은 `item1`의 문자열 표현으로 바뀌고, 세 번째 형식 항목인 `{2:C2}`는 `item1.Value`의 문자열 표현으로 바뀝니다.

[!code-csharp[Conceptual.Formatting.Overview#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/composite1.cs#14)]
[!code-vb[Conceptual.Formatting.Overview#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/composite1.vb#14)]

형식 항목을 해당 개체의 문자열 표현으로 바꾸는 것 외에도 형식 항목을 통해 다음을 제어할 수 있습니다.

- 개체가 <xref:System.IFormattable> 인터페이스를 구현하고 형식 문자열을 지원하는 경우 개체가 문자열로 표현되는 특정 방식. 이렇게 하려면 형식 항목의 인덱스 뒤에 `:` (콜론) 및 유효한 형식 문자열을 추가합니다. 이전 예제에서는 날짜 값의 형식을 "d"(짧은 날짜 패턴) 형식 문자열(예: `{0:d}`)로 지정하고 숫자 값의 형식을 "C2" 형식 문자열(예: `{2:C2}` )로 지정하여 소수 2자리의 통화 값으로 숫자를 나타냈습니다.

- 개체의 문자열 표현을 포함하는 필드의 너비 및 해당 필드의 문자열 표현 맞춤. 이렇게 하려면 형식 항목의 인덱스 뒤에 `,` (쉼표) 및 필드 너비를 추가합니다. 필드 너비가 양수 값이면 문자열이 필드에 오른쪽 맞춤되고, 필드 너비가 음수 값이면 왼쪽 맞춤됩니다. 다음 예제에서는 날짜 값을 20자 필드에 왼쪽 맞춤하고, 소수 1자리의 10진수 값을 11자 필드에 오른쪽 맞춤합니다.

     [!code-csharp[Conceptual.Formatting.Overview#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/composite2.cs#22)]
     [!code-vb[Conceptual.Formatting.Overview#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/composite2.vb#22)]

     맞춤 문자열 구성 요소와 형식 문자열 구성 요소가 둘 다 있는 경우 맞춤 문자열 구성 요소가 우선합니다(예: `{0,-20:g}`).

복합 서식 지정에 대한 자세한 내용은 [Composite Formatting](../../../docs/standard/base-types/composite-formatting.md)을 참조하세요.

<a name="Custom"></a>

## <a name="custom-formatting-with-icustomformatter"></a>ICustomFormatter를 사용한 사용자 지정 형식 지정

두 복합 형식 지정 메서드( <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 및 <xref:System.Text.StringBuilder.AppendFormat%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType>)에 사용자 지정 형식을 지원하는 형식 공급자 매개 변수가 포함되어 있습니다. 이러한 형식 지정 메서드 중 하나를 호출하면 <xref:System.Type> 인터페이스를 나타내는 <xref:System.ICustomFormatter> 개체가 형식 공급자의 <xref:System.IFormatProvider.GetFormat%2A> 메서드에 전달됩니다. 그러면 <xref:System.IFormatProvider.GetFormat%2A> 메서드가 사용자 지정 형식 지정을 제공하는 <xref:System.ICustomFormatter> 구현을 반환합니다.

<xref:System.ICustomFormatter> 인터페이스에는 복합 형식 지정 메서드에 의해 자동으로 복합 형식 문자열의 각 형식 항목에 대해 한 번씩 호출되는 <xref:System.ICustomFormatter.Format%28System.String%2CSystem.Object%2CSystem.IFormatProvider%29>라는 메서드가 하나 있습니다. <xref:System.ICustomFormatter.Format%28System.String%2CSystem.Object%2CSystem.IFormatProvider%29> 메서드에는 세 개의 매개 변수 즉, 형식 항목의 `formatString` 인수를 나타내는 형식 문자열, 형식을 지정할 개체 및 형식 지정 서비스를 제공하는 <xref:System.IFormatProvider> 개체가 포함되어 있습니다. 일반적으로 <xref:System.ICustomFormatter> 를 구현하는 클래스는 <xref:System.IFormatProvider>도 구현하여 이 마지막 매개 변수가 사용자 지정 형식 지정 클래스를 참조하도록 합니다. 이 메서드는 형식을 지정할 개체의 사용자 지정 형식 문자열 표현을 반환합니다. 이 메서드가 개체의 형식을 지정할 수 없는 경우에는 null 참조(Visual Basic의 경우`Nothing` )가 반환되어야 합니다.

다음 예제에서는 정수 값을 뒤에 공백이 오는 두 자리 16진수 값 시퀀스로 표시하는 <xref:System.ICustomFormatter> 라는 `ByteByByteFormatter` 구현을 제공합니다.

[!code-csharp[Conceptual.Formatting.Overview#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/icustomformatter1.cs#15)]
[!code-vb[Conceptual.Formatting.Overview#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/icustomformatter1.vb#15)]

다음 예제에서는 `ByteByByteFormatter` 클래스를 사용하여 정수 값의 형식을 지정합니다. 예제에서는 <xref:System.ICustomFormatter.Format%2A?displayProperty=nameWithType> 메서드는 두 번째 <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 메서드 호출에서 두 번 이상 호출되고 <xref:System.Globalization.NumberFormatInfo> 메서드가 "N0" 형식 문자열을 인식하지 못하고 null 참조(Visual Basic의 경우`ByteByByteFormatter.Format` )를 반환하기 때문에 세 번째 메서드 호출에서는 기본`Nothing` )와 동일한 형식 지정자에 대한 지원.

[!code-csharp[Conceptual.Formatting.Overview#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/icustomformatter1.cs#16)]
[!code-vb[Conceptual.Formatting.Overview#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/icustomformatter1.vb#16)]

<a name="RelatedTopics"></a>

## <a name="related-topics"></a>관련 항목

|제목|정의|
|-----------|----------------|
|[Standard Numeric Format Strings](../../../docs/standard/base-types/standard-numeric-format-strings.md)|숫자 값의 일반적으로 사용되는 문자열 표현을 만드는 표준 형식 문자열에 대해 설명합니다.|
|[Custom Numeric Format Strings](../../../docs/standard/base-types/custom-numeric-format-strings.md)|숫자 값의 애플리케이션별 형식을 만드는 사용자 지정 형식 문자열에 대해 설명합니다.|
|[표준 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)|<xref:System.DateTime> 값의 일반적으로 사용되는 문자열 표현을 만드는 표준 형식 문자열에 대해 설명합니다.|
|[사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)|<xref:System.DateTime> 값의 애플리케이션별 형식을 만드는 사용자 지정 형식 문자열에 대해 설명합니다.|
|[표준 TimeSpan 서식 문자열](../../../docs/standard/base-types/standard-timespan-format-strings.md)|시간 간격의 일반적으로 사용되는 문자열 표현을 만드는 표준 형식 문자열에 대해 설명합니다.|
|[사용자 지정 TimeSpan 서식 문자열](../../../docs/standard/base-types/custom-timespan-format-strings.md)|시간 간격의 애플리케이션별 형식을 만드는 사용자 지정 형식 문자열에 대해 설명합니다.|
|[Enumeration Format Strings](../../../docs/standard/base-types/enumeration-format-strings.md)|열거형 값의 문자열 표현을 만드는 데 사용되는 표준 형식 문자열에 대해 설명합니다.|
|[복합 형식 지정](../../../docs/standard/base-types/composite-formatting.md)|문자열에 형식이 지정된 하나 이상의 값을 포함시키는 방법에 대해 설명합니다. 그런 후 해당 문자열을 콘솔에 표시하거나 스트림에 쓸 수 있습니다.|
|[서식 지정 작업 수행](../../../docs/standard/base-types/performing-formatting-operations.md)|특정 형식 지정 작업을 수행하기 위한 단계별 지침을 제공하는 항목을 나열합니다.|
|[Parsing Strings](../../../docs/standard/base-types/parsing-strings.md)|개체를 해당 개체의 문자열 표현으로 표시되는 값으로 초기화하는 방법에 대해 설명합니다. 구문 분석은 형식 지정의 역순으로 진행됩니다.|

<a name="Reference"></a>

## <a name="reference"></a>참조

- <xref:System.IFormattable?displayProperty=nameWithType>
- <xref:System.IFormatProvider?displayProperty=nameWithType>
- <xref:System.ICustomFormatter?displayProperty=nameWithType>
