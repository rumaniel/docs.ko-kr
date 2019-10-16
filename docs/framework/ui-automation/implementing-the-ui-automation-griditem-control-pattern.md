---
title: UI 자동화 GridItem 컨트롤 패턴 구현
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, GridItem
- UI Automation GridItem control pattern
- GridItem control pattern
ms.assetid: bffbae08-fe2a-42fd-ab84-f37187518916
ms.openlocfilehash: fdaac3cad61f6047201587e48d4377fa61b868af
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043409"
---
# <a name="implementing-the-ui-automation-griditem-control-pattern"></a>UI 자동화 GridItem 컨트롤 패턴 구현
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 속성에 대한 정보를 포함하여 <xref:System.Windows.Automation.Provider.IGridItemProvider>를 구현하기 위한 지침 및 규칙을 제공합니다. 추가 참조에 대한 링크는 개요의 끝에 나열되어 있습니다.  
  
 <xref:System.Windows.Automation.GridItemPattern> 컨트롤 패턴은 <xref:System.Windows.Automation.Provider.IGridProvider>를 구현하는 컨테이너의 개별 자식 컨트롤을 지원하는 데 사용됩니다. 이 컨트롤 패턴을 구현하는 컨트롤의 예제를 보려면 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)을 참조하세요.  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>구현 지침 및 규칙  
 <xref:System.Windows.Automation.Provider.IGridProvider>를 구현할 때는 다음 지침 및 규칙에 유의하세요.  
  
- 표 좌표는 왼쪽 상단 셀 좌표가 (0, 0)인 0부터 시작되는 좌표입니다.  
  
- 병합된 셀은 UI 자동화 공급자가 정의한 기본 앵커 셀을 기반으로 해당 <xref:System.Windows.Automation.Provider.IGridItemProvider.Row%2A> 및 <xref:System.Windows.Automation.Provider.IGridItemProvider.Column%2A> 속성을 보고합니다. 일반적으로, 기본 앵커 셀은 맨 위쪽 및 맨 왼쪽 행이나 열입니다.  
  
- <xref:System.Windows.Automation.Provider.IGridItemProvider>는 셀 병합 또는 분할과 같은 표이 활성 조작 기능을 제공하지 않습니다.  
  
- <xref:System.Windows.Automation.Provider.IGridItemProvider>를 구현하는 컨트롤은 일반적으로 키보드를 사용하여 트래버스(즉, UI 자동화 클라이언트가 인접 컨트롤로 이동할 수 있음)할 수 있습니다.  
  
<a name="Required_Members_for_IGridItemProvider"></a>   
## <a name="required-members-for-igriditemprovider"></a>IGridItemProvider에 필요한 멤버  
 <xref:System.Windows.Automation.Provider.IGridItemProvider>를 구현하려면 다음과 같은 속성 및 메서드가 필요합니다.  
  
|필요한 멤버|멤버 형식|노트|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.Row%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.Column%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.RowSpan%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.ColumnSpan%2A>|속성|없음|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.ContainingGrid%2A>|속성|없음|  
  
 이 컨트롤 패턴에는 연결된 메서드 또는 이벤트가 없습니다.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>예외  
 이 컨트롤 패턴에 연결된 예외가 없습니다.  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [UI 자동화 Grid 컨트롤 패턴 구현](implementing-the-ui-automation-grid-control-pattern.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
