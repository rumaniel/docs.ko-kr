---
title: 속성 애니메이션 기술 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- animation [WPF], properties [WPF], methods for
- properties [WPF], methods for animating
ms.assetid: 74f61413-f8c0-4e75-bf04-951886426c8b
ms.openlocfilehash: ebee350f69b5c5e4f9d38c452b9c87bf003528ee
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62002263"
---
# <a name="property-animation-techniques-overview"></a>속성 애니메이션 기술 개요
이 항목에서는 storyboard, 로컬 애니메이션, 클록 및 프레임당 애니메이션 등, 속성에 애니메이션 효과를 주는 다양한 접근 방법을 설명합니다.  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목을 이해하려면 [애니메이션 개요](animation-overview.md)에 설명된 기본 애니메이션 기능에 대해 잘 알고 있어야 합니다.  
  
<a name="summary"></a>   
## <a name="different-ways-to-animate"></a>애니메이션 효과를 주는 다양한 방법  
 속성에 애니메이션 효과를 주는 다양한 시나리오가 있으므로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 속성에 애니메이션 효과를 주는 몇 가지 접근 방법을 제공합니다.  
  
 각 접근 방법에 대해 다음 표에는 인스턴스별로, 스타일, 컨트롤 템플릿 또는 데이터 템플릿에서 사용할 수 있는지, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서 사용할 수 있는지 여부 및 해당 접근 방식을 사용하여 애니메이션을 대화형으로 제어할 수 있는지가 나와 있습니다.  "인스턴스별"은 스타일, 컨트롤 템플릿 또는 데이터 템플릿이 아닌 개체의 인스턴스에 직접 애니메이션 또는 storyboard를 적용하는 기술을 나타냅니다.  
  
|애니메이션 기술|시나리오|XAML 지원|대화형으로 제어 가능|  
|-------------------------|---------------|-------------------|--------------------------------|  
|Storyboard 애니메이션|Per-instance, <xref:System.Windows.Style>, <xref:System.Windows.Controls.ControlTemplate>, <xref:System.Windows.DataTemplate>|예|예|  
|로컬 애니메이션|인스턴스별|아니요|아니요|  
|클록 애니메이션|인스턴스별|아니요|예|  
|프레임당 애니메이션|인스턴스별|아니요|N/A|  
  
<a name="storyboard_animations"></a>   
## <a name="storyboard-animations"></a>Storyboard 애니메이션  
 사용 하 여를 <xref:System.Windows.Media.Animation.Storyboard> 정의 하 고 애니메이션을 적용 하려는 경우 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]대화형으로 시작, 복잡 한 애니메이션 트리 만들거나 애니메이션 효과 줄 애니메이션 제어를 <xref:System.Windows.Style>, <xref:System.Windows.Controls.ControlTemplate> 또는 <xref:System.Windows.DataTemplate>합니다. 애니메이션을 적용할 개체에 대 한를 <xref:System.Windows.Media.Animation.Storyboard>, 이어야 합니다는 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement>를 설정 하려면 사용 해야 합니다를 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement>. 자세한 내용은 [Storyboard 개요](storyboards-overview.md)를 참조하세요.  
  
 <xref:System.Windows.Media.Animation.Storyboard> 는 특수 한 유형의 컨테이너 <xref:System.Windows.Media.Animation.Timeline> 포함 된 애니메이션에 대 한 대상 정보를 제공 합니다. 애니메이션 효과 주려는 <xref:System.Windows.Media.Animation.Storyboard>, 다음 세 단계를 완료 합니다.  
  
1. 선언 된 <xref:System.Windows.Media.Animation.Storyboard> 및 하나 이상의 애니메이션 합니다.  
  
2. 사용 된 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 및 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 대상 개체를 지정 하는 속성 및 각 애니메이션의 속성을 연결 합니다.  
  
3. (코드에만 해당) 정의 된 <xref:System.Windows.NameScope> 에 대 한는 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement>합니다. 등록 된 애니메이션 효과를 줄 개체의 이름을 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement>합니다.  
  
4. 시작 된 <xref:System.Windows.Media.Animation.Storyboard>합니다.  
  
 시작을 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션 효과 주는 속성에 애니메이션을 적용 하 고 시작 합니다. 시작 하는 방법은 두 가지를 <xref:System.Windows.Media.Animation.Storyboard>: 사용할 수는 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 에서 제공 하는 메서드는 <xref:System.Windows.Media.Animation.Storyboard> 클래스를 사용할 수 있습니다를 <xref:System.Windows.Media.Animation.BeginStoryboard> 작업. 애니메이션을 적용 하는 유일한 방법은 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 사용 하는 것을 <xref:System.Windows.Media.Animation.BeginStoryboard> 작업 합니다. A <xref:System.Windows.Media.Animation.BeginStoryboard> 작업에서 사용할 수는 <xref:System.Windows.EventTrigger>, 속성 <xref:System.Windows.Trigger>, 또는 <xref:System.Windows.DataTrigger>.  
  
 다음 표에서 다양 한 위치를 보여 줍니다. 여기서 각 <xref:System.Windows.Media.Animation.Storyboard> 시작 기술이 지원 되: 인스턴스별, 스타일, 컨트롤 템플릿 및 데이터 템플릿.  
  
|storyboard 시작 방법...|인스턴스별|스타일|컨트롤 템플릿|데이터 템플릿|예제|  
|--------------------------------|-------------------|-----------|----------------------|-------------------|-------------|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> 및 <xref:System.Windows.EventTrigger>|예|예|예|예|[Storyboard를 사용하여 속성에 애니메이션 효과 주기](how-to-animate-a-property-by-using-a-storyboard.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> 속성 <xref:System.Windows.Trigger>|아니요|예|예|예|[속성 값이 변경될 때 애니메이션 트리거](how-to-trigger-an-animation-when-a-property-value-changes.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> 및 <xref:System.Windows.DataTrigger>|아니요|예|예|예|[방법: 데이터가 변경 될 때 애니메이션 트리거](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/aa970679(v=vs.90))|  
|<xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드|예|아니요|아니요|아니요|[Storyboard를 사용하여 속성에 애니메이션 효과 주기](how-to-animate-a-property-by-using-a-storyboard.md)|  
  
 에 대 한 자세한 내용은 <xref:System.Windows.Media.Animation.Storyboard> 개체를 참조 합니다 [Storyboard 개요](storyboards-overview.md)합니다.  
  
## <a name="local-animations"></a>로컬 애니메이션  
 로컬 애니메이션의 종속성 속성에 애니메이션을 적용 하는 편리한 방법을 제공 <xref:System.Windows.Media.Animation.Animatable> 개체입니다. 속성에 단일 애니메이션을 적용하며 애니메이션이 시작된 후에 대화형으로 제어할 필요가 없으면 로컬 애니메이션을 사용합니다. 와 달리를 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션, 로컬 애니메이션을 애니메이션을 적용할 수와 연관 되지 않은 개체를 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement>합니다. 또한 정의할 필요가 없습니다를 <xref:System.Windows.NameScope> 이러한 유형의 애니메이션에 대 한 합니다.  
  
 로컬 애니메이션은 코드에만 사용할 수 있으며, 스타일, 컨트롤 템플릿 또는 데이터 템플릿에는 정의할 수 없습니다. 로컬 애니메이션은 시작된 후에 대화형으로 제어할 수 없습니다.  
  
 로컬 애니메이션을 사용하여 애니메이션 효과를 주려면 다음 단계를 완료합니다.  
  
1. 만들기는 <xref:System.Windows.Media.Animation.AnimationTimeline> 개체입니다.  
  
2. 사용 하 여는 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 적용할 애니메이션 효과 주려는 개체의 메서드는 <xref:System.Windows.Media.Animation.AnimationTimeline> 지정 하는 속성입니다.  
  
 다음 예제에서는 너비 및 배경색 색에 애니메이션을 적용 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.Button>합니다.  
  
 [!code-cpp[animateproperty#11](~/samples/snippets/cpp/VS_Snippets_Wpf/animateproperty/CPP/LocalAnimationExample.cpp#11)]
 [!code-csharp[animateproperty#11](~/samples/snippets/csharp/VS_Snippets_Wpf/animateproperty/CSharp/LocalAnimationExample.cs#11)]
 [!code-vb[animateproperty#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animateproperty/VisualBasic/LocalAnimationExample.vb#11)]  
  
## <a name="clock-animations"></a>클록 애니메이션  
 사용 하 여 <xref:System.Windows.Media.MediaPlayer.Clock%2A> 를 사용 하지 않고 애니메이션 효과 주려는 개체는 <xref:System.Windows.Media.Animation.Storyboard> 복잡 한 타이밍 트리를 만들거나 시작 되 면 애니메이션을 대화형으로 제어 하려는 합니다. 클록 개체를 사용 하 여 모든 종속성 속성에 애니메이션 효과를 <xref:System.Windows.Media.Animation.Animatable> 개체입니다.  
  
 사용할 수 없습니다 <xref:System.Windows.Media.Animation.Clock> 개체 직접 스타일에서 애니메이션 효과를 제어 템플릿 또는 데이터 템플릿. (실제로 애니메이션 및 타이밍 시스템에서 사용 <xref:System.Windows.Media.Animation.Clock> 이러한 스타일, 컨트롤 템플릿 및 데이터 템플릿이 하지만 애니메이션 효과 줄 개체 만들어야 <xref:System.Windows.Media.Animation.Clock> 에서 개체를 <xref:System.Windows.Media.Animation.Storyboard>합니다. 간의 관계에 대 한 자세한 내용은 <xref:System.Windows.Media.Animation.Storyboard> 개체 및 <xref:System.Windows.Media.Animation.Clock> 개체를 참조 합니다 [애니메이션 및 타이밍 시스템 개요](animation-and-timing-system-overview.md).)  
  
 단일 적용할 <xref:System.Windows.Media.Animation.Clock> 속성에 다음 단계를 완료 합니다.  
  
1. 만들기는 <xref:System.Windows.Media.Animation.AnimationTimeline> 개체입니다.  
  
2. 사용 하 여는 <xref:System.Windows.Media.Animation.AnimationTimeline.CreateClock%2A> 메서드를 <xref:System.Windows.Media.Animation.AnimationTimeline> 만들려는 <xref:System.Windows.Media.Animation.AnimationClock>.  
  
3. 사용 하 여는 <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%2A> 적용할 애니메이션 효과 주려는 개체의 메서드는 <xref:System.Windows.Media.Animation.AnimationClock> 지정할 속성입니다.  
  
 다음 예제에서는 만드는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.AnimationClock> 두 개의 비슷한 속성에 적용 합니다.  
  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/AnimationClockExample.cs#graphicsmmcreateanimationclockwholeclass)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/animationclockexample.vb#graphicsmmcreateanimationclockwholeclass)]  
  
 타이밍 트리를 만들고 속성에 애니메이션 효과를 주는 데 사용하려면 다음 단계를 완료합니다.  
  
1. 사용 하 여 <xref:System.Windows.Media.Animation.ParallelTimeline> 고 <xref:System.Windows.Media.Animation.AnimationTimeline> 타이밍 트리를 만드는 개체입니다.  
  
2. 사용 하 여는 <xref:System.Windows.Media.Animation.TimelineGroup.CreateClock%2A> 루트 <xref:System.Windows.Media.Animation.ParallelTimeline> 만들려는 <xref:System.Windows.Media.Animation.ClockGroup>합니다.  
  
3. 반복 합니다 <xref:System.Windows.Media.Animation.ClockGroup.Children%2A> 의 <xref:System.Windows.Media.Animation.ClockGroup> 자식 적용 <xref:System.Windows.Media.Animation.Clock> 개체입니다. 각 <xref:System.Windows.Media.Animation.AnimationClock> 자식을 사용 하 여는 <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%2A> 적용할 애니메이션 효과 주려는 개체의 메서드는 <xref:System.Windows.Media.Animation.AnimationClock> 지정할 속성  
  
 클록 개체에 대한 자세한 내용은 [애니메이션 및 타이밍 시스템 개요](animation-and-timing-system-overview.md)를 참조하세요.  
  
## <a name="per-frame-animation-bypass-the-animation-and-timing-system"></a>프레임당 애니메이션: 애니메이션 및 타이밍 시스템 무시  
 이 접근 방법은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션 시스템을 완전히 무시해야 할 때 사용합니다. 이 방법에 대한 한 가지 시나리오는 애니메이션의 각 단계에서 개체 상호 작용의 마지막 집합에 따라 개체가 다시 계산되어야 하는 물리학 애니메이션입니다.  
  
 스타일, 컨트롤 템플릿 또는 데이터 템플릿 내부에서는 프레임당 애니메이션을 정의할 수 없습니다.  
  
 프레임별으로 애니메이션 효과에 등록 된 <xref:System.Windows.Media.CompositionTarget.Rendering> 애니메이션 효과 적용할 개체가 포함 된 개체의 이벤트입니다. 이 이벤트 처리기 메서드는 프레임마다 한 번씩 호출됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]가 시각적 트리의 지속되는 렌더링 데이터를 컴퍼지션 트리로 마샬링할 때마다 이벤트 처리기 메서드가 호출됩니다.  
  
 이벤트 처리기에서 애니메이션 효과에 필요한 계산을 수행하고 이러한 값을 사용하여 애니메이션 효과를 적용하려는 개체의 속성을 설정합니다.  
  
 현재 프레임의 프레젠테이션 시간을 얻기 위해 합니다 <xref:System.EventArgs> 와 연결 된 이벤트로 캐스팅 될 수 <xref:System.Windows.Media.RenderingEventArgs>를 제공 하는 <xref:System.Windows.Media.RenderingEventArgs.RenderingTime%2A> 현재 프레임을 가져오는 데 사용할 수 있는 속성의 렌더링 시간.  
  
 자세한 내용은 참조는 <xref:System.Windows.Media.CompositionTarget.Rendering> 페이지입니다.  
  
## <a name="see-also"></a>참고자료

- [애니메이션 개요](animation-overview.md)
- [Storyboard 개요](storyboards-overview.md)
- [애니메이션 및 타이밍 시스템 개요](animation-and-timing-system-overview.md)
- [종속성 속성 개요](../advanced/dependency-properties-overview.md)
