---
title: UI 자동화 Toggle 컨트롤 패턴 구현
ms.date: 03/30/2017
helpviewer_keywords:
- Toggle control pattern
- control patterns, Toggle
- UI Automation, Toggle control pattern
ms.assetid: 3cfe875f-b0c0-413d-9703-5f14e6a1a30e
ms.openlocfilehash: a9b03fbffc4e922cb3d00738e8df00fc0393b799
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043131"
---
# <a name="implementing-the-ui-automation-toggle-control-pattern"></a>UI 자동화 Toggle 컨트롤 패턴 구현
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 메서드 및 속성에 대한 정보를 비롯하여 <xref:System.Windows.Automation.Provider.IToggleProvider>구현을 위한 지침 및 규칙을 제공합니다. 추가 참조에 대한 링크는 항목 끝에 나열되어 있습니다.  
  
 <xref:System.Windows.Automation.TogglePattern> 컨트롤 패턴은 일련의 상태를 순환할 수 있는 컨트롤을 지원하고 설정된 상태를 유지합니다. 이 컨트롤 패턴을 구현하는 컨트롤의 예제를 보려면 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)을 참조하세요.  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>구현 지침 및 규칙  
 Toggle 컨트롤 패턴을 구현할 때는 다음 지침 및 규칙에 유의하세요.  
  
- 활성화되면 상태가 유지되지 않는 컨트롤(예: 단추, 도구 모음 단추, 하이퍼링크)은 <xref:System.Windows.Automation.Provider.IInvokeProvider> 를 대신 구현해야 합니다.  
  
- 컨트롤은 다음 순서대로 <xref:System.Windows.Automation.ToggleState> 를 순환해야 합니다. <xref:System.Windows.Automation.ToggleState.On>, <xref:System.Windows.Automation.ToggleState.Off> , <xref:System.Windows.Automation.ToggleState.Indeterminate>(지원되는 경우)  
  
- <xref:System.Windows.Automation.TogglePattern> 은 적절한 <xref:System.Windows.Automation.ToggleState> 순서로 순환하지 않고 3상 확인란을 직접 설정하는 것과 관련된 문제로 인해 SetState(newState) 메서드를 제공하지 않습니다.  
  
- RadioButton 컨트롤은 유효한 상태를 순환할 수 없기 때문에 <xref:System.Windows.Automation.Provider.IToggleProvider>를 구현하지 않습니다.  
  
<a name="Required_Members_for_IToggleProvider"></a>   
## <a name="required-members-for-itoggleprovider"></a>IToggleProvider에 필요한 멤버  
 <xref:System.Windows.Automation.Provider.IToggleProvider>를 구현하려면 다음과 같은 속성 및 메서드가 필요합니다.  
  
|필요한 멤버|멤버 형식|참고|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.TogglePattern.Toggle%2A>|메서드|없음|  
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty>|속성|없음|  
  
 이 컨트롤 패턴에 연결된 이벤트가 없습니다.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>예외  
 이 컨트롤 패턴에 연결된 예외가 없습니다.  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [UI 자동화를 사용하여 확인란의 전환 상태 가져오기](get-the-toggle-state-of-a-check-box-using-ui-automation.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
