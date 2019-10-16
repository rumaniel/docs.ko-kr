---
title: UI 자동화 컨트롤 패턴 개요
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns
- UI Automation, control patterns
ms.assetid: cc229b33-234b-469b-ad60-f0254f32d45d
ms.openlocfilehash: c5dce6895ed9962cf20808417c50569db48de6d9
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042350"
---
# <a name="ui-automation-control-patterns-overview"></a>UI 자동화 컨트롤 패턴 개요
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 개요에서는 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 컨트롤 패턴을 소개합니다. 컨트롤 패턴은 컨트롤 형식 및 컨트롤의 모양에 관계없이 컨트롤의 기능을 분류하고 노출하는 방법을 제공합니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 은 컨트롤 패턴을 사용하여 공통된 컨트롤 동작을 나타냅니다. 예를 들어, 호출할 수 있는 컨트롤(예: 단추)에 대해 Invoke 컨트롤 패턴을 사용하고 스크롤 막대가 있는 컨트롤(예: 목록 상자, 목록 뷰 또는 콤보 상자)에 대해 Scroll 컨트롤 패턴을 사용합니다. 각 컨트롤 패턴은 별도 기능을 나타내므로 컨트롤 패턴을 조합하여 특정 컨트롤에서 지원하는 기능의 전체 집합을 설명할 수 있습니다.  
  
> [!NOTE]
> 부모 컨트롤이 노출한 기능에 대한 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 를 제공하는 하위 컨트롤을 사용하여 빌드된 집계 컨트롤은 각 하위 컨트롤과 정상적으로 연결된 모든 컨트롤 패턴을 구현해야 합니다. 따라서 이러한 동일한 컨트롤 패턴을 하위 컨트롤이 구현할 필요가 없습니다.  
  
<a name="uiautomation_control_pattern_includes"></a>   
## <a name="ui-automation-control-pattern-components"></a>UI 자동화 컨트롤 패턴 구성 요소  
 컨트롤 패턴은 컨트롤에 있는 개별 기능 항목을 정의하는 데 필요한 메서드, 속성, 이벤트 및 관계를 지원합니다.  
  
- UI 자동화 요소와 부모, 자식, 형제 간의 관계는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 내에서 해당 요소의 구조를 설명합니다.  
  
- 메서드는 UI 자동화 클라이언트가 컨트롤을 조작할 수 있도록 합니다.  
  
- 속성 및 이벤트는 컨트롤 상태에 대한 정보뿐만 아니라 컨트롤 패턴의 기능에 대한 정보를 제공합니다.  
  
 인터페이스 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 는 COM (구성 요소 개체 모델) 개체와 관련이 있으므로 컨트롤 패턴은와 관련 됩니다. COM에서 개체를 쿼리하여 개체에서 지 원하는 인터페이스를 확인 한 다음 이러한 인터페이스를 사용 하 여 기능에 액세스할 수 있습니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, UI 자동화 클라이언트는 컨트롤이 지원하는 컨트롤 패턴을 확인하고 지원되는 컨트롤 패턴이 노출하는 속성, 메서드, 이벤트 및 구조를 통해 컨트롤과 상호 작용할 수 있습니다. 예를 들어, 여러 줄 편집 상자에 대해 UI 자동화는 <xref:System.Windows.Automation.Provider.IScrollProvider>를 구현합니다. 클라이언트가 <xref:System.Windows.Automation.AutomationElement> 서 <xref:System.Windows.Automation.ScrollPattern> 컨트롤 패턴을 지원한다는 사실을 알고 있으면 클라이언트는 해당 컨트롤 패턴이 노출하는 속성, 메서드 및 이벤트를 사용하여 컨트롤을 조작하거나 컨트롤에 대한 정보에 액세스할 수 있습니다.  
  
<a name="uiautomation_control_pattern_client_provider"></a>   
## <a name="ui-automation-providers-and-clients"></a>UI 자동화 공급자 및 클라이언트  
 UI 자동화 공급자는 컨트롤에서 지원하는 특정 기능에 대해 적절한 동작을 노출하는 컨트롤 패턴을 구현합니다.  
  
 UI 자동화 클라이언트는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 컨트롤 패턴 클래스의 메서드 및 속성에 액세스하고 이를 사용하여 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]에 대한 정보를 가져오거나 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]를 조작합니다. 이러한 컨트롤 패턴 클래스는 <xref:System.Windows.Automation> 네임스페이스(예: <xref:System.Windows.Automation.InvokePattern> 및 <xref:System.Windows.Automation.SelectionPattern>)에서 볼 수 있습니다.  
  
 클라이언트는 <xref:System.Windows.Automation.AutomationElement> 메서드 ( <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=nameWithType> 예: 또는 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=nameWithType>) 또는 CLR (공용 언어 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 런타임) 접근자를 사용 하 여 패턴의 속성에 액세스 합니다. 각 컨트롤 패턴 클래스에는 컨트롤 패턴을 식별 하 고 <xref:System.Windows.Automation.InvokePattern.Pattern?displayProperty=nameWithType> 를 <xref:System.Windows.Automation.SelectionPattern.Pattern?displayProperty=nameWithType>에 <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> 대 한 매개 변수로 전달 하거나 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> 의 <xref:System.Windows.Automation.AutomationElement>해당 패턴을 검색할 수 있는 필드 멤버 (예: 또는)가 있습니다.  
  
<a name="uiautomation_control_patterns_dynamic"></a>   
## <a name="dynamic-control-patterns"></a>동적 컨트롤 패턴  
 일부 컨트롤에서는 동일한 컨트롤 패턴의 집합이 항상 지원되지는 않습니다. 컨트롤 패턴은 UI 자동화 클라이언트에 사용할 수 있을 때 지원되는 것으로 간주됩니다. 예를 들어, 여러 줄 편집 상자를 사용하면 볼 수 있는 영역에 표시할 수 있는 것보다 많은 텍스트 줄이 포함되어 있는 경우에만 세로로 스크롤할 수 있습니다. 스크롤이 더 이상 필요하지 않을만큼 충분한 양의 텍스트가 제거되면 스크롤이 비활성화됩니다. 이 예제에서, ScrollPattern 컨트롤 패턴은 컨트롤의 현재 상태(편집 상자에 있는 텍스트의 양)에 따라 동적으로 지원됩니다.  
  
<a name="Control_Pattern_Classes_and_Interfaces"></a>   
## <a name="control-pattern-classes-and-interfaces"></a>컨트롤 패턴 클래스 및 인터페이스  
 다음 표에서는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 컨트롤 패턴에 대해 설명합니다. 또한 UI 자동화 클라이언트가 컨트롤 패턴에 액세스하는 데 사용하는 클래스와, UI 자동화 공급자가 이러한 컨트롤 패턴을 구현하는 데 사용하는 인터페이스를 나열하여 보여줍니다.  
  
|컨트롤 패턴 클래스|공급자 인터페이스|설명|  
|---------------------------|------------------------|-----------------|  
|<xref:System.Windows.Automation.DockPattern>|<xref:System.Windows.Automation.Provider.IDockProvider>|도킹 컨테이너에서 도킹될 수 있는 컨트롤에 사용됩니다. 예를 들면, 도구 모음 또는 도구 팔레트입니다.|  
|<xref:System.Windows.Automation.ExpandCollapsePattern>|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|확장하거나 축소할 수 있는 컨트롤에 사용됩니다. 예를 들면, **파일** 메뉴와 같은 애플리케이션의 메뉴 항목입니다.|  
|<xref:System.Windows.Automation.GridPattern>|<xref:System.Windows.Automation.Provider.IGridProvider>|지정된 셀로 이동 및 크기 조정과 같은 표 기능을 지원하는 컨트롤에 사용됩니다. 예를 들면, Windows 탐색기의 큰 아이콘 보기 또는 [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)]의 헤더 없는 단순 테이블입니다.|  
|<xref:System.Windows.Automation.GridItemPattern>|<xref:System.Windows.Automation.Provider.IGridItemProvider>|표 내에서 셀이 있는 컨트롤에 사용됩니다. 개별 셀은 GridItem 패턴을 지원해야 합니다. 예를 들면, [!INCLUDE[TLA#tla_winexpl](../../../includes/tlasharptla-winexpl-md.md)] 자세히 보기의 각 셀입니다.|  
|<xref:System.Windows.Automation.InvokePattern>|<xref:System.Windows.Automation.Provider.IInvokeProvider>|호출할 수 있는 컨트롤(예: 단추)에 사용됩니다.|  
|<xref:System.Windows.Automation.MultipleViewPattern>|<xref:System.Windows.Automation.Provider.IMultipleViewProvider>|동일한 정보, 데이터 또는 자식 항목 집합의 여러 표현 간을 전환할 수 있는 컨트롤에 사용됩니다. 예를 들면, 데이터를 축소판, 타일, 아이콘, 목록 또는 자세히 보기로 사용할 수 있는 목록 뷰 컨트롤입니다.|  
|<xref:System.Windows.Automation.RangeValuePattern>|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|컨트롤에 적용할 수 있는 값의 범위가 있는 컨트롤에 사용됩니다. 예를 들어, 연도를 나타내는 회전자 컨트롤의 범위는 1900 ~ 2010이고 월을 나타내는 다른 회전자 컨트롤의 범위는 1 ~ 12입니다.|  
|<xref:System.Windows.Automation.ScrollPattern>|<xref:System.Windows.Automation.Provider.IScrollProvider>|스크롤할 수 있는 컨트롤에 사용됩니다. 예를 들면, 컨트롤의 볼 수 있는 영역에 표시될 수 있는 것보다 많은 정보가 있는 경우 활성 상태의 스크롤 막대가 있는 컨트롤입니다.|  
|<xref:System.Windows.Automation.ScrollItemPattern>|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|스크롤하는 목록의 개별 항목이 포함된 컨트롤에 사용됩니다. 예를 들면, 스크롤 목록의 개별 항목을 가진 목록 컨트롤(예: 콤보 상자 컨트롤)입니다.|  
|<xref:System.Windows.Automation.SelectionPattern>|<xref:System.Windows.Automation.Provider.ISelectionProvider>|선택 컨테이너 컨트롤에 사용됩니다. 예를 들면, 목록 상자 및 콤보 상자입니다.|  
|<xref:System.Windows.Automation.SelectionItemPattern>|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|목록 상자 및 콤보 상자와 같은 선택 컨테이너 컨트롤의 개별 항목에 사용됩니다.|  
|<xref:System.Windows.Automation.TablePattern>|<xref:System.Windows.Automation.Provider.ITableProvider>|헤더 정보 및 표가 있는 컨트롤에 사용됩니다. 예를 들면, [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] 워크시트입니다.|  
|<xref:System.Windows.Automation.TableItemPattern>|<xref:System.Windows.Automation.Provider.ITableItemProvider>|테이블의 항목에 사용됩니다.|  
|<xref:System.Windows.Automation.TextPattern>|<xref:System.Windows.Automation.Provider.ITextProvider>|편집 컨트롤 및 텍스트 정보를 노출하는 문서에 사용됩니다.|  
|<xref:System.Windows.Automation.TogglePattern>|<xref:System.Windows.Automation.Provider.IToggleProvider>|상태를 전환할 수 있는 컨트롤에 사용됩니다. 예를 들면, 확인란 및 선택 가능한 메뉴 항목입니다.|  
|<xref:System.Windows.Automation.TransformPattern>|<xref:System.Windows.Automation.Provider.ITransformProvider>|크기 조정, 이동 및 회전할 수 있는 컨트롤에 사용됩니다. Transform 컨트롤 패턴은 디자이너, 폼, 그래픽 편집기 및 그리기 애플리케이션에서 일반적으로 사용됩니다.|  
|<xref:System.Windows.Automation.ValuePattern>|<xref:System.Windows.Automation.Provider.IValueProvider>|클라이언트가 값 범위를 지원하지 않는 컨트롤에 값을 설정하거나 가져올 수 있습니다. 예를 들면, 날짜 시간 선택입니다.|  
|<xref:System.Windows.Automation.WindowPattern>|<xref:System.Windows.Automation.Provider.IWindowProvider>|창과 관련된 정보, 기초적인 개념을 [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] 운영 체제에 노출합니다. Windows 컨트롤의 예로는 최상위 응용 프로그램 창 ([!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)], [!INCLUDE[TLA#tla_winexpl](../../../includes/tlasharptla-winexpl-md.md)]등), MDI (다중 문서 인터페이스) 자식 창 및 대화 상자가 있습니다.|  
  
## <a name="see-also"></a>참고자료

- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [UI 자동화 클라이언트에 대한 컨트롤 패턴 매핑](control-pattern-mapping-for-ui-automation-clients.md)
- [UI 자동화 개요](ui-automation-overview.md)
- [클라이언트의 UI 자동화 속성](ui-automation-properties-for-clients.md)
- [클라이언트용 UI 자동화 이벤트](ui-automation-events-for-clients.md)
