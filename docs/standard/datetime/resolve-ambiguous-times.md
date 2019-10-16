---
title: '방법: 모호한 시간 확인'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], ambiguous time
- ambiguous time [.NET Framework]
ms.assetid: 2cf5fb25-492c-4875-9245-98cac8348e97
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6e98d5d8240492ca30da2825b72277d7a35f97f6
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106779"
---
# <a name="how-to-resolve-ambiguous-times"></a>방법: 모호한 시간 확인

모호한 시간은 하나 이상의 UTC(협정 세계시)를 매핑하는 시간입니다. 표준 시간대의 일광 절약 시간에서 표준 시간으로 전환하는 것과 같이 클록 시간을 뒤로 조정하는 경우 발생합니다. 모호한 시간을 처리하는 경우 다음 중 하나를 수행할 수 있습니다.

- 시간을 UTC로 매핑하는 방법에 대해 가정합니다. 예를 들어 있는 모호한 시간을 항상 표준 시간대의 표준 시간으로 표시한다고 가정할 수 있습니다.

- 모호한 시간이 사용자로부터 입력된 데이터 항목인 경우 사용자가 모호성을 해결하도록 맡기면 됩니다.

이 항목에서는 모호한 시간을 표준 시간대의 표준 시간을 나타내는 것으로 가정 하 여 해결 하는 방법을 보여 줍니다.

### <a name="to-map-an-ambiguous-time-to-a-time-zones-standard-time"></a>모호한 시간을 표준 시간대의 표준 시간으로 매핑하려면

1. 시간이 모호한 지 여부를 확인 하려면 메서드를호출합니다.<xref:System.TimeZoneInfo.IsAmbiguousTime%2A>

2. 시간이 모호한 경우 표준 시간대의 <xref:System.TimeSpan> <xref:System.TimeZoneInfo.BaseUtcOffset%2A> 속성에 의해 반환 된 개체에서 시간을 뺍니다.

3. <xref:System.DateTime.Kind%2A> <xref:System.DateTimeKind.Utc?displayProperty=nameWithType>(Visual Basic .net )<xref:System.DateTime.SpecifyKind%2A> 메서드를 호출 하 여 UTC 날짜 및 시간 값의 속성을로 설정 합니다.`Shared` `static`

## <a name="example"></a>예제

다음 예제에서는 모호한 시간을 UTC로 변환 하는 방법을 보여 줍니다 .이는 현지 표준 시간대의 표준 시간을 나타냅니다.

[!code-csharp[System.TimeZone2.Concepts#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#10)]
[!code-vb[System.TimeZone2.Concepts#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#10)]

예제는 전달 된 `ResolveAmbiguousTime` <xref:System.DateTime> 값이 모호한 지 여부를 결정 하는 라는 메서드로 구성 됩니다. 값이 모호한 경우 메서드는 해당 UTC 시간을 <xref:System.DateTime> 나타내는 값을 반환 합니다. 메서드는 현지 시간에서 현지 표준 시간대 <xref:System.TimeZoneInfo.BaseUtcOffset%2A> 의 속성 값을 빼서이 변환을 처리 합니다.

일반적으로 모호한 시간의 가능한 UTC 오프셋을 포함 하 <xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A> 는 개체의 <xref:System.TimeSpan> 배열을 검색 하기 위해 메서드를 호출 하 여 모호한 시간을 처리 합니다. 그러나 이 예제에서는 모호한 시간이 표준 시간대의 표준 시간으로 항상 매핑되어야 한다고 임의로 가정합니다. 속성 <xref:System.TimeZoneInfo.BaseUtcOffset%2A> 은 UTC와 표준 시간대의 표준 시간 사이의 오프셋을 반환 합니다.

이 예제에서는 로컬 표준 시간대에 대 한 모든 참조가 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> 속성을 통해 수행 됩니다. 로컬 표준 시간대는 개체 변수에 할당 되지 않습니다. 이 방법은 <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=nameWithType> 메서드를 호출 하 여 현지 표준 시간대가 할당 된 모든 개체를 무효화 하기 때문에 권장 되는 방법입니다.

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- 문을 사용 하 여 C# 네임 스페이스를 가져옵니다 (코드에 필요) <xref:System> `using` .

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [방법: 사용자가 모호한 시간을 확인 하도록 허용](../../../docs/standard/datetime/let-users-resolve-ambiguous-times.md)
