---
title: UI 자동화 ScrollItem 컨트롤 패턴 구현
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, Scroll Item
- UI Automation, Scroll Item control pattern
- Scroll Item control pattern
ms.assetid: 903bab5c-80c1-44d7-bdc2-0a418893b987
ms.openlocfilehash: e8f9373c840b00c8089f01a562f768f27f2cd945
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043296"
---
# <a name="implementing-the-ui-automation-scrollitem-control-pattern"></a>UI 자동화 ScrollItem 컨트롤 패턴 구현
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 속성, 메서드 및 이벤트에 대한 정보를 포함하여 <xref:System.Windows.Automation.Provider.IScrollItemProvider>를 구현하기 위한 지침 및 규칙을 제공합니다. 추가 참조에 대한 링크는 항목 끝에 나열되어 있습니다.  
  
 <xref:System.Windows.Automation.ScrollItemPattern> 컨트롤 패턴은 <xref:System.Windows.Automation.Provider.IScrollProvider>를 구현하는 컨테이너의 개별 자식 컨트롤을 지원하는 데 사용됩니다. 이 컨트롤 패턴은 자식 컨트롤과 해당 컨테이너 간에 통신 채널 역할을 하여 컨테이너가 자식 컨트롤이 표시되도록 뷰포트 내에 현재 표시된 콘텐츠(또는 영역)를 변경할 수 있습니다. 이 컨트롤 패턴을 구현하는 컨트롤의 예제를 보려면 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)을 참조하세요.  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>구현 지침 및 규칙  
 Scroll Item 컨트롤 패턴을 구현할 때는 다음 지침 및 규칙에 유의하세요.  
  
- 창 또는 캔버스 컨트롤 내에 포함된 항목은 IScrollItemProvider 인터페이스를 구현하는 데 필요하지 않습니다. 그 대신, <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>에 대해 유효한 위치를 노출해야 합니다. 이렇게 하면 UI 자동화 클라이언트 애플리케이션이 컨테이너의 <xref:System.Windows.Automation.ScrollPattern> 컨트롤 패턴 메서드를 사용하여 자식 항목을 표시할 수 있습니다.  
  
<a name="Required_Members_for_IScrollItemProvider"></a>   
## <a name="required-members-for-iscrollitemprovider"></a>IScrollItemProvider에 필요한 멤버  
 다음 메서드는 IScrollProvider 인터페이스를 구현하는 데 필요합니다.  
  
|필요한 멤버|멤버 형식|참고|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IScrollItemProvider.ScrollIntoView%2A>|-메서드|없음|  
  
 이 컨트롤 패턴에는 연결된 속성 또는 이벤트가 없습니다.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>예외  
 공급자는 다음과 같은 예외를 throw해야 합니다.  
  
|예외 형식|조건|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|항목을 스크롤하여 볼 수 없는 경우:<br /><br /> -   <xref:System.Windows.Automation.ScrollItemPattern.ScrollIntoView%2A>|  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
