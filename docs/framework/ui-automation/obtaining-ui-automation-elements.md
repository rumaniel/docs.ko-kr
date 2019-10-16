---
title: UI 자동화 요소 가져오기
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, obtaining elements
- elements, UI Automation, obtaining
ms.assetid: c2caaf45-e59c-42a1-bc9b-77a6de520171
ms.openlocfilehash: 46de1b5de8ef7585919d331e6bf4b1537739ae1d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042884"
---
# <a name="obtaining-ui-automation-elements"></a>UI 자동화 요소 가져오기
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 <xref:System.Windows.Automation.AutomationElement> 요소에 대한 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 개체를 가져오는 다양한 방법을 설명합니다.  
  
> [!CAUTION]
> 클라이언트 애플리케이션이 자체 사용자 인터페이스에서 요소를 찾으려고 시도하는 경우 별도 스레드에서 모든 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 을 호출해야 합니다. 자세한 내용은 [UI Automation Threading Issues](ui-automation-threading-issues.md)을 참조하세요.  
  
<a name="The_Root_Element"></a>   
## <a name="root-element"></a>루트 요소  
 <xref:System.Windows.Automation.AutomationElement> 개체에 대한 모든 검색은 시작 지점이 있어야 합니다. 데스크톱, 애플리케이션 창 또는 컨트롤을 포함한 모든 요소가 대상이 될 수 있습니다.  
  
 모든 요소가 하위 항목인 데스크톱의 루트 요소는 정적 <xref:System.Windows.Automation.AutomationElement.RootElement%2A?displayProperty=nameWithType> 속성에서 가져옵니다.  
  
> [!CAUTION]
> 일반적으로 <xref:System.Windows.Automation.AutomationElement.RootElement%2A>의 직계 자식 항목만 가져와야 합니다. 하위 항목 검색은 수 많은 요소에서 반복될 수 있기 때문에 스택 오버플로가 발생할 수 있습니다. 낮은 수준의 특정 요소를 가져오려고 시도하는 경우, 낮은 수준의 컨테이너 또는 애플리케이션 창에서 검색을 시작해야 합니다.  
  
<a name="Using_Conditions"></a>   
## <a name="conditions"></a>조건  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요소를 검색할 때 사용할 수 있는 대부분의 기술에 대해, 검색할 요소가 무엇인지 정의하는 기준 집합인 <xref:System.Windows.Automation.Condition>을 지정해야 합니다.  
  
 가장 간단한 조건은 <xref:System.Windows.Automation.Condition.TrueCondition>으로서, 검색 범위 내의 모든 요소가 반환되도록 하는 미리 정의된 개체입니다. <xref:System.Windows.Automation.Condition.FalseCondition>과는 반대로 <xref:System.Windows.Automation.Condition.TrueCondition>은 요소가 검색되지 않도록 하기 때문에 그다지 유용하지 않습니다.  
  
 단독으로 또는 다른 조건과 함께 사용할 수 있는 기타 미리 정의된 3개의 조건으로 <xref:System.Windows.Automation.Automation.ContentViewCondition>, <xref:System.Windows.Automation.Automation.ControlViewCondition>및 <xref:System.Windows.Automation.Automation.RawViewCondition>이 있습니다. 단독으로 사용되는<xref:System.Windows.Automation.Automation.RawViewCondition>은 <xref:System.Windows.Automation.Condition.TrueCondition>또는 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsControlElement%2A> 속성별로 요소를 필터링하지 않기 때문에 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsContentElement%2A> 에 해당합니다.  
  
 하나 이상의 <xref:System.Windows.Automation.PropertyCondition> 개체에서 기타 조건이 생성되고, 각 조건은 속성 값을 지정합니다. 예를 들어, <xref:System.Windows.Automation.PropertyCondition> 은 요소가 활성화되도록 지정하거나 특정 컨트롤 패턴을 지원하도록 지정할 수 있습니다.  
  
 개체 형식 <xref:System.Windows.Automation.AndCondition>, <xref:System.Windows.Automation.OrCondition>및 <xref:System.Windows.Automation.NotCondition>을 생성하고 부울 논리를 사용하여 조건을 조합할 수 있습니다.  
  
<a name="Search_Scope"></a>   
## <a name="search-scope"></a>검색 범위  
 <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> 또는 <xref:System.Windows.Automation.AutomationElement.FindAll%2A> 을 사용하여 수행되는 검색에는 시작 지점뿐만 아니라 범위가 있어야 합니다.  
  
 범위는 검색되는 시작 지점 주변의 공간을 정의합니다. 여기에는 요소 자체, 형제 항목, 부모 항목, 상위 항목, 직계 자식 항목, 하위 항목이 포함될 수 있습니다.  
  
 검색 범위는 <xref:System.Windows.Automation.TreeScope> 열거형의 값을 비트 조합하여 정의됩니다.  
  
<a name="Finding_a_Known_Element"></a>   
## <a name="finding-a-known-element"></a>알려진 요소 찾기  
 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name%2A>, <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.AutomationId%2A>또는 기타 속성이나 속성의 조합으로 식별된 알려진 요소를 찾으려면 <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> 메서드를 사용하는 것이 가장 쉬운 방법입니다. 검색된 요소가 애플리케이션 창일 경우 검색의 시작 지점은 <xref:System.Windows.Automation.AutomationElement.RootElement%2A>일 수 있습니다.  
  
 이렇게 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요소를 찾는 것은 자동화된 테스트 시나리오에서 가장 유용한 방법입니다.  
  
<a name="Finding_Elements_in_a_Subtree"></a>   
## <a name="finding-elements-in-a-subtree"></a>하위 트리에서 요소 찾기  
 알려진 요소와 관련된 특정 기준을 충족하는 모든 요소를 찾으려면 <xref:System.Windows.Automation.AutomationElement.FindAll%2A>을 사용합니다. 예를 들어, 목록 또는 메뉴에서 목록 항목이나 메뉴 항목을 검색하거나 대화 상자의 모든 컨트롤을 식별할 때 이 메서드를 사용할 수 있습니다.  
  
<a name="Walking_a_Subtree"></a>   
## <a name="walking-a-subtree"></a>하위 트리 탐색  
 클라이언트가 사용되는 애플리케이션에 대한 사전 지식이 없는 경우 <xref:System.Windows.Automation.TreeWalker> 클래스를 사용하여 필요한 모든 요소의 하위 트리를 생성할 수 있습니다. 애플리케이션이 포커스 변경 이벤트에 대한 응답으로 이 작업을 수행할 수 있습니다. 즉, 애플리케이션 또는 컨트롤이 입력 포커스를 받으면 UI 자동화 클라이언트는 포커스가 있는 요소의 자식 항목 및 모든 하위 항목을 검사합니다.  
  
 <xref:System.Windows.Automation.TreeWalker> 를 사용하여 요소의 상위 항목을 식별할 수도 있습니다. 예를 들어, 트리를 탐색하여 컨트롤의 부모 창을 식별할 수 있습니다.  
  
 필요한 클래스의 개체를 만들거나( <xref:System.Windows.Automation.TreeWalker> 을 전달하여 필요한 요소 정의) <xref:System.Windows.Automation.Condition>의 필드로 정의된 미리 정의된 다음 개체 중 하나를 사용하여 <xref:System.Windows.Automation.TreeWalker>를 사용할 수 있습니다.  
  
|||  
|-|-|  
|<xref:System.Windows.Automation.TreeWalker.ContentViewWalker>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsContentElement%2A> 속성이 `true`인 요소만 찾습니다.|  
|<xref:System.Windows.Automation.TreeWalker.ControlViewWalker>|<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsControlElement%2A> 속성이 `true`인 요소만 찾습니다.|  
|<xref:System.Windows.Automation.TreeWalker.RawViewWalker>|모든 요소를 찾습니다.|  
  
 <xref:System.Windows.Automation.TreeWalker>를 가져온 후에는 간단하게 사용할 수 있습니다. `Get` 메서드를 호출하여 하위 트리의 요소를 탐색하면 됩니다.  
  
 <xref:System.Windows.Automation.TreeWalker.Normalize%2A> 메서드를 사용하여 뷰에 속하지 않은 다른 요소의 하위 트리에서 요소를 탐색할 수 있습니다. 예를 들어, <xref:System.Windows.Automation.TreeWalker.ContentViewWalker>를 사용하여 하위 트리 뷰를 만들었다고 가정해 보겠습니다. 그러면 스크롤 막대가 입력 포커스를 받았다는 알림이 애플리케이션에 전달됩니다. 스크롤 막대는 콘텐츠 요소가 아니기 때문에 하위 트리의 뷰에 나타나지 않습니다. 하지만 스크롤 막대를 나타내는 <xref:System.Windows.Automation.AutomationElement> 를 <xref:System.Windows.Automation.TreeWalker.Normalize%2A> 에 전달하고 콘텐츠 뷰에 있는 가장 가까운 상위 항목을 검색할 수 있습니다.  
  
<a name="Other_Ways_to_Retrieve_an_Element"></a>   
## <a name="other-ways-to-retrieve-an-element"></a>요소를 검색하는 기타 방법  
 검색 및 탐색 외에도 다음과 같은 방법으로 <xref:System.Windows.Automation.AutomationElement> 를 검색할 수 있습니다.  
  
### <a name="from-an-event"></a>이벤트에서  
 애플리케이션이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트를 수신하면, 이벤트 처리기에 전달된 소스 개체는 <xref:System.Windows.Automation.AutomationElement>입니다. 예를 들어, 포커스 변경 이벤트를 구독한 경우 <xref:System.Windows.Automation.AutomationFocusChangedEventHandler> 에 전달된 소스는 포커스를 받은 요소입니다.  
  
 자세한 내용은 [Subscribe to UI Automation Events](subscribe-to-ui-automation-events.md)을 참조하세요.  
  
### <a name="from-a-point"></a>지점에서  
 화면 좌표가 있는 경우(예: 커서 위치) 정적 <xref:System.Windows.Automation.AutomationElement> 메서드를 사용하여 <xref:System.Windows.Automation.AutomationElement.FromPoint%2A> 를 검색할 수 있습니다.  
  
### <a name="from-a-window-handle"></a>창 핸들에서  
 HWND에서 <xref:System.Windows.Automation.AutomationElement> 를 검색하려면 정적 <xref:System.Windows.Automation.AutomationElement.FromHandle%2A> 메서드를 사용합니다.  
  
### <a name="from-the-focused-control"></a>포커스가 있는 컨트롤에서  
 정적 <xref:System.Windows.Automation.AutomationElement> 속성에서 포커스가 있는 컨트롤을 나타내는 <xref:System.Windows.Automation.AutomationElement.FocusedElement%2A> 를 검색할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [속성 조건을 기반으로 UI 자동화 요소 찾기](find-a-ui-automation-element-based-on-a-property-condition.md)
- [TreeWalker를 사용하여 UI 자동화 요소 간 탐색](navigate-among-ui-automation-elements-with-treewalker.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
