---
title: 표준 시간대 저장 및 복원
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- restoring time zones
- deserialization [.NET Framework], time zones
- serialization [.NET Framework], time zones
- time zone objects [.NET Framework], restoring
- saving time zones
- time zone objects [.NET Framework], deserializing
- time zones [.NET Framework], saving
- time zones [.NET Framework], restoring
- time zone objects [.NET Framework], serializing
- time zone objects [.NET Framework], saving
ms.assetid: 4028b310-e7ce-49d4-a646-1e83bfaf6f9d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ea44b29eaa0273baadbf02093108bc4da912a3e5
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106739"
---
# <a name="saving-and-restoring-time-zones"></a>표준 시간대 저장 및 복원

클래스 <xref:System.TimeZoneInfo> 는 레지스트리를 사용 하 여 미리 정의 된 표준 시간대 데이터를 검색 합니다. 그러나 레지스트리는 동적 구조입니다. 또한 레지스트리가 포함 하는 표준 시간대 정보는 운영 체제에서 주로 현재 연도의 시간 조정 및 변환을 처리 하는 데 사용 됩니다. 이는 정확한 표준 시간대 데이터를 사용 하는 응용 프로그램에 대 한 두 가지 주요 영향을 갖습니다.

- 응용 프로그램에 필요한 표준 시간대가 레지스트리에 정의 되어 있지 않거나 레지스트리에서 제거 되었거나 이름이 바뀌었을 수 있습니다.

- 레지스트리에 정의 된 표준 시간대에는 기록 표준 시간대 변환에 필요한 특정 조정 규칙에 대 한 정보가 부족할 수 있습니다.

클래스 <xref:System.TimeZoneInfo> 는 표준 시간대 데이터의 serialization (저장) 및 deserialization (복원)을 지원 하 여 이러한 제한 사항을 해결 합니다.

## <a name="time-zone-serialization-and-deserialization"></a>표준 시간대 직렬화 및 deserialization

표준 시간대 데이터를 serialize 및 deserialize 하 여 표준 시간대를 저장 하 고 복원 하는 작업에는 두 개의 메서드 호출만 포함 됩니다.

- 개체의 <xref:System.TimeZoneInfo> <xref:System.TimeZoneInfo.ToSerializedString%2A> 메서드를 호출 하 여 개체를 serialize 할 수 있습니다. 메서드는 매개 변수를 사용 하지 않고 표준 시간대 정보를 포함 하는 문자열을 반환 합니다.

- <xref:System.TimeZoneInfo> 해당 문자열 `static` 을 (`Shared` Visual Basic )<xref:System.TimeZoneInfo.FromSerializedString%2A?displayProperty=nameWithType> 메서드에 전달 하 여 serialize 된 문자열에서 개체를 deserialize 할 수 있습니다.

## <a name="serialization-and-deserialization-scenarios"></a>Serialization 및 deserialization 시나리오

<xref:System.TimeZoneInfo> 개체를 문자열에 저장 하거나 serialize 하 고 나중에 사용 하기 위해 복원 (또는 deserialize) 하는 기능을 사용 하면 유틸리티와 <xref:System.TimeZoneInfo> 클래스의 유연성이 모두 향상 됩니다. 이 섹션에서는 serialization 및 deserialization이 가장 유용한 상황 중 일부를 검사 합니다.

### <a name="serializing-and-deserializing-time-zone-data-in-an-application"></a>응용 프로그램에서 표준 시간대 데이터 serialize 및 deserialize

필요한 경우 문자열에서 serialize 된 표준 시간대를 복원할 수 있습니다. 레지스트리에서 검색 한 표준 시간대가 특정 날짜 범위 내에서 날짜 및 시간을 올바르게 변환할 수 없는 경우 응용 프로그램에서이 작업을 수행할 수 있습니다. 예를 들어 Windows XP 레지스트리에서 표준 시간대 데이터는 단일 조정 규칙을 지원 하 고 Windows Vista 레지스트리에 정의 된 표준 시간대는 일반적으로 두 가지 조정 규칙에 대 한 정보를 제공 합니다. 즉, 기록 시간 변환이 정확 하지 않을 수 있습니다. 표준 시간대 데이터의 Serialization 및 deserialization은 이러한 제한을 처리할 수 있습니다.

다음 예제에서는 조정 규칙이 없는 사용자 <xref:System.TimeZoneInfo> 지정 클래스를 정의 하 여 미국 미국의 일광 절약 시간이 도입 되기 전에 1883에서 1917 까지의 동부 표준 시간대입니다. 사용자 지정 표준 시간대는 전역 범위를 갖는 변수에 serialize 됩니다. 표준 시간대 변환 메서드인 `ConvertUtcTime`는 변환할 utc (협정 세계시) 시간에 전달 됩니다. 1917 또는 이전 버전에서 날짜 및 시간이 발생 하는 경우 사용자 지정 동부 표준 표준 시간대는 직렬화 된 문자열에서 복원 되 고 레지스트리에서 검색 된 표준 시간대를 대체 합니다.

[!code-csharp[System.TimeZone2.Serialization.1#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/cs/Serialization.cs#1)]
[!code-vb[System.TimeZone2.Serialization.1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/vb/Serialization.vb#1)]

### <a name="handling-time-zone-exceptions"></a>표준 시간대 예외 처리

레지스트리는 동적 구조 이므로 해당 콘텐츠는 실수나 의도적인 수정이 적용 됩니다. 즉, 레지스트리에 정의 되어야 하며 응용 프로그램을 성공적으로 실행 하는 데 필요한 표준 시간대가 없을 수 있습니다. 표준 시간대 serialization 및 deserialization을 지원 하지 않으면 응용 프로그램을 종료 하 여 결과 <xref:System.TimeZoneNotFoundException> 를 처리 하는 것이 거의 선택 되지 않습니다. 그러나 표준 시간대 serialization 및 deserialization을 사용 하면 serialize 된 문자열에서 필요한 표준 <xref:System.TimeZoneNotFoundException> 시간대를 복원 하 여 예기치 않은을 처리할 수 있으며 응용 프로그램은 계속 실행 됩니다.

다음 예제에서는 사용자 지정 중부 표준 시간대를 만들고 serialize 합니다. 그런 다음 레지스트리에서 중앙 표준 시간대 검색을 시도 합니다. 검색 작업에서 <xref:System.TimeZoneNotFoundException> <xref:System.InvalidTimeZoneException>또는를 throw 하는 경우 예외 처리기가 표준 시간대를 deserialize 합니다.

[!code-csharp[System.TimeZone2.Serialization.2#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/cs/Serialization2.cs#1)]
[!code-vb[System.TimeZone2.Serialization.2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/vb/Serialization2.vb#1)]

### <a name="storing-a-serialized-string-and-restoring-it-when-needed"></a>Serialize 된 문자열 저장 및 필요할 때 복원

이전 예에서는 표준 시간대 정보를 문자열 변수에 저장 하 고 필요할 때 복원 했습니다. 그러나 serialize 된 표준 시간대 정보를 포함 하는 문자열은 외부 파일, 응용 프로그램에 포함 된 리소스 파일 또는 레지스트리와 같은 일부 저장 미디어에 저장 될 수 있습니다. 사용자 지정 표준 시간대에 대 한 정보는 레지스트리의 시스템 표준 시간대 키와 별도로 저장 해야 합니다.

이러한 방식으로 serialize 된 표준 시간대 문자열을 저장 하면 표준 시간대 생성 루틴이 응용 프로그램 자체와 구분 됩니다. 예를 들어 표준 시간대 만들기 루틴은 응용 프로그램에서 사용할 수 있는 기록 표준 시간대 정보가 포함 된 데이터 파일을 실행 하 고 만들 수 있습니다. 그런 다음 응용 프로그램에 데이터 파일을 설치 하 고, 응용 프로그램에서 필요할 때 해당 표준 시간대를 하나 이상 deserialize 할 수 있습니다.

포함 된 리소스를 사용 하 여 serialize 된 표준 시간대 데이터를 저장 하는 [예제를 보려면 방법: 포함 리소스](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) 에 표준 시간대를 저장 하 [고 방법: 포함 리소스](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)에서 표준 시간대를 복원 합니다.

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
