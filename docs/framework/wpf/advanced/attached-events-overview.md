---
title: 연결된 이벤트 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- handling attached events [WPF]
- defining attached events as routed events [WPF]
- attached events [WPF], scenarios for
- attached events vs. routed events [WPF]
- backing attached events with routed events [WPF]
- attached events [WPF], definition
ms.assetid: 2c40eae3-80e4-4a45-ae09-df6c9ab4d91e
ms.openlocfilehash: 40e7bd34388bec06cd8a7c3610599d814aef101f
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69038150"
---
# <a name="attached-events-overview"></a>연결된 이벤트 개요

Extensible Application Markup Language (XAML)는 *연결 된 이벤트*라는 언어 구성 요소와 이벤트 유형을 정의 합니다. 연결된 이벤트의 개념을 사용하면 실제로 정의하거나 이벤트를 상속하는 요소가 아닌 임의의 요소에 특정 이벤트의 핸들러를 추가할 수 있습니다. 이 경우 이벤트를 잠재적으로 발생시키는 개체나 인스턴스를 처리하는 대상이 정의하지 않으며 또는 그렇지 않으면 이벤트를 "소유"합니다.  

<a name="prerequisites"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목에서는 [라우트된 이벤트 개요](routed-events-overview.md) 및 [XAML 개요(WPF)](xaml-overview-wpf.md)를 읽었다고 가정합니다.  
  
<a name="Syntax"></a>   
## <a name="attached-event-syntax"></a>연결된 이벤트 구문  
 연결 된 이벤트에는 연결 된 이벤트 사용을 지원 하기 위해 지원 코드에서 사용 해야 하는 XAML 구문 및 코딩 패턴이 있습니다.  
  
 XAML 구문에서 연결 된 이벤트는 이벤트 이름 뿐만 아니라 해당 이벤트 이름에는 점 (.)으로 구분 된 이벤트 이름에 의해 지정 됩니다. 이벤트 이름이 소유 형식의 이름으로 정규화되기 때문에, 연결된 이벤트 구문을 모든 연결된 이벤트를 인스턴스화할 수 있는 모든 요소에 연결할 수 있습니다.  
  
 예를 들어 다음은 사용자 지정 `NeedsCleaning` 연결 된 이벤트에 대 한 처리기를 연결 하는 XAML 구문입니다.  
  
 [!code-xaml[WPFAquariumSln#AE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquarium/Window1.xaml#ae)]  
  
 `aqua:` 접두사. 연결된 이벤트가 사용자 지정 맵핑된 xmlns에서 오는 사용자 지정 이벤트이기 때문에 이 경우에 접두사가 필요합니다.  
  
<a name="WPFImplements"></a>   
## <a name="how-wpf-implements-attached-events"></a>WPF가 연결된 이벤트를 구현하는 방법

WPF에서 연결 된 이벤트는 <xref:System.Windows.RoutedEvent> 필드에 의해 지원 되며 발생 한 후 트리를 통해 라우팅됩니다. 일반적으로 연결된 이벤트(이벤트를 발생하는 개체)의 소스는 시스템이나 서비스 소스이며, 이벤트를 발생하는 코드를 실행하는 개체는 직접적인 요소 트리 파트가 아닙니다.  
  
<a name="Scenarios"></a>   
## <a name="scenarios-for-attached-events"></a>연결된 이벤트에 대한 시나리오  
 WPF에서 연결 된 이벤트는 정적 <xref:System.Windows.Input.Mouse> 클래스 <xref:System.Windows.Controls.Validation> 또는 클래스에서 사용 하도록 설정 된 이벤트와 같이 서비스 수준 추상화가 있는 특정 기능 영역에 있습니다. 서비스와 상호 작용하거나 사용하는 클래스는 연결된 이벤트 구문에서 이벤트를 사용하거나, 클래스가 서비스의 기능을 통합하는 방법의 일부인 라우트된 이벤트로 연결된 이벤트를 나타내도록 선택할 수 있습니다.  
  
 WPF는 연결 된 이벤트의 수를 정의 하지만 연결 된 이벤트를 직접 사용 하거나 처리 하는 시나리오는 매우 제한적입니다. 일반적으로 연결 된 이벤트는 아키텍처 용도로 사용 되지만 연결 되지 않은 (CLR 이벤트 "래퍼"로 지원) 라우트된 이벤트에 전달 됩니다.  
  
 예를 들어 XAML 또는 코드에서 <xref:System.Windows.Input.Mouse.MouseDown?displayProperty=nameWithType> 연결 된 이벤트 구문을 처리 하는 <xref:System.Windows.UIElement> 대신 <xref:System.Windows.UIElement> 를 사용 <xref:System.Windows.UIElement.MouseDown> 하 여 지정 된에서 기본 연결 된 이벤트를 보다 쉽게 처리할 수 있습니다. 입력 디바이스의 향후 확장을 허용하므로 연결된 이벤트는 아키텍처의 용도로 사용됩니다. 가상 장치는 마우스 입력을 시뮬레이션 하기 <xref:System.Windows.Input.Mouse.MouseDown?displayProperty=nameWithType> 위해 발생 해야 하며, 이렇게 하려면에서 <xref:System.Windows.Input.Mouse> 파생 될 필요가 없습니다. 그러나이 시나리오에는 이벤트의 코드 처리가 포함 되며 연결 된 이벤트의 XAML 처리는이 시나리오와 관련이 없습니다.  
  
<a name="Handling"></a>   
## <a name="handling-an-attached-event-in-wpf"></a>WPF에서 연결된 이벤트 처리  
 연결된 이벤트를 처리하기 위한 프로세스 및 작성할 처리기 코드는 기본적으로 라우트된 이벤트의 경우와 동일합니다.  
  
 일반적으로 WPF 연결 된 이벤트는 WPF 라우트된 이벤트와 크게 다르지 않습니다. 이러한 차이점은 이벤트가 발생 하는 방법 및 클래스에서 멤버로 노출 되는 방법 (XAML 처리기 구문에도 영향을 줌)입니다.  
  
 그러나 앞에서 설명한 대로 기존 WPF 연결 된 이벤트는 특히 WPF에서 처리 하기 위한 것이 아닙니다. 이벤트의 목적은 합성 이벤트가 작성 시 부모 요소에 상태를 보고할 수 있게 하는 것으로, 이 경우 이벤트는 일반적으로 코드에서 발생하며 관련 부모 클래스에서 처리하는 클래스에도 사용됩니다. 예를 <xref:System.Windows.Controls.Primitives.Selector> 들어 내의 항목은 연결 <xref:System.Windows.Controls.Primitives.Selector.Selected> 된 이벤트를 발생 시켜야 합니다 .이 이벤트는 <xref:System.Windows.Controls.Primitives.Selector> 클래스에서 처리 된 다음 클래스에 의해 <xref:System.Windows.Controls.Primitives.Selector> 다른 라우트된 이벤트 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 로 변환 될 수 있습니다. . 라우트된 이벤트 및 클래스 처리에 대한 자세한 내용은 [라우트된 이벤트를 처리된 것으로 표시 및 클래스 처리](marking-routed-events-as-handled-and-class-handling.md)를 참조하십시오.  
  
<a name="Custom"></a>   
## <a name="defining-your-own-attached-events-as-routed-events"></a>연결된 이벤트를 라우트된 이벤트로 정의  
 공용 WPF 기본 클래스에서 파생 하는 경우 클래스에 특정 패턴 메서드를 포함 하 고 기본 클래스에 이미 있는 유틸리티 메서드를 사용 하 여 사용자 고유의 연결 된 이벤트를 구현할 수 있습니다.  
  
 패턴은 다음과 같습니다.  
  
- 메서드는 두 개의 매개 변수를 사용 하 여 __*EventName*처리기를 추가__ 합니다. 첫 번째 매개 변수는 이벤트 처리기가 추가 되는 인스턴스입니다. 두 번째 매개 변수는 추가할 이벤트 처리기입니다. 메서드는 반환 값 `public` 이 `static`없는 및 여야 합니다.  
  
- 메서드는 두 개의 매개 변수를 사용 하 여 __*EventName*처리기를 제거__ 합니다. 첫 번째 매개 변수는 이벤트 처리기가 제거 되는 인스턴스입니다. 두 번째 매개 변수는 제거할 이벤트 처리기입니다. 메서드는 반환 값 `public` 이 `static`없는 및 여야 합니다.  
  
 __Add*EventName*handler__ accessor 메서드는 요소에 연결 된 이벤트 처리기 특성이 선언 될 때 XAML 처리를 용이 하 게 합니다. __Add*eventname*Handler__ 및 __Remove*eventname*handler__ 메서드를 사용 하 여 연결 된 이벤트에 대 한 이벤트 처리기 저장소에 코드에 액세스할 수도 있습니다.  
  
 지정 된 XAML 판독기 구현에는 지원 언어 및 아키텍처의 기본 이벤트를 식별 하는 데 서로 다른 체계가 있을 수 있으므로이 일반적인 패턴은 프레임 워크의 실용적인 구현에 충분 하지 않습니다. 이는 WPF가 연결 된 이벤트를 라우트된 이벤트로 구현 하는 이유 중 하나입니다. 이벤트에 사용할 식별자 (<xref:System.Windows.RoutedEvent>)는 WPF 이벤트 시스템에 의해 이미 정의 되어 있습니다. 또한 이벤트 라우팅은 연결 된 이벤트의 XAML 언어 수준 개념에 대 한 자연 스러운 구현 확장입니다.  
  
 WPF 연결 된 이벤트에 대 한 __추가*EventName*처리기__ 구현은 라우트된 이벤트와 <xref:System.Windows.UIElement.AddHandler%2A> 처리기를 인수로 사용 하 여를 호출 하는 것으로 구성 됩니다.  
  
 일반적으로이 구현 전략과 라우트된 이벤트 시스템은 해당 클래스만 구현을 가지 <xref:System.Windows.UIElement> <xref:System.Windows.UIElement.AddHandler%2A> 므로 파생 <xref:System.Windows.ContentElement> 클래스나 파생 클래스에 연결 된 이벤트에 대 한 처리를 제한 합니다.  
  
 예를 들어 다음 코드는 연결 된 `NeedsCleaning` 이벤트를 라우트된 이벤트로 선언 `Aquarium`하는 WPF 연결 이벤트 전략을 사용 하 여 owner 클래스에서 연결 된 이벤트를 정의 합니다.  
  
 [!code-csharp[WPFAquariumSln#AECode](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#aecode)]
 [!code-vb[WPFAquariumSln#AECode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#aecode)]  
  
 연결 된 이벤트 식별자 필드 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A>를 설정 하는 데 사용 되는 메서드는 실제로 연결 되지 않은 라우트된 이벤트를 등록 하는 데 사용 되는 메서드와 동일 합니다. 연결된 이벤트 및 라우트된 이벤트 모두 중앙 집중화된 내부 저장소에 등록됩니다. 이 이벤트 저장소 구현은 [라우트된 이벤트 개요](routed-events-overview.md)에서 설명하는 “인터페이스로서의 이벤트” 개념 고려 사항을 사용합니다.  
  
<a name="Raising"></a>   
## <a name="raising-a-wpf-attached-event"></a>WPF 연결된 이벤트 발생  
 일반적으로 코드에서 기존 WPF 정의 연결 된 이벤트를 발생 시킬 필요가 없습니다. 이러한 이벤트는 일반적인 "서비스" 개념적 모델을 따르고와 같은 <xref:System.Windows.Input.InputManager> 서비스 클래스는 이벤트 발생을 담당 합니다.  
  
 그러나 기반 <xref:System.Windows.RoutedEvent>으로 연결 된 이벤트의 WPF 모델을 기반으로 사용자 지정 연결 된 이벤트를 정의 하는 경우를 사용 <xref:System.Windows.UIElement.RaiseEvent%2A> 하 여 <xref:System.Windows.UIElement> 또는 <xref:System.Windows.ContentElement>에서 연결 된 이벤트를 발생 시킬 수 있습니다. 라우트된 이벤트 (연결 됨 또는 없음)를 발생 시키려면 요소 트리에서 특정 요소를 이벤트 소스로 선언 해야 합니다. 해당 소스는 <xref:System.Windows.UIElement.RaiseEvent%2A> 호출자로 보고 됩니다. 트리에서 소스로 보고되는 요소 판별은 서비스에 따라 다릅니다.  
  
## <a name="see-also"></a>참고자료

- [라우트된 이벤트 개요](routed-events-overview.md)
- [XAML 구문 정보](xaml-syntax-in-detail.md)
- [WPF에 대한 XAML 및 사용자 지정 클래스](xaml-and-custom-classes-for-wpf.md)
