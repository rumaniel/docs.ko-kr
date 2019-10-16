---
title: UI 자동화 및 Microsoft Active Accessibility
ms.date: 03/30/2017
helpviewer_keywords:
- Active Accessibility
- UI Automation, Active Accessibility compared to
- UI Automation, Microsoft Active Accessibility
- Active Accessibility, UI Automation compared to
ms.assetid: 87bee662-0a3e-4232-a421-20e7a5968321
ms.openlocfilehash: 63b00f8eb35fa58ea0257d5e996fc2c51a248040
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042591"
---
# <a name="ui-automation-and-microsoft-active-accessibility"></a>UI 자동화 및 Microsoft Active Accessibility
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Microsoft Active Accessibility는 응용 프로그램에 액세스할 수 있도록 하기 위한 이전 솔루션 이었습니다. [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 은 [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] 의 새로운 접근성 모델로서 보조 기술 제품 및 자동 테스트 도구의 요구를 충족시키기 위한 것입니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]는 Active Accessibility에 비해 많은 향상 된 기능을 제공 합니다.  
  
 이 항목에서는의 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 주요 기능에 대해 설명 하며 이러한 기능이 Active Accessibility와 어떻게 다른 지 설명 합니다.  
  
<a name="Programming_Languages_compare"></a>   
## <a name="programming-languages"></a>프로그래밍 언어  
< Active Accessibility는 이중 인터페이스를 지 원하는 COM (구성 요소 개체 모델)을 기반으로 하므로 C/C++, [!INCLUDE[TLA#tla_vb6](../../../includes/tlasharptla-vb6-md.md)]및 스크립팅 언어로 프로그래밍 가능 합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)](표준 컨트롤에 대 한 클라이언트 쪽 공급자 라이브러리 포함)는 관리 코드로 작성 되며, 또는 Visual Basic .NET을 사용 하 여 C# UI 자동화 클라이언트 응용 프로그램을 가장 쉽게 프로그래밍할 수 있습니다. 인터페이스 구현인 UI 자동화 공급자는 관리되는 코드 또는 C/C++로 작성할 수 있습니다.  
  
<a name="Support_in_Windows_Presentation_Foundation_"></a>   
## <a name="support-in-windows-presentation-foundation"></a>Windows Presentation Foundation에서의 지원  
 WPF (Windows Presentation Foundation)는 사용자 인터페이스를 만들기 위한 새 모델입니다. [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]요소에는 Active Accessibility에 대 한 기본 지원이 포함 되지 않습니다. 그러나 Active Accessibility 클라이언트에 대 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]한 브리징 지원이 포함 된을 지원 합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 에 대해 특별히 작성된 클라이언트만 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]의 접근성 기능(예: 다양한 텍스트 지원)을 활용할 수 있습니다.  
  
<a name="Servers_and_Clients_compare"></a>   
## <a name="servers-and-clients"></a>서버 및 클라이언트  
 Active Accessibility 서버와 클라이언트는 대부분의 `IAccessible`서버 구현을 통해 직접 통신 합니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, 핵심 서비스는 서버(공급자라고 함)와 클라이언트 사이에 있습니다. 핵심 서비스 공급자는 공급자가 구현한 인터페이스를 호출하고, 요소에 대한 고유한 런타임 식별자 생성 등과 같은 추가적인 서비스를 제공합니다. 클라이언트 애플리케이션은  라이브러리 함수를 사용하여 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 서비스를 호출합니다.  
  
 UI 자동화 공급자는 Active Accessibility 클라이언트에 대 한 정보를 제공할 수 있으며 Active Accessibility 서버는 UI 자동화 클라이언트 응용 프로그램에 정보를 제공할 수 있습니다. 그러나 Active Accessibility는 만큼 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]많은 정보를 노출 하지 않기 때문에 두 모델이 완전히 호환 되지 않습니다.  
  
<a name="UI_Elements_compare"></a>   
## <a name="ui-elements"></a>UI 요소  
 Active Accessibility는 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] `IAccessible` 요소를 인터페이스 또는 자식 식별자로 표시 합니다. 두 `IAccessible` 포인터를 비교하여 동일한 요소를 참조하는지 확인하기는 어렵습니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, 모든 요소는 <xref:System.Windows.Automation.AutomationElement> 개체로 표시됩니다. 요소의 고유한 런타임 식별자를 비교하는 같음 연산자 또는 <xref:System.Windows.Automation.AutomationElement.Equals%2A> 메서드를 사용하여 비교합니다.  
  
<a name="Tree_Views_and_Navigation_compare"></a>   
## <a name="tree-views-and-navigation"></a>트리 뷰 및 탐색  
 화면의 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 요소는 데스크톱이 루트, 애플리케이션 창이 직계 자식, 애플리케이션 내의 요소가 추가적인 하위 항목인 트리 구조로 표시될 수 있습니다.  
  
 Active Accessibility 최종 사용자와 관련이 없는 많은 자동화 요소가 트리에 노출 됩니다. 클라이언트 애플리케이션은 모든 요소를 확인하여 의미 있는 요소를 파악해야 합니다.  
  
 UI 자동화 클라이언트 애플리케이션은 필터링된 뷰를 통해 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 를 표시합니다. 이 뷰에는 사용자에게 정보를 제공하거나 상호 작용을 활성화하는 등 필요한 요소만 포함됩니다. 컨트롤 요소만 미리 정의된 뷰와 콘텐츠 요소만 미리 정의된 뷰를 사용할 수 있습니다. 또한 애플리케이션이 사용자 지정 뷰를 정의할 수 있습니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 은 사용자에게 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 를 설명하고 응용 프로그램과 상호 작용할 수 있도록 도와주는 작업을 간소화합니다.  
  
 Active Accessibility에서 요소 간의 탐색은 공간 (예: 화면 왼쪽에 있는 요소로 이동), 논리적 (예: 다음 메뉴 항목으로 이동 또는 대화 상자 내에서 탭 순서의 다음 항목으로 이동), 계층적 ( 예를 들어 컨테이너의 첫 번째 자식 또는 자식에서 부모로 이동 합니다. 계층적 탐색의 경우, 자식 요소가 `IAccessible`을 구현하는 개체가 아닐 수도 있기 때문에 복잡한 방법입니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, 모든 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 요소는 동일한 기본 기능을 지원하는 <xref:System.Windows.Automation.AutomationElement> 개체입니다. (공급자의 관점에서 보면 이 개체는 <xref:System.Windows.Automation.Provider.IRawElementProviderSimple>에서 상속된 인터페이스를 구현하는 개체입니다.) 탐색은 주로 계층 구조입니다. 부모에서 자식으로, 한 형제에서 다른 형제로 탐색합니다. (형제 간 탐색은 탭 순서를 따를 수 있기 때문에 논리적 요소가 있습니다.) <xref:System.Windows.Automation.TreeWalker> 클래스를 사용하여 트리의 필터링된 뷰를 통해 시작점에서 탐색할 수 있습니다. <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> 및 <xref:System.Windows.Automation.AutomationElement.FindAll%2A>을 사용하여 특정 자식 또는 하위 항목을 탐색할 수도 있습니다. 예를 들어, 지정된 컨트롤 패턴을 지원하는 대화 상자 내에서 모든 요소를 쉽게 검색할 수 있습니다.  
  
 에서의 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 탐색은 Active Accessibility 보다 더 일관적입니다. 드롭다운 목록 및 팝업 창과 같은 일부 요소는 Active Accessibility 트리에 두 번 나타나며, 이러한 요소를 탐색 하면 예기치 않은 결과가 발생할 수 있습니다. 크기 조정 컨트롤에 대 한 Active Accessibility를 올바르게 구현 하는 것은 실제로 불가능 합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 을 사용하면 부모 재지정 및 위치 변경이 가능하므로, 창 소유권에 의해 계층 구조가 적용되더라도 트리에서 요소를 원하는 위치에 배치할 수 있습니다.  
  
<a name="Roles_and_Control_Types"></a>   
## <a name="roles-and-control-types"></a>역할 및 컨트롤 형식  
 Active Accessibility는 `accRole` 속성 (`IAccessible::get_actRole`)을 사용 하 여 ROLE_SYSTEM_SLIDER 또는 ROLE_SYSTEM_MENUITEM와 같은에서 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]요소 역할에 대 한 설명을 검색 합니다. 요소의 역할을 통해 사용 가능한 기능을 알 수 있습니다. `IAccessible::accSelect` 및 `IAccessible::accDoDefaultAction`과 같은 고정 메서드를 사용하여 컨트롤과 상호 작용할 수 있습니다. 클라이언트 애플리케이션과 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 간의 상호 작용은 `IAccessible`을 통해서 수행할 수 있는 작업으로 제한됩니다.  
  
 한편, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 은 주로 예상 기능에서 요소의 컨트롤 형식( <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ControlType%2A> 속성으로 설명됨)을 분리합니다. 기능은 특수화된 인터페이스의 구현을 통해 공급자가 지원하는 컨트롤 패턴에 의해 결정됩니다. 컨트롤 패턴을 조합하여 특정 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 요소가 지원하는 전체 기능 집합을 설명할 수 있습니다. 일부 공급자는 특정 컨트롤 패턴을 지원하는 데 필요합니다. 예를 들어, 확인란에 대한 공급자는 Toggle 컨트롤 패턴을 지원해야 합니다. 기타 공급자는 하나 이상의 컨트롤 패턴 집합을 지원하는 데 필요합니다. 예를 들어, 단추는 Toggle 또는 Invoke를 지원해야 합니다. 컨트롤 패턴을 지원하지 않는 공급자도 있습니다. 예를 들어 이동, 크기 조정 또는 도킹할 수 없는 창에는 컨트롤 패턴이 없습니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 은 <xref:System.Windows.Automation.ControlType.Custom> 속성으로 식별되고 <xref:System.Windows.Automation.AutomationElement.LocalizedControlTypeProperty> 속성으로 설명할 수 있는 사용자 지정 컨트롤을 지원합니다.  
  
 다음 표에서는 Active Accessibility 역할을 컨트롤 형식으로 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 매핑하는 방법을 보여 줍니다.  
  
|Active Accessibility 역할|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 컨트롤 형식|  
|----------------------------------------------------------------------|----------------------------------------------------------------------------------------|  
|ROLE_SYSTEM_PUSHBUTTON|단추|  
|ROLE_SYSTEM_CLIENT|일정|  
|ROLE_SYSTEM_CHECKBUTTON|확인란|  
|ROLE_SYSTEM_COMBOBOX|콤보 상자|  
|ROLE_SYSTEM_CLIENT|사용자 지정|  
|ROLE_SYSTEM_LIST|데이터 표|  
|ROLE_SYSTEM_LISTITEM|데이터 항목|  
|ROLE_SYSTEM_DOCUMENT|문서|  
|ROLE_SYSTEM_TEXT|편집|  
|ROLE_SYSTEM_GROUPING|그룹화|  
|ROLE_SYSTEM_LIST|헤더|  
|ROLE_SYSTEM_COLUMNHEADER|헤더 항목|  
|ROLE_SYSTEM_LINK|하이퍼링크|  
|ROLE_SYSTEM_GRAPHIC|이미지|  
|ROLE_SYSTEM_LIST|목록|  
|ROLE_SYSTEM_LISTITEM|목록 항목|  
|ROLE_SYSTEM_MENUPOPUP|메뉴|  
|ROLE_SYSTEM_MENUBAR|메뉴 모음|  
|ROLE_SYSTEM_MENUITEM|Menu item|  
|ROLE_SYSTEM_PANE|창|  
|ROLE_SYSTEM_PROGRESSBAR|진행률 표시줄|  
|ROLE_SYSTEM_RADIOBUTTON|라디오 단추|  
|ROLE_SYSTEM_SCROLLBAR|스크롤 막대|  
|ROLE_SYSTEM_SEPARATOR|구분 기호|  
|ROLE_SYSTEM_SLIDER|슬라이더|  
|ROLE_SYSTEM_SPINBUTTON|Spinner|  
|ROLE_SYSTEM_SPLITBUTTON|분할 단추|  
|ROLE_SYSTEM_STATUSBAR|상태 표시줄|  
|ROLE_SYSTEM_PAGETABLIST|탭|  
|ROLE_SYSTEM_PAGETAB|탭 항목|  
|ROLE_SYSTEM_TABLE|표|  
|ROLE_SYSTEM_STATICTEXT|텍스트|  
|ROLE_SYSTEM_INDICATOR|Thumb|  
|ROLE_SYSTEM_TITLEBAR|제목 표시줄|  
|ROLE_SYSTEM_TOOLBAR|도구 모음|  
|ROLE_SYSTEM_TOOLTIP|도구 설명|  
|ROLE_SYSTEM_OUTLINE|Tree|  
|ROLE_SYSTEM_OUTLINEITEM|트리 항목|  
|ROLE_SYSTEM_WINDOW|창|  
  
 다른 컨트롤 형식에 대한 자세한 내용은 [UI Automation Control Types](ui-automation-control-types.md)을 참조하세요.  
  
<a name="States_and_Properties"></a>   
## <a name="states-and-properties"></a>상태 및 속성  
 Active Accessibility에서 요소는 일반적인 속성 집합을 지원 하며,와 `accState`같은 일부 속성은 요소의 역할에 따라 매우 다른 작업을 설명 해야 합니다. 서버는 요소와 관련이 없더라도 속성을 반환하는 `IAccessible` 의 모든 메서드를 구현해야 합니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]은 더 많은 속성을 정의 하며, 그 중 일부는 Active Accessibility의 상태에 해당 합니다. 일부 속성은 모든 요소에 공통되지만 컨트롤 형식과 컨트롤 패턴에만 관련된 속성도 있습니다. 속성은 고유한 식별자로 구분되며, 대부분의 속성은 단일 메서드 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A> 또는 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A>를 사용하여 검색할 수 있습니다. <xref:System.Windows.Automation.AutomationElement.Current%2A> 및 <xref:System.Windows.Automation.AutomationElement.Cached%2A> 속성 접근자에서 다양한 속성을 쉽게 검색할 수도 있습니다.  
  
 UI 자동화 공급자는 관련이 없는 속성을 구현할 필요가 없지만 지원하지 않는 속성에 대해 `null` 값을 반환할 수 있습니다. 또한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 핵심 서비스는 기본 창 공급자에서 일부 속성을 가져올 수 있으며, 이러한 속성은 공급자가 명시적으로 구현하는 속성과 병합됩니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 는 기타 여러 속성을 지원하는 것 이외에도 하나의 프로세스 간 호출로 여러 속성을 검색할 수 있도록 허용하여 더 높은 성능을 제공합니다.  
  
 다음 표는 두 모델에서 속성 간의 상관 관계를 보여줍니다.  
  
|Active Accessibility 속성 접근자|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 ID|설명|  
|-----------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|-------------|  
|`get_accKeyboardShortcut`|<xref:System.Windows.Automation.AutomationElement.AccessKeyProperty> 또는 <xref:System.Windows.Automation.AutomationElement.AcceleratorKeyProperty>|둘 다 있는 경우`AccessKeyProperty` 가 우선적으로 적용됩니다.|  
|`get_accName`|<xref:System.Windows.Automation.AutomationElement.NameProperty>||  
|`get_accRole`|<xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>|컨트롤 형식에 대한 역할 매핑은 이전 표를 참조하세요.|  
|`get_accValue`|<xref:System.Windows.Automation.ValuePattern.ValueProperty?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Automation.RangeValuePattern.ValueProperty?displayProperty=nameWithType>|ValuePattern 또는 RangeValuePattern을 지원하는 컨트롤 형식에만 유효합니다. RangeValue 값은 MSAA 동작과 일관되도록 0-100으로 정규화됩니다. 값 항목은 문자열을 사용합니다.|  
|`get_accHelp`|<xref:System.Windows.Automation.AutomationElement.HelpTextProperty>||  
|`accLocation`|<xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty>||  
|`get_accDescription`|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|`accDescription` 은 MSAA 내에서 명확한 사양이 없기 때문에, 공급자가 이 속성에 다양한 정보를 배치합니다.|  
|`get_accHelpTopic`|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]||  
  
 다음 표에서는 Active Accessibility 상태 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 상수에 해당 하는 속성을 보여 줍니다.  
  
|Active Accessibility 상태|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성|상태 변경 트리거 여부|  
|-----------------------------------------------------------------------|------------------------------------------------------------------------------------|----------------------------|  
|STATE_SYSTEM_CHECKED|확인란의 경우, <xref:System.Windows.Automation.TogglePattern.ToggleStateProperty><br /><br /> 라디오 단추의 경우, <xref:System.Windows.Automation.SelectionItemPattern.IsSelectedProperty>|Y|  
|STATE_SYSTEM_COLLAPSED|<xref:System.Windows.Automation.ExpandCollapsePattern.ExpandCollapsePatternInformation.ExpandCollapseState%2A> = <xref:System.Windows.Automation.ExpandCollapseState.Collapsed>|Y|  
|STATE_SYSTEM_EXPANDED|<xref:System.Windows.Automation.ExpandCollapsePattern.ExpandCollapsePatternInformation.ExpandCollapseState%2A> = <xref:System.Windows.Automation.ExpandCollapseState.Expanded> 또는 <xref:System.Windows.Automation.ExpandCollapseState.PartiallyExpanded>|Y|  
|STATE_SYSTEM_FOCUSABLE|<xref:System.Windows.Automation.AutomationElement.IsKeyboardFocusableProperty>|N|  
|STATE_SYSTEM_FOCUSED|<xref:System.Windows.Automation.AutomationElement.HasKeyboardFocusProperty>|N|  
|STATE_SYSTEM_HASPOPUP|메뉴 항목에 대해<xref:System.Windows.Automation.ExpandCollapsePattern>|N|  
|STATE_SYSTEM_INVISIBLE|<xref:System.Windows.Automation.AutomationElement.IsOffscreenProperty> = True이며 <xref:System.Windows.Automation.AutomationElement.GetClickablePoint%2A> 가 <xref:System.Windows.Automation.NoClickablePointException>|N|  
|STATE_SYSTEM_LINKED|<xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> =<br /><br /> <xref:System.Windows.Automation.ControlType.Hyperlink>|N|  
|STATE_SYSTEM_MIXED|<xref:System.Windows.Automation.TogglePattern.TogglePatternInformation.ToggleState%2A> = <xref:System.Windows.Automation.ToggleState.Indeterminate>|N|  
|STATE_SYSTEM_MOVEABLE|<xref:System.Windows.Automation.TransformPattern.CanMoveProperty>|N|  
|STATE_SYSTEM_MUTLISELECTABLE|<xref:System.Windows.Automation.SelectionPattern.CanSelectMultipleProperty>|N|  
|STATE_SYSTEM_OFFSCREEN|<xref:System.Windows.Automation.AutomationElement.IsOffscreenProperty> = True|N|  
|STATE_SYSTEM_PROTECTED|<xref:System.Windows.Automation.AutomationElement.IsPasswordProperty>|N|  
|STATE_SYSTEM_READONLY|<xref:System.Windows.Automation.RangeValuePattern.IsReadOnlyProperty?displayProperty=nameWithType> 및 <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty?displayProperty=nameWithType>|N|  
|STATE_SYSTEM_SELECTABLE|<xref:System.Windows.Automation.SelectionItemPattern> 이 지원됨|N|  
|STATE_SYSTEM_SELECTED|<xref:System.Windows.Automation.SelectionItemPattern.IsSelectedProperty>|N|  
|STATE_SYSTEM_SIZEABLE|<xref:System.Windows.Automation.TransformPattern.TransformPatternInformation.CanResize%2A>|N|  
|STATE_SYSTEM_UNAVAILABLE|<xref:System.Windows.Automation.AutomationElement.IsEnabledProperty>|Y|  
  
 다음 상태는 대부분의 Active Accessibility 제어 서버에서 구현 되지 않았거나에 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]해당 항목이 없습니다.  
  
|Active Accessibility 상태|설명|  
|-----------------------------------------------------------------------|-------------|  
|STATE_SYSTEM_BUSY|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|  
|STATE_SYSTEM_DEFAULT|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|  
|STATE_SYSTEM_ANIMATED|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|  
|STATE_SYSTEM_EXTSELECTABLE|Active Accessibility 서버에서 폭넓게 구현 되지 않음|  
|STATE_SYSTEM_MARQUEED|Active Accessibility 서버에서 폭넓게 구현 되지 않음|  
|STATE_SYSTEM_SELFVOICING|Active Accessibility 서버에서 폭넓게 구현 되지 않음|  
|STATE_SYSTEM_TRAVERSED|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|  
|STATE_SYSTEM_ALERT_HIGH|Active Accessibility 서버에서 폭넓게 구현 되지 않음|  
|STATE_SYSTEM_ALERT_MEDIUM|Active Accessibility 서버에서 폭넓게 구현 되지 않음|  
|STATE_SYSTEM_ALERT_LOW|Active Accessibility 서버에서 폭넓게 구현 되지 않음|  
|STATE_SYSTEM_FLOATING|Active Accessibility 서버에서 폭넓게 구현 되지 않음|  
|STATE_SYSTEM_HOTTRACKED|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|  
|STATE_SYSTEM_PRESSED|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|  
  
 속성 식별자의 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 전체 목록은 [UI 자동화 속성 개요](ui-automation-properties-overview.md)를 참조 하세요.  
  
<a name="uiautomation_events_compare"></a>   
## <a name="events"></a>이벤트  
 Active Accessibility와 달리의 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]이벤트 메커니즘은 Windows 이벤트 라우팅 (창 핸들과 밀접 하 게 연결)을 사용 하지 않으며 후크를 설정 하는 데 클라이언트 응용 프로그램이 필요 하지 않습니다. 이벤트에 대한 구독은 특정 이벤트뿐만 아니라 트리의 특정 부분에 대해서도 미세하게 조정할 수 있습니다. 공급자는 이벤트가 수신 대기하고 있는 사항을 추적하여 이벤트 발생을 미세 조정할 수 있습니다.  
  
 요소가 이벤트 콜백에 직접 전달되므로 클라이언트는 이벤트를 발생하는 요소를 쉽게 검색할 수 있습니다. 클라이언트가 이벤트를 구독할 때 캐시 요청이 활성화되어 있으면 요소의 속성이 자동으로 프리페치됩니다.  
  
 다음 표에서는 Active Accessibility winevents 및 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트의 상관 관계를 보여 줍니다.  
  
|WinEvent|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이벤트 식별자|  
|--------------|--------------------------------------------------------------------------------------------|  
|EVENT_OBJECT_ACCELERATORCHANGE|<xref:System.Windows.Automation.AutomationElement.AcceleratorKeyProperty> 속성 변경|  
|EVENT_OBJECT_CONTENTSCROLLED|연결된 스크롤 막대의<xref:System.Windows.Automation.ScrollPattern.VerticalScrollPercentProperty> 또는 <xref:System.Windows.Automation.ScrollPattern.HorizontalScrollPercentProperty> 속성 변경|  
|EVENT_OBJECT_CREATE|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT_OBJECT_DEFACTIONCHANGE|동일한 요소 없음|  
|EVENT_OBJECT_DESCRIPTIONCHANGE|정확하게 해당하는 요소가 없습니다. <xref:System.Windows.Automation.AutomationElement.HelpTextProperty> 또는 <xref:System.Windows.Automation.AutomationElement.LocalizedControlTypeProperty> 속성 변경이 이에 해당할 수 있습니다.|  
|EVENT_OBJECT_DESTROY|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT_OBJECT_FOCUS|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent>|  
|EVENT_OBJECT_HELPCHANGE|<xref:System.Windows.Automation.AutomationElement.HelpTextProperty> 변경|  
|EVENT_OBJECT_HIDE|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT_OBJECT_LOCATIONCHANGE|<xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty> 속성 변경|  
|EVENT_OBJECT_NAMECHANGE|<xref:System.Windows.Automation.AutomationElement.NameProperty> 속성 변경|  
|EVENT_OBJECT_PARENTCHANGE|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT_OBJECT_REORDER|Active Accessibility에서 일관 되 게 사용 되지 않습니다. 직접적인 해당 이벤트가 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에 정의되지 않았습니다.|  
|EVENT_OBJECT_SELECTION|<xref:System.Windows.Automation.SelectionItemPattern.ElementSelectedEvent>|  
|EVENT_OBJECT_SELECTIONADD|<xref:System.Windows.Automation.SelectionItemPattern.ElementAddedToSelectionEvent>|  
|EVENT_OBJECT_SELECTIONREMOVE|<xref:System.Windows.Automation.SelectionItemPattern.ElementRemovedFromSelectionEvent>|  
|EVENT_OBJECT_SELECTIONWITHIN|동일한 요소 없음|  
|EVENT_OBJECT_SHOW|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|  
|EVENT_OBJECT_STATECHANGE|다양한 속성 변경 이벤트|  
|EVENT_OBJECT_VALUECHANGE|<xref:System.Windows.Automation.RangeValuePattern.ValueProperty?displayProperty=nameWithType> 및 <xref:System.Windows.Automation.ValuePattern.ValueProperty?displayProperty=nameWithType> 변경|  
|EVENT_SYSTEM_ALERT|동일한 요소 없음|  
|EVENT_SYSTEM_CAPTUREEND|동일한 요소 없음|  
|EVENT_SYSTEM_CAPTURESTART|동일한 요소 없음|  
|EVENT_SYSTEM_CONTEXTHELPEND|동일한 요소 없음|  
|EVENT_SYSTEM_CONTEXTHELPSTART|동일한 요소 없음|  
|EVENT_SYSTEM_DIALOGEND|<xref:System.Windows.Automation.WindowPattern.WindowClosedEvent>|  
|EVENT_SYSTEM_DIALOGSTART|<xref:System.Windows.Automation.WindowPattern.WindowOpenedEvent>|  
|EVENT_SYSTEM_DRAGDROPEND|동일한 요소 없음|  
|EVENT_SYSTEM_DRAGDROPSTART|동일한 요소 없음|  
|EVENT_SYSTEM_FOREGROUND|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent>|  
|EVENT_SYSTEM_MENUEND|<xref:System.Windows.Automation.AutomationElement.MenuClosedEvent>|  
|EVENT_SYSTEM_MENUPOPUPEND|<xref:System.Windows.Automation.AutomationElement.MenuClosedEvent>|  
|EVENT_SYSTEM_MENUPOPUPSTART|<xref:System.Windows.Automation.AutomationElement.MenuOpenedEvent>|  
|EVENT_SYSTEM_MENUSTART|<xref:System.Windows.Automation.AutomationElement.MenuOpenedEvent>|  
|EVENT_SYSTEM_MINIMIZEEND|<xref:System.Windows.Automation.WindowPattern.WindowVisualStateProperty> 속성 변경|  
|EVENT_SYSTEM_MINIMIZESTART|<xref:System.Windows.Automation.WindowPattern.WindowVisualStateProperty> 속성 변경|  
|EVENT_SYSTEM_MOVESIZEEND|<xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty> 속성 변경|  
|EVENT_SYSTEM_MOVESIZESTART|<xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty> 속성 변경|  
|EVENT_SYSTEM_SCROLLINGEND|<xref:System.Windows.Automation.ScrollPattern.VerticalScrollPercentProperty> or <xref:System.Windows.Automation.ScrollPattern.HorizontalScrollPercentProperty> 속성 변경|  
|EVENT_SYSTEM_SCROLLINGSTART|<xref:System.Windows.Automation.ScrollPattern.VerticalScrollPercentProperty> or <xref:System.Windows.Automation.ScrollPattern.HorizontalScrollPercentProperty> 속성 변경|  
|EVENT_SYSTEM_SOUND|동일한 요소 없음|  
|EVENT_SYSTEM_SWITCHEND|동일한 요소가 없지만 <xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent> 이벤트는 새 애플리케이션이 포커스를 받았음을 신호로 알립니다.|  
|EVENT_SYSTEM_SWITCHSTART|동일한 요소 없음|  
|동일한 요소 없음|<xref:System.Windows.Automation.MultipleViewPattern.CurrentViewProperty> 속성 변경|  
|동일한 요소 없음|<xref:System.Windows.Automation.ScrollPattern.HorizontallyScrollableProperty> 속성 변경|  
|동일한 요소 없음|<xref:System.Windows.Automation.ScrollPattern.VerticallyScrollableProperty> 속성 변경|  
|동일한 요소 없음|<xref:System.Windows.Automation.ScrollPattern.HorizontalScrollPercentProperty> 속성 변경|  
|동일한 요소 없음|<xref:System.Windows.Automation.ScrollPattern.VerticalScrollPercentProperty> 속성 변경|  
|동일한 요소 없음|<xref:System.Windows.Automation.ScrollPattern.HorizontalViewSizeProperty> 속성 변경|  
|동일한 요소 없음|<xref:System.Windows.Automation.ScrollPattern.VerticalViewSizeProperty> 속성 변경|  
|동일한 요소 없음|<xref:System.Windows.Automation.TogglePattern.ToggleStateProperty> 속성 변경|  
|동일한 요소 없음|<xref:System.Windows.Automation.WindowPattern.WindowVisualStateProperty> 속성 변경|  
|동일한 요소 없음|<xref:System.Windows.Automation.AutomationElement.AsyncContentLoadedEvent> 이벤트|  
|동일한 요소 없음|<xref:System.Windows.Automation.AutomationElement.ToolTipOpenedEvent>|  
  
<a name="Security_compare"></a>   
## <a name="security"></a>보안  
 일부 `IAccessible` 사용자 지정 시나리오에서는 기본 `IAccessible` 의 줄바꿈과 이를 호출해야 합니다. 부분적으로 신뢰할 수 있는 구성 요소는 코드 경로에 중간자로 사용할 수 없기 때문에 보안에 영향을 줍니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 모델에서는 다른 공급자 코드를 통해 호출하는 데 공급자가 필요하지 않습니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 핵심 서비스는 필요한 모든 집계를 수행합니다.  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 기본 사항](index.md)
