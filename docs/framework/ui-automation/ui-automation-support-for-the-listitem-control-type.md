---
title: ListItem 컨트롤 형식에 대한 UI 자동화 지원
ms.date: 03/30/2017
helpviewer_keywords:
- control types, List
- List Item control type
- UI Automation, List Item control type
ms.assetid: 34f533bf-fc14-4e78-8fee-fb7107345fab
ms.openlocfilehash: 18dcec2be6d9496c14dcc12c1d21b60967732db8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71041466"
---
# <a name="ui-automation-support-for-the-listitem-control-type"></a>ListItem 컨트롤 형식에 대한 UI 자동화 지원
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 컨트롤 형식에 대한 <xref:System.Windows.Automation.ControlType.ListItem> 지원 정보를 제공합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, 컨트롤 형식은 <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> 속성을 사용하기 위해 컨트롤이 충족해야 하는 조건 집합입니다. 이 조건에는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 값, 컨트롤 패턴에 대한 특정 지침이 포함됩니다.  
  
 목록 항목 컨트롤은 List 컨트롤 형식을 구현하는 컨트롤의 예입니다.  
  
 다음 섹션에서는 ListItem 컨트롤 형식에 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, 속성, 컨트롤 패턴, 이벤트를 정의합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요구 사항은 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]또는 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]의 모든 목록 컨트롤에 적용됩니다.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## <a name="required-ui-automation-tree-structure"></a>필요한 UI 자동화 트리 구조  
 다음 표는 목록 항목 컨트롤과 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰 및 콘텐츠 뷰를 보여주고 각 뷰에 포함될 수 있는 내용에 대해 설명합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 대 한 자세한 내용은 [UI 자동화 트리 개요](ui-automation-tree-overview.md)를 참조 하세요.  
  
|컨트롤 뷰|콘텐츠 뷰|  
|------------------|------------------|  
|ListItem<br /><br /> -Image (0 개 이상)<br />-Text (0 개 이상)<br />-Edit (0 개 이상)|ListItem|  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 콘텐츠 보기 내에서 목록 항목 컨트롤의 자식은 항상 "0" 이어야 합니다. 컨트롤의 구조가 목록 항목 아래에 다른 항목이 포함 되는 경우에는 [TreeItem 컨트롤 형식 컨트롤 형식에 대 한 UI 자동화 지원](ui-automation-support-for-the-treeitem-control-type.md) 에 대 한 요구 사항을 따라야 합니다.  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>필요한 UI 자동화 속성  
 다음 표에서는 값 또는 정의가 목록 항목 컨트롤과 특별히 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성을 나열하여 보여 줍니다. 속성에 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 대 한 자세한 내용은 [클라이언트에 대 한 UI 자동화 속성](ui-automation-properties-for-clients.md)을 참조 하세요.  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성|값|노트|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|메모를 참조하세요.|이 속성의 값은 애플리케이션의 모든 컨트롤에서 고유해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|메모를 참조하세요.|이 속성의 값은 목록 항목의 이미지 및 텍스트 내용의 영역에 포함되어야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|종속|목록 컨트롤에 클릭 가능한 지점(클릭하여 목록에서 포커스를 받을 수 있도록 하는 지점)이 있는 경우, 해당 지점은 이 속성을 통해 노출되어야 합니다. 목록 컨트롤이 하위 목록 항목에 의해 완전히 가려져 있는 경우 <xref:System.Windows.Automation.NoClickablePointException> 를 발생시켜 클라이언트가 목록 컨트롤 내에 항목이 포함되도록 요청해야 클릭 가능한 지점을 사용할 수 있음을 나타냅니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|메모를 참조하세요.|목록 항목 컨트롤의 이름 속성 값은 항목의 텍스트 내용에서 가져옵니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|메모를 참조하세요.|정적 텍스트 레이블이 있는 경우 이 속성은 해당 컨트롤에 대한 참조를 노출해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ListItem|이 값은 모든 UI 프레임워크에 대해 동일합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"list item"|ListItem 컨트롤 형식에 해당하는 지역화된 문자열입니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|목록 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 콘텐츠 뷰에 항상 포함됩니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|목록 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰에 항상 포함됩니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|컨테이너가 키보드 입력을 허용할 수 있으면 이 속성 값은 true여야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|""|목록 컨트롤에 대한 도움말 텍스트는 옵션 목록에서 선택할지 묻는 메시지가 사용자에게 표시되는 이유를 설명하며, 일반적으로 도구 설명을 통해 제공되는 정보 유형과 동일합니다. 예: "모니터의 디스플레이 해상도를 설정할 항목을 선택하세요."|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemTypeProperty>|종속|이 속성은 내부 개체를 나타내는 목록 항목 컨트롤에 대해 노출되어야 합니다. 이러한 목록 항목 컨트롤에는 일반적으로 사용자가 내부 개체와 연결하는 컨트롤과 연관된 아이콘이 있습니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|종속|이 속성은 Scroll 컨트롤 패턴을 구현하는 부모 컨테이너 내에서 목록 항목이 현재 스크롤해서 표시되는지를 나타내는 값을 반환해야 합니다.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## <a name="required-ui-automation-control-patterns"></a>필요한 UI 자동화 컨트롤 패턴  
 다음 표에서는 목록 항목 컨트롤에서 지원되는 데 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 컨트롤 패턴을 나열하여 보여 줍니다. 컨트롤 패턴에 대한 자세한 내용은 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)를 참조하세요.  
  
|컨트롤 패턴|Support(지원)|노트|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|예|목록 항목 컨트롤이 이 컨트롤 패턴을 구현해야 합니다. 이렇게 하면 목록 항목 컨트롤을 선택하여 전달할 수 있습니다.|  
|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|종속|스크롤 가능한 컨테이너 내에 목록 항목이 포함된 경우 이 컨트롤 패턴을 구현해야 합니다.|  
|<xref:System.Windows.Automation.Provider.IToggleProvider>|종속|목록 항목이 선택 가능하고 해당 작업에서 선택 상태 변경을 수행하지 않는 경우 이 컨트롤 패턴을 구현해야 합니다.|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|종속|정보를 표시하거나 숨기도록 항목을 조작할 수 있는 경우 이 컨트롤 패턴을 구현해야 합니다.|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|종속|항목을 편집할 수 있는 경우 이 컨트롤 패턴을 구현해야 합니다. 목록 항목 컨트롤이 변경되면 <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>및 <xref:System.Windows.Automation.Provider.IValueProvider.Value%2A>의 값이 변경됩니다.|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider>|종속|목록 컨테이너 내에서 항목 간 공간 탐색이 지원되고 컨테이너가 행 및 열로 정렬된 경우 Grid Item 컨트롤 패턴을 구현해야 합니다.|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|종속|선택된 항목과 별개로, 항목에서 수행할 수 있는 명령이 있는 경우 이 패턴을 구현해야 합니다. 이는 일반적으로 목록 항목 컨트롤을 두 번 클릭하는 것과 연관된 동작입니다. 이 예로는 [!INCLUDE[TLA#tla_winexpl](../../../includes/tlasharptla-winexpl-md.md)]에서 문서를 시작하거나 [!INCLUDE[TLA#tla_wmp](../../../includes/tlasharptla-wmp-md.md)]에서 음악 파일을 재생하는 동작이 있습니다.|  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>필요한 UI 자동화 이벤트  
 다음 표에서는 모든 목록 항목 컨트롤에서 지원되는 데 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트를 나열하여 보여 줍니다. 이벤트에 대한 자세한 내용은 [UI Automation Events Overview](ui-automation-events-overview.md)를 참조하세요.  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트|Support(지원)|노트|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|종속|없음|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|필수|없음|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|필수|없음|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 속성 변경 이벤트.|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 속성 변경 이벤트.|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 속성 변경 이벤트.|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemStatusProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|필수|없음|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Automation.ControlType.ListItem>
- [UI 자동화 컨트롤 형식 개요](ui-automation-control-types-overview.md)
- [UI 자동화 개요](ui-automation-overview.md)
