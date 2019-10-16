---
title: '방법: 포함 리소스에서 표준 시간대 복원'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], deserializing
- time zones [.NET Framework], restoring
ms.assetid: 6b7b4de9-da07-47e3-8f4c-823f81798ee7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 98813bf6685be78d33ebd5cc5e8c07a61a811c25
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106761"
---
# <a name="how-to-restore-time-zones-from-an-embedded-resource"></a>방법: 포함 리소스에서 표준 시간대 복원

이 항목에서는 리소스 파일에 저장 된 표준 시간대를 복원 하는 방법에 대해 설명 합니다. 표준 시간대를 [저장 하는 방법에 대 한 자세한 내용 및 지침은 방법: 포함 리소스](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)에 표준 시간대를 저장 합니다.

### <a name="to-deserialize-a-timezoneinfo-object-from-an-embedded-resource"></a>포함 리소스에서 TimeZoneInfo 개체를 deserialize 하려면

1. 검색할 표준 시간대가 사용자 지정 표준 시간대가 아닌 경우 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 메서드를 사용 하 여 인스턴스화합니다.

2. 포함 된 <xref:System.Resources.ResourceManager> 리소스 파일의 정규화 된 이름과 리소스 파일을 포함 하는 어셈블리에 대 한 참조를 전달 하 여 개체를 인스턴스화합니다.

   포함 된 리소스 파일의 정규화 된 이름을 확인할 수 없으면 [ildasm.exe (IL 디스어셈블러)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 를 사용 하 여 어셈블리의 매니페스트를 검사 합니다. `.mresource` 항목은 리소스를 식별 합니다. 이 `SerializeTimeZoneData.SerializedTimeZones`예제에서 리소스의 정규화 된 이름은입니다.

   리소스 파일이 표준 시간대 인스턴스화 코드를 포함 하는 동일한 어셈블리에 포함 된 경우 `static` (`Shared` Visual Basic) <xref:System.Reflection.Assembly.GetExecutingAssembly%2A> 메서드를 호출 하 여 해당 파일에 대 한 참조를 검색할 수 있습니다.

3. <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 메서드에 대 한 호출이 실패 하거나 사용자 지정 표준 시간대를 인스턴스화하는 경우 메서드를 <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType> 호출 하 여 serialize 된 표준 시간대가 포함 된 문자열을 검색 합니다.

4. 메서드를 <xref:System.TimeZoneInfo.FromSerializedString%2A> 호출 하 여 표준 시간대 데이터를 Deserialize 합니다.

## <a name="example"></a>예제

다음 예제에서는 포함 된 <xref:System.TimeZoneInfo> .net XML 리소스 파일에 저장 된 개체를 deserialize 합니다.

[!code-csharp[TimeZone2.Serialization#3](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#3)]
[!code-vb[TimeZone2.Serialization#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#3)]

이 코드에서는 응용 프로그램에 필요한 <xref:System.TimeZoneInfo> 개체가 있는지 확인 하는 예외 처리를 보여 줍니다. 먼저 메서드를 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 사용 하 여 <xref:System.TimeZoneInfo> 레지스트리에서 개체를 검색 하 여 인스턴스화합니다. 표준 시간대를 인스턴스화할 수 없는 경우 코드는 포함 된 리소스 파일에서 해당 표준 시간대를 검색 합니다.

사용자 지정 표준 시간대 (메서드를 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 사용 하 여 인스턴스화된 표준 시간대)의 데이터는 레지스트리에 저장 되지 않으므로 코드는를 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 호출 하 여 Palmer, 남극 지역에 대 한 표준 시간대를 인스턴스화하지 않습니다. 대신, <xref:System.TimeZoneInfo.FromSerializedString%2A> 메서드를 호출 하기 전에 표준 시간대의 데이터가 포함 된 문자열을 검색 하기 위해 포함 된 리소스 파일을 즉시 찾습니다.

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- 이 프로젝트에는 System.object와 System.object에 대 한 참조가 추가 됩니다.

- 다음 네임 스페이스를 가져옵니다.

  [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
  [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [표준 시간대 개요](../../../docs/standard/datetime/time-zone-overview.md)
- [방법: 포함 리소스에 표준 시간대 저장](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)
