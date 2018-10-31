---
title: List 컨트롤 형식에 대한 UI 자동화 지원
ms.date: 03/30/2017
helpviewer_keywords:
- control types, List
- List control type
- UI Automation, List control type
ms.assetid: 0e959fcb-50f2-413b-948d-7167d279bc11
author: Xansky
ms.author: mhopkins
ms.openlocfilehash: 1ae62cca72831b0319243acd9c5bf7a2b86138c3
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50205271"
---
# <a name="ui-automation-support-for-the-list-control-type"></a>List 컨트롤 형식에 대한 UI 자동화 지원
> [!NOTE]
>  이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에 대한 최신 정보는 [Windows 자동화 API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746)를 참조하세요.  
  
 이 항목에서는 List 컨트롤 형식에 대한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 지원 정보를 제공합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, 컨트롤 형식은 <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> 속성을 사용하기 위해 컨트롤이 충족해야 하는 조건 집합입니다. 이 조건에는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 값, 컨트롤 패턴에 대한 특정 지침이 포함됩니다.  
  
 List 컨트롤 형식은 항목의 플랫 그룹 구성 방법을 제공하며 사용자가 하나 이상의 이러한 항목을 선택할 수 있도록 합니다. List 컨트롤 형식에서는 포함될 수 있는 자식 요소 형식에 대한 제한이 엄격하지 않습니다. 따라서 UI 자동화 공급자가 선택 항목 컨테이너에 대해 잘 알려진 요소를 지원할 수 있습니다.  
  
 다음 섹션의 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요구 사항은 List 컨트롤 형식을 구현하는 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]또는 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]의 모든 컨트롤에 적용됩니다. 목록 컨테이너 컨트롤은 List 컨트롤 형식을 구현하는 컨트롤의 예입니다.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## <a name="required-ui-automation-tree-structure"></a>필요한 UI 자동화 트리 구조  
 다음 표는 목록 컨트롤과 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 두 뷰를 보여주고 각 뷰에 포함될 수 있는 내용에 대해 설명합니다. 컨트롤 뷰에는 컨트롤인 요소만 포함되며, 콘텐츠 뷰에서는 트리와 중복되는 정보가 제거됩니다. 예를 들어, 콤보 상자에 레이블을 지정하는 데 사용되는 텍스트 컨트롤은 `ComboBox NameProperty`로 노출됩니다. 하지만 텍스트 컨트롤이 컨트롤 뷰에서 이 방법으로 이미 노출되므로 두 번 노출시킬 필요는 없습니다. 따라서 콘텐츠 보기에서 제거됩니다. 에 대 한 자세한 합니다 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리를 참조 하십시오 [UI 자동화 트리 개요](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)합니다.  
  
|컨트롤 뷰|콘텐츠 뷰|  
|------------------|------------------|  
|컨트롤에 해당하는 요소를 포함합니다.|최종 사용자에게 의미 있는 가장 작은 정보 집합에서 보조 기술이 작동되도록 트리에서 중복되는 정보를 제거합니다.|  
|목록<br /><br /> -DataItem (0 개 이상)<br />-ListItem (0 개 이상)<br />-그룹 (0 개 이상)<br />-ScrollBar (0, 1 또는 2)|목록<br /><br /> -DataItem (0 개 이상)<br />-ListItem (0 개 이상)<br />-그룹 (0 개 이상)|  
  
 List 컨트롤 형식(예: 목록 컨트롤)을 구현하는 컨트롤의 컨트롤 뷰는 다음과 같이 구성되어 있습니다.  
  
- (항목 목록 Item 또는 Data Item 컨트롤 형식에 기반 할 수 있습니다) 목록 컨트롤 내에서 0 개 이상의 항목입니다.
  
- 목록 컨트롤 내에서 0 개 이상의 그룹 컨트롤입니다.
  
- 0, 1 개 또는 두 스크롤 막대 컨트롤입니다.
  
List 컨트롤 형식(예: 목록 컨트롤)을 구현하는 컨트롤의 콘텐츠 뷰는 다음과 같이 구성되어 있습니다.  
  
- (항목 목록 Item 또는 Data Item 컨트롤 형식에 기반 할 수 있습니다) 목록 컨트롤 내에서 0 개 이상의 항목입니다.
  
- 목록 컨트롤 내에서 0 개 이상의 그룹입니다.

함께 그룹화된 항목 외에 계층 관계가 있는 항목은 목록 컨트롤 항목에 포함되지 않아야 합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 항목의 자식이 있는 경우 목록 컨테이너는 Tree 컨트롤 형식을 기반으로 해야 합니다.  
  
 목록 컨트롤 내에서 선택 가능한 항목은 목록 컨트롤의 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 있는 하위 항목에서 사용할 수 있습니다. 목록 컨트롤 내의 모든 항목은 같은 선택 그룹에 속해야 합니다. 목록에서 선택 가능한 항목은 DataItem이 아닌 ListItem 컨트롤 형식으로 노출되어야 합니다.  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>필요한 UI 자동화 속성  
 다음 표에서는 값 또는 정의가 목록 컨트롤과 특별히 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성을 나열하여 보여 줍니다. 에 대 한 자세한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성을 참조 하세요 [클라이언트용 UI 자동화 속성](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)합니다.  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성|값|노트|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|메모를 참조하세요.|이 속성의 값은 응용 프로그램의 모든 컨트롤에서 고유해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|메모를 참조하세요.|전체 컨트롤이 포함된 가장 바깥쪽 사각형입니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|메모를 참조하세요.|목록 컨트롤에 클릭 가능한 지점(클릭하여 목록에서 포커스를 받을 수 있도록 하는 지점)이 있는 경우, 해당 지점은 이 속성을 통해 노출되어야 합니다.<br /><br /> 경우의 값을 `IsOffScreen` 속성이 true 이면 해당 <xref:System.Windows.Automation.NoClickablePointException> 발생 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|메모를 참조하세요.|컨트롤이 키보드 포커스를 받을 수 있으면 해당 컨트롤은 이 속성을 지원해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|메모를 참조하세요.|목록 컨트롤의 Name 속성 값은 사용자에게 선택하라고 요청하는 옵션의 범주를 전달해야 합니다. 이 속성은 일반적으로 정적 텍스트 레이블에서 이름을 가져옵니다. 정적 텍스트 레이블이 없는 경우 응용 프로그램 개발자 Name 속성의 값을 노출해야 합니다.<br /><br /> 컨트롤이 다른 컨트롤의 하위 트리 내에 사용되는 경우에만 이 속성이 목록 컨트롤에 필요하지 않습니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|메모를 참조하세요.|정적 텍스트 레이블이 있는 경우 이 속성은 해당 컨트롤에 대한 참조를 노출해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|목록|이 값은 모든 UI 프레임워크에 대해 동일합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"list"|List 컨트롤 형식에 해당하는 지역화된 문자열입니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|목록 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 콘텐츠 뷰에 항상 포함됩니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|목록 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰에 항상 포함됩니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|컨테이너가 키보드 입력을 허용할 수 있으면 이 속성 값은 true여야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|메모를 참조하세요.|목록 컨트롤의 도움말 텍스트는 사용자에게 옵션 목록에서 선택하라는 요청이 표시되는 이유를 설명합니다. 예: "이 목록에서 항목을 선택하면 모니터의 디스플레이 해상도가 설정됩니다."|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## <a name="required-ui-automation-control-patterns-and-properties"></a>필요한 UI 자동화 컨트롤 패턴 및 속성  
 다음 표에서는 목록 컨트롤에서 지원되는 데 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 컨트롤 패턴을 나열하여 보여 줍니다. 컨트롤 패턴에 대한 자세한 내용은 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)를 참조하세요.  
  
|컨트롤 패턴/패턴 속성|지원/값|노트|  
|---------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|필수|컨트롤에 포함된 항목 간에 선택 상태가 유지되면 List 컨트롤 형식을 지원하는 모든 컨트롤은 `ISelectionProvider` 를 구현해야 합니다. 항목을 컨테이너 내에서 선택할 수 없는 경우 Group 컨트롤 형식을 사용해야 합니다.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|종속|목록 컨트롤에서 항상 항목을 선택할 필요는 없습니다.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|종속|목록 컨트롤은 단일 또는 다중 선택 컨테이너입니다.|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|종속|컨테이너의 항목을 스크롤할 수 있는 경우에 이 컨트롤 패턴을 구현합니다.|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|종속|항목별로 항목에서 눈금 탐색을 사용할 수 있어야 하는 경우 이 패턴을 구현합니다.|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider>|종속|컨트롤이 컨테이너에 있는 항목의 여러 뷰를 지원할 수 있는 경우 이 컨트롤 패턴을 구현합니다.|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|Never|`ITableProvider` 가 List 컨트롤 형식에 지원되지 않습니다. 컨트롤에서 이 컨트롤 패턴을 지원해야 하는 경우 컨트롤은 Data Grid 컨트롤 형식을 기반으로 해야 합니다.|  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>필요한 UI 자동화 이벤트  
 다음 표에서는 모든 목록 컨트롤에서 지원되는 데 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트를 나열하여 보여 줍니다. 이벤트에 대한 자세한 내용은 [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md)를 참조하세요.  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트|지원/값|노트|  
|---------------------------------------------------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|종속|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent>|종속|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 속성 변경 이벤트.|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 속성 변경 이벤트.|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 속성 변경 이벤트.|필수|없음|  
|<xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|필수|없음|  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Windows.Automation.ControlType.List>  
 [UI 자동화 컨트롤 형식 개요](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)  
 [UI 자동화 개요](../../../docs/framework/ui-automation/ui-automation-overview.md)
