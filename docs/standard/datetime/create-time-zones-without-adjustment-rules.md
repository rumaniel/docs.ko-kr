---
title: '방법: 조정 규칙을 사용하지 않고 표준 시간대 만들기'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], adjustment rule
- time zones [.NET Framework], creating
- adjustment rule [.NET Framework]
ms.assetid: a6af8647-7893-4f29-95a9-d94c65a6e8dd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 510112c8b19ec002d1dcf918eb983b55dee68fd0
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106663"
---
# <a name="how-to-create-time-zones-without-adjustment-rules"></a>방법: 조정 규칙을 사용하지 않고 표준 시간대 만들기

응용 프로그램에 필요한 정확한 표준 시간대 정보는 다음과 같은 여러 가지 이유로 특정 시스템에 표시 되지 않을 수 있습니다.

- 현지 시스템의 레지스트리에서 표준 시간대가 정의 되지 않았습니다.

- 표준 시간대에 대 한 데이터가 레지스트리에서 수정 되었거나 제거 되었습니다.

- 표준 시간대가 있지만 특정 기록 기간의 표준 시간대 조정에 대 한 정확한 정보가 없습니다.

이러한 경우 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 메서드를 호출 하 여 응용 프로그램에 필요한 표준 시간대를 정의할 수 있습니다. 이 메서드의 오버 로드를 사용 하 여 조정 규칙을 사용 하거나 사용 하지 않고 표준 시간대를 만들 수 있습니다. 표준 시간대가 일광 절약 시간을 지 원하는 경우 고정 또는 부동 조정 규칙을 사용 하 여 조정을 정의할 수 있습니다. 이러한 용어에 대 한 정의는 [표준 시간대 개요](../../../docs/standard/datetime/time-zone-overview.md)의 "표준 시간대 용어" 섹션을 참조 하세요.

> [!IMPORTANT]
> 메서드를 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 호출 하 여 만든 사용자 지정 표준 시간대는 레지스트리에 추가 되지 않습니다. 대신 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 메서드 호출에서 반환 되는 개체 참조를 통해서만 액세스할 수 있습니다.

이 항목에서는 조정 규칙을 사용 하지 않고 표준 시간대를 만드는 방법을 보여 줍니다. 일광 절약 시간 조정 규칙을 [지 원하는 표준 시간대를 만들려면 방법: 조정 규칙](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)을 사용 하 여 표준 시간대를 만듭니다.

### <a name="to-create-a-time-zone-without-adjustment-rules"></a>조정 규칙을 사용 하지 않고 표준 시간대를 만들려면

1. 표준 시간대의 표시 이름을 정의 합니다.

   표시 이름은 UTC (협정 세계시)의 표준 시간대 오프셋을 괄호로 묶고 표준 시간대를 나타내는 문자열, 표준 시간대의 하나 이상의 도시 또는 하나 이상의 cou를 나타내는 문자열을 따르는 매우 일반적인 형식입니다. n 번 시도 하거나 표준 시간대의 지역입니다.

2. 표준 시간대의 표준 시간 이름을 정의 합니다. 일반적으로이 문자열은 표준 시간대의 식별자로도 사용 됩니다.

3. 표준 시간대의 표준 이름과 다른 식별자를 사용 하려면 표준 시간대 식별자를 정의 합니다.

4. UTC에서 <xref:System.TimeSpan> 표준 시간대의 오프셋을 정의 하는 개체를 인스턴스화합니다. 시간이 UTC 보다 늦은 표준 시간대에는 양의 오프셋이 있습니다. 시간이 UTC 보다 이전인 표준 시간대에는 음의 오프셋이 있습니다.

5. 메서드를 <xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%29?displayProperty=nameWithType> 호출 하 여 새 표준 시간대를 인스턴스화합니다.

## <a name="example"></a>예제

다음 예제에서는 조정 규칙이 없는 모슨에 대 한 사용자 지정 표준 시간대를 정의 합니다.

[!code-csharp[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#1)]
[!code-vb[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#1)]

<xref:System.TimeZoneInfo.DisplayName%2A> 속성에 할당 된 문자열은 표준 시간대의 오프셋 뒤에 표준 시간대에 대 한 설명이 표시 되는 표준 형식을 따릅니다.

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- 다음 네임 스페이스를 가져옵니다.

  [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
  [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [표준 시간대 개요](../../../docs/standard/datetime/time-zone-overview.md)
- [방법: 조정 규칙을 사용 하 여 표준 시간대 만들기](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)
