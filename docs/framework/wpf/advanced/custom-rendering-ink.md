---
title: 잉크 렌더링 사용자 지정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom-rendering ink
- ink [WPF], custom-rendering
- classes [WPF], InkCanvas
ms.assetid: 65c978a7-0ee0-454f-ac7f-b1bd2efecac5
ms.openlocfilehash: 9a62a16f4fa16cfe40bbf830de2255bea25f8d3f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64611981"
---
# <a name="custom-rendering-ink"></a>잉크 렌더링 사용자 지정
합니다 <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> 스트로크의 속성을 사용 하면 해당 크기, 색 및 셰이프 등 스트로크의 모양을 지정할 수 있습니다 하지만 어떤 모양을 사용자 지정 하려는 경우가 있을 수 있습니다 <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> 허용 합니다. 에어브러시, 오일 페인트 및 다른 많은 효과가 있는 모양을 렌더링하여 잉크 모양을 사용자 지정하려는 경우도 있을 수 있습니다. 사용자 지정을 구현 하 여 잉크 렌더링 사용자 지정 하는 Windows Presentation Foundation (WPF) 허용 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 고 <xref:System.Windows.Ink.Stroke> 개체입니다.  
  
 이 항목에는 다음과 같은 하위 단원이 포함되어 있습니다.  
  
- [아키텍처](#Architecture)  
  
- [동적 렌더러 구현](#ImplementingADynamicRenderer)  
  
- [사용자 지정 스트로크 구현](#ImplementingCustomStrokes)  
  
- [사용자 지정 InkCanvas 구현](#ImplementingACustomInkCanvas)  
  
- [결론](#Conclusion)  
  
<a name="Architecture"></a>   
## <a name="architecture"></a>아키텍처  
 잉크 렌더링은 두 번 발생합니다. 사용자가 잉크 입력 표면에 잉크를 쓸 때 한 번 발생하고 잉크 지원 표면에 스트로크가 추가된 후에 다시 한 번 발생합니다. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 디지타이저에서 태블릿 펜을 이동할 때 잉크를 렌더링 하며 <xref:System.Windows.Ink.Stroke> 요소에 추가 되 면 자체를 렌더링 합니다.  
  
 동적으로 잉크를 렌더링하는 경우 세 가지 클래스를 구현해야 합니다.  
  
1. **DynamicRenderer**: <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>에서 파생되는 클래스를 구현합니다. 이 클래스는 특수화 된 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 렌더링 하는 스트로크를 그릴 때. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 잉크 화면 처럼 응용 프로그램 사용자 인터페이스 (UI) 스레드가 차단 되는 경우에 잉크를 수집 하는 별도 스레드에서 렌더링을 수행 합니다. 스레딩 모델에 대한 자세한 내용은 [잉크 스레딩 모델](the-ink-threading-model.md)을 참조하세요. 스트로크 렌더링을 동적으로 사용자 지정 하려면 재정의 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.OnDraw%2A> 메서드.  
  
2. **스트로크**: <xref:System.Windows.Ink.Stroke>에서 파생되는 클래스를 구현합니다. 이 클래스는 정적으로 렌더링 합니다 <xref:System.Windows.Input.StylusPoint> 으로 변환한 후 데이터는 <xref:System.Windows.Ink.Stroke> 개체입니다. 재정의 <xref:System.Windows.Ink.Stroke.DrawCore%2A> 스트로크의 정적 렌더링과 해당 메서드는 동적 렌더링와 일치 합니다.  
  
3. **InkCanvas:** <xref:System.Windows.Controls.InkCanvas>에서 파생되는 클래스를 구현합니다. 사용자 지정 할당 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 에 <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> 속성입니다. 재정의 <xref:System.Windows.Controls.InkCanvas.OnStrokeCollected%2A> 메서드를 사용자 지정 스트로크를 추가 하 고는 <xref:System.Windows.Controls.InkCanvas.Strokes%2A> 속성입니다. 이를 통해 잉크 모양이 일관되게 유지됩니다.  
  
<a name="ImplementingADynamicRenderer"></a>   
## <a name="implementing-a-dynamic-renderer"></a>동적 렌더러 구현  
 하지만 합니다 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 클래스는 표준의 일부인 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]전문적인 렌더링을 수행 하려면,에서 파생 되는 사용자 지정된 동적 렌더러를 만들어야 합니다를 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 재정의 및는 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.OnDraw%2A> 메서드.  
  
 다음 예제에서는 사용자 지정 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 는 선형 그라데이션 브러시 효과 사용 하 여 잉크를 그립니다.  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#1](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#1)]
[!code-vb[AdvancedInkTopicsSamples#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#1)]  
  
<a name="ImplementingCustomStrokes"></a>   
## <a name="implementing-custom-strokes"></a>사용자 지정 스트로크 구현  
 <xref:System.Windows.Ink.Stroke>에서 파생되는 클래스를 구현합니다. 이 클래스는 렌더링 <xref:System.Windows.Input.StylusPoint> 으로 변환한 후 데이터는 <xref:System.Windows.Ink.Stroke> 개체입니다. 재정의 <xref:System.Windows.Ink.Stroke.DrawCore%2A> 실제 그리기를 수행 하는 클래스입니다.  
  
 Stroke 클래스를 사용 하 여 사용자 지정 데이터를 저장할 수도 있습니다는 <xref:System.Windows.Ink.Stroke.AddPropertyData%2A> 메서드. 이 데이터는 스트로크 데이터와 함께 저장되어 유지됩니다.  
  
 <xref:System.Windows.Ink.Stroke> 클래스는 적중 횟수 테스트를 수행할 수도 있습니다. 고유의 적중 횟수 테스트 알고리즘을 재정의 하 여 구현할 수도 있습니다는 <xref:System.Windows.Ink.Stroke.HitTest%2A> 현재 클래스의 메서드.  
  
 다음 C# 코드에 사용자 지정 방법을 보여 줍니다 <xref:System.Windows.Ink.Stroke> 렌더링 하는 클래스 <xref:System.Windows.Input.StylusPoint> 데이터를 3 차원 스트로크로 합니다.  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#2](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#2)]
[!code-vb[AdvancedInkTopicsSamples#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#2)]  
  
<a name="ImplementingACustomInkCanvas"></a>   
## <a name="implementing-a-custom-inkcanvas"></a>사용자 지정 InkCanvas 구현  
 사용자 지정을 사용 하는 가장 쉬운 방법은 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 스트로크에서 파생 되는 클래스를 구현 하 고 <xref:System.Windows.Controls.InkCanvas> 이러한 클래스를 사용 합니다. 합니다 <xref:System.Windows.Controls.InkCanvas> 에 <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> 사용자 그릴 때 스트로크가 렌더링 되는 방식을 지정 하는 속성입니다.  
  
 사용자 지정 스트로크에서 렌더링을 <xref:System.Windows.Controls.InkCanvas> 다음을 수행 합니다.  
  
- 파생 된 클래스를 만들기는 <xref:System.Windows.Controls.InkCanvas>합니다.  
  
- 사용자 지정 할당 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 에 <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A?displayProperty=nameWithType> 속성입니다.  
  
- <xref:System.Windows.Controls.InkCanvas.OnStrokeCollected%2A> 메서드를 재정의합니다. 이 메서드에서 InkCanvas에 추가된 원래 스트로크를 제거합니다. 만든 다음 사용자 지정 스트로크를 추가 합니다 <xref:System.Windows.Controls.InkCanvas.Strokes%2A> 속성 및 기본 클래스를 새 호출 <xref:System.Windows.Controls.InkCanvasStrokeCollectedEventArgs> 사용자 지정 스트로크를 포함 하는 합니다.  
  
 다음 C# 코드에 사용자 지정 방법을 보여 줍니다 <xref:System.Windows.Controls.InkCanvas> 사용자 지정을 사용 하는 클래스 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 하 고 사용자 지정 스트로크를 수집 합니다.  
  
 [!code-csharp[AdvancedInkTopicsSamples#9](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#9)]  
  
 <xref:System.Windows.Controls.InkCanvas> 둘 이상의 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>합니다. 여러 개 추가할 수 있습니다 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 개체를 <xref:System.Windows.Controls.InkCanvas> 추가 하 여는 <xref:System.Windows.UIElement.StylusPlugIns%2A> 속성입니다.  
  
<a name="Conclusion"></a>   
## <a name="conclusion"></a>결론  
 직접 파생 시켜 잉크 모양을 사용자 지정할 수 있습니다 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>하십시오 <xref:System.Windows.Ink.Stroke>, 및 <xref:System.Windows.Controls.InkCanvas> 클래스입니다. 이와 함께 이러한 클래스는 사용자가 스트로크를 그릴 때와 스트로크가 수집된 후의 모양이 일관되도록 합니다.  
  
## <a name="see-also"></a>참고자료

- [고급 잉크 처리](advanced-ink-handling.md)
