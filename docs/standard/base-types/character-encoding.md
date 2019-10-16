---
title: .NET의 문자 인코딩
description: .NET에서 문자 인코딩 및 디코딩에 대해 알아봅니다.
ms.date: 12/22/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- encoding, understanding
- encoding, choosing
- encoding, fallback strategy
ms.assetid: bf6d9823-4c2d-48af-b280-919c5af66ae9
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: 248628d9907a3984b2c06e5f2f3a1e5c2faa2a67
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040543"
---
# <a name="character-encoding-in-net"></a>.NET의 문자 인코딩

문자는 다양한 방법으로 표현할 수 있는 추상 엔터티입니다. 문자 인코딩은 지원되는 문자 집합의 각 문자와 해당 문자를 나타내는 일부 값의 쌍을 만드는 시스템입니다. 예를 들어 모르스 부호는 로마 알파벳의 각 문자와 전화선을 통한 전송에 적합한 점과 대시 패턴의 쌍을 만드는 문자 인코딩입니다. 컴퓨터의 문자 인코딩은 지원되는 문자 집합의 각 문자와 해당 문자를 나타내는 숫자 값의 쌍을 만듭니다. 문자 인코딩에는 다음 두 가지 구성 요소가 있습니다.

- 인코더 - 문자 시퀀스를 숫자 값(바이트) 시퀀스로 변환합니다.

- 디코더 - 바이트 시퀀스를 문자 시퀀스로 변환합니다.

문자 인코딩은 인코더와 디코더가 작동하는 규칙을 설명합니다. 예를 들어 <xref:System.Text.UTF8Encoding> 클래스는 1-4바이트를 사용하여 단일 유니코드 문자를 나타내는 UTF-8(8비트 유니코드 변환 형식)으로 인코딩 및 디코딩하는 규칙을 설명합니다. 인코딩 및 디코딩에 유효성 검사가 포함될 수도 있습니다. 예를 들어 <xref:System.Text.UnicodeEncoding> 클래스는 모든 서로게이트를 검사하여 유효한 서로게이트 쌍을 구성하는지 확인합니다. 서로게이트 쌍은 코드 포인트가 U+D800에서 U+DBFF 사이의 범위인 문자와 코드 포인트가 U+DC00에서 U+DFFF 사이의 범위인 문자가 이 순서로 결합되어 구성됩니다.  대체(fallback) 전략은 인코더에서 잘못된 문자를 처리하는 방법 또는 디코더에서 잘못된 바이트를 처리하는 방법을 결정합니다.

> [!WARNING]
> .NET 인코딩 클래스는 문자 데이터를 저장 및 변환하는 방법을 제공합니다. 이진 데이터를 문자열 형식으로 저장하는 데 사용하면 안 됩니다. 사용되는 인코딩에 따라 인코딩 클래스를 통해 이진 데이터를 문자열로 변환할 때 예기치 못한 동작이 발생하고 부정확하거나 손상된 데이터가 생성될 수 있습니다. 이진 데이터를 문자열 형식으로 변환하려면 <xref:System.Convert.ToBase64String%2A?displayProperty=nameWithType> 메서드를 사용합니다.

.NET에서는 UTF-16 인코딩(<xref:System.Text.UnicodeEncoding> 클래스로 표시)을 사용하여 문자와 문자열을 나타냅니다. 공용 언어 런타임을 대상으로 하는 애플리케이션은 인코더를 사용하여 공용 언어 런타임에서 지원하는 유니코드 문자 표현을 다른 인코딩 체계에 매핑합니다. 디코더를 사용하여 문자를 비유니코드 인코딩에서 유니코드로 매핑합니다.

이 항목은 다음 섹션으로 구성되어 있습니다.

- [.NET의 인코딩](../../../docs/standard/base-types/character-encoding.md#Encodings)

- [인코딩 클래스 선택](../../../docs/standard/base-types/character-encoding.md#Selecting)

- [인코딩 개체 사용](../../../docs/standard/base-types/character-encoding.md#Using)

- [대체(fallback) 전략 선택](../../../docs/standard/base-types/character-encoding.md#FallbackStrategy)

- [Implementing a Custom Fallback Strategy](../../../docs/standard/base-types/character-encoding.md#Custom)

<a name="Encodings"></a>

## <a name="encodings-in-net"></a>.NET의 인코딩

.NET의 모든 문자 인코딩 클래스는 모든 문자 인코딩에 공통된 기능을 정의하는 추상 클래스인 <xref:System.Text.Encoding?displayProperty=nameWithType> 클래스에서 상속됩니다. .NET에서 구현된 개별 인코딩 개체에 액세스하려면 다음을 수행합니다.

- .NET에서 사용할 수 있는 표준 문자 인코딩(ASCII, UTF-7, UTF-8, UTF-16 및 UTF-32)을 나타내는 개체를 반환하는 <xref:System.Text.Encoding> 클래스의 정적 속성을 사용합니다. 예를 들어 <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType> 속성은 <xref:System.Text.UnicodeEncoding> 개체를 반환합니다. 각 개체는 교체 대체(fallback)를 사용하여 인코딩할 수 없는 문자열과 디코딩할 수 없는 바이트를 처리합니다. 자세한 내용은 [Replacement Fallback](../../../docs/standard/base-types/character-encoding.md#Replacement) 섹션을 참조하세요.

- 인코딩의 클래스 생성자를 호출합니다. 이런 방식으로 ASCII, UTF-7, UTF-8, UTF-16 및 UTF-32 인코딩에 대한 개체를 인스턴스화할 수 있습니다. 기본적으로 각 개체는 교체 대체(fallback)를 사용하여 인코딩할 수 없는 문자열과 디코딩할 수 없는 바이트를 처리하지만 대신 예외가 발생하도록 지정할 수 있습니다. 자세한 내용은 [Replacement Fallback](../../../docs/standard/base-types/character-encoding.md#Replacement) 및 [Exception Fallback](../../../docs/standard/base-types/character-encoding.md#Exception) 섹션을 참조하세요.

- <xref:System.Text.Encoding.%23ctor%28System.Int32%29?displayProperty=nameWithType> 생성자를 호출하고 인코딩을 나타내는 정수를 전달합니다. 표준 인코딩 개체는 교체 대체(fallback)를 사용하고, 코드 페이지와 DBCS(더블바이트 문자 집합) 인코딩 개체는 최적 맞춤 대체(fallback)를 사용하여 인코딩할 수 없는 문자열과 디코딩할 수 없는 바이트를 처리합니다. 자세한 내용은 [Best-Fit Fallback](../../../docs/standard/base-types/character-encoding.md#BestFit) 섹션을 참조하세요.

- .NET에서 사용할 수 있는 표준, 코드 페이지 또는 DBCS 인코딩을 반환하는 <xref:System.Text.Encoding.GetEncoding%2A?displayProperty=nameWithType> 메서드를 호출합니다. 오버로드를 통해 인코더와 디코더 둘 다에 대체(fallback) 개체를 지정할 수 있습니다.

> [!NOTE]
> 유니코드 표준은 지원되는 모든 스크립트의 각 문자에 코드 포인트(숫자)와 이름을 할당합니다. 예를 들어 "A" 문자는 코드 포인트 U+0041 및 이름 "LATIN CAPITAL LETTER A"로 표시됩니다. UTF(유니코드 변환 형식) 인코딩은 코드 포인트를 하나 이상의 바이트 시퀀스로 인코딩하는 방법을 정의합니다. 유니코드 인코딩 체계를 사용하면 모든 문자 집합의 문자를 단일 인코딩으로 나타낼 수 있으므로 국제 애플리케이션 개발이 간소화됩니다. 애플리케이션 개발자가 더 이상 특정 언어나 쓰기 시스템을 위한 문자를 생성하는 데 사용된 인코딩 체계를 추적할 필요가 없으며 손상 없이 전 세계 시스템 간에 데이터를 공유할 수 있습니다.
>
> .NET에서는 유니코드 표준에서 정의된 세 가지 인코딩을 지원합니다. UTF-8, UTF-16 및 UTF-32. 자세한 내용은 [유니코드 홈페이지](https://www.unicode.org/)에서 유니코드 표준을 참조하세요.

<xref:System.Text.Encoding.GetEncodings%2A?displayProperty=nameWithType> 메서드를 호출하여 .NET에서 사용할 수 있는 모든 인코딩에 대한 정보를 검색할 수 있습니다. .NET에서는 다음 표에 나열된 문자 인코딩 시스템을 지원합니다.

|인코딩|클래스|설명|장점/단점|
|--------------|-----------|-----------------|-------------------------------|
|ASCII|<xref:System.Text.ASCIIEncoding>|바이트의 하위 7비트를 사용하여 제한된 범위의 문자를 인코딩합니다.|이 인코딩은 U+0000에서 U+007F 사이의 문자 값만 지원하므로 대부분의 경우 국제화된 애플리케이션에는 적합하지 않습니다.|
|UTF-7|<xref:System.Text.UTF7Encoding>|7비트 ASCII 문자 시퀀스로 문자를 나타냅니다. 비 ASCII 유니코드 문자는 ASCII 문자의 이스케이프 시퀀스로 표시됩니다.|UTF-7은 전자 메일 및 뉴스 그룹 프로토콜과 같은 프로토콜을 지원합니다. 그러나 UTF-7은 특별히 안전하거나 강력하지 않습니다. 경우에 따라 1비트를 변경해도 전체 UTF-7 문자열의 해석이 완전히 바뀔 수 있습니다. 다른 UTF-7 문자열이 동일한 텍스트를 인코딩할 수도 있습니다. 비 ASCII 문자를 포함하는 시퀀스의 경우 UTF-7에서 UTF-8보다 많은 공간이 필요하며 인코딩/디코딩 속도가 느려집니다. 따라서 가능하면 UTF-7 대신 UTF-8을 사용해야 합니다.|
|UTF-8|<xref:System.Text.UTF8Encoding>|각 유니코드 코드 포인트를 1-4바이트의 시퀀스로 나타냅니다.|UTF-8은 8비트 데이터 크기를 지원하며 기존의 많은 운영 체제에서 제대로 작동합니다. ASCII 문자 범위의 경우 UTF-8은 ASCII 인코딩과 동일하며 광범위한 문자 집합을 허용합니다. 그러나 CJK(중국어-일본어-한국어) 스크립트의 경우 UTF-8에서 각 문자에 대해 3바이트를 요구할 수 있으며 데이터 크기가 UTF-16보다 커질 수 있습니다. 때로는 HTML 태그와 같은 ASCII 데이터의 양이 CJK 범위의 크기 증가와 관련이 있습니다.|
|UTF-16|<xref:System.Text.UnicodeEncoding>|각 유니코드 코드 포인트를 한두 개의 16비트 정수 시퀀스로 나타냅니다. 가장 일반적인 유니코드 문자에는 UTF-16 코드 포인트 한 개만 있으면 됩니다. 단, 유니코드 보조 문자(U+10000 이상)에는 UTF-16 서로게이트 코드 포인트 두 개가 필요합니다. little-endian 및 big-endian 바이트 순서가 둘 다 지원됩니다.|UTF-16 인코딩은 공용 언어 런타임에서 <xref:System.Char> 및 <xref:System.String> 값을 나타내는 데 사용되며 Windows 운영 체제에서 `WCHAR` 값을 나타내는 데 사용됩니다.|
|UTF-32|<xref:System.Text.UTF32Encoding>|각 유니코드 코드 포인트를 32비트 정수 한 개로 나타냅니다. little-endian 및 big-endian 바이트 순서가 둘 다 지원됩니다.|UTF-32 인코딩은 인코딩된 공간이 너무 중요한 운영 체제에서 애플리케이션이 UTF-16 인코딩의 서로게이트 코드 포인트 동작을 방지하려는 경우에 사용됩니다. 디스플레이에 렌더링되는 단일 문자 모양은 여전히 둘 이상의 UTF-32 문자로 인코딩될 수 있습니다.|
|ANSI/ISO 인코딩||다양한 코드 페이지에 대해 지원됩니다. Windows 운영 체제에서 코드 페이지는 특정 언어 또는 언어 그룹을 지원하는 데 사용됩니다. .NET에서 지원되는 코드 페이지를 나열하는 표는 <xref:System.Text.Encoding> 클래스를 참조하세요. <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> 메서드를 호출하여 특정 코드 페이지에 대한 인코딩 개체를 검색할 수 있습니다.|코드 페이지에는 256개의 코드 포인트가 포함되며 0부터 시작합니다. 대부분의 코드 페이지에서 코드 포인트 0-127은 ASCII 문자 집합을 나타내고, 코드 포인트 128-255는 코드 페이지마다 상당한 차이가 있습니다. 예를 들어 코드 페이지 1252는 영어, 독일어, 프랑스어 등 라틴 문자 쓰기 시스템에 대한 문자를 제공합니다. 코드 페이지 1252의 마지막 128개 코드 포인트에는 악센트 문자가 포함됩니다. 코드 페이지 1253은 그리스어 문자 체계에 필요한 문자 코드를 제공합니다. 코드 페이지 1253의 마지막 128개 코드 포인트에는 그리스어 문자가 포함됩니다. 따라서, ANSI 코드 페이지를 사용하는 애플리케이션은 참조된 코드 페이지를 나타내는 식별자를 포함하지 않는 한 동일한 텍스트 스트림에 그리스어와 독일어를 저장할 수 없습니다.|
|DBCS(더블바이트 문자 집합) 인코딩||256자가 넘는 문자를 포함하는 언어(예: 중국어, 일본어 및 한국어)를 지원합니다. DBCS에서는 한 쌍의 코드 포인트(더블바이트)가 각 문자를 나타냅니다. <xref:System.Text.Encoding.IsSingleByte%2A?displayProperty=nameWithType> 속성은 DBCS 인코딩에 대해 `false` 를 반환합니다. <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> 메서드를 호출하여 특정 DBCS에 대한 인코딩 개체를 검색할 수 있습니다.|DBCS에서는 한 쌍의 코드 포인트(더블바이트)가 각 문자를 나타냅니다. 애플리케이션에서 DBCS 데이터를 처리할 때 DBCS 문자의 첫 번째 바이트(선행 바이트)는 바로 뒤에 오는 후행 바이트와 함께 처리됩니다. 한 쌍의 더블바이트 코드 포인트가 코드 페이지에 따라 서로 다른 문자를 나타낼 수 있기 때문에 이 구성표에서는 여전히 동일한 데이터 스트림에 두 언어(예: 일본어 및 중국어)를 함께 사용할 수 없습니다.|

이러한 인코딩을 통해 유니코드 문자는 물론 레거시 애플리케이션에서 가장 일반적으로 사용되는 인코딩으로 작업할 수 있습니다. 또한 <xref:System.Text.Encoding> 에서 파생되는 클래스를 정의하고 해당 멤버를 재정의하여 사용자 지정 인코딩을 만들 수 있습니다.

### <a name="platform-notes-net-core"></a>플랫폼 참고 사항: .NET Core

기본적으로 .NET Core에서는 코드 페이지 28591 이외의 코드 페이지 인코딩 및 유니코드 인코딩(예: UTF-8 및 UTF-16)을 사용할 수 없습니다. 그러나 .NET을 대상으로 하는 표준 Windows 앱에 있는 코드 페이지 인코딩을 해당 앱에 추가할 수 있습니다. 자세한 내용은 <xref:System.Text.CodePagesEncodingProvider> 항목을 참조하세요.

<a name="Selecting"></a>

## <a name="selecting-an-encoding-class"></a>인코딩 클래스 선택

애플리케이션에서 사용할 인코딩을 선택할 수 있는 경우 유니코드 인코딩인 <xref:System.Text.UTF8Encoding> 또는 <xref:System.Text.UnicodeEncoding>를 사용해야 합니다. .NET에서는 세 번째 유니코드 인코딩인 <xref:System.Text.UTF32Encoding>도 지원합니다.

ASCII 인코딩(<xref:System.Text.ASCIIEncoding>)을 사용하려는 경우 <xref:System.Text.UTF8Encoding> 을 대신 사용합니다. 두 인코딩은 ASCII 문자 집합에서 동일하지만 <xref:System.Text.UTF8Encoding> 에는 다음과 같은 이점이 있습니다.

- <xref:System.Text.ASCIIEncoding> 은 U+0000에서 U+007F 사이의 유니코드 문자 값만 지원하는 반면, 모든 유니코드 문자를 나타낼 수 있습니다.

- 오류 검색 및 향상된 보안을 제공합니다.

- 최대한 빠르도록 조정되었으며 다른 인코딩보다 더 빨라야 합니다. 완전히 ASCII인 콘텐츠의 경우에도 <xref:System.Text.UTF8Encoding> 으로 수행된 작업이 <xref:System.Text.ASCIIEncoding>으로 수행된 작업보다 더 빠릅니다.

<xref:System.Text.ASCIIEncoding> 은 레거시 애플리케이션에만 사용해야 합니다. 그러나 레거시 애플리케이션의 경우에도 다음과 같은 이유로 <xref:System.Text.UTF8Encoding> 이 더 적합할 수 있습니다(기본 설정 가정).

- 애플리케이션에 엄격하게 ASCII가 아닌 콘텐츠가 있고 <xref:System.Text.ASCIIEncoding>으로 인코딩하는 경우 각각의 비 ASCII 문자가 물음표(?)로 인코딩됩니다. 그런 후에 애플리케이션에서 이 데이터를 디코딩하면 정보가 손실됩니다.

- 애플리케이션에 엄격하게 ASCII가 아닌 콘텐츠가 있고 <xref:System.Text.UTF8Encoding>으로 인코딩하는 경우 결과를 ASCII로 해석하면 인식할 수 없는 것처럼 보입니다. 그러나 애플리케이션이 UTF-8 디코더를 사용하여 이 데이터를 디코딩하면 데이터가 성공적으로 라운드트립을 수행합니다.

웹 애플리케이션에서는 웹 요청에 대한 응답으로 클라이언트에 전송되는 문자가 클라이언트에서 사용되는 인코딩을 반영해야 합니다. 대부분의 경우 사용자에게 필요한 인코딩으로 텍스트를 표시하기 위해 <xref:System.Web.HttpResponse.ContentEncoding%2A?displayProperty=nameWithType> 속성을 <xref:System.Web.HttpRequest.ContentEncoding%2A?displayProperty=nameWithType> 속성에서 반환된 값으로 설정해야 합니다.

<a name="Using"></a>

## <a name="using-an-encoding-object"></a>인코딩 개체 사용

인코더는 문자의 문자열(가장 일반적으로 유니코드 문자)을 해당 숫자(바이트)로 변환합니다. 예를 들어 콘솔에 표시될 수 있도록 ASCII 인코더를 사용하여 유니코드 문자를 ASCII로 변환할 수 있습니다. 변환을 수행하려면 <xref:System.Text.Encoding.GetBytes%2A?displayProperty=nameWithType> 메서드를 호출합니다. 인코딩을 수행하기 전에 인코딩된 문자를 저장하는 데 필요한 바이트 수를 확인하려는 경우 <xref:System.Text.Encoding.GetByteCount%2A> 메서드를 호출할 수 있습니다.

다음 예제에서는 싱글바이트 배열을 사용하여 두 개의 별도 작업에서 문자열을 인코딩합니다. 바이트 배열에서 ASCII로 인코딩된 다음 바이트 집합의 시작 위치를 나타내는 인덱스를 유지 관리합니다. <xref:System.Text.ASCIIEncoding.GetByteCount%28System.String%29?displayProperty=nameWithType> 메서드를 호출하여 바이트 배열이 인코딩된 문자열을 포함하기에 충분히 큰지 확인합니다. 그런 다음 <xref:System.Text.ASCIIEncoding.GetBytes%28System.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Byte%5B%5D%2CSystem.Int32%29?displayProperty=nameWithType> 메서드를 호출하여 문자열의 문자를 인코딩합니다.

[!code-csharp[Conceptual.Encoding#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/getbytes1.cs#8)]
[!code-vb[Conceptual.Encoding#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/getbytes1.vb#8)]

디코더는 특정 문자 인코딩을 반영하는 바이트 배열을 문자 배열 또는 문자열의 문자 집합으로 변환합니다. 바이트 배열을 문자 배열로 디코딩하려면 <xref:System.Text.Encoding.GetChars%2A?displayProperty=nameWithType> 메서드를 호출합니다. 바이트 배열을 문자열로 디코딩하려면 <xref:System.Text.Encoding.GetString%2A> 메서드를 호출합니다. 디코딩을 수행하기 전에 디코딩된 바이트를 저장하는 데 필요한 문자 수를 확인하려는 경우 <xref:System.Text.Encoding.GetCharCount%2A> 메서드를 호출할 수 있습니다.

다음 예제에서는 세 개의 문자열을 인코딩한 후 단일 문자 배열로 디코딩합니다. 문자 배열에서 디코딩된 다음 문자 집합의 시작 위치를 나타내는 인덱스를 유지 관리합니다. <xref:System.Text.ASCIIEncoding.GetCharCount%2A> 메서드를 호출하여 문자 배열이 디코딩된 모든 문자를 포함하기에 충분히 큰지 확인합니다. 그런 다음 <xref:System.Text.ASCIIEncoding.GetChars%28System.Byte%5B%5D%2CSystem.Int32%2CSystem.Int32%2CSystem.Char%5B%5D%2CSystem.Int32%29?displayProperty=nameWithType> 메서드를 호출하여 바이트 배열을 디코딩합니다.

[!code-csharp[Conceptual.Encoding#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/getchars1.cs#9)]
[!code-vb[Conceptual.Encoding#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/getchars1.vb#9)]

<xref:System.Text.Encoding> 에서 파생된 클래스의 인코딩 및 디코딩 메서드는 전체 데이터 집합에서 작동하도록 설계되었습니다. 즉, 인코딩 또는 디코딩할 모든 데이터가 단일 메서드 호출에서 제공됩니다. 그러나 스트림으로 데이터가 제공되고, 인코딩 또는 디코딩할 데이터를 별도의 읽기 작업에서만 사용할 수 있는 경우도 있습니다. 이 경우 인코딩 또는 디코딩 작업이 이전 호출에서 저장된 상태를 기억해야 합니다. <xref:System.Text.Encoder> 및 <xref:System.Text.Decoder> 에서 파생된 클래스의 메서드는 여러 메서드 호출에 걸쳐 있는 인코딩 및 디코딩 작업을 처리할 수 있습니다.

특정 인코딩에 대한 <xref:System.Text.Encoder> 개체는 해당 인코딩의 <xref:System.Text.Encoding.GetEncoder%2A?displayProperty=nameWithType> 속성에서 확인할 수 있습니다. 특정 인코딩에 대한 <xref:System.Text.Decoder> 개체는 해당 인코딩의 <xref:System.Text.Encoding.GetDecoder%2A?displayProperty=nameWithType> 속성에서 확인할 수 있습니다. 디코딩 작업의 경우 <xref:System.Text.Decoder> 에서 파생된 클래스에 <xref:System.Text.Decoder.GetChars%2A?displayProperty=nameWithType> 메서드가 포함되지만 <xref:System.Text.Encoding.GetString%2A?displayProperty=nameWithType>에 해당하는 메서드가 없습니다.

다음 예제에서는 유니코드 바이트 배열 디코딩에 <xref:System.Text.Encoding.GetChars%2A?displayProperty=nameWithType> 및 <xref:System.Text.Decoder.GetChars%2A?displayProperty=nameWithType> 메서드를 사용하는 경우의 차이점을 보여 줍니다. 이 예제에서는 일부 유니코드 문자를 포함하는 문자열을 파일로 인코딩한 다음 두 개의 디코딩 메서드를 사용하여 한 번에 10바이트씩 디코딩합니다. 10번째 및 11번째 바이트에서 서로게이트 쌍이 발생하기 때문에 별도 메서드 호출에서 디코딩됩니다. 출력에서 볼 수 있듯이 <xref:System.Text.Encoding.GetChars%2A?displayProperty=nameWithType> 메서드는 바이트를 올바르게 디코딩할 수 없으며, 대신 U+FFFD(REPLACEMENT CHARACTER)로 바꿉니다. 반면, <xref:System.Text.Decoder.GetChars%2A?displayProperty=nameWithType> 메서드는 바이트 배열을 성공적으로 디코딩하여 원래 문자열을 가져올 수 있습니다.

[!code-csharp[Conceptual.Encoding#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/stream1.cs#10)]
[!code-vb[Conceptual.Encoding#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/stream1.vb#10)]

<a name="FallbackStrategy"></a>

## <a name="choosing-a-fallback-strategy"></a>대체(fallback) 전략 선택

메서드가 문자를 인코딩 또는 디코딩하려고 하는데 매핑이 없는 경우 실패한 매핑의 처리 방법을 결정하는 대체(fallback) 전략을 구현해야 합니다. 다음 세 가지 유형의 대체 (fallback) 전략이 있습니다.

- Best-Fit Fallback

- Replacement Fallback

- Exception Fallback

> [!IMPORTANT]
> 인코딩 작업의 가장 일반적인 문제는 유니코드 문자를 특정 코드 페이지 인코딩에 매핑할 수 없는 경우에 발생합니다. 디코딩 작업의 가장 일반적인 문제는 잘못된 바이트 시퀀스를 유효한 유니코드 문자로 변환할 수 없는 경우에 발생합니다. 이러한 이유로 특정 인코딩 개체에서 사용하는 대체(fallback) 전략을 알고 있어야 합니다. 가능하면 개체를 인스턴스화할 때 인코딩 개체에서 사용할 대체(fallback) 전략을 지정해야 합니다.

<a name="BestFit"></a>

### <a name="best-fit-fallback"></a>Best-Fit Fallback

대상 인코딩에 문자와 정확히 일치하는 항목이 없을 경우 인코더가 유사한 문자에 매핑하려고 시도할 수 있습니다. 최적 대체(fallback)는 주로 디코딩 문제가 아니라 인코딩 문제입니다. 성공적으로 유니코드에 매핑할 수 없는 문자가 포함된 코드 페이지는 거의 없습니다. 최적 대체(fallback)는 <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> 및 <xref:System.Text.Encoding.GetEncoding%28System.String%29?displayProperty=nameWithType> 오버로드를 통해 검색되는 코드 페이지 및 더블바이트 문자 집합 인코딩의 기본값입니다.

> [!NOTE]
> 이론적으로 .NET에서 제공되는 유니코드 인코딩 클래스(<xref:System.Text.UTF8Encoding>, <xref:System.Text.UnicodeEncoding> 및 <xref:System.Text.UTF32Encoding>)는 모든 문자 집합의 모든 문자를 지원하므로 최적 대체(fallback) 문제를 제거하는 데 사용할 수 있습니다.

최적 전략은 코드 페이지마다 다릅니다. 예를 들어 일부 코드 페이지에서는 전자 라틴 문자가 더 일반적인 반자 라틴 문자에 매핑됩니다. 다른 코드 페이지에서는 이 매핑이 수행되지 않습니다. 적극적인 최적 전략에서도 일부 인코딩의 일부 문자는 상상할 수 있는 최적 항목이 없습니다. 예를 들어 중국어 표의 문자에는 코드 페이지 1252에 적합한 매핑이 없습니다. 이 경우 대체 문자열이 사용됩니다. 기본적으로 이 문자열은 단일 QUESTION MARK(U+003F)입니다.

> [!NOTE]
> 최적 전략은 자세히 문서화되지 않습니다. 그러나 여러 가지 코드 페이지가 [유니코드 컨소시엄](https://www.unicode.org/Public/MAPPINGS/VENDORS/MICSFT/WindowsBestFit/) 웹 사이트에서 문서화됩니다. 매핑 파일을 해석하는 방법에 대한 설명은 해당 폴더의 **readme.txt** 파일을 검토하세요.

다음 예제에서는 코드 페이지 1252(서유럽 언어에 대한 Windows 코드 페이지)를 사용하여 최적 매핑과 해당 결점을 보여 줍니다. <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=nameWithType> 메서드는 코드 페이지 1252에 대한 인코딩 개체를 검색하는 데 사용됩니다. 기본적으로 지원하지 않는 유니코드 문자에 대해 최적 매핑을 사용합니다. 이 예제에서는 CIRCLED LATIN CAPITAL LETTER S(U+24C8), SUPERSCRIPT FIVE(U+2075) 및 INFINITY(U+221E)라는 3개의 비 ASCII 문자가 공백으로 구분되어 포함된 문자열을 인스턴스화합니다. 예제의 출력에서 볼 수 있듯이, 문자열을 인코딩할 때 공백이 아닌 원래 문자 3자가 QUESTION MARK(U+003F), DIGIT FIVE(U+0035) 및 DIGIT EIGHT(U+0038)으로 대체됩니다. DIGIT EIGHT은 지원되지 않는 INFINITY 문자에 대한 특히 부적절한 대체이고, QUESTION MARK는 원래 문자에 사용할 수 있는 매핑이 없음을 나타냅니다.

[!code-csharp[Conceptual.Encoding#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1.cs#1)]
[!code-vb[Conceptual.Encoding#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1.vb#1)]

최적 매핑은 유니코드 데이터를 코드 페이지 데이터로 인코딩하는 <xref:System.Text.Encoding> 개체에 대한 기본 동작이며, 이 동작에 의존하는 레거시 애플리케이션이 있습니다. 그러나 대부분의 새 애플리케이션은 보안상의 이유로 최적 동작을 피해야 합니다. 예를 들어 애플리케이션에서 최적 인코딩을 통해 도메인 이름을 넣으면 안 됩니다.

> [!NOTE]
> 인코딩에 대한 사용자 지정 최적 대체(fallback) 매핑을 구현할 수도 있습니다. 자세한 내용은 [Implementing a Custom Fallback Strategy](../../../docs/standard/base-types/character-encoding.md#Custom) 섹션을 참조하세요.

최적 대체(fallback)가 인코딩 개체에 대한 기본값인 경우 <xref:System.Text.Encoding> 또는 <xref:System.Text.Encoding.GetEncoding%28System.Int32%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> 오버로드를 호출하여 <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> 개체를 검색할 때 다른 대체(fallback) 전략을 선택할 수 있습니다. 다음 섹션에는 코드 페이지 1252로 매핑할 수 없는 각 문자를 별표(*)로 대체하는 예제가 포함되어 있습니다.

[!code-csharp[Conceptual.Encoding#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1a.cs#3)]
[!code-vb[Conceptual.Encoding#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1a.vb#3)]

<a name="Replacement"></a>

### <a name="replacement-fallback"></a>Replacement Fallback

대상 구성표에 문자와 정확히 일치하는 항목이 없고 매핑할 수 있는 적절한 문자가 없는 경우 애플리케이션에서 대체 문자 또는 문자열을 지정할 수 있습니다. 이는 유니코드 디코더의 기본 동작으로, 디코딩할 수 없는 모든 2바이트 시퀀스를 REPLACEMENT_CHARACTER(U+FFFD)로 대체합니다. <xref:System.Text.ASCIIEncoding> 클래스의 기본 동작이기도 하며, 인코딩 또는 디코딩할 수 없는 각 문자를 물음표로 대체합니다. 다음 예제에서는 이전 예제의 유니코드 문자열에 대한 문자 대체를 보여 줍니다. 출력에서 볼 수 있듯이, ASCII 바이트 값으로 디코딩할 수 없는 각 문자는 물음표의 ASCII 코드인 0x3F로 대체됩니다.

[!code-csharp[Conceptual.Encoding#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/replacementascii.cs#2)]
[!code-vb[Conceptual.Encoding#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/replacementascii.vb#2)]

.NET에는 문자가 인코딩 또는 디코딩 작업에서 정확히 매핑되지 않는 경우 대체 문자열로 바꾸는 <xref:System.Text.EncoderReplacementFallback> 및 <xref:System.Text.DecoderReplacementFallback> 클래스가 포함되어 있습니다. 기본적으로 이 대체 문자열은 물음표지만 클래스 생성자 오버로드를 호출하여 다른 문자열을 선택할 수 있습니다. 요구 사항은 아니지만 일반적으로 대체 문자열은 단일 문자입니다. 다음 예제에서는 별표(*)를 사용하는 <xref:System.Text.EncoderReplacementFallback> 개체를 대체 문자열로 인스턴스화하여 코드 페이지 1252 인코더의 동작을 변경합니다.

[!code-csharp[Conceptual.Encoding#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1a.cs#3)]
[!code-vb[Conceptual.Encoding#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1a.vb#3)]

> [!NOTE]
> 인코딩에 대한 대체 클래스를 구현할 수도 있습니다. 자세한 내용은 [Implementing a Custom Fallback Strategy](../../../docs/standard/base-types/character-encoding.md#Custom) 섹션을 참조하세요.

QUESTION MARK(U+003F) 외에도 일반적으로 유니코드 REPLACEMENT CHARACTER(U+FFFD)가 대체 문자열로 사용됩니다. 특히 유니코드 문자로 변환할 수 없는 바이트 시퀀스를 디코딩하는 경우에 해당합니다. 그러나 자유롭게 대체 문자열을 선택할 수 있으며 여러 문자를 포함할 수 있습니다.

<a name="Exception"></a>

### <a name="exception-fallback"></a>Exception Fallback

최적 대체(fallback) 또는 대체 문자열을 제공하는 대신 인코더가 문자 집합을 인코딩할 수 없는 경우 <xref:System.Text.EncoderFallbackException> 이 발생하고, 디코더가 바이트 배열을 디코딩할 수 없는 경우 <xref:System.Text.DecoderFallbackException> 이 발생할 수 있습니다. 인코딩 및 디코딩 작업에서 예외를 발생시키려면 <xref:System.Text.EncoderExceptionFallback> 메서드에 각각 <xref:System.Text.DecoderExceptionFallback> 개체 및 <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> 개체를 제공합니다. 다음 예제에서는 <xref:System.Text.ASCIIEncoding> 클래스를 사용한 예외 대체(fallback)를 보여 줍니다.

[!code-csharp[Conceptual.Encoding#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/exceptionascii.cs#4)]
[!code-vb[Conceptual.Encoding#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/exceptionascii.vb#4)]

> [!NOTE]
> 인코딩 작업에 대한 사용자 지정 예외 처리기를 구현할 수도 있습니다. 자세한 내용은 [Implementing a Custom Fallback Strategy](../../../docs/standard/base-types/character-encoding.md#Custom) 섹션을 참조하세요.

<xref:System.Text.EncoderFallbackException> 및 <xref:System.Text.DecoderFallbackException> 개체는 예외를 발생시킨 조건에 대한 다음 정보를 제공합니다.

- <xref:System.Text.EncoderFallbackException> 개체에는 인코딩할 수 없는 문자가 알 수 없는 서로게이트 쌍을 나타내는지(이 경우 메서드에서 <xref:System.Text.EncoderFallbackException.IsUnknownSurrogate%2A> 가 반환됨) 또는 알 수 없는 단일 문자를 나타내는지(이 경우 메서드에서 `true`가 반환됨)를 표시하는 `false`메서드가 포함됩니다. 서로게이트 쌍의 문자는 <xref:System.Text.EncoderFallbackException.CharUnknownHigh%2A?displayProperty=nameWithType> 및 <xref:System.Text.EncoderFallbackException.CharUnknownLow%2A?displayProperty=nameWithType> 속성에서 확인할 수 있습니다. 알 수 없는 단일 문자는 <xref:System.Text.EncoderFallbackException.CharUnknown%2A?displayProperty=nameWithType> 속성에서 확인할 수 있습니다. <xref:System.Text.EncoderFallbackException.Index%2A?displayProperty=nameWithType> 속성은 인코딩할 수 없는 첫 번째 문자가 발견된 문자열의 위치를 나타냅니다.

- <xref:System.Text.DecoderFallbackException> 개체에는 디코딩할 수 없는 바이트 배열을 반환하는 <xref:System.Text.DecoderFallbackException.BytesUnknown%2A> 속성이 포함됩니다. <xref:System.Text.DecoderFallbackException.Index%2A?displayProperty=nameWithType> 속성은 알 수 없는 바이트의 시작 위치를 나타냅니다.

<xref:System.Text.EncoderFallbackException> 및 <xref:System.Text.DecoderFallbackException> 개체는 예외에 대한 적절한 진단 정보를 제공하지만 인코딩 또는 디코딩 버퍼에 대한 액세스는 제공하지 않습니다. 따라서 인코딩 또는 디코딩 메서드 내에서 잘못된 데이터를 바꾸거나 수정할 수 있도록 허용하지 않습니다.

<a name="Custom"></a>

## <a name="implementing-a-custom-fallback-strategy"></a>Implementing a Custom Fallback Strategy

코드 페이지에서 내부적으로 구현되는 최적 매핑 외에도 .NET에는 대체(fallback) 전략을 구현하기 위한 다음과 같은 클래스가 포함되어 있습니다.

- <xref:System.Text.EncoderReplacementFallback> 및 <xref:System.Text.EncoderReplacementFallbackBuffer> 를 사용하여 인코딩 작업에서 문자를 바꿉니다.

- <xref:System.Text.DecoderReplacementFallback> 및 <xref:System.Text.DecoderReplacementFallbackBuffer> 를 사용하여 디코딩 작업에서 문자를 바꿉니다.

- <xref:System.Text.EncoderExceptionFallback> 및 <xref:System.Text.EncoderExceptionFallbackBuffer> 를 사용하여 문자를 인코딩할 수 없는 경우 <xref:System.Text.EncoderFallbackException> 을 발생시킵니다.

- <xref:System.Text.DecoderExceptionFallback> 및 <xref:System.Text.DecoderExceptionFallbackBuffer> 를 사용하여 문자를 디코딩할 수 없는 경우 <xref:System.Text.DecoderFallbackException> 을 발생시킵니다.

또한 다음 단계를 수행하여 최적 대체(fallback), 교체 대체(fallback) 또는 예외 대체(fallback)를 사용하는 사용자 지정 솔루션을 구현할 수 있습니다.

1. 인코딩 작업의 경우 <xref:System.Text.EncoderFallback> 에서 클래스를 파생시키고, 디코딩 작업의 경우 <xref:System.Text.DecoderFallback> 에서 클래스를 파생시킵니다.

2. 인코딩 작업의 경우 <xref:System.Text.EncoderFallbackBuffer> 에서 클래스를 파생시키고, 디코딩 작업의 경우 <xref:System.Text.DecoderFallbackBuffer> 에서 클래스를 파생시킵니다.

3. 예외 대체(fallback)의 경우 미리 정의된 <xref:System.Text.EncoderFallbackException> 및 <xref:System.Text.DecoderFallbackException> 클래스가 요구를 충족하지 않는 경우 <xref:System.Exception> 또는 <xref:System.ArgumentException>과 같은 예외 개체에서 클래스를 파생시킵니다.

### <a name="deriving-from-encoderfallback-or-decoderfallback"></a>EncoderFallback 또는 DecoderFallback에서 파생

사용자 지정 대체(fallback) 솔루션을 구현하려면 인코딩 작업의 경우 <xref:System.Text.EncoderFallback> 에서 상속하고 디코딩 작업의 경우 <xref:System.Text.DecoderFallback> 에서 상속하는 클래스를 만들어야 합니다. 이러한 클래스의 인스턴스는 <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> 메서드에 전달되며 인코딩 클래스와 대체(fallback) 구현 간의 중개자 역할을 합니다.

인코더 또는 디코더에 대한 사용자 지정 대체(fallback) 솔루션을 만드는 경우 다음과 같은 멤버를 구현해야 합니다.

- 최적, 교체 또는 예외 대체(fallback)가 단일 문자를 대체하기 위해 반환할 수 있는 최대 문자 수를 반환하는 <xref:System.Text.EncoderFallback.MaxCharCount%2A?displayProperty=nameWithType> 또는 <xref:System.Text.DecoderFallback.MaxCharCount%2A?displayProperty=nameWithType> 속성. 사용자 지정 예외 대체(fallback)의 경우 해당 값은 0입니다.

- 사용자 지정 <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> 또는 <xref:System.Text.DecoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> 구현을 반환하는 <xref:System.Text.EncoderFallbackBuffer> 또는 <xref:System.Text.DecoderFallbackBuffer> 메서드. 메서드는 성공적으로 인코딩할 수 없는 첫 번째 문자를 발견할 때 인코더에 의해 호출되거나 성공적으로 디코딩할 수 없는 첫 번째 바이트를 발견할 때 디코더에 의해 호출됩니다.

### <a name="deriving-from-encoderfallbackbuffer-or-decoderfallbackbuffer"></a>EncoderFallbackBuffer 또는 DecoderFallbackBuffer에서 파생

사용자 지정 대체(fallback) 솔루션을 구현하려면 인코딩 작업의 경우 <xref:System.Text.EncoderFallbackBuffer> 에서 상속하고 디코딩 작업의 경우 <xref:System.Text.DecoderFallbackBuffer> 에서 상속하는 클래스도 만들어야 합니다. 이러한 클래스의 인스턴스는 <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A> 및 <xref:System.Text.EncoderFallback> 클래스의 <xref:System.Text.DecoderFallback> 메서드에서 반환됩니다. <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> 메서드는 인코딩할 수 없는 첫 번째 문자를 발견할 때 인코더에 의해 호출되고, <xref:System.Text.DecoderFallback.CreateFallbackBuffer%2A?displayProperty=nameWithType> 메서드는 디코딩할 수 없는 바이트를 하나 이상 발견할 때 디코더에 의해 호출됩니다. <xref:System.Text.EncoderFallbackBuffer> 및 <xref:System.Text.DecoderFallbackBuffer> 클래스는 대체(fallback) 구현을 제공합니다. 각 인스턴스는 인코딩할 수 없는 문자 또는 디코딩할 수 없는 바이트를 대체하는 대체(fallback) 문자가 포함된 버퍼를 나타냅니다.

인코더 또는 디코더에 대한 사용자 지정 대체(fallback) 솔루션을 만드는 경우 다음과 같은 멤버를 구현해야 합니다.

- <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> 또는 <xref:System.Text.DecoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> 메서드. <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> 은 인코딩할 수 없는 문자 정보를 대체(fallback) 버퍼에 제공하기 위해 인코더에서 호출됩니다. 인코딩할 문자가 서로게이트 쌍일 수 있으므로 이 메서드는 오버로드됩니다. 하나의 오버로드에는 인코딩할 문자 및 문자열에서 해당 인덱스가 전달됩니다. 두 번째 오버로드에는 상위 및 하위 서로게이트와 문자열에서 해당 인덱스가 전달됩니다. <xref:System.Text.DecoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> 메서드는 디코딩할 수 없는 바이트 정보를 대체(fallback) 버퍼에 제공하기 위해 디코더에서 호출됩니다. 이 메서드에는 디코딩할 수 없는 바이트 배열 및 첫 번째 바이트의 인덱스가 전달됩니다. 대체(fallback) 버퍼가 최적 또는 교체 문자를 제공할 수 있는 경우 대체(fallback) 메서드에서 `true` 를 반환해야 하고, 그러지 않으면 `false`를 반환해야 합니다. 예외 대체(fallback)의 경우 대체(fallback) 메서드에서 예외를 발생시켜야 합니다.

- 인코더 또는 디코더가 대체(fallback) 버퍼에서 다음 문자를 가져오기 위해 반복적으로 호출하는 <xref:System.Text.EncoderFallbackBuffer.GetNextChar%2A?displayProperty=nameWithType> 또는 <xref:System.Text.DecoderFallbackBuffer.GetNextChar%2A?displayProperty=nameWithType> 메서드. 모든 대체(fallback) 문자가 반환되고 나면 메서드에서 U+0000을 반환해야 합니다.

- 대체(fallback) 버퍼에 남아 있는 문자 수를 반환하는 <xref:System.Text.EncoderFallbackBuffer.Remaining%2A?displayProperty=nameWithType> 또는 <xref:System.Text.DecoderFallbackBuffer.Remaining%2A?displayProperty=nameWithType> 속성

- 대체(fallback) 버퍼의 현재 위치를 이전 문자로 이동하는 <xref:System.Text.EncoderFallbackBuffer.MovePrevious%2A?displayProperty=nameWithType> 또는 <xref:System.Text.DecoderFallbackBuffer.MovePrevious%2A?displayProperty=nameWithType> 메서드

- 대체(fallback) 버퍼를 다시 초기화하는 <xref:System.Text.EncoderFallbackBuffer.Reset%2A?displayProperty=nameWithType> 또는 <xref:System.Text.DecoderFallbackBuffer.Reset%2A?displayProperty=nameWithType> 메서드

대체(fallback) 구현이 최적 대체(fallback) 또는 교체 대체(fallback)인 경우 <xref:System.Text.EncoderFallbackBuffer> 및 <xref:System.Text.DecoderFallbackBuffer> 에서 파생된 클래스가 두 개의 전용 인스턴스 필드(버퍼의 정확한 문자 수 및 버퍼에서 반환할 다음 문자의 인덱스)도 유지 관리합니다.

### <a name="an-encoderfallback-example"></a>EncoderFallback 예제

이전 예제에서는 교체 대체(fallback)를 사용하여 ASCII 문자에 응답하지 않은 유니코드 문자를 별표(*)로 대체했습니다. 다음 예제에서는 사용자 지정 최적 대체(fallback) 구현을 대신 사용하여 보다 효과적인 비 ASCII 문자 매핑을 제공합니다.

다음 코드에서는 비 ASCII 문자의 최적 매핑을 처리하기 위해 `CustomMapper` 에서 파생된 <xref:System.Text.EncoderFallback> 라는 클래스를 정의합니다. 해당 `CreateFallbackBuffer` 메서드는 `CustomMapperFallbackBuffer` 구현을 제공하는 <xref:System.Text.EncoderFallbackBuffer> 개체를 반환합니다. `CustomMapper` 클래스는 <xref:System.Collections.Generic.Dictionary%602> 개체를 사용하여 지원되지 않는 유니코드 문자(키 값) 및 해당 8비트 문자(64비트 정수에서는 연속된 2바이트에 저장됨)의 매핑을 저장합니다. 대체(fallback) 버퍼에서 이 매핑을 사용할 수 있도록 `CustomMapper` 인스턴스가 `CustomMapperFallbackBuffer` 클래스 생성자에 매개 변수로 전달됩니다. 가장 긴 매핑은 유니코드 문자 U+221E에 해당하는 문자열 "INF"이므로 `MaxCharCount` 속성은 3을 반환합니다.

[!code-csharp[Conceptual.Encoding#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#5)]
[!code-vb[Conceptual.Encoding#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#5)]

다음 코드에서는 `CustomMapperFallbackBuffer` 에서 파생된 <xref:System.Text.EncoderFallbackBuffer>클래스를 정의합니다. 최적 매핑을 포함하며 `CustomMapper` 인스턴스에서 정의된 사전은 해당 클래스 생성자에서 사용할 수 있습니다. ASCII 인코더가 인코딩할 수 없는 유니코드 문자가 매핑 사전에 정의된 경우 해당 `Fallback` 메서드가 `true` 를 반환하고, 그러지 않으면 `false`를 반환합니다. 각 대체(fallback)에서 private `count` 변수는 반환해야 하는 남은 문자 수를 나타내고, private `index` 변수는 문자열 버퍼 `charsToReturn`에서 반환할 다음 문자의 위치를 나타냅니다.

[!code-csharp[Conceptual.Encoding#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#6)]
[!code-vb[Conceptual.Encoding#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#6)]

다음 코드는 `CustomMapper` 개체를 인스턴스화하고 해당 인스턴스를 <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=nameWithType> 메서드에 전달합니다. 출력은 최적 대체(fallback) 구현에서 원래 문자열에 있는 3자의 비 ASCII 문자를 성공적으로 처리했음을 나타냅니다.

[!code-csharp[Conceptual.Encoding#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#7)]
[!code-vb[Conceptual.Encoding#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#7)]

## <a name="see-also"></a>참고 항목

- <xref:System.Text.Encoder>
- <xref:System.Text.Decoder>
- <xref:System.Text.DecoderFallback>
- <xref:System.Text.Encoding>
- <xref:System.Text.EncoderFallback>
- [전역화 및 지역화](../../../docs/standard/globalization-localization/index.md)
