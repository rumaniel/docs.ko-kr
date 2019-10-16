---
title: DateTime, DateTimeOffset, TimeSpan 및 TimeZoneInfo 중 선택
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTimeOffset structure
- TimeZoneInfo class
- time zones [.NET Framework], common uses
- date and time classes [.NET Framework]
- time zones [.NET Framework], type options
- DateTime structure
ms.assetid: 07f17aad-3571-4014-9ef3-b695a86f3800
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f51ac96105f6d6ae0ea5fbd57a0dc50735e470a3
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835304"
---
# <a name="choosing-between-datetime-datetimeoffset-timespan-and-timezoneinfo"></a>DateTime, DateTimeOffset, TimeSpan 및 TimeZoneInfo 중 선택

날짜 및 시간 정보를 사용하는 .NET 애플리케이션은 매우 다양하며 해당 정보를 여러 가지 방법으로 사용할 수 있습니다. 날짜 및 시간 정보를 사용하는 보다 일반적인 방법에는 다음 중 하나 이상이 포함됩니다.

- 시간 정보가 중요하지 않도록 날짜만 반영합니다.

- 날짜 정보가 중요하지 않도록 시간만 반영합니다.

- 특정 시간과 장소에 연결되지 않은 추상 날짜와 시간을 반영합니다(예: 국제 체인의 상점은 대부분 평일 오전 9:00에 열림).

- 일반적으로 날짜 및 시간 정보가 단순 데이터 형식으로 저장 되는 .NET 외부의 소스에서 날짜 및 시간 정보를 검색 합니다.

- 단일 시점을 고유하고 명확하게 식별합니다. 호스트 시스템에서만 날짜와 시간이 명확하면 되는 애플리케이션도 있고, 시스템 간에 명확해야 하는 애플리케이션도 있습니다(즉, 한 시스템에서 직렬화된 날짜를 다른 시스템에서 의미 있게 역직렬화하고 사용할 수 있음).

- 여러 개의 관련 시간(예: 요청자의 현지 시간 및 서버의 웹 요청 수신 시간)을 보존합니다.

- 날짜 및 시간 산술 연산을 수행합니다(단일 시점을 고유하고 명확하게 식별하는 결과를 제공할 수 있음).

.NET에는 날짜 및 시간을 사용 하는 응용 프로그램을 빌드하는 데 사용할 수 있는 <xref:System.DateTime>, <xref:System.DateTimeOffset>, <xref:System.TimeSpan> 및 @no__t 3 형식이 포함 되어 있습니다.

> [!NOTE]
> 해당 기능이 <xref:System.TimeZoneInfo> 클래스에 거의 완전히 통합 되었기 때문에이 항목에서는 @no__t에 대해 다루지 않습니다. 가능 하면 사용 합니다 <xref:System.TimeZoneInfo> 대신 클래스는 <xref:System.TimeZone> 클래스입니다.

## <a name="the-datetime-structure"></a>DateTime 구조체

<xref:System.DateTime> 값은 특정 날짜와 시간을 정의합니다. 여기에는 해당 날짜와 시간이 속한 표준 시간대에 대 한 제한 된 정보를 제공 하는 <xref:System.DateTime.Kind%2A> 속성이 포함 되어 있습니다. <xref:System.DateTimeKind> 값은 <xref:System.DateTime.Kind%2A> 속성에서 반환된 값은 <xref:System.DateTime> 값이 현지 시간(<xref:System.DateTimeKind.Local?displayProperty=nameWithType>), UTC(협정 세계시)(<xref:System.DateTimeKind.Utc?displayProperty=nameWithType>) 또는 지정되지 않은 시간(<xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>)인지를 나타냅니다.

<xref:System.DateTime> 구조체는 다음을 수행하는 애플리케이션에 적합합니다.

- 날짜만 사용합니다.

- 시간만 사용합니다.

- 추상 날짜와 시간을 사용합니다.

- 표준 시간대 정보가 없는 날짜 및 시간을 사용합니다.

- UTC 날짜 및 시간만 사용합니다.

- SQL 데이터베이스와 같은 .NET 외부의 소스에서 날짜 및 시간 정보를 검색 합니다. 일반적으로 이러한 소스는 <xref:System.DateTime> 구조체와 호환되는 간단한 형식으로 날짜 및 시간 정보를 저장합니다.

- 날짜 및 시간 산술 연산을 수행하지만 일반적인 결과와 관련이 있습니다. 예를 들어 특정 날짜와 시간에 6개월을 더하는 더하기 연산에서 일광 절약 시간제에 맞게 결과를 조정하는지 여부는 대체로 중요하지 않습니다.

특정 <xref:System.DateTime> 값이 UTC를 나타내지 않는 경우 해당 날짜 및 시간 값은 대체로 모호하거나 이식성이 제한됩니다. 예를 들어 <xref:System.DateTime> 값이 현지 시간을 나타내는 경우 현지 표준 시간대 내에서 이식할 수 있습니다(즉, 동일한 표준 시간대의 다른 시스템에서 값을 역직렬화하는 경우 해당 값이 여전히 단일 시점을 명확하게 식별함). 현지 표준 시간대 외부에서는 해당 <xref:System.DateTime> 값이 여러 가지로 해석될 수 있습니다. 값의 <xref:System.DateTime.Kind%2A> 속성이 <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>이면 이식성이 훨씬 감소합니다. 이제 동일한 표준 시간대 내에서 모호하며 처음 직렬화된 시스템에서도 모호할 수 있습니다. <xref:System.DateTime> 값이 UTC를 나타내는 경우에만 값이 사용되는 시스템이나 표준 시간대에 관계없이 단일 시점을 명확하게 식별합니다.

> [!IMPORTANT]
> <xref:System.DateTime> 데이터를 저장하거나 공유하는 경우 UTC를 사용해야 하며 <xref:System.DateTime> 값의 <xref:System.DateTime.Kind%2A> 속성을 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType>로 설정해야 합니다.

## <a name="the-datetimeoffset-structure"></a>DateTimeOffset 구조체

<xref:System.DateTimeOffset> 구조체는 날짜 및 시간 값과 해당 값이 UTC와 다른 정도를 나타내는 오프셋을 나타냅니다. 따라서 값이 항상 단일 시점을 명확하게 식별합니다.

<xref:System.DateTimeOffset> 형식에는 <xref:System.DateTime> 형식의 모든 기능과 표준 시간대 인식 기능이 포함됩니다. 이렇게 하면 다음을 수행 하는 응용 프로그램에 적합 합니다.

- 단일 시점을 고유하고 명확하게 식별합니다. <xref:System.DateTimeOffset> 형식을 통해 “now"의 의미를 명확하게 정의하고, 트랜잭션 시간을 기록하고, 시스템 또는 애플리케이션 이벤트의 시간을 기록하고, 파일을 만든 시간과 수정 시간을 기록할 수 있습니다.

- 일반적인 날짜 및 시간 산술 연산을 수행합니다.

- 시간이 두 개의 개별 값으로 저장되거나 한 구조체의 두 멤버로 저장된 경우 관련된 여러 시간을 보존합니다.

> [!NOTE]
> <xref:System.DateTimeOffset> 값의 사용은 <xref:System.DateTime> 값의 사용보다 훨씬 더 일반적입니다. 따라서 <xref:System.DateTimeOffset> 을 애플리케이션 개발의 기본 날짜 및 시간 형식으로 간주해야 합니다.

<xref:System.DateTimeOffset> 값은 특정 표준 시간대와 연결되지 않고 다양한 표준 시간대에서 발생할 수 있습니다. 이를 설명하기 위해 다음 예제에서는 많은 <xref:System.DateTimeOffset> 값(현지 태평양 표준시 포함)이 속할 수 있는 표준 시간대를 나열합니다.

[!code-csharp[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual1.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual1.vb#1)]

출력은 이 예제의 각 날짜 및 시간 값이 세 개 이상의 표준 시간대에 속할 수 있음을 보여 줍니다. <xref:System.DateTimeOffset> 값 6/10/2007은 날짜 및 시간 값이 일광 절약 시간제를 나타내는 경우 UTC에서의 오프셋이 시작 표준 시간대의 기본 UTC 오프셋이나 표시 이름에 있는 UTC에서의 오프셋과 일치하지 않을 수도 있음을 보여 줍니다. 즉, 단일 <xref:System.DateTimeOffset> 값은 해당 표준 시간대와 긴밀히 연결되어 있지 않으므로 표준 시간대의 일광 절약 시간제 전환을 반영할 수 없습니다. 이는 날짜 및 시간 산술 연산을 사용하여 <xref:System.DateTimeOffset> 값을 조작하는 경우에 특히 문제가 될 수 있습니다. 표준 시간대의 조정 규칙을 고려하는 방식으로 날짜 및 시간 산술 연산을 수행하는 방법에 대한 자세한 내용은 [날짜 및 시간으로 산술 연산 수행](performing-arithmetic-operations.md)을 참조하십시오.

## <a name="the-timespan-structure"></a>TimeSpan 구조체

<xref:System.TimeSpan> 구조체는 시간 간격을 나타냅니다. 일반적으로 다음 두 가지 용도로 사용됩니다.

- 두 개의 날짜 및 시간 값의 시간 간격을 반영합니다. 예를 들어 다른 값에서 <xref:System.DateTime> 값을 빼면 <xref:System.TimeSpan> 값이 반환됩니다.

- 경과 시간을 측정합니다. 예를 들어 <xref:System.Diagnostics.Stopwatch.Elapsed%2A?displayProperty=nameWithType> 속성은 경과 시간 측정을 시작 하는 <xref:System.Diagnostics.Stopwatch> 메서드 중 하나를 호출한 후 경과 된 시간 간격을 반영 하는 <xref:System.TimeSpan> 값을 반환 합니다.

@No__t-0 값은 특정 날짜에 대 한 참조 없이 시간을 반영 하는 경우 <xref:System.DateTime> 값을 대체 하는 데 사용할 수도 있습니다. 이 사용법은 <xref:System.DateTime.TimeOfDay%2A?displayProperty=nameWithType> 및 <xref:System.DateTimeOffset.TimeOfDay%2A?displayProperty=nameWithType> 속성과 비슷하며 날짜를 참조 하지 않고 시간을 나타내는 <xref:System.TimeSpan> 값을 반환 합니다. 예를 들어 <xref:System.TimeSpan> 구조체를 사용하여 매일 상점을 여는 시간 또는 닫는 시간을 반영하거나 정기 이벤트가 발생하는 시간을 나타낼 수 있습니다.

다음 예제에서는 상점을 여는 시간과 닫는 시간에 사용되는 `StoreInfo` 개체와 상점의 표준 시간대를 나타내는 <xref:System.TimeSpan> 개체가 포함된 <xref:System.TimeZoneInfo> 구조체를 정의합니다. 구조체에는 현지 표준 시간대에 있는 것으로 가정되는 사용자가 지정한 시간에 상점이 열려 있는지 여부를 나타내는 `IsOpenNow` 및 `IsOpenAt`의 두 메서드도 포함됩니다.

[!code-csharp[Conceptual.ChoosingDates#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#1)]
[!code-vb[Conceptual.ChoosingDates#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#1)]

`StoreInfo` 구조체는 클라이언트 코드에서 다음과 같이 사용될 수 있습니다.

[!code-csharp[Conceptual.ChoosingDates#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#2)]
[!code-vb[Conceptual.ChoosingDates#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#2)]

## <a name="the-timezoneinfo-class"></a>TimeZoneInfo 클래스

<xref:System.TimeZoneInfo> 클래스는 지구의 표준 시간대를 나타내며, 한 표준 시간대의 날짜 및 시간을 다른 표준 시간대의 해당 항목으로 변환할 수 있습니다. <xref:System.TimeZoneInfo> 클래스를 사용하면 모든 날짜 및 시간 값이 명확하게 단일 시점을 식별하도록 날짜 및 시간 작업을 할 수 있습니다. <xref:System.TimeZoneInfo> 클래스는 확장도 가능합니다. Windows 시스템에 대해 제공되고 레지스트리에 정의된 표준 시간대 정보에 따라 달라지지만 사용자 지정 표준 시간대 생성을 지원합니다. 또한 표준 시간대 정보의 직렬화 및 역직렬화를 지원합니다.

<xref:System.TimeZoneInfo> 클래스를 완전히 활용하기 위해 추가 개발 작업이 필요한 경우도 있습니다. 날짜 및 시간 값이 속해 있는 표준 시간대와 긴밀 하 게 연결 되지 않은 경우에는 추가 작업이 필요 합니다. 응용 프로그램에서 날짜 및 시간을 관련 표준 시간대와 연결 하기 위한 몇 가지 메커니즘을 제공 하지 않는 한 특정 날짜 및 시간 값이 표준 시간대에서 분리 될 수 있습니다. 이 정보를 연결하는 한 가지 방법으로 날짜 및 시간 값, 그리고 연결되는 표준 시간대 개체를 둘 다 포함하는 클래스나 구조체를 정의합니다.

날짜 및 시간 개체를 인스턴스화할 때 날짜 및 시간 값이 속하는 표준 시간대가 알려진 경우에만 .NET의 표준 시간대 지원을 활용할 수 있습니다. 웹 또는 네트워크 애플리케이션에서는 특히 알 수 없는 경우가 많습니다.

## <a name="see-also"></a>참조

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
