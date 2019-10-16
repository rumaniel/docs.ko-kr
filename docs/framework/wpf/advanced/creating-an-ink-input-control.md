---
title: 잉크 입력 컨트롤 만들기
ms.date: 03/30/2017
helpviewer_keywords:
- ink strokes [WPF], managing
- managing ink strokes [WPF]
- ink input control [WPF]
- input from mouse [WPF], accepting
- mouse input [WPF], accepting
- ink [WPF], rendering
- ink strokes [WPF], collecting
- rendering ink [WPF]
- collecting ink strokes [WPF]
- DynamicRenderer objects [WPF]
- StylusPlugIn objects [WPF]
ms.assetid: c31f3a67-cb3f-4ded-af9e-ed21f6575b26
ms.openlocfilehash: bd9fef806434b4ae064161eba11ad113fab07784
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64627383"
---
# <a name="creating-an-ink-input-control"></a>잉크 입력 컨트롤 만들기
사용자 지정 컨트롤을 동적으로 만들 수 하 고이 정보를 정적으로 잉크를 렌더링 합니다. 즉, 사용자를 "flow"에서 태블릿 펜 후 잉크를 표시 하는 컨트롤에 추가 클립보드에서 붙여 넣거나 파일에서 로드 태블릿 펜을 통해 표시할 잉크가 스트로크를 그릴 때에 잉크를 렌더링 합니다. 동적으로 잉크를 렌더링 하려면 컨트롤을 사용 해야는 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>합니다. 잉크를 정적으로 렌더링 하려면 스타일러스 이벤트 메서드를 재정의 해야 합니다 (<xref:System.Windows.UIElement.OnStylusDown%2A>, <xref:System.Windows.UIElement.OnStylusMove%2A>, 및 <xref:System.Windows.UIElement.OnStylusUp%2A>)를 수집 하 <xref:System.Windows.Input.StylusPoint> 데이터를 만들고 추가할는 <xref:System.Windows.Controls.InkPresenter> (컨트롤에서 잉크를 렌더링).  
  
 이 항목에는 다음과 같은 하위 단원이 포함되어 있습니다.  
  
- [방법: 잉크 스트로크를 만들어 스타일러스 지점 데이터를 수집 합니다.](#CollectingStylusPointDataAndCreatingInkStrokes)  
  
- [방법: 마우스 입력을 허용 하도록 컨트롤을 사용 하도록 설정](#EnablingYourControlToAcceptInputTromTheMouse)  
  
- [과정](#PuttingItTogether)  
  
- [추가 플러그 인 및 DynamicRenderers를 사용 하 여](#UsingAdditionalPluginsAndDynamicRenderers)  
  
- [결론](#AdvancedInkHandling_Conclusion)  
  
<a name="CollectingStylusPointDataAndCreatingInkStrokes"></a>   
## <a name="how-to-collect-stylus-point-data-and-create-ink-strokes"></a>방법: 잉크 스트로크를 만들어 스타일러스 지점 데이터를 수집 합니다.  
 스트로크 수집 하 고 잉크를 관리 하는 컨트롤을 만들려면 다음을 수행 합니다.  
  
1. 클래스를 파생 <xref:System.Windows.Controls.Control> 에서 파생 된 클래스 중 하나 또는 <xref:System.Windows.Controls.Control>와 같은 <xref:System.Windows.Controls.Label>합니다.  
  
     [!code-csharp[AdvancedInkTopicsSamples#20](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
    [!code-csharp[AdvancedInkTopicsSamples#14](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#14)]  
    [!code-csharp[AdvancedInkTopicsSamples#15](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#15)]  
  
2. 추가 <xref:System.Windows.Controls.InkPresenter> 클래스를 설정 합니다 <xref:System.Windows.Controls.ContentControl.Content%2A> 속성을 새 <xref:System.Windows.Controls.InkPresenter>.  
  
     [!code-csharp[AdvancedInkTopicsSamples#16](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#16)]  
  
3. 연결를 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> 의 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 에 <xref:System.Windows.Controls.InkPresenter> 호출 하 여를 <xref:System.Windows.Controls.InkPresenter.AttachVisuals%2A> 메서드를 추가 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 에 <xref:System.Windows.UIElement.StylusPlugIns%2A> 컬렉션. 따라서는 <xref:System.Windows.Controls.InkPresenter> 컨트롤에서 스타일러스 지점 데이터를 수집 하는 대로 잉크를 표시 합니다.  
  
     [!code-csharp[AdvancedInkTopicsSamples#17](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#17)]  
    [!code-csharp[AdvancedInkTopicsSamples#18](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#18)]  
  
4. <xref:System.Windows.UIElement.OnStylusDown%2A> 메서드를 재정의합니다.  이 메서드를 호출 하 여 스타일러스 캡처 <xref:System.Windows.Input.Stylus.Capture%2A>합니다. 계속 수신 하는 컨트롤에서 스타일러스를 캡처한 <xref:System.Windows.UIElement.StylusMove> 고 <xref:System.Windows.UIElement.StylusUp> 스타일러스가 컨트롤의 경계를 벗어날 경우에 이벤트입니다. 엄격 하 게 필수 하지만 좋은 사용자 환경을 위해 거의 항상 원하는 아닙니다. 새 <xref:System.Windows.Input.StylusPointCollection> 수집 <xref:System.Windows.Input.StylusPoint> 데이터입니다. 마지막으로 초기 집합을 추가 <xref:System.Windows.Input.StylusPoint> 데이터는 <xref:System.Windows.Input.StylusPointCollection>합니다.  
  
     [!code-csharp[AdvancedInkTopicsSamples#7](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#7)]  
  
5. 재정의 <xref:System.Windows.UIElement.OnStylusMove%2A> 메서드 추가 합니다 <xref:System.Windows.Input.StylusPoint> 데이터를를 <xref:System.Windows.Input.StylusPointCollection> 앞에서 만든 개체입니다.  
  
     [!code-csharp[AdvancedInkTopicsSamples#8](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#8)]  
  
6. 재정의 <xref:System.Windows.UIElement.OnStylusUp%2A> 메서드는 새 <xref:System.Windows.Ink.Stroke> 사용 하 여를 <xref:System.Windows.Input.StylusPointCollection> 데이터. 새 추가 <xref:System.Windows.Ink.Stroke> 하기 위해 생성 했던 합니다 <xref:System.Windows.Controls.InkPresenter.Strokes%2A> 의 컬렉션을 <xref:System.Windows.Controls.InkPresenter> 스타일러스 캡처를 해제 하 고.  
  
     [!code-csharp[AdvancedInkTopicsSamples#10](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#10)]  
  
<a name="EnablingYourControlToAcceptInputTromTheMouse"></a>   
## <a name="how-to-enable-your-control-to-accept-input-from-the-mouse"></a>방법: 마우스 입력을 허용 하도록 컨트롤을 사용 하도록 설정  
 응용 프로그램에 위의 컨트롤을 추가 하 고 실행 한 마우스를 사용 하 여 입력 장치로 스트로크 유지 되지 않습니다을 알 수 있습니다. 스트로크 입력 장치로 마우스를 사용 하는 경우 유지 하려면 다음을 수행 합니다.  
  
1. 재정의 <xref:System.Windows.UIElement.OnMouseLeftButtonDown%2A> 을 새로 만듭니다 <xref:System.Windows.Input.StylusPointCollection> 만들고 이벤트가 발생할 때 마우스 위치를 가져옵니다을 <xref:System.Windows.Input.StylusPoint> 지점 데이터를 사용 하 고 추가 <xref:System.Windows.Input.StylusPoint> 에 <xref:System.Windows.Input.StylusPointCollection>합니다.  
  
     [!code-csharp[AdvancedInkTopicsSamples#11](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#11)]  
  
2. <xref:System.Windows.UIElement.OnMouseMove%2A> 메서드를 재정의합니다. 이벤트가 발생할 때 마우스의 위치를 가져오기 및 만들기를 <xref:System.Windows.Input.StylusPoint> 지점 데이터를 사용 하 여 합니다.  추가 합니다 <xref:System.Windows.Input.StylusPoint> 에 <xref:System.Windows.Input.StylusPointCollection> 앞에서 만든 개체입니다.  
  
     [!code-csharp[AdvancedInkTopicsSamples#12](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#12)]  
  
3. <xref:System.Windows.UIElement.OnMouseLeftButtonUp%2A> 메서드를 재정의합니다.  새 <xref:System.Windows.Ink.Stroke> 사용 하 여는 <xref:System.Windows.Input.StylusPointCollection> 데이터를 새 추가 <xref:System.Windows.Ink.Stroke> 하기 위해 생성 했던를 <xref:System.Windows.Controls.InkPresenter.Strokes%2A> 의 컬렉션을 <xref:System.Windows.Controls.InkPresenter>.  
  
     [!code-csharp[AdvancedInkTopicsSamples#13](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#13)]  
  
<a name="PuttingItTogether"></a>   
## <a name="putting-it-together"></a>과정  
 다음 예제는 사용자가 마우스 또는 펜을 사용할 때 잉크를 수집 하는 사용자 지정 컨트롤입니다.  
  
 [!code-csharp[AdvancedInkTopicsSamples#20](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
[!code-csharp[AdvancedInkTopicsSamples#6](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#6)]  
  
<a name="UsingAdditionalPluginsAndDynamicRenderers"></a>   
## <a name="using-additional-plug-ins-and-dynamicrenderers"></a>추가 플러그 인 및 DynamicRenderers를 사용 하 여  
 사용자 지정 컨트롤에는 InkCanvas 같이 사용자 지정을 가질 수 있습니다 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 및 추가 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 개체입니다. 이러한 클래스를 추가 합니다 <xref:System.Windows.UIElement.StylusPlugIns%2A> 컬렉션입니다. 순서는 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 개체의 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> 렌더링 될 때 적용 될 잉크의 모양을. 가정은 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 라는 `dynamicRenderer` 및 사용자 지정 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 라는 `translatePlugin` 태블릿 펜에서 잉크를 오프셋 하는. 경우 `translatePlugin` 첫 번째 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 에 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>, 및 `dynamicRenderer` , 두 번째는 사용자가 펜을 움직이면 "흐르는" 잉크가 오프셋 됩니다. 하는 경우 `dynamicRenderer` 처음에 및 `translatePlugin` 는 두 번째 사용자가 펜을 뗄 때까지 잉크 오프셋 되지 것입니다.  
  
<a name="AdvancedInkHandling_Conclusion"></a>   
## <a name="conclusion"></a>결론  
 수집 하 여 스타일러스 이벤트 메서드를 재정의 하 여 잉크를 렌더링 하는 컨트롤을 만들 수 있습니다. 사용자 고유의 컨트롤을 만들면 파생 고유한 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 클래스를 삽입 하는에 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>, 디지털 잉크를 사용 하 여 상상할 수 있는 거의 모든 동작을 구현할 수 있습니다. 에 액세스할 수 합니다 <xref:System.Windows.Input.StylusPoint> 데이터를 사용자 지정할 수 있으므로 생성 됩니다 <xref:System.Windows.Input.Stylus> 입력 하 고 응용 프로그램에 대해 적절 하 게 화면에 렌더링 합니다. 이러한 하위 수준 액세스를 갖고 있으므로 <xref:System.Windows.Input.StylusPoint> 데이터 잉크 컬렉션을 구현 하 고 응용 프로그램에 대 한 최적의 성능으로 렌더링할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [고급 잉크 처리](advanced-ink-handling.md)
- [액세스 및 조작을 펜 입력](https://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409)
