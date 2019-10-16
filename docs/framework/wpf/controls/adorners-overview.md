---
title: 표시기 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adorners [WPF], about adorners
ms.assetid: 33d4c5c2-2daf-4e45-ba9a-5b673e2b8280
ms.openlocfilehash: d8e6e53edc92a2847c001377706d313cf97cced5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956104"
---
# <a name="adorners-overview"></a>표시기 개요
표시기는 사용자에 게 시각적 <xref:System.Windows.FrameworkElement>신호를 제공 하는 데 사용 되는 특수 한 형식입니다. 표시기는 다른 용도로 요소에 기능 핸들을 추가하거나 컨트롤에 대한 상태 정보를 제공하는 데 사용할 수 있습니다.  

<a name="about_Adorners"></a>   
## <a name="about-adorners"></a>표시기 정보  
 는에 <xref:System.Windows.FrameworkElement> 바인딩되<xref:System.Windows.UIElement>는 사용자 지정입니다. <xref:System.Windows.Documents.Adorner> 표시기는 항상 표시 된 <xref:System.Windows.Documents.AdornerLayer>요소 또는 표시 된 요소 컬렉션의 맨 위에 있는 렌더링 화면인에서 렌더링 됩니다. 표시기 렌더링은 표시기가 바인딩된의 렌더링과 <xref:System.Windows.UIElement> 독립적입니다. 표시기는 일반적으로 표시한 요소의 왼쪽 위에 있는 표준 2차원 좌표 원점을 사용하여, 바인딩되어 있는 요소에 상대적으로 배치됩니다.  
  
 표시기에 대한 일반 애플리케이션은 다음과 같습니다.  
  
- 사용자가 특정 방식으로 <xref:System.Windows.UIElement> 요소를 조작할 수 있게 하는 함수 핸들을에 추가 (크기 조정, 회전, 위치 변경 등) 합니다.  
  
- 다양한 상태를 나타내거나 다양한 이벤트에 대한 응답으로 시각적 피드백을 제공합니다.  
  
- 의 오버레이 시각적 장식 <xref:System.Windows.UIElement>입니다.  
  
- 의 일부 또는 전체를 <xref:System.Windows.UIElement>시각적으로 마스킹 또는 재정의 합니다.  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]는 시각적 요소를 표시하는 기본 프레임워크를 제공합니다. 다음 표에 개체 및 해당 용도를 표시할 때 사용되는 기본 유형이 나와 있습니다. 다음은 여러 사용법의 예입니다.  
  
|||  
|-|-|  
|<xref:System.Windows.Documents.Adorner>|모든 구체적인 표시기 구현이 상속받는 추상 기본 클래스입니다.|  
|<xref:System.Windows.Documents.AdornerLayer>|하나 이상의 표시한 요소의 표시기에 대한 렌더링 계층을 나타내는 클래스입니다.|  
|<xref:System.Windows.Documents.AdornerDecorator>|표시기 계층이 요소 컬렉션에 연결될 수 있도록 하는 클래스입니다.|  
  
<a name="implement_custom_Adorner"></a>   
## <a name="implementing-a-custom-adorner"></a>사용자 지정 표시기 구현  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서 제공하는 표시기 프레임워크는 기본적으로 사용자 지정 표시기의 생성을 지원하는 데 사용됩니다. 사용자 지정 표시기는 추상 <xref:System.Windows.Documents.Adorner> 클래스에서 상속 되는 클래스를 구현 하 여 만듭니다.  
  
> [!NOTE]
> 부모는 <xref:System.Windows.Documents.Adorner> 은 합니다 <xref:System.Windows.Documents.AdornerLayer> 렌더링 하는 <xref:System.Windows.Documents.Adorner>, 표시 되는 요소가 없습니다.  
  
 다음 예제에서는 간단한 표시기를 구현하는 클래스를 보여 줍니다. 예제 표시기는 단순히 원이 <xref:System.Windows.UIElement> 있는의 모퉁이를 원으로 합니다.  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_simplecircleadornerbody)]
 [!code-vb[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_simplecircleadornerbody)]  
  
 다음 이미지는에 적용 되 <xref:System.Windows.Controls.TextBox>는 SimpleCircleAdorner를 보여 줍니다.  
  
 ![표시 된 텍스트 상자를 표시 하는 스크린샷](./media/adorners-overview/simplecircleadorner-textbox.png)  
  
<a name="rendering_behavior_for_Adorners"></a>   
## <a name="rendering-behavior-for-adorners"></a>표시기에 대한 렌더링 동작  
 표시기에는 고유 렌더링 동작이 포함되어 있지 않음에 유의해야 합니다. 표시기를 렌더링하는 것은 표시기 구현자의 책임입니다.   렌더링 동작을 구현 하는 일반적인 방법은 메서드를 <xref:System.Windows.UIElement.OnRender%2A> 재정의 하 고 하나 <xref:System.Windows.Media.DrawingContext> 이상의 개체를 사용 하 여 필요에 따라 표시기의 시각적 개체를 렌더링 하는 것입니다 (위 예제에 표시 된 것 처럼).  
  
> [!NOTE]
> 표시기 계층에 배치된 모든 개체는 설정한 스타일의 나머지 부분 맨 위에 렌더링됩니다. 즉, 표시기는 시각적으로 항상 맨 위에 있으며 z-순서를 사용하여 재정의할 수 없습니다.  
  
<a name="adorner_events_hittest"></a>   
## <a name="events-and-hit-testing"></a>이벤트 및 적중 횟수 테스트  
 표시기는 다른 <xref:System.Windows.FrameworkElement>것 처럼 입력 이벤트를 수신 합니다.  표시기의 z 순서는 항상 원으로 요소 보다 더 높습니다. 표시기는 기본 표시 된 요소에 사용할 수 있는 입력 이벤트 <xref:System.Windows.UIElement.Drop> ( <xref:System.Windows.UIElement.MouseMove>예: 또는)를 수신 합니다.  표시기는 특정 입력 이벤트를 수신하고 이벤트를 다시 발생시켜 표시한 기본 요소에 전달할 수 있습니다.  
  
 표시기에서 요소에 대 한 통과 적중 테스트를 사용 하도록 설정 하려면 표시기에서 적중 <xref:System.Windows.UIElement.IsHitTestVisible%2A> 횟수 테스트 속성을 **false** 로 설정 합니다.  적중 횟수 테스트에 대한 자세한 내용은  
  
 [시각적 계층에서 적중 횟수 테스트](../graphics-multimedia/hit-testing-in-the-visual-layer.md)를 참조하세요.  
  
<a name="adorn_single_element"></a>   
## <a name="adorning-a-single-uielement"></a>단일 UIElement 표시  
 표시기를 특정 <xref:System.Windows.UIElement>에 바인딩하려면 다음 단계를 수행 합니다.  
  
1. 정적 메서드 <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> 를 호출 하 여 표시할 <xref:System.Windows.Documents.AdornerLayer> 에 대 한 <xref:System.Windows.UIElement> 개체를 가져옵니다. <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A>지정 <xref:System.Windows.UIElement>된에서 시작 하 여 시각적 트리를 탐색 하 고 찾은 첫 번째 표시기 계층을 반환 합니다. (표시기 계층이 없으면 메서드가 null을 반환합니다.)  
  
2. 메서드를 <xref:System.Windows.Documents.AdornerLayer.Add%2A> 호출 하 여 표시기를 대상 <xref:System.Windows.UIElement>에 바인딩합니다.  
  
 다음 예제에서는 SimpleCircleAdorner (위에 표시 됨) <xref:System.Windows.Controls.TextBox> 를 *mytextbox*라는에 바인딩합니다.  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornSingleElement](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornsingleelement)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornSingleElement](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornsingleelement)]  
  
> [!NOTE]
> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]를 사용하여 표시기를 다른 요소에 바인딩하는 것은 현재 지원되지 않습니다.  
  
<a name="adorn_children_panel"></a>   
## <a name="adorning-the-children-of-a-panel"></a>패널의 자식 표시  
 표시기를의 <xref:System.Windows.Controls.Panel>자식에 바인딩하려면 다음 단계를 수행 합니다.  
  
1. 자식을 표시할 `static` 요소의 <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> 표시기 계층을 찾으려면 메서드를 호출 합니다.  
  
2. 부모 요소의 자식을 열거 하 고 메서드를 <xref:System.Windows.Documents.AdornerLayer.Add%2A> 호출 하 여 각 자식 요소에 표시기를 바인딩합니다.  
  
 다음 예제에서는 SimpleCircleAdorner (위에 표시 됨)를 <xref:System.Windows.Controls.StackPanel> *mystackpanel*이라는의 자식에 바인딩합니다.  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornChildren](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornchildren)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornChildren](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornchildren)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.AdornerHitTestResult>
- [WPF에서 Shape 및 기본 그리기 개요](../graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)
- [이미지, 그림 및 시각적 표시로 그리기](../graphics-multimedia/painting-with-images-drawings-and-visuals.md)
- [Drawing 개체 개요](../graphics-multimedia/drawing-objects-overview.md)
- [방법 항목](adorners-how-to-topics.md)
