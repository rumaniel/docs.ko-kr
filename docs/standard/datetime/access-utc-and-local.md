---
title: '방법: 미리 정의된 UTC 및 현지 표준 시간대 개체에 액세스'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], local
- predefined time zones
- UTC times, predefined
- local time zone access
- time zones [.NET Framework], retrieving
- time zones [.NET Framework], UTC
ms.assetid: 961fb70b-83f0-4dab-a042-cb5fcd817cf5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8aa19118ce0837b9ce0eb523f3e086fcbcecb9e8
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106561"
---
# <a name="how-to-access-the-predefined-utc-and-local-time-zone-objects"></a>방법: 미리 정의된 UTC 및 현지 표준 시간대 개체에 액세스

클래스 <xref:System.TimeZoneInfo> 는 미리 정의 된 표준 <xref:System.TimeZoneInfo.Utc%2A> 시간대 <xref:System.TimeZoneInfo.Local%2A>개체에 대 한 코드 액세스를 제공 하는 및의 두 속성을 제공 합니다. 이 항목에서는 이러한 속성들이 반환하는 <xref:System.TimeZoneInfo> 개체에 액세스하는 방법에 설명합니다.

### <a name="to-access-the-coordinated-universal-time-utc-timezoneinfo-object"></a>UTC TimeZoneInfo 개체에 액세스하려면

1. (Visual Basic)`Shared` 속성을 사용 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType> 하 여 utc (협정 세계시)에 액세스 합니다. `static`

2. 속성에서 반환 하 <xref:System.TimeZoneInfo> 는 개체를 개체 변수에 할당 하는 대신 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType> 속성을 통해 협정 세계시에 계속 액세스 합니다.

### <a name="to-access-the-local-time-zone"></a>현지 표준 시간대 TimeZoneInfo 개체에 액세스하려면

1. `static` (VisualBasic`Shared` ) 속성을사용하여<xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> 로컬 시스템 표준 시간대에 액세스 합니다.

2. 속성에서 반환 하 <xref:System.TimeZoneInfo> 는 개체를 개체 변수에 할당 하는 대신 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> 속성을 통해 현지 표준 시간대에 계속 액세스 합니다.

## <a name="example"></a>예제

다음 코드에서는 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> 및 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType> 속성을 사용하여 시간을 미국 및 캐나다 동부 표준 시간대에서 변환하고 해당 표준 시간대 이름을 콘솔에 표시합니다.

[!code-csharp[System.TimeZone2.Concepts#13](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#13)]
[!code-vb[System.TimeZone2.Concepts#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#13)]

항상 통해 현지 표준 시간대에 액세스 해야 합니다 <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> 현지 시간을 할당 하는 것이 아니라 속성 시간대를 <xref:System.TimeZoneInfo> 개체 변수입니다. 마찬가지로 <xref:System.TimeZoneInfo> 개체 변수에 utc 영역을 할당 하는 대신 속성 <xref:System.TimeZoneInfo.Utc%2A?displayProperty=nameWithType> 을 통해 항상 협정 세계시에 액세스 해야 합니다. 그래야 합니다 <xref:System.TimeZoneInfo> 개체 변수를 호출 하 여 무효화 하지는 <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=nameWithType> 메서드.

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- 문을 사용 하 여 C# 네임 스페이스를 가져옵니다 (코드에 필요) <xref:System> `using` .

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [로컬 시스템에 정의된 표준 시간대 찾기](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)
- [방법: TimeZoneInfo 개체 인스턴스화](../../../docs/standard/datetime/instantiate-time-zone-info.md)
