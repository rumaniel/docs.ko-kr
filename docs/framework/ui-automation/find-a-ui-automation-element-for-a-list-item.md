---
title: 목록 항목의 UI 자동화 요소 찾기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- list items, finding elements for
- elements, finding for list items
- UI Automation, finding elements for List items
ms.assetid: c326ad2b-2144-4f64-ae4c-d850c74f95c5
ms.openlocfilehash: 2b9fb1ffe4b20074de66afe6d418a7cf5d39be0c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043722"
---
# <a name="find-a-ui-automation-element-for-a-list-item"></a>목록 항목의 UI 자동화 요소 찾기
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 항목의 인덱스를 <xref:System.Windows.Automation.AutomationElement> 알고 있을 때 목록 내의 항목에 대 한를 검색 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 목록에서 지정 된 항목을 검색 하 <xref:System.Windows.Automation.TreeWalker> 는 두 가지 방법, 즉를 사용 하는 방법과를 사용 <xref:System.Windows.Automation.AutomationElement.FindAll%2A>하는 방법을 보여 줍니다.  
  
 첫 번째 기술은 컨트롤의 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 속도는 더 빠르지만 Windows Presentation Foundation (WPF) 컨트롤에 대 한 두 번째 기술은 더 빠릅니다.  
  
 [!code-csharp[UIAClient_snip#184](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#184)]
 [!code-vb[UIAClient_snip#184](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#184)]  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 요소 가져오기](obtaining-ui-automation-elements.md)
