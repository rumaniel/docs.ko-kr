---
title: UI 자동화 요소 속성 가져오기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties, retrieving
- UI Automation, retrieving properties of elements
ms.assetid: 09576b1a-291f-435c-980e-dee32d899ae1
ms.openlocfilehash: 158ebf29bb504dd11f9e8416011226fc5846873e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043610"
---
# <a name="get-ui-automation-element-properties"></a>UI 자동화 요소 속성 가져오기
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요소의 속성을 검색 하는 방법을 보여 줍니다.  
  
### <a name="get-a-current-property-value"></a>현재 속성 값을 가져옵니다.  
  
1. 가져올 속성이 <xref:System.Windows.Automation.AutomationElement> 있는를 가져옵니다.  
  
2. 를 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A>호출 하거나 속성 구조 <xref:System.Windows.Automation.AutomationElement.Current%2A> 를 검색 하 고 해당 멤버 중 하나에서 값을 가져옵니다.  
  
### <a name="get-a-cached-property-value"></a>캐시 된 속성 값 가져오기  
  
1. 가져올 속성이 <xref:System.Windows.Automation.AutomationElement> 있는를 가져옵니다. 속성은에 <xref:System.Windows.Automation.CacheRequest>지정 되어 있어야 합니다.  
  
2. 를 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A>호출 하거나 속성 구조 <xref:System.Windows.Automation.AutomationElement.Cached%2A> 를 검색 하 고 해당 멤버 중 하나에서 값을 가져옵니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 <xref:System.Windows.Automation.AutomationElement>현재 속성을 검색 하는 다양 한 방법을 보여 줍니다.  
  
 [!code-csharp[UIAClient_snip#170](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#170)]
 [!code-vb[UIAClient_snip#170](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#170)]  
  
## <a name="see-also"></a>참고자료

- [클라이언트의 UI 자동화 속성](ui-automation-properties-for-clients.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
- [UI 자동화 클라이언트의 캐싱](caching-in-ui-automation-clients.md)
