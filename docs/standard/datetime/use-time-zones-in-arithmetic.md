---
title: '방법: 날짜 및 시간 산술 연산에서 표준 시간대 사용'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], arithmetic operations
- arithmetic operations [.NET Framework], dates and times
- dates [.NET Framework], adding and subtracting
ms.assetid: 83dd898d-1338-415d-8cd6-445377ab7871
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 417d8f00c9323f096a2d6228e853a55b1573f48c
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106711"
---
# <a name="how-to-use-time-zones-in-date-and-time-arithmetic"></a>방법: 날짜 및 시간 산술 연산에서 표준 시간대 사용

일반적으로 또는 <xref:System.DateTime> <xref:System.DateTimeOffset> 값을 사용 하 여 날짜 및 시간 산술 연산을 수행 하는 경우 결과는 표준 시간대 조정 규칙을 반영 하지 않습니다. 이는 날짜 및 시간 값의 표준 시간대를 명확 하 게 식별할 수 있는 경우에도 마찬가지입니다 (예 <xref:System.DateTime.Kind%2A> : 속성이로 <xref:System.DateTimeKind.Local>설정 된 경우). 이 항목에서는 특정 표준 시간대에 속하는 날짜 및 시간 값에 대 한 산술 연산을 수행 하는 방법을 보여 줍니다. 산술 연산 작업의 결과는 표준 시간대의 조정 규칙을 반영합니다.

### <a name="to-apply-adjustment-rules-to-date-and-time-arithmetic"></a>날짜 및 시간 산술 연산에 조정 규칙을 적용하려면

1. 날짜 및 시간 값을 속해 있는 표준 시간대와 밀접하게 연결하는 몇 가지 메서드를 구현합니다. 예를 들어, 날짜 및 시간 값 및 해당 표준 시간대를 모두 포함하는 구조체를 선언합니다. 다음 예제에서는이 방법을 사용 하 여 값 <xref:System.DateTime> 을 표준 시간대와 연결 합니다.

   [!code-csharp[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#6)]
   [!code-vb[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#6)]

2. <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> 메서드나<xref:System.TimeZoneInfo.ConvertTime%2A> 메서드를 호출 하 여 시간을 utc (협정 세계시)로 변환 합니다.

3. UTC 시간에 대한 산술 연산을 수행합니다.

4. 메서드를 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTime%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> 호출 하 여 시간을 UTC에서 원래 시간의 연결 된 표준 시간대로 변환 합니다.

## <a name="example"></a>예제

다음 예제에서는 중부 표준시 2008년 3월 9일 오전 1시 30분에 2시간 30분을 추가합니다. 30분 뒤인 2008년 3월 9일 오전 2시에 표준 시간대가 일광 절약 시간으로 전환됩니다. 이 예제에서는 이전 섹션의 네 단계를 수행하므로 결과 시간이 2008년 3월 9일 오전 5시로 올바르게 이전 코드와 유사합니다.

[!code-csharp[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual8.cs#8)]
[!code-vb[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual8.vb#8)]

<xref:System.DateTime> 및<xref:System.DateTimeOffset> 값은 모두 속할 수 있는 표준 시간대에서 분리 됩니다. 자동으로 표준 시간대의 조정 규칙을 적용하는 방식으로 날짜 및 시간 산술 연산을 수행하려면 모든 날짜 및 시간 값이 속해 있는 표준 시간대를 즉시 식별할 수 있어야 합니다. 즉, 날짜 및 시간과 관련된 표준 시간대는 밀접하게 결합되어야 합니다. 여러 가지 방법을 통해 다음을 포함하는 작업을 수행할 수 있습니다.

- 애플리케이션에서 사용되는 모든 시간이 특정 표준 시간대에 속한다고 가정합니다. 일부 경우에는 적합하지만 이 방식은 제한된 유연성과 이식성을 제공합니다.

- 모두 형식의 필드로 포함하여 관련된 표준 시간대와 날짜 및 시간을 밀접하게 결합하는 형식을 정의합니다. 이 방법은 코드 예제에 사용되며 여기서 두 개의 구성원 필드에 있는 날짜 및 시간과 표준 시간대를 저장하는 구조체를 정의합니다.

이 예제에서는 표준 시간대 조정 규칙이 결과에 <xref:System.DateTime> 적용 되도록 값에 대 한 산술 연산을 수행 하는 방법을 보여 줍니다. 그러나 값 <xref:System.DateTimeOffset> 을 쉽게 사용할 수 있습니다. 다음 예제에서는 원래 예제의 코드를 <xref:System.DateTimeOffset> <xref:System.DateTime> 값 대신 사용 하도록 조정 하는 방법을 보여 줍니다.

[!code-csharp[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#7)]

이러한 추가 작업이 먼저 <xref:System.DateTimeOffset> 값에 대해 수행 되는 경우에는 값을 먼저 UTC로 변환 하지 않고 결과는 올바른 시점을 반영 하지만 해당 오프셋은 해당 시간에 대해 지정 된 표준 시간대의 오프셋을 반영 하지 않습니다.

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- 문을 사용 하 여 C# 네임 스페이스를 가져옵니다 (코드에 필요) <xref:System> `using` .

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [날짜 및 시간에 대한 산술 연산 수행](../../../docs/standard/datetime/performing-arithmetic-operations.md)
