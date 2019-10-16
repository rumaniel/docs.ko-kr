---
title: 타이밍 동작 개요
ms.date: 03/30/2017
helpviewer_keywords:
- timing behaviors [WPF]
- behaviors [WPF], timing
ms.assetid: 5b714d46-bd46-48b8-b467-b4be89ba3091
ms.openlocfilehash: 1433583c4c8e20533e7e18f1722d5481ffed3bbc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625683"
---
# <a name="timing-behaviors-overview"></a>타이밍 동작 개요
이 항목에서는 애니메이션 및 기타의 타이밍 동작을 설명 <xref:System.Windows.Media.Animation.Timeline> 개체입니다.  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목을 이해하려면 기본 애니메이션 기능을 잘 알고 있어야 입니다. 자세한 내용은 참조는 [애니메이션 개요](animation-overview.md)합니다.  
  
<a name="timelinetypes"></a>   
## <a name="timeline-types"></a>타임라인 형식  
 <xref:System.Windows.Media.Animation.Timeline> 시간의 세그먼트를 나타냅니다. 해당 세그먼트의 길이, 시작 시기, 반복 횟수, 해당 세그먼트에서 진행되는 속도 등을 지정할 수 있는 속성이 제공됩니다.  
  
 타임라인 클래스에서 상속하는 클래스는 애니메이션 및 미디어 재생 등의 추가 기능을 제공합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 다음 기능을 제공 <xref:System.Windows.Media.Animation.Timeline> 형식입니다.  
  
|타임라인 형식|설명|  
|-------------------|-----------------|  
|<xref:System.Windows.Media.Animation.AnimationTimeline>|추상 기본 클래스에 대 한 <xref:System.Windows.Media.Animation.Timeline> 출력 값 속성에 애니메이션 효과 생성 하는 개체입니다.|  
|<xref:System.Windows.Media.MediaTimeline>|미디어 파일에서 출력을 생성합니다.|  
|<xref:System.Windows.Media.Animation.ParallelTimeline>|형식을 <xref:System.Windows.Media.Animation.TimelineGroup> 해당 그룹 및 컨트롤 자식 <xref:System.Windows.Media.Animation.Timeline> 개체입니다.|  
|<xref:System.Windows.Media.Animation.Storyboard>|형식의 <xref:System.Windows.Media.Animation.ParallelTimeline> 포함 하는 타임 라인 개체에 대 한 대상 정보를 제공 합니다.|  
|<xref:System.Windows.Media.Animation.Timeline>|타이밍 동작을 정의하는 추상 기본 클래스입니다.|  
|<xref:System.Windows.Media.Animation.TimelineGroup>|추상 클래스에 대 한 <xref:System.Windows.Media.Animation.Timeline> 기타를 포함할 수 있는 개체 <xref:System.Windows.Media.Animation.Timeline> 개체입니다.|  
  
<a name="propertiesthatcontroltimelinelength"></a>   
## <a name="properties-that-control-the-length-of-a-timeline"></a>타임라인의 길이를 제어하는 속성  
 <xref:System.Windows.Media.Animation.Timeline> 나타내는 시간의 세그먼트 및 타임 라인의 길이 다양 한 방식으로 설명할 수 있습니다. 다음 표에서는 타임라인의 길이를 설명하기 위한 몇 가지 용어를 정의합니다.  
  
|용어|설명|속성||||  
|----------|-----------------|----------------|-|-|-|  
|단순 지속 시간|타임라인이 단일 정방향 반복을 수행하는 데 걸리는 시간입니다.|<xref:System.Windows.Media.Animation.Timeline.Duration%2A>||||  
|1회 반복|재생 되 면 및 경우에 타임 라인에 걸리는 시간의 길이 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 속성이 true 이면 거꾸로 1 번만 재생 합니다.|<xref:System.Windows.Media.Animation.Timeline.Duration%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>||||  
|활성 기간|지정한 모든 반복을 완료 하려면 타임 라인에 걸리는 시간의 길이 <xref:System.Windows.Media.Animation.RepeatBehavior> 속성입니다.|<xref:System.Windows.Media.Animation.Timeline.Duration%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>, <xref:System.Windows.Media.Animation.RepeatBehavior>||||  
  
<a name="duration"></a>   
### <a name="the-duration-property"></a>Duration 속성  
 앞서 설명한 것처럼 타임라인은 시간 세그먼트를 나타냅니다. 해당 세그먼트의 길이 타임 라인의 의해 결정 됩니다 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>합니다. 타임라인이 기간 끝에 도달하면 재생을 중지합니다. 타임라인에 자식 타임라인이 있어도 재생을 중지합니다. 애니메이션의 경우는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 애니메이션 걸리는 전환에서 해당 시작 값 끝 값을 지정 합니다. 타임 라인의 기간 이라고 해당 *단순 지속 기간 동안*, 단일 반복의 기간과 반복을 포함 하 여 애니메이션을 재생 시간의 총 길이 구별할 수 있습니다. 제한 시간 값 또는 특수 값을 사용 하 여 기간을 지정할 수 있습니다 <xref:System.Windows.Duration.Automatic%2A> 또는 <xref:System.Windows.Duration.Forever%2A>합니다. 애니메이션의 지속 된 <xref:System.Windows.Duration.TimeSpan%2A> 값을 값 간을 전환할 수 있도록 합니다.  
  
 에서는 다음 예제는 <xref:System.Windows.Media.Animation.DoubleAnimation> 사용 하 여를 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 5 초입니다.  
  
 [!code-xaml[animation_ovws_snippet#AnimationWith5SecondDurationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#animationwith5seconddurationinline)]  
  
 컨테이너 타임 라인와 같은 <xref:System.Windows.Media.Animation.Storyboard> 하 고 <xref:System.Windows.Media.Animation.ParallelTimeline>, 기본 기간이 <xref:System.Windows.Duration.Automatic%2A>, 즉, 마지막 자식의 재생이 중지 되 면 자동으로 종료 합니다. 다음 예제와 <xref:System.Windows.Media.Animation.Storyboard> 해당 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 5 초를 모든 자식에 걸리는 시간의 길이를 확인 <xref:System.Windows.Media.Animation.DoubleAnimation> 완료 하는 개체입니다.  
  
 [!code-xaml[animation_ovws_snippet#ContainerTimelineExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#containertimelineexampleinline)]  
  
 설정 하 여는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 을 컨테이너 타임 라인의를 <xref:System.Windows.Duration.TimeSpan%2A> 값을 할 수 있습니다 자식 보다 길거나 짧은 재생 하는 데 <xref:System.Windows.Media.Animation.Timeline> 개체 재생 하는 것입니다. 설정 하는 경우는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 되는 컨테이너 타임 라인의 자식 항목의 길이 보다 작은 값으로 <xref:System.Windows.Media.Animation.Timeline> 개체, 자식 <xref:System.Windows.Media.Animation.Timeline> 개체 컨테이너 타임 라인에서 수행 하는 경우 재생을 중지 합니다. 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 의 <xref:System.Windows.Media.Animation.Storyboard> 3 초를 앞의 예제에서 합니다. 결과적으로, 첫 번째 <xref:System.Windows.Media.Animation.DoubleAnimation> 경우 애니메이션 효과가 적용 대상 사각형의 너비에 60 3 초 후에 진행 되 고 중지 합니다.  
  
 [!code-xaml[animation_ovws_snippet#ContainerTimelineWithShorterDurationExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#containertimelinewithshorterdurationexampleinline)]  
  
<a name="repeatinganimations"></a>   
### <a name="the-repeatbehavior-property"></a>RepeatBehavior 속성  
 합니다 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 의 속성을 <xref:System.Windows.Media.Animation.Timeline> 단순 지속 시간의 반복 횟수를 제어 합니다. 사용 하는 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 속성을 타임 라인 수행 하는 횟수를 지정할 수 있습니다 (반복 <xref:System.Windows.Media.Animation.RepeatBehavior.Count%2A>) 또는 총 재생 해야 하는 시간의 길이 (반복 <xref:System.Windows.Media.Animation.RepeatBehavior.Duration%2A>). 두 경우 모두 애니메이션은 요청된 횟수 또는 기간을 채우는 데 필요한만큼 시작-끝 실행을 반복합니다. 기본적으로 타임 라인의 반복 횟수를는 `1.0`, 즉, 한 번 재생 되 고 전혀 반복 되지 않습니다.  
  
 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 속성을는 <xref:System.Windows.Media.Animation.DoubleAnimation> 단순 지속 시간의 두 번 반복 횟수를 지정 하 여 재생 합니다.  
  
 [!code-xaml[animation_ovws_snippet#TBRepeatBehavior2xExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#tbrepeatbehavior2xexampleinline)]  
  
 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 속성을는 <xref:System.Windows.Media.Animation.DoubleAnimation> 절반 단순 지속 시간 동안 재생 합니다.  
  
 [!code-xaml[animation_ovws_snippet#TBRepeatBehavior05xExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#tbrepeatbehavior05xexampleinline)]  
  
 설정 하는 경우는 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 의 속성을 <xref:System.Windows.Media.Animation.Timeline> 에 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>, <xref:System.Windows.Media.Animation.Timeline> 대화형으로 또는 타이밍 시스템에 의해 중지 될 때까지 반복 합니다. 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 속성을는 <xref:System.Windows.Media.Animation.DoubleAnimation> 무한정 재생 하도록 합니다.  
  
 [!code-xaml[animation_ovws_snippet#TBRepeatBehaviorForeverExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#tbrepeatbehaviorforeverexampleinline)]  
  
 추가 예제를 보려면 [애니메이션 반복](how-to-repeat-an-animation.md)합니다.  
  
<a name="autoreverseproperty"></a>   
### <a name="the-autoreverse-property"></a>AutoReverse 속성  
 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 속성을 지정 여부는 <xref:System.Windows.Media.Animation.Timeline> 각 정방향 반복 끝에서 거꾸로 재생 됩니다. 설정 하는 다음 예제는 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 의 속성을 <xref:System.Windows.Media.Animation.DoubleAnimation> 에 `true`; 결과적으로, 100으로 0에서 그 다음 0 100에서 애니메이션 효과 주는 합니다. 총 10초 동안 재생됩니다.  
  
 [!code-xaml[animation_ovws_snippet#TBAutoReverseExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#tbautoreverseexampleinline)]  
  
 사용 하는 경우를 <xref:System.Windows.Media.Animation.RepeatBehavior.Count%2A> 값을 지정 합니다 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 의 <xref:System.Windows.Media.Animation.Timeline> 및 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 속성의 <xref:System.Windows.Media.Animation.Timeline> 는 `true`, 하나로 단일 반복을 구성 정방향 반복 하나가 오는 이전 버전과 반복.  다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 의 <xref:System.Windows.Media.Animation.DoubleAnimation> 하려면 앞의 예제에서를 <xref:System.Windows.Media.Animation.RepeatBehavior.Count%2A> 두. 결과적으로 <xref:System.Windows.Media.Animation.DoubleAnimation> 20 초 동안 재생: 5 초에 대 한 이전 버전과 5 초를 5 초 동안 다시 전달에 대 한 전달 및 5 초 동안 뒤로.  
  
 [!code-xaml[animation_ovws_snippet#TBAutoReverseRepeatExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#tbautoreverserepeatexampleinline)]  
  
 컨테이너 타임 라인에 자식 <xref:System.Windows.Media.Animation.Timeline> 는 컨테이너 타임 라인이 될 때 마찬가지로 거꾸로 개체입니다. 추가 예제를 보려면 [지정 여부는 타임 라인을 자동으로 뒤집을](how-to-specify-whether-a-timeline-automatically-reverses.md)합니다.  
  
<a name="timelinebegin"></a>   
## <a name="the-begintime-property"></a>BeginTime 속성  
 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 속성을 사용 하면 타임 라인 시작 될 때 지정할 수 있습니다.  타임라인의 시작 시간은 부모 타임라인에 상대적입니다. 타임라인 0초는 부모 타임라인이 시작되자마자 해당 타임라인이 시작됨을 의미합니다. 다른 값을 지정하면 부모 타임라인이 재생을 시작하는 시간과 자식 타임라인이 재생되는 시간 사이에 오프셋이 생성됩니다. 예를 들어 시작 시간이 2초면 부모 타임라인이 2초에 도달할 때 해당 타임라인이 재생을 시작함을 의미합니다. 기본적으로 모든 타임라인의 시작 시간은 0초입니다. 타임 라인의를 설정할 수도 있습니다 시작 시간에 `null`, 타임 라인이 시작 되지 않도록 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 사용 하 여 null을 지정 합니다 [X:null 태그 확장](../../xaml-services/x-null-markup-extension.md)합니다.  
  
 시작 시간 하지는 때문에 라인이 반복 될 때마다 적용 해당 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 설정 합니다. 사용 하 여 애니메이션을 만드는 경우는 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 10 시간 (초) 및 <xref:System.Windows.Media.Animation.RepeatBehavior> 의 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>, 각 연속 반복 아니라 처음으로 애니메이션 재생 하기 전에 10 초 지연 됩니다. 그러나 애니메이션의 부모 타임라인이 다시 시작되거나 반복되면 10초의 지연이 발생할 것입니다.  
  
 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 속성은 타임 라인에 유용 합니다. 다음 예제는 <xref:System.Windows.Media.Animation.Storyboard> 자식이 두 <xref:System.Windows.Media.Animation.DoubleAnimation> 개체입니다. 첫 번째 애니메이션에는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 5 초의 되 고 두 번째는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 3 초입니다. 예제에서는 합니다 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 초의 <xref:System.Windows.Media.Animation.DoubleAnimation> 5 초를 따라서 재생을 시작 후 첫 번째 <xref:System.Windows.Media.Animation.DoubleAnimation> 종료 합니다.  
  
 [!code-xaml[animation_ovws_snippet#TBBeginTimeExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#tbbegintimeexampleinline)]  
  
<a name="fillbehaviorproperty"></a>   
## <a name="the-fillbehavior-property"></a>FillBehavior 속성  
 경우는 <xref:System.Windows.Media.Animation.Timeline> 총 해당 활성 기간의 끝에 도달한는 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 중지는 마지막 값을 유지 여부를 지정 하는 속성입니다. 애니메이션을 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 의 <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd> 출력 값을 "유지": 애니메이션의 마지막 값이 유지 되는 속성입니다. 값 <xref:System.Windows.Media.Animation.FillBehavior.Stop> 끝낸 후 대상 속성에 영향을 주는 애니메이션 중지는 발생 합니다.  
  
 다음 예제는 <xref:System.Windows.Media.Animation.Storyboard> 자식이 두 <xref:System.Windows.Media.Animation.DoubleAnimation> 개체입니다. 둘 다 <xref:System.Windows.Media.Animation.DoubleAnimation> 개체에 애니메이션 효과 주기 합니다 <xref:System.Windows.FrameworkElement.Width%2A> 의 <xref:System.Windows.Shapes.Rectangle> 0 ~ 100입니다. 합니다 <xref:System.Windows.Shapes.Rectangle> 요소에 애니메이션이 적용 되지 않은 <xref:System.Windows.FrameworkElement.Width%2A> 값 500 [장치 독립적 픽셀]입니다.  
  
- 합니다 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 첫 번째 속성 <xref:System.Windows.Media.Animation.DoubleAnimation> 로 설정 되어 <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd>, 기본 값입니다. 결과적으로 사각형의 너비 후 100을 유지 합니다 <xref:System.Windows.Media.Animation.DoubleAnimation> 종료 합니다.  
  
- 합니다 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 속성의 두 번째 <xref:System.Windows.Media.Animation.DoubleAnimation> 로 설정 된 <xref:System.Windows.Media.Animation.FillBehavior.Stop>합니다. 결과적으로 <xref:System.Windows.FrameworkElement.Width%2A> 두 번째 <xref:System.Windows.Shapes.Rectangle> 후 500 되돌아갑니다는 <xref:System.Windows.Media.Animation.DoubleAnimation> 종료 합니다.  
  
 [!code-xaml[animation_ovws_snippet#TBFillBehaviorExample](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/TimingBehaviorsExample1.xaml#tbfillbehaviorexample)]  
  
<a name="speedproperties"></a>   
## <a name="properties-that-control-the-speed-of-a-timeline"></a>타임라인의 속도를 제어하는 속성  
 <xref:System.Windows.Media.Animation.Timeline> 클래스는 해당 속도 지정 하는 것에 대 한 세 가지 속성을 제공 합니다.  
  
- <xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A> – 시간이 진행 되는 부모 기준으로 하는 속도 지정 합니다.는 <xref:System.Windows.Media.Animation.Timeline>합니다. 1 보다 큰 값의 속도 높일 합니다 <xref:System.Windows.Media.Animation.Timeline> 및 해당 자식 <xref:System.Windows.Media.Animation.Timeline> 개체, 값 0과 1 사이의 속도가 저하 됩니다. 값이 1 이면 <xref:System.Windows.Media.Animation.Timeline> 부모와 같은 속도로 진행 합니다. 합니다 <xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A> 컨테이너 타임 라인의 설정은 모든 자식 <xref:System.Windows.Media.Animation.Timeline> 개체도 합니다.  
  
- <xref:System.Windows.Media.Animation.Timeline.AccelerationRatio%2A> – 비율을 지정 합니다.는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 타임 라인 소요 된 시간의 가속화 합니다. 예는 [방법: 가속 또는 감속 애니메이션](how-to-accelerate-or-decelerate-an-animation.md)합니다. 
  
- <xref:System.Windows.Media.Animation.Timeline.DecelerationRatio%2A> --비율을 지정 하는 중의 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 타임 라인의 감속 합니다. 예는 [방법: 가속 또는 감속 애니메이션](how-to-accelerate-or-decelerate-an-animation.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [애니메이션 개요](animation-overview.md)
- [애니메이션 및 타이밍 시스템 개요](animation-and-timing-system-overview.md)
- [타이밍 이벤트 개요](timing-events-overview.md)
- [방법 항목](animation-and-timing-how-to-topics.md)
- [애니메이션 타이밍 동작 샘플](https://go.microsoft.com/fwlink/?LinkID=159970)
