---
title: 날짜 및 시간에 대한 산술 연산 수행
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- times [.NET Framework], arithmetic operations
- dates [.NET Framework], arithmetic operations
- time zones [.NET Framework], arithmetic operations
- arithmetic operations [.NET Framework], dates and times
- dates [.NET Framework], comparing
- DateTime structure, arithmetic operations
- DateTimeOffset structure, arithmetic operations
ms.assetid: 87c7ddf2-f15e-48af-8602-b3642237e6d0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 01314c160fc531f5c97a1369c8444dce7f590d53
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106611"
---
# <a name="performing-arithmetic-operations-with-dates-and-times"></a>날짜 및 시간에 대한 산술 연산 수행

<xref:System.DateTime> 및 구조체는 <xref:System.DateTimeOffset> 모두 값에 대 한 산술 연산을 수행 하는 멤버를 제공 하지만 산술 연산 결과는 매우 다릅니다. 이 항목에서는 이러한 차이점을 검토 하 고 날짜 및 시간 데이터에서 표준 시간대 인식의 각도에 대해 설명 하 고 날짜 및 시간 데이터를 사용 하 여 전체 표준 시간대 인식 작업을 수행 하는 방법을 설명 합니다.

## <a name="comparisons-and-arithmetic-operations-with-datetime-values"></a>DateTime 값을 사용한 비교 및 산술 연산

속성을 사용 하면 날짜 및 시간에 값을할당하여현지시간,utc(협정세계시)또는지정되지않은표준시간대의시간을나타내는지여부를나타낼수있습니다.<xref:System.DateTimeKind> <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 그러나이 제한 된 표준 시간대 정보는 값에 대 <xref:System.DateTimeKind> 한 날짜 및 시간 산술 연산을 비교 하거나 수행할 때 무시 됩니다. 현재 UTC 시간을 포함한 현재 현지 시간을 비교하는 다음 예제에서는 이를 보여 줍니다.

[!code-csharp[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual2.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual2.vb#2)]

메서드 <xref:System.DateTime.CompareTo%28System.DateTime%29> 는 현지 시간이 utc 시간 보다 빠르거나 적은지 보고 하 고, 빼기 연산은 미국에 있는 시스템의 utc와 현지 시간 사이의 차이를 나타냅니다. 태평양 표준 시간대는 7시간입니다. 하지만 이러한 두 개의 값은 시간에서 단일 지점의 다양한 표현을 제공하기 때문에 이 경우에 이 시간 간격이 UTC에서 현지 표준 시간대 오프셋을 발생시키는 것이 명확합니다.

보다 일반적으로 속성 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 은 <xref:System.DateTime.Kind> 비교 및 산술 메서드에서 반환 되는 결과에 영향을 주지 않습니다 (시간에서 두 개의 동일한 지점의 비교는 해당 결과의 해석에 영향을 줄 수 있음). 예를 들어:

- 두 개의 날짜 및 시간 값 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> <xref:System.DateTimeKind> 에 대해 수행 되는 산술 연산 결과는 두 값 사이의 실제 시간 간격을 반영 합니다. 마찬가지로 이러한 두 개의 날짜 및 시간 값을 비교하면 시간 간의 관계를 정확하게 반영합니다.

- 두 개의 날짜 및 시간 값 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> <xref:System.DateTimeKind> 에 대해 속성 값이 서로 다른 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 두 개의 날짜 및 시간 값과 두 개의 날짜 및 시간 값에 대해 수행 되는 산술 또는 비교 연산의 결과는 클록 시간의 차이를 반영 합니다. 두 값 사이

- 로컬 날짜 및 시간 값에 대한 산술 또는 비교 작업은 특정 값이 모호하거나 잘못되었는지 여부를 고려하지 않거나 현지 표준 시간대 전환 또는 일광 절약 시간에서 발생하는 모든 조정 규칙의 효과를 고려하지 않습니다.

- UTC와 현지 시간 사이의 차이를 비교하거나 계산하는 작업에는 결과에 있는 UTC에서 현지 표준 시간대 오프셋과 동일한 시간 간격이 포함됩니다.

- 지정되지 않은 시간과 UTC 또는 현지 시간 사이의 차이를 비교하거나 계산하는 작업은 간단한 클록 시간을 반영합니다. 표준 시간대 차이를 고려하지 않으면 결과가 표준 시간대 조정 규칙의 애플리케이션을 반영하지 않습니다.

- 두 개의 지정되지 않은 시간 사이의 차이를 비교하거나 계산하는 작업에는 두 개의 다른 시간대의 시간 사이의 차이를 반영하는 알 수 없는 간격이 포함될 수 있습니다.

표준 시간대 차이가 날짜 및 시간 계산에 영향을 주지 않는 시나리오는 여러 가지가 있습니다 (이 중 일부에 대 한 자세한 내용은 [DateTime, DateTimeOffset, TimeSpan 및 TimeZoneInfo](../../../docs/standard/datetime/choosing-between-datetime.md)중에서 선택 참조). 또는 날짜 및 시간 데이터의 컨텍스트가 비교 또는 산술 연산의 의미를 정의 합니다.

## <a name="comparisons-and-arithmetic-operations-with-datetimeoffset-values"></a>DateTimeOffset 값을 사용한 비교 및 산술 연산

값 <xref:System.DateTimeOffset> 은 날짜 및 시간 뿐만 아니라 UTC를 기준으로 해당 날짜와 시간을 명확 하 게 정의 하는 오프셋을 포함 합니다. 이렇게 하면 값의 경우 <xref:System.DateTimeOffset> 보다 약간 다르게 같음을 정의할 수 있습니다. 동일한 날짜 및 시간 <xref:System.DateTimeOffset> 값이 있는 경우 값은동일하지만동일한지정시간을참조하는경우에는값이같습니다.<xref:System.DateTime> 이렇게 하면 <xref:System.DateTimeOffset> 두 날짜 및 시간 사이의 간격을 결정 하는 비교 및 대부분의 산술 연산에서 사용 되는 경우 값이 더 정확 하 고 해석이 필요 하지 않습니다. 로컬 및 UTC <xref:System.DateTimeOffset> 값을 비교 하 <xref:System.DateTimeOffset> 는 이전 예제와 동일한 다음 예제에서는 이러한 동작의 차이를 보여 줍니다.

[!code-csharp[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual3.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual3.vb#3)]

이 예제에서 메서드는 <xref:System.DateTimeOffset.CompareTo%2A> 현재 현지 시간과 현재 UTC 시간이 동일 함을 나타내고, 값의 <xref:System.DateTimeOffset.CompareTo(System.DateTimeOffset)> 빼기는 두 시간 <xref:System.TimeSpan.Zero?displayProperty=nameWithType>사이의 차이가 임을 나타냅니다.

날짜 및 시간 산술 연산 <xref:System.DateTimeOffset> 에서 값을 사용 하는 경우의 주요 <xref:System.DateTimeOffset> 제한 사항은 값에 표준 시간대 인식이 있지만 완전히 표준 시간대를 인식 하지 않는다는 것입니다. 값의 <xref:System.DateTimeOffset> 오프셋은 <xref:System.DateTimeOffset> 변수에 첫 번째 값이 할당 될 때 UTC의 표준 시간대 오프셋을 반영 하지만 이후에는 해당 표준 시간대와의 연결이 해제 됩니다. 더 이상 식별 가능한 시간과 직접 연결되어 있기 때문에 날짜 및 시간 간격의 더하기 및 빼기는 표준 시간대의 조정 규칙을 고려하지 않습니다.

예를 들어 미국 중부 표준시에서는 2008년 3월 9일 오전 2시에 표준 시간대가 일광 절약 시간제로 전환됩니다. 즉, 중부 표준시 2008년 3월 9일 오전 1시 30분에 2시간 30분의 간격을 더하면 날짜와 시간은 2008년 3월 9일 오전 5시가 됩니다. 그러나 다음 예제와 같이 이 더하기 연산의 결과는 2008년 3월 9일 오전 4시가 됩니다. 관심 있는 표준 시간대의 시간이 아니지만(즉, 예상된 표준 시간대 오프셋이 아님) 이 작업의 결과는 올바른 특정 시점을 나타냅니다.

[!code-csharp[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual4.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual4.vb#4)]

## <a name="arithmetic-operations-with-times-in-time-zones"></a>표준 시간대의 시간을 사용한 산술 연산

클래스 <xref:System.TimeZoneInfo> 에는 시간을 한 표준 시간대에서 다른 표준 시간대로 변환 하는 경우 자동으로 조정을 적용 하는 여러 변환 메서드가 포함 되어 있습니다. 이러한 요구 사항은 다음과 같습니다.

- <xref:System.TimeZoneInfo.ConvertTime%2A> 및<xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A> 메서드로, 두 표준 시간대 간에 시간을 변환 합니다.

- 특정 표준 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> 시간대의 시간을 utc로 변환 하거나 utc를 특정 표준 시간대의 시간으로 변환 하는 및메서드.<xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A>

자세한 내용은 [표준 시간대 간의 시간 변환](../../../docs/standard/datetime/converting-between-time-zones.md)을 참조 하세요.

클래스 <xref:System.TimeZoneInfo.ConvertTimeToUtc(System.DateTime)> 는 날짜 및 시간 산술 연산을 수행할 때 자동으로 조정 규칙을 적용 하는 메서드를 제공 하지 않습니다. 그러나 이렇게 하려면 표준 시간대의 시간을 UTC로 변환하고 산술 연산을 수행하며 UTC에서 표준 시간대의 시간으로 다시 변환해야 합니다. 자세한 내용은 [방법: 날짜 및 시간 산술 연산의](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md)표준 시간대를 사용 합니다.

예를 들어 다음 코드는 2008년 3월 9일 오전 2시에 2시간 30분을 더한 이전 코드와 유사합니다. 그러나 날짜 및 시간 산술 연산을 수행하기 전에 중부 표준시를 UTC로 변환한 다음 UTC의 결과를 중부 표준시로 다시 변환하기 때문에 결과 시간은 일광 절약 시간제로 전환된 중앙 표준 시간대를 반영합니다.

[!code-csharp[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual5.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual5.vb#5)]

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [방법: 날짜 및 시간 산술 연산의 표준 시간대 사용](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md)
