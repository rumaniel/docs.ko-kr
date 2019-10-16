---
title: 애니메이션 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboards [WPF], animations
- animations [WPF], overview
ms.assetid: bd9ce563-725d-4385-87c9-d7ee38cf79ea
ms.openlocfilehash: 5c776942bced836437fdcb8aaf30faef48e3aaff
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67780154"
---
# <a name="animation-overview"></a>애니메이션 개요

<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 강력한 매력적인 사용자 인터페이스와 멋진 문서를 만드는 데 사용할 수 있는 그래픽 및 레이아웃 기능 집합을 제공 합니다. 애니메이션은 매력적인 사용자 인터페이스를 훨씬 더 화려하고 유용하게 만들어줄 수 있습니다. 방금 배경색에 애니메이션을 적용 하거나 애니메이션을 적용 하 여 <xref:System.Windows.Media.Transform>, 만으로도 멋진 화면 전환을 하거나 유용한 시각적 효과 입력할 수 있습니다.

이 개요에 대해 소개 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션 및 타이밍 시스템입니다. 애니메이션에 중점을 둡니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 스토리 보드를 사용 하 여 개체입니다.

<a name="introducinganimations"></a>

## <a name="introducing-animations"></a>애니메이션 소개

애니메이션은 마지막까지 조금씩 달라지는 일련의 이미지를 빠르게 순환하면서 만들어지는 효과입니다. 뇌는 이미지 그룹을 변화하는 하나의 영상으로 인식합니다. 영화에서는 많은 사진 또는 프레임을 초별로 기록하는 카메라를 사용하여 이러한 효과를 만듭니다. 프로젝터에서 프레임이 재생되면 청중은 동영상을 보게 됩니다.

컴퓨터의 애니메이션도 유사합니다. 예를 들어 사각형 그림을 보기에서 페이드 아웃하는 프로그램은 다음과 같이 작동할 수 있습니다.

- 프로그램이 타이머를 만듭니다.

- 프로그램이 설정된 간격으로 타이머를 확인하여 경과된 시간을 파악합니다.

- 프로그램이 타이머를 확인할 때마다 경과된 시간에 따라 사각형의 현재 불투명도 값을 계산합니다.

- 그런 다음 새 값으로 사각형을 업데이트한 후 그립니다.

이전 버전 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 개발자가 만들고가 자체 타이밍 시스템을 관리 하거나 특수 한 사용자 지정 라이브러리를 사용 해야 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 관리 되는 코드를 통해 노출 되는 효율적인 타이밍 시스템이 포함 하 고 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 에 긴밀히 통합 되 고는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 프레임 워크입니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션을 사용하면 쉽게 컨트롤 및 기타 그래픽 개체에 애니메이션 효과를 줄 수 있습니다.

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 타이밍 시스템을 관리하고 화면을 효율적으로 다시 그리는 모든 백그라운드 작업을 처리합니다. 그뿐 아니라 이러한 효과를 달성하는 기법이 아닌, 만들려는 효과에 집중할 수 있도록 하는 타이밍 클래스를 제공합니다. 또한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 클래스가 상속할 수 있는 애니메이션 기본 클래스를 노출하여 사용자 고유의 애니메이션을 쉽게 만들 수 있도록 하므로 애니메이션을 사용자 지정할 수 있습니다. 이러한 사용자 지정 애니메이션은 표준 애니메이션 클래스에 비해 성능상의 이점도 큽니다.

<a name="thewpftimingsystem"></a>

## <a name="wpf-property-animation-system"></a>WPF 속성 애니메이션 시스템

타이밍 시스템에 대 한 몇 가지 중요 한 개념을 이해 하면 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션을 쉽게 사용할 수 있습니다. 가장 중요 한 한다는 것 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], 개별 속성에 애니메이션을 적용 하 여 개체를 애니메이션 합니다. 예를 들어, 프레임 워크 요소가 확장 되도록 애니메이션을 적용 하면 해당 <xref:System.Windows.FrameworkElement.Width%2A> 고 <xref:System.Windows.FrameworkElement.Height%2A> 속성입니다. 보기에서 사라지게 하는 개체를 위해 애니메이션을 적용 하면 해당 <xref:System.Windows.UIElement.Opacity%2A> 속성입니다.

속성에 애니메이션 기능을 부여하려면 다음 세 가지 요구 사항을 충족해야 합니다.

- 종속성 속성이어야 합니다.

- 상속 된 클래스에 속해 있어야 <xref:System.Windows.DependencyObject> 하 고 구현 합니다 <xref:System.Windows.Media.Animation.IAnimatable> 인터페이스입니다.

- 사용 가능한 호환되는 애니메이션 형식이어야 합니다. (경우 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 제공 하지 않으면, 직접 만들 수 있습니다. 참조 된 [사용자 지정 애니메이션 개요](custom-animations-overview.md).)

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 갖는 많은 개체가 포함 <xref:System.Windows.Media.Animation.IAnimatable> 속성입니다. 와 같은 컨트롤 <xref:System.Windows.Controls.Button> 하 고 <xref:System.Windows.Controls.TabControl>, 그리고 <xref:System.Windows.Controls.Panel> 및 <xref:System.Windows.Shapes.Shape> 개체에서 상속 <xref:System.Windows.DependencyObject>합니다. 해당 속성 대부분은 종속성 속성입니다.

스타일 및 템플릿 컨트롤을 비롯한 거의 모든 위치에서 애니메이션을 사용할 수 있습니다. 애니메이션은 시각적일 필요가 없습니다. 이 섹션에 설명된 조건을 충족하지 않을 경우 사용자 인터페이스에 속하지 않는 개체에 애니메이션 효과를 줄 수 있습니다.

<a name="storyboardwalkthrough"></a>

## <a name="example-make-an-element-fade-in-and-out-of-view"></a>예제: 보기 내부 및 외부 요소 페이드 인

사용 하는 방법을 보여 주는이 예제는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 종속성 속성의 값에 애니메이션 효과를 애니메이션 합니다. 사용 하 여를 <xref:System.Windows.Media.Animation.DoubleAnimation>를 생성 하는 애니메이션의 형식인 <xref:System.Double> 값에 애니메이션 효과 주기를 <xref:System.Windows.UIElement.Opacity%2A> 의 속성을 <xref:System.Windows.Shapes.Rectangle>. 결과적으로 <xref:System.Windows.Shapes.Rectangle> 보기 내부 및 외부 사라집니다.

예제의 첫 번째 부분은 만듭니다는 <xref:System.Windows.Shapes.Rectangle> 요소입니다. 다음 단계는 애니메이션을 만들고 사각형의에 적용 하는 방법을 보여 줍니다 <xref:System.Windows.UIElement.Opacity%2A> 속성입니다.

다음 만드는 방법을 보여 줍니다.는 <xref:System.Windows.Shapes.Rectangle> 요소에는 <xref:System.Windows.Controls.StackPanel> XAML에서.

[!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_1)]

다음 만드는 방법을 보여 줍니다.는 <xref:System.Windows.Shapes.Rectangle> 요소에는 <xref:System.Windows.Controls.StackPanel> 코드에서입니다.

[!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_1)]
[!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_1)]

<a name="opacity_animation_step1"></a>

### <a name="part-1-create-a-doubleanimation"></a>1단계: DoubleAnimation 만들기

애니메이션 효과를 주는 페이드 보기 내부 및 외부 요소를 한 가지 방법은 해당 <xref:System.Windows.UIElement.Opacity%2A> 속성입니다. 때문에 합니다 <xref:System.Windows.UIElement.Opacity%2A> 형식의 속성이 <xref:System.Double>를 double 값을 생성 하는 애니메이션이 필요 합니다. <xref:System.Windows.Media.Animation.DoubleAnimation> 이러한 애니메이션 중 하나는 합니다. <xref:System.Windows.Media.Animation.DoubleAnimation> 두 개의 double 값 사이 전환을 만듭니다. 설정한 해당 시작 값을 지정 하려면 해당 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 속성입니다. 설정한 끝 값을 지정 하려면 해당 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 속성입니다.

1. 불투명도 값 `1.0` 완전히 불투명 개체와의 불투명도 값을 사용 하면 `0.0` 설정 하면 완전히 보이지 않습니다. 애니메이션 전환 하기로 `1.0` 에 `0.0` 설정한 해당 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 속성을 `1.0` 및 해당 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 속성을 `0.0`입니다. 다음 만드는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.DoubleAnimation> XAML에서.

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_2)]

    다음 만드는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.DoubleAnimation> 코드에서입니다.

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_2)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_2)]

2. 다음으로 지정 해야 합니다는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>합니다. <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 애니메이션의 시작 값에서 해당 대상 값으로 이동 하는 기간을 지정 합니다. 다음을 설정 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> XAML에서 5 초입니다.

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_3)]

    다음을 설정 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 코드에서 5 초입니다.

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_3)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_3)]

3. 이전 코드에서 전환 되는 애니메이션을 보여 주었습니다 `1.0` 에 `0.0`는으로 인해 대상 요소가 완전 불투명 상태에서 완전히 보이지 않는 페이드 인 합니다. 완전히 사라진 후 보기로 다시 페이드 인 요소를 설정 합니다 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 애니메이션의 속성 `true`합니다. 애니메이션 반복 무기한 설정를 해당 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 속성을 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>입니다. 다음을 설정 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 및 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> XAML의 속성입니다.

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_4](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_4)]

    다음을 설정 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 및 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 코드에서 속성입니다.

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_4](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_4)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_4)]

<a name="opacity_animation_step2"></a>

### <a name="part-2-create-a-storyboard"></a>2부: 스토리 보드 만들기

만든 개체에 애니메이션을 적용할를 <xref:System.Windows.Media.Animation.Storyboard> 사용 하 여는 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 및 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 개체를 지정 하는 속성 및 속성에 애니메이션 효과를 연결 합니다.

1. 만들기는 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션을 자식으로 추가 합니다. 다음 만드는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.Storyboard> XAML에서.

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_5](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_5)]

    만들려는 합니다 <xref:System.Windows.Media.Animation.Storyboard> 코드에서 선언를 <xref:System.Windows.Media.Animation.Storyboard> 클래스 수준 변수입니다.

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_100](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_100)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_100)]

    초기화는 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션을 자식으로 추가 합니다.

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_101](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_101)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_101)]

2. <xref:System.Windows.Media.Animation.Storyboard> 애니메이션 효과 적용할 위치를 알아야 합니다. 사용 된 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> 연결 된 속성을 개체에 애니메이션 효과를 지정 합니다. 다음의 대상 이름을 설정 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Media.Animation.DoubleAnimation> 에 `MyRectangle` XAML에서.

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_6](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_6)]

    다음의 대상 이름을 설정 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Media.Animation.DoubleAnimation> 에 `MyRectangle` 코드에서입니다.

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_102](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_102)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_102)]

3. 사용 된 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 연결 된 속성에 애니메이션 효과를 주는 속성을 지정 합니다. 다음 애니메이션을 구성 하는 방법을 보여 줍니다. 대상에는 <xref:System.Windows.UIElement.Opacity%2A> 의 속성을 <xref:System.Windows.Shapes.Rectangle> XAML에서.

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_7](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_7)]

    다음 애니메이션을 구성 하는 방법을 보여 줍니다. 대상에는 <xref:System.Windows.UIElement.Opacity%2A> 의 속성을 <xref:System.Windows.Shapes.Rectangle> 코드에서.

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_103](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_103)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_103)]

에 대 한 자세한 내용은 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 구문 및 추가 예제를 참조 하세요. 합니다 [Storyboard 개요](storyboards-overview.md)합니다.

<a name="opacity_animation_step3"></a>

### <a name="part-3-xaml-associate-the-storyboard-with-a-trigger"></a>(XAML) 3 부: 트리거를 사용 하 여 스토리 보드 연결

적용 하 고 시작 하는 가장 쉬운 방법은 <xref:System.Windows.Media.Animation.Storyboard> 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 이벤트 트리거를 사용 하는 것입니다. 이 섹션에 연결 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.Storyboard> XAML의 트리거를 사용 하 여 합니다.

1. 만들기는 <xref:System.Windows.Media.Animation.BeginStoryboard> 개체 및 스토리 보드를 연결 합니다. A <xref:System.Windows.Media.Animation.BeginStoryboard> 의 형식인 <xref:System.Windows.TriggerAction> 를 적용 하 고 시작을 <xref:System.Windows.Media.Animation.Storyboard>입니다.

    [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_3)]

2. 만들기는 <xref:System.Windows.EventTrigger> 추가한 합니다 <xref:System.Windows.Media.Animation.BeginStoryboard> 에 해당 <xref:System.Windows.EventTrigger.Actions%2A> 컬렉션입니다. 설정를 <xref:System.Windows.EventTrigger.RoutedEvent%2A> 의 속성을 <xref:System.Windows.EventTrigger> 시작 하려는 라우트된 이벤트에는 <xref:System.Windows.Media.Animation.Storyboard>합니다. (라우트된 이벤트에 대 한 자세한 내용은 참조는 [라우트된 이벤트 개요](../advanced/routed-events-overview.md).)

    [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_2)]

3. 추가 된 <xref:System.Windows.EventTrigger> 에 <xref:System.Windows.FrameworkElement.Triggers%2A> 사각형의 컬렉션입니다.

    [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_1)]

<a name="opacity_animation_step3code"></a>

### <a name="part-3-code-associate-the-storyboard-with-an-event-handler"></a>(코드) 3 부: 이벤트 처리기를 사용 하 여 스토리 보드 연결

적용 하 고 시작 하는 가장 쉬운 방법은 <xref:System.Windows.Media.Animation.Storyboard> 이벤트 처리기를 사용 하는 코드입니다. 이 섹션에 연결 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.Storyboard> 코드에서 이벤트 처리기를 사용 하 여 합니다.

1. 등록 된 <xref:System.Windows.FrameworkElement.Loaded> 사각형의 이벤트입니다.

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_104](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_104)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_104)]

2. 이벤트 처리기를 선언합니다. 이벤트 처리기에서 사용 된 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> storyboard를 적용 하는 방법입니다.

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_105](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_105)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_105](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_105)]

### <a name="complete-example"></a>완성된 예제

다음은 XAML에서 뷰 페이드 인 되는 사각형을 만드는 방법.

[!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml#rectangleopacityfadeexamplexaml)]

다음에서는 코드에서 보기로부터 페이드 인 및 페이드 아웃되는 사각형을 만드는 방법을 보여 줍니다.

[!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode)]
[!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode)]

<a name="animationtypes"></a>

## <a name="animation-types"></a>애니메이션 형식

애니메이션은 속성 값을 생성하므로 속성 형식마다 다양한 애니메이션 형식이 존재합니다. 사용 하는 속성에 애니메이션 효과 <xref:System.Double>와 같은 합니다 <xref:System.Windows.FrameworkElement.Width%2A> 요소의 속성을 생성 하는 애니메이션을 사용 <xref:System.Double> 값입니다. 사용 하는 속성에 애니메이션 효과 <xref:System.Windows.Point>를 생성 하는 애니메이션을 사용 하 여 <xref:System.Windows.Point> 값 및 등입니다. 다른 속성 유형의 수, 때문에 몇 가지 애니메이션 클래스가 <xref:System.Windows.Media.Animation> 네임 스페이스입니다. 다행스럽게도 쉬운 구분을 위해 엄격한 명명 규칙을 따릅니다.

- \<*형식*> 애니메이션

  "From/To/By" 또는 "basic" 애니메이션으로도 알려져 있는 이러한 클래스는 시작 값과 대상 값 사이에 애니메이션 효과를 주거나 시작 값에 오프셋 값을 추가하여 애니메이션 효과를 줍니다.

  - 시작 값을 지정하려면 애니메이션의 From 속성을 설정합니다.

  - 끝 값을 지정하려면 애니메이션의 To 속성을 설정합니다.

  - 오프셋 값을 지정하려면 애니메이션의 By 속성을 설정합니다.

  이러한 애니메이션이 가장 사용하기 쉬우므로 이 개요의 예제에서도 사용됩니다. From/To/By 애니메이션 From/To/By 애니메이션 개요에서 자세히 설명 되어 있습니다.

- \<*Type*>AnimationUsingKeyFrames

  키 프레임 애니메이션은 원하는 수의 대상 값을 지정하고 보간 방법을 제어할 수 있으므로 From/To/By 애니메이션보다 훨씬 더 강력합니다. 일부 형식은 키 프레임 애니메이션으로만 애니메이션 효과를 줄 수 있습니다. 키 프레임 애니메이션에 자세히 설명 합니다 [키 프레임 애니메이션 개요](key-frame-animations-overview.md)합니다.

- \<*Type*>AnimationUsingPath

  경로 애니메이션에서는 기하학적 경로를 사용하여 애니메이션 사용 값을 생성할 수 있습니다.

- \<*Type*>AnimationBase

  구현 하는 경우 애니메이션을 적용 하는 추상 클래스는 \< *형식*> 값입니다. 이 클래스에 대 한 기본 클래스로 사용 됩니다 \< *형식을*> 애니메이션 및 \< *형식*> AnimationUsingKeyFrames 클래스입니다. 사용자 고유의 사용자 지정 애니메이션을 만들려는 경우에만 이러한 클래스를 직접 처리해야 합니다. 그렇지 않은 경우 사용을 \< *형식*> 또는 KeyFrame\<*형식*> 애니메이션 합니다.

대부분의 경우에는 사용 하려는 합니다 \< *형식을*> 등의 애니메이션 클래스 <xref:System.Windows.Media.Animation.DoubleAnimation> 및 <xref:System.Windows.Media.Animation.ColorAnimation>합니다.

다음 표에서는 몇 가지 일반적인 애니메이션 형식 및 사용되는 일부 속성을 보여 줍니다.

|속성 형식|해당 basic(From/To/By) 애니메이션|해당 키 프레임 애니메이션|해당 경로 애니메이션|사용 예제|
|-------------------|----------------------------------------------------|---------------------------------------|----------------------------------|-------------------|
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>|없음|애니메이션을 적용 합니다 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 의 <xref:System.Windows.Media.SolidColorBrush> 또는 <xref:System.Windows.Media.GradientStop>합니다.|
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|애니메이션을 적용 합니다 <xref:System.Windows.FrameworkElement.Width%2A> 의 <xref:System.Windows.Controls.DockPanel> 또는 <xref:System.Windows.FrameworkElement.Height%2A> 의 <xref:System.Windows.Controls.Button>합니다.|
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|애니메이션을 적용 합니다 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 의 위치는 <xref:System.Windows.Media.EllipseGeometry>합니다.|
|<xref:System.String>|없음|<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>|없음|애니메이션을 적용 합니다 <xref:System.Windows.Controls.TextBlock.Text%2A> 의 <xref:System.Windows.Controls.TextBlock> 또는 <xref:System.Windows.Controls.ContentControl.Content%2A> 의 <xref:System.Windows.Controls.Button>합니다.|

<a name="animationsaretimelines"></a>

### <a name="animations-are-timelines"></a>애니메이션은 타임라인임

모든 애니메이션 형식은에서 상속 된 <xref:System.Windows.Media.Animation.Timeline> 클래스; 따라서 모든 애니메이션은 특수 한 유형의 타임 라인입니다. <xref:System.Windows.Media.Animation.Timeline> 시간의 세그먼트를 정의 합니다. 지정할 수 있습니다 합니다 *타이밍 동작* 타임 라인의: 해당 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>, 몇 번 반복 되며도 시간 진행 속도 대 한 것입니다.

애니메이션은을 <xref:System.Windows.Media.Animation.Timeline>, 시간 세그먼트를 나타냅니다. 애니메이션 출력 값을 계산 해당 지정된 시간 세그먼트를 통해 진행 되는 동안 (또는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>). 애니메이션은 진행되거나 "재생"되면서 연결된 속성을 업데이트합니다.

세 가지 자주 사용 되는 타이밍 속성은 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>하십시오 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>, 및 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>합니다.

#### <a name="the-duration-property"></a>Duration 속성

앞서 설명한 것처럼 타임라인은 시간 세그먼트를 나타냅니다. 해당 세그먼트의 길이에 의해 결정 됩니다는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 일반적으로 사용 하 여 지정 된 타임 라인을 <xref:System.Windows.Duration.TimeSpan%2A> 값입니다. 타임라인이 기간 끝에 도달하면 반복이 완료되는 것입니다.

애니메이션 사용 하 여 해당 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 속성 현재 값을 결정 하도록 합니다. 지정 하지 않으면 경우는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 값 기본값인 1 초가 애니메이션을 사용 합니다.

구문을의 단순화 된 버전을 보여 줍니다 합니다 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 특성에 대 한 구문을 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 속성입니다.

*hours* `:` *minutes* `:` *seconds*

다음 표에 몇 가지 나와 <xref:System.Windows.Duration> 설정과 해당 결과 값입니다.

|설정|결과 값|
|-------------|---------------------|
|0:0:5.5|5.5초|
|0:30:5.5|30분 5.5초|
|1:30:5.5|1시간 30분 5.5초|

지정 하는 한 가지 방법은 <xref:System.Windows.Duration> 코드에서 사용 하는 합니다 <xref:System.TimeSpan.FromSeconds%2A> 메서드를를 <xref:System.TimeSpan>, 새을 선언 <xref:System.Windows.Duration> 는 사용 하 여 구조체 <xref:System.TimeSpan>합니다.

에 대 한 자세한 내용은 <xref:System.Windows.Duration> 값 및 전체 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 구문을 참조는 <xref:System.Windows.Duration> 구조입니다.

#### <a name="autoreverse"></a>AutoReverse

합니다 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 속성의 끝에 도달한 후 타임 라인이 거꾸로 재생 여부를 지정 합니다. 해당 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>합니다. 이 애니메이션 속성을 설정 하는 경우 `true`, 끝에 도달한 후에 반전 해당 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>, 끝 값에서 시작 값으로 다시 재생 합니다. 이 속성은 기본적으로 `false`입니다.

#### <a name="repeatbehavior"></a>RepeatBehavior

<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 속성 타임 라인이 재생 되는 횟수를 지정 합니다. 기본적으로 타임 라인의 반복 횟수를는 `1.0`, 재생 되 고 전혀 반복 되지 않습니다.

이러한 속성 및 다른 사용자에 대 한 자세한 내용은 참조는 [타이밍 동작 개요](timing-behaviors-overview.md)합니다.

<a name="applyanimationstoproperty"></a>

## <a name="applying-an-animation-to-a-property"></a>속성에 애니메이션 적용

이전 섹션에서는 다양한 애니메이션 유형 및 타이밍 속성에 대해 설명합니다. 이 섹션에서는 애니메이션 효과를 주려는 속성에 애니메이션을 적용하는 방법을 보여 줍니다. <xref:System.Windows.Media.Animation.Storyboard> 개체 속성에 애니메이션을 적용 하는 방법을 제공 합니다. A <xref:System.Windows.Media.Animation.Storyboard> 되는 *컨테이너 타임 라인* 포함 된 애니메이션에 대 한 대상 지정 정보를 제공 하는 합니다.

### <a name="targeting-objects-and-properties"></a>개체 및 속성을 대상으로 지정

합니다 <xref:System.Windows.Media.Animation.Storyboard> 클래스를 제공 합니다 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 및 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 연결 된 속성입니다. 애니메이션에 이러한 속성을 설정하여 적용할 애니메이션을 지정합니다. 그러나 애니메이션이 개체를 대상으로 지정하려면 먼저 해당 개체에 이름을 지정해야 합니다.

에 이름을 할당 한 <xref:System.Windows.FrameworkElement> 에 이름을 할당에서 다른는 <xref:System.Windows.Freezable> 개체. 대부분의 컨트롤 및 패널은 프레임워크 요소입니다. 그러나 브러시, 변환, 기 하 도형 등의 순수한 그래픽 개체 대부분은 Freezable 개체입니다. 형식 인지 확실 하지 않은 경우는 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.Freezable>를 참조 합니다 **상속 계층 구조** 해당 참조 설명서의 섹션입니다.

- 확인 하는 <xref:System.Windows.FrameworkElement> 애니메이션 대상으로 사용자 이름을 설정 하 여 해당 <xref:System.Windows.FrameworkElement.Name%2A> 속성입니다. 코드에서 사용 해야는 <xref:System.Windows.FrameworkElement.RegisterName%2A> 속해 있는 페이지를 사용 하 여 요소 이름을 등록 하는 방법입니다.

- 있도록를 <xref:System.Windows.Freezable> 개체를 애니메이션 대상에 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], 사용할 합니다 [X:name 지시문](../../xaml-services/x-name-directive.md) 이름을 할당할 합니다. 코드에서 바로 사용을 <xref:System.Windows.FrameworkElement.RegisterName%2A> 속해 있는 페이지를 사용 하 여 개체를 등록 하는 방법입니다.

요소 이름 지정의 예제를 제공 하는 이어지는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 및 코드입니다. 이름 및 대상 지정에 대 한 자세한 내용은 참조는 [스토리 보드 개요](storyboards-overview.md)합니다.

### <a name="applying-and-starting-storyboards"></a>Storyboard 적용 및 시작

Storyboard를 시작 하려면 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]를 사용 하 여 연결을 <xref:System.Windows.EventTrigger>합니다. <xref:System.Windows.EventTrigger> 는 지정된 된 이벤트가 발생할 때 수행할 작업을 설명 하는 개체입니다. 수 이러한 동작 중 하나는 <xref:System.Windows.Media.Animation.BeginStoryboard> 스토리 보드를 시작 하는 데 사용할 수 있는 작업입니다. 이벤트 트리거는 애플리케이션이 특정 이벤트에 응답하는 방법을 지정할 수 있도록 하므로 개념적으로 이벤트 처리기와 비슷합니다. 이벤트 처리기 달리 이벤트 트리거에서 완벽 하 게 설명할 수 있는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]; 다른 코드가 필요 하지 않습니다.

시작 하는 <xref:System.Windows.Media.Animation.Storyboard> 코드에서 사용할 수 있습니다는 <xref:System.Windows.EventTrigger> 사용할지를 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드의 <xref:System.Windows.Media.Animation.Storyboard> 클래스.

<a name="controllingstoryboards"></a>

## <a name="interactively-control-a-storyboard"></a>대화식으로 Storyboard 제어

이전 예제에서는 시작 하는 방법을 보여 주었습니다.는 <xref:System.Windows.Media.Animation.Storyboard> 이벤트가 발생 합니다. 대화형으로 제어할 수 있습니다.는 <xref:System.Windows.Media.Animation.Storyboard> 시작 된 후: 일시 중지, 다시 시작, 중지, 채우기 기간으로 이동, 찾기 및 제거할 수는 <xref:System.Windows.Media.Animation.Storyboard>합니다. 자세한 내용 및 대화형으로 제어 하는 방법을 보여 주는 예제는 <xref:System.Windows.Media.Animation.Storyboard>, 참조는 [Storyboard 개요](storyboards-overview.md)합니다.

<a name="fillbehaviorsection"></a>

## <a name="what-happens-after-an-animation-ends"></a>애니메이션이 끝난 후에 발생하는 결과

<xref:System.Windows.Media.Animation.FillBehavior> 속성 종료 될 때 타임 라인의 동작을 지정 합니다. 기본적으로 타임 라인 시작 <xref:System.Windows.Media.Animation.ClockState.Filling> 종료 될 때입니다. 하는 애니메이션은 <xref:System.Windows.Media.Animation.ClockState.Filling> 최종 출력 값을 유지 합니다.

합니다 <xref:System.Windows.Media.Animation.DoubleAnimation> 앞의 예제에서 끝나지 때문에 해당 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 속성이 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>합니다. 다음 예제에서는 유사한 애니메이션을 사용하여 사각형에 애니메이션 효과를 줍니다. 이전 예와 달리 합니다 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 고 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 이 애니메이션의 속성은 기본값으로 남겨져 있습니다. 따라서 애니메이션은 5초 넘게 1에서 0으로 진행된 후 중지합니다.

[!code-xaml[animation_ovws_snippet#FillBehaviorExampleRectangleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/FillBehaviorExample.xaml#fillbehaviorexamplerectangleinline)]

[!code-csharp[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/FillBehaviorExample.cs#fillbehaviorexamplerectangleinline)]
[!code-vb[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/fillbehaviorexample.vb#fillbehaviorexamplerectangleinline)]

때문에 해당 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 는 해당 기본값에서 변경 되지 않았습니다 <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd>, 애니메이션이 종료 될 때 해당 최종 값인 0을 포함 합니다. 따라서는 <xref:System.Windows.UIElement.Opacity%2A> 애니메이션 후 0으로 사각형 유지의 종료 합니다. 설정 하는 경우는 <xref:System.Windows.UIElement.Opacity%2A> 사각형을 다른 값의 코드가 아무런 효과가 없으며, 애니메이션에 여전히 영향 때문에 <xref:System.Windows.UIElement.Opacity%2A> 속성입니다.

다시 코드에서 애니메이션된 속성을 제어 하는 방법을 사용 하는 것은 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 메서드 null을 지정 하는 <xref:System.Windows.Media.Animation.AnimationTimeline> 매개 변수입니다. 자세한 내용 및 예제를 참조 하세요 [속성 설정 후 애니메이션 스토리 보드를 사용 하 여](how-to-set-a-property-after-animating-it-with-a-storyboard.md)입니다.

에 속성 값을 설정 하는 없지만 <xref:System.Windows.Media.Animation.ClockState.Active> 또는 <xref:System.Windows.Media.Animation.ClockState.Filling> 애니메이션을 주지 않는 표시, 속성 값은 변경 합니다. 자세한 내용은 참조는 [애니메이션 및 타이밍 시스템 개요](animation-and-timing-system-overview.md)합니다.

<a name="databindingAndAnimatingAnimationsSection"></a>

## <a name="data-binding-and-animating-animations"></a>데이터 바인딩 및 애니메이션 효과 적용

대부분의 애니메이션 속성에 데이터 바인딩 또는 애니메이션; 수 합니다. 예를 들어 애니메이션을 적용할 수는 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 의 속성을 <xref:System.Windows.Media.Animation.DoubleAnimation>입니다. 그러나 타이밍 시스템이 작동하는 방식 때문에 데이터 바인딩 또는 애니메이션 효과 주기가 다른 데이터 바인딩 또는 애니메이션 개체와 다르게 동작합니다. 해당 동작을 이해하기 위해 속성에 애니메이션을 적용하는 것이 어떤 의미를 갖는지 이해하면 도움이 됩니다.

애니메이션 효과를 주는 방법을 보여 주는 이전 섹션에서 예제를 참조 하십시오는 <xref:System.Windows.UIElement.Opacity%2A> 사각형입니다. 이전 예제의 사각형이 로드 되 면 해당 이벤트 트리거가 적용 되는 <xref:System.Windows.Media.Animation.Storyboard>합니다. 타이밍 시스템의 복사본을 만듭니다는 <xref:System.Windows.Media.Animation.Storyboard> 및 애니메이션 합니다. 이러한 복사본은 고정 (읽기 전용 됨) 및 <xref:System.Windows.Media.Animation.Clock> 개체에서 생성 됩니다. 이러한 클록은 대상 속성에 애니메이션 효과를 주는 실제 작업을 수행합니다.

타이밍 시스템에 대 한 clock을 만듭니다는 <xref:System.Windows.Media.Animation.DoubleAnimation> 개체 및 지정 된 속성에 적용 하는 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 및 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 의 <xref:System.Windows.Media.Animation.DoubleAnimation>. 타이밍 시스템 시계를 적용 하는 경우에 <xref:System.Windows.UIElement.Opacity%2A> "MyRectangle." 라고 하는 개체의 속성

클록이 한도 생성 됩니다. 하지만 <xref:System.Windows.Media.Animation.Storyboard>, 시계 속성에 적용 되지 않습니다. 해당 자식 클록에 대해 만든 제어 하기 위한 것은 <xref:System.Windows.Media.Animation.DoubleAnimation>합니다.

애니메이션에 데이터 바인딩 또는 애니메이션 변경 내용을 반영하려면 해당 클록이 다시 생성되어야 합니다. 클록은 자동으로 다시 생성되지 않습니다. 변경 내용을 반영 하는 애니메이션을 만들려면 해당 스토리 보드를 사용 하 여 다시 적용을 <xref:System.Windows.Media.Animation.BeginStoryboard> 또는 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드. 이러한 메서드 중 하나를 사용하면 애니메이션이 다시 시작됩니다. 코드에서 사용할 수는 <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> 메서드 storyboard를 이전 위치로 돌아갑니다.

애니메이션을 바인딩된 데이터의 예제를 참조 하세요 [키 스플라인 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160011)합니다. 애니메이션 및 타이밍 시스템 작동 방식에 대 한 자세한 내용은 참조 하십시오 [애니메이션 및 타이밍 시스템 개요](animation-and-timing-system-overview.md)합니다.

<a name="otherWaysToAnimateSection"></a>

## <a name="other-ways-to-animate"></a>애니메이션 효과를 주는 다른 방법

이 개요의 예제에서는 Storyboard를 사용하여 애니메이션 효과를 주는 방법을 보여 줍니다. 코드를 사용하면 여러 가지 방법으로 애니메이션 효과를 줄 수 있습니다. 자세한 내용은 참조는 [속성 애니메이션 기술 개요](property-animation-techniques-overview.md)합니다.

<a name="animation_samples"></a>

## <a name="animation-samples"></a>애니메이션 샘플

다음 샘플은 애플리케이션에 애니메이션을 추가하는 데 도움이 될 수 있습니다.

- [From, To 및 By 애니메이션 대상 값 샘플](https://go.microsoft.com/fwlink/?LinkID=159988)

  다른 From/To/By 설정을 보여 줍니다.

- [애니메이션 타이밍 동작 샘플](https://go.microsoft.com/fwlink/?LinkID=159970)

  애니메이션의 타이밍 동작을 제어할 수는 여러 가지 방법을 보여 줍니다. 또한 이 샘플은 애니메이션의 대상 값에 대해 데이터 바인딩을 수행하는 방법을 보여 줍니다.

<a name="related_topics"></a>

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[애니메이션 및 타이밍 시스템 개요](animation-and-timing-system-overview.md)|타이밍 시스템을 사용 하는 방법에 대해 설명 합니다 <xref:System.Windows.Media.Animation.Timeline> 및 <xref:System.Windows.Media.Animation.Clock> 클래스가 애니메이션을 만들 수 있습니다.|
|[애니메이션에 대한 유용한 정보](animation-tips-and-tricks.md)|성능 같은 애니메이션 문제 해결에 도움이 되는 유용한 정보를 나열합니다.|
|[사용자 지정 애니메이션 개요](custom-animations-overview.md)|키 프레임, 애니메이션 클래스 또는 프레임당 콜백으로 애니메이션 시스템을 확장하는 방법을 설명합니다.|
|[From/To/By 애니메이션 개요](from-to-by-animations-overview.md)|두 값 사이를 전환하는 애니메이션을 만드는 방법을 설명합니다.|
|[키 프레임 애니메이션 개요](key-frame-animations-overview.md)|보간 방법을 제어하는 기능을 포함하여 여러 대상 값을 사용하여 애니메이션을 만드는 방법을 설명합니다.|
|[감속/가속 함수](easing-functions.md)|반송 같은 실질적인 동작을 얻기 위해 애니메이션에 수학 수식을 적용하는 방법을 설명합니다.|
|[경로 애니메이션 개요](path-animations-overview.md)|복잡한 경로를 따라 개체를 이동하거나 회전하는 방법을 설명합니다.|
|[속성 애니메이션 기술 개요](property-animation-techniques-overview.md)|Storyboard, 로컬 애니메이션, 시계 및 프레임당 애니메이션을 사용하는 속성 애니메이션에 대해 설명합니다.|
|[Storyboard 개요](storyboards-overview.md)|여러 개의 타임라인을 갖는 Storyboard를 사용하여 복잡한 애니메이션을 만드는 방법을 설명 합니다.|
|[타이밍 동작 개요](timing-behaviors-overview.md)|에 대해 설명 합니다 <xref:System.Windows.Media.Animation.Timeline> 형식 및 애니메이션에 사용 되는 속성입니다.|
|[타이밍 이벤트 개요](timing-events-overview.md)|사용할 수 있는 이벤트에 설명 합니다 <xref:System.Windows.Media.Animation.Timeline> 및 <xref:System.Windows.Media.Animation.Clock> 개체와 같은 타임 라인의 시점에서 코드를 실행 하는 것에 대 한 시작, 일시 중지, 다시 시작, 건너뛰기, 또는 중지 합니다.|
|[방법 항목](animation-and-timing-how-to-topics.md)|애플리케이션에서 애니메이션 및 타임라인을 사용하기 위한 코드 예제가 포함되어 있습니다.|
|[Clock 방법 항목](clocks-how-to-topics.md)|사용 하기 위한 코드 예제가 포함 된 <xref:System.Windows.Media.Animation.Clock> 응용 프로그램의 개체입니다.|
|[키 프레임 방법 항목](key-frame-animation-how-to-topics.md)|애플리케이션에서 키 프레임 애니메이션을 사용하기 위한 코드 예제가 포함되어 있습니다.|
|[경로 애니메이션 방법 항목](path-animation-how-to-topics.md)|애플리케이션에서 경로 애니메이션을 사용하기 위한 코드 예제가 포함되어 있습니다.|

<a name="reference"></a>

## <a name="reference"></a>참조

- <xref:System.Windows.Media.Animation.Timeline>

- <xref:System.Windows.Media.Animation.Storyboard>

- <xref:System.Windows.Media.Animation.BeginStoryboard>

- <xref:System.Windows.Media.Animation.Clock>
