---
title: 클라이언트에 대한 UI 자동화 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, events for clients
- events, UI Automation clients
ms.assetid: b909e388-3f24-4997-b6d4-bd9c35c2dc27
ms.openlocfilehash: f4ce2d996d5a1a6ecd149118b7499650882a732f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042287"
---
# <a name="ui-automation-events-for-clients"></a>클라이언트에 대한 UI 자동화 이벤트
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 이벤트가 UI 자동화 클라이언트에서 사용되는 방법을 설명합니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]을 통해 클라이언트가 원하는 이벤트를 구독할 수 있습니다. 이 기능은 정보, 구조 또는 상태가 변경되었는지 확인하기 위해 시스템의 모든 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 요소를 지속적으로 폴링하지 않고도 성능을 향상시킵니다.  
  
 정의된 기능 내에서만 이벤트를 수신 대기하는 기능을 통해 효율성도 향상되었습니다. 예를 들어, 클라이언트는 트리의 모든 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요소에서 포커스 변경 이벤트를 수신 대기하거나, 하나의 요소와 해당 하위 항목만 수신 대기할 수 있습니다.  
  
> [!NOTE]
> 가능한 모든 이벤트가 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 공급자에서 발생되지는 않습니다. 예를 들어, 일부 속성의 경우 변경된 사항이 있더라도 표준 프록시 공급자가 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] 및 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 컨트롤에 대한 이벤트를 발생시키지 않습니다.  
  
 광범위 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트 보기는 [UI 자동화 이벤트 개요](ui-automation-events-overview.md)를 참조 하세요.  
  
<a name="Subscribing_to_Events"></a>   
## <a name="subscribing-to-events"></a>이벤트 구독  
 클라이언트 애플리케이션은 다음 방법 중 하나로 이벤트 처리기를 등록하여 특정 종류의 이벤트를 구독합니다.  
  
|메서드|이벤트 형식|이벤트 인수 형식|대리자 형식|  
|------------|----------------|--------------------------|-------------------|  
|<xref:System.Windows.Automation.Automation.AddAutomationFocusChangedEventHandler%2A>|포커스 변경|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|<xref:System.Windows.Automation.AutomationFocusChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>|속성 변경|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|<xref:System.Windows.Automation.AutomationPropertyChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddStructureChangedEventHandler%2A>|구조 변경|<xref:System.Windows.Automation.StructureChangedEventArgs>|<xref:System.Windows.Automation.StructureChangedEventHandler>|  
|<xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>|<xref:System.Windows.Automation.AutomationEvent>로 식별된 기타 모든 이벤트|<xref:System.Windows.Automation.AutomationEventArgs> 또는 <xref:System.Windows.Automation.WindowClosedEventArgs>|<xref:System.Windows.Automation.AutomationEventHandler>|  
  
 메서드를 호출하기 전에, 이벤트를 처리하는 대리자 메서드를 만들어야 합니다. 원하는 경우, 단일 메서드에서 여러 종류의 이벤트를 처리하고 이 메서드를 여러 번 호출하여 테이블에 있는 메서드 중 하나에 전달할 수 있습니다. 예를 들어, 다양한 이벤트를 <xref:System.Windows.Automation.AutomationEventArgs.EventId%2A>에 따라 다르게 처리하도록 단일 <xref:System.Windows.Automation.AutomationEventHandler>를 설정할 수 있습니다.  
  
> [!NOTE]
> 창이 닫힌 이벤트를 처리하려면 <xref:System.Windows.Automation.WindowClosedEventArgs>로 이벤트 처리기에 전달되는 인수 형식을 캐스팅합니다. 창의 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 요소가 더 이상 유효하지 않기 때문에 `sender` 매개 변수를 사용하여 검색을 검색할 수 없습니다. 대신 <xref:System.Windows.Automation.WindowClosedEventArgs.GetRuntimeId%2A>를 사용해야 합니다.  
  
> [!CAUTION]
> 애플리케이션이 자체 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]에서 이벤트를 검색하려는 경우에는 애플리케이션의 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 스레드를 사용하여 이벤트를 구독하거나 구독을 취소하지 않아야 합니다. 이렇게 하면 예기치 않은 동작이 발생할 수 있습니다. 자세한 내용은 [UI Automation Threading Issues](ui-automation-threading-issues.md)을 참조하세요.  
  
 종료되거나 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트가 더 이상 애플리케이션에 필요하지 않는 경우에는 UI 자동화 클라이언트가 다음 메서드 중 하나를 호출해야 합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationEventHandler%2A>|<xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>를 사용하여 등록된 이벤트 처리기의 등록을 취소합니다.|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationFocusChangedEventHandler%2A>|<xref:System.Windows.Automation.Automation.AddAutomationFocusChangedEventHandler%2A>를 사용하여 등록된 이벤트 처리기의 등록을 취소합니다.|  
|<xref:System.Windows.Automation.Automation.RemoveAutomationPropertyChangedEventHandler%2A>|<xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>를 사용하여 등록된 이벤트 처리기의 등록을 취소합니다.|  
|<xref:System.Windows.Automation.Automation.RemoveAllEventHandlers%2A>|등록된 모든 이벤트 처리기를 등록 취소합니다.|  
  
 예제 코드는 [UI 자동화 이벤트 구독](subscribe-to-ui-automation-events.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 이벤트 구독](subscribe-to-ui-automation-events.md)
- [UI 자동화 이벤트 개요](ui-automation-events-overview.md)
- [UI 자동화 속성 개요](ui-automation-properties-overview.md)
- [가는 주요 샘플 샘플](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/FocusTracker)
