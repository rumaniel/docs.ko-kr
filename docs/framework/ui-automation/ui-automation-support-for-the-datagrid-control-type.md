---
title: DataGrid 컨트롤 형식에 대한 UI 자동화 지원
ms.date: 03/30/2017
helpviewer_keywords:
- Data Grid control type
- control types, Data Grid
- UI Automation, Data Grid control type
ms.assetid: a3db4a3f-feb5-4e5f-9b42-aae7fa816e8a
ms.openlocfilehash: 0677e600864954040ac650afaf647f2c4e30e351
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71041824"
---
# <a name="ui-automation-support-for-the-datagrid-control-type"></a>DataGrid 컨트롤 형식에 대한 UI 자동화 지원
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 DataGrid 컨트롤 형식에 대한 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 지원 정보를 제공합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, 컨트롤 형식은 `ControlType` 속성을 사용하기 위해 컨트롤이 충족해야 하는 조건 집합입니다. 이 조건에는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 값, 컨트롤 패턴에 대한 특정 지침이 포함됩니다.  
  
 DataGrid 컨트롤 형식을 통해 사용자는 열에 표시된 메타데이터가 포함된 항목을 쉽게 작업할 수 있습니다. 데이터 표 컨트롤에는 항목의 행과 항목에 대한 정보 열이 있습니다. Microsoft Vista 탐색기에서 목록 뷰 컨트롤은 DataGrid 컨트롤 형식을 지원하는 예입니다.  
  
 다음 섹션에서는 DataGrid 컨트롤 형식에 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조, 속성, 컨트롤 패턴, 이벤트를 정의합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요구 사항은 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]또는 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]의 모든 데이터 표 컨트롤에 적용됩니다.  
  
## <a name="required-ui-automation-tree-structure"></a>필요한 UI 자동화 트리 구조  
 다음 표는 데이터 표 컨트롤과 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰 및 콘텐츠 뷰를 보여주고 각 뷰에 포함될 수 있는 내용에 대해 설명합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 대 한 자세한 내용은 [UI 자동화 트리 개요](ui-automation-tree-overview.md)를 참조 하세요.  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 - 컨트롤 뷰|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리-콘텐츠 뷰|  
|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|  
|DataGrid<br /><br /> <ul><li>Header(0, 1 또는 1개)<br /><br /> <ul><li>HeaderItem(행 또는 열 개수)</li></ul></li><li>DataItem(0개 이상, 계층 구조로 구조화할 수 있음)</li></ul>|DataGrid<br /><br /> -DataItem (0 개 이상, 계층 구조에서 구조화할 수 있음)|  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>필요한 UI 자동화 속성  
 다음 표에서는 값 또는 정의가 데이터 표 컨트롤과 특별히 관련된 속성을 나열하여 보여줍니다. 속성에 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 대 한 자세한 내용은 [클라이언트에 대 한 UI 자동화 속성](ui-automation-properties-for-clients.md)을 참조 하세요.  
  
|속성|값|노트|  
|--------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|메모를 참조하세요.|이 속성의 값은 애플리케이션의 모든 컨트롤에서 고유해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|메모를 참조하세요.|전체 컨트롤이 포함된 가장 바깥쪽 사각형입니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|메모를 참조하세요.|경계 사각형이 없는 경우 지원됩니다. 경계 사각형 내의 일부 지점이 클릭 가능하지 않으며 특수화된 적중 테스트를 수행하는 경우 클릭 가능한 지점을 재정의하고 제공하세요.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|DataGrid|이 값은 모든 UI 프레임워크에 대해 동일합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|이 속성의 값은 항상 True여야 합니다. 이는 데이터 표 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 콘텐츠 보기에 항상 포함되어야 함을 의미합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|이 속성의 값은 항상 True여야 합니다. 이는 데이터 표 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 보기에 항상 포함되어야 함을 의미합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|메모를 참조하세요.|컨트롤이 키보드 포커스를 받을 수 있으면 해당 컨트롤은 이 속성을 지원해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|메모를 참조하세요.|정적 텍스트 레이블이 있는 경우 이 속성은 해당 컨트롤에 대한 참조를 노출해야 합니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"data grid"|DataGrid 컨트롤 형식에 해당하는 지역화된 문자열입니다.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|메모를 참조하세요.|데이터 표 컨트롤은 일반적으로 정적 텍스트 레이블에서 `Name` 속성의 값을 가져옵니다. 정적 텍스트 레이블이 없는 경우 애플리케이션 개발자가 `Name` 속성의 값을 할당해야 합니다. `Name` 속성 값은 편집 컨트롤의 텍스트 내용이 포함되지 않아야 합니다.|  
  
## <a name="required-ui-automation-control-patterns"></a>필요한 UI 자동화 컨트롤 패턴  
 다음 표에서는 모든 데이터 표 컨트롤에서 지원되는 데 필요한 컨트롤 패턴을 나열하여 보여줍니다. 컨트롤 패턴에 대한 자세한 내용은 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)를 참조하세요.  
  
|컨트롤 패턴|Support(지원)|노트|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|예|데이터 표 컨트롤의 항목에는 표에 배치되는 메타데이터가 포함되어 있기 때문에 이 컨트롤은 항상 Grid 컨트롤 패턴을 지원합니다.|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|종속|데이터 표를 스크롤할 수 있는 기능은 내용 및 스크롤 막대가 있는지 여부에 따라 다릅니다.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|종속|데이터 표를 선택할 수 있는 기능은 내용에 따라 다릅니다.|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|예|데이터 표 컨트롤의 하위 트리에는 항상 헤더가 있으므로 Table 컨트롤 패턴이 지원되어야 합니다.|  
  
 데이터 표 컨테이너 내의 데이터 항목은 최소한 다음과 같은 사항을 지원합니다.  
  
- Selection Item 컨트롤 패턴(데이터 표가 선택 가능한 경우)  
  
- Scroll Item 컨트롤 패턴(데이터 표가 스크롤 가능한 경우)  
  
- Grid Item 컨트롤 패턴  
  
- Table Item 컨트롤 패턴  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>필요한 UI 자동화 이벤트  
 다음 표에서는 모든 데이터 표 컨트롤에서 지원되는 데 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트를 나열하여 보여줍니다. 이벤트에 대한 자세한 내용은 [UI Automation Events Overview](ui-automation-events-overview.md)를 참조하세요.  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트|Support(지원)|노트|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 속성 변경 이벤트.|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 속성 변경 이벤트.|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 속성 변경 이벤트.|필수|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent>|종속|없음|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|필수|없음|  
|<xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty> 속성 변경 이벤트.|종속|없음|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> 속성 변경 이벤트.|종속|컨트롤이 Scroll 패턴을 지원하는 경우 이 이벤트를 지원해야 합니다.|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> 속성 변경 이벤트.|종속|컨트롤이 Scroll 패턴을 지원하는 경우 이 이벤트를 지원해야 합니다.|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> 속성 변경 이벤트.|종속|컨트롤이 Scroll 패턴을 지원하는 경우 이 이벤트를 지원해야 합니다.|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> 속성 변경 이벤트.|종속|컨트롤이 Scroll 패턴을 지원하는 경우 이 이벤트를 지원해야 합니다.|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> 속성 변경 이벤트.|종속|컨트롤이 Scroll 패턴을 지원하는 경우 이 이벤트를 지원해야 합니다.|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> 속성 변경 이벤트.|종속|컨트롤이 Scroll 패턴을 지원하는 경우 이 이벤트를 지원해야 합니다.|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|필수|없음|  
  
## <a name="date-grid-control-type-example"></a>Date Grid 컨트롤 형식 예제  
 다음 그림은 DataGrid 컨트롤 형식을 구현하는 목록 뷰 컨트롤을 보여줍니다.  
  
 ![두 데이터 항목을 포함 하는 목록 뷰 컨트롤의 그래픽](./media/uiauto-data-grid-detailed.GIF "uiauto_data_grid_detailed")  
  
 다음은 목록 뷰 컨트롤과 관련된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰 및 콘텐츠 보기입니다. 각 자동화 요소에 대한 컨트롤 패턴은 괄호 안에 표시됩니다.  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 - 컨트롤 뷰|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리-콘텐츠 뷰|  
|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|  
|<ul><li>DataGrid(Table, Grid, Selection)</li><li>헤더<br /><br /> <ul><li>HeaderItem "Name" (Invoke)</li><li>HeaderItem "Date Modified" (Invoke)</li><li>HeaderItem "Size" (Invoke)</li></ul></li><li>그룹 "Contoso" (TableItem, GridItem, SelectionItem, Table *, Grid\*)<br /><br /> <ul><li>DataItem "외상 미수금. doc" (selectionitem, Invoke, tableitem\*, GridItem\*)</li><li>DataItem "Accounts GridItem" (selectionitem, Invoke, tableitem\*,)\*</li></ul></li></ul>|<ul><li>DataGrid(Table, Grid, Selection)</li><li>그룹 "Contoso" (TableItem, GridItem, SelectionItem, Table *, Grid\*)<br /><br /> <ul><li>DataItem "외상 미수금. doc" (selectionitem, Invoke, tableitem\*, GridItem\*)</li><li>DataItem "Accounts GridItem" (selectionitem, Invoke, tableitem\*,)\*</li></ul></li></ul>|  
  
 \*이전 예제에서는 여러 수준의 컨트롤이 포함 된 DataGrid를 보여 줍니다. Group ("Contoso") 컨트롤에는 두 개의 DataItem 컨트롤("Accounts Receivable.doc" 및 "Accounts Payable.doc")이 있습니다. DataGrid/GridItem 쌍은 다른 수준의 쌍과 관계가 없습니다. Group 아래의 DataItem 컨트롤은 ListItem 컨트롤 형식으로도 노출될 수 있으므로, 단순한 데이터 요소가 아닌 선택 가능한 개체로서 보다 명확하게 표시될 수 있습니다. 이 예제에서는 그룹화된 데이터 항목의 하위 요소는 포함되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Automation.ControlType.DataGrid>
- [UI 자동화 컨트롤 형식 개요](ui-automation-control-types-overview.md)
- [UI 자동화 개요](ui-automation-overview.md)
