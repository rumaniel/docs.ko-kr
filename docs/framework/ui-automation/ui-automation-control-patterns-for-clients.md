---
title: 클라이언트용 UI 자동화 컨트롤 패턴
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, control patterns for clients
- control patterns, UI Automation clients
ms.assetid: 571561d8-5f49-43a9-a054-87735194e013
ms.openlocfilehash: 320833bf147fa16889cd188c7c729cd4dc028843
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042517"
---
# <a name="ui-automation-control-patterns-for-clients"></a>클라이언트용 UI 자동화 컨트롤 패턴
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 개요에서는 UI 자동화 클라이언트에 대한 컨트롤 패턴을 소개합니다. UI 자동화 클라이언트에서 컨트롤 패턴을 사용하여 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)]에 대한 정보에 액세스하는 방법도 소개합니다.  
  
 컨트롤 패턴은 컨트롤 형식 및 컨트롤의 모양에 관계없이 컨트롤의 기능을 분류하고 노출하는 방법을 제공합니다. UI 자동화 클라이언트는 <xref:System.Windows.Automation.AutomationElement> 를 검사하여 지원되는 컨트롤 패턴을 확인하고 컨트롤의 동작을 보장할 수 있습니다.  
  
 컨트롤 패턴의 전체 목록은 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)를 참조하세요.  
  
<a name="uiautomation_getting_control_patterns"></a>   
## <a name="getting-control-patterns"></a>컨트롤 패턴 가져오기  
 클라이언트는 <xref:System.Windows.Automation.AutomationElement> 또는 <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A?displayProperty=nameWithType> 을 호출하여 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A?displayProperty=nameWithType>에서 컨트롤 패턴을 검색합니다.  
  
 클라이언트는 <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A> 메서드 또는 개별 `IsPatternAvailable` 속성(예: <xref:System.Windows.Automation.AutomationElement.IsTextPatternAvailableProperty>)을 사용하여 패턴이나 패턴 그룹이 <xref:System.Windows.Automation.AutomationElement>에서 지원되는지 확인할 수 있습니다. 그러나 컨트롤 패턴을 가져오고 `null` 참조를 테스트하면 프로세스 간 호출을 줄일 수 있으므로 지원되는 속성을 확인하고 컨트롤 패턴을 검색하는 것보다 더 효율적입니다.  
  
 다음 예제에서는 <xref:System.Windows.Automation.TextPattern> 에서 <xref:System.Windows.Automation.AutomationElement>컨트롤 패턴을 가져오는 방법을 보여 줍니다.  
  
 [!code-csharp[UIATextPattern_snip#1037](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIATextPattern_snip/CSharp/SearchWindow.cs#1037)]  
  
<a name="uiautomation_properties_on_control_patterns"></a>   
## <a name="retrieving-properties-on-control-patterns"></a>컨트롤 패턴에 대한 속성 검색  
 클라이언트는 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=nameWithType> 또는 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=nameWithType> 를 호출하고 적절한 형식으로 반환되는 개체를 캐스팅하여 컨트롤 패턴에 대한 속성 값을 검색할 수 있습니다. 속성에 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 대 한 자세한 내용은 [클라이언트에 대 한 UI 자동화 속성](ui-automation-properties-for-clients.md)을 참조 하세요.  
  
 `GetPropertyValue` 메서드 외에도 CLR (공용 언어 런타임) 접근자를 통해 속성 값을 검색 하 여 패턴에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성에 액세스할 수 있습니다.  
  
<a name="uiautomation_with_variable_patterns"></a>   
## <a name="controls-with-variable-patterns"></a>가변 패턴을 사용하는 컨트롤  
 일부 컨트롤 형식은 컨트롤의 상태 또는 컨트롤이 사용되는 방식에 따라 다양한 패턴을 지원합니다. 가변 패턴을 사용할 수 있는 컨트롤의 예로는 목록 보기(미리 보기, 타일, 아이콘, 목록, 자세히), [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] 차트(원형, 꺾은선형, 막대형, 수식이 있는 셀 값), [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)]의 문서 영역(기본, 웹 모양, 개요, 인쇄 모양, 인쇄 미리 보기) 및 [!INCLUDE[TLA#tla_wmp](../../../includes/tlasharptla-wmp-md.md)] 스킨이 있습니다.  
  
 사용자 지정 컨트롤 형식을 구현하는 컨트롤에는 해당 기능을 나타내는 데 필요한 컨트롤 패턴 집합이 있을 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 컨트롤 패턴](ui-automation-control-patterns.md)
- [UI 자동화 텍스트 패턴](ui-automation-text-pattern.md)
- [UI 자동화를 사용하여 컨트롤 호출](invoke-a-control-using-ui-automation.md)
- [UI 자동화를 사용하여 확인란의 전환 상태 가져오기](get-the-toggle-state-of-a-check-box-using-ui-automation.md)
- [UI 자동화 클라이언트에 대한 컨트롤 패턴 매핑](control-pattern-mapping-for-ui-automation-clients.md)
- [TextPattern Insert 텍스트 샘플](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InsertText)
- [TextPattern 검색 및 선택 샘플](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/FindText)
- [InvokePattern, ExpandCollapsePattern 및 TogglePattern 샘플](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InvokePattern)
