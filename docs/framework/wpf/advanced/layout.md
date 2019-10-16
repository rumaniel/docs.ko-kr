---
title: 레이아웃
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF layout system [WPF]
- controls [WPF], layout system
- layout system [WPF]
ms.assetid: 3eecdced-3623-403a-a077-7595453a9221
ms.openlocfilehash: d4ea8d105b2d956323566a42108c7db3bfc4936d
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046345"
---
# <a name="layout"></a>레이아웃

이 항목에서는 Windows Presentation Foundation (WPF) 레이아웃 시스템에 대해 설명 합니다. WPF에서 사용자 인터페이스를 만드는 데는 레이아웃 계산이 발생 하는 방법과 시기를 이해 하는 것이 중요 합니다.

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

- [요소 경계 상자](#LayoutSystem_BoundingBox)

- [레이아웃 시스템](#LayoutSystem_Overview)

- [자식 측정 및 정렬](#LayoutSystem_Measure_Arrange)

- [패널 요소 및 사용자 지정 레이아웃 동작](#LayoutSystem_PanelsCustom)

- [레이아웃 성능 고려 사항](#LayoutSystem_Performance)

- [하위 픽셀 렌더링 및 레이아웃 반올림](#LayoutSystem_LayoutRounding)

- [새로운 기능](#LayoutSystem_whatsnext)

<a name="LayoutSystem_BoundingBox"></a>

## <a name="element-bounding-boxes"></a>요소 경계 상자

WPF의 레이아웃을 고려할 때 모든 요소를 둘러싸는 경계 상자를 이해 하는 것이 중요 합니다. 레이아웃 <xref:System.Windows.FrameworkElement> 시스템에서 사용 하는 각는 레이아웃에 슬롯으로 사용 되는 사각형으로 간주할 수 있습니다. 클래스 <xref:System.Windows.Controls.Primitives.LayoutInformation> 는 요소의 레이아웃 할당 또는 슬롯의 경계를 반환 합니다. 사각형의 크기는 사용 가능한 화면 공간, 모든 제약 조건의 크기, 레이아웃 관련 속성 (예: 여백 및 안쪽 여백) 및 부모 <xref:System.Windows.Controls.Panel> 요소의 개별 동작을 계산 하 여 결정 됩니다. 레이아웃 시스템은이 데이터를 처리 하 여 특정 <xref:System.Windows.Controls.Panel>의 모든 자식 항목의 위치를 계산할 수 있습니다. 부모 요소에 정의 된 크기 조정 특성 (예: <xref:System.Windows.Controls.Border>)은 자식에 영향을 줍니다.

다음 그림에서는 간단한 레이아웃을 보여 줍니다.

![경계 상자를 표시 하지 않는 일반적인 그리드를 표시 하는 스크린샷](./media/layout/grid-no-bounding-box-superimpose.png)

다음 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]을 사용하여 이 레이아웃을 실현할 수 있습니다.

[!code-xaml[LayoutInformation#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml#1)]

단일 <xref:System.Windows.Controls.TextBlock> 요소는 <xref:System.Windows.Controls.Grid>내에서 호스팅됩니다. 텍스트는 첫 번째 열의 왼쪽 위 모서리로만 채워지며,에 <xref:System.Windows.Controls.TextBlock> 할당 된 공간은 실제로 훨씬 더 큽니다. 모든 <xref:System.Windows.FrameworkElement> 의 경계 상자는 메서드를 <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> 사용 하 여 검색할 수 있습니다. 다음 그림에서는 <xref:System.Windows.Controls.TextBlock> 요소에 대 한 경계 상자를 보여 줍니다.

![TextBlock 경계 상자가 현재 표시 되는 것을 보여 주는 스크린샷](./media/layout/visible-textblock-bounding-box.png)

노란색 사각형에 표시 된 것 처럼 <xref:System.Windows.Controls.TextBlock> 요소에 할당 된 공간은 실제로 표시 되는 것 보다 훨씬 큽니다. 추가 요소가에 추가 <xref:System.Windows.Controls.Grid>되 면 추가 된 요소의 형식 및 크기에 따라이 할당을 축소 하거나 확장할 수 있습니다.

의 <xref:System.Windows.Controls.TextBlock> 레이아웃 슬롯은 메서드를 <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> 사용 하 <xref:System.Windows.Shapes.Path> 여으로 변환 됩니다. 이 기술은 요소의 경계 상자를 표시하는 데 유용합니다.

[!code-csharp[LayoutInformation#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml.cs#2)]
[!code-vb[LayoutInformation#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/LayoutInformation/VisualBasic/Window1.xaml.vb#2)]

<a name="LayoutSystem_Overview"></a>

## <a name="the-layout-system"></a>레이아웃 시스템

가장 간단한 레이아웃은 재귀 시스템이며 이를 통해 요소의 크기가 조정되고 요소가 배치되고 그려집니다. 구체적으로 말하자면 레이아웃은 <xref:System.Windows.Controls.Panel> <xref:System.Windows.Controls.Panel.Children%2A> 요소 컬렉션의 멤버를 측정 하 고 정렬 하는 프로세스를 설명 합니다. 레이아웃은 집약적인 프로세스입니다. <xref:System.Windows.Controls.Panel.Children%2A> 컬렉션이 클수록 수행 해야 하는 계산 횟수가 커집니다. 컬렉션을 소유 하는 <xref:System.Windows.Controls.Panel> 요소에 의해 정의 된 레이아웃 동작에 따라 복잡성이 도입 될 수도 있습니다. 와 같이 비교적 <xref:System.Windows.Controls.Panel>간단 <xref:System.Windows.Controls.Canvas>하 게는와 <xref:System.Windows.Controls.Grid>같이 보다 복잡 <xref:System.Windows.Controls.Panel>한 성능을 훨씬 더 향상 시킬 수 있습니다.

자식 <xref:System.Windows.UIElement> 에서 해당 위치를 변경할 때마다 레이아웃 시스템에서 새 패스를 트리거할 수 있습니다. 따라서 불필요한 호출로 인해 애플리케이션 성능이 저하될 수 있으므로 레이아웃 시스템을 호출할 수 있는 이벤트를 이해해야 합니다. 다음에서 레이아웃 시스템이 호출될 때 발생하는 프로세스에 대해 설명합니다.

1. 자식은 <xref:System.Windows.UIElement> 먼저 핵심 속성을 측정 하 여 레이아웃 프로세스를 시작 합니다.

2. 에 <xref:System.Windows.FrameworkElement> 정의 된 크기 조정 속성 (예 <xref:System.Windows.FrameworkElement.Width%2A>:, <xref:System.Windows.FrameworkElement.Height%2A>및 <xref:System.Windows.FrameworkElement.Margin%2A>)이 계산 됩니다.

3. <xref:System.Windows.Controls.Panel>-특정 논리 (예: <xref:System.Windows.Controls.Dock> 방향 또는 스택 <xref:System.Windows.Controls.StackPanel.Orientation%2A>)가 적용 됩니다.

4. 모든 자식을 측정한 후에 콘텐츠가 정렬됩니다.

5. <xref:System.Windows.Controls.Panel.Children%2A> 컬렉션은 화면에 그려집니다.

6. 추가 <xref:System.Windows.Controls.Panel.Children%2A> 가 컬렉션 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 에 추가 되거나 <xref:System.Windows.UIElement.UpdateLayout%2A> 가 적용 되거나 메서드가 호출 되 면 프로세스가 다시 호출 됩니다.

이 프로세스와 해당 프로세스가 호출되는 방법은 다음 섹션에 자세히 정의되어 있습니다.

<a name="LayoutSystem_Measure_Arrange"></a>

## <a name="measuring-and-arranging-children"></a>자식 측정 및 정렬

레이아웃 시스템은 <xref:System.Windows.Controls.Panel.Children%2A> 컬렉션의 각 멤버, 측정 단계 및 정렬 단계에 대해 두 개의 패스를 완료 합니다. 각 자식은 <xref:System.Windows.Controls.Panel> 고유한 특정 레이아웃 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 동작 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 을 수행 하는 자체 및 메서드를 제공 합니다.

측정 단계 중에는 <xref:System.Windows.Controls.Panel.Children%2A> 컬렉션의 각 멤버가 평가 됩니다. 이 프로세스는 <xref:System.Windows.UIElement.Measure%2A> 메서드를 호출 하 여 시작 됩니다. 이 메서드는 부모 <xref:System.Windows.Controls.Panel> 요소의 구현 내에서 호출 되며 레이아웃을 수행 하기 위해 명시적으로 호출할 필요가 없습니다.

먼저의 <xref:System.Windows.UIElement> 기본 크기 속성 ( <xref:System.Windows.UIElement.Clip%2A> 예: 및 <xref:System.Windows.UIElement.Visibility%2A>)이 계산 됩니다. 그러면에 `constraintSize` <xref:System.Windows.FrameworkElement.MeasureCore%2A>전달 되는 라는 값이 생성 됩니다.

그런 다음에 <xref:System.Windows.FrameworkElement> 정의 된 프레임 워크 속성이 처리 되어의 `constraintSize`값에 영향을 줍니다. 이러한 속성은 <xref:System.Windows.UIElement>일반적으로 <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.Width%2A> <xref:System.Windows.FrameworkElement.Margin%2A> ,,등의기본에대한크기조정특성<xref:System.Windows.FrameworkElement.Style%2A>을 설명 합니다. 이러한 각 속성은 요소를 표시하는 데 필요한 공간을 변경할 수 있습니다. <xref:System.Windows.FrameworkElement.MeasureOverride%2A>는를 매개 변수로 `constraintSize` 사용 하 여 호출 됩니다.

> [!NOTE]
> <xref:System.Windows.FrameworkElement.Height%2A> 및<xref:System.Windows.FrameworkElement.Width%2A>의속성과 와의 속성 간에는 차이가 있습니다. <xref:System.Windows.FrameworkElement.ActualWidth%2A> <xref:System.Windows.FrameworkElement.ActualHeight%2A> 예를 들어 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 속성은 다른 높이 입력 및 레이아웃 시스템을 기반으로 하는 계산 된 값입니다. 값은 실제 렌더링 패스를 기준으로 레이아웃 시스템 자체에 의해 설정 되므로 입력 변경의 기준이 되는와 <xref:System.Windows.FrameworkElement.Height%2A>같은 속성의 설정 값 보다 약간 지연 될 수 있습니다.
>
> 때문에 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 은 계산된 된 값 수는 여러 개 있을 수 있습니다 또는 보고 변경 하 여 다양 한 작업의 결과로 레이아웃 시스템에서. 레이아웃 시스템은 자식 요소에 필요한 측정 공간, 부모 요소에 의한 제약 조건 등을 계산할 수도 있습니다.

측정 단계의 궁극적인 목표는 자식에서 <xref:System.Windows.UIElement.DesiredSize%2A> <xref:System.Windows.FrameworkElement.MeasureCore%2A> 호출 중에 발생 하는을 확인 하는 것입니다. 값 <xref:System.Windows.UIElement.DesiredSize%2A> 은에 의해 <xref:System.Windows.UIElement.Measure%2A> 저장 되어 콘텐츠 정렬 단계 중에 사용 됩니다.

정렬 단계는 <xref:System.Windows.UIElement.Arrange%2A> 메서드를 호출 하 여 시작 합니다. 정렬 단계 중에 부모 <xref:System.Windows.Controls.Panel> 요소는 자식의 범위를 나타내는 사각형을 생성 합니다. 이 값은 처리를 위해 <xref:System.Windows.FrameworkElement.ArrangeCore%2A> 메서드에 전달 됩니다.

메서드 <xref:System.Windows.FrameworkElement.ArrangeCore%2A> 는 자식의를 <xref:System.Windows.UIElement.DesiredSize%2A> 평가 하 고 요소의 렌더링 된 크기에 영향을 줄 수 있는 추가 여백을 계산 합니다. <xref:System.Windows.FrameworkElement.ArrangeCore%2A><xref:System.Windows.FrameworkElement.ArrangeOverride%2A> `arrangeSize` 의<xref:System.Windows.Controls.Panel> 메서드에 매개 변수로 전달 되는를 생성 합니다. <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>자식의을 `finalSize` 생성 합니다. 마지막으로 메서드 <xref:System.Windows.FrameworkElement.ArrangeCore%2A> 는 여백 및 맞춤과 같은 오프셋 속성에 대 한 최종 평가를 수행 하 고 자식를 해당 레이아웃 슬롯 내에 배치 합니다. 자식은 할당된 공간을 모두 채울 필요가 없으며 실제 모두 채우는 경우가 드뭅니다. 그러면 컨트롤이 부모 <xref:System.Windows.Controls.Panel> 에 반환 되 고 레이아웃 프로세스가 완료 됩니다.

<a name="LayoutSystem_PanelsCustom"></a>

## <a name="panel-elements-and-custom-layout-behaviors"></a>패널 요소 및 사용자 지정 레이아웃 동작

WPF는에서 <xref:System.Windows.Controls.Panel>파생 되는 요소 그룹을 포함 합니다. 이러한 <xref:System.Windows.Controls.Panel> 요소를 사용 하면 복잡 한 여러 레이아웃을 사용할 수 있습니다. 예를 들어 <xref:System.Windows.Controls.StackPanel> 요소를 사용 하 여 스택 요소를 쉽게 달성할 수 있으며,를 <xref:System.Windows.Controls.Canvas>사용 하 여 더 복잡 하 고 사용 가능한 흐름 레이아웃을 사용할 수 있습니다.

다음 표에서는 사용 가능한 레이아웃 <xref:System.Windows.Controls.Panel> 요소를 요약 하 여 보여 줍니다.

|패널 이름|설명|
|----------------|-----------------|
|<xref:System.Windows.Controls.Canvas>|<xref:System.Windows.Controls.Canvas> 영역에 상대적인 좌표를 기준으로 자식 요소의 위치를 명시적으로 지정할 수 있는 영역을 정의 합니다.|
|<xref:System.Windows.Controls.DockPanel>|자식 요소를 서로 맞춰 가로 또는 세로로 정렬할 수 있는 영역을 정의합니다.|
|<xref:System.Windows.Controls.Grid>|열 및 행으로 구성되는 유연한 모눈 영역을 정의합니다.|
|<xref:System.Windows.Controls.StackPanel>|가로 또는 세로 방향으로 한 줄로 자식 요소를 정렬합니다.|
|<xref:System.Windows.Controls.VirtualizingPanel>|에 대 한 프레임 워크를 제공 <xref:System.Windows.Controls.Panel> 해당 자식 데이터 컬렉션을 가상화 하는 요소입니다. 이 클래스는 추상 클래스입니다.|
|<xref:System.Windows.Controls.WrapPanel>|콘텐츠를 컨테이너의 가장자리에서 다음 줄로 나눠 왼쪽에서 오른쪽으로 자식 요소의 위치를 지정합니다. 이후 정렬은 <xref:System.Windows.Controls.WrapPanel.Orientation%2A> 속성의 값에 따라 위쪽에서 아래쪽으로 또는 오른쪽에서 왼쪽으로 순차적으로 발생 합니다.|

미리 정의 <xref:System.Windows.Controls.Panel> 된 요소 중 하나를 사용 하 여 가능 하지 않은 레이아웃이 필요한 응용 프로그램의 경우 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 및 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 메서드를 <xref:System.Windows.Controls.Panel> 상속 하 고 재정의 하 여 사용자 지정 레이아웃 동작을 구현할 수 있습니다.

<a name="LayoutSystem_Performance"></a>

## <a name="layout-performance-considerations"></a>레이아웃 성능 고려 사항

레이아웃은 재귀적인 프로세스입니다. <xref:System.Windows.Controls.Panel.Children%2A> 컬렉션의 각 자식 요소는 레이아웃 시스템을 호출할 때마다 처리 됩니다. 따라서 필요하지 않을 때 레이아웃 시스템을 트리거하는 것을 피해야 합니다. 다음은 보다 뛰어난 성능을 얻는 데 도움이 되는 고려 사항입니다.

- 레이아웃 시스템에서 재귀적으로 업데이트하도록 하는 속성 값 변경에 주의해야 합니다.

  레이아웃 시스템을 초기화하는 값을 가진 종속성 속성은 공용 플래그로 표시됩니다. <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>및 <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> 는 레이아웃 시스템에서 재귀 업데이트를 적용 하는 속성 값 변경에 대 한 유용한 단서를 제공 합니다. 일반적으로 요소의 경계 상자 크기에 영향을 줄 수 있는 모든 속성은 <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> 플래그가 true로 설정 되어야 합니다. 자세한 내용은 [종속성 속성 개요](dependency-properties-overview.md)를 참조하세요.

- 가능 하면 대신 <xref:System.Windows.UIElement.RenderTransform%2A> <xref:System.Windows.FrameworkElement.LayoutTransform%2A>을 사용 합니다.

  <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 는[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]의 콘텐츠에 영향을 주는 매우 유용한 방법일 수 있습니다. 그러나 변환 결과가 다른 요소의 위치에 영향을 주지 않아도 되는 경우이 레이아웃 시스템을 호출 하지 않으므로 <xref:System.Windows.UIElement.RenderTransform%2A> <xref:System.Windows.UIElement.RenderTransform%2A> 를 대신 사용 하는 것이 가장 좋습니다. <xref:System.Windows.FrameworkElement.LayoutTransform%2A>변환을 적용 하 고 재귀적 레이아웃 업데이트를 적용 하 여 영향을 받는 요소의 새 위치를 고려 합니다.

- 에 대 한 불필요 <xref:System.Windows.UIElement.UpdateLayout%2A>한 호출을 방지 합니다.

  메서드 <xref:System.Windows.UIElement.UpdateLayout%2A> 는 재귀적 레이아웃 업데이트를 강제 적용 하며 반드시 필요한 것은 아닙니다. 전체 업데이트가 필요하다고 확신하는 경우를 제외하고는 레이아웃 시스템에서만 이 메서드를 호출합니다.

- 많은 <xref:System.Windows.Controls.Panel.Children%2A> 컬렉션을 사용 하 여 작업 하는 경우 <xref:System.Windows.Controls.VirtualizingStackPanel> 일반 <xref:System.Windows.Controls.StackPanel>대신를 사용 하는 것이 좋습니다.

  자식 컬렉션을 가상화 하 여는 <xref:System.Windows.Controls.VirtualizingStackPanel> 현재 부모의 뷰포트 내에 있는 개체만 메모리에 보관 합니다. 이를 통해 대부분의 시나리오에서 성능이 크게 향상됩니다.

<a name="LayoutSystem_LayoutRounding"></a>

## <a name="sub-pixel-rendering-and-layout-rounding"></a>하위 픽셀 렌더링 및 레이아웃 반올림

WPF 그래픽 시스템은 장치 독립적 단위를 사용 하 여 해상도 및 장치 독립성을 사용 하도록 설정 합니다. 각 장치 독립적 픽셀은 시스템의 dpi (인치당 도트 수) 설정에 따라 자동으로 크기가 조정 됩니다. 이렇게 하면 WPF 응용 프로그램에서 dpi 설정에 맞게 적절 한 크기 조정을 제공 하 고 응용 프로그램에서 자동으로 dpi를 인식 하도록 합니다.

그러나이 dpi 독립성은 앤티앨리어싱으로 인해 불규칙 한 가장자리 렌더링을 만들 수 있습니다. 일반적으로 흐리거나 반투명한 가장자리로 표시되는 이러한 아티팩트는 가장자리의 위치가 디바이스 픽셀 사이가 아닌 디바이스 픽셀 가운데에 있을 때 발생할 수 있습니다. 레이아웃 시스템에서는 레이아웃 반올림을 사용하여 조정할 수 있는 방법을 제공합니다. 레이아웃 반올림에서 레이아웃 단계 동안 모든 비정수 픽셀 값을 레이아웃 시스템이 반올림합니다.

레이아웃 반올림은 기본적으로 사용되지 않습니다. 레이아웃 반올림을 사용 하려면 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> 속성을 any <xref:System.Windows.FrameworkElement>로 `true` 설정 합니다. 종속성 속성이므로 값이 시각적 트리의 모든 자식에 전파됩니다. 전체 UI에 대해 레이아웃 반올림을 사용 하려면 루트 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> 컨테이너 `true` 에서을로 설정 합니다. 예제를 보려면 <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A>를 참조하십시오.

<a name="LayoutSystem_whatsnext"></a>

## <a name="whats-next"></a>새로운 기능

요소의 측정 방법과 정렬 방법을 이해하는 것이 레이아웃을 이해하기 위한 첫 단계입니다. 사용할 수 있는 <xref:System.Windows.Controls.Panel> 요소에 대 한 자세한 내용은 [패널 개요](../controls/panels-overview.md)를 참조 하세요. 레이아웃에 영향을 줄 수 있는 다양한 배치 속성을 더 잘 이해하려면 [맞춤, 여백 및 안쪽 여백 개요](alignment-margins-and-padding-overview.md)를 참조하세요. 간단한 응용 프로그램 [에서 모두 함께 사용할 준비가 되 면 연습: 내 첫 번째 WPF 데스크톱](../getting-started/walkthrough-my-first-wpf-desktop-application.md)응용 프로그램입니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.UIElement>
- [패널 개요](../controls/panels-overview.md)
- [맞춤, 여백 및 안쪽 여백 개요](alignment-margins-and-padding-overview.md)
- [레이아웃 및 디자인](optimizing-performance-layout-and-design.md)
