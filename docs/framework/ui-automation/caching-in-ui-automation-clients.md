---
title: UI 자동화 클라이언트의 캐싱
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation caching in clients
- caching, UI Automation clients
ms.assetid: 94c15031-4975-43cc-bcd5-c9439ed21c9c
ms.openlocfilehash: bf617279b16f53164209f5ae7605830dabda4c2e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043922"
---
# <a name="caching-in-ui-automation-clients"></a>UI 자동화 클라이언트의 캐싱
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 항목에서는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 및 컨트롤 패턴의 캐싱에 대해 설명합니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서, 캐싱은 데이터의 프리페치를 의미합니다. 이렇게 하면 추가 크로스 프로세스와 통신하지 않고도 데이터에 액세스할 수 있습니다. 캐싱은 일반적으로 UI 자동화 클라이언트 애플리케이션에서 속성 및 컨트롤 패턴을 일괄적으로 검색하는 데 사용됩니다. 필요에 따라 캐시에서 정보가 검색됩니다. 애플리케이션은 일반적으로 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 에서 변경된 사항이 있음을 나타내는 이벤트에 대한 응답으로 캐시를 주기적으로 업데이트합니다.  
  
 캐싱의 이점은 WPF (Windows Presentation Foundation) 컨트롤과 서버 쪽 UI 자동화 공급자가 있는 사용자 지정 컨트롤에서 가장 두드러지게 나타납니다. [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 컨트롤의 기본 공급자와 같은 클라이언트 쪽 공급자에 액세스할 때는 캐싱의 효율성이 떨어집니다.  
  
 캐싱은 애플리케이션이 <xref:System.Windows.Automation.CacheRequest> 를 활성화한 다음 <xref:System.Windows.Automation.AutomationElement>를 반환하는 메서드 또는 속성을 사용하는 경우에 발생합니다. 예: <xref:System.Windows.Automation.AutomationElement.FindFirst%2A>, <xref:System.Windows.Automation.AutomationElement.FindAll%2A> <xref:System.Windows.Automation.TreeWalker> 클래스의 메서드는 예외입니다. 캐싱은 <xref:System.Windows.Automation.CacheRequest> 가 매개 변수로 지정된 경우에만 수행됩니다(예: <xref:System.Windows.Automation.TreeWalker.GetFirstChild%28System.Windows.Automation.AutomationElement%2CSystem.Windows.Automation.CacheRequest%29?displayProperty=nameWithType>).  
  
 또한 캐싱은 <xref:System.Windows.Automation.CacheRequest> 가 활성화되어 있는 동안 이벤트를 구독할 때 발생합니다. 이벤트 소스로 이벤트 처리기에 전달된 <xref:System.Windows.Automation.AutomationElement> 에는 원래 <xref:System.Windows.Automation.CacheRequest>가 지정한 캐시된 속성 및 패턴이 포함됩니다. 이벤트를 구독한 이후의 <xref:System.Windows.Automation.CacheRequest> 변경 내용은 영향을 주지 않습니다.  
  
 요소의 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 및 컨트롤 패턴을 캐시할 수 있습니다.  
  
<a name="Options_for_Caching"></a>   
## <a name="options-for-caching"></a>캐싱 옵션  
 <xref:System.Windows.Automation.CacheRequest> 는 다음과 같은 캐싱 옵션을 지정합니다.  
  
<a name="Properties_to_Cache"></a>   
### <a name="properties-to-cache"></a>캐시할 속성  
 요청을 활성화하기 전에 각 속성에 대해 <xref:System.Windows.Automation.CacheRequest.Add%28System.Windows.Automation.AutomationProperty%29> 를 호출하여 캐시할 속성을 지정할 수 있습니다.  
  
<a name="Control_Patterns_to_Cache"></a>   
### <a name="control-patterns-to-cache"></a>캐시할 컨트롤 패턴  
 요청을 활성화하기 전에 각 패턴에 대해 <xref:System.Windows.Automation.CacheRequest.Add%28System.Windows.Automation.AutomationPattern%29> 를 호출하여 캐시할 패턴을 지정할 수 있습니다. 패턴이 캐시될 때 해당 속성이 자동으로 캐시되지 않으므로, <xref:System.Windows.Automation.CacheRequest.Add%2A?displayProperty=nameWithType>를 사용하여 캐시할 속성을 지정해야 합니다.  
  
<a name="Scope_of_the_Caching"></a>   
### <a name="scope-and-filtering-of-caching"></a>캐싱의 범위 및 필터링  
 요청을 활성화하기 전에 <xref:System.Windows.Automation.CacheRequest.TreeScope%2A?displayProperty=nameWithType> 속성을 설정하여 속성 및 패턴을 캐시할 요소를 지정할 수 있습니다. 해당 범위는 요청이 활성 상태인 동안 검색 되는 요소를 기준으로 합니다. 예를 들어 <xref:System.Windows.Automation.TreeScope.Children>만 설정한 다음 <xref:System.Windows.Automation.AutomationElement>를 검색하는 경우, 요소의 자식 속성 및 패턴이 캐시되지만 요소 자체의 속성 및 패턴은 캐시되지 않습니다. 검색된 요소 자체에 캐시가 수행되도록 하려면 <xref:System.Windows.Automation.TreeScope.Element> 속성에 <xref:System.Windows.Automation.CacheRequest.TreeScope%2A> 를 포함해야 합니다. 범위를 <xref:System.Windows.Automation.TreeScope.Parent> 또는 <xref:System.Windows.Automation.TreeScope.Ancestors>로 설정할 수 없습니다. 하지만 자식 요소가 캐시될 때 부모 요소를 캐시할 수 있습니다. 이 항목의 캐시된 자식 및 부모 검색을 참조하세요.  
  
 <xref:System.Windows.Automation.CacheRequest.TreeFilter%2A?displayProperty=nameWithType> 속성도 캐싱 범위에 영향을 줍니다. 기본적으로, 캐싱은 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰에 나타나는 요소에 대해서만 수행됩니다. 하지만 모든 요소 또는 콘텐츠 뷰에 나타나는 요소에만 캐싱을 적용하도록 이 속성을 변경할 수 있습니다.  
  
<a name="Strength_of_the_Element_References"></a>   
### <a name="strength-of-the-element-references"></a>요소 참조의 장점  
 <xref:System.Windows.Automation.AutomationElement>를 검색할 때, 캐시되지 않은 속성 및 패턴을 비롯하여 해당 요소의 모든 속성 및 패턴에 대해 기본적으로 액세스할 수 있습니다. 하지만 효율성을 높이기 위해 <xref:System.Windows.Automation.CacheRequest.AutomationElementMode%2A> 의 <xref:System.Windows.Automation.CacheRequest> 속성을 <xref:System.Windows.Automation.AutomationElementMode.None>으로 설정하여 요소에 대한 참조가 캐시된 데이터만 나타내도록 지정할 수 있습니다. 이 경우, 검색된 요소의 캐시되지 않은 속성 및 패턴에는 액세스할 수 없습니다. 이는 <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A> 또는 `Current` 의 <xref:System.Windows.Automation.AutomationElement> 속성이나 컨트롤 패턴을 통해 속성에 액세스할 수 없으며 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> 또는 <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>를 사용하여 패턴을 검색할 수 없다는 의미입니다. 캐시된 패턴에서, 배열 속성을 검색하는 메서드(예: <xref:System.Windows.Automation.SelectionPattern.SelectionPatternInformation.GetSelection%2A?displayProperty=nameWithType>)를 호출할 수 있지만 컨트롤에서 작업을 수행하는 메서드(예: <xref:System.Windows.Automation.InvokePattern.Invoke%2A?displayProperty=nameWithType>)는 호출할 수 없습니다.  
  
 개체를 완전히 참조할 필요가 없는 애플리케이션의 예로는 화면 판독기가 있습니다. 이 애플리케이션은 창에 있는 요소의 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name%2A> 및 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ControlType%2A> 속성을 프리페치하지만 <xref:System.Windows.Automation.AutomationElement> 개체 자체가 필요하지 않습니다.  
  
<a name="Activating_the_CacheRequest"></a>   
## <a name="activating-the-cacherequest"></a>CacheRequest 활성화  
 캐싱은 현재 스레드에 대해 <xref:System.Windows.Automation.AutomationElement> 가 활성 상태일 때 <xref:System.Windows.Automation.CacheRequest> 개체가 검색되는 경우에만 수행됩니다. <xref:System.Windows.Automation.CacheRequest>를 활성화하는 방법은 두 가지입니다.  
  
 일반적인 방법은 <xref:System.Windows.Automation.CacheRequest.Activate%2A>를 호출하는 것입니다. 이 메서드는 <xref:System.IDisposable>을 구현하는 개체를 반환합니다. <xref:System.IDisposable> 개체가 존재하는 한 이 요청은 활성 상태로 유지됩니다. 개체의 수명을 제어 하는 가장 쉬운 방법은 `using` (C#) 또는 `Using` (Visual Basic) 블록 내에 호출을 묶는 것입니다. 이렇게 하면 예외가 발생하더라도 요청이 스택에서 팝됩니다.  
  
 다른 방법으로는 <xref:System.Windows.Automation.CacheRequest.Push%2A>를 호출하는 것이며, 이 방법은 캐시 요청을 중첩할 때 유용합니다. 이렇게 하면 스택에 요청이 배치되고 활성화됩니다. 이 요청은 <xref:System.Windows.Automation.CacheRequest.Pop%2A>에 의해 스택에서 제거될 때까지 활성 상태로 유지됩니다. 다른 요청이 스택에 푸시되면 이 요청이 일시적으로 비활성 상태가 되고 스택 맨 위의 요청만 활성 상태로 유지됩니다.  
  
<a name="Retrieving_Cached_Properties"></a>   
## <a name="retrieving-cached-properties"></a>캐시된 속성 검색  
 다음과 같은 메서드 및 속성을 통해 요소의 캐시된 속성을 검색할 수 있습니다.  
  
- <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.Cached%2A>  
  
 요청된 속성이 캐시에 없는 경우 예외가 발생합니다.  
  
 <xref:System.Windows.Automation.AutomationElement.Cached%2A>와 마찬가지로, <xref:System.Windows.Automation.AutomationElement.Current%2A>는 개별 속성을 구조의 멤버로 노출합니다. 하지만 이 구조를 검색할 필요는 없습니다. 개별 속성에 직접 액세스할 수 있습니다. 예를 들어, <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name%2A> 가 `element.Cached.Name`인 `element` 에서 <xref:System.Windows.Automation.AutomationElement>속성을 가져올 수 있습니다.  
  
<a name="Retrieving_Cached_Control_Patterns"></a>   
## <a name="retrieving-cached-control-patterns"></a>캐시된 컨트롤 패턴 검색  
 다음과 같은 메서드를 통해 요소의 캐시된 컨트롤 패턴을 검색할 수 있습니다.  
  
- <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A>  
  
 해당 패턴에 캐시에 없으면, <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> 이 예외를 발생시키고 <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A> 이 `false`를 반환합니다.  
  
 패턴 개체의 `Cached` 속성을 사용하여 컨트롤 패턴의 캐시된 속성을 검색할 수 있습니다. `Current` 속성을 통해 현재 값을 검색할 수도 있지만, <xref:System.Windows.Automation.AutomationElementMode.None> 가 검색될 때 <xref:System.Windows.Automation.AutomationElement> 가 지정되지 않았어야 합니다. (<xref:System.Windows.Automation.AutomationElementMode.Full> 은 기본값이며 현재 값에 대한 액세스를 허용합니다.)  
  
<a name="Retrieving_Cached_Children_and_Parents"></a>   
## <a name="retrieving-cached-children-and-parents"></a>캐시된 자식 및 부모 검색  
 <xref:System.Windows.Automation.AutomationElement> 를 검색하고 요청의 <xref:System.Windows.Automation.CacheRequest.TreeScope%2A> 속성을 통해 이 요소의 자식 캐싱을 요청하는 경우, 이후에 검색한 요소의 <xref:System.Windows.Automation.AutomationElement.CachedChildren%2A> 속성에서 자식 요소를 가져올 수 있습니다.  
  
 <xref:System.Windows.Automation.TreeScope.Element> 캐시 요청 범위에 포함된 경우, 나중에 모든 자식 요소의 <xref:System.Windows.Automation.AutomationElement.CachedParent%2A> 속성에서 요청의 루트 요소를 사용할 수 있습니다.  
  
> [!NOTE]
> 요청의 루트 요소의 부모 또는 상위 항목은 캐시할 수 없습니다.  
  
<a name="Updating_the_Cache"></a>   
## <a name="updating-the-cache"></a>캐시 업데이트  
 캐시는 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]에서 변경된 사항이 없는 경우에만 유효합니다. 애플리케이션은 일반적으로 이벤트에 대한 응답으로 캐시를 업데이트합니다.  
  
 <xref:System.Windows.Automation.CacheRequest> 가 활성화되어 있는 동안 이벤트를 구독하는 경우, 이벤트 처리기 대리자가 호출될 때마다 이벤트의 소스로 업데이트된 캐시를 사용하여 <xref:System.Windows.Automation.AutomationElement> 를 가져옵니다. <xref:System.Windows.Automation.AutomationElement.GetUpdatedCache%2A>를 호출하여 요소의 캐시된 정보를 업데이트할 수도 있습니다. 원본 <xref:System.Windows.Automation.CacheRequest> 를 전달하여 이전에 캐시된 모든 정보를 업데이트할 수 있습니다.  
  
 캐시를 업데이트해도 기존 <xref:System.Windows.Automation.AutomationElement> 참조의 속성이 변경되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [클라이언트용 UI 자동화 이벤트](ui-automation-events-for-clients.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
- [FetchTimer 샘플](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771456(v=vs.90))
