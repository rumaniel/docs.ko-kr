---
title: UI 자동화 ExpandCollapse 컨트롤 패턴 구현
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, ExpandCollapse control pattern
- ExpandCollapse control pattern
- control patterns, ExpandCollapse
ms.assetid: 1dbabb8c-0d68-47c1-a35e-1c01cb01af26
ms.openlocfilehash: 232bceba8286c2566a7df03b9001a5c43b348b20
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043456"
---
# <a name="implementing-the-ui-automation-expandcollapse-control-pattern"></a>UI 자동화 ExpandCollapse 컨트롤 패턴 구현

> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).

이 항목에서는 속성, 메서드 및 이벤트에 대한 정보를 포함하여 <xref:System.Windows.Automation.Provider.IExpandCollapseProvider>를 구현하기 위한 지침 및 규칙을 제공합니다. 추가 참조에 대한 링크는 개요의 끝에 나열되어 있습니다.

<xref:System.Windows.Automation.ExpandCollapsePattern> 컨트롤 패턴은 시각적으로 확장되어 더 많은 콘텐츠를 표시하거나 축소되어 콘텐츠를 숨기는 컨트롤을 지원하는 데 사용됩니다. 이 컨트롤 패턴을 구현하는 컨트롤의 예제를 보려면 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)을 참조하세요.

<a name="Implementation_Guidelines_and_Conventions"></a>

## <a name="implementation-guidelines-and-conventions"></a>구현 지침 및 규칙

ExpandCollapse 컨트롤 패턴을 구현할 때는 다음 지침 및 규칙에 유의하세요.

- UI에 확장/축소 기능을 제공하는 자식 개체로 빌드된 집계 컨트롤은 <xref:System.Windows.Automation.ExpandCollapsePattern> 컨트롤 패턴을 지원해야 하지만 자식 요소는 그렇지 않습니다. 예를 들어 콤보 상자 컨트롤은 목록 상자, 단추 및 편집 컨트롤 조합으로 빌드되지만 <xref:System.Windows.Automation.ExpandCollapsePattern>을 지원해야 하는 부모 콤보 상자일 뿐입니다.

  > [!NOTE]
  > 단, 개별 MenuItem 개체의 집계인 메뉴 컨트롤은 예외입니다. MenuItem 개체는 <xref:System.Windows.Automation.ExpandCollapsePattern> 컨트롤 패턴을 지원할 수 있지만 부모 메뉴 컨트롤은 그렇지 않습니다. 트리 및 트리 항목 컨트롤에도 유사한 예외가 적용됩니다.

- 컨트롤의 <xref:System.Windows.Automation.ExpandCollapseState> 가 <xref:System.Windows.Automation.ExpandCollapseState.LeafNode>로 설정되어 있으면 모든 <xref:System.Windows.Automation.ExpandCollapsePattern> 기능이 컨트롤에 대해 비활성화되고 이 컨트롤 패턴을 사용하여 가져올 수 있는 유일한 정보는 <xref:System.Windows.Automation.ExpandCollapseState>입니다. 나중에 자식 개체를 추가하면 <xref:System.Windows.Automation.ExpandCollapseState> 가 변경되고 <xref:System.Windows.Automation.ExpandCollapsePattern> 기능이 활성화됩니다.

- <xref:System.Windows.Automation.ExpandCollapseState> 는 직계 자식 개체의 표시 유형을 나타내며, 모든 하위 개체의 표시 유형을 나타내지는 않습니다.

- 확장 및 축소는 컨트롤 관련 기능입니다. 다음은 이 동작의 예입니다.

  - Office 개인 메뉴는 세가지 상태의 MenuItem(<xref:System.Windows.Automation.ExpandCollapseState.Expanded>, <xref:System.Windows.Automation.ExpandCollapseState.Collapsed> 및 <xref:System.Windows.Automation.ExpandCollapseState.PartiallyExpanded>)이 될 수 있으며, 이때 컨트롤은 <xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> 또는 <xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A> 가 호출될 때 적용할 상태를 지정합니다.

  - TreeItem에서 <xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> 를 호출하면 모든 하위 항목 또는 직계 자식만 표시될 수 있습니다.

  - 컨트롤에서 <xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> 또는 <xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A> 를 호출하여 하위 항목의 상태를 유지 관리하는 경우 상태 변경 이벤트가 아니라 표시 유형 변경 이벤트를 전송해야 합니다. 축소될 때 부모 컨트롤이 하위 항목의 상태를 유지 관리하지 않으면 컨트롤이 더 이상 표시되지 않는 모든 하위 항목을 삭제하고 삭제된 이벤트를 발생시킬 수 있습니다. 또는 각 하위 항목에 대해 <xref:System.Windows.Automation.Provider.IExpandCollapseProvider.ExpandCollapseState%2A> 를 변경하고 표시 유형 변경 이벤트를 발생시킬 수 있습니다.

- 탐색을 보장하려면 부모 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 에 관계없이 개체를 적절한 표시 유형 상태로 <xref:System.Windows.Automation.ExpandCollapseState>트리에 배치하는 것이 좋습니다. 요청 시 생성되는 하위 항목의 경우 처음으로 표시된 다음이나 표시되는 동안만 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 나타날 수 있습니다.

<a name="Required_Members_for_the_IValueProvider_Interface"></a>

## <a name="required-members-for-iexpandcollapseprovider"></a>IExpandCollapseProvider에 필요한 멤버

<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>를 구현하려면 다음과 같은 속성 및 메서드가 필요합니다.

|필요한 멤버|멤버 형식|노트|
|----------------------|-----------------|-----------|
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider.ExpandCollapseState%2A>|속성|없음|
|<xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A>|메서드|없음|
|<xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A>|메서드|없음|
|<xref:System.Windows.Automation.AutomationPropertyChangedEventHandler>|이벤트|이 컨트롤에는 연결된 이벤트가 없습니다. 이 제네릭 대리자를 사용합니다.|

<a name="Exceptions"></a>

## <a name="exceptions"></a>예외

공급자는 다음과 같은 예외를 throw해야 합니다.

|예외 형식|조건|
|--------------------|---------------|
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> 또는 이<xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A> 호출 될 때 <xref:System.Windows.Automation.ExpandCollapseState>  =  가<xref:System.Windows.Automation.ExpandCollapseState.LeafNode>호출 됩니다.|

## <a name="see-also"></a>참고자료

- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [TreeWalker를 사용하여 UI 자동화 요소 간 탐색](navigate-among-ui-automation-elements-with-treewalker.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
