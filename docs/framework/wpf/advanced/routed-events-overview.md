---
title: 라우트된 이벤트 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- attached events [WPF]
- grouped button set [WPF]
- routed events [WPF]
- events [WPF], routed
- tunneling [WPF]
- events [WPF], attached
- routing strategies for events [WPF]
- button set [WPF], grouped
- bubbling [WPF]
ms.assetid: 1a2189ae-13b4-45b0-b12c-8de2e49c29d2
ms.openlocfilehash: 24fa283ec0c1fef2023845df0a05c3f1ebf5df06
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68400759"
---
# <a name="routed-events-overview"></a>라우트된 이벤트 개요

이 항목에서는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서 라우트된 이벤트의 개념을 설명합니다. 이 항목에서는 라우트된 이벤트 용어를 정의하고, 라우트된 이벤트가 요소 트리를 통해 라우트되는 방식을 설명하고, 라우트된 이벤트를 처리하는 방법을 요약하고, 자체 사용자 지정 라우트된 이벤트를 만드는 방법을 소개합니다.

<a name="prerequisites"></a>

## <a name="prerequisites"></a>전제 조건

이 항목에서는 CLR (공용 언어 런타임) 및 개체 지향 프로그래밍에 대 한 기본 지식이 있다고 가정 하 고 요소 간의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 관계를 트리로 개념화 하는 방법에 대 한 개념을 설명 합니다. 이 항목의 예제를 따르려면 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]을 이해하고 매우 기본적인 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애플리케이션 또는 페이지를 작성하는 방법을 알아야 합니다. 자세한 내용은 [연습: 내 첫 번째 wpf 데스크톱](../getting-started/walkthrough-my-first-wpf-desktop-application.md) 응용 프로그램 및 [XAML 개요 (wpf)](xaml-overview-wpf.md)

<a name="routing"></a>

## <a name="what-is-a-routed-event"></a>라우트된 이벤트란?

기능 또는 구현 측면에서 라우트된 이벤트를 살펴볼 수 있습니다. 사용자마다 더 유용하다고 생각하는 정의가 다르므로 여기에서는 두 가지 정의를 모두 제공합니다.

함수 정의: 라우트된 이벤트는 이벤트를 발생 시킨 개체 뿐만 아니라 요소 트리의 여러 수신기에서 처리기를 호출할 수 있는 이벤트 형식입니다.

구현 정의: 라우트된 이벤트는 <xref:System.Windows.RoutedEvent> 클래스의 인스턴스에서 지원 되 고 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 이벤트 시스템에서 처리 되는 CLR 이벤트입니다.

일반적인 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애플리케이션에는 많은 요소가 포함됩니다. 코드로 만들어지든지, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에 선언되든지 관계없이 이러한 요소는 서로에 대한 요소 트리 관계로 존재합니다. 이벤트 경로는 이벤트 정의에 따라 두 방향 중 하나로 이동할 수 있지만, 일반적으로 경로는 소스 요소부터 이동하여 요소 트리 루트(일반적으로 페이지 또는 창)에 도달할 때까지 요소 트리를 통해 위쪽으로 "버블링"됩니다. 이전에 DHTML 개체 모델을 사용했다면 이 버블링 개념이 익숙할 것입니다.

다음 간단한 요소 트리를 살펴보세요.

[!code-xaml[EventOvwSupport#GroupButton](~/samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml#groupbutton)]

이 요소 트리는 다음과 같은 항목을 생성합니다.

![예, 아니요 및 취소 단추](./media/routedevent-ovw-1.gif "RoutedEvent_ovw_1")

이 간소화 된 요소 트리에서 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트의 소스는 <xref:System.Windows.Controls.Button> 요소 <xref:System.Windows.Controls.Button> 중 하나 이며 클릭 한 것은 이벤트를 처리할 수 있는 첫 번째 요소입니다. 그러나에 연결 <xref:System.Windows.Controls.Button> 된 처리기가 이벤트에 대해 작동 하지 않는 경우이 이벤트는 요소 <xref:System.Windows.Controls.StackPanel>트리의 <xref:System.Windows.Controls.Button> 부모 ()로 위쪽으로 버블링 됩니다. 잠재적으로 이벤트는로 <xref:System.Windows.Controls.Border>버블링 된 다음 요소 트리의 페이지 루트 (표시 되지 않음)로 표시 됩니다.

즉,이 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트에 대 한 이벤트 경로는 다음과 같습니다.

Button-->StackPanel-->Border-->...

### <a name="top-level-scenarios-for-routed-events"></a>라우트된 이벤트에 대한 최상위 시나리오

다음은 라우트된 이벤트 개념에 대해 동기를 받은 시나리오와 일반적인 CLR 이벤트가 이러한 시나리오에 적합 하지 않은 이유에 대 한 간략 한 요약입니다.

**컨트롤 컴퍼지션 및 캡슐화:** 의 다양 한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤에는 풍부한 콘텐츠 모델이 있습니다. 예를 들어, 단추의 시각적 트리를 효과적으로 확장 <xref:System.Windows.Controls.Button>하는의 내에 이미지를 놓을 수 있습니다. 그러나 추가 된 이미지는 사용자가 기술적으로 이미지의 일부인 픽셀을 클릭 하더라도 단추가 해당 콘텐츠의에 응답 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 하 게 하는 적중 테스트 동작을 중단 하면 안 됩니다.

**단일 처리기 첨부 파일 위치:** [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]에서는 여러 요소에서 발생할 수 있는 이벤트를 처리 하기 위해 동일한 처리기를 여러 번 연결 해야 합니다. 라우트된 이벤트를 사용하면 이전 예제에서 살펴본 것처럼 해당 처리기를 한 번만 연결하고 처리기 논리를 사용하여 필요한 경우 이벤트가 발생한 위치를 확인할 수 있습니다. 예를 들어 이것은 이전에 표시된 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에 대한 처리기일 수 있습니다.

[!code-csharp[EventOvwSupport#GroupButtonCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml.cs#groupbuttoncodebehind)]
[!code-vb[EventOvwSupport#GroupButtonCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EventOvwSupport/visualbasic/default.xaml.vb#groupbuttoncodebehind)]

**클래스 처리:** 라우트된 이벤트는 클래스로 정의 된 정적 처리기를 허용 합니다. 이 클래스 처리기는 연결된 인스턴스 처리기보다 먼저 이벤트를 처리할 수 있습니다.

**리플렉션을 사용 하지 않고 이벤트 참조:** 특정 코드 및 태그 기술에는 특정 이벤트를 식별 하는 방법이 필요 합니다. 라우트된 이벤트는 필드를 <xref:System.Windows.RoutedEvent> 식별자로 만들며,이를 통해 정적 또는 런타임 리플렉션이 필요 하지 않은 강력한 이벤트 식별 기법을 사용할 수 있습니다.

### <a name="how-routed-events-are-implemented"></a>라우트된 이벤트를 구현하는 방법

라우트된 이벤트는 <xref:System.Windows.RoutedEvent> 클래스의 인스턴스에서 지원 되 고 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 이벤트 시스템에 등록 된 CLR 이벤트입니다. 등록에서 가져온 `public` `static` `readonly` 인스턴스는 일반적으로 라우트된 이벤트를 등록 하 고 "소유" 하는 클래스의 필드 멤버로 유지 됩니다. <xref:System.Windows.RoutedEvent> 동일 하 게 명명 된 clr 이벤트 ("래퍼" 이벤트 라고도 함)에 대 한 연결은 CLR 이벤트에 대 한 `add` 및 `remove` 구현을 재정의 하 여 수행 됩니다. 일반적으로 `add` 및 `remove`는 해당 이벤트의 처리기를 추가 및 제거하기 위한 적절한 언어별 이벤트 구문을 사용하는 암시적 기본값으로 남아 있습니다. 라우트된 이벤트 지원 및 연결 메커니즘은 개념적으로 종속성 속성이 <xref:System.Windows.DependencyProperty> 클래스에서 지원 되 고 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 속성 시스템에 등록 된 CLR 속성인 것과 비슷합니다.

`Tap` 다음 예제에서는 <xref:System.Windows.RoutedEvent> 식별자 필드 `add` 의 등록과 노출 및 `Tap` CLR 이벤트에 대 한 및 `remove` 구현을 포함 하 여 사용자 지정 라우트된 이벤트에 대 한 선언을 보여 줍니다.

[!code-csharp[RoutedEventCustom#AddRemoveHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventCustom/CSharp/SDKSampleLibrary/class1.cs#addremovehandler)]
[!code-vb[RoutedEventCustom#AddRemoveHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventCustom/VB/SDKSampleLibrary/Class1.vb#addremovehandler)]

### <a name="routed-event-handlers-and-xaml"></a>라우트된 이벤트 처리기 및 XAML

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]을 사용하여 이벤트 처리기를 추가하려면 이벤트 이름을 이벤트 수신기인 요소의 특성으로 선언합니다. 특성 값은 구현된 처리기 메서드의 이름으로, 코드 숨김 파일의 partial 클래스에 있어야 합니다.

[!code-xaml[EventOvwSupport#SimplestSyntax](~/samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml#simplestsyntax)]

라우트된 이벤트 처리기를 추가 하기 위한 구문은라우트된이벤트처리기를추가하는것과같습니다.여기에는라우트된이벤트구현을포함하는clr이벤트래퍼에처리기를추가하는것이중요합니다.[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]의 이벤트 처리기 추가에 대한 자세한 내용은 [XAML 개요(WPF)](xaml-overview-wpf.md)를 참조하세요.

<a name="routing_strategies"></a>

## <a name="routing-strategies"></a>라우트 전략

라우트된 이벤트는 다음 세 가지 라우트 전략 중 하나를 사용합니다.

- **버블링** 이벤트 원본에 대 한 이벤트 처리기가 호출 됩니다. 라우트된 이벤트는 요소 트리 루트에 도달할 때까지 다음 부모 요소로 라우트됩니다. 대부분의 라우트된 이벤트는 버블링 라우트 전략을 사용합니다. 버블링 라우트된 이벤트는 일반적으로 개별 컨트롤 또는 기타 UI 요소에서 입력 또는 상태 변경을 보고하는 데 사용됩니다.

- **계좌** 소스 요소 자체에는 응답으로 처리기를 호출할 수 있는 기회가 제공 됩니다. 이 전략은 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]에서 이벤트에 사용하는 “라우트”와 비슷합니다. 그러나 표준 CLR 이벤트와는 달리 직접 라우트된 이벤트는 클래스 처리를 지원 합니다. 클래스 처리는 이후 섹션에서 설명 하 고 및 <xref:System.Windows.EventSetter> <xref:System.Windows.EventTrigger>에서 사용할 수 있습니다.

- **터널링** 처음에는 요소 트리 루트에 있는 이벤트 처리기가 호출 됩니다. 그 다음에 라우트된 이벤트는 경로를 따라 있는 다음 자식 요소를 통해 경로를 이동하여 라우트된 이벤트 소스인 노드 요소(라우트된 이벤트를 발생시킨 요소)를 향합니다. 터널링 라우트된 이벤트는 보통 컨트롤 합치기의 일부로 사용 또는 처리되므로 복합 부분의 이벤트가 의도적으로 전체 컨트롤에 관련된 이벤트에 의해 억제되거나 대체될 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 제공된 입력 이벤트는 터널링/버블링 쌍으로 구현됩니다. 쌍에 사용되는 명명 규칙 때문에 터널링 이벤트를 미리 보기 이벤트라고도 합니다.

<a name="why_use"></a>

## <a name="why-use-routed-events"></a>라우트된 이벤트를 사용하는 이유는 무엇인가요?

애플리케이션 개발자가 항상 처리 중인 이벤트가 라우트된 이벤트로 구현되는지 알거나 주의할 필요는 없습니다. 라우트된 이벤트에는 특별한 동작이 있지만 이벤트가 발생한 요소에서 해당 이벤트를 처리할 경우 이 동작은 대체로 표시되지 않습니다.

공통 루트에서 공통 처리기 정의, 자체 컨트롤 합치기 또는 자체 사용자 지정 컨트롤 클래스 정의와 같은 제안된 시나리오를 사용할 경우 라우트된 이벤트가 강력해집니다.

라우트된 이벤트 수신기와 라우트된 이벤트 소스는 계층 구조에서 공통 이벤트를 공유할 필요가 없습니다. 모든 <xref:System.Windows.UIElement> 또는<xref:System.Windows.ContentElement> 는 모든 라우트된 이벤트에 대 한 이벤트 수신기 일 수 있습니다. 따라서 작업 API 집합 전체에서 사용할 수 있는 전체 라우트된 이벤트 집합을 응용 프로그램의 서로 다른 요소가 이벤트 정보를 교환할 수 있는 개념 "인터페이스"로 사용할 수 있습니다. 라우트된 이벤트에 대한 이 “인터페이스” 개념은 특히 입력 이벤트에 적합합니다.

이벤트에 대한 이벤트 데이터는 경로의 각 요소에 대해 지속되기 때문에 라우트된 이벤트는 요소 트리를 통해 통신하는 데도 사용될 수 있습니다. 하나의 요소가 이벤트 데이터의 무엇인가를 변경할 수 있고 해당 변경은 경로의 다음 요소에 사용할 수 있습니다.

라우팅 측면 외에도 지정 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 된 이벤트를 표준 CLR 이벤트 대신 라우트된 이벤트로 구현할 수 있는 두 가지 다른 이유가 있습니다. 자체 이벤트를 구현할 경우 다음 원칙을 고려할 수도 있습니다.

- 및<xref:System.Windows.EventSetter> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 와같은특정스타일지정및템플릿기능을통해참조되는이벤트를라우트된이벤트로<xref:System.Windows.EventTrigger> 지정 해야 합니다. 이는 앞에서 언급한 이벤트 식별자 시나리오입니다.

- 라우트된 이벤트는 등록된 인스턴스 처리기가 라우트된 이벤트에 액세스하기 전에 클래스가 라우트된 이벤트를 처리할 기회를 가지는 정적 메서드를 지정하는 데 사용될 수 있는 클래스 처리 메커니즘을 지원합니다. 이 메커니즘은 컨트롤 디자인에서 매우 유용합니다. 클래스는 이벤트가 인스턴스에서 처리되어 실수로 억제될 수 있는 이벤트 기반 클래스 동작을 강제 실행할 수 있기 때문입니다.

위 고려 사항은 각각 이 항목의 개별 섹션에서 설명합니다.

<a name="event_handing"></a>

## <a name="adding-and-implementing-an-event-handler-for-a-routed-event"></a>라우트된 이벤트에 대한 이벤트 처리기 추가 및 구현

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서 이벤트 처리기를 추가하려면 이벤트 이름을 요소에 특성으로 추가하고 특성 값을 다음 예제와 같이 적절한 대리자를 구현하는 이벤트 처리기의 이름으로 설정하면 됩니다.

[!code-xaml[EventOvwSupport#SimplestSyntax](~/samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml#simplestsyntax)]

`b1SetColor`이벤트를 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 처리 하는 코드를 포함 하는 구현 된 처리기의 이름입니다. `b1SetColor`는 <xref:System.Windows.RoutedEventHandler> 이벤트<xref:System.Windows.Controls.Primitives.ButtonBase.Click> 에 대 한 이벤트 처리기 대리자 인 대리자와 동일한 시그니처를 가져야 합니다. 모든 라우트된 이벤트 처리기 대리자의 첫 번째 매개 변수는 이벤트 처리기가 추가되는 요소를 지정하고 두 번째 매개 변수는 이벤트에 대한 데이터를 지정합니다.

[!code-csharp[EventOvwSupport#SimpleHandlerA](~/samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml.cs#simplehandlera)]
[!code-vb[EventOvwSupport#SimpleHandlerA](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EventOvwSupport/visualbasic/default.xaml.vb#simplehandlera)]

<xref:System.Windows.RoutedEventHandler>는 기본 라우트된 이벤트 처리기 대리자입니다. 특정 컨트롤 또는 시나리오에 특수화된 라우트된 이벤트의 경우 라우트된 이벤트 처리기에 사용할 대리자는 더 특수화되어 특수화된 이벤트 데이터를 전송할 수 있습니다. 예를 들어 일반적인 입력 시나리오에서 <xref:System.Windows.UIElement.DragEnter> 라우트된 이벤트를 처리할 수 있습니다. 처리기에서 대리자를 <xref:System.Windows.DragEventHandler> 구현 해야 합니다. 가장 구체적인 대리자를 사용 하 여 처리기에서를 <xref:System.Windows.DragEventArgs> 처리 하 고 끌기 작업의 클립보드 페이로드를 포함 하는 <xref:System.Windows.DragEventArgs.Data%2A> 속성을 읽을 수 있습니다.

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]을 사용하여 이벤트 처리기를 요소에 추가하는 방법의 전체 예제를 보려면 [라우트된 이벤트 처리](how-to-handle-a-routed-event.md)를 참조하세요.

코드로 만들어진 애플리케이션에 라우트된 이벤트에 대한 처리기를 추가하는 방법은 간단합니다. 라우트된 이벤트 처리기는 항상 기존 백업에서 <xref:System.Windows.UIElement.AddHandler%2A> `add`호출 하는 것과 동일한 메서드인 도우미 메서드를 통해 추가할 수 있습니다. 하지만 기존 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 라우트된 이벤트에는 일반적으로 언어별 이벤트 구문(도우미 메서드보다 더 직관적인 구문)을 통해 라우트된 이벤트에 대한 처리기를 추가할 수 있는 `add` 및 `remove` 논리의 지원 구현이 포함됩니다. 도우미 메서드 사용 예제는 다음과 같습니다.

[!code-csharp[EventOvwSupport#AddHandlerCode](~/samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml.cs#addhandlercode)]
[!code-vb[EventOvwSupport#AddHandlerCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EventOvwSupport/visualbasic/default.xaml.vb#addhandlercode)]

다음 예에서는 C# 연산자 Visual Basic 구문을 보여 줍니다. 역참조를 처리 하기 때문에 연산자 구문이 약간 다릅니다.

[!code-csharp[EventOvwSupport#AddHandlerPlusEquals](~/samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml.cs#addhandlerplusequals)]
[!code-vb[EventOvwSupport#AddHandlerPlusEquals](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EventOvwSupport/visualbasic/default.xaml.vb#addhandlerplusequals)]

이벤트 처리기를 코드에 추가하는 방법의 예제를 보려면 [코드를 사용하여 이벤트 처리기 추가](how-to-add-an-event-handler-using-code.md)를 참조하세요.

Visual Basic를 사용 하는 경우 `Handles` 키워드를 사용 하 여 처리기를 처리기 선언의 일부로 추가할 수도 있습니다. 자세한 내용은 [Visual Basic 및 WPF 이벤트 처리](visual-basic-and-wpf-event-handling.md)를 참조하세요.

<a name="concept_handled"></a>

### <a name="the-concept-of-handled"></a>Handled 개념

모든 라우트된 이벤트는 공용 이벤트 데이터 기본 클래스인을 <xref:System.Windows.RoutedEventArgs>공유 합니다. <xref:System.Windows.RoutedEventArgs>부울 값을 사용 하는 속성을정의합니다.<xref:System.Windows.RoutedEventArgs.Handled%2A> <xref:System.Windows.RoutedEventArgs.Handled%2A> 속성의 목적은의 <xref:System.Windows.RoutedEventArgs.Handled%2A> 값을로 `true`설정 하 여 경로를 따라 라우트된 이벤트를 *처리*된 것으로 표시 하는 이벤트 처리기를 사용 하도록 설정 하는 것입니다. 경로를 따라 있는 한 요소에 있는 처리기에서 처리된 후 공유된 이벤트 데이터는 다시 경로를 따라 있는 각 수신기에 보고됩니다.

값은 경로 <xref:System.Windows.RoutedEventArgs.Handled%2A> 를 따라 추가로 이동할 때 라우트된 이벤트를 보고 하거나 처리 하는 방법에 영향을 줍니다. <xref:System.Windows.RoutedEventArgs.Handled%2A> 가`true` 라우트된 이벤트에 대 한 이벤트 데이터에 있으면 다른 요소에서 해당 라우트된 이벤트를 수신 하는 처리기는 일반적으로 해당 특정 이벤트 인스턴스에 대해 더 이상 호출 되지 않습니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서 연결된 처리기 및 `+=` 또는 `Handles`와 같은 언어별 이벤트 처리기 연결 구문을 통해 추가된 처리기에도 이 내용이 적용됩니다. 대부분의 일반적인 처리기 시나리오에서을로 <xref:System.Windows.RoutedEventArgs.Handled%2A> `true` 설정 하 여 이벤트를 처리 된 것으로 표시 하면 터널링 경로 또는 버블링 경로에 대 한 라우팅을 "중지" 하 고 클래스 처리기에 의해 경로의 지점에서 처리 되는 모든 이벤트에 대해 "중지" 됩니다.

그러나 수신기가 이벤트 데이터 <xref:System.Windows.RoutedEventArgs.Handled%2A> `true` 에 있는 라우트된 이벤트에 대 한 응답으로 처리기를 계속 실행할 수 있는 "handledEventsToo" 메커니즘이 있습니다. 즉, 이벤트 데이터를 처리됨으로 표시해도 실제로 이벤트 경로는 중지되지 않습니다. 코드 또는에서 <xref:System.Windows.EventSetter>handledEventsToo 메커니즘도 사용할 수 있습니다.

- 코드에서 일반적인 CLR 이벤트에 대해 작동 하는 언어별 이벤트 구문을 사용 하는 대신 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 메서드 <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 를 호출 하 여 처리기를 추가 합니다. `handledEventsToo` 값을 `true`로 지정합니다.

- 에서 특성을 로`true`설정 합니다. <xref:System.Windows.EventSetter.HandledEventsToo%2A> <xref:System.Windows.EventSetter>

<xref:System.Windows.RoutedEventArgs.Handled%2A> 의<xref:System.Windows.RoutedEventArgs.Handled%2A> 개념은 라우트된 이벤트에서 상태가 생성 하는 동작 외에도 응용 프로그램을 디자인 하 고 이벤트 처리기 코드를 작성 하는 방법에 영향을 줍니다. 라우트된 이벤트에 <xref:System.Windows.RoutedEventArgs.Handled%2A> 의해 노출 되는 단순한 프로토콜로 이해할 수 있습니다. 이 프로토콜을 사용 하는 정확한 방법은 사용자에 게 적합 하지만의 <xref:System.Windows.RoutedEventArgs.Handled%2A> 값을 사용 하는 방법에 대 한 개념 디자인은 다음과 같습니다.

- 라우트된 이벤트가 처리됨으로 표시되면 해당 경로를 따라 있는 다른 요소가 해당 라우트된 이벤트를 다시 처리할 필요가 없습니다.

- 라우트된 이벤트가 처리 된 것으로 표시 되지 않은 경우 경로를 따라 이전에 있던 다른 수신기가 처리기를 등록 하지 않거나 등록 된 처리기가 이벤트 데이터를 조작 하 고로 <xref:System.Windows.RoutedEventArgs.Handled%2A> `true`설정 하지 않도록 선택 했습니다. 또는 현재 수신기가 경로의 첫 번째 지점일 수도 있습니다. 이제 현재 수신기의 처리기에는 세 가지 가능한 작업 과정이 있습니다.

  - 아무 작업도 수행하지 않습니다. 이벤트는 처리되지 않고 다음 수신기로 라우트됩니다.

  - 이벤트에 대한 응답으로 코드를 실행하지만 수행된 작업이 이벤트를 처리됨으로 표시하도록 보장할 만큼 충분히 효과적인지에 대한 결정을 내립니다. 이벤트는 다음 수신기로 라우트됩니다.

  - 이벤트에 대한 응답으로 코드를 실행합니다. 처리기에 전달된 이벤트 데이터에서 이벤트를 처리됨으로 표시합니다. 이는 수행된 작업이 처리됨으로 표시하도록 보장할 만큼 충분히 효과적이라고 생각되기 때문입니다. 이벤트는 계속 해 서 다음 수신기로 라우트 하지만 이벤트 <xref:System.Windows.RoutedEventArgs.Handled%2A> 데이터에서를 사용 = `true` 하 여 수신기 `handledEventsToo` 만 추가 처리기를 호출할 수 있습니다.

이 개념 디자인은 앞에서 언급 한 라우팅 동작에 의해 강화 됩니다. 경로를 따라 이전 처리기가 이미 설정 <xref:System.Windows.RoutedEventArgs.Handled%2A>된경우에도호출되는라우트된이벤트에대한처리기를연결하는것이더어렵거나(코드또는스타일에서도가능하지만) to`true`.

에 <xref:System.Windows.RoutedEventArgs.Handled%2A>대 한 자세한 내용, 라우트된 이벤트의 클래스 처리 및 라우트된 이벤트를로 <xref:System.Windows.RoutedEventArgs.Handled%2A>표시 하는 것이 적절 한 경우에 대 한 권장 사항은 [라우트된 이벤트를 처리 된 것으로 표시 및 클래스 처리](marking-routed-events-as-handled-and-class-handling.md)를 참조 하세요.

애플리케이션에서는 일반적으로 버블링 라우트된 이벤트를 발생시킨 개체에서 이 이벤트를 처리하며 이벤트의 라우트 특징은 전혀 관련이 없습니다. 하지만 요소 트리에서 더 위쪽에 있는 요소에 같은 라우트된 이벤트에 대한 연결된 처리기가 있는 경우 예기치 않은 부작용을 방지하기 위해 이벤트 데이터에서는 라우트된 이벤트를 처리됨으로 표시하는 것이 좋습니다.

<a name="class_handlers"></a>

## <a name="class-handlers"></a>클래스 처리기

에서 <xref:System.Windows.DependencyObject>파생 되는 클래스를 정의 하는 경우 클래스의 선언 되거나 상속 된 이벤트 멤버인 라우트된 이벤트에 대 한 클래스 처리기를 정의 하 고 연결할 수도 있습니다. 라우트된 이벤트가 경로의 요소 인스턴스에 도달할 때마다 클래스 처리기는 해당 클래스의 인스턴스에 연결된 인스턴스 수신기 처리기보다 먼저 호출됩니다.

일부 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤에는 특정 라우트된 이벤트에 대한 고유 클래스 처리 기능이 있습니다. 이 기능을 사용하면 표면적으로는 라우트된 이벤트가 발생하지 않은 것처럼 보이지만 실제로는 클래스가 처리되는 것이고 특정 기술을 사용하면 라우트된 이벤트가 인스턴스 처리기에서 처리될 수 있습니다. 또한 많은 기본 클래스 및 컨트롤이 클래스 처리 동작을 재정의하는 데 사용될 수 있는 가상 메서드를 표시합니다. 원하지 않는 클래스 처리를 해결하는 방법 및 사용자 지정 클래스에서 자체 클래스 처리를 정의하는 방법에 대한 자세한 내용은 [라우트된 이벤트를 처리된 것으로 표시 및 클래스 처리](marking-routed-events-as-handled-and-class-handling.md)를 참조하세요.

<a name="attached_events"></a>

## <a name="attached-events-in-wpf"></a>WPF의 연결된 이벤트

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 언어는 *연결된 이벤트*라는 특수 이벤트 형식을 정의합니다. 연결된 이벤트를 사용하여 특정 이벤트에 대한 처리기를 임의 요소에 추가할 수 있습니다. 이벤트를 처리하는 요소는 연결된 이벤트를 정의하거나 상속할 필요가 없고 이벤트를 발생시키는 개체 및 인스턴스를 처리하는 대상은 모두 해당 이벤트를 클래스 멤버로 정의하거나 소유하면 안 됩니다.

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 입력 시스템은 연결된 이벤트를 광범위하게 사용합니다. 하지만 이러한 연결된 이벤트는 거의 모두 기본 요소를 통해 전달됩니다. 그 다음에 입력 이벤트는 기본 요소 클래스의 멤버인 해당하는 연결되지 않은 라우트된 이벤트로 표시됩니다. 예를 들어 또는 코드에서 <xref:System.Windows.Input.Mouse.MouseDown?displayProperty=nameWithType> <xref:System.Windows.UIElement.MouseDown> <xref:System.Windows.UIElement> <xref:System.Windows.UIElement> 연결[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 된 이벤트 구문을 처리 하는 대신를 사용 하 여 지정 된에서 기본 연결 된 이벤트를 보다 쉽게 처리할 수 있습니다.

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 연결된 이벤트에 대한 자세한 내용은 [연결된 이벤트 개요](attached-events-overview.md)를 참조하세요.

<a name="Qualifying_Event_Names_in_XAML_for_Anticipated_Routing"></a>

## <a name="qualified-event-names-in-xaml"></a>XAML의 정규화된 이벤트 이름

*typename*.*eventname* 연결된 이벤트 구문과 비슷하지만 엄격히 말하면 연결된 이벤트 사용이 아닌 또 다른 구문 사용은 자식 요소에서 발생한 라우트된 이벤트에 대한 처리기를 연결하는 경우입니다. 공통 부모에 관련 라우트된 이벤트가 멤버로 포함되지 않더라도 처리기를 공통 부모에 연결하면 이벤트 라우트를 이용할 수 있습니다. 이 예제를 다시 살펴보세요.

[!code-xaml[EventOvwSupport#GroupButton](~/samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml#groupbutton)]

여기서 처리기가 추가 <xref:System.Windows.Controls.StackPanel>되는 부모 요소 수신기는입니다. 그러나 선언 되었으며 <xref:System.Windows.Controls.Button> 클래스에서 발생 하는 라우트된 이벤트에 대 한 처리기를 추가 하는 것입니다 (<xref:System.Windows.Controls.Primitives.ButtonBase> 실제로는 이지만 상속을 <xref:System.Windows.Controls.Button> 통해 사용 가능). <xref:System.Windows.Controls.Button>이벤트를 "소유" 하지만 라우트된 이벤트 시스템은 라우트된 모든 이벤트에 대 한 처리기를 CLR (공용 언어 <xref:System.Windows.UIElement> 런타임 <xref:System.Windows.ContentElement> ) 이벤트에 대 한 수신기를 연결할 수 있는 모든 또는 인스턴스 수신기에 연결할 수 있습니다. 일반적으로 이러한 정규화된 이벤트 특성 이름에 대한 기본 xmlns 네임스페이스는 기본 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] xmlns 네임스페이스이지만 사용자 지정 라우트된 이벤트에 대한 접두사가 추가된 네임스페이스를 지정할 수도 있습니다. xmlns에 대한 자세한 내용은 [WPF XAML을 위한 XAML 네임스페이스 및 네임스페이스 매핑](xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)을 참조하세요.

<a name="how_event_processing_works"></a>

## <a name="wpf-input-events"></a>WPF 입력 이벤트

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 플랫폼 내에서 라우트된 이벤트가 자주 사용되는 한 가지 응용 프로그램은 입력 이벤트와 관련됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 터널링 라우트된 이벤트에는 규칙에 따라 "Preview"라는 단어가 접두사로 추가됩니다. 입력 이벤트는 보통 쌍으로 제공되고, 쌍 중 하나는 버블링 이벤트가 되고 다른 하나는 터널링 이벤트가 됩니다. 예 <xref:System.Windows.ContentElement.KeyDown> 를 들어 이벤트 <xref:System.Windows.ContentElement.PreviewKeyDown> 와 이벤트는 동일한 서명을 가지 며, 이전에는 버블링 입력 이벤트로, 후자는 터널링 입력 이벤트입니다. 입력 이벤트에 버블링 버전만 포함되거나 직접 라우트된 버전만 포함되는 경우도 있습니다. 문서의 라우트된 이벤트 항목에서는 라우트된 이벤트가 있는 경우 대체 라우트 전략을 통해 비슷한 라우트된 이벤트를 상호 참조하고 관리되는 참조 페이지의 섹션에서는 각 라우트된 이벤트의 라우트 전략을 설명합니다.

쌍으로 제공되는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 입력 이벤트는 마우스 단추 누르기와 같은 입력의 단일 사용자 작업이 해당 쌍의 라우트된 이벤트를 둘 다 순차적으로 발생시키도록 구현됩니다. 먼저 터널링 이벤트가 발생하고 경로를 이동합니다. 그 다음에 버블링 이벤트가 발생하고 경로를 이동합니다. 버블링 이벤트를 발생 시키는 구현 클래스의 <xref:System.Windows.UIElement.RaiseEvent%2A> 메서드 호출은 터널링 이벤트에서 이벤트 데이터를 수신 하 고 새 발생 이벤트에서 다시 사용할 수 있기 때문에 두 이벤트는 동일한 이벤트 데이터 인스턴스를 그대로 공유 합니다. 터널링 이벤트에 대한 처리기가 있는 수신기는 우선적으로 라우트된 이벤트를 처리됨으로 표시할 수 있습니다(클래스 처리기 우선, 그 다음에 인스턴스 처리기). 터널링 경로에 따라 있는 요소가 라우트된 이벤트를 처리됨으로 표시한 경우 버블링 이벤트에 대한 이미 처리된 이벤트 데이터가 전송되고 해당하는 버블링 입력 이벤트에 대한 일반 연결된 처리기는 호출되지 않습니다. 표면적으로는 처리된 버블링 이벤트가 발생하지 않은 경우처럼 보입니다. 이 처리 동작은 컨트롤 합치기에 유용합니다. 이 경우 모든 적중 테스트 기반 입력 이벤트나 포커스 기반 입력 이벤트를 복합 부분이 아닌 최종 컨트롤이 보고하도록 할 수 있습니다. 최종 컨트롤 요소는 합치기에서 루트에 더 근접하므로 터널링 이벤트를 먼저 클래스에서 처리하고 라우트된 이벤트를 컨트롤에 대한 관련성이 더 높은 이벤트(컨트롤 클래스를 지원하는 코드의 일부)로 “대체”할 수 있습니다.

입력 이벤트 처리가 적용되는 방식에 대한 그림으로 다음 입력 이벤트 예제를 살펴보겠습니다. 다음 트리 그림 `leaf element #2` 에서는 `PreviewMouseDown` 와 `MouseDown` 이벤트의 소스입니다.

![이벤트 라우팅 다이어그램](./media/routed-events-overview/input-event-routing.png)

이벤트 처리 순서는 다음과 같습니다.

1. 루트 요소의 `PreviewMouseDown`(터널링).

2. 중간 요소 #1의 `PreviewMouseDown`(터널링).

3. 소스 요소 #2의 `PreviewMouseDown`(터널링).

4. 소스 요소 #2의 `MouseDown`(버블링).

5. 중간 요소 #1의 `MouseDown`(버블링).

6. 루트 요소의 `MouseDown`(버블링).

라우트된 이벤트 처리기 대리자는 두 개체인, 이벤트를 발생시킨 개체 및 처리기가 호출된 개체에 대한 참조를 제공합니다. 처리기가 호출된 개체는 `sender` 매개 변수를 통해 보고된 개체입니다. 이벤트가 처음 발생 한 개체는 이벤트 데이터의 <xref:System.Windows.RoutedEventArgs.Source%2A> 속성에 의해 보고 됩니다. 라우트된 이벤트는 같은 개체에서 계속 발생 하 고 처리할 수 있습니다 .이 경우 `sender` 및 <xref:System.Windows.RoutedEventArgs.Source%2A> 는 동일 합니다 (이벤트 처리 예제 목록에서 3 단계 및 4 단계를 사용 하는 경우).

터널링 및 버블링으로 인해 부모 요소는 <xref:System.Windows.RoutedEventArgs.Source%2A> 이 자식 요소 중 하나인 입력 이벤트를 수신 합니다. 원본 요소를 파악 하는 것이 중요 한 경우 <xref:System.Windows.RoutedEventArgs.Source%2A> 속성에 액세스 하 여 원본 요소를 식별할 수 있습니다.

일반적으로 입력 이벤트가 표시 <xref:System.Windows.RoutedEventArgs.Handled%2A>되 면 추가 처리기가 호출 되지 않습니다. 보통은 입력 이벤트의 의미에 대한 애플리케이션별 논리 처리를 해결하는 처리기가 호출된 후 바로 입력 이벤트를 처리됨으로 표시해야 합니다.

상태에 대 한 <xref:System.Windows.RoutedEventArgs.Handled%2A> 이 일반적인 문의 예외는 이벤트 데이터의 상태를 의도적으로 무시 <xref:System.Windows.RoutedEventArgs.Handled%2A> 하도록 등록 된 입력 이벤트 처리기가 경로를 따라 계속 호출 된다는 것입니다. 자세한 내용은 [미리 보기 이벤트](preview-events.md) 또는 [라우트된 이벤트를 처리된 것으로 표시 및 클래스 처리](marking-routed-events-as-handled-and-class-handling.md)를 참조하세요.

터널링 이벤트와 버블링 이벤트 간에 공유된 이벤트 데이터 모델과 터널링 이벤트 다음에 버블링 이벤트가 발생하는 순차적 발생은 일반적으로 모든 라우트된 이벤트에 적용되는 개념이 아닙니다. 이 동작은 특별히 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 입력 디바이스가 입력 이벤트 쌍을 발생시키고 연결하도록 선택하는 방법을 통해 구현됩니다. 자체 입력 이벤트를 구현하는 것은 고급 시나리오이지만 자체 입력 이벤트에 대해 해당 모델을 따르도록 선택할 수도 있습니다.

특정 클래스는 대개 특정 사용자 기반 입력 이벤트가 해당 컨트롤 내에서 가지는 의미를 다시 정의하고 새 이벤트를 발생시키기 위해 특정 입력 이벤트를 클래스에서 처리하도록 선택합니다. 자세한 내용은 [라우트된 이벤트를 처리된 것으로 표시 및 클래스 처리](marking-routed-events-as-handled-and-class-handling.md)를 참조하세요.

입력 및 입력과 이벤트가 일반적인 애플리케이션 시나리오에서 상호 작용하는 방식에 대한 자세한 내용은 [입력 개요](input-overview.md)를 참조하세요.

<a name="events_styles"></a>

## <a name="eventsetters-and-eventtriggers"></a>EventSetter 및 EventTrigger

스타일에서를 <xref:System.Windows.EventSetter>사용 하 여 태그에 미리 선언 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 된 이벤트 처리 구문을 포함할 수 있습니다. 스타일이 적용되면 참조된 처리기가 스타일 지정된 인스턴스에 추가됩니다. 라우트된 이벤트에 대해서 <xref:System.Windows.EventSetter> 만를 선언할 수 있습니다. 다음은 예제입니다. 여기서 참조되는 `b1SetColor` 메서드는 코드 숨김 파일에 있습니다.

[!code-xaml[EventOvwSupport#XAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/page2.xaml#xaml2)]

여기에서 얻을 수 있는 이점은 응용 프로그램의 모든 단추에 적용 될 수 있는 다양 한 정보를 스타일에 포함할 수 있고 해당 스타일의 일부가 되도록 하면 <xref:System.Windows.EventSetter> 태그 수준 에서도 코드 재사용을 촉진 하는 것입니다. <xref:System.Windows.EventSetter> 또한 처리기에 대 한 메서드 이름이 일반 응용 프로그램 및 페이지 태그에서 한 단계 더 멀리 떨어져 있습니다.

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 의<xref:System.Windows.EventTrigger>라우트된 이벤트와 애니메이션 기능을 결합 하는 또 다른 특수화 된 구문은입니다. 와 <xref:System.Windows.EventSetter>마찬가지로 라우트된 이벤트만 <xref:System.Windows.EventTrigger>에 사용 될 수 있습니다. 일반적으로는 <xref:System.Windows.EventTrigger> 스타일의 일부로 선언 되지만는 <xref:System.Windows.EventTrigger> 페이지 수준 <xref:System.Windows.FrameworkElement.Triggers%2A> 요소에 대해 컬렉션의 일부로 선언 하거나에서 <xref:System.Windows.Controls.ControlTemplate>선언할 수도 있습니다. 를 사용 하면 라우트된 이벤트가 해당 <xref:System.Windows.Media.Animation.Storyboard> 이벤트 <xref:System.Windows.EventTrigger> 에 대해를 선언 하는 해당 경로에 있는 요소에 도달할 때마다 실행 되는를 지정할 수 있습니다. <xref:System.Windows.EventTrigger> 는 이벤트를 처리 <xref:System.Windows.EventTrigger> 하 고 기존 storyboard를 시작 하도록 하는 것에 비해는 스토리 보드 및 <xref:System.Windows.EventTrigger> 해당 런타임 동작에 대 한 보다 효율적인 제어를 제공 한다는 점입니다. 자세한 내용은 [Storyboard를 시작한 후 이벤트 트리거를 사용하여 제어](../graphics-multimedia/how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)를 참조하세요.

<a name="more_about"></a>

## <a name="more-about-routed-events"></a>라우트된 이벤트에 대한 추가 정보

이 항목에서는 기본 개념을 설명하고 다양한 기본 요소 및 컨트롤에 이미 있는 라우트된 이벤트에 응답하는 방법 및 시점에 대한 지침을 제공하는 관점에서 주로 라우트된 이벤트를 살펴봅니다. 하지만 특수화된 이벤트 데이터 클래스 및 대리자와 같은 모든 필요한 지원과 함께 사용자 지정 클래스에서 자체 라우트된 이벤트를 만들 수 있습니다. 라우트된 이벤트 소유자는 모든 클래스가 될 수 있지만, 라우트된 이벤트는에 의해 발생 하 고 <xref:System.Windows.UIElement> 또는 <xref:System.Windows.ContentElement> 파생 클래스에 의해 처리 되어야 유용 합니다. 사용자 지정 이벤트에 대한 자세한 내용은 [사용자 지정 라우트된 이벤트 만들기](how-to-create-a-custom-routed-event.md)를 참조하세요.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.EventManager>
- <xref:System.Windows.RoutedEvent>
- <xref:System.Windows.RoutedEventArgs>
- [라우트된 이벤트를 처리된 것으로 표시 및 클래스 처리](marking-routed-events-as-handled-and-class-handling.md)
- [입력 개요](input-overview.md)
- [명령 개요](commanding-overview.md)
- [사용자 지정 종속성 속성](custom-dependency-properties.md)
- [WPF의 트리](trees-in-wpf.md)
- [약한 이벤트 패턴](weak-event-patterns.md)
