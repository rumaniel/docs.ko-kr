---
title: Edit 컨트롤 형식에 대한 UI 자동화 지원
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Edit
- Edit control type
- UI Automation, Edit control type
ms.assetid: 6db9d231-c0a0-4e17-910e-ac80357f774f
ms.openlocfilehash: 5cce634e2ba80b496b808a4ec66c4c06118b5989
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71041702"
---
# <a name="ui-automation-support-for-the-edit-control-type"></a>Edit 컨트롤 형식에 대한 UI 자동화 지원

> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).

이 항목에서는 Edit 컨트롤 형식에 대한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 지원 정보를 제공합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, 컨트롤 형식은 <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> 속성을 사용하기 위해 컨트롤이 충족해야 하는 조건 집합입니다. 이 조건에는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 값, 컨트롤 패턴에 대한 특정 지침이 포함됩니다.

편집 컨트롤은 다양한 서식 지원 없이 사용자가 간단한 텍스트 줄을 보고 편집할 수 있도록 합니다.

다음 섹션에서는 Edit 컨트롤 형식에 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, 속성, 컨트롤 패턴, 이벤트를 정의합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요구 사항은 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]또는 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]의 모든 편집 컨트롤에 적용됩니다.

<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>필요한 UI 자동화 트리 구조

다음 표는 편집 컨트롤과 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰 및 콘텐츠 뷰를 보여주고 각 뷰에 포함될 수 있는 내용에 대해 설명합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 대 한 자세한 내용은 [UI 자동화 트리 개요](ui-automation-tree-overview.md)를 참조 하세요.

|컨트롤 뷰|콘텐츠 뷰|
|------------------|------------------|
|편집|편집|

Edit 컨트롤 형식을 구현하는 컨트롤은 한 줄 컨트롤이기 때문에 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰에 항상 스크롤 막대가 없습니다. 일부 레이아웃 시나리오에서는 텍스트 한 줄이 줄 바꿈될 수도 있습니다. Edit 컨트롤 형식은 편집 가능하거나 선택 가능한 텍스트의 양이 적은 경우에 가장 적합합니다.

<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>필요한 UI 자동화 속성

다음 표에서는 값 또는 정의가 편집 컨트롤과 특별히 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성을 나열하여 보여줍니다. 속성에 대 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 한 자세한 내용은 [클라이언트에 대 한 UI 자동화 속성](ui-automation-properties-for-clients.md)을 참조 하세요.

|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성|값|노트|
|------------------------------------------------------------------------------------|-----------|-----------|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|메모를 참조하세요.|이 속성의 값은 애플리케이션의 모든 컨트롤에서 고유해야 합니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|메모를 참조하세요.|전체 컨트롤이 포함된 가장 바깥쪽 사각형입니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|메모를 참조하세요.|편집 컨트롤에는 사용자가 마우스로 클릭할 때 컨트롤의 편집 부분에 입력 포커스를 제공하는 클릭 가능한 지점이 있어야 합니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|메모를 참조하세요.|컨트롤이 키보드 포커스를 받을 수 있으면 해당 컨트롤은 이 속성을 지원해야 합니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|메모를 참조하세요.|편집 컨트롤의 이름은 일반적으로 정적 텍스트 레이블에서 생성됩니다. 정적 텍스트 레이블이 없는 경우 애플리케이션 개발자가 `Name` 의 속성 값을 할당해야 합니다. `Name` 속성에는 편집 컨트롤의 텍스트 내용이 포함되지 않아야 합니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|메모를 참조하세요.|컨트롤과 연결된 정적 텍스트 레이블이 있는 경우, 이 속성은 해당 컨트롤에 대한 참조를 노출해야 합니다. 텍스트 컨트롤이 다른 컨트롤의 하위 구성 요소일 경우 이 컨트롤에 `LabeledBy` 속성 집합이 없습니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|편집|이 값은 모든 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 프레임워크에 대해 동일합니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"edit"|Edit 컨트롤 형식에 해당하는 지역화된 문자열입니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|편집 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 콘텐츠 뷰에 항상 포함됩니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|편집 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰에 항상 포함됩니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsPasswordProperty>|메모를 참조하세요.|암호가 포함된 편집 컨트롤에서 True로 설정되어야 합니다. 편집 컨트롤에 암호 콘텐츠가 포함되어 있는 경우, 화면 읽기 프로그램에서 이 속성을 사용하여 사용자가 키를 입력할 때 입력 내용을 읽을지 결정할 수 있습니다.|

<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns-and-properties"></a>필요한 UI 자동화 컨트롤 패턴 및 속성

다음 표에서는 모든 편집 컨트롤에서 지원되는 데 필요한 컨트롤 패턴을 나열하여 보여줍니다. 컨트롤 패턴에 대한 자세한 내용은 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)를 참조하세요.

|컨트롤 패턴/컨트롤 패턴 속성|지원/값|노트|
|-----------------------------------------------|--------------------|-----------|
|<xref:System.Windows.Automation.Provider.ITextProvider>|종속|클라이언트에서 자세한 텍스트 정보를 항상 사용할 수 있어야 하기 때문에 편집 컨트롤은 Text 컨트롤 패턴을 지원해야 합니다.|
|<xref:System.Windows.Automation.Provider.IValueProvider>|종속|문자열을 사용할 수 있는 모든 편집 컨트롤은 Value 패턴을 노출해야 합니다.|
|<xref:System.Windows.Automation.Provider.IValueProvider.IsReadOnly%2A>|메모를 참조하세요.|이 속성은 컨트롤에 프로그래밍 방식으로 설정된 값을 사용할 수 있는지 또는 사용자가 컨트롤을 편집할 수 있는지를 나타내도록 설정되어야 합니다.|
|<xref:System.Windows.Automation.Provider.IValueProvider.Value%2A>|메모를 참조하세요.|이 속성은 편집 컨트롤의 텍스트 내용을 반환합니다. `IsPasswordProperty` 가 `true`로 설정되어 있으면, 이 속성은 요청될 때 `InvalidOperationException` 을 발생해야 합니다.|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|종속|숫자 범위를 사용할 수 있는 모든 편집 컨트롤은 Range Value 컨트롤 패턴을 노출해야 합니다.|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.Minimum%2A>|메모를 참조하세요.|이 속성은 편집 컨트롤의 콘텐츠를 설정할 수 있는 가장 작은 값이어야 합니다.|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.Maximum%2A>|메모를 참조하세요.|이 속성은 편집 컨트롤의 콘텐츠를 설정할 수 있는 가장 큰 값이어야 합니다.|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.SmallChange%2A>|메모를 참조하세요.|이 속성은 값을 설정할 수 있는 소수 자릿수를 나타내야 합니다. 편집에 정수만 사용할 수 있는 경우 `SmallChangeProperty` 는 1이어야 합니다. 편집에 1.0에서 2.0까지의 범위를 사용할 수 있는 경우 `SmallChangeProperty` 는 0.1이어야 합니다. 편집 컨트롤에 1.00에서 2.00까지의 범위를 사용할 수 있는 경우 `SmallChangeProperty` 는 0.001이어야 합니다.|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.LargeChange%2A>|`Null`|이 속성은 편집 컨트롤에 노출될 필요가 없습니다.|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.Value%2A>|메모를 참조하세요.|이 속성은 편집 컨트롤의 숫자 콘텐츠를 나타냅니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 및 `Minimum` 속성에 지정된 범위 내에서 `Maximum` 클라이언트가 보다 정확한 값을 설정하면, Value 속성은 허용되는 가장 근접한 값으로 자동으로 반올림됩니다.|

<a name="Required_UI_Automation_Events"></a>

## <a name="required-ui-automation-events"></a>필요한 UI 자동화 이벤트

다음 표에서는 모든 편집 컨트롤에서 지원되는 데 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트를 나열하여 보여줍니다. 이벤트에 대한 자세한 내용은 [UI Automation Events Overview](ui-automation-events-overview.md)를 참조하세요.

|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트|Support(지원)|노트|
|---------------------------------------------------------------------------------|-------------|-----------|
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|필수|없음|
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent>|필수|없음|
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent>|필수|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 속성 변경 이벤트.|필수|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 속성 변경 이벤트.|필수|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 속성 변경 이벤트.|필수|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> 속성 변경 이벤트.|필수|없음|
|<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> 속성 변경 이벤트.|종속|없음|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> 속성 변경 이벤트.|Never|없음|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> 속성 변경 이벤트.|Never|없음|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> 속성 변경 이벤트.|Never|없음|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> 속성 변경 이벤트.|Never|없음|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> 속성 변경 이벤트.|Never|없음|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> 속성 변경 이벤트.|Never|없음|
|<xref:System.Windows.Automation.RangeValuePatternIdentifiers.ValueProperty> 속성 변경 이벤트.|종속|컨트롤이 Range Value 컨트롤 패턴을 지원하는 경우 이 이벤트를 지원해야 합니다.|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|필수|없음|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|필수|없음|

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Automation.ControlType.Edit>
- [UI 자동화 컨트롤 형식 개요](ui-automation-control-types-overview.md)
- [UI 자동화 개요](ui-automation-overview.md)
