---
title: UI 자동화 Scroll 컨트롤 패턴 구현
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Scroll control pattern
- control patterns, Scroll
- Scroll control pattern
ms.assetid: 73d64242-6cbb-424c-92dd-dc69530b7899
ms.openlocfilehash: b8193ed8c7b5fab934d83eb31f5b562136a290ec
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043312"
---
# <a name="implementing-the-ui-automation-scroll-control-pattern"></a>UI 자동화 Scroll 컨트롤 패턴 구현
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 이벤트 및 속성에 대한 정보를 포함하여 <xref:System.Windows.Automation.Provider.IScrollProvider>를 구현하기 위한 지침 및 규칙을 제공합니다. 추가 참조에 대한 링크는 항목 끝에 나열되어 있습니다.  
  
 <xref:System.Windows.Automation.ScrollPattern> 컨트롤 패턴은 자식 개체의 컬렉션에 대해 스크롤할 수 있는 컨테이너 역할을 하는 컨트롤을 지원하는 데 사용됩니다. 이 컨트롤은 스크롤 기능을 지원하기 위해 스크롤 막대를 사용할 필요는 없지만 일반적으로는 스크롤 막대를 사용합니다.  
  
 ![스크롤 막대를 사용 하지 않고 컨트롤을 스크롤합니다.](./media/uia-scrollpattern-without-scrollbars.PNG "UIA_ScrollPattern_Without_Scrollbars")  
스크롤 막대를 사용하지 않는 스크롤 컨트롤의 예제  
  
 이 컨트롤을 구현하는 컨트롤의 예제를 보려면 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)을 참조하세요.  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>구현 지침 및 규칙  
 Scroll 컨트롤 패턴을 구현할 때는 다음 지침 및 규칙에 유의하세요.  
  
- 이 컨트롤의 자식 항목은 <xref:System.Windows.Automation.Provider.IScrollItemProvider>를 구현해야 합니다.  
  
- 컨테이너 컨트롤의 스크롤 막대는 <xref:System.Windows.Automation.ScrollPattern> 컨트롤 패턴을 지원하지 않습니다. 이 스크롤 막대는 <xref:System.Windows.Automation.RangeValuePattern> 컨트롤 패턴을 지원해야 합니다.  
  
- 스크롤이 백분율로 측정되면, 스크롤 눈금과 관련된 모든 값 또는 양은 0에서 100까지의 범위로 정규화되어야 합니다.  
  
- <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> 및 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> 는 <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty>와 관계가 없습니다.  
  
- <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> 이면`false` 를 100%로 설정 하 고<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> 를 로<xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>설정 해야 합니다.  =  <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> 마찬가지로, <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> = `false` 일 경우 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> 는 100%로 설정되어야 하며 <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> 는 <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>를 참조하세요. 따라서 클라이언트가 원하지 않는 스크롤 방향이 활성화되어 있는 경우 UI 자동화 클라이언트는 <xref:System.Windows.Automation.ScrollPattern.SetScrollPercent%2A> 경합 상태 [를 방지하면서](https://support.microsoft.com/default.aspx?scid=kb;en-us;317723) 메서드 내에서 이러한 속성 값을 사용할 수 있습니다.  
  
- <xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalScrollPercent%2A> 는 로캘과 관련됩니다. HorizontalScrollPercent = 100.0으로 설정하는 경우 왼쪽에서 오른쪽으로 읽는 언어(예: 영어)에서 컨트롤의 스크롤 위치는 맨 오른쪽 위치에 해당하는 값으로 설정해야 합니다. 또는 오른쪽에서 왼쪽으로 읽는 언어(예: 아랍어)의 경우 HorizontalScrollPercent = 100.0으로 설정할 경우 스크롤 위치는 맨 왼쪽 위치로 설정해야 합니다.  
  
<a name="Required_Members_for_IScrollProvider"></a>   
## <a name="required-members-for-iscrollprovider"></a>IScrollProvider에 필요한 멤버  
 <xref:System.Windows.Automation.Provider.IScrollProvider>를 구현하려면 다음과 같은 속성 및 메서드가 필요합니다.  
  
|필요한 멤버|멤버 형식|노트|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalScrollPercent%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticalScrollPercent%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalViewSize%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticalViewSize%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontallyScrollable%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticallyScrollable%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A>|메서드|없음|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A>|메서드|없음|  
  
 이 컨트롤 패턴에 연결된 이벤트가 없습니다.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>예외  
 공급자는 다음과 같은 예외를 throw해야 합니다.  
  
|예외 형식|조건|  
|--------------------|---------------|  
|<xref:System.ArgumentException>|컨트롤이 가로 또는 세로 스크롤에 대해서만<xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A> 값을 지원하지만 <xref:System.Windows.Automation.ScrollAmount.SmallIncrement> 값이 전달되는 경우에 <xref:System.Windows.Automation.ScrollAmount.LargeIncrement> 은 이 예외를 발생시킵니다.|  
|<xref:System.ArgumentException>|double로 변환할 수 없는 값이 전달되는 경우<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> 가 이 예외를 발생시킵니다.|  
|<xref:System.ArgumentOutOfRangeException>|100보다 크거나 0보다 작은 값이 전달되는 경우(<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> 에 해당하는 -1 제외) <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>가 이 예외를 발생시킵니다.|  
|<xref:System.InvalidOperationException>|지원되지 않는 방향으로 스크롤이 시도되면 <xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A> 및 <xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> 둘 다 이 예외를 발생시킵니다.|  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
