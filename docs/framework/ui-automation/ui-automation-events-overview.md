---
title: UI 자동화 이벤트 개요
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, providers
- UI Automation, events
- clients, UI Automation
- events, UI Automation
- providers, UI Automation
- UI Automation, clients
ms.assetid: 69eebd8b-39ed-40e7-93cc-4457c4caf746
ms.openlocfilehash: d342e4382cfe227e477ab87c2ca428834010768e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042157"
---
# <a name="ui-automation-events-overview"></a>UI 자동화 이벤트 개요
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 이벤트 알림은 화면 판독기 및 화면 돋보기 같은 보조 기술의 핵심 기능입니다. 이러한 UI 자동화 클라이언트는 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 에서 상황이 발생하면 UI 자동화 공급자에서 생기는 이벤트를 추적하고 이 정보를 사용해 최종 사용자에게 알립니다.  
  
 클라이언트가 이벤트 알림에 가입했는지 여부에 따라 공급자 애플리케이션에서 선택적으로 이벤트를 발생시키거나 이벤트 수신 가입한 클라이언트가 없는 경우 이벤트를 전혀 발생시키지 않도록 하면 효율성이 향상됩니다.  
  
<a name="Types_of_Events"></a>   
## <a name="types-of-events"></a>이벤트 유형  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트는 다음 범주로 구분됩니다.  
  
|이벤트(event)|설명|  
|-----------|-----------------|  
|속성 변경|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요소의 속성이나 컨트롤 패턴이 변경되면 발생합니다. 예를 들어 클라이언트가 애플리케이션의 확인란 컨트롤을 모니터링해야 하는 경우 <xref:System.Windows.Automation.TogglePattern.TogglePatternInformation.ToggleState%2A> 속성에 대한 속성 변경 이벤트를 수신하도록 등록할 수 있습니다. 확인란 컨트롤을 선택하거나 선택 취소하면 공급자가 이벤트를 발생시키며 클라이언트가 필요에 따라 동작할 수 있습니다.|  
|요소 작업|[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 결과가 최종 사용자나 프로그래밍 작업에 의해 변경되면(예: 단추를 클릭하거나 <xref:System.Windows.Automation.InvokePattern>을 통해 호출) 발생합니다.|  
|구조 변경|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 구조가 변경되면 발생합니다. 새 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 항목이 데스크톱에서 표시되거나 숨겨지거나 제거되면 구조가 변경됩니다.|  
|전역 데스크톱 변경|요소 간에 포커스가 전환되거나 창이 닫히는 경우와 같이 클라이언트에 전역적으로 영향을 미치는 작업이 이루어지면 발생합니다.|  
  
 일부 이벤트는 UI 상태가 변경된 것을 의미하지 않을 수도 있습니다. 예를 들어 사용자가 텍스트 입력 필드를 탭한 다음 단추를 클릭하여 필드를 업데이트하면 사용자가 실제로 텍스트를 변경하지 않았어도 `TextChangedEvent` 이벤트가 발생합니다. 이벤트를 처리할 때 클라이언트 애플리케이션이 작업을 수행하기 전에 실제로 변경된 사항이 있는지 여부를 확인해야 할 수도 있습니다.  
  
 다음 이벤트는 UI의 상태가 변경되지 않은 경우에도 발생할 수 있습니다.  
  
- `AutomationPropertyChangedEvent` (변경된 속성에 따라 다름)  
  
- `ElementSelectedEvent`  
  
- `InvalidatedEvent`  
  
- `TextChangedEvent`  
  
<a name="UI_Automation_Event_Identifiers"></a>   
## <a name="ui-automation-event-identifiers"></a>UI 자동화 이벤트 식별자  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 이벤트는 <xref:System.Windows.Automation.AutomationEvent> 개체에 의해 식별됩니다. <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> 속성에는 이런 종류의 이벤트를 고유하게 식별하는 값이 포함되어 있습니다.  
  
 <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> 에 가능한 값은 이벤트 인수에 사용되는 형식과 함께 다음 표에 나와 있습니다. 클라이언트 및 공급자에서 사용되는 식별자는 서로 다른 클래스에서 나온, 이름이 같은 필드입니다.  
  
|클라이언트 식별자|공급자 식별자|이벤트 인수 형식|  
|-----------------------|-------------------------|--------------------------|  
|<xref:System.Windows.Automation.AutomationElement.AsyncContentLoadedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AsyncContentLoadedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AsyncContentLoadedEventArgs>|  
|<xref:System.Windows.Automation.SelectionItemPattern.ElementAddedToSelectionEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionItemPattern.ElementRemovedFromSelectionEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionItemPattern.ElementSelectedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionPattern.InvalidatedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.InvokePattern.InvokedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.LayoutInvalidatedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.MenuClosedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.MenuOpenedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.TextPattern.TextChangedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.TextPattern.TextSelectionChangedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.ToolTipClosedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElement.ToolTipOpenedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.WindowPattern.WindowOpenedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.MenuClosedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.MenuOpenedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipClosedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipOpenedEvent?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.AutomationPropertyChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationPropertyChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.StructureChangedEventArgs>|  
|<xref:System.Windows.Automation.WindowPattern.WindowClosedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent?displayProperty=nameWithType>|<xref:System.Windows.Automation.WindowClosedEventArgs>|  
  
<a name="UI_Automation_Event_Arguments"></a>   
## <a name="ui-automation-event-arguments"></a>UI 자동화 이벤트 인수  
 다음 클래스는 이벤트 인수를 캡슐화합니다.  
  
|클래스|설명|  
|-----------|-----------------|  
|<xref:System.Windows.Automation.AsyncContentLoadedEventArgs>|로딩 완료율을 포함하여 콘텐츠의 비동기 로드에 대한 정보를 포함합니다.|  
|<xref:System.Windows.Automation.AutomationEventArgs>|추가 데이터가 필요 없는 간단한 이벤트에 대한 정보를 포함합니다.|  
|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|요소 간의 입력 포커스 변경에 대한 정보를 포함합니다. 이 유형의 이벤트는 공급자가 아니라 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 시스템에서 발생합니다.|  
|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|요소 속성 값 또는 컨트롤 패턴의 변경에 대한 정보를 포함합니다.|  
|<xref:System.Windows.Automation.StructureChangedEventArgs>|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 변경에 대한 정보를 포함합니다.|  
|<xref:System.Windows.Automation.WindowClosedEventArgs>|창 닫기에 대한 정보를 포함합니다.|  
  
 모든 이벤트 인수 클래스에 <xref:System.Windows.Automation.AutomationEventArgs.EventId%2A> 멤버가 포함됩니다. 이 식별자는 <xref:System.Windows.Automation.AutomationEvent>에서 캡슐화됩니다.  
  
 이벤트를 식별하는 데 사용되는 <xref:System.Windows.Automation.AutomationEvent> 개체는 공급자가 <xref:System.Windows.Automation.AutomationElementIdentifiers> 의 필드 및 <xref:System.Windows.Automation.DockPatternIdentifiers>등의 컨트롤 패턴 식별자 클래스에서 가져옵니다. 해당하는 필드는 클라이언트 애플리케이션이 <xref:System.Windows.Automation.AutomationElement> 의 필드 및 <xref:System.Windows.Automation.DockPattern>등의 컨트롤 패턴 클래스에서 가져옵니다.  
  
 이벤트 식별자 목록은 [UI Automation Events for Clients](ui-automation-events-for-clients.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [클라이언트용 UI 자동화 이벤트](ui-automation-events-for-clients.md)
- [서버 쪽 UI 자동화 공급자 구현](server-side-ui-automation-provider-implementation.md)
- [UI 자동화 이벤트 구독](subscribe-to-ui-automation-events.md)
