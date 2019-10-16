---
title: '방법: 포함 리소스에 표준 시간대 저장'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], saving
- time zone objects [.NET Framework], serializing
- time zone objects [.NET Framework], saving
ms.assetid: 3c96d83a-a057-4496-abb0-8f4b12712558
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9ca39d989cc7bc16ec2678ba5fa53710899f3ac4
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70107150"
---
# <a name="how-to-save-time-zones-to-an-embedded-resource"></a>방법: 포함 리소스에 표준 시간대 저장

표준 시간대 인식 응용 프로그램은 종종 특정 표준 시간대가 있어야 합니다. 그러나 개별 <xref:System.TimeZoneInfo> 개체의 사용 가능 여부는 로컬 시스템의 레지스트리에 저장 된 정보에 따라 달라 지므로 일반적으로 사용 가능한 표준 시간대도 없을 수 있습니다. 또한 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 메서드를 사용 하 여 인스턴스화된 사용자 지정 표준 시간대에 대 한 정보는 레지스트리에 다른 표준 시간대 정보와 함께 저장 되지 않습니다. 필요할 때 이러한 표준 시간대를 사용할 수 있도록 하려면 serialize 하 여 저장 하 고 나중에 deserialize 하 여 복원할 수 있습니다.

일반적으로 <xref:System.TimeZoneInfo> 개체 직렬화는 표준 시간대 인식 응용 프로그램과는 차이가 있습니다. 직렬화 <xref:System.TimeZoneInfo> 된 개체를 저장 하는 데 사용 되는 데이터 저장소에 따라, 데이터를 레지스트리의 응용 프로그램 키에 저장 하는 경우와 같이 설치 또는 설치 루틴의 일부로 표준 시간대 데이터를 직렬화 하거나, 실행 되는 유틸리티 루틴의 일부로 직렬화 할 수 있습니다. serialize 된 데이터가 .NET XML 리소스 (.resx) 파일에 저장 되는 경우와 같이 최종 응용 프로그램이 컴파일됩니다.

응용 프로그램을 사용 하 여 컴파일되는 리소스 파일 외에도 여러 다른 데이터 저장소를 표준 시간대 정보에 사용할 수 있습니다. 여기에는 다음과 같은 옵션이 포함됩니다.

- 레지스트리입니다. 응용 프로그램은 자체 응용 프로그램 키의 하위 키를 사용 하 여 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time 영역의 하위 키를 사용 하는 대신 사용자 지정 표준 시간대 데이터를 저장 해야 합니다.

- 구성 파일.

- 기타 시스템 파일.

### <a name="to-save-a-time-zone-by-serializing-it-to-a-resx-file"></a>.Resx 파일로 serialize 하 여 표준 시간대를 저장 하려면

1. 기존 표준 시간대를 검색 하거나 새 표준 시간대를 만듭니다.

   기존 표준 시간대 [를 검색 하려면 방법: 미리 정의 된 UTC 및 현지 표준 시간대 개체](../../../docs/standard/datetime/access-utc-and-local.md) 에 [액세스 하 고 방법: TimeZoneInfo 개체](../../../docs/standard/datetime/instantiate-time-zone-info.md)를 인스턴스화합니다.

   새 표준 시간대를 만들려면 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 메서드의 오버 로드 중 하나를 호출 합니다. 자세한 내용은 [방법: 조정 규칙](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md) 을 사용 하지 않고 표준 [시간대 만들기 및 방법: 조정 규칙](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)을 사용 하 여 표준 시간대를 만듭니다.

2. 메서드를 <xref:System.TimeZoneInfo.ToSerializedString%2A> 호출 하 여 표준 시간대의 데이터를 포함 하는 문자열을 만듭니다.

3. 이름 및 <xref:System.IO.StreamWriter> 선택적으로 .resx 파일의 경로를 <xref:System.IO.StreamWriter> 클래스 생성자에 제공 하 여 개체를 인스턴스화합니다.

4. <xref:System.IO.StreamWriter> 개체를 <xref:System.Resources.ResXResourceWriter> <xref:System.Resources.ResXResourceWriter> 클래스 생성자에 전달 하 여 개체를 인스턴스화합니다.

5. 표준 시간대의 직렬화 된 문자열 <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=nameWithType> 을 메서드에 전달 합니다.

6. <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType> 메서드를 호출합니다.

7. <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=nameWithType> 메서드를 호출합니다.

8. <xref:System.IO.StreamWriter> 해당<xref:System.IO.StreamWriter.Close%2A> 메서드를 호출 하 여 개체를 닫습니다.

9. 생성 된 .resx 파일을 응용 프로그램의 Visual Studio 프로젝트에 추가 합니다.

10. Visual Studio의 **속성** 창을 사용 하 여 .resx 파일의 **빌드 작업** 속성이 **포함 리소스**로 설정 되었는지 확인 합니다.

## <a name="example"></a>예제

다음 예제에서는 중앙 표준 <xref:System.TimeZoneInfo> 시간을 나타내는 개체 <xref:System.TimeZoneInfo> 와 Palmer 스테이션을 나타내는 개체를 SerializedTimeZones 라는 .net XML 리소스 파일에 serialize 합니다. 일반적으로 중부 표준시는 레지스트리에 정의 되어 있습니다. Palmer 국, 남극 사용자 지정 표준 시간대입니다.

[!code-csharp[TimeZone2.Serialization#1](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#1)]
[!code-vb[TimeZone2.Serialization#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#1)]

이 예제에서는 <xref:System.TimeZoneInfo> 컴파일 타임에 리소스 파일에서 사용할 수 있도록 개체를 serialize 합니다.

메서드는 <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=nameWithType> .net XML 리소스 파일에 전체 헤더 정보를 추가 하므로 기존 파일에 리소스를 추가 하는 데 사용할 수 없습니다. 이 예제에서는 SerializedTimeZones 파일을 확인 하 고, 있는 경우 두 개의 serialize 된 표준 시간대 이외의 모든 리소스를 제네릭 <xref:System.Collections.Generic.Dictionary%602> 개체에 저장 하 여이를 처리 합니다. 그러면 기존 파일이 삭제 되 고 기존 리소스가 새 SerializedTimeZones 파일에 추가 됩니다. Serialize 된 표준 시간대 데이터도이 파일에 추가 됩니다.

리소스의 키 (또는 **이름**) 필드에는 공백이 포함 되 면 안 됩니다. <xref:System.String.Replace%28System.String%2CSystem.String%29> 메서드를 호출 하 여 리소스 파일에 할당 되기 전에 표준 시간대 식별자의 포함 된 모든 공백을 제거 합니다.

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- 이 프로젝트에는 System.object와 System.object에 대 한 참조가 추가 됩니다.

- 다음 네임 스페이스를 가져옵니다.

  [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
  [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [표준 시간대 개요](../../../docs/standard/datetime/time-zone-overview.md)
- [방법: 포함 리소스에서 표준 시간대 복원](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)
