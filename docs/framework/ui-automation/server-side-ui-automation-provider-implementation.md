---
title: 서버 쪽 UI 자동화 공급자 구현
ms.date: 03/30/2017
helpviewer_keywords:
- server-side UI Automation provider implementation
- UI Automation, server-side provider implementation
- provider implementation, UI Automation
ms.assetid: 6acc6d08-bd67-4e2e-915c-9c1d34eb86fe
ms.openlocfilehash: eb7156e0e2794fb7cb18e7bfce0e8488d0b145c3
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042773"
---
# <a name="server-side-ui-automation-provider-implementation"></a>서버 쪽 UI 자동화 공급자 구현

> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).

이 섹션에서는 사용자 지정 컨트롤에 대한 서버 쪽 UI 자동화 공급자를 구현하는 방법을 설명합니다.

WPF (Windows Presentation Foundation) 요소 및[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 요소가 아닌 요소 (예: 용 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]으로 디자인 된 요소)의 구현은 근본적으로 다릅니다. [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 요소는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 에서 파생 클래스를 통해 <xref:System.Windows.Automation.Peers.AutomationPeer>에 대해 지원합니다. 비[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 요소는 공급자 인터페이스의 구현을 통해 지원합니다.

<a name="Security_Considerations"></a>

## <a name="security-considerations"></a>보안 고려 사항

부분적 신뢰 환경에서 작동할 수 있도록 공급자를 작성해야 합니다. UIAutomationClient.dll은 부분적 신뢰 환경에서 실행되도록 구성되지 않았으므로, 공급자 코드가 해당 어셈블리를 참조해서는 안 됩니다. 참조하는 경우에는 이 코드를 완전 신뢰 환경에서 실행할 수 있지만 부분적 신뢰 환경에서 실패합니다.

특히 UIAutomationClient.dll의 클래스에서 가져온 필드(예: <xref:System.Windows.Automation.AutomationElement>의 필드)를 사용하지 않습니다. 대신, UIAutomationTypes.dll의 클래스(예: <xref:System.Windows.Automation.AutomationElementIdentifiers>)에서 가져온 해당 필드를 사용합니다.

<a name="Provider_Implementation_by_WPF_Elements"></a>

## <a name="provider-implementation-by-windows-presentation-foundation-elements"></a>Windows Presentation Foundation 요소를 사용한 공급자 구현

이 항목에 대한 자세한 내용은 [WPF 사용자 지정 컨트롤의 UI 자동화](../wpf/controls/ui-automation-of-a-wpf-custom-control.md)를 참조하세요.

<a name="Provider_Implementation_by_non_WPF_Elements"></a>

## <a name="provider-implementation-by-non-wpf-elements"></a>비 WPF 요소를 사용한 공급자 구현

[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 프레임워크의 일부가 아니지만 관리 코드로 작성된 사용자 지정 컨트롤(대부분의 경우 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] 컨트롤)은 인터페이스를 구현하여 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 에 대해 지원합니다. 모든 요소는 다음 섹션의 첫 번째 표에 나온 인터페이스 중 하나 이상을 구현해야 합니다. 또한 요소가 하나 이상의 컨트롤 패턴을 지원하는 경우 각 컨트롤 패턴에 대해 적절한 인터페이스를 구현해야 합니다.

[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 공급자 프로젝트는 다음 어셈블리를 참조해야 합니다.

- UIAutomationProviders.dll

- UIAutomationTypes.dll

- WindowsBase.dll

<a name="Provider_Interfaces"></a>

### <a name="provider-interfaces"></a>공급자 인터페이스

모든 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 공급자는 다음 인터페이스 중 하나를 구현해야 합니다.

|인터페이스|설명|
|---------------|-----------------|
|<xref:System.Windows.Automation.Provider.IRawElementProviderSimple>|컨트롤 패턴 및 속성에 대한 지원을 포함하여 창에서 호스트되는 간단한 제어용 기능을 제공합니다.|
|<xref:System.Windows.Automation.Provider.IRawElementProviderFragment>|<xref:System.Windows.Automation.Provider.IRawElementProviderSimple>에서 상속됩니다. 조각 내의 탐색, 포커스 설정, 요소의 경계 사각형 반환 등을 포함하여 복잡한 제어에 있는 요소에 대한 기능을 추가합니다.|
|<xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>|<xref:System.Windows.Automation.Provider.IRawElementProviderFragment>에서 상속됩니다. 지정된 좌표에 자식 요소 배치, 전체 컨트롤에 대한 포커스 상태 설정을 포함하여 복잡한 제어에 있는 루트 요소에 대한 기능을 추가합니다.|

다음 인터페이스는 추가된 기능을 제공하지만 반드시 구현할 필요는 없습니다.

|인터페이스|설명|
|---------------|-----------------|
|<xref:System.Windows.Automation.Provider.IRawElementProviderAdviseEvents>|공급자가 이벤트에 대한 요청을 추적할 수 있게 합니다.|
|<xref:System.Windows.Automation.Provider.IRawElementProviderHwndOverride>|조각의 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 내에서 창 기반 요소의 위치 변경을 가능하게 합니다.|

<xref:System.Windows.Automation.Provider> 네임스페이스의 다른 모든 인터페이스는 컨트롤 패턴을 지원하는 용도입니다.

<a name="Requirements_for_Non_WPF_Providers"></a>

### <a name="requirements-for-non-wpf-providers"></a>비 WPF 공급자에 대한 요구 사항

[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]와 통신하려면 컨트롤이 다음과 같은 주요 기능 영역을 구현해야 합니다.

|기능|구현|
|-------------------|--------------------|
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|제어 창에 전송된 WM_GETOBJECT 메시지에 대한 응답으로, <xref:System.Windows.Automation.Provider.IRawElementProviderSimple> 을 구현하는 개체(또는 파생된 인터페이스)를 반환합니다. 조각의 경우, 이는 조각 루트에 대한 공급자여야 합니다.|
|속성 값 제공|<xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPropertyValue%2A> 를 구현하여 값을 제공하거나 재정의합니다.|
|클라이언트에서 컨트롤을 조작할 수 있게 설정|<xref:System.Windows.Automation.Provider.IInvokeProvider>와 같은 컨트롤 패턴을 지원하는 인터페이스를 구현합니다. 이러한 패턴 공급자를 <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPatternProvider%2A>구현에서 반환합니다.|
|이벤트 발생|<xref:System.Windows.Automation.Provider.AutomationInteropProvider> 의 정적 메서드 중 하나를 호출하여 클라이언트가 수신할 수 있는 이벤트를 발생시킵니다.|
|조각 내에서 탐색 및 포커스를 사용하도록 설정합니다.|조각 내의 각 요소에 대해 <xref:System.Windows.Automation.Provider.IRawElementProviderFragment> 를 구현합니다. (조각의 포함되지 않은 요소의 경우 필요 없습니다.)|
|조각 내 자식 요소의 포커스 및 위치를 사용하도록 설정합니다.|<xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>를 구현해야 합니다. (조각 루트가 아닌 요소의 경우 필요 없습니다.)|

<a name="Property_Values_in_Non_WPF_Providers"></a>

### <a name="property-values-in-non-wpf-providers"></a>비 WPF 공급자의 속성 값

사용자 지정 컨트롤에 대한[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 공급자는 자동화 시스템뿐만 아니라 클라이언트 응용 프로그램에서도 사용할 수 있는 특정 속성을 지원해야 합니다. 창에서 호스트되는 요소(HWND)의 경우 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 에서는 기본 창 공급자에서 일부 속성을 검색할 수 있지만 다른 일부 속성은 사용자 지정 공급자에서 가져와야 합니다.

HWND 기반 컨트롤에 대한 공급자는 일반적으로 다음 속성(필드 값으로 식별됨)을 제공할 필요가 없습니다.

- <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.ProcessIdProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.ClassNameProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.HasKeyboardFocusProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.IsPasswordProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>

- <xref:System.Windows.Automation.AutomationElementIdentifiers.RuntimeIdProperty>

> [!NOTE]
> 간단한 요소나 창에서 호스트되는 조각 루트의 <xref:System.Windows.Automation.AutomationElementIdentifiers.RuntimeIdProperty> 는 창에서 가져옵니다. 그러나 루트 아래의 조각 요소(예: 목록 상자에 있는 목록 항목)는 고유 식별자를 제공해야 합니다. 자세한 내용은 <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.GetRuntimeId%2A>을 참조하세요.
>
> <xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty> 컨트롤에서 호스트되는 공급자에 대해 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] 를 반환해야 합니다. 이 경우 기본 창 공급자가 올바른 값을 검색하지 못할 수 있습니다.
>
> <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> 는 일반적으로 호스트 공급자가 제공합니다. 예를 들어 사용자 지정 컨트롤이 <xref:System.Windows.Forms.Control>에서 파생된 경우 이름은 컨트롤의 `Text` 속성에서 파생됩니다.

예제 코드를 보려면 [Return Properties from a UI Automation Provider](return-properties-from-a-ui-automation-provider.md)를 참조하세요.

<a name="Events_in_Non_WPF_Providers"></a>

### <a name="events-in-non-wpf-providers"></a>비 WPF 공급자의 이벤트

[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 공급자는 UI 상태 변경 시 이를 클라이언트 응용 프로그램에 알리는 이벤트를 발생시켜야 합니다. 다음 메서드는 이벤트를 발생시키는 데 사용됩니다.

|메서드|설명|
|------------|-----------------|
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.RaiseAutomationEvent%2A>|컨트롤 패턴에 의해 트리거되는 이벤트를 포함하여 다양한 이벤트를 발생시킵니다.|
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.RaiseAutomationPropertyChangedEvent%2A>|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성이 변경되면 이벤트를 발생시킵니다.|
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.RaiseStructureChangedEvent%2A>|예를 들어 요소가 제거되거나 추가되는 등, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리가 변경되면 이벤트를 발생시킵니다.|

이벤트의 목적은 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)]에서 발생하는 상황과 이 활동이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 시스템 자체에서 트리거되는지 여부를 클라이언트에 알리는 것입니다. 예를 들어 <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent> 로 식별되는 이벤트는 직접적인 사용자 입력을 통해서든 아니면 클라이언트 애플리케이션이 <xref:System.Windows.Automation.InvokePattern.Invoke%2A>를 호출해서든 상관없이 컨트롤이 호출될 때마다 발생해야 합니다.

성능을 최적화하기 위해 공급자는 선택적으로 이벤트를 발생시키거나 이벤트 수신을 등록한 클라이언트 애플리케이션이 없는 경우에는 이벤트를 전혀 발생시키지 않을 수 있습니다. 최적화를 위해 다음 메서드가 사용됩니다.

|메서드|설명|
|------------|-----------------|
|<xref:System.Windows.Automation.Provider.AutomationInteropProvider.ClientsAreListening%2A>|이 정적 속성은 클라이언트 애플리케이션이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트를 수신하도록 가입했는지 여부를 지정합니다.|
|<xref:System.Windows.Automation.Provider.IRawElementProviderAdviseEvents>|공급자가 조각 루트에 대해 이 인터페이스를 구현하면 클라이언트가 조각의 이벤트에 대해 이벤트 처리기를 등록하거나 등록 취소할 때 이에 대해 알림을 받을 수 있습니다.|

<a name="Non_WPF_Provider_Navigation"></a>

### <a name="non-wpf-provider-navigation"></a>비 WPF 공급자 탐색

창에서 호스트되는 사용자 지정 단추(HWND)와 같은 간단한 컨트롤의 공급자는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 내의 탐색을 지원할 필요가 없습니다. 요소 및 요소 간 탐색은 호스트 창에 대한 기본 공급자가 처리하며, 이에 대해서는 <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A>구현에서 지정됩니다. 그러나 복잡한 사용자 지정 제어를 위한 공급자를 구현하는 경우에는 조각의 루트 노드와 해당 하위 항목 사이, 그리고 형제 노드 사이의 탐색을 지원해야 합니다.

> [!NOTE]
> 루트 이외의 조각 요소는 창에서 직접 호스트되지 않으며 기본 공급자가 이 요소에 대한 탐색을 지원할 수 없기 때문에 `null` 에서 <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A>참조를 반환해야 합니다.

조각의 구조는 <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.Navigate%2A>의 구현에 따라 결정됩니다. 각 조각에서 가능한 각 방향에 대해, 이 메서드는 해당 방향에 있는 요소에 대한 공급자 개체를 반환합니다. 해당 방향에 요소가 없는 경우 메서드는 `null` 참조를 반환합니다.

조각 루트는 자식 요소에 대해서만 탐색을 지원합니다. 예를 들어 방향이 <xref:System.Windows.Automation.Provider.NavigateDirection.FirstChild>이면 목록 상자는 목록의 첫 번째 항목을 반환하고 방향이 <xref:System.Windows.Automation.Provider.NavigateDirection.LastChild>이면 마지막 항목을 반환합니다. 조각 루트는 부모 또는 형제 항목 탐색을 지원하지 않습니다. 이 작업은 호스트 창 공급자에 의해 처리됩니다.

조각의 루트가 아닌 요소는 부모뿐만 아니라 해당 형제 및 자식 항목에 대해서도 탐색을 지원해야 합니다.

<a name="Non_WPF_Provider_Reparenting"></a>

### <a name="non-wpf-provider-reparenting"></a>비 WPF 공급자 부모 재지정

팝업 창은 실제로 최상위 창이므로 기본적으로 데스크톱의 자식 항목으로 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리에 나타납니다. 그러나 많은 경우, 팝업 창은 논리적으로 다른 일부 컨트롤의 자식 항목입니다. 예를 들어 콤보 상자의 드롭다운 목록은 논리적으로 콤보 상자의 자식 항목입니다. 마찬가지로, 메뉴 팝업 창은 논리적으로 메뉴의 자식 항목입니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 에서는 팝업 창이 관련 컨트롤의 자식 항목으로 보이도록 팝업 창의 부모 재지정을 지원합니다.

팝업 창의 부모를 다시 지정하려면

1. 팝업 창에 대한 공급자를 만듭니다. 그러려면 팝업 창의 클래스를 미리 알고 있어야 합니다.

2. 해당 팝업에 대해 평소와 같이, 고유 권한이 있는 컨트롤처럼 모든 속성과 패턴을 구현합니다.

3. <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A> 에서 가져온 값을 반환하도록 <xref:System.Windows.Automation.Provider.AutomationInteropProvider.HostProviderFromHandle%2A>속성을 구현합니다. 여기서 매개 변수는 팝업 창의 창 핸들입니다.

4. 논리 부모에서 논리 자식으로, 그리고 형제 자식 사이에 탐색이 올바르게 처리되도록 팝업 창 및 해당 상위 항목에 대해 <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.Navigate%2A> 을 구현합니다.

[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서 팝업 창을 발견하면 탐색이 기본값에서 재정의된다는 것을 인식하며 데스크톱의 자식 항목으로 발견된 경우에는 팝업 창으로 건너뜁니다. 대신, 조각을 통해서만 노드에 도달할 수 있습니다.

부모 재지정은 컨트롤이 클래스의 창을 호스트할 수 있는 경우에는 적합하지 않습니다. 예를 들어 rebar는 모든 유형의 HWND를 밴드에서 호스트할 수 있습니다. 이런 경우를 처리하기 위해 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 에서는 다음 섹션의 설명대로 다른 형식의 HWND 재배치를 지원합니다.

<a name="Non_WPF_Provider_Repositioning"></a>

### <a name="non-wpf-provider-repositioning"></a>비 WPF 공급자 위치 변경

[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 조각은 각각 창에 포함된 두 개 이상의 항목(HWND)을 포함할 수 있습니다. 각 HWND에는 HWND를 이를 포함하는 HWND의 자식으로 간주하는 고유한 기본 공급자가 있기 때문에, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리는 기본적으로 조각에 있는 HWND를 부모 창의 자식 항목으로 표시합니다. 대부분의 경우 이것은 바람직한 동작이지만, 때로는 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]의 논리 구조와 일치하지 않기 때문에 혼란을 일으킬 수 있습니다.

그 좋은 예가 rebar 컨트롤입니다. rebar에는 밴드가 있고, 각 밴드에는 도구 모음, 편집 상자, 콤보 상자와 같은 HWND 기반 컨트롤이 있을 수 있습니다. rebar HWND에 대한 기본 창 공급자는 밴드 컨트롤 HWND를 자식으로 간주하고, rebar 공급자는 밴드를 자식으로 간주합니다. HWND 공급자 및 rebar 공급자는 함께 작업하며 각 자식 항목을 결합하기 때문에 밴드와 HWND 기반 컨트롤이 모두 rebar의 자식으로 나타납니다. 그러나 논리적으로는 밴드만 rebar의 자식으로 나타나야 하며 각 밴드 공급자는 포함된 컨트롤에 대한 기본 HWND 공급자와 연결되어야 합니다.

이를 위해 rebar에 대한 조각 루트 공급자는 밴드는 나타내는 일련의 자식 항목을 노출합니다. 각 밴드에는 속성 및 패턴을 노출할 수 있는 단일 공급자가 있습니다. <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.HostRawElementProvider%2A>구현에서 밴드 공급자는 <xref:System.Windows.Automation.Provider.AutomationInteropProvider.HostProviderFromHandle%2A>호출 후 컨트롤의 창 핸들에 전달하여 가져온 컨트롤 HWND에 대한 기본 창 공급자를 반환합니다. 마지막으로, rebar에 대한 조각 루트 공급자는 <xref:System.Windows.Automation.Provider.IRawElementProviderHwndOverride> 인터페이스를 구현하고 <xref:System.Windows.Automation.Provider.IRawElementProviderHwndOverride.GetOverrideProviderForHwnd%2A> 구현에서 지정된 HWND에 포함된 컨트롤에 적절한 밴드 공급자를 반환합니다.

## <a name="see-also"></a>참고자료

- [UI 자동화 공급자 개요](ui-automation-providers-overview.md)
- [서버 쪽 UI 자동화 공급자 노출](expose-a-server-side-ui-automation-provider.md)
- [UI 자동화 공급자에서 속성 반환](return-properties-from-a-ui-automation-provider.md)
- [UI 자동화 공급자에서 이벤트 발생](raise-events-from-a-ui-automation-provider.md)
- [UI 자동화 조각 공급자에서 탐색 사용](enable-navigation-in-a-ui-automation-fragment-provider.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
