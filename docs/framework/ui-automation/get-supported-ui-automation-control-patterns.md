---
title: 지원되는 UI 자동화 컨트롤 패턴 가져오기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- control patterns, getting
- UI Automation, getting control patterns
- getting, control patterns
ms.assetid: 006c54c9-50bf-48d9-a855-9d62eb95603a
ms.openlocfilehash: 133dabe861fbbcf5cac3fbb8669b78e582f8b87b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043653"
---
# <a name="get-supported-ui-automation-control-patterns"></a>지원되는 UI 자동화 컨트롤 패턴 가져오기
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]  요소에서 컨트롤 패턴을 검색하는 방법을 보여 줍니다.  
  
### <a name="obtain-all-control-patterns"></a>모든 컨트롤 패턴 가져오기  
  
1. 사용할 컨트롤 패턴이 있는 <xref:System.Windows.Automation.AutomationElement>를 가져옵니다.  
  
2. 요소에서 모든 컨트롤 패턴을 가져오려면 <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>를 호출합니다.  
  
> [!CAUTION]
> 클라이언트가 <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A>를 사용하지 않는 것이 좋습니다. 이 메서드는 기존의 각 컨트롤 패턴에 대해 내부적으로 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>을 호출하기 때문에 성능에 심각한 영향을 줄 수 있습니다. 가능하면 클라이언트는 사용할 키 패턴에 대해 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>을 호출해야 합니다.  
  
### <a name="obtain-a-specific-control-pattern"></a>특정 컨트롤 패턴 가져오기  
  
1. 사용할 컨트롤 패턴이 있는 <xref:System.Windows.Automation.AutomationElement>를 가져옵니다.  
  
2. 특정 패턴을 쿼리하려면 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> 또는 <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>를 호출합니다. 이러한 메서드는 비슷하지만, 해당 패턴을 찾을 수 없는 경우 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A>에서 예외가 발생하고 <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>가 `false`를 반환합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 목록 항목에 대해 <xref:System.Windows.Automation.AutomationElement>를 검색하고 해당 요소에서 <xref:System.Windows.Automation.SelectionItemPattern>을 가져옵니다.  
  
 [!code-csharp[UIAClient_snip#103](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#103)]
 [!code-vb[UIAClient_snip#103](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#103)]  
  
## <a name="see-also"></a>참고자료

- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
