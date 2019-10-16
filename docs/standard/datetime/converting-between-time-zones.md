---
title: 표준 시간대 간 시간 변환
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- times [.NET Framework], converting
- time zones [.NET Framework], conversions
- UTC times, converting
- converting times
- local time conversions
ms.assetid: a51e1a3b-c983-4320-b31a-1f9fa3cf824a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c5b78e3985169954d71b479aa2e8a034f61afc01
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106963"
---
# <a name="converting-times-between-time-zones"></a>표준 시간대 간 시간 변환

날짜 및 시간을 사용하는 애플리케이션에서 표준 시간대 간의 차이를 처리하는 것이 더욱 중요해지고 있습니다. 응용 프로그램은 더 이상 <xref:System.DateTime> 구조체에서 사용할 수 있는 시간인 현지 시간으로 모든 시간을 표현할 수 있는 것으로 간주할 수 없습니다. 예를 들어 동아시아 지역 고객에게는 미국 동부 지역의 현재 시간을 표시하는 웹 페이지의 신뢰성이 떨어집니다. 이 항목에서는 표준 시간대를 한 표준 시간대에서 다른 표준 시간대로 변환 하는 방법과 표준 시간대 <xref:System.DateTimeOffset> 인식이 제한 된 값을 변환 하는 방법에 대해 설명 합니다.

## <a name="converting-to-coordinated-universal-time"></a>UTC로 변환

UTC(협정 세계시)는 고정밀 원자 시간 표준입니다. 전세계의 표준 시간대가 UTC의 양 또는 음 오프셋으로 표시됩니다. 따라서 UTC는 어느 정도 표준 시간대에서 자유롭거나 중립적인 시간을 제공합니다. 컴퓨터 간에 날짜 및 시간의 이식성이 중요한 경우 UTC 시간을 사용하는 것이 좋습니다. 날짜 및 시간을 사용 하는 세부 정보 및 기타 모범 사례 [는 .NET Framework에서 DateTime을 사용 하 여 최선의 코딩 방법](https://docs.microsoft.com/previous-versions/dotnet/articles/ms973825(v=msdn.10))을 참조 하세요.) 개별 표준 시간대를 UTC로 변환하면 시간을 보다 쉽게 비교할 수 있습니다.

> [!NOTE]
> 구조체를 <xref:System.DateTimeOffset> serialize 하 여 단일 시점을 명확 하 게 나타낼 수도 있습니다. 개체 <xref:System.DateTimeOffset> 는 날짜 및 시간 값을 utc의 오프셋과 함께 저장 하므로 항상 utc와의 관계에 있는 특정 시점을 나타냅니다.

시간을 UTC로 변환 하는 가장 쉬운 방법은 `static` (`Shared` Visual Basic) <xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=nameWithType> 메서드를 호출 하는 것입니다. 메서드에서 수행 하는 정확한 변환은 다음 표와 같이 `dateTime` <xref:System.DateTime.Kind%2A> 매개 변수의 속성 값에 따라 달라 집니다.

| `DateTime.Kind`            | 변환                                                                     |
| -------------------------- | ------------------------------------------------------------------------------ |
| `DateTimeKind.Local`       | 현지 시간을 UTC로 변환합니다.                                                    |
| `DateTimeKind.Unspecified` | `dateTime` 매개 변수가 현지 시간인 것으로 가정하고 현지 시간을 UTC로 변환합니다. |
| `DateTimeKind.Utc`         | 변경하지 않은 `dateTime` 매개 변수를 반환합니다.                                    |

다음 코드에서는 현재 현지 시간을 UTC로 변환하고 그 결과를 콘솔에 표시합니다.

[!code-csharp[System.TimeZone2.Concepts#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#6)]
[!code-vb[System.TimeZone2.Concepts#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#6)]

날짜 및 시간 값이 현지 시간이 나 UTC를 나타내지 않는 경우이 메서드는 <xref:System.DateTime.ToUniversalTime%2A> 잘못 된 결과를 반환할 수 있습니다. 그러나 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> 메서드를 사용 하 여 지정 된 표준 시간대의 날짜 및 시간을 변환할 수 있습니다. 대상 표준 시간대를 나타내는 개체 <xref:System.TimeZoneInfo> 를 검색 하는 방법에 대 한 자세한 내용은 [로컬 시스템에 정의 된 표준 시간대 찾기](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)를 참조 하십시오. 다음 코드에서는 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> 메서드를 사용 하 여 동부 표준시를 UTC로 변환 합니다.

[!code-csharp[System.TimeZone2.Concepts#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#7)]
[!code-vb[System.TimeZone2.Concepts#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#7)]

<xref:System.DateTime> 개체 <xref:System.ArgumentException> 의<xref:System.DateTime.Kind%2A> 속성과 표준 시간대가 일치 하지 않는 경우이 메서드는을 throw 합니다. <xref:System.DateTime.Kind%2A> 속성이이 <xref:System.DateTime.Kind%2A> 고개체가현지<xref:System.TimeZoneInfo>표준시간대 를 나타내지 않는 경우 <xref:System.TimeZoneInfo.Utc?displayProperty=nameWithType>또는 속성이 이지만개체가와같지않은경우불일치가발생합니다.<xref:System.DateTimeKind.Utc?displayProperty=nameWithType> <xref:System.TimeZoneInfo> <xref:System.DateTimeKind.Local?displayProperty=nameWithType>

이러한 모든 메서드는 값 <xref:System.DateTime> 을 매개 변수로 사용 하 고 <xref:System.DateTime> 값을 반환 합니다. 값 <xref:System.DateTimeOffset> <xref:System.DateTimeOffset.ToUniversalTime%2A> 의 경우 구조체에는 현재 인스턴스의 날짜와 시간을 UTC로 변환 하는 인스턴스 메서드가 있습니다. <xref:System.DateTimeOffset> 다음 예제에서는 <xref:System.DateTimeOffset.ToUniversalTime%2A> 현지 시간과 여러 다른 시간을 utc (협정 세계시)로 변환 하는 방법입니다.

[!code-csharp[System.DateTimeOffset.Methods#16](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/cs/Methods.cs#16)]
[!code-vb[System.DateTimeOffset.Methods#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/vb/Methods.vb#16)]

## <a name="converting-utc-to-a-designated-time-zone"></a>UTC를 지정한 표준 시간대로 변환

UTC를 현지 시간으로 변환 하려면 다음에 나오는 "UTC를 현지 시간으로 변환" 섹션을 참조 하세요. UTC를 지정 하는 표준 시간대의 시간으로 변환 하려면 <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> 메서드를 호출 합니다. 이 메서드에서 사용하는 두 개의 매개 변수는 다음과 같습니다.

- 변환할 UTC. <xref:System.DateTime> 속성이 또는 <xref:System.DateTime.Kind%2A> 로설정`Unspecified` 되어 있는 값 이어야 합니다. `Utc`

- UTC를 변환한 값이 속하게 될 표준 시간대

다음 코드는 UTC를 중부 표준시로 변환합니다.

[!code-csharp[System.TimeZone2.Concepts#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#8)]
[!code-vb[System.TimeZone2.Concepts#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#8)]

## <a name="converting-utc-to-local-time"></a>UTC를 현지 시간으로 변환

UTC를 현지 시간으로 변환 하려면 시간을 <xref:System.DateTime.ToLocalTime%2A> 변환할 <xref:System.DateTime> 개체의 메서드를 호출 합니다. 메서드의 정확한 동작은 다음 표와 같이 개체 <xref:System.DateTime.Kind%2A> 의 속성 값에 따라 달라 집니다.

| `DateTime.Kind`            | 변환                                                                               |
| -------------------------- | ---------------------------------------------------------------------------------------- |
| `DateTimeKind.Local`       | 변경 되지 <xref:System.DateTime> 않은 값을 반환 합니다.                                      |
| `DateTimeKind.Unspecified` | <xref:System.DateTime> 값이 utc 인 것으로 가정 하 고 utc를 현지 시간으로 변환 합니다. |
| `DateTimeKind.Utc`         | <xref:System.DateTime> 값을 현지 시간으로 변환 합니다.                                 |

> [!NOTE]
> 메서드 <xref:System.TimeZone.ToLocalTime%2A?displayProperty=nameWithType> 는 `DateTime.ToLocalTime` 메서드와 동일 하 게 동작 합니다. 이 메서드는 변환할 날짜 및 시간 값인 단일 매개 변수를 사용 합니다.

Visual Basic ( `static` `Shared` ) 메서드를사용하여지정된표준시간대의시간을현지시간으로변환할수도있습니다.<xref:System.TimeZoneInfo.ConvertTime%2A?displayProperty=nameWithType> 이 기법은 다음 섹션에서 설명 합니다.

## <a name="converting-between-any-two-time-zones"></a>두 표준 시간대 간 변환

클래스의 다음 두 `static` (`Shared` Visual Basic) 메서드 중 하나를 사용 하 여 두 표준 시간대 간에 변환할 수 있습니다. <xref:System.TimeZoneInfo>

- <xref:System.TimeZoneInfo.ConvertTime%2A>

  이 메서드의 매개 변수는 변환할 날짜 및 시간 값, `TimeZoneInfo` 날짜 및 시간 값의 표준 시간대를 나타내는 개체 `TimeZoneInfo` 및 날짜 및 시간 값을로 변환할 표준 시간대를 나타내는 개체입니다.

- <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>

  이 메서드의 매개 변수는 변환할 날짜 및 시간 값, 날짜 및 시간 값의 표준 시간대의 식별자 및 날짜 및 시간 값을로 변환할 표준 시간대의 식별자입니다.

두 메서드 모두 변환할 <xref:System.DateTime.Kind%2A> <xref:System.TimeZoneInfo> 날짜 및 시간 값의 속성과 표준 시간대를 나타내는 개체 또는 표준 시간대 식별자가 서로 일치 해야 합니다. 그렇지 않으면 <xref:System.ArgumentException>이 throw됩니다. 예 `Kind` 를 들어 날짜 및 시간 `DateTimeKind.Local`값의 속성이 이면 메서드에 `TimeZoneInfo.Local`매개 변수로 전달 된 `TimeZoneInfo` 개체가와 같지 않으면 예외가 throw 됩니다. 메서드에 매개 변수로 전달 된 식별자가와 같지 않은 경우에 `TimeZoneInfo.Local.Id`도 예외가 throw 됩니다.

다음 예제에서는 <xref:System.TimeZoneInfo.ConvertTime%2A> 메서드를 사용 하 여 하와이 표준시를 현지 시간으로 변환 합니다.

[!code-csharp[System.TimeZone2.Concepts#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#9)]
[!code-vb[System.TimeZone2.Concepts#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#9)]

## <a name="converting-datetimeoffset-values"></a>DateTimeOffset 값 변환

개체로 표시 <xref:System.DateTimeOffset> 되는 날짜 및 시간 값은 개체가 인스턴스화될 때 해당 표준 시간대에서 연결이 해제 되기 때문에 전체 시간대를 인식 하지 못합니다. 그러나 많은 경우에는 애플리케이션에서 특정 표준 시간대의 시간이 아니라 단순히 서로 다른 UTC 오프셋 두 개를 기준으로 날짜 및 시간을 변환하면 됩니다. 이 변환을 수행 하려면 현재 인스턴스의 <xref:System.DateTimeOffset.ToOffset%2A> 메서드를 호출 하면 됩니다. 메서드의 단일 매개 변수는 메서드에서 반환할 새 날짜 및 시간 값의 오프셋입니다.

예를 들어 사용자가 웹 페이지에서 요청한 날짜 및 시간이 알려져 있고 이 값이 MM/dd/yyyy hh:mm:ss zzzz 형식의 문자열로 serialize된 경우 뒤따르는 `ReturnTimeOnServer` 메서드에서 이 날짜 및 시간 값을 웹 서버의 날짜 및 시간 값으로 변환합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/TimeConversions.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions.vb#1)] 

UTC보다 다섯 시간 빠른 표준 시간대의 날짜 및 시간을 나타내는 "9/1/2007 5:32:07 -05:00" 문자열이 메서드에 전달되는 경우 이 메서드에서는 미국 태평양 표준 시간대에 있는 서버에 대해 9/1/2007 3:32:07 AM -07:00을 보여 줍니다.

클래스 <xref:System.TimeZoneInfo> 에는 값을 사용 하 여 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> <xref:System.DateTimeOffset.ToOffset(System.TimeSpan)> 표준 시간대 변환을 수행 하는 메서드의 오버 로드도 포함 되어 있습니다. 메서드의 매개 변수 <xref:System.DateTimeOffset> 는 시간을 변환할 표준 시간대에 대 한 참조 및 값입니다. 메서드 호출은 값을 <xref:System.DateTimeOffset> 반환 합니다. 예 `ReturnTimeOnServer` 를 들어 이전 예제의 메서드를 다음과 같이 다시 작성 하 여 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29> 메서드를 호출할 수 있습니다.

[!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/timeconversions2.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions2.vb#2)]

## <a name="see-also"></a>참고자료

- <xref:System.TimeZoneInfo>
- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [로컬 시스템에 정의된 표준 시간대 찾기](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)
