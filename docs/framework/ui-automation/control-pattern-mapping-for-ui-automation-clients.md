---
title: UI 자동화 클라이언트에 대한 컨트롤 패턴 매핑
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, for UI Automation clients
- UI Automation, clients, control patterns for
ms.assetid: 8b81645b-8be3-4e26-9c98-4fb0fceca06b
ms.openlocfilehash: cfd8e5dbe34df7b947646c714a360cf56b0435a4
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043855"
---
# <a name="control-pattern-mapping-for-ui-automation-clients"></a>UI 자동화 클라이언트에 대한 컨트롤 패턴 매핑
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 컨트롤 형식 및 이 형식과 연결된 컨트롤 패턴을 나열하여 보여줍니다.  
  
 다음 표는 컨트롤 패턴을 다음과 같은 범주로 정리하여 보여줍니다.  
  
- 지원됩니다. 컨트롤은 이 컨트롤 패턴을 지원해야 합니다.  
  
- 조건부 지원입니다. 컨트롤은 컨트롤의 상태에 따라 이 컨트롤 패턴을 지원할 수 있습니다.  
  
- 지원되지 않습니다. 컨트롤은 이 컨트롤 패턴을 지원하지 않습니다. 사용자 지정 컨트롤이 이 컨트롤 패턴을 지원할 수 있습니다.  
  
> [!NOTE]
> 일부 컨트롤은 컨트롤 기능에 따라 몇몇 컨트롤 패턴을 조건부로 지원합니다. 예를 들어, 메뉴 항목 컨트롤은 메뉴 컨트롤의 기능에 따라 <xref:System.Windows.Automation.InvokePattern>, <xref:System.Windows.Automation.ExpandCollapsePattern>, <xref:System.Windows.Automation.TogglePattern>또는 <xref:System.Windows.Automation.SelectionItemPattern> 컨트롤 패턴을 조건부로 지원합니다.  
  
<a name="control_mapping_clients"></a>   
## <a name="ui-automation-control-patterns-for-clients"></a>클라이언트용 UI 자동화 컨트롤 패턴  
  
|컨트롤 종류|지원함|조건부 지원|지원되지 않음|  
|------------------|---------------|-------------------------|-------------------|  
|단추|없음|Invoke, Toggle, Expand Collapse|없음|  
|일정|Grid, Table|Selection, Scroll|값|  
|확인란|설정/해제|없음|없음|  
|Combo Box|확장 축소|선택, 값|Scroll|  
|Data Grid|표 형태|Scroll, Selection, Table|없음|  
|Data Item|Selection Item|Expand Collapse, Grid Item, Scroll Item, Table, Toggle, Value|없음|  
|문서|텍스트|Scroll, Value|없음|  
|편집|없음|Text, Range Value, Value|없음|  
|그룹|없음|확장 축소|없음|  
|머리글|없음|변형|없음|  
|Header Item|없음|Transform, Invoke|없음|  
|하이퍼링크|호출|값|없음|  
|이미지|없음|Grid Item, Table Item|Invoke, Selection Item|  
|List|없음|Grid, Multiple View, Scroll, Selection|Table|  
|List Item|Selection Item|Expand Collapse, Grid Item, Invoke, Scroll Item, Toggle, Value|없음|  
|메뉴|없음|없음|없음|  
|메뉴 모음|없음|Expand Collapse, Dock, Transform|없음|  
|메뉴 항목|없음|Expand Collapse, Invoke, Selection Item, Toggle|없음|  
|창|없음|Dock. Scroll, Transform|창|  
|Progress Bar|없음|Range Value, Value|없음|  
|Radio Button|Selection Item|없음|설정/해제|  
|Scroll Bar|없음|Range Value|Scroll|  
|구분 기호|없음|없음|없음|  
|슬라이더|없음|Range Value, Selection, Value|없음|  
|Spinner|없음|Range Value, Selection, Value|없음|  
|분할 단추|Invoke, Expand Collapse|없음|없음|  
|상태 표시줄|없음|표 형태|없음|  
|탭|선택|Scroll|없음|  
|Tab Item|Selection Item|없음|호출|  
|Table|Grid, Grid Item, Table, Table Item|없음|없음|  
|텍스트|없음|Grid Item, Table Item, Text|값|  
|Thumb|변환|없음|없음|  
|제목 표시줄|없음|없음|없음|  
|Tool Bar|없음|Dock, Expand Collapse, Transform|없음|  
|Tool Tip|없음|Text, Window|없음|  
|Tree|없음|Scroll, Selection|없음|  
|Tree Item|확장 축소|Invoke, Scroll Item, Selection Item, Toggle|없음|  
|창|Transform, Window|도킹|없음|  
  
> [!NOTE]
> 컨트롤 형식에 지원되는 컨트롤 패턴이 없지만 조건부로 지원되는 하나 이상의 컨트롤 패턴이 있는 경우, 조건부 컨트롤 패턴 중 하나는 항상 지원됩니다.  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 개요](ui-automation-overview.md)
