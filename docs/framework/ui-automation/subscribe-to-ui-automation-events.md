---
title: UI 자동화 이벤트 구독
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UI Automation, subscribing to events
- subscribing to UI Automation events
- events, subscribing to
- listening for events
ms.assetid: b688effa-b3e8-4b05-944d-05ed89a245aa
ms.openlocfilehash: 1e148869f619729c72eae67892d4767eed9f8fb3
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042636"
---
# <a name="subscribe-to-ui-automation-events"></a>UI 자동화 이벤트 구독
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 UI 자동화 공급자가 발생시킨 이벤트를 구독하는 방법을 보여줍니다.  
  
## <a name="example"></a>예제  
 다음 예제 코드는 단추와 같은 컨트롤을 호출할 때 발생하는 이벤트에 대한 이벤트 처리기를 등록하고, 애플리케이션 폼이 닫힐 때 이벤트 처리기를 제거하는 방법을 보여줍니다. 해당 이벤트는 <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>에 매개 변수로 전달된 <xref:System.Windows.Automation.AutomationEvent>로 식별됩니다.  
  
 [!code-csharp[UIAClient_snip#101](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#101)]
 [!code-vb[UIAClient_snip#101](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#101)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]을 사용하여 포커스가 변경될 때 발생되는 이벤트를 구독하는 방법을 보여줍니다. 이벤트 처리기는 애플리케이션 종료 시 호출될 수 있는 메서드에서 등록 취소되거나, UI 이벤트 알림이 더 이상 필요하지 않은 경우에 등록 취소됩니다.  
  
 [!code-csharp[UIAClient_snip#102](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#102)]
 [!code-vb[UIAClient_snip#102](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#102)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>
- <xref:System.Windows.Automation.Automation.RemoveAllEventHandlers%2A>
- <xref:System.Windows.Automation.Automation.RemoveAutomationEventHandler%2A>
- [UI 자동화 이벤트 개요](ui-automation-events-overview.md)
