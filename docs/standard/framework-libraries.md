---
title: 프레임워크 라이브러리
description: 라이브러리가 많은 일반 및 앱별 형식, 알고리즘 및 유틸리티 기능에 대한 구현을 제공하는 방법을 알아봅니다.
author: richlander
ms.author: ronpet
ms.date: 06/20/2016
ms.technology: dotnet-standard
ms.assetid: 7b77b6c1-8367-4602-bff3-91e4c05ac643
ms.openlocfilehash: 494ac194fe8dc9554c6e0d1d87ba2ed613d1d16b
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663222"
---
# <a name="framework-libraries"></a>프레임워크 라이브러리

.NET에는 기본 클래스 라이브러리(핵심 집합) 또는 프레임워크 클래스 라이브러리(전체 집합)라는 광범위한 표준 클래스 라이브러리 집합이 있습니다. 이러한 라이브러리는 많은 일반 및 앱별 형식, 알고리즘 및 유틸리티 기능에 대한 구현을 제공합니다. 상업용 및 커뮤니티 라이브러리 둘 다 프레임워크 클래스 라이브러리를 기반으로 해서 구축되며 광범위한 컴퓨팅 작업에 사용하기 쉬운 기본 제공 라이브러리를 제공합니다.

이 라이브러리의 하위 집합이 각 .NET 구현에 제공됩니다. BCL(기본 클래스 라이브러리) API는 개발자가 원할 뿐 아니라 인기 있는 라이브러리를 사용하려면 이 API를 실행해야 하기 때문에 모든 .NET 구현에 제공됩니다. ASP.NET과 같은 BCL 위의 앱별 라이브러리는 일부 .NET 구현에서 사용할 수 없습니다.

## <a name="base-class-libraries"></a>기본 클래스 라이브러리

BCL은 가장 기본적인 형식과 유틸리티 기능을 제공하며 다른 모든 .NET 클래스 라이브러리의 기초가 됩니다. BCL의 목적은 어떠한 작업에도 편향되지 않고 매우 일반적인 구현을 제공하는 것입니다. 앱에서 높은 처리량보다 짧은 대기 시간 우선, 낮은 CPU 사용량보다 낮은 메모리 사용량 우선 등의 특정 정책을 선호할 수 있으므로 성능은 항상 중요한 고려 사항입니다. 이 라이브러리는 일반적으로 고성능으로 설계되었으며 이러한 다양한 성능 문제에 따라 중도적인 방식을 선택합니다. 대부분의 앱에서 이 방식은 매우 성공적이었습니다.

## <a name="primitive-types"></a>기본 형식

.NET에는 모든 프로그램에서 사용되는(다양한 수준으로) 기본 형식 집합이 있습니다. 이러한 형식은 숫자, 문자열, 바이트, 임의 개체 등의 데이터를 포함합니다. C# 언어에는 이 형식의 키워드가 있습니다. 이러한 형식의 샘플 집합 및 일치하는 C# 키워드가 아래에 나와 있습니다.

* <xref:System.Object?displayProperty=nameWithType>([object](../csharp/language-reference/keywords/object.md)) - CLR 형식 시스템의 궁극적인 기본 클래스입니다. 형식 계층 구조의 루트입니다.
* <xref:System.Int16?displayProperty=nameWithType>([short](../csharp/language-reference/builtin-types/integral-numeric-types.md)) - 16비트 부호 있는 정수 형식입니다. 부호 없는 <xref:System.UInt16>도 있습니다.
* <xref:System.Int32?displayProperty=nameWithType>([int](../csharp/language-reference/builtin-types/integral-numeric-types.md)) - 32비트 부호 있는 정수 형식입니다. 부호 없는 [UInt32](../csharp/language-reference/builtin-types/integral-numeric-types.md)도 있습니다.
* <xref:System.Single?displayProperty=nameWithType>([float](../csharp/language-reference/builtin-types/floating-point-numeric-types.md)) - 32비트 부동 소수점 형식입니다.
* <xref:System.Decimal?displayProperty=nameWithType>([decimal](../csharp/language-reference/builtin-types/floating-point-numeric-types.md)) - 128비트 10진수 형식입니다.
* <xref:System.Byte?displayProperty=nameWithType>([byte](../csharp/language-reference/builtin-types/integral-numeric-types.md)) - 1바이트의 메모리를 나타내는 부호 없는 8비트 정수입니다.
* <xref:System.Boolean?displayProperty=nameWithType>([bool](../csharp/language-reference/keywords/bool.md)) - `true` 또는 `false`를 나타내는 부울 형식입니다.
* <xref:System.Char?displayProperty=nameWithType>([char](../csharp/language-reference/keywords/char.md)) - 유니코드 문자를 나타내는 16비트 숫자 형식입니다.
* <xref:System.String?displayProperty=nameWithType>([string](../csharp/language-reference/keywords/string.md)) - 일련의 문자를 나타냅니다. `char[]`와 다르지만 `string`의 각 개별 `char`를 인덱싱할 수 있습니다.

## <a name="data-structures"></a>데이터 구조

.NET에는 거의 모든 .NET 앱의 원동력인 데이터 구조 집합이 포함되어 있습니다. 대부분 컬렉션이지만 다른 형식도 있습니다.

* <xref:System.Array> - 인덱스로 액세스할 수 있는 강력한 형식의 개체 배열을 나타냅니다. 구성별로 고정 크기가 있습니다.
* <xref:System.Collections.Generic.List%601> - 인덱스로 액세스할 수 있는 강력한 형식의 개체 목록을 나타냅니다. 필요에 따라 크기가 자동으로 조정됩니다.
* <xref:System.Collections.Generic.Dictionary%602> - 키로 인덱싱된 값의 컬렉션을 나타냅니다. 키를 통해 값에 액세스할 수 있습니다. 필요에 따라 크기가 자동으로 조정됩니다.
* <xref:System.Uri> - URI(Uniform Resource Identifier)의 개체 표현을 제공하며 URI 부분에 쉽게 액세스할 수 있도록 합니다.
* <xref:System.DateTime> - 일반적으로 날짜와 시간으로 표시된 시간을 나타냅니다.

## <a name="utility-apis"></a>유틸리티 API

.NET에는 여러 중요한 작업에 대한 기능을 제공하는 유틸리티 API 집합이 포함되어 있습니다.

* <xref:System.Net.Http.HttpClient> - URI로 식별되는 리소스에서 HTTP 요청을 보내고 HTTP 응답을 받기 위한 API입니다.
* <xref:System.Xml.Linq.XDocument> - XML 문서를 로드하고 LINQ를 사용하여 쿼리하기 위한 API입니다.
* <xref:System.IO.StreamReader> - 파일을 읽기 위한 API. 
* <xref:System.IO.StreamWriter> - 파일을 쓰기 위한 API.

## <a name="app-model-apis"></a>앱 모델 API

여러 회사에서 제공하는, .NET에 사용할 수 있는 많은 앱 모델이 있습니다.

* [ASP.NET](https://www.asp.net) - 웹 사이트와 서비스를 구축하기 위한 웹 프레임워크를 제공합니다. Windows, Linux 및 macOS에서 지원됩니다(ASP.NET 버전에 따라 다름).
