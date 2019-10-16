---
title: 로컬 시스템에 정의된 표준 시간대 찾기
ms.date: 04/10/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- time zones [.NET Framework], local
- time zones [.NET Framework], finding local system time zones
- time zone identifiers [.NET Framework]
- local time zone access
- time zones [.NET Framework], retrieving
- UTC times, finding local system time zones
- time zones [.NET Framework], UTC
ms.assetid: 3f63b1bc-9a4b-4bde-84ea-ab028a80d3e1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a65798c46b01bb7a702559d685590ecf7a6f2793
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61819758"
---
# <a name="finding-the-time-zones-defined-on-a-local-system"></a>로컬 시스템에 정의된 표준 시간대 찾기

<xref:System.TimeZoneInfo> 클래스는 public 생성자를 노출하지 않습니다. 따라서 `new` 키워드는 새 <xref:System.TimeZoneInfo> 개체를 만드는 데 사용할 수 없습니다. 대신, <xref:System.TimeZoneInfo> 개체는 레지스트리에서 미리 정의된 표준 시간대에 대한 정보를 검색하거나 사용자 지정 표준 시간대를 만드는 방식으로 인스턴스화됩니다. 이 항목에서는 레지스트리에 저장된 데이터에서 표준 시간대를 인스턴스화하는 방법을 설명합니다. 또한 <xref:System.TimeZoneInfo> 클래스의 `static`(Visual Basic의 `shared`) 속성은 협정 세계시(UTC) 및 로컬 시간대에 대한 액세스를 제공합니다.

> [!NOTE]
> 레지스트리에 정의되지 않은 표준 시간대의 경우 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 메서드의 오버로드를 호출하여 사용자 지정 시간대를 만들 수 있습니다. 에 설명 되어 사용자 지정 표준 시간대 만들기는 [방법: 표준 시간대 조정 규칙 없이 만들](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md) 고 [방법: 표준 시간대 조정 규칙을 사용 하 여 만들기](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md) 항목입니다. 또한 <xref:System.TimeZoneInfo.FromSerializedString%2A> 메서드를 사용하여 serialize된 문자열에서 복원하는 방식으로 <xref:System.TimeZoneInfo> 개체를 인스턴스화할 수 있습니다. 직렬화 및 역직렬화를 <xref:System.TimeZoneInfo> 개체에서 설명 된 [방법: 포함된 리소스에 표준 시간대 저장](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) 고 [방법: 포함 리소스에서 표준 시간대 복원](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md) 항목입니다.

## <a name="accessing-individual-time-zones"></a>개별 표준 시간대에 액세스

<xref:System.TimeZoneInfo> 클래스는 UTC 시간과 로컬 시간대를 나타내는 미리 정의 된 표준 시간대 개체 두 개를 제공합니다. 두 개체는 각각 <xref:System.TimeZoneInfo.Utc%2A> 및 <xref:System.TimeZoneInfo.Local%2A> 속성에서 사용할 수 있습니다. UTC 또는 현지 표준 시간대 액세스에 대 한 자세한 내용은 참조 하세요. [방법: 미리 정의 된 UTC 및 현지 표준 시간대 개체에 액세스할](../../../docs/standard/datetime/access-utc-and-local.md)합니다.

또한 레지스트리에 정의된 표준 시간대를 나타내는 <xref:System.TimeZoneInfo> 개체를 인스턴스화할 수 있습니다. 에 대 한 지침은 특정 표준 시간대 개체 인스턴스화를 [방법: TimeZoneInfo 개체 인스턴스화](../../../docs/standard/datetime/instantiate-time-zone-info.md)합니다.

## <a name="time-zone-identifiers"></a>표준 시간대 식별자

표준 시간대 식별자는 표준 시간대를 고유하게 식별하는 키 필드입니다. 대부분 키는 비교적 짧지만 표준 시간대 식별자는 비교적 깁니다. 대부분 경우에 해당 값은 표준 시간대의 표준 시간 이름을 제공하는 데 사용되는 <xref:System.TimeZoneInfo.StandardName%2A?displayProperty=nameWithType> 속성에 해당합니다. 그러나 예외 사항이 있습니다. 올바른 식별자를 제공하는지 확인하는 가장 좋은 방법은 시스템에서 사용 가능한 표준 시간대를 열거하고 관련 식별자를 확인하는 것입니다.

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [방법: 미리 정의 된 UTC 및 현지 표준 시간대 개체에 액세스](../../../docs/standard/datetime/access-utc-and-local.md)
- [방법: TimeZoneInfo 개체 인스턴스화](../../../docs/standard/datetime/instantiate-time-zone-info.md)
- [표준 시간대 간에 시간 변환](../../../docs/standard/datetime/converting-between-time-zones.md)
