---
title: WPF 사용자 지정 컨트롤의 UI 자동화
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [WPF], applying UI automation
- accessibility [WPF], applying to custom controls
- custom controls [WPF], improving accessibility
- UI Automation [WPF], using with custom controls
ms.assetid: 47b310fc-fbd5-4ce2-a606-22d04c6d4911
ms.openlocfilehash: ef045ffaac47c6cb196d821c25d96c4d2cd7bf88
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70254256"
---
# <a name="ui-automation-of-a-wpf-custom-control"></a>WPF 사용자 지정 컨트롤의 UI 자동화
[!INCLUDE[TLA#tla_uiautomation](../../../../includes/tlasharptla-uiautomation-md.md)]에서는 자동화 클라이언트가 다양한 플랫폼 및 프레임워크의 사용자 인터페이스를 검사하거나 운영하는 데 사용할 수 있는 일반화된 단일 인터페이스를 제공합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]를 통해 품질 보증(테스트) 코드 및 화면 읽기 프로그램과 같은 접근성 응용 프로그램은 사용자 인터페이스 요소를 검사하고 다른 코드에서 해당 요소에 대한 사용자 상호 작용을 시뮬레이트할 수 있습니다. 모든 플랫폼에서 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]에 대한 자세한 내용은 접근성을 참조하세요.  
  
 이 항목에서는 WPF 애플리케이션에서 실행되는 사용자 지정 컨트롤에 대한 서버 쪽 UI 자동화 공급자를 구현하는 방법을 설명합니다. WPF는 사용자 인터페이스 요소의 트리에 대응하는 피어 자동화 개체의 트리를 통해 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]를 지원합니다. 접근성 기능을 제공하는 애플리케이션 및 테스트 코드는 자동화 피어 개체를 직접 사용(in-process 코드의 경우)하거나 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]에서 제공하는 일반화된 인터페이스를 통해 사용할 수 있습니다.  

<a name="AutomationPeerClasses"></a>   
## <a name="automation-peer-classes"></a>자동화 피어 클래스  
 WPF는에서 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] 파생 되는 피어 클래스의 트리를 통해 <xref:System.Windows.Automation.Peers.AutomationPeer>를 지원 합니다. 규칙에 따라 피어 클래스 이름은 컨트롤 클래스 이름으로 시작하고 "AutomationPeer"로 끝납니다. 예를 들어 <xref:System.Windows.Automation.Peers.ButtonAutomationPeer> 는 <xref:System.Windows.Controls.Button> 컨트롤 클래스의 피어 클래스입니다. 피어 클래스는 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] 컨트롤 형식과 거의 동일하지만 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 요소와 관련됩니다. [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] 인터페이스를 통해 WPF 응용 프로그램에 액세스하는 자동화 코드는 자동화 피어를 직접 사용하지 않지만 동일한 프로세스 공간의 자동화 코드는 자동화 피어를 직접 사용할 수 있습니다.  
  
<a name="BuiltInAutomationPeerClasses"></a>   
## <a name="built-in-automation-peer-classes"></a>기본 제공 자동화 피어 클래스  
 요소는 사용자의 인터페이스 작업을 허용하는 경우 또는 화면 읽기 프로그램 애플리케이션 사용자에게 필요한 정보를 포함하는 경우 자동화 피어 클래스를 구현합니다. 일부 WPF 시각적 요소에는 자동화 피어가 없습니다. 자동화 피어를 구현 하는 클래스의 <xref:System.Windows.Controls.Button>예로 <xref:System.Windows.Controls.TextBox>는, <xref:System.Windows.Controls.Label>및가 있습니다. 자동화 피어를 구현 하지 않는 클래스의 예로는 <xref:System.Windows.Controls.Decorator>에서 파생 되는 클래스 (예 <xref:System.Windows.Controls.Border>: <xref:System.Windows.Controls.Grid> 및 <xref:System.Windows.Controls.Canvas>)와를 <xref:System.Windows.Controls.Panel>기반으로 하는 클래스가 있습니다.  
  
 기본 <xref:System.Windows.Controls.Control> 클래스에 해당 하는 피어 클래스가 없습니다. 에서 <xref:System.Windows.Controls.Control>파생 되는 사용자 지정 컨트롤에 해당 하는 피어 클래스가 필요한 경우에서 <xref:System.Windows.Automation.Peers.FrameworkElementAutomationPeer>사용자 지정 피어 클래스를 파생 해야 합니다.  
  
<a name="SecurityConsiderations"></a>   
## <a name="security-considerations-for-derived-peers"></a>파생된 피어의 보안 고려 사항  
 자동화 피어는 부분 신뢰 환경에서 실행되어야 합니다. UIAutomationClient 어셈블리의 코드는 부분 신뢰 환경에서 실행되도록 구성되지 않았으며 자동화 피어 코드는 해당 어셈블리를 참조해서는 안 됩니다. 대신 UIAutomationTypes 어셈블리의 클래스를 사용해야 합니다. 예를 들어 UIAutomationClient 어셈블리의 <xref:System.Windows.Automation.AutomationElementIdentifiers> <xref:System.Windows.Automation.AutomationElement> 클래스에 해당 하는 uiautomationtypes.dll 어셈블리의 클래스를 사용 해야 합니다. 자동화 피어 코드에서 UIAutomationTypes 어셈블리를 참조해도 안전합니다.  
  
<a name="PeerNavigation"></a>   
## <a name="peer-navigation"></a>피어 탐색  
 자동화 피어를 찾은 후 in-process 코드는 개체의 <xref:System.Windows.Automation.Peers.AutomationPeer.GetChildren%2A> 및 <xref:System.Windows.Automation.Peers.AutomationPeer.GetParent%2A> 메서드를 호출 하 여 피어 트리를 탐색할 수 있습니다. 컨트롤 내의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 요소 간 탐색은 피어의 <xref:System.Windows.Automation.Peers.AutomationPeer.GetChildrenCore%2A> 메서드 구현에서 지원 됩니다. UI 자동화 시스템은 이 메서드를 호출하여 컨트롤 내에 포함된 하위 요소의 트리를 작성합니다(예: 목록 상자의 목록 항목). 기본 <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetChildrenCore%2A?displayProperty=nameWithType> 메서드는 요소의 시각적 트리를 순회 하 여 자동화 피어의 트리를 빌드합니다. 사용자 지정 컨트롤은 자식 요소를 자동화 클라이언트에 노출하도록 이 메서드를 재정의하여 정보를 전달하거나 사용자 상호 작용을 허용하는 요소의 자동화 피어를 반환합니다.  
  
<a name="Customizations"></a>   
## <a name="customizations-in-a-derived-peer"></a>파생된 피어의 사용자 지정  
 에서 <xref:System.Windows.UIElement> 파생 되 고 <xref:System.Windows.ContentElement> 보호 된 가상 메서드 <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A>를 포함 하는 모든 클래스입니다. WPF는 <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> 를 호출 하 여 각 컨트롤에 대 한 자동화 피어 개체를 가져옵니다. 자동화 코드는 피어를 사용하여 컨트롤의 특성 및 기능에 대한 정보를 가져오고 대화형 사용을 시뮬레이트할 수 있습니다. 자동화를 지 원하는 사용자 지정 컨트롤은 <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> 에서 <xref:System.Windows.Automation.Peers.AutomationPeer>파생 된 클래스의 인스턴스를 재정의 하 고 반환 해야 합니다. 예를 들어 사용자 지정 컨트롤이 <xref:System.Windows.Controls.Primitives.ButtonBase> 클래스에서 파생 되는 경우에서 <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> 반환 되는 개체는에서 <xref:System.Windows.Automation.Peers.ButtonBaseAutomationPeer>파생 되어야 합니다.  
  
 사용자 지정 컨트롤을 구현할 때 사용자 지정 컨트롤과 관련된 고유한 동작을 설명하는 "Core" 메서드를 기본 자동화 피어 클래스에서 재정의해야 합니다.  
  
### <a name="override-oncreateautomationpeer"></a>OnCreateAutomationPeer 재정의  
 <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> 에서<xref:System.Windows.Automation.Peers.AutomationPeer>직접 또는 간접적으로 파생 되어야 하는 공급자 개체를 반환 하도록 사용자 지정 컨트롤에 대 한 메서드를 재정의 합니다.  
  
### <a name="override-getpattern"></a>GetPattern 재정의  
 자동화 피어는 서버 쪽 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] 공급자의 몇 가지 구현 측면을 간소화하지만 사용자 지정 컨트롤 자동화 피어는 패턴 인터페이스를 계속 처리해야 합니다. 비 WPF 공급자와 마찬가지로, 피어는 <xref:System.Windows.Automation.Provider?displayProperty=nameWithType> 네임 스페이스에서 인터페이스의 구현 ( <xref:System.Windows.Automation.Provider.IInvokeProvider>예:)을 제공 하 여 컨트롤 패턴을 지원 합니다. 컨트롤 패턴 인터페이스는 피어 자체 또는 다른 개체를 통해 구현할 수 있습니다. 의 <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> 피어 구현은 지정 된 패턴을 지 원하는 개체를 반환 합니다. [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]코드는 메서드 <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> 를 호출 하 고 <xref:System.Windows.Automation.Peers.PatternInterface> 열거형 값을 지정 합니다. 재정의는 지정 <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> 된 패턴을 구현 하는 개체를 반환 해야 합니다. 컨트롤에 패턴의 사용자 지정 구현이 없는 경우의 기본 형식 구현을 호출 하 여 해당 구현이 나 null을 검색할 <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> 수 있습니다 .이 컨트롤 형식에 대해 패턴이 지원 되지 않는 경우에는 null입니다. 예를 들어 사용자 지정 NumericUpDown 컨트롤을 범위 내의 값으로 설정 하 여 해당 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] 피어가 인터페이스를 <xref:System.Windows.Automation.Provider.IRangeValueProvider> 구현할 수 있습니다. 다음 예제에서는 <xref:System.Windows.Automation.Peers.PatternInterface.RangeValue?displayProperty=nameWithType> 값에 응답 하도록 피어의 <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> 메서드를 재정의 하는 방법을 보여 줍니다.  
  
 [!code-csharp[CustomControlNumericUpDown#GetPattern](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#getpattern)]
 [!code-vb[CustomControlNumericUpDown#GetPattern](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#getpattern)]  
  
 메서드 <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> 는 하위 요소를 패턴 공급자로 지정할 수도 있습니다. 다음 코드에서는 스크롤 패턴 <xref:System.Windows.Controls.ItemsControl> 처리를 내부 <xref:System.Windows.Controls.ScrollViewer> 컨트롤의 피어로 전송 하는 방법을 보여 줍니다.  
  
```csharp  
public override object GetPattern(PatternInterface patternInterface)  
{  
    if (patternInterface == PatternInterface.Scroll)  
    {  
        ItemsControl owner = (ItemsControl) base.Owner;  
  
        // ScrollHost is internal to the ItemsControl class  
        if (owner.ScrollHost != null)  
        {  
            AutomationPeer peer = UIElementAutomationPeer.CreatePeerForElement(owner.ScrollHost);  
            if ((peer != null) && (peer is IScrollProvider))  
            {  
                peer.EventsSource = this;  
                return (IScrollProvider) peer;  
            }  
        }  
    }  
    return base.GetPattern(patternInterface);  
}  
```  
  
```vb  
Public Class Class1  
    Public Overrides Function GetPattern(ByVal patternInterface__1 As PatternInterface) As Object  
        If patternInterface1 = PatternInterface.Scroll Then  
            Dim owner As ItemsControl = DirectCast(MyBase.Owner, ItemsControl)  
  
            ' ScrollHost is internal to the ItemsControl class  
            If owner.ScrollHost IsNot Nothing Then  
                Dim peer As AutomationPeer = UIElementAutomationPeer.CreatePeerForElement(owner.ScrollHost)  
                If (peer IsNot Nothing) AndAlso (TypeOf peer Is IScrollProvider) Then  
                    peer.EventsSource = Me  
                    Return DirectCast(peer, IScrollProvider)  
                End If  
            End If  
        End If  
        Return MyBase.GetPattern(patternInterface1)  
    End Function  
End Class  
```  
  
 패턴 처리를 위한 하위 요소를 지정 하기 위해이 코드는 하위 요소 개체를 가져오고, <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.CreatePeerForElement%2A> 메서드를 사용 하 여 피어를 만들며, 새 피어의 <xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A> 속성을 현재 피어로 설정 하 고, 새 피어를 반환 합니다. 하위 <xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A> 요소에 대해를 설정 하면 하위 요소는 자동화 피어 트리에 나타나지 않으며 하위 요소에 의해 발생 하는 모든 이벤트를에 <xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A>지정 된 컨트롤의 원본으로 지정 합니다. 컨트롤 <xref:System.Windows.Controls.ScrollViewer> 은 자동화 트리에 나타나지 않으며 생성 되는 스크롤 이벤트는 <xref:System.Windows.Controls.ItemsControl> 개체에서 시작 된 것 처럼 보입니다.  
  
### <a name="override-core-methods"></a>"Core" 메서드 재정의  
 자동화 코드는 피어 클래스의 public 메서드를 호출하여 컨트롤에 대한 정보를 가져옵니다. 컨트롤에 대한 정보를 제공하려면 컨트롤 구현이 기본 자동화 피어 클래스에서 제공하는 구현과 다른 경우 이름이 "Core"로 끝나는 각 메서드를 재정의합니다. 다음 예제와 같이 최소한의 컨트롤은 <xref:System.Windows.Automation.Peers.AutomationPeer.GetClassNameCore%2A> 및 <xref:System.Windows.Automation.Peers.AutomationPeer.GetAutomationControlTypeCore%2A> 메서드를 구현 해야 합니다.  
  
 [!code-csharp[CustomControlNumericUpDown#CoreOverrides](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#coreoverrides)]
 [!code-vb[CustomControlNumericUpDown#CoreOverrides](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#coreoverrides)]  
  
 구현 <xref:System.Windows.Automation.Peers.AutomationPeer.GetAutomationControlTypeCore%2A> 에서는 값을 <xref:System.Windows.Automation.ControlType> 반환 하 여 컨트롤을 설명 합니다. 를 반환할 <xref:System.Windows.Automation.ControlType.Custom?displayProperty=nameWithType>수 있지만 컨트롤을 정확 하 게 설명 하는 경우에는 보다 구체적인 컨트롤 형식 중 하나를 반환 해야 합니다. 의 <xref:System.Windows.Automation.ControlType.Custom?displayProperty=nameWithType> 반환 값에는 공급자를 구현 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]하기 위한 추가 작업이 필요 하며 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] , 클라이언트 제품은 컨트롤 구조, 키보드 조작 및 가능한 컨트롤 패턴을 예상할 수 없습니다.  
  
 <xref:System.Windows.Automation.Peers.AutomationPeer.IsContentElementCore%2A> 및<xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A> 메서드를 구현 하 여 컨트롤에 데이터 콘텐츠가 포함 되어 있거나 사용자 인터페이스 (또는 둘 다)에서 대화형 역할을 수행할지 여부를 나타냅니다. 기본적으로 두 메서드 모두 `true`를 반환합니다. 이러한 설정에서는 화면 읽기 프로그램과 같은 자동화 도구의 유용성이 향상되며, 이러한 메서드를 사용하여 자동화 트리를 필터링할 수 있습니다. 메서드가 하위 요소 피어로 패턴 처리를 전송 하는 경우 하위 요소 <xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A> 피어의 메서드는 false를 반환 하 여 자동화 트리에서 하위 요소 피어를 숨길 수 있습니다. <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> 예를 들어 <xref:System.Windows.Controls.ListBox> ,의 스크롤은에 <xref:System.Windows.Controls.ScrollViewer>의해 처리 되 고 <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> 에 대 한 <xref:System.Windows.Automation.Peers.PatternInterface.Scroll?displayProperty=nameWithType> 자동화 피어는와 <xref:System.Windows.Automation.Peers.ListBoxAutomationPeer>연결 된의 <xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer> 메서드에 의해 반환 됩니다. 따라서의 메서드 <xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A> <xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer> 는 `false` 를<xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer> 반환 하므로이 자동화 트리에 나타나지 않습니다.  
  
 자동화 피어는 컨트롤에 적절한 기본값을 제공해야 합니다. 컨트롤을 참조 하는 XAML은 특성을 포함 <xref:System.Windows.Automation.AutomationProperties> 하 여 핵심 메서드의 피어 구현을 재정의할 수 있습니다. 예를 들어 다음 XAML에서는 사용자 지정된 두 가지 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] 속성이 있는 단추를 만듭니다.  
  
```xaml  
<Button AutomationProperties.Name="Special"   
    AutomationProperties.HelpText="This is a special button."/>  
```  
  
### <a name="implement-pattern-providers"></a>패턴 공급자 구현  
 소유 하는 요소가에서 <xref:System.Windows.Controls.Control>직접 파생 되는 경우 사용자 지정 공급자에 의해 구현 되는 인터페이스는 명시적으로 선언 됩니다. 예를 들어 다음 코드에서는 범위 값을 구현 <xref:System.Windows.Controls.Control> 하는에 대 한 피어를 선언 합니다.  
  
```csharp  
public class RangePeer1 : FrameworkElementAutomationPeer, IRangeValueProvider { }  
```  
  
```vb  
Public Class RangePeer1  
    Inherits FrameworkElementAutomationPeer  
    Implements IRangeValueProvider  
End Class  
```  
  
 소유 하는 컨트롤이와 <xref:System.Windows.Controls.Primitives.RangeBase>같은 특정 형식의 컨트롤에서 파생 되는 경우 피어는 해당 하는 파생 피어 클래스에서 파생 될 수 있습니다. 이 경우 피어는의 <xref:System.Windows.Automation.Peers.RangeBaseAutomationPeer> <xref:System.Windows.Automation.Provider.IRangeValueProvider>기본 구현을 제공 하는에서 파생 됩니다. 다음 코드에서는 이러한 피어의 선언을 보여 줍니다.  
  
```csharp  
public class RangePeer2 : RangeBaseAutomationPeer { }  
```  
  
```vb  
Public Class RangePeer2  
    Inherits RangeBaseAutomationPeer  
End Class  
```  
  
구현 예제는 NumericUpDown 사용자 지정 컨트롤 [C#](https://github.com/dotnet/samples/tree/master/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp) 을 구현 하 고 소비 하는 또는 [Visual Basic](https://github.com/dotnet/samples/tree/master/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic) 소스 코드를 참조 하세요.  
  
### <a name="raise-events"></a>이벤트 발생  
 자동화 클라이언트는 자동화 이벤트를 구독할 수 있습니다. 사용자 지정 컨트롤은 메서드를 <xref:System.Windows.Automation.Peers.AutomationPeer.RaiseAutomationEvent%2A> 호출 하 여 컨트롤 상태의 변경 내용을 보고 해야 합니다. 마찬가지로 속성 값이 변경 되 면 <xref:System.Windows.Automation.Peers.AutomationPeer.RaisePropertyChangedEvent%2A> 메서드를 호출 합니다. 다음 코드에서는 컨트롤 코드 내에서 피어 개체를 가져오고 메서드를 호출하여 이벤트를 발생시키는 방법을 보여 줍니다. 최적화 방법으로 코드는 이 이벤트 유형에 대한 수신기가 있는지 확인합니다. 수신기가 있는 경우에만 이벤트가 발생되면 불필요한 오버헤드를 방지하고 컨트롤이 응답 가능한 상태를 유지하는 데 도움이 됩니다.  
  
 [!code-csharp[CustomControlNumericUpDown#RaiseEventFromControl](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#raiseeventfromcontrol)]
 [!code-vb[CustomControlNumericUpDown#RaiseEventFromControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#raiseeventfromcontrol)]  
  
## <a name="see-also"></a>참고자료

- [UI 자동화 개요](../../ui-automation/ui-automation-overview.md)
- [서버 쪽 UI 자동화 공급자 구현](../../ui-automation/server-side-ui-automation-provider-implementation.md)
- [GitHub의 NumericUpDown 사용자C#지정 컨트롤 ()](https://github.com/dotnet/samples/tree/master/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp)  
- [GitHub의 NumericUpDown 사용자 지정 컨트롤 (Visual Basic)](https://github.com/dotnet/samples/tree/master/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic)
