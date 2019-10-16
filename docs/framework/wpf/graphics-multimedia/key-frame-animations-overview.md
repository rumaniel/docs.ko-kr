---
title: 키 프레임 애니메이션 개요
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], key-frame
- key frames [WPF], about key-frame animations
- multiple animation target values [WPF]
ms.assetid: 10028f97-bb63-41fc-b8ad-663dac7ea203
ms.openlocfilehash: 5c0e574ea494bedc1c359d38cda0d17bbb03fcdf
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645336"
---
# <a name="key-frame-animations-overview"></a>키 프레임 애니메이션 개요
이 항목에서는 키 프레임 애니메이션을 소개합니다. 키 프레임 애니메이션을 사용하면 두 개 이상의 대상 값을 사용하여 애니메이션 효과를 주고 애니메이션의 보간 방법을 제어할 수 있습니다.  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 개요를 이해하려면 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 애니메이션 및 타임라인을 잘 알고 있어야 입니다. 애니메이션 소개를 보려면 [애니메이션 개요](animation-overview.md)를 참조하세요. From/To/By 애니메이션을 잘 알고 있어도 도움이 됩니다. 자세한 내용은 From/To/By 애니메이션 개요를 참조하세요.  
  
<a name="whatisakeyframeanimation"></a>   
## <a name="what-is-a-key-frame-animation"></a>키 프레임 애니메이션이란?  
 From/To/By 애니메이션처럼 키 프레임 애니메이션도 대상 속성의 값에 애니메이션 효과를 줍니다. 통해 대상 값 간에 전환을 만듭니다. 해당 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>합니다. 그러나 From/To/By 애니메이션은 두 값 사이에 전환을 만들지만 단일 키 프레임 애니메이션은 원하는 수의 대상 값 사이에 전환을 만들 수 있습니다. From/To/By 애니메이션과 달리, 키 프레임 애니메이션에는 해당 대상 값을 설정하는 데 사용할 From, To 또는 By 속성이 없습니다. 키 프레임 애니메이션의 대상 값은 키 프레임 개체를 사용하여 설명합니다(그래서 "키 프레임 애니메이션"이라고 지칭함). 애니메이션의 대상 값을 지정 하려면 키 프레임 개체를 만들고 애니메이션의 추가할 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.KeyFrames%2A> 컬렉션입니다. 이 애니메이션은 실행될 때 지정된 프레임 간에 전환됩니다.  
  
 일부 키 프레임 메서드는 여러 대상 값을 지원할 뿐만 아니라 여러 보간 방법도 지원합니다. 애니메이션의 보간 방법은 한 값에서 다음 값으로 전환되는 방식을 정의합니다. 보간에는 불연속, 선형 및 스플라인의 세 가지 유형이 있습니다.  
  
 키 프레임 애니메이션으로 애니메이션 효과를 주려면 다음 단계를 완료합니다.  
  
- 애니메이션을 선언 하 고 지정 해당 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>를 from/to/by 애니메이션의 경우와 같이 합니다.  
  
- 각 대상 값에 대해 적절 한 형식의 키 프레임을 만들고, 해당 값을 설정 하 고 <xref:System.Windows.Media.Animation.KeyTime>, 애니메이션의 추가할 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.KeyFrames%2A> 컬렉션입니다.  
  
- From/To/By 애니메이션의 경우처럼 애니메이션을 속성에 연결합니다. storyboard를 사용하여 속성에 애니메이션을 적용하는 방법에 대한 자세한 내용은 [Storyboard 개요](storyboards-overview.md)를 참조하세요.  
  
 다음 예제에서는 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 애니메이션 효과를 주는 <xref:System.Windows.Shapes.Rectangle> 네 개의 서로 다른 위치에 요소입니다.  
  
 [!code-xaml[keyframes_ovw_snippet#BasicKeyFrameExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyFramesIntroduction.xaml#basickeyframeexamplewholepage)]  
  
 From/To/By와 같은 애니메이션 키 프레임 애니메이션을 적용할 수 속성을 사용 하 여는 <xref:System.Windows.Media.Animation.Storyboard> 태그와 코드 또는 사용 하 여는 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 코드에서 메서드. 만들려는 키 프레임 애니메이션을 사용할 수도 있습니다는 <xref:System.Windows.Media.Animation.AnimationClock> 하나 이상의 속성에 적용 합니다. 애니메이션 효과를 주기 위한 여러 다양한 방법에 대한 자세한 내용은 [속성 애니메이션 기술 개요](property-animation-techniques-overview.md)를 참조하세요.  
  
<a name="animation_types"></a>   
## <a name="key-frame-animation-types"></a>키 프레임 애니메이션 형식  
 애니메이션은 속성 값을 생성하므로 속성 형식이 다르면 애니메이션 형식도 다릅니다. 사용 하는 속성에 애니메이션 효과 <xref:System.Double> (요소와 같은 <xref:System.Windows.FrameworkElement.Width%2A> 속성)를 생성 하는 애니메이션을 사용 하 여 <xref:System.Double> 값. 사용 하는 속성에 애니메이션 효과를 <xref:System.Windows.Point>를 생성 하는 애니메이션을 사용 하 여 <xref:System.Windows.Point> 값 및 등입니다.  
  
 키 프레임 애니메이션 클래스에 속하는 <xref:System.Windows.Media.Animation> 네임 스페이스 다음 명명 규칙을 준수 합니다.  
  
 *\<Type>* `AnimationUsingKeyFrames`  
  
 여기서 *\<Type>* 은 클래스가 애니메이션을 적용하는 값의 형식입니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 다음 키 프레임 애니메이션 클래스를 제공합니다.  
  
|속성 형식|해당 From/To/By 애니메이션 클래스|지원되는 보간 방법|  
|-------------------|------------------------------------------------|-------------------------------------|  
|<xref:System.Boolean>|<xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames>|불연속|  
|<xref:System.Byte>|<xref:System.Windows.Media.Animation.ByteAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Decimal>|<xref:System.Windows.Media.Animation.DecimalAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Int16>|<xref:System.Windows.Media.Animation.Int16AnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Int32>|<xref:System.Windows.Media.Animation.Int32AnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Int64>|<xref:System.Windows.Media.Animation.Int64AnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Windows.Media.Matrix>|<xref:System.Windows.Media.Animation.MatrixAnimationUsingKeyFrames>|불연속|  
|<xref:System.Object>|<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>|불연속|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Windows.Media.Media3D.Quaternion>|<xref:System.Windows.Media.Animation.QuaternionAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Windows.Rect>|<xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Windows.Media.Media3D.Rotation3D>|<xref:System.Windows.Media.Animation.Rotation3DAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Single>|<xref:System.Windows.Media.Animation.SingleAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.String>|<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>|불연속|  
|<xref:System.Windows.Size>|<xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Windows.Thickness>|<xref:System.Windows.Media.Animation.ThicknessAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Windows.Media.Media3D.Vector3D>|<xref:System.Windows.Media.Animation.Vector3DAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
|<xref:System.Windows.Vector>|<xref:System.Windows.Media.Animation.VectorAnimationUsingKeyFrames>|불연속, 선형, 스플라인|  
  
<a name="animation_target_values"></a>   
## <a name="target-values-key-frames-and-key-times"></a>대상 값(키 프레임) 및 키 시간  
 다양한 속성 형식에 애니메이션 효과를 주기 위한 다양한 형식의 키 프레임 애니메이션이 있는 것처럼, 애니메이션 효과가 적용되는 각 형식의 값 및 지원되는 보간 방법에 따라 다양한 형식의 키 프레임 개체가 사용됩니다. 키 프레임 형식은 다음과 같은 명명 규칙을 따릅니다.  
  
 *\<InterpolationMethod>\<Type>* `KeyFrame`  
  
 여기서 *\<InterpolationMethod>* 는 키 프레임이 사용하는 보간 방법이고 *\<Type>* 은 클래스가 애니메이션 효과를 주는 값의 형식입니다. 세 가지 보간 방법을 모두 지원하는 키 프레임 애니메이션에는 사용할 수 있는 세 가지 키 프레임 형식이 있습니다. 예를 들어 세 개의 키 프레임 형식을 사용할 수 있습니다는 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>: <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame>를 <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame>, 및 <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame>합니다. (보간 방법은 뒤에 나오는 섹션에 자세히 설명되어 있습니다.)  
  
 키 프레임의 주요 목적은 지정 하는 것을 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 및 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>합니다. 모든 키 프레임 형식은 이러한 두 가지 속성을 제공합니다.  
  
- <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 속성에 해당 키 프레임에 대 한 대상 값을 지정 합니다.  
  
- 합니다 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 속성을 지정 하는 경우 (애니메이션의 내 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>) 키 프레임의 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 에 도달 합니다.  
  
 에 정의 된 순서 대로 키 프레임을 반복 하는 키 프레임 애니메이션이 시작 되 면 해당 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 속성입니다.  
  
- 애니메이션 대상 속성의 현재 값 간에 전환을 만듭니다 시간 0에 키 프레임이 없으면 있으면 및 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 첫 번째 키 프레임;이 고, 그렇지 애니메이션의 출력 값은 첫 번째 키 프레임의 값입니다.  
  
- 애니메이션 간에 전환을 만듭니다는 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 에서 두 번째 키 프레임으로 지정한 보간 방법을 사용 하 여 첫 번째 및 두 번째 키 프레임입니다. 첫 번째 키 프레임의 전환을 시작 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 될 때 종료 하 고 두 번째 키 프레임의 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 에 도달 합니다.  
  
- 애니메이션이 지속되면서 각 후속 키 프레임 및 해당 이전 키 프레임 간에 전환이 생성됩니다.  
  
- 마지막으로 가장 큰 키 시간을 사용 하 여 키 프레임의 값은 애니메이션 전환 하는 애니메이션의 보다 작거나 같은 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>합니다.  
  
 경우 애니메이션의 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 은 <xref:System.Windows.Duration.Automatic%2A> 또는 해당 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 마지막 키 프레임 애니메이션이 종료 시간과 같습니다. 그렇지 않고 애니메이션의 <xref:System.Windows.Duration> 될 때까지 키 프레임 값의 끝에 도달 하면 애니메이션 포함 마지막 키 프레임의 키 시간 보다 크면 해당 <xref:System.Windows.Duration>합니다. 모든 애니메이션 처럼 키 프레임 애니메이션을 사용 하 여 해당 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 있는지 여부를 보유 최종 값은 활성 기간의 끝에 도달 하면 결정할 속성입니다. 자세한 내용은 [타이밍 동작 개요](timing-behaviors-overview.md)를 참조하세요.  
  
 다음 예제에서는 합니다 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 보여 주기 위해 앞의 예제에 정의 된 개체 하는 방법을 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 및 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 속성의 작동 합니다.  
  
- 첫 번째 키 프레임은 애니메이션의 출력 값을 0으로 즉시 설정합니다.  
  
- 두 번째 키 프레임은 0에서 350으로 애니메이션 효과를 줍니다. 이 키 프레임은 첫 번째 키 프레임이 종료된 후(시간 = 0초) 시작되고 2초 동안 재생된 후 시간 = 0:0:2에 종료됩니다.  
  
- 세 번째 키 프레임은 350에서 50으로 애니메이션 효과를 줍니다. 이 키 프레임은 두 번째 키 프레임이 종료된 후(시간 = 2초) 시작되고 5초 동안 재생된 후 시간 = 0:0:7에 종료됩니다.  
  
- 네 번째 키 프레임은 50에서 200으로 애니메이션 효과를 줍니다. 이 키 프레임은 세 번째 키 프레임이 종료된 후(시간 = 7초) 시작되고 1초 동안 재생된 후 시간 = 0:0:8에 종료됩니다.  
  
- 때문에 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 애니메이션의 속성을 10 초로 설정 된, 애니메이션 끝나기 전에 2 초에 대 한 최종 값을 보유 시간 = 0:0:10입니다.  
  
 [!code-xaml[keyframes_ovw_snippet#BasicKeyFrameExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyFramesIntroduction.xaml#basickeyframeexamplewholepage)]  
  
<a name="interpolationmethods"></a>   
## <a name="interpolation-methods"></a>보간 방법  
 이전 섹션에서는 일부 키 프레임 애니메이션이 여러 보간 방법을 지원한다고 언급했습니다. 애니메이션의 보간은 애니메이션이 지속 기간 동안 값 사이에서 전환되는 방식을 설명합니다. 애니메이션에서 사용하는 키 프레임 형식을 선택하여 해당 키 프레임 세그먼트에 대한 보간 방법을 정의할 수 있습니다. 보간 방법 종류에는 선형, 불연속 및 스플라인의 세 가지가 있습니다.  
  
### <a name="linear-interpolation"></a>선형 보간  
 선형 보간을 사용하면 애니메이션이 세그먼트 기간에 일정한 속도로 진행됩니다. 예를 들어 키 프레임 세그먼트가 5초 동안 0에서 10으로 전환되면 애니메이션은 지정된 시간에 다음 값을 출력합니다.  
  
|시간|출력 값|  
|----------|------------------|  
|0|0|  
|1|2|  
|2|4|  
|3|6|  
|4|8|  
|4.25|8.5|  
|4.5|9|  
|5|10|  
  
### <a name="discrete-interpolation"></a>불연속 보간  
 불연속 보간을 사용하면 애니메이션 함수가 보간 없이 한 값에서 다음 값으로 이동합니다. 키 프레임 세그먼트가 5초 동안 0에서 10으로 전환되면 애니메이션은 지정된 시간에 다음 값을 출력합니다.  
  
|시간|출력 값|  
|----------|------------------|  
|0|0|  
|1|0|  
|2|0|  
|3|0|  
|4|0|  
|4.25|0|  
|4.5|0|  
|5|10|  
  
 세그먼트 기간의 거의 끝날 때까지 애니메이션이 출력 값을 변경하지 않는 방식을 살펴보세요.  
  
 스플라인 보간은 좀 더 복잡합니다. 이 방식은 다음 섹션에서 설명합니다.  
  
<a name="anim_spline"></a>   
### <a name="splined-interpolation"></a>스플라인 보간  
 스플라인 보간은 보다 실제적인 타이밍 효과를 얻기 위해 사용할 수 있습니다. 애니메이션은 실제 환경에서 발생하는 효과를 모방하는 데 주로 사용되므로 개발자는 개체의 가속 및 감속을 보다 세밀하게 제어하고 타이밍 세그먼트를 면밀히 조작해야 할 수 있습니다. 스플라인 키 프레임을 사용하면 스플라인 보간을 사용하여 애니메이션 효과를 줄 수 있습니다. 다른 키 프레임을 사용 하 여 지정 된 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 및 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>. 스플라인 키 프레임을 사용 하 여도 지정 된 <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame.KeySpline%2A>합니다. 다음 예제에서는 단일 스플라인 키 프레임을 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>입니다. 통지를 <xref:System.Windows.Media.Animation.KeySpline> 스플라인 키 프레임을 다른 형식의 키 프레임에서 다른 이유는 속성입니다.  
  
 [!code-xaml[keyframes_ovw_snippet#SingleSplineKeyFrameExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#singlesplinekeyframeexample)]  
  
 입방형 3차원 곡선은 시작점, 끝점 및 두 개의 제어점에 의해 정의됩니다. <xref:System.Windows.Media.Animation.KeySpline> 스플라인 키 프레임의 속성 (0, 0)에서 (1, 1)를 확장 하는 베 지 어 곡선의 두 제어점을 정의 합니다. 첫 번째 제어점은 3차원 곡선의 첫 번째 절반 부분에 대한 곡선 요소를 제어하 고 두 번째 제어점은 3차원 곡선의 두 번째 절반 부분에 대한 곡선 요소를 제어합니다. 결과 곡선은 해당 스플라인 키 프레임의 변동률을 설명합니다. 곡선이 더 가파를수록 키 프레임 값이 더 빠르게 변경됩니다. 곡선이 평평해지면 키 프레임은 값을 더 느리게 변경합니다.  
  
 사용할 수 있습니다 <xref:System.Windows.Media.Animation.KeySpline> 떨어지는 물 이나 튕기는 공과 같은 물리적 궤적을 시뮬레이트하거나 다른 "점점" 및 "점점 멀리" 효과 동작 애니메이션에 적용 하 합니다. 배경 페이드 또는 컨트롤 단추 리바운드와 같은 사용자 상호 작용 효과의 경우 스플라인 보간을 적용하여 특정한 방식으로 애니메이션의 변동률을 빠르게 하거나 느리게 할 수 있습니다.  
  
 다음 예제에서는 지정 된 <xref:System.Windows.Media.Animation.KeySpline> 의 0, 1 1, 0, 다음 베 지 어 곡선을 만듭니다.  
  
 ![베 지 어 곡선](./media/graphicsmm-keyspline-0-1-1-0.png "graphicsmm_keyspline_0_1_1_0")  
제어점 (0.0, 1.0) 및 (1.0, 0.0)을 갖는 키 스플라인  
  
 [!code-xaml[keyframes_ovw_snippet#SingleSplineKeyFrameExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#singlesplinekeyframeexample)]  
  
 이 키 프레임을 사용하면 애니메이션이 시작할 때 빨라졌다가 느려진 후 끝나기 전에 다시 빨라집니다.  
  
 다음 예제에서는 지정 된 <xref:System.Windows.Media.Animation.KeySpline> 다음 베 지 어 곡선을 만듭니다으로 0.5, 0.25 0.75, 1.0의 합니다.  
  
 ![베 지 어 곡선](./media/graphicsmm-keyspline-025-050-075-10.png "graphicsmm_keyspline_025_050_075_10")  
제어점 (0.25, 0.5) 및 (0.75, 1.0)을 갖는 키 스플라인  
  
 [!code-xaml[keyframes_ovw_snippet#SingleSplineKeyFrameExampleInline3](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#singlesplinekeyframeexampleinline3)]  
  
 이 3차원 곡선의 곡률은 거의 변경되지 않으므로 이 키 프레임 애니메이션은 거의 일정한 속도를 유지하다가 끝에서는 다소 느려집니다.  
  
 다음 예제에서는 한 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 사각형의 위치에 애니메이션 효과를 합니다. 때문에 합니다 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 사용 하 여 <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame> 각 키 프레임 값 간의 전환에 스플라인 보간을 사용 하 여 개체입니다.  
  
 [!code-xaml[keyframes_ovw_snippet#SplinedInterpolationExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#splinedinterpolationexample)]  
  
 스플라인 보간은 이해하기 어려울 수 있으므로 다른 설정을 사용해서 시험해보면 도움이 될 수 있습니다. [키 스플라인 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160011)을 사용하여 키 스플라인 값을 변경하고 애니메이션에 나타나는 결과를 볼 수 있습니다.  
  
<a name="combininginterpolationmethods"></a>   
### <a name="combining-interpolation-methods"></a>보간 방법 조합  
 단일 키 프레임 애니메이션에서 여러 다른 보간 형식을 갖는 키 프레임을 사용할 수 있습니다. 다른 보간을 사용하는 두 개의 키 프레임 애니메이션이 서로를 따라 진행되면 두 번째 키 프레임의 보간 방법이 첫 번째 값에서 두 번째 값으로의 전환을 만드는 데 사용됩니다.  
  
 다음 예제에서는 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> 해당 사용 하 여 선형, 스플라인 및 불연속 보간 만들어집니다.  
  
 [!code-xaml[keyframes_ovw_snippet#ComboInterpolationExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#combointerpolationexample)]  
  
<a name="keytimes"></a>   
## <a name="more-about-duration-and-key-times"></a>기간 및 키 시간에 대한 추가 정보  
 다른 애니메이션과 마찬가지로 키 프레임 애니메이션에는 한 <xref:System.Windows.Duration> 속성입니다. 애니메이션의 지정 외에도 <xref:System.Windows.Duration>, 어떤 부분이 해당 기간 동안 각 키 프레임에 지정 된을 지정 해야 합니다. 설명 하 여 이렇게는 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 각 애니메이션의 키 프레임에 대 한 합니다. 각 키 프레임의 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 해당 키 프레임이 끝나는 시기를 지정 합니다.  
  
 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 속성 키 시간이 재생 길이 지정 하지 않습니다. 키 프레임이 재생되는 기간은 키 프레임이 끝나는 시점, 이전 키 프레임 끝난 시점 및 애니메이션의 지속 시간에 의해 결정됩니다. 키 시간은 시간 값 백분율 또는 특수 한 값으로 지정할 수 있습니다 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> 또는 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A>합니다.  
  
 다음 목록에서는 키 시간을 지정하는 여러 가지 방법을 설명합니다.  
  
### <a name="timespan-values"></a>TimeSpan 값  
 사용할 수 있습니다 <xref:System.TimeSpan> 지정 하는 값을 <xref:System.Windows.Media.Animation.KeyTime>입니다. 값은 0보다 크거나 같고 애니메이션의 지속 시간보다 작거나 같아야 합니다. 다음 예제에서는 기간이 10초이고 해당 키 시간이 시간 값으로 지정된 4개의 키 프레임을 갖는 애니메이션을 보여 줍니다.  
  
- 첫 번째 키 프레임은 처음 3초 동안 기준 값에서 100까지 애니메이션 효과를 준 다음 시간 = 0:0:03에서 끝납니다.  
  
- 두 번째 키 프레임은 100에서 200으로 애니메이션 효과를 줍니다. 이 키 프레임은 첫 번째 키 프레임이 종료된 후(시간 = 3초) 시작되고 5초 동안 재생된 후 시간 = 0:0:8에 종료됩니다.  
  
- 세 번째 키 프레임은 200에서 500으로 애니메이션 효과를 줍니다. 이 키 프레임은 두 번째 키 프레임이 종료된 후(시간 = 8초) 시작되고 1초 동안 재생된 후 시간 = 0:0:9에 종료됩니다.  
  
- 네 번째 키 프레임은 500에서 600으로 애니메이션 효과를 줍니다. 이 키 프레임은 세 번째 키 프레임이 종료된 후(시간 = 9초) 시작되고 1초 동안 재생된 후 시간 = 0:0:10에 종료됩니다.  
  
 [!code-xaml[keyframes_ovw_snippet#TimeSpanKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#timespankeytimeexample)]  
  
### <a name="percentage-values"></a>백분율 값  
 백분율 값을 키 프레임 애니메이션의 일정 비율에서 끝나도록 지정 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>합니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서는 숫자를 입력한 후 `%` 기호를 입력하여 백분율을 지정합니다. 코드를 사용 하 여는 <xref:System.Windows.Media.Animation.KeyTime.FromPercent%2A> 메서드를 전달는 <xref:System.Double> 백분율을 나타내는입니다. 값은 0보다 크거나 같고 100%보다 작거나 같아야 합니다. 다음 예제에서는 기간이 10초이고 해당 키 시간이 백분율로 지정된 4개의 키 프레임을 갖는 애니메이션을 보여 줍니다.  
  
- 첫 번째 키 프레임은 처음 3초 동안 기준 값에서 100까지 애니메이션 효과를 준 다음 시간 = 0:0:3에서 끝납니다.  
  
- 두 번째 키 프레임은 100에서 200으로 애니메이션 효과를 줍니다. 이 키 프레임은 첫 번째 키 프레임이 종료된 후(시간 = 3초) 시작되고 5초 동안 재생된 후 시간 = 0:0:8(0.8 * 10 = 8)에 종료됩니다.  
  
- 세 번째 키 프레임은 200에서 500으로 애니메이션 효과를 줍니다. 이 키 프레임은 두 번째 키 프레임이 종료된 후(시간 = 8초) 시작되고 1초 동안 재생된 후 시간 = 0:0:9(0.9 * 10 = 9)에 종료됩니다.  
  
- 네 번째 키 프레임은 500에서 600으로 애니메이션 효과를 줍니다. 이 키 프레임은 세 번째 키 프레임이 종료된 후(시간 = 9초) 시작되고 1초 동안 재생된 후 시간 = 0:0:10(1 * 10 = 10)에 종료됩니다.  
  
 [!code-xaml[keyframes_ovw_snippet#PercentageKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#percentagekeytimeexample)]  
  
### <a name="special-value-uniform"></a>특수 값, Uniform  
 사용 하 여 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> 동일한 양의 시간을 각 키 프레임을 원하는 경우 시간입니다.  
  
 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> 키 시간 나눈 사용 가능한 시간 동일 하 게 각 키 프레임의 종료 시간을 확인 하려면 키 프레임 수입니다. 다음 예제에서는 기간이 10 초를 사용 하 여 애니메이션을 보여 줍니다. 및 해당 키 시간이 4 개의 키 프레임으로 지정 된 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>합니다.  
  
- 첫 번째 키 프레임은 처음 2.5초 동안 기준 값에서 100까지 애니메이션 효과를 준 다음 시간 = 0:0:2.5에서 끝납니다.  
  
- 두 번째 키 프레임은 100에서 200으로 애니메이션 효과를 줍니다. 이 키 프레임은 첫 번째 키 프레임이 종료된 후(시간 = 2.5초) 시작되고 약 2.5초 동안 재생된 후 시간 = 0:0:5에 종료됩니다.  
  
- 세 번째 키 프레임은 200에서 500으로 애니메이션 효과를 줍니다. 이 키 프레임은 두 번째 키 프레임이 종료된 후(시간 = 5초) 시작되고 2.5초 동안 재생된 후 시간 = 0:0:7.5에 종료됩니다.  
  
- 네 번째 키 프레임은 500에서 600으로 애니메이션 효과를 줍니다. 이 키 프레임은 두 번째 키 프레임이 종료된 후(시간 = 7.5초) 시작되고 2.5초 동안 재생된 후 시간 = 0:0:1에 종료됩니다.  
  
 [!code-xaml[keyframes_ovw_snippet#UniformKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#uniformkeytimeexample)]  
  
### <a name="special-value-paced"></a>특수 값, Paced  
 사용 하 여 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> 일정 한 속도로 애니메이션 효과 적용할 때 시간이 있습니다.  
  
 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> 키 시간은 각 프레임의 기간을 결정 하는 키 프레임의 각 길이 따라 사용할 수 있는 시간을 할당 합니다.  이를 통해 애니메이션의 속도가 일정하게 유지되는 동작이 제공됩니다.  다음 예제에서는 기간이 10 초를 사용 하 여 애니메이션을 보여 줍니다. 및 해당 키 시간이 세 가지 키 프레임으로 지정 된 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A>합니다.  
  
 [!code-xaml[keyframes_ovw_snippet#PacedKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#pacedkeytimeexample)]  
  
 이때 마지막 키 프레임의 키 시간이 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> 또는 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>, 확인된 된 키 시간이 100%로 설정 됩니다. 다중 프레임 애니메이션의 첫 번째 키 프레임 속도가 지정되면 확인된 키 시간이 0으로 설정됩니다. (키 프레임 컬렉션에 단일 키 프레임만 포함되며 속도가 지정된 키 프레임인 경우 확인된 키 시간이 100%로 설정됩니다.)  
  
 단일 키 프레임 애니메이션 내의 다른 키 프레임은 다른 키 시간 형식을 사용할 수 있습니다.  
  
<a name="combiningkeytimes"></a>   
## <a name="combining-key-times-out-of-order-key-frames"></a>키 시간 결합, 정렬되지 않은 키 프레임  
 키 프레임을 사용 하 여 다른 <xref:System.Windows.Media.Animation.KeyTime> 동일한 애니메이션의 값 형식이 있습니다. 또한 키 프레임을 재생되는 순서대로 추가하는 것이 좋지만 반드시 그래야 할 필요는 없습니다. 애니메이션 및 타이밍 시스템은 정렬되지 않은 키 프레임을 확인할 수 있습니다. 잘못된 키 프레임을 갖는 키 시간은 무시됩니다.  
  
 다음 목록에서는 키 프레임 애니메이션의 키 프레임에 대한 키 시간을 확인하는 절차를 설명합니다.  
  
1. 확인할 <xref:System.TimeSpan> <xref:System.Windows.Media.Animation.KeyTime> 값입니다.  
  
2. 키 프레임 애니메이션이 정방향 반복을 완료하는 데 걸리는 총 시간을 나타내는 애니메이션의 *총 보간 시간*을 확인합니다.  
  
    1. 경우 애니메이션의 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 아닙니다 <xref:System.Windows.Duration.Automatic%2A> 또는 <xref:System.Windows.Duration.Forever%2A>, 총 보간 시간은 애니메이션의 값인 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 속성입니다.  
  
    2. 그렇지 않으면 총 보간 시간은 가장 큽니다 <xref:System.TimeSpan> <xref:System.Windows.Media.Animation.KeyTime> 있을 경우 해당 키 프레임 간에 지정 된 값입니다.  
  
    3. 이 값이 없으면 총 보간 시간은 1초입니다.  
  
3. 총 보간 시간 값을 확인 하는 데 <xref:System.Windows.Media.Animation.KeyTimeType.Percent> <xref:System.Windows.Media.Animation.KeyTime> 값입니다.  
  
4. 이전 단계에서 확인하지 않은 경우 마지막 키 프레임을 확인합니다. 경우는 <xref:System.Windows.Media.Animation.KeyTime> 키 프레임은 마지막 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> 또는 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A>, 확인 된 시간은 총 보간 시간은 같게 됩니다.  
  
     경우는 <xref:System.Windows.Media.Animation.KeyTime> 첫 번째 키 프레임은 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> 이 애니메이션에 두 개 키 프레임에서 해결 하 고 해당 <xref:System.Windows.Media.Animation.KeyTime> 하나만 키 프레임이 없으면 0입니다; 값 및 해당 <xref:System.Windows.Media.Animation.KeyTime> 값은 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A>, 총 해결 되었기 이전 단계에 설명 된 대로 보간 시간입니다.  
  
5. 남은 해결할 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> <xref:System.Windows.Media.Animation.KeyTime> 값: 각 학생은 사용할 수 있는 시간을 균등 하 게 요약 하는 합니다.  이 과정에서 unresolved <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> <xref:System.Windows.Media.Animation.KeyTime> 값으로 일시적으로 처리 됩니다 <xref:System.Windows.Media.Animation.KeyTime.Uniform%2A> <xref:System.Windows.Media.Animation.KeyTime> 값 및 임시 해결 시간 가져오기.  
  
6. 해결 합니다 <xref:System.Windows.Media.Animation.KeyTime> 갖는 키 프레임의 값 키 시간을 지정 하지 않으면 해결 된 선언으로 가장 가까운 키 프레임을 사용 하 여 <xref:System.Windows.Media.Animation.KeyTime> 값입니다.  
  
7. 남은 해결할 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> <xref:System.Windows.Media.Animation.KeyTime> 값입니다. <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> <xref:System.Windows.Media.Animation.KeyTime> 사용 된 <xref:System.Windows.Media.Animation.KeyTime> 값은 인접 키 프레임이 해당 해결된 시간을 결정 합니다.  이것은 이 키 프레임의 확인된 시간 동안 애니메이션의 속도가 일정한지 확인하기 위한 것입니다.  
  
8. 즉, 해결된 시간 (기본 키), 순서 및 (보조 키)를 선언 순서 대로 키 프레임 정렬, 확인 된 키 프레임을 기반으로 안정적인 정렬을 사용 <xref:System.Windows.Media.Animation.KeyTime> 값입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.KeyTime>
- <xref:System.Windows.Media.Animation.KeySpline>
- <xref:System.Windows.Media.Animation.Timeline>
- [키 스플라인 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160011)
- [키 프레임 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160012)
- [애니메이션 개요](animation-overview.md)
- [Storyboard 개요](storyboards-overview.md)
- [키 프레임 방법 항목](key-frame-animation-how-to-topics.md)
- [타이밍 동작 개요](timing-behaviors-overview.md)
