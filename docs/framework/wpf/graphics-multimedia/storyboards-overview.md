---
title: Storyboard 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboard syntax [WPF]
- syntax [WPF], Storyboard
- timelines [WPF]
ms.assetid: 1a698c3c-30f1-4b30-ae56-57e8a39811bd
ms.openlocfilehash: 4d5a5ee3f1fcbd09fad9e25773d0e508209e1492
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855843"
---
# <a name="storyboards-overview"></a>Storyboard 개요

이 항목에서는 개체를 사용 <xref:System.Windows.Media.Animation.Storyboard> 하 여 애니메이션을 구성 하 고 적용 하는 방법을 보여 줍니다. 개체를 대화형으로 조작 <xref:System.Windows.Media.Animation.Storyboard> 하 고 간접 속성 대상 지정 구문을 설명 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>전제 조건

이 항목을 이해하려면 다양한 애니메이션 형식과 해당 기본 기능에 대해 잘 알고 있어야 합니다. 애니메이션 소개를 보려면 [애니메이션 개요](animation-overview.md)를 참조하세요. 또한 연결된 속성을 사용하는 방법을 알아야 합니다. 연결된 속성에 대한 자세한 내용은 [연결된 속성 개요](../advanced/attached-properties-overview.md)를 참조하세요.

<a name="whatisatimeline"></a>

## <a name="what-is-a-storyboard"></a>Storyboard란?

애니메이션만이 타임라인의 유용한 형식은 아닙니다. 타임라인의 집합을 구성하고 속성에 타임라인을 적용하는 데 도움이 되는 다른 타임라인 클래스도 제공됩니다. 컨테이너 타임 라인은 <xref:System.Windows.Media.Animation.TimelineGroup> 클래스에서 파생 되며 및 <xref:System.Windows.Media.Animation.ParallelTimeline> <xref:System.Windows.Media.Animation.Storyboard>를 포함 합니다.

는 <xref:System.Windows.Media.Animation.Storyboard> 포함 된 타임 라인에 대 한 대상 정보를 제공 하는 컨테이너 타임 라인의 유형입니다. 스토리 보드에는 다른 컨테이너 타임 <xref:System.Windows.Media.Animation.Timeline>라인 및 애니메이션을 비롯 한 모든 유형이 포함 될 수 있습니다. <xref:System.Windows.Media.Animation.Storyboard>개체를 사용 하면 다양 한 개체와 속성에 영향을 주는 타임 라인을 단일 타임 라인 트리에 결합 하 여 복잡 한 타이밍 동작을 쉽게 구성 하 고 제어할 수 있습니다. 예를 들어 다음 세 가지 작업을 수행하는 단추가 필요하다고 가정해 봅니다.

- 단추를 선택하면 단추가 커지고 색이 변경됩니다.

- 클릭할 때 축소되었다가 다시 원래 크기로 커집니다.

- 사용되지 않도록 설정되면 축소되었다가 50% 불투명도로 페이드됩니다.

이 경우 동일한 개체에 적용되는 여러 애니메이션 집합이 있고 단추 상태에 따라 다른 시간에 재생하려고 합니다. <xref:System.Windows.Media.Animation.Storyboard>개체를 사용 하 여 애니메이션을 구성 하 고 그룹에서 하나 이상의 개체에 적용할 수 있습니다.

<a name="wherecanyouuseastoryboard"></a>

## <a name="where-can-you-use-a-storyboard"></a>Storyboard를 사용할 수 있는 위치

는 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션 효과 클래스의 종속성 속성에 애니메이션 효과를 주는 데 사용할 수 있습니다. 클래스를 애니메이션 효과 하는 방법에 대 한 자세한 내용은 [애니메이션 개요](animation-overview.md)를 참조 하세요. 그러나 스토리 보 딩은 프레임 워크 수준 기능 이므로 개체는 <xref:System.Windows.NameScope> <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement>의에 속해야 합니다.

예를 들어를 사용 <xref:System.Windows.Media.Animation.Storyboard> 하 여 다음을 수행할 수 있습니다.

- 단추 ( <xref:System.Windows.Media.SolidColorBrush> 의 <xref:System.Windows.FrameworkElement>형식)의 배경을 칠하는 (프레임 워크가 아닌 요소)에 애니메이션 효과를 적용 합니다.

- (<xref:System.Windows.FrameworkElement>) <xref:System.Windows.Media.SolidColorBrush> 를 사용 하 여 <xref:System.Windows.Controls.Image> 표시 되는 (프레임 워크가 아닌 요소 <xref:System.Windows.Media.GeometryDrawing> )의 채우기를 칠하는 (프레임 워크가 아닌 요소)에 애니메이션 효과를 적용 합니다.

- 코드에서를 <xref:System.Windows.FrameworkElement>포함 하 <xref:System.Windows.Media.SolidColorBrush> 는 클래스에 의해 선언 된에 애니메이션을 적용 합니다 <xref:System.Windows.Media.SolidColorBrush> <xref:System.Windows.FrameworkElement>. 해당 이름이로 등록 된 경우에도이를 포함 합니다.

그러나를 사용 <xref:System.Windows.Media.Animation.Storyboard> 하 여 <xref:System.Windows.FrameworkElement> 이름을 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement>로 등록 하지 <xref:System.Windows.Media.SolidColorBrush> 않았거나 또는 <xref:System.Windows.FrameworkContentElement>의 속성을 설정 하는 데 사용 되지 않은에 애니메이션 효과를 적용할 수 없습니다.

<a name="applyanimationswithastoryboard"></a>

## <a name="how-to-apply-animations-with-a-storyboard"></a>Storyboard를 사용하여 애니메이션을 적용하는 방법

를 사용 <xref:System.Windows.Media.Animation.Storyboard> 하 여 애니메이션을 구성 하 고 적용 하려면 애니메이션을 <xref:System.Windows.Media.Animation.Storyboard>의 자식 타임 라인으로 추가 합니다. 클래스 <xref:System.Windows.Media.Animation.Storyboard> 는 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> 및 연결된속성을제공합니다.<xref:System.Windows.Media.Animation.Storyboard.TargetProperty?displayProperty=nameWithType> 애니메이션에 이러한 속성을 설정하여 해당 대상 개체 및 속성을 지정합니다.

애니메이션을 대상에 적용 하려면 트리거 동작이 나 메서드 <xref:System.Windows.Media.Animation.Storyboard> 를 사용 하 여를 시작 합니다. 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] <xref:System.Windows.EventTrigger>, <xref:System.Windows.Media.Animation.BeginStoryboard> 또는 와<xref:System.Windows.DataTrigger>함께 개체를사용합니다<xref:System.Windows.Trigger>. 코드에서 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드를 사용할 수도 있습니다.

다음 표에서는 각 <xref:System.Windows.Media.Animation.Storyboard> begin 기술이 지원 되는 다양 한 위치, 즉 인스턴스별, 스타일, 컨트롤 템플릿 및 데이터 템플릿을 보여 줍니다. "인스턴스별"은 스타일, 컨트롤 템플릿 또는 데이터 템플릿이 아닌 개체의 인스턴스에 직접 애니메이션 또는 storyboard를 적용하는 기술을 나타냅니다.

|storyboard 시작 방법...|인스턴스별|스타일|컨트롤 템플릿|데이터 템플릿|예제|
|--------------------------------|-------------------|-----------|----------------------|-------------------|-------------|
|<xref:System.Windows.Media.Animation.BeginStoryboard>및<xref:System.Windows.EventTrigger>|예|예|예|예|[Storyboard를 사용하여 속성에 애니메이션 효과 주기](how-to-animate-a-property-by-using-a-storyboard.md)|
|<xref:System.Windows.Media.Animation.BeginStoryboard>및 속성<xref:System.Windows.Trigger>|아니요|예|예|예|[속성 값이 변경될 때 애니메이션 트리거](how-to-trigger-an-animation-when-a-property-value-changes.md)|
|<xref:System.Windows.Media.Animation.BeginStoryboard>및<xref:System.Windows.DataTrigger>|아니요|예|예|예|[방법: 데이터가 변경 될 때 애니메이션 트리거](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/aa970679(v=vs.90))|
|<xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드|예|아니오|아니요|아니요|[Storyboard를 사용하여 속성에 애니메이션 효과 주기](how-to-animate-a-property-by-using-a-storyboard.md)|

다음 예제에서는를 <xref:System.Windows.Media.Animation.Storyboard> 사용 하 여 <xref:System.Windows.Shapes.Rectangle> 요소의 <xref:System.Windows.FrameworkElement.Width%2A> <xref:System.Windows.Media.SolidColorBrush.Color%2A> 에 애니메이션 효과를 주는 <xref:System.Windows.Media.SolidColorBrush> <xref:System.Windows.Shapes.Rectangle>데 사용 되는의를 그립니다.

[!code-xaml[storyboards_ovw_snip_XAML#1](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#1)]

[!code-csharp[storyboards_ovw_snip#100](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#100)]

다음 섹션에서는 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 및 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 연결 된 속성에 대해 자세히 설명 합니다.

<a name="targetingelementsandfreezables"></a>

## <a name="targeting-framework-elements-framework-content-elements-and-freezables"></a>프레임워크 요소, 프레임워크 콘텐츠 요소 및 Freezable을 대상으로 지정

이전 섹션에서는 애니메이션이 대상을 찾기 위해서는 대상의 이름 및 애니메이션 효과를 주려는 속성을 알고 있어야 한다는 사실을 언급했습니다. 애니메이션 효과를 적용할 속성을 지정 하는 것은 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty?displayProperty=nameWithType> 바로 애니메이션 효과가 적용 되는 속성의 이름으로 설정 하면 됩니다.  애니메이션에 속성을 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> 설정 하 여 애니메이션 효과를 적용할 속성을 가진 개체의 이름을 지정 합니다.

<xref:System.Windows.Setter.TargetName%2A> 속성이 작동 하려면 대상 개체에 이름이 있어야 합니다. 이름을 <xref:System.Windows.FrameworkElement> 또는[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 에 할당 하<xref:System.Windows.Freezable> 는 것은 개체에 이름을 할당 하는 것과 다릅니다. <xref:System.Windows.FrameworkContentElement>

프레임 워크 요소는 <xref:System.Windows.FrameworkElement> 클래스에서 상속 되는 클래스입니다. 프레임 <xref:System.Windows.Window>워크 요소의 <xref:System.Windows.Controls.DockPanel> <xref:System.Windows.Shapes.Rectangle>예로는,, 및가 있습니다. <xref:System.Windows.Controls.Button> 기본적으로 모든 창, 패널 및 컨트롤은 요소입니다. 프레임 워크 콘텐츠 요소는 <xref:System.Windows.FrameworkContentElement> 클래스에서 상속 되는 클래스입니다. 프레임 워크 콘텐츠 요소의 <xref:System.Windows.Documents.FlowDocument> 예로는 및 <xref:System.Windows.Documents.Paragraph>가 있습니다. 형식이 프레임워크 요소인지 또는 프레임워크 콘텐츠 요소인지 확실하지 않은 경우 Name 속성을 가지는지 여부를 확인합니다. 이 속성을 가질 경우 프레임워크 요소이거나 프레임워크 콘텐츠 요소일 것입니다. 확실히 하려면 해당 형식 페이지의 상속 계층 구조 섹션을 확인합니다.

에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]프레임 워크 요소나 프레임 워크 콘텐츠 요소를 대상으로 지정할 수 있도록 설정 하려면 해당 <xref:System.Windows.FrameworkElement.Name%2A> 속성을 설정 합니다. 또한 코드에서 <xref:System.Windows.NameScope.RegisterName%2A> 메서드를 사용 하 여를 <xref:System.Windows.NameScope>만든 요소에 요소 이름을 등록 해야 합니다.

앞의 예제에서 가져온 다음 예제는 이름 `MyRectangle` a <xref:System.Windows.Shapes.Rectangle>를 <xref:System.Windows.FrameworkElement>할당 합니다.

[!code-xaml[storyboards_ovw_snip_XAML#2](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#2)]

[!code-csharp[storyboards_ovw_snip#102](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#102)]

이름이 지정되면 해당 요소의 속성에 애니메이션 효과를 줄 수 있습니다.

[!code-xaml[storyboards_ovw_snip_XAML#5](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#5)]

[!code-csharp[storyboards_ovw_snip#105](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#105)]

<xref:System.Windows.Freezable>형식은 <xref:System.Windows.Freezable> 클래스에서 상속 되는 클래스입니다. 예를 들면 ,<xref:System.Windows.Media.RotateTransform> 및<xref:System.Windows.Media.GradientStop>가있습니다. <xref:System.Windows.Freezable> <xref:System.Windows.Media.SolidColorBrush>

<xref:System.Windows.Freezable> 에서[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]애니메이션을 통해를 대상으로 하도록 설정 하려면 [x:Name 지시문](../../xaml-services/x-name-directive.md) 을 사용 하 여 이름을 할당 합니다. 코드에서는 <xref:System.Windows.NameScope.RegisterName%2A> 메서드를 사용 하 여를 <xref:System.Windows.NameScope>만든 요소에 해당 이름을 등록 합니다.

다음 예에서는 <xref:System.Windows.Freezable> 개체에 이름을 할당 합니다.

[!code-xaml[storyboards_ovw_snip_XAML#3](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#3)]

[!code-csharp[storyboards_ovw_snip#103](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#103)]

그런 후 개체를 애니메이션 대상으로 지정할 수 있습니다.

[!code-xaml[storyboards_ovw_snip_XAML#7](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#7)]

[!code-csharp[storyboards_ovw_snip#107](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#107)]

<xref:System.Windows.Media.Animation.Storyboard>개체는 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 이름 범위를 사용 하 여 속성을 확인 합니다. WPF 이름 범위에 대한 자세한 내용은 [WPF XAML 이름 범위](../advanced/wpf-xaml-namescopes.md)를 참조하세요. <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 속성이 생략 된 경우 애니메이션은 해당 속성이 정의 된 요소를 대상으로 하거나 스타일의 경우 스타일이 지정 된 요소를 대상으로 지정 합니다.

경우에 따라 <xref:System.Windows.Freezable> 개체에 이름을 할당할 수 없습니다. 예를 들어, <xref:System.Windows.Freezable> 이 리소스로 선언 되거나 속성 값을 스타일로 설정 하는 데 사용 되는 경우에는 이름을 지정할 수 없습니다. 이름이 없기 때문에 직접적으로 대상으로 지정할 수 없지만 간접적으로 지정할 수는 있습니다. 다음 섹션에서는 간접 대상 지정을 사용하는 방법을 설명합니다.

<a name="pathsyntaxforchangeable"></a>

## <a name="indirect-targeting"></a>간접 대상 지정

가 리소스로 선언 되거나 <xref:System.Windows.Freezable> 스타일에서 속성 값을 설정 하는 데 사용 되는 경우와 같이 애니메이션에서 직접 대상을 지정할 수 없는 경우가 있습니다. <xref:System.Windows.Freezable> 이러한 경우 직접 대상으로 지정할 수 없지만 개체에 <xref:System.Windows.Freezable> 도 애니메이션 효과를 적용할 수 있습니다. 속성을 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 의 이름 <xref:System.Windows.Freezable>으로 설정 하는 대신 <xref:System.Windows.Freezable> "속해 있는" 요소의 이름을 지정 합니다. 예를 들어 사각형 <xref:System.Windows.Media.SolidColorBrush> 요소의를 <xref:System.Windows.Shapes.Shape.Fill%2A> 설정 하는 데 사용 되는은 해당 사각형에 속합니다. 브러시에 애니메이션 효과를 주려면 애니메이션의 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 속성을 <xref:System.Windows.Freezable> 설정 하 고 종료 하는 데 사용 된 프레임 워크 요소 또는 프레임 워크 콘텐츠 <xref:System.Windows.Freezable> 요소의 속성에서 시작 하는 속성 체인으로 애니메이션을 설정 합니다.

[!code-xaml[storyboards_ovw_snip_XAML#33](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#33)]

[!code-csharp[storyboards_ovw_snip#134](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#134)]

<xref:System.Windows.Freezable> 이 고정 되 면 복제본이 생성 되 고 복제에 애니메이션 효과가 적용 됩니다. 이 경우 원래 개체에 실제로 애니메이션이 적용 <xref:System.Windows.Media.Animation.Animatable.HasAnimatedProperties%2A> 되지 않기 때문에 `false`원래 개체의 속성은을 계속 반환 합니다. 복제에 대 한 자세한 내용은 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)를 참조 하세요.

또한 간접 속성 대상 지정을 사용할 경우에는 존재하지 않는 개체를 대상으로 지정할 수 있습니다. 예를 들어, 실제로 <xref:System.Windows.Controls.Control.Background%2A> <xref:System.Windows.Media.LinearGradientBrush> 가 단추의 배경을 설정 하는 데 사용 된 경우 특정 <xref:System.Windows.Media.SolidColorBrush> 단추의가로 설정 되 고 색에 애니메이션을 적용 하는 경우를 가정 합니다. 이 경우 예외가 throw 되지 않습니다. 가 <xref:System.Windows.Media.LinearGradientBrush> <xref:System.Windows.Media.SolidColorBrush.Color%2A> 속성 변경 내용에 반응 하지 않으므로 애니메이션이 표시 되지 않습니다.

다음 섹션에서는 간접 속성 대상 지정 구문을 좀 더 자세히 설명합니다.

<a name="xamlsyntaxchangeableproperty"></a>

### <a name="indirectly-targeting-a-property-of-a-freezable-in-xaml"></a>XAML에서 Freezable 속성을 간접적으로 대상으로 지정

에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]freezable의 속성을 대상으로 하려면 다음 구문을 사용 합니다.

| |
|-|
|*ElementPropertyName* `.` *FreezablePropertyName*|

Where

- *Elementpropertyname* 은를 설정 하는 <xref:System.Windows.FrameworkElement> 데 사용 <xref:System.Windows.Freezable> 되는의 속성입니다.

- *FreezablePropertyName* 은 애니메이션 효과 <xref:System.Windows.Freezable> 를 적용할의 속성입니다.

다음 코드에서는 사각형 요소의를 <xref:System.Windows.Media.SolidColorBrush.Color%2A> <xref:System.Windows.Shapes.Shape.Fill%2A> 설정 하는 <xref:System.Windows.Media.SolidColorBrush> 데 사용 되는의에 애니메이션 효과를 주는 방법을 보여 줍니다.

[!code-xaml[storyboards_ovw_snip_XAML#32](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#32)]

컬렉션 또는 배열에 포함된 Freezable을 대상으로 지정해야 하는 경우도 있습니다.

컬렉션에 포함된 Freezable을 대상으로 지정하려면 다음 경로 구문을 사용합니다.

| |
|-|
|*ElementPropertyName* `.Children[` *CollectionIndex* `].` *FreezablePropertyName*|

여기서 *Collectionindex* 는 배열 또는 컬렉션에 있는 개체의 인덱스입니다.

예를 들어 사각형 <xref:System.Windows.Media.TransformGroup> 에 해당 <xref:System.Windows.UIElement.RenderTransform%2A> 속성에 적용 된 리소스가 있고 포함 된 변환 중 하나에 애니메이션 효과를 적용 하려는 경우를 가정 합니다.

[!code-xaml[storyboards_ovw_snip_XAML#34](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#34)]

다음 코드에서는 앞의 예제에 <xref:System.Windows.Media.RotateTransform.Angle%2A> <xref:System.Windows.Media.RotateTransform> 표시 된의 속성에 애니메이션 효과를 주는 방법을 보여 줍니다.

[!code-xaml[storyboards_ovw_snip_XAML#35](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#35)]

<a name="targetingpropertyofchangeableincode"></a>

### <a name="indirectly-targeting-a-property-of-a-freezable-in-code"></a>코드에서 Freezable 속성을 간접적으로 대상으로 지정

코드에서 <xref:System.Windows.PropertyPath> 개체를 만듭니다. 를 만들 <xref:System.Windows.PropertyPath>때 <xref:System.Windows.PropertyPath.Path%2A> 및 <xref:System.Windows.PropertyPath.PathParameters%2A>를 지정 합니다.

을 만들려면 <xref:System.Windows.PropertyPath.PathParameters%2A>종속성 속성 식별자 필드의 목록이 포함 <xref:System.Windows.DependencyProperty> 된 형식의 배열을 만듭니다. 첫 번째 식별자 필드는의 속성 <xref:System.Windows.FrameworkElement> 에 대 한 것 이거나 <xref:System.Windows.FrameworkContentElement> 를 <xref:System.Windows.Freezable> 설정 하는 데 사용 되는입니다. 다음 식별자 필드는 대상 <xref:System.Windows.Freezable> 으로 할의 속성을 나타냅니다. 를 <xref:System.Windows.Freezable> 개체<xref:System.Windows.FrameworkElement> 에 연결 하는 속성 체인으로 생각 하면 됩니다.

다음은 사각형 요소의를 <xref:System.Windows.Media.SolidColorBrush.Color%2A> <xref:System.Windows.Shapes.Shape.Fill%2A> 설정 하는 <xref:System.Windows.Media.SolidColorBrush> 데 사용 되는의를 대상으로 하는 종속성 속성 체인의 예입니다.

[!code-csharp[storyboards_ovw_snip#135](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#135)]

또한를 지정 <xref:System.Windows.PropertyPath.Path%2A>해야 합니다. 는 <xref:System.Windows.PropertyPath.Path%2A>를 해석 <xref:System.Windows.PropertyPath.Path%2A> 하는방법을설명하는입니다.<xref:System.Windows.PropertyPath.PathParameters%2A> <xref:System.String> 여기서는 다음 구문을 사용합니다.

| |
|-|
|`(` *OwnerPropertyArrayIndex* `).(` *FreezablePropertyArrayIndex* `)`|

Where

- *OwnerPropertyArrayIndex* 는를 설정 하는 <xref:System.Windows.DependencyProperty> 데 사용 되는 <xref:System.Windows.FrameworkElement> <xref:System.Windows.Freezable> 개체의 속성 식별자를 포함 하는 배열의 인덱스입니다.

- *FreezablePropertyArrayIndex* 은 대상으로 할 속성 <xref:System.Windows.DependencyProperty> 의 식별자를 포함 하는 배열의 인덱스입니다.

다음 예제에서는 앞의 <xref:System.Windows.PropertyPath.Path%2A> 예제에서 정의 된 <xref:System.Windows.PropertyPath.PathParameters%2A> 와 함께 제공 되는을 보여 줍니다.

[!code-csharp[storyboards_ovw_snip#PropertyChainAndPath](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#propertychainandpath)]

다음 예제에서는 이전 예제의 코드를 결합 하 여 사각형 요소의를 <xref:System.Windows.Media.SolidColorBrush.Color%2A> <xref:System.Windows.Shapes.Shape.Fill%2A> 설정 하 <xref:System.Windows.Media.SolidColorBrush> 는 데 사용 되는의에 애니메이션 효과를 줍니다.

[!code-csharp[storyboards_ovw_snip#137](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#137)]

컬렉션 또는 배열에 포함된 Freezable을 대상으로 지정해야 하는 경우도 있습니다. 예를 들어 사각형 <xref:System.Windows.Media.TransformGroup> 에 해당 <xref:System.Windows.UIElement.RenderTransform%2A> 속성에 적용 된 리소스가 있고 포함 된 변환 중 하나에 애니메이션 효과를 적용 하려는 경우를 가정 합니다.

[!code-xaml[storyboards_ovw_snip#142](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml#142)]

컬렉션에 포함 <xref:System.Windows.Freezable> 된를 대상으로 하려면 다음 경로 구문을 사용 합니다.

| |
|-|
|`(` *OwnerPropertyArrayIndex* `).(` *CollectionChildrenPropertyArrayIndex* `)` `[` *CollectionIndex* `].(` *FreezablePropertyArrayIndex* `)`|

여기서 *Collectionindex* 는 배열 또는 컬렉션에 있는 개체의 인덱스입니다.

<xref:System.Windows.Media.RotateTransform.Angle%2A> 에서 <xref:System.Windows.Media.RotateTransform> <xref:System.Windows.PropertyPath.PathParameters%2A>두 번째 변환의 속성을 대상으로 하려면 다음 <xref:System.Windows.PropertyPath.Path%2A> 및를 사용 합니다. <xref:System.Windows.Media.TransformGroup>

[!code-csharp[storyboards_ovw_snip#139](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#139)]

다음 예제에서는 내 <xref:System.Windows.Media.RotateTransform.Angle%2A> <xref:System.Windows.Media.RotateTransform> 에 포함 된의에 애니메이션 효과를 주는 전체 코드를 보여 줍니다. <xref:System.Windows.Media.TransformGroup>

[!code-csharp[storyboards_ovw_snip#138](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#138)]

### <a name="indirectly-targeting-with-a-freezable-as-the-starting-point"></a>Freezable을 시작 지점으로 사용해서 간접적으로 대상 지정

이전 <xref:System.Windows.Freezable> 섹션에서는 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement> 를 시작 하 고 <xref:System.Windows.Freezable> 하위 속성에 대 한 속성 체인을 만들어를 간접적으로 대상으로 하는 방법에 대해 설명 했습니다. 또한를 <xref:System.Windows.Freezable> 시작 점으로 사용 하 고 해당 <xref:System.Windows.Freezable> 하위 속성 중 하나를 간접적으로 대상으로 지정할 수 있습니다. 를 <xref:System.Windows.Freezable> 간접 대상 지정의 시작 점으로 사용 하는 경우 한 가지 추가 제한 사항이 적용 <xref:System.Windows.Freezable> 됩니다. <xref:System.Windows.Freezable> 즉, 시작 및 그 사이의 모든 및 간접적으로 대상이 지정 된 하위 속성은 고정 되지 않아야 합니다.

<a name="controllable_storyboards"></a>

## <a name="interactively-controlling-a-storyboard-in-xaml"></a>XAML에서 Storyboard를 대화형으로 제어

에서 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]storyboard를 시작 하려면 <xref:System.Windows.Media.Animation.BeginStoryboard> 트리거 동작을 사용 합니다. <xref:System.Windows.Media.Animation.BeginStoryboard>애니메이션을 적용 하는 개체 및 속성에 애니메이션을 배포 하 고 스토리 보드를 시작 합니다. 이 프로세스에 대 한 자세한 내용은 [애니메이션 및 타이밍 시스템 개요](animation-and-timing-system-overview.md)를 참조 하세요. 속성을<xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> 지정 하 여 이름을 지정 하면 제어 가능한 storyboard로 설정 됩니다. <xref:System.Windows.Media.Animation.BeginStoryboard> 그러면 Storyboard를 시작한 후에 대화형으로 제어할 수 있습니다. 다음은 Storyboard를 제어하기 위해 이벤트 트리거와 함께 사용하는 제어 가능한 Storyboard 작업 목록입니다.

- <xref:System.Windows.Media.Animation.PauseStoryboard>: 스토리 보드를 일시 중지 합니다.

- <xref:System.Windows.Media.Animation.ResumeStoryboard>: 일시 중지 된 스토리 보드를 다시 시작 합니다.

- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>: 스토리 보드의 속도를 변경 합니다.

- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>: 스토리 보드가 있는 경우 해당 채우기 기간의 끝까지 storyboard를 이동 합니다.

- <xref:System.Windows.Media.Animation.StopStoryboard>: 스토리 보드를 중지 합니다.

- <xref:System.Windows.Media.Animation.RemoveStoryboard>: 스토리 보드를 제거 합니다.

다음 예제에서는 제어 가능한 Storyboard 작업이 Storyboard를 대화형으로 제어하는 데 사용됩니다.

[!code-xaml[animation_ovws_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snip/CS/ControllableStoryboardExample.xaml#controllablestoryboardexamplewholepage)]

<a name="controllable_storyboards_procedural"></a>

## <a name="interactively-controlling-a-storyboard-by-using-code"></a>코드를 사용하여 Storyboard를 대화형으로 제어

앞의 예제에서는 트리거 작업을 사용해서 애니메이션 효과를 적용하는 방법을 살펴보았습니다. 코드에서 <xref:System.Windows.Media.Animation.Storyboard> 클래스의 대화형 메서드를 사용 하 여 스토리 보드를 제어할 수도 있습니다. 코드에서 <xref:System.Windows.Media.Animation.Storyboard> 대화형으로 만들려면 storyboard의 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드에 적절 한 오버 로드를 사용 하 고를 제어 하 여 제어 가능 `true` 하도록 지정 해야 합니다. 참조 된 <xref:System.Windows.Media.Animation.Storyboard.Begin%28System.Windows.FrameworkElement%2CSystem.Boolean%29> 자세한 페이지입니다.

다음 목록에서는가 시작 된 후를 <xref:System.Windows.Media.Animation.Storyboard> 조작 하는 데 사용할 수 있는 메서드를 보여 줍니다.

- <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>

- <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Remove%2A>

이러한 메서드를 사용 하는 경우의 이점은 또는 <xref:System.Windows.Trigger> <xref:System.Windows.TriggerAction> 개체를 만들 필요가 없다는 것입니다. 조작 하려는 제어 <xref:System.Windows.Media.Animation.Storyboard> 대상에 대 한 참조만 있으면 됩니다.

> [!NOTE]
> 에서 수행 <xref:System.Windows.Media.Animation.Clock> <xref:System.Windows.Media.Animation.Storyboard> 되는 모든 대화형 작업은 다음 렌더링 직전에 발생 하는 타이밍 엔진의 다음 틱에서 발생 합니다. 예를 들어 <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> 메서드를 사용 하 여 애니메이션의 다른 위치로 이동 하는 경우 속성 값이 즉시 변경 되지 않고 타이밍 엔진의 다음 틱에서 값이 변경 됩니다.

다음 예제에서는 <xref:System.Windows.Media.Animation.Storyboard> 클래스의 대화형 메서드를 사용 하 여 애니메이션을 적용 하 고 제어 하는 방법을 보여 줍니다.

[!code-csharp[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/ControllableStoryboardExample.cs#controllablestoryboardexamplewholepage)]
[!code-vb[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/controllablestoryboardexample.vb#controllablestoryboardexamplewholepage)]

<a name="usingstoryboardsinstyles"></a>

## <a name="animate-in-a-style"></a>스타일에서 애니메이션 효과 주기

개체를 사용 <xref:System.Windows.Media.Animation.Storyboard> 하 여 <xref:System.Windows.Style>에서 애니메이션을 정의할 수 있습니다. 에서를 사용 하 여 애니메이션을 적용 하 <xref:System.Windows.Media.Animation.Storyboard> 는것은다른위치를사용하는것과비슷하지만다음과같은세가지예외가있습니다.<xref:System.Windows.Style> <xref:System.Windows.Media.Animation.Storyboard>

- 는 지정 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>하지 않습니다 .는 <xref:System.Windows.Media.Animation.Storyboard> 항상 <xref:System.Windows.Style> 이 적용 되는 요소를 대상으로 합니다. 개체를 <xref:System.Windows.Freezable> 대상으로 지정 하려면 간접 대상 지정을 사용 해야 합니다. 간접 대상 지정에 대 한 자세한 내용은 [간접 대상 지정](#pathsyntaxforchangeable) 섹션을 참조 하세요.

- 또는 에대해<xref:System.Windows.EventTrigger.SourceName%2A> 를 지정할 수 없습니다. <xref:System.Windows.Trigger> <xref:System.Windows.EventTrigger>

- 동적 리소스 참조 또는 데이터 바인딩 식을 사용 하 여 또는 애니메이션 <xref:System.Windows.Media.Animation.Storyboard> 속성 값을 설정할 수 없습니다. 내부의 <xref:System.Windows.Style> 모든 항목은 스레드로부터 안전 해야 하며 타이밍 <xref:System.Windows.Freezable.Freeze%2A> <xref:System.Windows.Media.Animation.Storyboard> 시스템은 개체를 스레드로부터 안전 하 게 만들어야 합니다. 에 <xref:System.Windows.Media.Animation.Storyboard> 동적 리소스 참조 또는 데이터 바인딩 식이 포함 된 경우에는를 고정할 수 없습니다. 고정 및 기타 <xref:System.Windows.Freezable> 기능에 대 한 자세한 내용은 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)를 참조 하세요.

- 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]또는 애니메이션 이벤트에 대 한 <xref:System.Windows.Media.Animation.Storyboard> 이벤트 처리기를 선언할 수 없습니다.

스타일에서 storyboard를 정의 하는 방법을 보여 주는 예제는 [스타일 예제에서 애니메이션 효과 적용](how-to-animate-in-a-style.md) 을 참조 하세요.

<a name="defineAStoryboardInAControlTemplateSection"></a>

## <a name="animate-in-a-controltemplate"></a>ControlTemplate에서 애니메이션 효과 적용

개체를 사용 <xref:System.Windows.Media.Animation.Storyboard> 하 여 <xref:System.Windows.Controls.ControlTemplate>에서 애니메이션을 정의할 수 있습니다. 에서를 사용 하 여 애니메이션을 적용 하 <xref:System.Windows.Media.Animation.Storyboard> 는것은다른위치를사용하는것과비슷하지만다음두가지예외가있습니다.<xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Media.Animation.Storyboard>

- <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 는<xref:System.Windows.Controls.ControlTemplate>의 자식 개체만 참조할 수 있습니다. 을 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 지정 하지 않으면 애니메이션은 <xref:System.Windows.Controls.ControlTemplate> 가 적용 되는 요소를 대상으로 합니다.

- 또는의는 <xref:System.Windows.EventTrigger.SourceName%2A> 의 자식 개체만 참조할 <xref:System.Windows.Controls.ControlTemplate> 수있습니다.<xref:System.Windows.Trigger> <xref:System.Windows.EventTrigger>

- 동적 리소스 참조 또는 데이터 바인딩 식을 사용 하 여 또는 애니메이션 <xref:System.Windows.Media.Animation.Storyboard> 속성 값을 설정할 수 없습니다. 내부의 <xref:System.Windows.Controls.ControlTemplate> 모든 항목은 스레드로부터 안전 해야 하며 타이밍 <xref:System.Windows.Freezable.Freeze%2A> <xref:System.Windows.Media.Animation.Storyboard> 시스템은 개체를 스레드로부터 안전 하 게 만들어야 합니다. 에 <xref:System.Windows.Media.Animation.Storyboard> 동적 리소스 참조 또는 데이터 바인딩 식이 포함 된 경우에는를 고정할 수 없습니다. 고정 및 기타 <xref:System.Windows.Freezable> 기능에 대 한 자세한 내용은 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)를 참조 하세요.

- 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]또는 애니메이션 이벤트에 대 한 <xref:System.Windows.Media.Animation.Storyboard> 이벤트 처리기를 선언할 수 없습니다.

에서 <xref:System.Windows.Controls.ControlTemplate>storyboard를 정의 하는 방법을 보여 주는 예제는 [ControlTemplate 예제에서 애니메이션 효과 적용](how-to-animate-in-a-controltemplate.md) 을 참조 하세요.

<a name="animateWhenAPropertyValueChanges"></a>

## <a name="animate-when-a-property-value-changes"></a>속성 값이 변경될 때 애니메이션 효과 주기

스타일 및 컨트롤 템플릿에서 트리거 개체를 사용하여 속성이 변경될 때 Storyboard를 시작할 수 있습니다. 예제는 [속성 값이 변경 되](how-to-trigger-an-animation-when-a-property-value-changes.md) 고 [ControlTemplate에서 애니메이션 효과](how-to-animate-in-a-controltemplate.md)를 주는 경우 애니메이션 트리거를 참조 하세요.

속성 <xref:System.Windows.Trigger> 개체에서 적용 하는 애니메이션은 메서드를 사용 하 <xref:System.Windows.EventTrigger> 여 <xref:System.Windows.Media.Animation.Storyboard> 시작 된 애니메이션이 나 애니메이션 보다 더 복잡 한 방식으로 동작 합니다.  다른 <xref:System.Windows.Trigger> 개체에서 정의 된 애니메이션을 "전달" 하지만 <xref:System.Windows.EventTrigger> 및 메서드 트리거 애니메이션으로 작성 합니다.

## <a name="see-also"></a>참고자료

- [애니메이션 개요](animation-overview.md)
- [속성 애니메이션 기술 개요](property-animation-techniques-overview.md)
- [Freezable 개체 개요](../advanced/freezable-objects-overview.md)
