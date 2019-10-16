---
title: UI 자동화 Invoke 컨트롤 패턴 구현
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Invoke control pattern
- control patterns, Invoke
- Invoke control pattern
ms.assetid: e5b1e239-49f8-468e-bfec-1fba02ec9ac4
ms.openlocfilehash: e9815e4c2c0740f213632681200e48c8e4786657
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043388"
---
# <a name="implementing-the-ui-automation-invoke-control-pattern"></a>UI 자동화 Invoke 컨트롤 패턴 구현

> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).

이 항목에서는 이벤트 및 속성에 대한 정보를 포함하여 <xref:System.Windows.Automation.Provider.IInvokeProvider>를 구현하기 위한 지침 및 규칙을 제공합니다. 추가 참조에 대한 링크는 항목 끝에 나열되어 있습니다.

<xref:System.Windows.Automation.InvokePattern> 컨트롤 패턴은 활성화되었을 때 상태를 유지하지 않고 명확한 단일 작업을 시작하거나 수행하는 컨트롤을 지원하는 데 사용됩니다. 확인란 및 라디오 단추와 같이 상태를 유지하는 컨트롤은 각각 <xref:System.Windows.Automation.Provider.IToggleProvider> 및 <xref:System.Windows.Automation.Provider.ISelectionItemProvider> 를 구현해야 합니다. Invoke 컨트롤 패턴을 구현하는 컨트롤의 예제를 보려면 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)을 참조하세요.

<a name="Implementation_Guidelines_and_Conventions"></a>

## <a name="implementation-guidelines-and-conventions"></a>구현 지침 및 규칙

Invoke 컨트롤 패턴을 구현할 때는 다음 지침 및 규칙에 유의하세요.

- 동일한 동작이 다른 컨트롤 패턴 공급자를 통해 노출되지 않으면 컨트롤이 <xref:System.Windows.Automation.Provider.IInvokeProvider> 를 구현합니다. 예를 들어, 컨트롤의 <xref:System.Windows.Automation.InvokePattern.Invoke%2A> 메서드가 <xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> 또는 <xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A> 메서드와 동일한 작업을 수행하는 경우 이 컨트롤은 <xref:System.Windows.Automation.Provider.IInvokeProvider>를 구현하지 않아야 합니다.

- 일반적으로 컨트롤은 미리 정의된 키보드 바로 가기 또는 몇 가지 키 입력의 조합을 클릭하거나, 두 번 클릭하거나, ENTER 키를 눌러 호출합니다.

- <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent> 는 활성화된 컨트롤에서 발생합니다(연결된 작업을 수행하는 컨트롤에 대한 응답으로) 가능하면, 컨트롤이 작업을 완료하여 차단하지 않고 반환된 후에 이벤트가 발생해야 합니다. 다음 시나리오에서 호출 요청을 처리하기 전에 Invoked 이벤트가 발생해야 합니다.

  - 작업이 완료될 때까지 기다리는 것은 실제로 불가능합니다.

  - 작업에는 사용자 개입이 필요합니다.

  - 작업은 시간이 오래 걸리므로 상당한 시간 동안 호출 클라이언트가 차단됩니다.

- 컨트롤 호출로 인해 심각한 부작용이 발생하는 경우, 이러한 부작용은 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.HelpText%2A> 속성을 통해 노출되어야 합니다. 예를 들어, <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> 가 선택 항목과 연결되지 않은 경우에도 <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> 로 인해 다른 컨트롤이 선택될 수 있습니다.

- 마우스 포인터(또는 마우스를 위에 올려 놓기) 효과는 일반적으로 Invoked 이벤트로 간주되지 않습니다. 하지만 가리키기 상태를 기반으로 작업을 수행(시각적 효과를 발생시키는 것과 반대 개념)하는 컨트롤은 <xref:System.Windows.Automation.InvokePattern> 컨트롤 패턴을 지원해야 합니다.

> [!NOTE]
> 이 구현은 컨트롤을 마우스 관련 부작용의 결과로만 호출할 수 있는 경우 접근성 문제로 간주됩니다.

- 컨트롤을 호출하는 것은 항목을 선택하는 것과 다릅니다. 그러나 컨트롤에 따라, 컨트롤 호출로 인해 항목이 잘못된 방식으로 선택될 수 있습니다. 예를 들어, 내 문서 폴더에서 [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] 문서 목록 항목을 호출하면 항목이 선택되고 문서가 열리는 두 가지 작업이 수행됩니다.

- 호출하는 즉시 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에서 요소가 사라질 수 있습니다. 그 결과, 이벤트 콜백에서 제공하는 요소로부터 정보를 요청하는 작업에 실패할 수 있습니다. 이러한 문제의 해결 방법으로 캐시된 정보를 프리페치하는 것이 좋습니다.

- 컨트롤은 여러 개의 컨트롤 패턴을 구현할 수 있습니다. 예를 들어, [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] 도구 모음의 채우기 색 컨트롤은 <xref:System.Windows.Automation.InvokePattern> 및 <xref:System.Windows.Automation.ExpandCollapsePattern> 컨트롤 패턴 둘 다 구현합니다. <xref:System.Windows.Automation.ExpandCollapsePattern> 은 메뉴를 노출하고 <xref:System.Windows.Automation.InvokePattern> 은 선택된 색으로 활성 상태의 선택 항목을 채웁니다.

<a name="Required_Members_for_the_IValueProvider_Interface"></a>

## <a name="required-members-for-iinvokeprovider"></a>IInvokeProvider에 필요한 멤버

<xref:System.Windows.Automation.Provider.IInvokeProvider>를 구현하려면 다음과 같은 속성 및 메서드가 필요합니다.

|필요한 멤버|멤버 형식|참고|
|----------------------|-----------------|-----------|
|<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A>|메서드|<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> 는 비동기 호출이며 차단하지 않고 즉시 반환해야 합니다.<br /><br /> 이 동작은 호출될 때 직접 또는 간접적으로 모달 대화 상자를 시작하는 컨트롤에 특히 중요합니다. 이벤트를 발생시킨 모든 UI 자동화 클라이언트는 모달 대화 상자가 닫힐 때까지 차단된 상태로 유지됩니다.|

<a name="Exceptions"></a>

## <a name="exceptions"></a>예외

공급자는 다음과 같은 예외를 throw해야 합니다.

|예외 형식|조건|
|--------------------|---------------|
|<xref:System.Windows.Automation.ElementNotEnabledException>|컨트롤이 사용 설정되지 않은 경우.|

## <a name="see-also"></a>참고자료

- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [UI 자동화를 사용하여 컨트롤 호출](invoke-a-control-using-ui-automation.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
