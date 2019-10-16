---
title: '방법: 컴퓨터에 있는 표준 시간대 열거'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], enumerating
- enumerating time zones [.NET Framework]
ms.assetid: bb7a42ab-6bd9-4c5c-b734-5546d51f8669
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: afc3b57659dd6719f72cefba8a6d2f1abe08c0d0
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106646"
---
# <a name="how-to-enumerate-time-zones-present-on-a-computer"></a>방법: 컴퓨터에 있는 표준 시간대 열거

지정한 표준 시간대를 성공적으로 사용하려면 해당 표준 시간대 관련 정보를 시스템에서 사용할 수 있어야 합니다. Windows XP 및 Windows Vista 운영 체제에서는이 정보를 레지스트리에 저장 합니다. 그러나 전세계에 있는 표준 시간대의 전체 수는 상당히 많지만 레지스트리에는 이들 중 일부에 대한 정보만 포함됩니다. 또한 레지스트리 자체도 동적 구조이므로 그 내용이 실수나 고의로 변경될 수 있습니다. 따라서 언제나 애플리케이션에서 특정 표준 시간대가 정의되어 있고 시스템에서 사용할 수 있다고 가정할 수는 없습니다. 표준 시간대 정보 애플리케이션을 사용하는 많은 애플리케이션의 첫 번째 단계는 필요한 표준 시간대를 로컬 시스템에서 사용할 수 있는지를 확인하거나 사용자에게 표준 시간대를 선택할 수 있는 목록을 제공하는 것입니다. 이렇게 하려면 애플리케이션에서 로컬 시스템에 정의되어 있는 표준 시간대를 나열해야 합니다.

> [!NOTE]
> 응용 프로그램에서 로컬 시스템에 정의 되어 있지 않을 수 있는 특정 표준 시간대가 있는 경우 응용 프로그램은 표준 시간대에 대 한 정보를 serialize 하 고 deserialize 하 여 해당 상태를 확인할 수 있습니다. 그러면 응용 프로그램 사용자가 선택할 수 있도록 표준 시간대를 목록 컨트롤에 추가할 수 있습니다. 자세한 내용은 [방법: 포함 리소스](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) 에 표준 시간대를 저장 하 [고 방법: 포함 리소스](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)에서 표준 시간대를 복원 합니다.

### <a name="to-enumerate-the-time-zones-present-on-the-local-system"></a>로컬 시스템에 있는 표준 시간대를 열거하려면

1. <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=nameWithType> 메서드를 호출합니다. 메서드는 개체의 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> <xref:System.TimeZoneInfo> 제네릭 컬렉션을 반환 합니다. 컬렉션의 항목은 해당 <xref:System.TimeZoneInfo.DisplayName%2A> 속성을 기준으로 정렬 됩니다. 예를 들어:

   [!code-csharp[System.TimeZone2.Concepts#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#1)]
   [!code-vb[System.TimeZone2.Concepts#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#1)]

2. 루프 (in <xref:System.TimeZoneInfo> C#) 또는 ...를사용하여컬렉션의개별개체를열거합니다.`For Each` `foreach``Next` 루프 (Visual Basic)를 수행 하 고 각 개체에 필요한 처리를 수행 합니다. 예를 들어 다음 코드는 1 단계 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 에서 반환 <xref:System.TimeZoneInfo> 된 개체의 컬렉션을 열거 하 고 각 표준 시간대의 표시 이름을 콘솔에 나열 합니다.

   [!code-csharp[System.TimeZone2.Concepts#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#12)]
   [!code-vb[System.TimeZone2.Concepts#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#12)]

### <a name="to-present-the-user-with-a-list-of-time-zones-present-on-the-local-system"></a>로컬 시스템에 있는 표준 시간대 목록을 사용자에 게 표시 하려면

1. <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=nameWithType> 메서드를 호출합니다. 메서드는 개체의 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> <xref:System.TimeZoneInfo> 제네릭 컬렉션을 반환 합니다.

2. 1 단계에서 반환 된 컬렉션을 Windows forms `DataSource` 또는 ASP.NET list 컨트롤의 속성에 할당 합니다.

3. 사용자가 <xref:System.TimeZoneInfo> 선택한 개체를 검색 합니다.

이 예에서는 Windows 응용 프로그램에 대 한 설명을 제공 합니다.

## <a name="example"></a>예제

이 예제에서는 목록 상자에 시스템에 정의 된 표준 시간대를 표시 하는 Windows 응용 프로그램을 시작 합니다. 그런 다음 사용자가 선택한 표준 시간대 개체의 <xref:System.TimeZoneInfo.DisplayName%2A> 속성 값을 포함 하는 대화 상자를 표시 합니다.

[!code-csharp[System.TimeZone2.Concepts#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#2)]
[!code-vb[System.TimeZone2.Concepts#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#2)]

대부분의 목록 컨트롤 (예: <xref:System.Windows.Forms.ListBox?displayProperty=nameWithType> 또는 <xref:System.Web.UI.WebControls.BulletedList?displayProperty=nameWithType> 컨트롤)을 사용 하면 해당 컬렉션이 인터페이스를 <xref:System.Collections.IEnumerable> 구현 하는 한 `DataSource` 개체 변수의 컬렉션을 해당 속성에 할당할 수 있습니다. 제네릭 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 클래스는이를 수행 합니다. 컬렉션에 개별 개체를 표시 하기 위해 컨트롤은 개체의 `ToString` 메서드를 호출 하 여 개체를 나타내는 데 사용 되는 문자열을 추출 합니다. 개체의 <xref:System.TimeZoneInfo> 경우 메서드는 `ToString` <xref:System.TimeZoneInfo> 개체의 표시 이름 ( <xref:System.TimeZoneInfo.DisplayName%2A> 속성의 값)을 반환 합니다.

> [!NOTE]
> 목록 컨트롤은 개체 `ToString` 의 메서드를 호출 하기 때문에 개체의 <xref:System.TimeZoneInfo> 컬렉션을 컨트롤에 할당 하 고, 컨트롤에 각 <xref:System.TimeZoneInfo> 개체에 대 한 의미 있는 이름을 표시 하 고, 사용자가 선택한 개체를 검색할 수 있습니다. 이렇게 하면 컬렉션의 각 개체에 대 한 문자열을 추출 하 고, 컨트롤의 `DataSource` 속성에 할당 된 컬렉션에 문자열을 할당 하 고, 사용자가 선택한 문자열을 검색 한 다음,이 문자열을 사용 하 여 개체를 추출할 필요가 없습니다. 설명 합니다. 

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- 다음 네임 스페이스를 가져옵니다.

  <xref:System>( C# 코드)

  <xref:System.Collections.ObjectModel>

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
- [방법: 포함 리소스에 표준 시간대 저장](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)
- [방법: 포함 리소스에서 표준 시간대 복원](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)
