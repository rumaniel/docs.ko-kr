---
title: UI 자동화 SelectionItem 컨트롤 패턴 구현
ms.date: 03/30/2017
helpviewer_keywords:
- Selection Item control pattern
- UI Automation, Selection Item control pattern
- control patterns, Selection Item
ms.assetid: 76b0949a-5b23-4cfc-84cc-154f713e2e12
ms.openlocfilehash: 8b1492bbc9f761c08b178bf42bdf5287bc5ebfb1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043205"
---
# <a name="implementing-the-ui-automation-selectionitem-control-pattern"></a>UI 자동화 SelectionItem 컨트롤 패턴 구현
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 속성, 메서드 및 이벤트에 대한 정보를 포함하여 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>를 구현하기 위한 지침 및 규칙을 제공합니다. 추가 참조에 대한 링크는 개요의 끝에 나열되어 있습니다.  
  
 <xref:System.Windows.Automation.SelectionItemPattern> 컨트롤 패턴은 <xref:System.Windows.Automation.Provider.ISelectionProvider>를 구현하는 컨테이너 컨트롤의 선택 가능한 개별 자식 항목 역할을 하는 컨트롤을 지원하는 데 사용됩니다. SelectionItem 컨트롤 패턴을 구현 하는 컨트롤의 예제는 [UI 자동화 클라이언트에 대 한 컨트롤 패턴 매핑](control-pattern-mapping-for-ui-automation-clients.md) 을 참조 하세요.  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>구현 지침 및 규칙  
 Selection Item 컨트롤 패턴을 구현할 때는 다음 지침 및 규칙에 유의하세요.  
  
- <xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>표시 속성 **대화 상자의** 화면 해상도 **슬라이더와 같이** 를 구현하는 자식 컨트롤을 관리하는 단일 선택 컨트롤은 <xref:System.Windows.Automation.Provider.ISelectionProvider> 를 구현해야 하며, 해당 자식 항목은 <xref:System.Windows.Automation.Provider.IRawElementProviderFragment> 및 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>둘 다 구현해야 합니다.  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>   
## <a name="required-members-for-iselectionitemprovider"></a>ISelectionItemProvider에 필요한 멤버  
 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>를 구현하려면 다음과 같은 속성, 메서드 및 이벤트가 필요합니다.  
  
|필요한 멤버|멤버 형식|노트|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.GetSelection%2A>|메서드|없음|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|이벤트|컨테이너의 선택 항목이 현저히 변경되어 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent> 상수가 허용하는 것보다 더 많은 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent> 및 <xref:System.Windows.Automation.Provider.AutomationInteropProvider.InvalidateLimit> 이벤트를 보내야 하는 경우에 발생합니다.|  
  
- <xref:System.Windows.Automation.SelectionItemPattern.Select%2A> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent> /  <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent> , 또는 의<xref:System.Windows.Automation.SelectionItemPattern.RemoveFromSelection%2A> 결과가 선택 된 단일 항목인 경우이 발생 해야 합니다. 그렇지 않으면를 적절 하 게 보냅니다. <xref:System.Windows.Automation.SelectionItemPattern.AddToSelection%2A>  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>예외  
 공급자는 다음과 같은 예외를 throw해야 합니다.  
  
|예외 형식|조건|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|다음 중 하나가 시도되는 경우:<br /><br /> -   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> 이 <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> = `true` 이고 요소가 이미 선택되어 있는 단일 선택 컨테이너에 호출되는 경우.<br />-   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> 이 <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> = `true` 이고 요소가 하나만 선택된 다중 선택 컨테이너에 호출되는 경우.<br />-   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.AddToSelection%2A> 이 <xref:System.Windows.Automation.SelectionPattern.CanSelectMultipleProperty> = `false` 이고 다른 요소가 이미 선택된 단일 선택 컨테이너에 호출되는 경우.|  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [UI 자동화 Selection 컨트롤 패턴 구현](implementing-the-ui-automation-selection-control-pattern.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
- [조각 공급자 샘플](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771502(v=vs.90))
