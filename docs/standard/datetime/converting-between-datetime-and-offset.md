---
title: DateTime과 DateTimeOffset 간 변환
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTime structure, converting
- time zones [.NET Framework], conversions
- UTC times, converting
- DateTimeOffset structure, converting
- converting DateTimeOffset and DateTime values
- dates [.NET Framework], converting
- converting times
- Date data type, converting
- local time conversions
ms.assetid: b605ff97-0c45-4c24-833f-4c6a3e8be64c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: eb91ed8edd0c5cd3cb1d051157596f311718195d
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70107062"
---
# <a name="converting-between-datetime-and-datetimeoffset"></a>DateTime과 DateTimeOffset 간 변환

구조는 <xref:System.DateTimeOffset> <xref:System.DateTime> 구조<xref:System.DateTime> 보다 더 높은 수준의 표준 시간대 인식을 제공 하지만 매개 변수는 메서드 호출에서 보다 일반적으로 사용 됩니다. 따라서 값을 값으로 <xref:System.DateTimeOffset> <xref:System.DateTime> 변환 하거나 그 반대로 변환 하는 기능은 매우 중요 합니다. 이 항목에서는 표준 시간대 정보를 최대한 많이 보존 하는 방식으로 이러한 변환을 수행 하는 방법을 보여 줍니다.

> [!NOTE]
> 표준 시간대 <xref:System.DateTime> 의 시간 <xref:System.DateTimeOffset> 을 나타낼 때와 형식에는 몇 가지 제한 사항이 있습니다. 속성을사용하여은utc(협정세계시)와시스템의현지표준시간대만반영할수있습니다.<xref:System.DateTime.Kind%2A> <xref:System.DateTime> <xref:System.DateTimeOffset>UTC에서의 시간 오프셋을 반영 하지만 해당 오프셋이 속한 실제 표준 시간대를 반영 하지는 않습니다. 표준 시간대에 대 한 시간 값 및 지원에 대 한 자세한 내용은 [DateTime, DateTimeOffset, TimeSpan 및 TimeZoneInfo 중에서 선택](../../../docs/standard/datetime/choosing-between-datetime.md)을 참조 하세요.

## <a name="conversions-from-datetime-to-datetimeoffset"></a>DateTime에서 DateTimeOffset으로 변환

구조 <xref:System.DateTimeOffset> 는 대부분의 변환에 적합 한 <xref:System.DateTime> <xref:System.DateTimeOffset> 변환을 수행 하는 두 가지 동일한 방법을 제공 합니다.

- 값을 기반으로 <xref:System.DateTimeOffset> <xref:System.DateTimeOffset.%23ctor%2A> 새 개체를 만드는 생성자입니다. <xref:System.DateTime>

- 개체에 값을 <xref:System.DateTime> 할당할 수 있는 암시적 변환 연산자입니다. <xref:System.DateTimeOffset>

Utc 및 지역 <xref:System.DateTime> 값의 경우 결과 <xref:System.DateTimeOffset.Offset%2A> <xref:System.DateTimeOffset> 값의 속성은 utc 또는 현지 표준 시간대 오프셋을 정확 하 게 반영 합니다. 예를 들어 다음 코드는 UTC 시간을 해당 하 <xref:System.DateTimeOffset> 는 값으로 변환 합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#1)]

이 경우 `utcTime2` 변수의 오프셋은 00:00입니다. 마찬가지로 다음 코드에서는 현지 시간을 해당 <xref:System.DateTimeOffset> 하는 값으로 변환 합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#2)]

그러나 <xref:System.DateTime.Kind%2A> 속성이 인 <xref:System.DateTime> <xref:System.DateTimeOffset> 값의 경우 이러한 두 변환 메서드는 현지 표준 시간대의 오프셋 인 값을 생성 합니다. <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> 미국 태평양 표준시에서 실행되는 다음 예제에서 이러한 변환을 보여 줍니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#3)]

값이 현지 표준 시간대 또는 UTC와 다른 날짜 및 시간을 반영 하는 경우에는 <xref:System.DateTimeOffset> 값으로 변환 하 고 오버 로드 <xref:System.DateTimeOffset.%23ctor%2A> 된 생성자를 호출 하 여 해당 표준 시간대 정보를 보존할 수 있습니다. <xref:System.DateTime> 예를 들어 다음 예제에서는 중부 표준시 <xref:System.DateTimeOffset> 를 반영 하는 개체를 인스턴스화합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#4)]

이 생성자 오버 로드에 대 한 두 번째 <xref:System.TimeSpan> 매개 변수 (UTC에서의 시간 오프셋을 나타내는 개체)는 시간의 해당 표준 <xref:System.TimeZoneInfo.GetUtcOffset%28System.DateTime%29?displayProperty=nameWithType> 시간대의 메서드를 호출 하 여 검색 해야 합니다. 메서드의 단일 매개 변수 <xref:System.DateTime> 는 변환할 날짜와 시간을 나타내는 값입니다. 표준 시간대에서 일광 절약 시간제를 지원하는 경우 이 매개 변수를 사용하면 특정 날짜와 시간에 적절한 오프셋을 해당 메서드에서 결정할 수 있습니다.

## <a name="conversions-from-datetimeoffset-to-datetime"></a>DateTimeOffset에서 DateTime으로 변환

속성 <xref:System.DateTimeOffset.DateTime%2A> 은 변환을<xref:System.DateTime> 수행 <xref:System.DateTimeOffset> 하는 데 가장 일반적으로 사용 됩니다. 그러나 다음 예제와 같이 <xref:System.DateTime> <xref:System.DateTime.Kind%2A> 속성이 <xref:System.DateTimeKind.Unspecified>인 값을 반환 합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#5)]

즉, <xref:System.DateTimeOffset.DateTime%2A> 속성을 사용 하는 <xref:System.DateTimeOffset> 경우 변환에서 UTC와의 값 관계에 대 한 모든 정보가 손실 됩니다. 이는 <xref:System.DateTimeOffset> 해당 <xref:System.DateTimeOffset.DateTime%2A> 속성에서두표준시간대만반영하므로UTC시간이나시스템의현지시간에해당하는값에<xref:System.DateTime.Kind%2A> 영향을 줍니다.

을 <xref:System.DateTimeOffset> <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=nameWithType> <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> 값으로 변환할 때 표준 시간대 정보를 최대한 많이 유지 하려면 및 속성을 사용할 수 있습니다. <xref:System.DateTime>

### <a name="converting-a-utc-time"></a>UTC 시간 변환

변환 <xref:System.DateTimeOffset.DateTime%2A> 된 값이 UTC 시간 임을 나타내려면 <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=nameWithType> 속성의 값을 검색할 수 있습니다. 속성은 <xref:System.DateTimeOffset.DateTime%2A> 두 가지 방법으로 다릅니다.

- 속성이 인 값을 <xref:System.DateTime> 반환 합니다. <xref:System.DateTimeKind.Utc> <xref:System.DateTime.Kind%2A>

- 속성 값이와 같지 <xref:System.TimeSpan.Zero?displayProperty=nameWithType>않으면 시간을 UTC로 변환 합니다. <xref:System.DateTimeOffset.Offset%2A>

> [!NOTE]
> 응용 프로그램에서 <xref:System.DateTime> 변환 된 값이 특정 시점을 명확 하 게 식별 해야 하는 경우에는 <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=nameWithType> <xref:System.DateTime> 속성을 사용 하 <xref:System.DateTimeOffset> 여 모든 변환을 처리 하는 것이 좋습니다.

다음 코드에서는 <xref:System.DateTimeOffset.UtcDateTime%2A> 속성을 사용 하 여 오프셋이 <xref:System.DateTimeOffset> <xref:System.DateTime> 값과 같은 <xref:System.TimeSpan.Zero?displayProperty=nameWithType> 값을 변환 합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#6)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#6)]

다음 코드에서는 <xref:System.DateTimeOffset.UtcDateTime%2A> 속성을 사용 하 여 <xref:System.DateTimeOffset> 값에 대 한 표준 시간대 변환과 형식 변환을 모두 수행 합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#12)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#12)]

### <a name="converting-a-local-time"></a>현지 시간 변환

<xref:System.DateTimeOffset> 값이 현지 시간을 나타내는 경우 `static` <xref:System.DateTimeOffset.DateTime%2A?displayProperty=nameWithType> 속성에서 반환 된 <xref:System.DateTime> 값을 (`Shared` Visual Basic) <xref:System.DateTime.SpecifyKind%2A> 메서드에 전달할 수 있습니다. 메서드는 전달 된 날짜와 시간을 첫 번째 매개 변수로 반환 하지만 <xref:System.DateTime.Kind%2A> 속성을 두 번째 매개 변수로 지정 된 값으로 설정 합니다. 다음 코드에서는 오프셋이 현지 <xref:System.DateTime.SpecifyKind%2A> 표준 시간대의 값 <xref:System.DateTimeOffset> 과 일치 하는 값을 변환 하는 경우 메서드를 사용 합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#7)]

<xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> 속성을 사용 하 여 <xref:System.DateTimeOffset> 값을 로컬 <xref:System.DateTime> 값으로 변환할 수도 있습니다. <xref:System.DateTimeKind.Local>반환 <xref:System.DateTime.Kind%2A> 된<xref:System.DateTime> 값의 속성은입니다. 다음 코드에서는 오프셋이 현지 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> 표준 시간대의 값 <xref:System.DateTimeOffset> 과 일치 하는 값을 변환할 때 속성을 사용 합니다. 

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#10)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#10)]

<xref:System.DateTime> `get` <xref:System.DateTimeOffset> <xref:System.DateTimeOffset.ToLocalTime%2A> 속성을 사용 하 여 값을 검색 하는 경우 속성의 접근자는 먼저 값을 UTC로 변환한 다음 메서드를 호출 하 여 현지 시간으로 변환 합니다. <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> 즉, <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> 속성에서 값을 검색 하 여 형식 변환을 수행할 때 표준 시간대 변환을 수행할 수 있습니다. 또한 변환을 수행할 때 현지 표준 시간대의 조정 규칙도 적용됩니다. 다음 코드에서는 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> 속성을 사용 하 여 형식과 표준 시간대 변환을 모두 수행 하는 방법을 보여 줍니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#11)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#11)]

### <a name="a-general-purpose-conversion-method"></a>범용 변환 메서드

다음 예제에서는 값을 `ConvertFromDateTimeOffset` <xref:System.DateTime> 값으로 변환 <xref:System.DateTimeOffset> 하는 라는 메서드를 정의 합니다. 해당 오프셋을 기반으로 <xref:System.DateTimeOffset> 값이 UTC 시간, 현지 시간 또는 다른 시간 중 어느 것인지 결정 하 고이에 따라 반환 된 날짜 및 시간 값의 <xref:System.DateTime.Kind%2A> 속성을 정의 합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#8)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#8)]

다음 예제에서는 메서드를 `ConvertFromDateTimeOffset` 호출 하 여 <xref:System.DateTimeOffset> UTC 시간, 현지 시간 및 미국의 시간을 나타내는 값을 변환 합니다. 변환합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#9)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#9)]

이 코드에서는 다음 두 가지를 가정합니다. 이러한 가정은 애플리케이션과 애플리케이션에서 사용하는 날짜 및 시간 값의 소스에 따라 맞지 않을 수도 있습니다.

- 오프셋이 UTC를 <xref:System.TimeSpan.Zero?displayProperty=nameWithType> 나타내는 날짜 및 시간 값이 있다고 가정 합니다. 실제로 UTC는 특정 표준 시간대의 시간이 아니라 표준화된 전세계 표준 시간대의 시간입니다. 표준 시간대의 <xref:System.TimeSpan.Zero>오프셋이 있을 수도 있습니다.

- 현지 표준 시간대 오프셋과 동일한 오프셋의 날짜와 시간이 현지 표준 시간대를 나타낸다고 가정합니다. 그러나 날짜 및 시간 값이 원래 표준 시간대와 관련이 없기 때문에 이와 다른 경우가 있을 수 있습니다. 날짜와 시간은 동일한 오프셋을 사용하는 다른 표준 시간대에서 가져올 수 있습니다.

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
