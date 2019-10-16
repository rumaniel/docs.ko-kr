---
title: 클라이언트의 UI 자동화 속성
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties, UI Automation clients
- UI Automation, client properties
ms.assetid: 255905af-0b17-485c-93d4-8a2db2a6524b
ms.openlocfilehash: 9c92ea154a078ff5a059edd82f06b8f3d5bab239
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042128"
---
# <a name="ui-automation-properties-for-clients"></a>클라이언트의 UI 자동화 속성
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 개요에서는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성이 UI 자동화 클라이언트 애플리케이션에 노출될 때 이 속성에 대해 설명합니다.  
  
 <xref:System.Windows.Automation.AutomationElement> 개체의 속성에는 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 요소에 대한 정보가 포함됩니다(일반적으로 컨트롤). <xref:System.Windows.Automation.AutomationElement> 의 속성은 제네릭으로서 컨트롤 형식과 관련되지 않습니다. 이러한 속성 중 대부분은 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation> 구조로 노출됩니다.  
  
 컨트롤 패턴에는 속성도 있습니다. 컨트롤 패턴의 속성은 패턴에 따라 다릅니다. 예를 들어, <xref:System.Windows.Automation.ScrollPattern> 에는 클라이언트 애플리케이션이 창을 가로 또는 세로로 스크롤할 수 있는지와 현재 뷰 크기 및 스크롤 위치를 확인할 수 있는 속성이 있습니다. 컨트롤 패턴은 구조를 통해 모든 속성을 노출합니다(예: <xref:System.Windows.Automation.ScrollPattern.ScrollPatternInformation>).  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성이 읽기 전용입니다. 컨트롤의 속성을 설정하려면 적절한 컨트롤 패턴의 메서드를 사용해야 합니다. 예를 들어, 스크롤 창의 위치 값을 변경하려면 <xref:System.Windows.Automation.ScrollPattern.Scroll%2A> 를 사용합니다.  
  
 성능 향상을 위해 <xref:System.Windows.Automation.AutomationElement> 개체가 검색될 때 컨트롤 및 컨트롤 패턴의 속성 값을 캐시할 수 있습니다. 자세한 내용은 [UI 자동화 클라이언트에서 캐싱](caching-in-ui-automation-clients.md)을 참조 하세요.  
  
## <a name="property-ids"></a>속성 ID  
 Id (속성 식별자)는 개체에서 <xref:System.Windows.Automation.AutomationProperty> 캡슐화 되는 고유한 상수 값입니다. UI 자동화 클라이언트 응용 프로그램은 <xref:System.Windows.Automation.AutomationElement> 클래스 또는와 <xref:System.Windows.Automation.ScrollPattern>같은 적절 한 컨트롤 패턴 클래스에서 이러한 id를 가져옵니다. UI 자동화 공급자는 이러한 ID를 <xref:System.Windows.Automation.AutomationElementIdentifiers> 또는 <xref:System.Windows.Automation.ScrollPatternIdentifiers>와 같은 컨트롤 패턴 식별자 클래스 중 하나에서 가져옵니다.  
  
 <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> 의 <xref:System.Windows.Automation.AutomationProperty> 숫자는 공급자가 <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPropertyValue%2A?displayProperty=nameWithType> 메서드에서 쿼리되는 속성을 식별하는 데 사용됩니다. 일반적으로 클라이언트 애플리케이션은 <xref:System.Windows.Automation.AutomationIdentifier.Id%2A>를 검사할 필요가 없습니다. <xref:System.Windows.Automation.AutomationIdentifier.ProgrammaticName%2A> 은 디버깅 및 진단 용도로만 사용됩니다.  
  
## <a name="property-conditions"></a>속성 조건  
 속성 id는 개체를 찾는 <xref:System.Windows.Automation.PropertyCondition> <xref:System.Windows.Automation.AutomationElement> 데 사용 되는 개체를 생성 하는 데 사용 됩니다. 예를 들어, 특정 이름의 <xref:System.Windows.Automation.AutomationElement> 를 찾거나 활성화된 모든 컨트롤을 찾을 수 있습니다. 각 <xref:System.Windows.Automation.PropertyCondition> 은 속성과 일치해야 하는 <xref:System.Windows.Automation.AutomationProperty> 식별자 및 값을 지정합니다.  
  
 자세한 내용은 다음 참조 항목을 참조하세요.  
  
- <xref:System.Windows.Automation.AutomationElement.FindFirst%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.FindAll%2A>  
  
- <xref:System.Windows.Automation.TreeWalker.Condition%2A>  
  
## <a name="retrieving-properties"></a>속성 검색  
 <xref:System.Windows.Automation.AutomationElement> 의 일부 속성 및 컨트롤 패턴 클래스의 모든 속성은 `Current` 또는 컨트롤 패턴 개체의 `Cached` 또는 <xref:System.Windows.Automation.AutomationElement> 속성의 중첩 속성으로 노출됩니다.  
  
 또한 다음 메서드 중 하나를 사용하여 <xref:System.Windows.Automation.AutomationElement> 또는 <xref:System.Windows.Automation.AutomationElement.Cached%2A> 구조에서 사용할 수 없는 속성을 비롯한 <xref:System.Windows.Automation.AutomationElement.Current%2A> 또는 컨트롤 패턴 속성을 검색할 수 있습니다.  
  
- <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A>  
  
 이러한 메서드는 전체 범위 속성에 대한 액세스는 물론 약간 향상된 성능을 제공합니다.  
  
 다음 코드 예제에서는 <xref:System.Windows.Automation.AutomationElement>의 속성을 검색하는 두 가지 방법을 보여 줍니다.  
  
 [!code-csharp[UIAClient_snip#121](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#121)]
 [!code-vb[UIAClient_snip#121](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#121)]  
  
 <xref:System.Windows.Automation.AutomationElement>에서 지원되는 컨트롤 패턴의 속성을 검색하기 위해 컨트롤 패턴 개체를 검색할 필요가 없습니다. 패턴 속성 식별자 중 하나를 메서드에 전달하면 됩니다.  
  
 다음 코드 예제에서는 컨트롤 패턴의 속성을 검색 하는 두 가지를 보여 줍니다.  
  
 [!code-csharp[UIAClient_snip#122](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#122)]
 [!code-vb[UIAClient_snip#122](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#122)]  
  
 `Get` 메서드는 <xref:System.Object>를 반환합니다. 애플리케이션은 값을 사용하기 전에 적절한 형식으로 반환된 개체를 캐스팅해야 합니다.  
  
## <a name="default-property-values"></a>기본 속성 값  
 UI 자동화 공급자가 속성을 구현하지 않는 경우 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 시스템에서 기본값을 제공할 수 있습니다. 예를 들어, 컨트롤의 공급자가 <xref:System.Windows.Automation.AutomationElement.HelpTextProperty>로 식별된 속성을 지원하지 않는 경우 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이 빈 문자열을 반환합니다. 마찬가지로, 공급자가 <xref:System.Windows.Automation.AutomationElement.IsDockPatternAvailableProperty>로 식별된 속성을 지원하지 않는 경우 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이 `false`를 반환합니다.  
  
 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=nameWithType> 메서드 오버로드를 사용하여 이 동작을 변경할 수 있습니다. `true` 를 두 번째 매개 변수로 지정하는 경우 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 이 기본값을 반환하지 않고 특수 값인 <xref:System.Windows.Automation.AutomationElement.NotSupported>를 반환합니다.  
  
 다음 예제 코드는 요소에서 속성을 검색하고, 이 속성이 지원되지 않을 경우 애플리케이션에서 정의된 값이 사용됩니다.  
  
 [!code-csharp[UIAClient_snip#123](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#123)]
 [!code-vb[UIAClient_snip#123](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#123)]  
  
 요소에서 지원되지 않는 속성을 검색하려면 <xref:System.Windows.Automation.AutomationElement.GetSupportedProperties%2A>를 사용합니다. 그러면 <xref:System.Windows.Automation.AutomationProperty> 식별자의 배열이 반환됩니다.  
  
## <a name="property-changed-events"></a>속성 변경 이벤트  
 <xref:System.Windows.Automation.AutomationElement> 또는 컨트롤 패턴의 속성 값이 변경되면 이벤트가 발생합니다. 애플리케이션은 <xref:System.Windows.Automation.Automation.AddAutomationPropertyChangedEventHandler%2A>를 호출하고, 원하는 속성을 지정하기 위해 <xref:System.Windows.Automation.AutomationProperty> 식별자의 배열을 마지막 매개 변수로 제공하여 이러한 이벤트를 구독할 수 있습니다.  
  
 <xref:System.Windows.Automation.AutomationPropertyChangedEventHandler>에서, 이벤트 인수의 <xref:System.Windows.Automation.AutomationPropertyChangedEventArgs.Property%2A> 멤버를 확인하여 변경된 속성을 식별할 수 있습니다. 이 인수에는 변경된 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성의 이전 값과 새 값이 포함됩니다. 이러한 값은 <xref:System.Object> 형식이며 사용하기 전에 올바른 형식으로 캐스팅되어야 합니다.  
  
## <a name="additional-automationelement-properties"></a>추가 AutomationElement 속성  
 <xref:System.Windows.Automation.AutomationElement.Current%2A> 및 <xref:System.Windows.Automation.AutomationElement.Cached%2A> 속성 구조 외에, <xref:System.Windows.Automation.AutomationElement> 에는 다음과 같은 속성이 있으며 이러한 속성은 간단한 속성 접근자를 통해 검색됩니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Windows.Automation.AutomationElement.CachedChildren%2A>|캐시에 있는 자식 <xref:System.Windows.Automation.AutomationElement> 개체의 컬렉션입니다.|  
|<xref:System.Windows.Automation.AutomationElement.CachedParent%2A>|캐시에 있는 <xref:System.Windows.Automation.AutomationElement> 부모 개체입니다.|  
|<xref:System.Windows.Automation.AutomationElement.FocusedElement%2A>|(정적 속성) 입력 포커스가 있는 <xref:System.Windows.Automation.AutomationElement> 입니다.|  
|<xref:System.Windows.Automation.AutomationElement.RootElement%2A>|(정적 속성) 루트 <xref:System.Windows.Automation.AutomationElement>입니다.|  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 클라이언트의 캐싱](caching-in-ui-automation-clients.md)
- [서버 쪽 UI 자동화 공급자 구현](server-side-ui-automation-provider-implementation.md)
- [UI 자동화 이벤트 구독](subscribe-to-ui-automation-events.md)
