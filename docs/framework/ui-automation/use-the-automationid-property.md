---
title: AutomationID 속성 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- AutomationId property
- UI Automation, AutomationId property
- properties, AutomationId
ms.assetid: a24e807b-d7c3-4e93-ac48-80094c4e1c90
ms.openlocfilehash: 7a172db8bcb626d78a24b546147b4e32f20f5d83
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291352"
---
# <a name="use-the-automationid-property"></a>AutomationID 속성 사용
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. @No__t-0에 대 한 최신 정보는 [Windows Automation API를 참조 하세요. UI 자동화 @ no__t-0.  
  
 이 항목에는 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 를 사용하여 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 내에서 요소를 찾는 방법과 시기를 보여주는 시나리오와 샘플 코드가 있습니다.  
  
 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 는 형제 항목에서 UI 자동화 요소를 고유하게 식별합니다. 컨트롤 식별과 관련된 속성 식별자에 대한 자세한 내용은 [UI Automation Properties Overview](ui-automation-properties-overview.md)를 참조하세요.  
  
> [!NOTE]
> <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 는 트리 전체에서 고유한 ID를 보장하지 않습니다. 일반적으로 컨테이너 및 범위 정보가 필요합니다. 예를 들어, 애플리케이션에는 여러 개의 최상위 메뉴가 있는 메뉴 컨트롤과 여러 개의 자식 메뉴 항목이 포함될 수 있습니다. 이러한 보조 메뉴 항목은 "Item1", "Item 2" 등과 같이 일반적인 체계로 식별되어 최상위 메뉴 항목에서 자식에 대한 중복 식별자가 허용될 수 있습니다.  
  
## <a name="scenarios"></a>시나리오  
 주 UI 자동화 클라이언트 애플리케이션의 3가지 시나리오에서, <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 를 사용해야 요소를 검색할 때 정확하고 일관된 결과를 얻을 수 있다고 확인되었습니다.  
  
> [!NOTE]
> <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> 는 최상위 애플리케이션 창, ID 또는 x:Uid가 없는 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 컨트롤에서 파생된 UI 자동화 요소, 컨트롤 ID가 없는 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 컨트롤에서 파생된 UI 자동화 요소를 제외하고 컨트롤 뷰의 모든 UI 자동화 요소에서 지원됩니다.  
  
#### <a name="use-a-unique-and-discoverable-automationid-to-locate-a-specific-element-in-the-ui-automation-tree"></a>검색 가능하고 고유한 AutomationID를 사용하여 UI 자동화 트리에서 특정 요소를 찾습니다.  
  
- UI Spy와 같은 도구를 사용 하 여 관심 있는 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 요소의 <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty>을 보고 합니다. 그런 다음 이 값을 복사하여 클라이언트 애플리케이션에 붙여넣을 수 있습니다(예: 이후의 자동 테스트를 위한 테스트 스크립트). 이 방법은 런타임 시에 요소를 식별하고 찾는 데 필요한 코드의 수를 줄이고 간소화합니다.  
  
> [!CAUTION]
> 일반적으로 <xref:System.Windows.Automation.AutomationElement.RootElement%2A>의 직계 자식 항목만 가져와야 합니다. 하위 항목 검색은 수 많은 요소에서 반복될 수 있기 때문에 스택 오버플로가 발생할 수 있습니다. 낮은 수준의 특정 요소를 가져오려고 시도하는 경우, 낮은 수준의 컨테이너 또는 애플리케이션 창에서 검색을 시작해야 합니다.  
  
 [!code-csharp[UIAAutomationID_snip#100](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAAutomationID_snip/CSharp/FindByAutomationID.xaml.cs#100)]
 [!code-vb[UIAAutomationID_snip#100](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAAutomationID_snip/VisualBasic/FindByAutomationID.xaml.vb#100)]  
  
#### <a name="use-a-persistent-path-to-return-to-a-previously-identified-automationelement"></a>영구 경로를 사용하여 이전에 식별된 AutomationElement로 돌아가기  
  
- 간단한 테스트 스크립트에서 견고한 레코드 및 재생 유틸리티에 이르기까지, 클라이언트 애플리케이션은 파일 열기 대화 상자 또는 메뉴 항목 등과 같이 현재 인스턴스화되지 않아서 UI 자동화 트리에 존재하지 않는 요소에 액세스해야 할 수 있습니다. 이러한 요소는 AutomationID, 컨트롤 패턴 및 이벤트 수신기와 같은 UI 자동화 속성을 사용 하 여 UI 작업의 특정 시퀀스를 재현 하거나 "재생" 해야만 인스턴스화할 수 있습니다.
  
 [!code-csharp[UIAAutomationID_snip#UIAWorkerThread](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAAutomationID_snip/CSharp/FindByAutomationID.xaml.cs#uiaworkerthread)]
 [!code-vb[UIAAutomationID_snip#UIAWorkerThread](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAAutomationID_snip/VisualBasic/FindByAutomationID.xaml.vb#uiaworkerthread)]  
[!code-csharp[UIAAutomationID_snip#Playback](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAAutomationID_snip/CSharp/FindByAutomationID.xaml.cs#playback)]
[!code-vb[UIAAutomationID_snip#Playback](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAAutomationID_snip/VisualBasic/FindByAutomationID.xaml.vb#playback)]  
  
#### <a name="use-a-relative-path-to-return-to-a-previously-identified-automationelement"></a>상대 경로를 사용하여 이전에 식별된 AutomationElement로 돌아가기  
  
- 특정 상황에서는 AutomationID가 형제 항목 간에서만 고유하기 때문에 UI 자동화 트리에서 여러 요소의 AutomationID 속성 값이 동일할 수 있습니다. 이러한 상황에서는 필요에 따라 최상위 항목을 기준으로 요소를 고유하게 식별할 수 있습니다. 예를 들어, 개발자가 자식 항목이 "Item1", "Item2" 등과 같은 순차적 AutomationID로 식별되는 여러 개의 자식 메뉴 항목과 함께 다수의 메뉴 항목이 있는 메뉴 모음을 제공할 수 있습니다. 이 경우, 필요에 따라 상위 항목 및 최상위 항목(필요한 경우)의 AutomationID와 함께 각 메뉴 항목의 AutomationID로 고유하게 식별할 수 있습니다.  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty>
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [속성 조건을 기반으로 UI 자동화 요소 찾기](find-a-ui-automation-element-based-on-a-property-condition.md)
