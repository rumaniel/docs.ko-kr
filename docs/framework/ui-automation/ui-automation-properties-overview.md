---
title: UI 자동화 속성 개요
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, properties
- properties, UI Automation
ms.assetid: a6c31d7b-b33e-49b3-b5c1-31a345f9b7c8
ms.openlocfilehash: 59d65601a37c9aba63708748a82fd5e85261b75b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042138"
---
# <a name="ui-automation-properties-overview"></a>UI 자동화 속성 개요
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 UI 자동화 공급자는 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 요소에 속성을 노출합니다. 이러한 속성을 통해 UI 자동화 클라이언트 애플리케이션은 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)]항목에 대한 정보(특히 정적 및 동적 데이터를 포함한 컨트롤)를 검색할 수 있습니다.  
  
 이 섹션에서는 광범위한 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 속성 개요를 제공합니다. 보다 구체적인 정보는 다음 항목에서 제공됩니다.  
  
- [클라이언트의 UI 자동화 속성](ui-automation-properties-for-clients.md)  
  
- [서버 쪽 UI 자동화 공급자 구현](server-side-ui-automation-provider-implementation.md)  
  
<a name="Property_Identifiers"></a>   
## <a name="property-identifiers"></a>속성 식별자  
 모든 속성은 숫자 및 이름으로 식별됩니다. 속성의 이름은 디버깅 및 진단용으로만 사용됩니다. 공급자는 숫자 Id를 사용 하 여 들어오는 속성 요청을 식별 합니다. 그러나 클라이언트 애플리케이션은 숫자 및 이름 캡슐화하는 <xref:System.Windows.Automation.AutomationProperty>만 사용하여 검색하려는 속성을 식별합니다.  
  
 특정 속성을 나타내는<xref:System.Windows.Automation.AutomationProperty> 개체는 다양한 클래스에 필드로 사용할 수 있습니다. 보안상의 이유로, UI 자동화 공급자는 Uiautomationtypes.dll에 포함된 별도의 클래스 집합에서 이러한 개체를 가져옵니다.  
  
 다음 표에서는 id를 <xref:System.Windows.Automation.AutomationProperty>포함 하는 클래스로 속성을 분류 합니다.  
  
|속성의 종류|클라이언트가 ID를 가져오는 위치|공급자 ID를 가져오는 위치|  
|-------------------------|--------------------------|----------------------------|  
|모든 요소에 공통된 속성(다음 표 참조)|<xref:System.Windows.Automation.AutomationElement>|<xref:System.Windows.Automation.AutomationElementIdentifiers>|  
|도킹 창의 위치|<xref:System.Windows.Automation.DockPattern>|<xref:System.Windows.Automation.DockPatternIdentifiers>|  
|확장 및 축소할 수 있는 요소의 상태|<xref:System.Windows.Automation.ExpandCollapsePattern>|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers>|  
|표에 있는 항목의 속성|<xref:System.Windows.Automation.GridItemPattern>|<xref:System.Windows.Automation.GridItemPatternIdentifiers>|  
|표의 속성|<xref:System.Windows.Automation.GridPattern>|<xref:System.Windows.Automation.GridPatternIdentifiers>|  
|여러 뷰가 있는 요소의 현재 및 지원되는 뷰|<xref:System.Windows.Automation.MultipleViewPattern>|<xref:System.Windows.Automation.MultipleViewPatternIdentifiers>|  
|값 범위 내에서 이동하는 요소의 속성(예: 슬라이더)|<xref:System.Windows.Automation.RangeValuePattern>|<xref:System.Windows.Automation.RangeValuePatternIdentifiers>|  
|스크롤 창의 속성|<xref:System.Windows.Automation.ScrollPattern>|<xref:System.Windows.Automation.ScrollPatternIdentifiers>|  
|선택할 수 있는 항목의 상태 및 컨테이너(예: 목록 내부)|<xref:System.Windows.Automation.SelectionItemPattern>|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers>|  
|선택 항목을 포함하는 컨트롤의 속성|<xref:System.Windows.Automation.SelectionPattern>|<xref:System.Windows.Automation.SelectionPatternIdentifiers>|  
|테이블에 있는 항목의 열 및 행 헤더|<xref:System.Windows.Automation.TableItemPattern>|<xref:System.Windows.Automation.TableItemPatternIdentifiers>|  
|테이블의 열 및 행 헤더와 방향|<xref:System.Windows.Automation.TablePattern>|<xref:System.Windows.Automation.TablePatternIdentifiers>|  
|토글 컨트롤의 상태|<xref:System.Windows.Automation.TogglePattern>|<xref:System.Windows.Automation.TogglePatternIdentifiers>|  
|이동, 회전, 크기 조정할 수 있는 요소의 기능|<xref:System.Windows.Automation.TransformPattern>|<xref:System.Windows.Automation.TransformPatternIdentifiers>|  
|값이 있는 요소의 값과 읽기/쓰기 기능|<xref:System.Windows.Automation.ValuePattern>|<xref:System.Windows.Automation.ValuePatternIdentifiers>|  
|창의 기능 및 상태|<xref:System.Windows.Automation.WindowPattern>|<xref:System.Windows.Automation.WindowPatternIdentifiers>|  
  
<a name="Properties_by_Category"></a>   
## <a name="properties-by-category"></a>범주별 속성  
 다음 표에서는 및 <xref:System.Windows.Automation.AutomationElement> <xref:System.Windows.Automation.AutomationElementIdentifiers>에서 id를 찾을 수 있는 속성을 분류 합니다. 이러한 속성은 모든 컨트롤에 공통됩니다. 일부를 제외한 모든 속성은 공급자 애플리케이션의 수명 동안 정적일 가능성이 높습니다. 대부분의 동적 속성은 컨트롤 패턴과 연결되어 있습니다.  
  
 **속성 액세스** 열에는 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A> 및 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A>외에도 각 속성에 대한 기타 접근자가 나열됩니다. 클라이언트 애플리케이션에서 속성을 가져오는 방법에 대한 자세한 내용은 [UI Automation Properties for Clients](ui-automation-properties-for-clients.md)을 참조하세요.  
  
> [!NOTE]
> 각 속성에 대한 특정 정보를 보려면 **속성 액세스** 열에 있는 링크를 클릭하세요.  
  
### <a name="display-characteristics"></a>특성 표시  
  
|속성 식별자|속성 액세스|  
|-------------------------|---------------------|  
|<xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.BoundingRectangle%2A>|  
|<xref:System.Windows.Automation.AutomationElement.CultureProperty>|N/A|  
|<xref:System.Windows.Automation.AutomationElement.HelpTextProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.HelpText%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsOffscreenProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsOffscreen%2A>|  
|<xref:System.Windows.Automation.AutomationElement.OrientationProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Orientation%2A>|  
  
### <a name="element-type"></a>요소 형식  
  
|속성 식별자|속성 액세스|  
|-------------------------|---------------------|  
|<xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ControlType%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsContentElementProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsContentElement%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsControlElementProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsControlElement%2A>|  
|<xref:System.Windows.Automation.AutomationElement.ItemTypeProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ItemType%2A>|  
|<xref:System.Windows.Automation.AutomationElement.LocalizedControlTypeProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.LocalizedControlType%2A>|  
  
### <a name="identification"></a>ID  
  
|속성 식별자|속성 액세스|  
|-------------------------|---------------------|  
|<xref:System.Windows.Automation.AutomationElement.AutomationIdProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.AutomationId%2A>|  
|<xref:System.Windows.Automation.AutomationElement.ClassNameProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ClassName%2A>|  
|<xref:System.Windows.Automation.AutomationElement.FrameworkIdProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.FrameworkId%2A>|  
|<xref:System.Windows.Automation.AutomationElement.LabeledByProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.LabeledBy%2A>|  
|<xref:System.Windows.Automation.AutomationElement.NameProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name%2A>|  
|<xref:System.Windows.Automation.AutomationElement.ProcessIdProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ProcessId%2A>|  
|<xref:System.Windows.Automation.AutomationElement.RuntimeIdProperty>|<xref:System.Windows.Automation.AutomationElement.GetRuntimeId%2A>|  
|<xref:System.Windows.Automation.AutomationElement.NativeWindowHandleProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.NativeWindowHandle%2A>|  
  
### <a name="interaction"></a>상호 작용  
  
|속성 식별자|속성 액세스|  
|-------------------------|---------------------|  
|<xref:System.Windows.Automation.AutomationElement.AcceleratorKeyProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.AcceleratorKey%2A>|  
|<xref:System.Windows.Automation.AutomationElement.AccessKeyProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.AccessKey%2A>|  
|<xref:System.Windows.Automation.AutomationElement.ClickablePointProperty>|<xref:System.Windows.Automation.AutomationElement.GetClickablePoint%2A>|  
|<xref:System.Windows.Automation.AutomationElement.HasKeyboardFocusProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.HasKeyboardFocus%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsEnabledProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsEnabled%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsKeyboardFocusableProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsKeyboardFocusable%2A>|  
  
### <a name="support-for-patterns"></a>패턴에 대한 지원  
  
|속성 식별자|속성 액세스|  
|-------------------------|---------------------|  
|<xref:System.Windows.Automation.AutomationElement.IsDockPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsExpandCollapsePatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsGridItemPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsGridPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsInvokePatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsMultipleViewPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsRangeValuePatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsScrollItemPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsScrollPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsSelectionItemPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsSelectionPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsTableItemPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsTablePatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsTextPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsTogglePatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsTransformPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsValuePatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsWindowPatternAvailableProperty>|<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>|  
  
### <a name="miscellaneous"></a>기타  
  
|속성 식별자|속성 액세스|  
|-------------------------|---------------------|  
|<xref:System.Windows.Automation.AutomationElement.IsRequiredForFormProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsRequiredForForm%2A>|  
|<xref:System.Windows.Automation.AutomationElement.IsPasswordProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsPassword%2A>|  
|<xref:System.Windows.Automation.AutomationElement.ItemStatusProperty>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ItemStatus%2A>|  
  
<a name="Localization"></a>   
## <a name="localization"></a>지역화  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 공급자는 운영 체제의 언어에 다음과 같은 속성을 제공해야 합니다.  
  
- <xref:System.Windows.Automation.AutomationElementIdentifiers.AcceleratorKeyProperty>  
  
- <xref:System.Windows.Automation.AutomationElementIdentifiers.AccessKeyProperty>  
  
- <xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>  
  
- <xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>  
  
- <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>  
  
<a name="Properties_and_Events"></a>   
## <a name="properties-and-events"></a>속성 및 이벤트  
 의 속성을 사용한 밀접한 관계는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 변경 이벤트의 개념입니다. 동적 속성의 경우, 클라이언트 애플리케이션에서는 속성 값이 변경되었는지 확인하는 방법이 필요합니다. 그에 따라 정보 캐시를 업데이트하거나 다른 방법으로 새로운 정보에 대응할 수 있습니다.  
  
 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 에 변경이 수행되면 공급자가 이벤트를 발생시킵니다. 예를 들어, 확인란이 선택되거나 선택 취소되면 공급자의 Toggle 패턴 구현에서 속성 변경 이벤트가 발생합니다. 공급자는 클라이언트가 이벤트 또는 특정 이벤트를 수신 대기하는지에 따라 선택적으로 이벤트를 발생시킬 수 있습니다.  
  
 일부 공급자는 이벤트를 발생시키지 않습니다. 이는 요소에 대한 UI 자동화 공급자의 구현에 따라 다릅니다. 예를 들어, 목록 상자에 대한 표준 프록시 공급자는 <xref:System.Windows.Automation.SelectionPattern.SelectionProperty> 가 변경될 때 이벤트를 발생시키지 않습니다. 이 경우, 애플리케이션은 <xref:System.Windows.Automation.SelectionItemPattern.ElementSelectedEvent>를 수신 대기합니다.  
  
 클라이언트는 이벤트를 구독하여 이벤트를 수신 대기합니다. 이벤트를 구독하는 것은 이벤트를 처리할 수 있는 대리자 메서드를 만들고, 이러한 메서드에서 처리될 특정 이벤트와 함께 해당 메서드를 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 에 전달한다는 의미입니다. 특히 속성 변경 이벤트의 경우 클라이언트는 <xref:System.Windows.Automation.AutomationPropertyChangedEventHandler>를 구현해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 클라이언트의 캐싱](caching-in-ui-automation-clients.md)
- [클라이언트의 UI 자동화 속성](ui-automation-properties-for-clients.md)
- [서버 쪽 UI 자동화 공급자 구현](server-side-ui-automation-provider-implementation.md)
- [속성 조건을 기반으로 UI 자동화 요소 찾기](find-a-ui-automation-element-based-on-a-property-condition.md)
- [UI 자동화 공급자에서 속성 반환](return-properties-from-a-ui-automation-provider.md)
- [UI 자동화 공급자에서 이벤트 발생](raise-events-from-a-ui-automation-provider.md)
