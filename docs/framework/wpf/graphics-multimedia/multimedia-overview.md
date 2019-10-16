---
title: 멀티미디어 개요
ms.date: 03/30/2017
helpviewer_keywords:
- multimedia [WPF]
- media [WPF]
ms.assetid: feb25b15-d741-4ac3-818f-1b19f63a3562
ms.openlocfilehash: 44059fe96a0deeda18f0abd9079100b55be98e77
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929616"
---
# <a name="multimedia-overview"></a>멀티미디어 개요
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]의 멀티미디어 기능을 통해 오디오 및 비디오를 응용 프로그램에 통합하여 사용자 환경을 개선할 수 있습니다. 이 항목에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 멀티미디어 기능을 소개합니다.  

<a name="mediaapi"></a>   
## <a name="media-api"></a>미디어 API  
 <xref:System.Windows.Controls.MediaElement> 및<xref:System.Windows.Media.MediaPlayer> 클래스는 오디오 또는 비디오 콘텐츠를 표시 하는 데 사용 됩니다. 이러한 클래스는 대화형으로 또는 클록을 통해 제어할 수 있습니다. 이러한 클래스는 미디어 재생을 위한 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 10 컨트롤에서 사용할 수 있습니다. 사용하는 클래스는 시나리오에 따라 달라집니다.  
  
 <xref:System.Windows.Controls.MediaElement>는 [레이아웃](../advanced/layout.md) 에서 지원 되며 많은 컨트롤의 콘텐츠로 사용 될 수 있는입니다.<xref:System.Windows.UIElement> 코드 뿐만 아니라 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]에서도 사용할 수 있습니다. <xref:System.Windows.Media.MediaPlayer>반면,는 개체를 위해 <xref:System.Windows.Media.Drawing> 디자인 되었으며 레이아웃은 지원 하지 않습니다. 을 사용 하 여 <xref:System.Windows.Media.MediaPlayer> 로드 된 미디어는와 직접 <xref:System.Windows.Media.VideoDrawing> 상호 작용 하는 <xref:System.Windows.Media.DrawingContext>방법 으로만 제공할 수 있습니다. <xref:System.Windows.Media.MediaPlayer>는 XAML에서 사용할 수 없습니다.  
  
 Drawing 개체 및 그리기 컨텍스트에 대한 자세한 내용은 [Drawing 개체 개요](drawing-objects-overview.md)를 참조하세요.  
  
> [!NOTE]
> 애플리케이션을 사용하여 미디어를 배포하는 경우 미디어 파일을 프로젝트 리소스로 사용할 수 없습니다. 대신 프로젝트 파일에서 미디어 형식을 `Content`로 설정하고 `CopyToOutputDirectory`를 `PreserveNewest` 또는 `Always`로 설정해야 합니다.  
  
<a name="mediaplaybackmodes"></a>   
## <a name="media-playback-modes"></a>미디어 재생 모드  
  
> [!NOTE]
> <xref:System.Windows.Controls.MediaElement> 와<xref:System.Windows.Media.MediaPlayer> 는 모두 유사한 멤버를 가집니다. 이 섹션의 링크는 <xref:System.Windows.Controls.MediaElement> 클래스 멤버를 참조 합니다. 구체적으로 언급 하지 않는 한 클래스의에 <xref:System.Windows.Controls.MediaElement> 연결 된 멤버는 <xref:System.Windows.Media.MediaPlayer> 클래스 에서도 찾을 수 있습니다.  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서 미디어 재생을 이해하려면 미디어를 재생할 수 있는 여러 다른 모드를 이해해야 합니다. <xref:System.Windows.Controls.MediaElement> 및<xref:System.Windows.Media.MediaPlayer> 둘 다 서로 다른 두 미디어 모드, 즉 독립 모드와 클록 모드로 사용할 수 있습니다. 미디어 모드는 속성에 <xref:System.Windows.Controls.MediaElement.Clock%2A> 의해 결정 됩니다. 가 이면 `null`미디어 개체는 독립 모드입니다. <xref:System.Windows.Controls.MediaElement.Clock%2A> <xref:System.Windows.Controls.MediaElement.Clock%2A> 가 null이 아닌 경우 미디어 개체는 클록 모드입니다. 기본적으로 미디어 개체는 독립 모드입니다.  
  
### <a name="independent-mode"></a>독립 모드  
 독립 모드에서 미디어 콘텐츠는 미디어 재생을 주도합니다. 독립 모드에서는 다음과 같은 옵션을 사용할 수 있습니다.  
  
- <xref:System.Uri> 미디어를 직접 지정할 수 있습니다.  
  
- 미디어 재생을 직접 제어할 수 있습니다.  
  
- 미디어의 <xref:System.Windows.Controls.MediaElement.Position%2A> 및 <xref:System.Windows.Controls.MediaElement.SpeedRatio%2A> 속성을 수정할 수 있습니다.  
  
 <xref:System.Windows.Controls.MediaElement> 개체의 <xref:System.Windows.Controls.MediaElement.Source%2A> 속성을 설정 하거나 개체의 <xref:System.Windows.Media.MediaPlayer.Open%2A> 메서드를 <xref:System.Windows.Media.MediaPlayer> 호출 하 여 미디어를 로드 합니다.  
  
 독립 모드에서 미디어 재생을 제어하려면 미디어 개체의 컨트롤 메서드를 사용할 수 있습니다. 사용할 수 있는 <xref:System.Windows.Controls.MediaElement.Play%2A>컨트롤 메서드는 <xref:System.Windows.Controls.MediaElement.Pause%2A> <xref:System.Windows.Controls.MediaElement.Close%2A>,, 및 <xref:System.Windows.Controls.MediaElement.Stop%2A>입니다. 의 <xref:System.Windows.Controls.MediaElement>경우 이러한 메서드를 사용 하는 대화형 제어는 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 가로 <xref:System.Windows.Controls.MediaState.Manual>설정 된 경우에만 사용할 수 있습니다. 이러한 메서드는 미디어 개체가 클록 모드에 있을 때는 사용할 수 없습니다.  
  
 독립 모드의 예제를 보려면 [MediaElement 제어(재생, 일시 중지, 정지, 볼륨 및 속도)](how-to-control-a-mediaelement-play-pause-stop-volume-and-speed.md)를 참조하세요.  
  
### <a name="clock-mode"></a>클록 모드  
 클록 모드 <xref:System.Windows.Media.MediaTimeline> 에서는 미디어 재생을 구동 합니다. 클록 모드에는 다음과 같은 특징이 있습니다.  
  
- 미디어의 <xref:System.Uri> 는를 <xref:System.Windows.Media.MediaTimeline>통해 간접적으로 설정 됩니다.  
  
- 미디어 재생을 클록으로 제어할 수 있습니다. 미디어 개체의 컨트롤 메서드를 사용할 수 없습니다.  
  
- 미디어는 개체의 <xref:System.Windows.Media.MediaTimeline> <xref:System.Windows.Media.MediaTimeline.Source%2A> 속성을 설정 하 고, 타임 라인에서 시계를 만들고, 미디어 개체에 시계를 할당 하 여 로드 됩니다. <xref:System.Windows.Media.MediaTimeline> 내에서<xref:System.Windows.Controls.MediaElement>가를 대상으로 하는 경우에도 미디어가 로드 됩니다. <xref:System.Windows.Media.Animation.Storyboard>  
  
 클록 모드에서 미디어 재생을 제어 하려면 컨트롤 <xref:System.Windows.Media.Animation.ClockController> 메서드를 사용 해야 합니다. 는의 <xref:System.Windows.Media.Animation.ClockController> 속성에서 가져옵니다. <xref:System.Windows.Media.MediaClock> <xref:System.Windows.Media.Animation.ClockController> 클록 모드 <xref:System.Windows.Controls.MediaElement> <xref:System.Windows.Media.MediaPlayer>에서또는 개체의 control 메서드를 사용 하려고 하면 이throw됩니다.<xref:System.InvalidOperationException>  
  
 클록 및 타임라인에 대한 자세한 내용은 [애니메이션 개요](animation-overview.md)를 참조하세요.  
  
 클록 모드 예제를 보려면 [Storyboard를 사용하여 MediaElement 제어](how-to-control-a-mediaelement-by-using-a-storyboard.md)를 참조하세요.  
  
<a name="mediaelement"></a>   
## <a name="mediaelement-class"></a>MediaElement 클래스  
 응용 프로그램에 미디어를 추가 하는 것은 응용 <xref:System.Windows.Controls.MediaElement> 프로그램의에 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 컨트롤을 추가 하 고 포함 <xref:System.Uri> 하려는 미디어에를 제공 하는 것 만큼 간단 합니다. [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 10에서 지원하는 모든 미디어 형식이 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서 지원됩니다. 다음 예에서는의를 간단 하 게 사용 <xref:System.Windows.Controls.MediaElement> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]하는 방법을 보여 줍니다.  
  
 [!code-xaml[MediaElement_snip#SimpleMediaElementUsageWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaElement_snip/CSharp/SimpleUsage.xaml#simplemediaelementusagewholepage)]  
  
 이 샘플에서는 미디어가 로드되는 즉시 자동으로 재생됩니다. 미디어 재생이 완료되면 미디어가 닫히고 모든 미디어 리소스(비디오 메모리 포함)는 해제됩니다. 이는 <xref:System.Windows.Controls.MediaElement> 개체의 기본 동작이 며 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 및 <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> 속성에 의해 제어 됩니다.  
  
### <a name="controlling-a-mediaelement"></a>MediaElement 제어  
 및 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> <xref:System.Windows.Controls.MediaElement> <xref:System.Windows.FrameworkElement.IsLoaded%2A> 속성은 가`true` 또는 일`false`때의 동작을 제어 합니다. <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> <xref:System.Windows.Controls.MediaState> 속성은 미디어 재생 동작에 영향을 주기 위해 설정 됩니다. 예 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 를 들어 기본값은이 <xref:System.Windows.Controls.MediaState.Play> 고 기본값 <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> <xref:System.Windows.Controls.MediaState.Close>은입니다. 즉, <xref:System.Windows.Controls.MediaElement> 가 로드 되 고 미리 받기가 완료 되 면 미디어 재생이 시작 됩니다. 재생이 완료되면 미디어가 닫히고 모든 미디어 리소스가 해제됩니다.  
  
 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 및<xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> 속성은 미디어 재생을 제어 하는 유일한 방법이 아닙니다. 클록 모드에서 clock은를 제어할 <xref:System.Windows.Controls.MediaElement> 수 있으며, 대화형 컨트롤 메서드는 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> 가 인 <xref:System.Windows.Controls.MediaState.Manual>경우 제어를 가집니다. <xref:System.Windows.Controls.MediaElement>는 다음과 같은 우선 순위를 평가 하 여 제어의 경쟁을 처리 합니다.  
  
1. <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>. 미디어가 언로드될 때 적용됩니다. 이렇게 하면 <xref:System.Windows.Media.MediaClock> 가 <xref:System.Windows.Controls.MediaElement>와 연결 된 경우에도 모든 미디어 리소스가 기본적으로 해제 됩니다.  
  
2. <xref:System.Windows.Media.MediaClock>. 미디어에가 <xref:System.Windows.Controls.MediaElement.Clock%2A>있는 경우 미디어가 언로드되 <xref:System.Windows.Media.MediaClock> 는 경우 <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> 이 인 경우가 <xref:System.Windows.Controls.MediaState.Manual>적용 됩니다. 클록 모드는 <xref:System.Windows.Controls.MediaElement>항상의 로드 된 동작을 재정의 합니다.  
  
3. <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>. 미디어가 로드될 때 적용됩니다.  
  
4. 대화형 컨트롤 메서드. 가 인 경우 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> <xref:System.Windows.Controls.MediaState.Manual> 사용할 수 있는 <xref:System.Windows.Controls.MediaElement.Play%2A>컨트롤 메서드는 <xref:System.Windows.Controls.MediaElement.Pause%2A> <xref:System.Windows.Controls.MediaElement.Close%2A>,, 및 <xref:System.Windows.Controls.MediaElement.Stop%2A>입니다.  
  
### <a name="displaying-a-mediaelement"></a>MediaElement 표시  
 을 <xref:System.Windows.Controls.MediaElement> 표시 하려면 렌더링할 콘텐츠가 있어야 하며 콘텐츠가 로드 될 때까지 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 및 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 속성이 0으로 설정 됩니다. 오디오 전용 콘텐츠의 경우 이러한 속성은 항상 0입니다. 비디오 콘텐츠의 <xref:System.Windows.Controls.MediaElement.MediaOpened> 경우 이벤트가 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 발생 하면이 고 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 로드 된 미디어의 크기를 보고 합니다. 즉, <xref:System.Windows.Controls.MediaElement> <xref:System.Windows.FrameworkElement.Width%2A> [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 또는<xref:System.Windows.FrameworkElement.Height%2A> 속성이 설정 되지 않은 경우는 미디어가 로드 될 때까지에서 실제 공간을 차지 하지 않습니다.  
  
 <xref:System.Windows.FrameworkElement.Width%2A> <xref:System.Windows.Controls.MediaElement>및 속성을모두설정하면미디어가늘어나에대해제공된영역을채웁니다.<xref:System.Windows.FrameworkElement.Height%2A> 미디어의 원래 가로 세로 비율을 유지 하기 위해 <xref:System.Windows.FrameworkElement.Width%2A> 또는 <xref:System.Windows.FrameworkElement.Height%2A> 속성 중 하나만 설정 해야 합니다. <xref:System.Windows.FrameworkElement.Width%2A> 및<xref:System.Windows.FrameworkElement.Height%2A> 속성을 모두 설정 하면 미디어가 고정 요소 크기에 표시 되므로 바람직하지 않을 수 있습니다.  
  
 고정 크기 요소를 유지하지 못하게 하기 위해 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서 미디어를 미리 받을 수 있습니다. 이 작업은을 <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> <xref:System.Windows.Controls.MediaState.Play> 또는 <xref:System.Windows.Controls.MediaState.Pause>로 설정 하 여 수행 합니다. <xref:System.Windows.Controls.MediaState.Pause> 상태에서 미디어는 미리 받고 첫 번째 프레임을 표시 합니다. <xref:System.Windows.Controls.MediaState.Play> 상태에서 미디어는 미리 받고 재생을 시작 합니다.  
  
<a name="mediaplayer"></a>   
## <a name="mediaplayer-class"></a>MediaPlayer 클래스  
 클래스가 프레임 워크 요소인 경우 클래스는 <xref:System.Windows.Media.MediaPlayer> 개체에서 <xref:System.Windows.Media.Drawing> 사용 하도록 디자인 되었습니다. <xref:System.Windows.Controls.MediaElement> 그리기 개체는 성능 이점을 얻기 위해 또는 기능이 필요할 <xref:System.Windows.Freezable> 때 프레임 워크 수준 기능을 저하 시킬 수 있는 경우에 사용 됩니다. <xref:System.Windows.Media.MediaPlayer>를 사용 하면 응용 프로그램에서 미디어 콘텐츠를 제공 하는 동시에 이러한 기능을 활용할 수 있습니다. 와 마찬가지로 <xref:System.Windows.Controls.MediaElement>는 독립적 또는 클록 모드에서 사용할 <xref:System.Windows.Controls.MediaElement> 수있지만개체의언로드및로드상태는포함되지않습니다.<xref:System.Windows.Media.MediaPlayer> 이렇게 하면 <xref:System.Windows.Media.MediaPlayer>의 재생 제어 복잡성이 줄어듭니다.  
  
### <a name="controlling-mediaplayer"></a>MediaPlayer 제어  
 는 <xref:System.Windows.Media.MediaPlayer> 상태 비저장 이므로 미디어 재생을 제어 하는 방법에는 두 가지가 있습니다.  
  
1. 대화형 컨트롤 메서드. 독립 모드 (`null` <xref:System.Windows.Media.MediaPlayer.Clock%2A> 속성)에 있을 때 적용 됩니다.  
  
2. <xref:System.Windows.Media.MediaClock>. 미디어에가 <xref:System.Windows.Media.MediaPlayer.Clock%2A>있는 경우  
  
### <a name="displaying-a-mediaplayer"></a>MediaPlayer 표시  
 기술적으로는 <xref:System.Windows.Media.MediaPlayer> 물리적 표현이 없기 때문에를 표시할 수 없습니다. 그러나 <xref:System.Windows.Media.Drawing> <xref:System.Windows.Media.VideoDrawing> 클래스를 사용 하 여에 미디어를 표시 하는 데 사용할 수 있습니다. 다음 예제에서는를 <xref:System.Windows.Media.VideoDrawing> 사용 하 여 미디어를 표시 하는 방법을 보여 줍니다.  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 개체에 대 한 <xref:System.Windows.Media.Drawing> 자세한 내용은 [Drawing 개체 개요](drawing-objects-overview.md) 를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.DrawingGroup>
- [레이아웃](../advanced/layout.md)
- [방법 항목](audio-and-video-how-to-topics.md)
