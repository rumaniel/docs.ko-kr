---
title: MenuItem 컨트롤 형식에 대한 UI 자동화 지원
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Menu Item
- Menu Item control type
- UI Automation, Menu Item control type
ms.assetid: 54bce311-3d23-40b9-ba90-1bdbdaf8fbba
ms.openlocfilehash: a1dba653a308bc4fa865e8ee362893cbd15d68da
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71041285"
---
# <a name="ui-automation-support-for-the-menuitem-control-type"></a>MenuItem 컨트롤 형식에 대한 UI 자동화 지원

> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).

이 항목에서는 MenuItem 컨트롤 형식에 대한 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 지원 정보를 제공합니다. 컨트롤의 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 트리 구조에 대해 설명하고 MenuItem 컨트롤 형식에 필요한 속성 및 컨트롤 패턴을 제공합니다.

메뉴 컨트롤을 사용하면 명령 및 이벤트 처리기와 연관된 요소를 계층적으로 구성할 수 있습니다. 일반적인 [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] 애플리케이션에서는, 메뉴 모음에 몇 가지 메뉴 항목(예: **파일**, **편집**, **창**)이 있고 각 메뉴 항목에 메뉴가 표시됩니다. 메뉴 하나에 메뉴 항목 컬렉션(예: **새로 만들기**, **열기**, **닫기**)이 들어 있으며, 클릭하면 확장되어 추가 메뉴 항목이 표시되거나 특정 작업을 수행할 수 있습니다. 메뉴 항목은 메뉴, 메뉴 모음 또는 도구 모음에서 호스트될 수 있습니다.

다음 섹션에서는 MenuItem 컨트롤 형식에 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, 속성, 컨트롤 패턴, 이벤트를 정의합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요구 사항은 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]또는 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]의 모든 목록 컨트롤에 적용됩니다.

<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>필요한 UI 자동화 트리 구조

다음 표는 메뉴 항목 컨트롤과 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰 및 콘텐츠 뷰를 보여주고 각 뷰에 포함될 수 있는 내용에 대해 설명합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 대 한 자세한 내용은 [UI 자동화 트리 개요](ui-automation-tree-overview.md)를 참조 하세요.

|컨트롤 뷰|콘텐츠 뷰|
|------------------|------------------|
|MenuItem "도움말"<br /><br /> <ul><li>Menu(도움말 메뉴 항목의 하위 메뉴)<br /><br /> <ul><li>MenuItem "도움말 항목"</li><li>MenuItem "메모장 정보"</li></ul></li></ul>|MenuItem "도움말"<br /><br /> -MenuItem "도움말 항목"<br />-MenuItem "메모장 정보"|

메뉴 항목 컨트롤의 컨트롤 보기에는 위에 표시된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조가 있습니다. **도움말** 메뉴 항목이 포함 되어 일반 메뉴의 하위 메뉴 계층 구조를 보다 잘 보여 줍니다.

콘텐츠 뷰의 경우, 최종 사용자에게 의미 있는 정보를 전달하지 않기 때문에 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 메뉴가 없습니다.

<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>필요한 UI 자동화 속성

다음 표에서는 값 또는 정의가 메뉴 항목 컨트롤과 특별히 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성을 나열하여 보여줍니다. 속성에 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 대 한 자세한 내용은 [클라이언트에 대 한 UI 자동화 속성](ui-automation-properties-for-clients.md)을 참조 하세요.

|속성|값|설명|
|--------------|-----------|-----------------|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|메모를 참조하세요.|이 속성의 값은 애플리케이션의 모든 컨트롤에서 고유해야 합니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|메모를 참조하세요.|전체 컨트롤이 포함된 가장 바깥쪽 사각형입니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|메모를 참조하세요.|경계 사각형이 없는 경우 지원됩니다. 경계 사각형 내의 일부 지점이 클릭 가능하지 않으며 특수화된 적중 테스트를 수행하는 경우 클릭 가능한 지점을 재정의하고 제공하세요.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|메모를 참조하세요.|컨트롤이 키보드 포커스를 받을 수 있으면 해당 컨트롤은 이 속성을 지원해야 합니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|메모를 참조하세요.|메뉴 항목 컨트롤은 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 콘텐츠 뷰에 포함되어 있으며 이름으로 자체 레이블 지정됩니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|레이블이 없습니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|MenuItem|이 값은 모든 UI 프레임워크에 대해 동일합니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"menu item"|MenuItem 컨트롤 형식에 해당하는 지역화된 문자열입니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|메뉴 항목 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 콘텐츠 뷰에 포함되지 않습니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|메뉴 항목 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰에 항상 포함되어야 합니다.|

<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns"></a>필요한 UI 자동화 컨트롤 패턴

다음 표에서는 메뉴 항목 컨트롤에서 지원되는 데 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 컨트롤 패턴을 나열하여 보여줍니다. 컨트롤 패턴에 대한 자세한 내용은 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)를 참조하세요.

|컨트롤 패턴 속성|지원|노트|
|------------------------------|-------------|-----------|
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|종속|컨트롤을 확장하거나 축소할 수 있는 경우 <xref:System.Windows.Automation.Provider.IExpandCollapseProvider>를 구현합니다.|
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|종속|컨트롤이 단일 작업 또는 명령을 실행하는 경우 <xref:System.Windows.Automation.Provider.IInvokeProvider>를 구현합니다.|
|<xref:System.Windows.Automation.Provider.IToggleProvider>|종속|컨트롤이 설정하거나 해제할 수 있는 옵션을 나타내는 경우 <xref:System.Windows.Automation.Provider.IToggleProvider>를 구현합니다.|
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|종속|컨트롤을 사용하여 메뉴 항목 간의 옵션 목록에서 선택하는 경우 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>를 구현합니다.|

<a name="UI_Automation_Events_for_Menu_Item"></a>

## <a name="ui-automation-events-for-menu-item"></a>메뉴 항목용 UI 자동화 이벤트

다음 표에서는 메뉴 항목 컨트롤과 연결된 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 이벤트를 보여줍니다.

|이벤트(event)|Support(지원)|설명|
|-----------|-------------|-----------------|
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|종속|컨트롤에서 Invoke 컨트롤 패턴을 지원하는 경우 발생되어야 합니다.|
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty> 속성 변경 이벤트.|종속|컨트롤에서 Toggle 컨트롤 패턴을 지원하는 경우 발생되어야 합니다.|
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> 속성 변경 이벤트.|종속|컨트롤에서 Expand Collapse 컨트롤 패턴을 지원하는 경우 발생되어야 합니다.|
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|종속|없음|

<a name="Required_UI_Automation_Events"></a>

## <a name="required-ui-automation-events"></a>필요한 UI 자동화 이벤트

다음 표에서는 모든 메뉴 항목 컨트롤에서 지원되는 데 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트를 나열하여 보여줍니다. 이벤트에 대한 자세한 내용은 [UI Automation Events Overview](ui-automation-events-overview.md)를 참조하세요.

|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트|지원/값|노트|
|---------------------------------------------------------------------------------|--------------------|-----------|
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|종속|없음|
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|종속|없음|
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|종속|없음|
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|종속|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 속성 변경 이벤트.|필수|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 속성 변경 이벤트.|필수|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 속성 변경 이벤트.|필수|없음|
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> 속성 변경 이벤트.|종속|없음|
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty> 속성 변경 이벤트.|종속|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|필수|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|필수|없음|

<a name="Legacy_Issues"></a>

## <a name="legacy-issues"></a>레거시 문제

Toggle 패턴은 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 메뉴 항목이 선택되고 Toggle 패턴을 지원하는 데 필요하다고 프로그래밍 방식으로 판단할 수 있는 경우에만 지원됩니다. [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 메뉴 항목은 선택될 수 있는지 여부를 노출하지 않기 때문에 메뉴 항목이 선택되지 않으면 Invoke 패턴이 지원됩니다. Toggle 패턴만 지원하는 메뉴 항목에 대해서도 Invoke 패턴이 항상 지원되도록 하는 예외가 적용됩니다. Invoke 패턴을 지원했던(메뉴 항목이 선택 취소되었을 때) 요소가 이 패턴이 선택된 후에는 더 이상 지원하지 않게 되므로 클라이언트에서 혼동되지 않습니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Automation.ControlType.MenuItem>
- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 컨트롤 형식 개요](ui-automation-control-types-overview.md)
- [UI 자동화 개요](ui-automation-overview.md)
