---
title: DrawingVisual 개체 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- visual layer [WPF], DrawingVisual objects
- DrawingVisual objects in visual layer [WPF]
ms.assetid: 0b4e711d-e640-40cb-81c3-8f5c59909b7d
ms.openlocfilehash: 4e6fc89b64f7b0acc1a0077708d567eb97e2868e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962838"
---
# <a name="using-drawingvisual-objects"></a>DrawingVisual 개체 사용
이 항목에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시각적 계층에서 개체를 사용 <xref:System.Windows.Media.DrawingVisual> 하는 방법에 대 한 개요를 제공 합니다.  
  
<a name="drawingvisual_object"></a>   
## <a name="drawingvisual-object"></a>DrawingVisual 개체  
 는 <xref:System.Windows.Media.DrawingVisual> 도형, 이미지 또는 텍스트를 렌더링 하는 데 사용 되는 간단한 그리기 클래스입니다. 이 클래스는 성능을 향상시키는 레이아웃이나 이벤트 처리를 제공하지 않으므로 간단한 클래스로 간주됩니다. 이러한 이유 때문에 그리기는 배경 및 클립 아트에 적합합니다.  
  
<a name="drawingvisual_host_container"></a>   
## <a name="drawingvisual-host-container"></a>DrawingVisual 호스트 컨테이너  
 사용 하기 위해 <xref:System.Windows.Media.DrawingVisual> 개체를 개체에 대 한 호스트 컨테이너를 만들어야 합니다. 호스트 컨테이너 개체는 클래스에서 <xref:System.Windows.FrameworkElement> 파생 되어야 합니다. 클래스는 클래스의 <xref:System.Windows.Media.DrawingVisual> 레이아웃 및 이벤트 처리 지원을 제공 합니다. 호스트 컨테이너 개체는 주 목적이 자식 개체를 포함하는 것이므로 표시 가능한 속성을 표시하지 않습니다. 그러나 호스트 컨테이너의 <xref:System.Windows.Visibility.Visible> 속성을로설정해야합니다.그렇지않으면자식요소가표시되지않습니다.<xref:System.Windows.UIElement.Visibility%2A>  
  
 시각적 개체에 대 한 호스트 컨테이너 개체를 만드는 경우 시각적 개체 참조 <xref:System.Windows.Media.VisualCollection>를에 저장 해야 합니다. <xref:System.Windows.Media.VisualCollection.Add%2A> 메서드를 사용 하 여 호스트 컨테이너에 시각적 개체를 추가 합니다. 다음 예제에서는 호스트 컨테이너 개체가 만들어지고 세 개의 시각적 개체가에 <xref:System.Windows.Media.VisualCollection>추가 됩니다.  
  
 [!code-csharp[DrawingVisualSample#100](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#100)]
 [!code-vb[DrawingVisualSample#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#100)]  
  
> [!NOTE]
> 위의 코드 예제가 발췌된 전체 코드 샘플을 보려면 [DrawingVisuals를 사용하여 적중 테스트 샘플](https://go.microsoft.com/fwlink/?LinkID=159994)을 참조하세요.  
  
<a name="creating_drawingvisual_objects"></a>   
## <a name="creating-drawingvisual-objects"></a>DrawingVisual 개체 만들기  
 만들 때를 <xref:System.Windows.Media.DrawingVisual> 개체를 그리기 내용이 없습니다. 개체의 <xref:System.Windows.Media.DrawingContext> 및 그리기를 검색 하 여 텍스트, 그래픽 또는 이미지 콘텐츠를 추가할 수 있습니다. 개체의<xref:System.Windows.Media.DrawingVisual> 메서드를 <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A> 호출 하 여 이반환됩니다.<xref:System.Windows.Media.DrawingContext>  
  
 에 사각형 <xref:System.Windows.Media.DrawingContext>을 그리려면 <xref:System.Windows.Media.DrawingContext> 개체의 <xref:System.Windows.Media.DrawingContext.DrawRectangle%2A> 메서드를 사용 합니다. 다른 형식의 콘텐츠를 그리기 위한 비슷한 메서드가 존재합니다. 에 콘텐츠 <xref:System.Windows.Media.DrawingContext>를 그리기를 마치면 <xref:System.Windows.Media.DrawingContext.Close%2A> 메서드를 호출 하 여를 <xref:System.Windows.Media.DrawingContext> 닫고 콘텐츠를 유지 합니다.  
  
 다음 예제 <xref:System.Windows.Media.DrawingVisual> 에서는 개체가 만들어지고 사각형은 <xref:System.Windows.Media.DrawingContext>로 그려집니다.  
  
 [!code-csharp[DrawingVisualSample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#101)]
 [!code-vb[DrawingVisualSample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#101)]  
  
<a name="creating_overrides"></a>   
## <a name="creating-overrides-for-frameworkelement-members"></a>FrameworkElement 멤버에 대한 재정의 만들기  
 호스트 컨테이너 개체는 시각적 개체의 컬렉션을 관리합니다. 이렇게 하려면 호스트 컨테이너가 파생 <xref:System.Windows.FrameworkElement> 된 클래스에 대 한 멤버 재정의를 구현 해야 합니다.  
  
 다음 목록에서는 재정의해야 하는 두 멤버에 대해 설명합니다.  
  
- <xref:System.Windows.FrameworkElement.GetVisualChild%2A>: 자식 요소의 컬렉션에서 지정 된 인덱스에 있는 자식을 반환 합니다.  
  
- <xref:System.Windows.FrameworkElement.VisualChildrenCount%2A>: 이 요소 내 시각적 자식 요소의 수를 가져옵니다.  
  
 다음 예제에서는 두 <xref:System.Windows.FrameworkElement> 멤버에 대 한 재정의가 구현 됩니다.  
  
 [!code-csharp[DrawingVisualSample#102](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#102)]
 [!code-vb[DrawingVisualSample#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#102)]  
  
<a name="providing_hit_testing_support"></a>   
## <a name="providing-hit-testing-support"></a>적중 테스트 지원 제공  
 호스트 컨테이너 개체는 표시 되는 속성을 표시 하지 않는 경우에도 이벤트 처리를 제공할 수 있습니다 <xref:System.Windows.UIElement.Visibility%2A> . 그러나 속성을로 <xref:System.Windows.Visibility.Visible>설정 해야 합니다. 이 경우 왼쪽 마우스 단추 놓기와 같은 마우스 이벤트를 트래핑할 수 있는 호스트 컨테이너에 대한 이벤트 처리 루틴을 만들 수 있습니다. 그런 다음 이벤트 처리 루틴은 메서드를 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 호출 하 여 적중 테스트를 구현할 수 있습니다. 메서드의 <xref:System.Windows.Media.HitTestResultCallback> 매개 변수는 적중 테스트의 결과 동작을 확인 하는 데 사용할 수 있는 사용자 정의 프로시저를 참조 합니다.  
  
 다음 예제에서는 호스트 컨테이너 개체 및 해당 자식에 대해 적중 테스트 지원이 구현됩니다.  
  
 [!code-csharp[DrawingVisualSample#103](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#103)]
 [!code-vb[DrawingVisualSample#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#103)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.DrawingVisual>
- <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A>
- [WPF 그래픽 렌더링 개요](wpf-graphics-rendering-overview.md)
- [시각적 계층에서 적중 테스트](hit-testing-in-the-visual-layer.md)
