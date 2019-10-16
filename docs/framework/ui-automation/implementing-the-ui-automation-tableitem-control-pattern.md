---
title: UI 자동화 TableItem 컨트롤 패턴 구현
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, Table Item
- UI Automation, Table Item control pattern
- TableItem control pattern
ms.assetid: ac178408-1485-436f-8d3e-eee3bf80cb24
ms.openlocfilehash: cdbfc8d24dce3b63801682528a49c13d89660935
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043172"
---
# <a name="implementing-the-ui-automation-tableitem-control-pattern"></a>UI 자동화 TableItem 컨트롤 패턴 구현
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 이벤트 및 속성에 대한 정보를 포함하여 <xref:System.Windows.Automation.Provider.ITableItemProvider>를 구현하기 위한 지침 및 규칙을 제공합니다. 추가 참조에 대한 링크는 개요의 끝에 나열되어 있습니다.  
  
 <xref:System.Windows.Automation.TableItemPattern> 컨트롤 패턴은 <xref:System.Windows.Automation.Provider.ITableProvider>를 구현하는 컨테이너의 자식 컨트롤을 지원하는 데 사용됩니다. 개별 셀 기능에 대한 액세스는 <xref:System.Windows.Automation.Provider.IGridItemProvider>의 필수 동시 구현에서 제공됩니다. 이 컨트롤 패턴은 <xref:System.Windows.Automation.Provider.IGridItemProvider>와 유사하지만, <xref:System.Windows.Automation.Provider.ITableItemProvider>를 구현하는 컨트롤은 개별 셀과 셀의 행 및 열 정보 간의 관계를 프로그래밍 방식으로 노출해야 한다는 점이 다릅니다. 이 컨트롤 패턴을 구현하는 컨트롤의 예제를 보려면 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)을 참조하세요.  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>구현 지침 및 규칙  
  
- 관련 그리드 항목 기능에 대해서는 [UI 자동화 GridItem 컨트롤 패턴 구현](implementing-the-ui-automation-griditem-control-pattern.md)을 참조 하세요.  
  
<a name="Required_Members_for_ITableItemProvider"></a>   
## <a name="required-members-for-itableitemprovider"></a>ITableItemProvider에 필요한 멤버  
  
|필요한 멤버|멤버 형식|참고|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.ITableItemProvider.GetColumnHeaderItems%2A>|메서드|없음|  
|<xref:System.Windows.Automation.Provider.ITableItemProvider.GetRowHeaderItems%2A>|메서드|없음|  
  
 이 컨트롤 패턴에는 연결된 속성 또는 이벤트가 없습니다.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>예외  
 이 컨트롤 패턴에 연결된 예외가 없습니다.  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [UI 자동화 Table 컨트롤 패턴 구현](implementing-the-ui-automation-table-control-pattern.md)
- [UI 자동화 GridItem 컨트롤 패턴 구현](implementing-the-ui-automation-griditem-control-pattern.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
