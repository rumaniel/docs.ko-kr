---
title: Panel 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Panel control [WPF], about Panel control
- controls [WPF], Panel
ms.assetid: f73644af-9941-4611-8754-6d4cef03fc44
ms.openlocfilehash: d77ce78fe914bf300c5b33019d7cf67aa4ad74c3
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291452"
---
# <a name="panels-overview"></a>Panel 개요
@no__t 요소는 요소의 크기와 크기, 위치 및 자식 콘텐츠의 정렬 등 요소의 렌더링을 제어 하는 구성 요소입니다. @No__t-0은 미리 정의 된 @no__t 1 개 요소 뿐만 아니라 사용자 지정 <xref:System.Windows.Controls.Panel> 요소를 생성할 수 있는 기능을 제공 합니다.  
  
 이 항목에는 다음 섹션이 수록되어 있습니다.  
  
- [Panel 클래스](#Panels_view_from_10000_feet)  
  
- [패널 요소의 공통 멤버](#Panels_declared_members)  
  
- [파생 패널 요소](#Panels_derived_elements)  
  
- [사용자 인터페이스 패널](#Panels_main_UI_elements)  
  
- [중첩 Panel 요소](#Panels_nested_panel_elements)  
  
- [사용자 지정 Panel 요소](#Panels_custom_panel_elements)  
  
- [지역화/세계화 지원](#Panels_global_localization)  
  
<a name="Panels_view_from_10000_feet"></a>   
## <a name="the-panel-class"></a>Panel 클래스  
 <xref:System.Windows.Controls.Panel>은 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서 레이아웃 지원을 제공 하는 모든 요소의 기본 클래스입니다. 파생 <xref:System.Windows.Controls.Panel> 요소는 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 및 코드에서 요소를 배치 하 고 정렬 하는 데 사용 됩니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에는 많은 복잡한 레이아웃을 가능하게 하는 파생 패널 구현의 포괄적인 집합이 포함됩니다. 이러한 파생 클래스는 대부분의 표준 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 시나리오를 가능하게 하는 속성 및 메서드를 표시합니다. 사용자의 요구를 충족 하는 자식 정렬 동작을 찾을 수 없는 개발자는 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 및 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 메서드를 재정의 하 여 새 레이아웃을 만들 수 있습니다. 사용자 지정 레이아웃 동작에 대한 자세한 내용은 [사용자 지정 Panel 요소](#Panels_custom_panel_elements)를 참조하세요.  
  
<a name="Panels_declared_members"></a>   
## <a name="panel-common-members"></a>패널의 공통 멤버  
 모든 <xref:System.Windows.Controls.Panel> 요소는 <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.Width%2A>, <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>, @no__t, <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 등 <xref:System.Windows.FrameworkElement>로 정의 되는 기본 크기 조정 및 위치 지정 속성을 지원 합니다. @No__t-0으로 정의 된 속성의 위치를 지정 하는 방법에 대 한 자세한 내용은 [맞춤, 여백 및 안쪽 여백 개요](../advanced/alignment-margins-and-padding-overview.md)를 참조 하세요.  
  
 <xref:System.Windows.Controls.Panel>은 레이아웃을 이해 하 고 사용 하는 데 중요 한 추가 속성을 노출 합니다. @No__t-0 속성은 <xref:System.Windows.Media.Brush>과 함께 파생 된 패널 요소 경계 사이의 영역을 채우는 데 사용 됩니다. <xref:System.Windows.Controls.Panel.Children%2A>은 <xref:System.Windows.Controls.Panel>이 구성 된 요소의 자식 컬렉션을 나타냅니다. <xref:System.Windows.Controls.Panel.InternalChildren%2A>은 <xref:System.Windows.Controls.Panel.Children%2A> 컬렉션의 내용과 데이터 바인딩에서 생성 된 멤버를 나타냅니다. 둘 다 부모에서 호스트 되는 자식 요소의 <xref:System.Windows.Controls.UIElementCollection>으로 구성 됩니다 <xref:System.Windows.Controls.Panel>.  
  
 또한 패널은 파생 된 <xref:System.Windows.Controls.Panel>에서 계층화 된 순서를 구현 하는 데 사용할 수 있는 <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType> 연결 된 속성을 노출 합니다. @No__t-1 값이 더 높은 패널의 <xref:System.Windows.Controls.Panel.Children%2A> 컬렉션의 멤버는 <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType> 값이 낮은 값 앞에 표시 됩니다. 이 기능은 <xref:System.Windows.Controls.Canvas> 및 <xref:System.Windows.Controls.Grid>과 같은 패널에 특히 유용 합니다 .이 경우 자식에서 같은 좌표 공간을 공유할 수 있습니다.  
  
 <xref:System.Windows.Controls.Panel>은 <xref:System.Windows.Controls.Panel>의 기본 프레젠테이션 동작을 재정의 하는 데 사용할 수 있는 <xref:System.Windows.Controls.Panel.OnRender%2A> 메서드를 정의 합니다.  
  
#### <a name="attached-properties"></a>연결된 속성  
 파생 패널 요소는 연결된 속성을 광범위하게 사용합니다. 연결 된 속성은 기본 CLR (공용 언어 런타임) 속성 "래퍼"가 없는 종속성 속성의 특수 한 형태입니다. 연결된 속성에는 다음 여러 예제에서 확인할 수 있는 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]의 특수 구문이 있습니다.  
  
 연결된 속성의 한 가지 목적은 자식 요소가 부모 요소를 통해 실제로 정의되는 속성의 고유 값을 저장하도록 하는 것입니다. 이 기능을 제공하는 애플리케이션에서는 자식 요소가 자신이 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]에 표시되는 방식을 부모에게 알립니다. 이 기능은 애플리케이션 레이아웃에 매우 유용합니다. 자세한 내용은 [연결된 속성 개요](../advanced/attached-properties-overview.md)를 참조하세요.  
  
<a name="Panels_derived_elements"></a>   
## <a name="derived-panel-elements"></a>파생 패널 요소  
 대부분의 개체는 <xref:System.Windows.Controls.Panel>에서 파생 되지만 모두 루트 레이아웃 공급자로 사용 하기 위한 것이 아닙니다. 응용 프로그램 @no__t를 만들도록 특별히 설계 된 6 개의 정의 된 패널 클래스 (<xref:System.Windows.Controls.Canvas>, <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Grid>, <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.VirtualizingStackPanel>, @no__t)가 있습니다.  
  
 각 패널 요소는 다음 테이블에 나와 있는 자체 특수 기능을 캡슐화합니다.  
  
|요소 이름|UI 패널 여부|설명|  
|------------------|---------------|-----------------|  
|<xref:System.Windows.Controls.Canvas>|예|@No__t-0 영역에 상대적인 좌표를 기준으로 자식 요소를 명시적으로 배치할 수 있는 영역을 정의 합니다.|  
|<xref:System.Windows.Controls.DockPanel>|예|자식 요소를 서로 맞춰 가로 또는 세로로 정렬할 수 있는 영역을 정의합니다.|  
|<xref:System.Windows.Controls.Grid>|예|열 및 행으로 구성되는 유연한 그리드 영역을 정의합니다. @No__t-0의 자식 요소는 <xref:System.Windows.FrameworkElement.Margin%2A> 속성을 사용 하 여 정확 하 게 배치할 수 있습니다.|  
|<xref:System.Windows.Controls.StackPanel>|예|가로 또는 세로 방향으로 한 줄로 자식 요소를 정렬합니다.|  
|<xref:System.Windows.Controls.Primitives.TabPanel>|아니요|@No__t-0의 탭 단추 레이아웃을 처리 합니다.|  
|<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|아니요|@No__t-0 컨트롤 내에서 콘텐츠를 정렬 합니다.|  
|<xref:System.Windows.Controls.Primitives.UniformGrid>|아니요|<xref:System.Windows.Controls.Primitives.UniformGrid>은 동일한 셀 크기를 모두 포함 하는 표 형태의 자식을 정렬 하는 데 사용 됩니다.|  
|<xref:System.Windows.Controls.VirtualizingPanel>|아니요|자식 컬렉션을 "가상화"할 수 있는 패널의 기본 클래스를 제공합니다.|  
|<xref:System.Windows.Controls.VirtualizingStackPanel>|예|가로 또는 세로 방향으로 한 줄로 콘텐츠를 정렬하고 가상화합니다.|  
|<xref:System.Windows.Controls.WrapPanel>|예|<xref:System.Windows.Controls.WrapPanel>은 왼쪽에서 오른쪽으로 자식 요소를 배치 하 고 콘텐츠를 포함 하는 상자의 가장자리에 있는 다음 줄로 바꿉니다. 다음 정렬은 <xref:System.Windows.Controls.WrapPanel.Orientation%2A> 속성의 값에 따라 위쪽에서 아래쪽으로 또는 오른쪽에서 왼쪽으로 순차적으로 발생 합니다.|  
  
<a name="Panels_main_UI_elements"></a>   
## <a name="user-interface-panels"></a>사용자 인터페이스 패널  
 @No__t에서 사용할 수 있는 6 개의 패널 클래스는 <xref:System.Windows.Controls.Canvas>, <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Grid>, <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.VirtualizingStackPanel>, <xref:System.Windows.Controls.WrapPanel> [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 시나리오를 지원 하도록 최적화 되어 있습니다. 이러한 패널 요소는 쉽게 사용할 수 있고, 유연하고, 대부분 애플리케이션용으로 충분히 확장 가능합니다.  
  
 각각의 파생 된 <xref:System.Windows.Controls.Panel> 요소는 크기 조정 제약 조건을 다르게 처리 합니다. 수평 또는 수직 방향의 제약 조건을 처리 하는 <xref:System.Windows.Controls.Panel>의 경우 레이아웃을 보다 예측 가능 하 게 만들 수 있습니다.  
  
|**패널 이름**|**x 차원**|**y 차원**|  
|--------------------|----------------------|----------------------|  
|<xref:System.Windows.Controls.Canvas>|콘텐츠로 제한됨|콘텐츠로 제한됨|  
|<xref:System.Windows.Controls.DockPanel>|제한됨|제한됨|  
|<xref:System.Windows.Controls.StackPanel> (세로 방향)|제한됨|콘텐츠로 제한됨|  
|<xref:System.Windows.Controls.StackPanel> (가로 방향)|콘텐츠로 제한됨|제한됨|  
|<xref:System.Windows.Controls.Grid>|제한됨|@No__t-0이 행 및 열에 적용 되는 경우를 제외 하 고 제한 됩니다.|  
|<xref:System.Windows.Controls.WrapPanel>|콘텐츠로 제한됨|콘텐츠로 제한됨|  
  
 이러한 각 요소에 대한 자세한 설명과 사용법 예제는 아래 내용을 참조하세요.  
  
<a name="Panels_overview_Canvas_subsection"></a>   
### <a name="canvas"></a>Canvas  
 @No__t-0 요소는 절대 *x* 및 *y*좌표에 따라 콘텐츠의 위치를 지정할 수 있습니다. 요소를 고유한 위치에 그릴 수 있고, 여러 요소가 같은 좌표를 사용하는 경우에는 요소가 태그에 표시되는 순서에 따라 요소를 그리는 순서가 결정됩니다.  
  
 <xref:System.Windows.Controls.Canvas>은 <xref:System.Windows.Controls.Panel>의 가장 유연한 레이아웃 지원 기능을 제공 합니다. Height 및 Width 속성은 캔버스 영역을 정의 하는 데 사용 되 고 내부 요소에는 부모 <xref:System.Windows.Controls.Canvas>의 영역을 기준으로 하는 절대 좌표가 할당 됩니다. @No__t-0, <xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=nameWithType> <xref:System.Windows.Controls.Canvas.Right%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Controls.Canvas.Bottom%2A?displayProperty=nameWithType>의 네 가지 연결 된 속성을 @no__t 사용 하 여 개발자가 화면에서 요소를 정확 하 게 배치 하 고 정렬할 수 있습니다.  
  
#### <a name="cliptobounds-within-a-canvas"></a>캔버스 내의 ClipToBounds  
 <xref:System.Windows.FrameworkElement.Height%2A>  및 <xref:System.Windows.FrameworkElement.Width%2A>의 바깥쪽에 있는 좌표의 경우에도 화면에서 임의의 위치에 자식 요소를 배치할 수 있습니다. 또한 <xref:System.Windows.Controls.Canvas>은 자식 크기의 영향을 받지 않습니다. 따라서 자식 요소가 부모 <xref:System.Windows.Controls.Canvas>의 경계 사각형 외부에 있는 다른 요소를 과도 하 게 그릴 수 있습니다. @No__t-0의 기본 동작은 부모 <xref:System.Windows.Controls.Canvas>의 범위 밖에 자식을 그릴 수 있도록 하는 것입니다. 이 동작이 원치 않는 경우 <xref:System.Windows.UIElement.ClipToBounds%2A> 속성을 `true`로 설정할 수 있습니다. 이렇게 하면 <xref:System.Windows.Controls.Canvas>이 자체 크기에 맞게 잘립니다. <xref:System.Windows.Controls.Canvas>은 자식 요소를 해당 범위 밖으로 그릴 수 있는 유일한 레이아웃 요소입니다.  
  
 [너비 속성 비교 샘플](https://go.microsoft.com/fwlink/?LinkID=160050)에서 동작을 그래픽 방식으로 설명합니다.  
  
#### <a name="defining-and-using-a-canvas"></a>Canvas 정의 및 사용  
 @No__t-0 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 또는 코드를 사용 하 여 인스턴스화할 수 있습니다. 다음 예제에서는 <xref:System.Windows.Controls.Canvas>을 사용 하 여 콘텐츠를 절대적으로 배치 하는 방법을 보여 줍니다. 이 코드는 세 개의 100픽셀 사각형을 생성합니다. 첫 번째 사각형은 빨간색이고 왼쪽 위(*x, y*) 위치는 (0, 0)으로 지정됩니다. 두 번째 사각형은 녹색이고 왼쪽 위 위치는 (100, 100)으로, 첫 번째 사각형의 오른쪽 바로 아래입니다. 세 번째 사각형은 파란색이고 왼쪽 위 위치는 (50, 50)이므로 첫 번째 사각형의 오른쪽 아래 사분면과 두 번째 사각형의 왼쪽 위 사분면을 포함합니다. 세 번째 사각형이 마지막으로 배치되므로 다른 두 개의 사각형 위에 있는 것처럼 보입니다. 즉, 겹치는 부분은 세 번째 상자의 색으로 표시됩니다.  
  
 [!code-csharp[CanvasOvwSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CanvasOvwSample/CSharp/Canvas_Ovw_Sample.cs#1)]
 [!code-vb[CanvasOvwSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasOvwSample/VisualBasic/canvas_vb.vb#1)]
 [!code-xaml[CanvasOvwSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/CanvasOvwSample/XAML/default.xaml#1)]  
  
 컴파일된 애플리케이션은 다음과 같은 새 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]를 생성합니다.  
  
 ![일반적인 Canvas 요소](./media/panel-intro-canvas.PNG "panel_intro_canvas")  
  
<a name="Panels_overview_DockPanel_subsection"></a>   
### <a name="dockpanel"></a>DockPanel  
 @No__t-0 요소는 자식 콘텐츠 요소에 설정 된 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> 연결 된 속성을 사용 하 여 컨테이너의 가장자리를 따라 콘텐츠를 배치 합니다. @No__t-0이 <xref:System.Windows.Controls.Dock.Top> 또는 <xref:System.Windows.Controls.Dock.Bottom>로 설정 된 경우 자식 요소를 서로 위나 아래에 배치 합니다. @No__t-0이 <xref:System.Windows.Controls.Dock.Left> 또는 <xref:System.Windows.Controls.Dock.Right>로 설정 된 경우 자식 요소를 서로 왼쪽 또는 오른쪽에 배치 합니다. @No__t-0 속성은 <xref:System.Windows.Controls.DockPanel>의 자식으로 추가 된 마지막 요소의 위치를 결정 합니다.  
  
 @No__t-0을 사용 하 여 일련의 단추와 같은 관련 컨트롤 그룹을 배치할 수 있습니다. 또는이를 사용 하 여 Microsoft Outlook에서 발견 된 것과 유사한 "가는" [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]을 만들 수 있습니다.  
  
#### <a name="sizing-to-content"></a>콘텐츠에 맞게 크기 조정  
 @No__t-0 및 <xref:System.Windows.FrameworkElement.Width%2A> 속성이 지정 되지 않은 경우 해당 내용에 @no__t 2 크기를 지정 합니다. 자식 요소의 크기를 수용하도록 크기가 증가 또는 감소할 수 있습니다. 그러나 이러한 속성을 지정 하 고 지정 된 다음 자식 요소에 더 이상 공간이 없는 경우 <xref:System.Windows.Controls.DockPanel>은 자식 요소 또는 후속 자식 요소를 표시 하지 않고 이후 자식 요소를 측정 하지 않습니다.  
  
#### <a name="lastchildfill"></a>LastChildFill  
 기본적으로 <xref:System.Windows.Controls.DockPanel> 요소의 마지막 자식은 나머지 할당 되지 않은 공간을 "채웁니다". 이 동작을 원하지 않는 경우 <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> 속성을 `false`로 설정 합니다.  
  
#### <a name="defining-and-using-a-dockpanel"></a>DockPanel 정의 및 사용  
 다음 예제에서는 <xref:System.Windows.Controls.DockPanel>을 사용 하 여 공간을 분할 하는 방법을 보여 줍니다. 5 개의 <xref:System.Windows.Controls.Border> 요소는 부모 <xref:System.Windows.Controls.DockPanel>의 자식으로 추가 됩니다. 각각은 <xref:System.Windows.Controls.DockPanel>의 다른 위치 지정 속성을 사용 하 여 공간을 분할 합니다. 마지막 요소가 나머지 할당되지 않은 공간을 “채웁니다”.  
  
 [!code-cpp[DockPanelOvwSample#1](~/samples/snippets/cpp/VS_Snippets_Wpf/DockPanelOvwSample/CPP/DockPanel_Ovw_Sample.cpp#1)]
 [!code-csharp[DockPanelOvwSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/DockPanelOvwSample/CSharp/DockPanel_Ovw_Sample.cs#1)]
 [!code-vb[DockPanelOvwSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelOvwSample/VisualBasic/dockpanel_vb.vb#1)]
 [!code-xaml[DockPanelOvwSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/DockPanelOvwSample/XAML/default.xaml#1)]  
  
 컴파일된 애플리케이션은 다음과 같은 새 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]를 생성합니다.  
  
 ![일반적인 DockPanel 시나리오](./media/panel-intro-dockpanel.PNG "panel_intro_dockpanel")  
  
<a name="Panels_overview_Grid_subsection"></a>   
### <a name="grid"></a>표 형태  
 @No__t-0 요소는 절대 위치 지정 및 표 형식 데이터 컨트롤의 기능을 병합 합니다. @No__t-0을 사용 하면 요소를 쉽게 배치 하 고 스타일을 지정할 수 있습니다. <xref:System.Windows.Controls.Grid>을 사용 하면 유연한 행 및 열 그룹화를 정의할 수 있으며 여러 <xref:System.Windows.Controls.Grid> 요소 간의 크기 조정 정보를 공유 하는 메커니즘도 제공 합니다.  
  
#### <a name="how-is-grid-different-from-table"></a>Grid는 Table과 어떻게 다를까요?  
 <xref:System.Windows.Documents.Table> 및 <xref:System.Windows.Controls.Grid>은 몇 가지 일반적인 기능을 공유 하지만 각각 서로 다른 시나리오에 가장 적합 합니다. @No__t-0은 유동 콘텐츠 내에서 사용 하도록 설계 되었습니다 (유동 콘텐츠에 대 한 자세한 내용은 [유동 문서 개요](../advanced/flow-document-overview.md) 참조). 그리드는 폼 내부에서 사용하는 것이 적합합니다(기본적으로 유동 콘텐츠 외부의 모든 위치). @No__t-0에서 <xref:System.Windows.Documents.Table>은 페이지 매김, 열 리플로우 및 내용 선택과 같은 유동 콘텐츠 동작을 지원 하지만 <xref:System.Windows.Controls.Grid>는 그렇지 않습니다. 반면에 <xref:System.Windows.Controls.Grid>은 <xref:System.Windows.Controls.Grid>를 포함 하 여 행 및 열 인덱스를 기반으로 하는 요소를 추가 하는 등의 다양 한 이유로 <xref:System.Windows.Documents.FlowDocument>의 외부에서 가장 잘 사용 되며, <xref:System.Windows.Documents.Table>은 그렇지 않습니다. @No__t-0 요소를 사용 하면 자식 콘텐츠를 계층화 하 여 단일 "셀"에 두 개 이상의 요소가 있을 수 있습니다. <xref:System.Windows.Documents.Table> 레이어를 지원 하지 않습니다. @No__t의 자식 요소는 "셀" 경계 영역을 기준으로 절대적으로 배치 될 수 있습니다. <xref:System.Windows.Documents.Table> 이 기능을 지원 하지 않습니다. 마지막으로 <xref:System.Windows.Controls.Grid>은 <xref:System.Windows.Documents.Table> 보다 더 밝은 가중치입니다.  
  
#### <a name="sizing-behavior-of-columns-and-rows"></a>열 및 행의 크기 조정 동작  
 @No__t 내에서 정의 된 열과 행은 <xref:System.Windows.GridUnitType.Star> 크기 조정을 사용 하 여 나머지 공간을 비례적으로 배포할 수 있습니다. 행 또는 열의 높이나 너비로 <xref:System.Windows.GridUnitType.Star>을 선택 하면 해당 열 이나 행이 사용 가능한 나머지 공간의 가중치 비율을 받습니다. 이는 열 또는 행 내의 콘텐츠 크기에 따라 공간을 균등 하 게 분산 하는 <xref:System.Windows.GridUnitType.Auto>과는 대조적입니다. 이 값은 `*` 또는 `2*`([!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]을 사용할 경우)로 표현됩니다. 첫 번째 경우에 행 또는 열에는 사용 가능한 공간의 1배가 할당되고, 두 번째 경우에는 2배가 할당됩니다. 이 기법을 결합 하 여 공간을 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 및 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> @no__t의 공간에 비례 하 게 분산 하면 화면 공간의 백분율을 기준으로 레이아웃 공간을 분할할 수 있습니다. <xref:System.Windows.Controls.Grid> 이 방식으로 공간을 배분할 수 있는 유일한 레이아웃 패널 이며  
  
#### <a name="defining-and-using-a-grid"></a>그리드 정의 및 사용  
 다음 예제에서는 Windows 시작 메뉴에서 사용할 수 있는 실행 대화 상자에 있는 것과 유사한 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]을 빌드하는 방법을 보여 줍니다.  
  
 [!code-csharp[GridRunDialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
 컴파일된 애플리케이션은 다음과 같은 새 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]를 생성합니다.  
  
 ![일반적인 Grid 요소](./media/avalon-run-dialog.PNG "avalon_run_dialog")  
  
<a name="Panels_overview_StackPanel_subsection"></a>   
### <a name="stackpanel"></a>StackPanel  
 @No__t-0은 할당 된 방향으로 요소를 "stack" 할 수 있습니다. 기본 누적 방향은 세로 방향입니다. @No__t-0 속성은 콘텐츠 흐름을 제어 하는 데 사용할 수 있습니다.  
  
#### <a name="stackpanel-vs-dockpanel"></a>StackPanel 및 DockPanel  
 @No__t-0은 자식 요소를 "stack" 할 수 있지만 <xref:System.Windows.Controls.DockPanel>과 <xref:System.Windows.Controls.StackPanel>는 일부 사용 시나리오에서 유사한 결과를 생성 하지 않습니다. 예를 들어 자식 요소의 순서는 <xref:System.Windows.Controls.DockPanel>의 크기에 영향을 줄 수 있지만 <xref:System.Windows.Controls.StackPanel>에는 영향을 주지 않습니다. @No__t-0은 <xref:System.Double.PositiveInfinity>의 방향으로 측정 되는 반면, <xref:System.Windows.Controls.DockPanel>는 사용 가능한 크기만 측정 하기 때문입니다.  
  
 다음 예제에서는 이 키의 차이를 보여 줍니다.  
  
 [!code-cpp[StackPanelOvw4#1](~/samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xaml[StackPanelOvw4#1](~/samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
 이 그림에서 렌더링 동작의 차이를 확인할 수 있습니다.  
  
 ![Screenshot: StackPanel 및 DockPanel 스크린샷](./media/layout-smiley-stackpanel.PNG "layout_smiley_stackpanel")  
  
#### <a name="defining-and-using-a-stackpanel"></a>StackPanel 정의 및 사용  
 다음 예제에서는 <xref:System.Windows.Controls.StackPanel>을 사용 하 여 세로로 배치 된 단추 집합을 만드는 방법을 보여 줍니다. 가로 위치 지정의 경우 <xref:System.Windows.Controls.StackPanel.Orientation%2A> 속성을 <xref:System.Windows.Controls.Orientation.Horizontal>로 설정 합니다.  
  
 [!code-csharp[StackPanel_ovw2#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanel_ovw2/CSharp/StackPanel_Ovw_Sample2.cs#1)]
 [!code-vb[StackPanel_ovw2#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanel_ovw2/VisualBasic/StackPanelOvw.vb#1)]  
  
 컴파일된 애플리케이션은 다음과 같은 새 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]를 생성합니다.  
  
 ![일반적인 StackPanel 요소](./media/panel-intro-stackpanel.PNG "panel_intro_stackpanel")  
  
<a name="Panels_overview_VirtualizingStackPanel_subsection"></a>   
#### <a name="virtualizingstackpanel"></a>VirtualizingStackPanel  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]은 데이터 바인딩된 자식 콘텐츠를 자동으로 "가상화" 하는 <xref:System.Windows.Controls.StackPanel> 요소의 변형을 제공 합니다. 여기서 가상화라는 단어는 화면에 표시되는 항목에 따라 많은 수의 데이터 항목에서 요소의 하위 집합이 생성되는 기술을 가리킵니다. 특정 시점에 화면에 표시되는 것보다 많은 개수의 UI 요소를 생성하는 것은 메모리 및 프로세서 측면에서 비효율적입니다. <xref:System.Windows.Controls.VirtualizingStackPanel> (<xref:System.Windows.Controls.VirtualizingPanel>에서 제공 하는 기능을 통해)은 표시 되는 항목을 계산 하 고 <xref:System.Windows.Controls.ItemsControl>의 <xref:System.Windows.Controls.ItemContainerGenerator> (예: <xref:System.Windows.Controls.ListBox> 또는 @no__t)와 연동 하 여 표시 되는 항목에 대 한 요소만 만듭니다.  
  
 @No__t-0 요소는 <xref:System.Windows.Controls.ListBox>과 같은 컨트롤에 대 한 항목으로 호스트 되는 항목으로 자동 설정 됩니다. 데이터 바인딩된 컬렉션을 호스트 하는 경우 콘텐츠가 @no__t 범위 내에 있으면 콘텐츠가 자동으로 가상화 됩니다. 이렇게 하면 많은 자식 항목을 호스트할 때 성능이 향상됩니다.  
  
 다음 태그는 <xref:System.Windows.Controls.VirtualizingStackPanel>을 항목 호스트로 사용 하는 방법을 보여 줍니다. 가상화를 수행 하려면 <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizingProperty?displayProperty=nameWithType> 연결 된 속성을 `true` (기본값)으로 설정 해야 합니다.  
  
 [!code-xaml[VirtualizingStackPanel_Intro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/VirtualizingStackPanel_Intro/CS/default.xaml#1)]  
  
<a name="Panels_overview_WrapPanel"></a>   
### <a name="wrappanel"></a>WrapPanel  
 <xref:System.Windows.Controls.WrapPanel>은 자식 요소를 왼쪽에서 오른쪽으로 순차적으로 배치 하는 데 사용 되며, 부모 컨테이너의 가장자리에 도달할 때 콘텐츠를 다음 줄로 나눕니다. 콘텐츠는 가로 또는 세로 방향으로 설정할 수 있습니다. <xref:System.Windows.Controls.WrapPanel>은 간단한 흐름 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 시나리오에 유용 합니다. 또한 모든 자식 요소에 균일한 크기를 적용하는 데 사용될 수 있습니다.  
  
 다음 예제에서는 <xref:System.Windows.Controls.WrapPanel>을 만들어 해당 컨테이너의 가장자리에 도달할 때 줄 바꿈되는 @no__t 1 컨트롤을 표시 하는 방법을 보여 줍니다.  
  
 [!code-cpp[WrapPanel_Intro#1](~/samples/snippets/cpp/VS_Snippets_Wpf/WrapPanel_Intro/CPP/WrapPanel_Code.cpp#1)]
 [!code-csharp[WrapPanel_Intro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/WrapPanel_Intro/CSharp/WrapPanel_Code.cs#1)]
 [!code-vb[WrapPanel_Intro#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WrapPanel_Intro/VisualBasic/WrapPanel_vb.vb#1)]
 [!code-xaml[WrapPanel_Intro#1](~/samples/snippets/xaml/VS_Snippets_Wpf/WrapPanel_Intro/XAML/default.xaml#1)]  
  
 컴파일된 애플리케이션은 다음과 같은 새 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]를 생성합니다.  
  
 ![일반적인 WrapPanel 요소](./media/wrappanel-element.PNG "WrapPanel_Element")  
  
<a name="Panels_nested_panel_elements"></a>   
## <a name="nested-panel-elements"></a>중첩 Panel 요소  
 <xref:System.Windows.Controls.Panel> 요소는 복합 레이아웃을 만들기 위해 서로 중첩 될 수 있습니다. 이는 1 개의 <xref:System.Windows.Controls.Panel> @no__t의 일부에 이상적 이지만 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]의 다른 부분에 대 한 요구 사항을 충족 하지 못할 수 있는 상황에서 매우 유용 합니다.  
  
 애플리케이션에서 지원할 수 있는 중첩 횟수에는 실제로 제한이 없지만, 일반적으로 원하는 레이아웃에 실제로 필요한 패널만 사용하도록 애플리케이션을 제한하는 것이 가장 좋습니다. 대부분의 경우에는 레이아웃 컨테이너로 서의 유연성으로 인해 중첩 된 패널 대신 <xref:System.Windows.Controls.Grid> 요소를 사용할 수 있습니다. 이 요소를 통해 불필요한 요소를 트리에서 제거하여 애플리케이션 성능을 향상할 수 있습니다.  
  
 다음 예제에서는 특정 레이아웃을 얻기 위해 중첩 된 <xref:System.Windows.Controls.Panel> 요소를 활용 하는 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]을 만드는 방법을 보여 줍니다. 이 경우 <xref:System.Windows.Controls.DockPanel> 요소를 사용 하 여 @no__t 1 구조와 중첩 된 <xref:System.Windows.Controls.StackPanel> 요소, <xref:System.Windows.Controls.Grid>을 제공 하 고 <xref:System.Windows.Controls.Canvas>를 사용 하 여 자식 요소를 부모 <xref:System.Windows.Controls.DockPanel> 내에 정확 하 게 배치할 수 있습니다.  
  
 [!code-csharp[Nested_Panels#1](~/samples/snippets/csharp/VS_Snippets_Wpf/Nested_Panels/CSharp/nestedpanels.cs#1)]
 [!code-vb[Nested_Panels#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Nested_Panels/VisualBasic/nestedpanels.vb#1)]  
  
 컴파일된 애플리케이션은 다음과 같은 새 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]를 생성합니다.  
  
 ![중첩된 패널의 이점을 활용하는 UI](./media/nested-panels.PNG "nested_panels")  
  
<a name="Panels_custom_panel_elements"></a>   
## <a name="custom-panel-elements"></a>사용자 지정 Panel 요소  
 @No__t-0은 유연한 레이아웃 컨트롤 배열을 제공 하지만 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 및 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 메서드를 재정의 하 여 사용자 지정 레이아웃 동작을 구현할 수도 있습니다. 사용자 지정 크기 조정 및 위치 지정을 수행하려면 이러한 재정의 메서드 내에 새로운 위치 지정 동작을 정의합니다.  
  
 마찬가지로, 파생 클래스 (예: <xref:System.Windows.Controls.Canvas> 또는 <xref:System.Windows.Controls.Grid>)를 기반으로 하는 사용자 지정 레이아웃 동작은 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 및 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 메서드를 재정의 하 여 정의할 수 있습니다.  
  
 다음 태그는 사용자 지정 <xref:System.Windows.Controls.Panel> 요소를 만드는 방법을 보여 줍니다. @No__t-1로 정의 된이 새 <xref:System.Windows.Controls.Panel>은 하드 코딩 된 *x* 및 *y*좌표를 사용 하 여 자식 요소의 위치 지정을 지원 합니다. 이 예제에서 <xref:System.Windows.Shapes.Rectangle> 요소 (표시 되지 않음)는 플롯 지점 50 (*x*) 및 50 (*y*)에 배치 됩니다.  
  
 [!code-cpp[PlotPanel#1](~/samples/snippets/cpp/VS_Snippets_Wpf/PlotPanel/CPP/PlotPanel.cpp#1)]
 [!code-csharp[PlotPanel#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PlotPanel/CSharp/PlotPanel.cs#1)]
 [!code-vb[PlotPanel#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PlotPanel/VisualBasic/PlotPanel.vb#1)]  
  
 더 복잡한 사용자 지정 패널 구현을 보려면 [Create a Custom Content-Wrapping Panel Sample](https://go.microsoft.com/fwlink/?LinkID=159979)(사용자 지정 콘텐츠 줄 바꿈 패널 샘플 만들기)을 참조하세요.  
  
<a name="Panels_global_localization"></a>   
## <a name="localizationglobalization-support"></a>지역화/세계화 지원  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 지역화 가능한 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 만들기에 유용한 다양한 기능을 지원합니다.  
  
 모든 패널 요소는 기본적으로 사용자의 로캘 또는 언어 설정에 따라 콘텐츠를 동적으로 다시 이동 하는 데 사용할 수 있는 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 속성을 지원 합니다. 자세한 내용은 <xref:System.Windows.FrameworkElement.FlowDirection%2A>을 참조하세요.  
  
 @No__t-0 속성은 응용 프로그램 개발자가 지역화 된 @no__t의 필요성을 예상할 수 있도록 하는 메커니즘을 제공 합니다. 이 속성의 <xref:System.Windows.SizeToContent.WidthAndHeight> 값을 사용 하면 부모 <xref:System.Windows.Window>은 항상 내용에 맞게 동적으로 크기가 조정 되며 인공 높이나 너비 제한으로 제한 되지 않습니다.  
  
 <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Grid> 및 <xref:System.Windows.Controls.StackPanel>는 지역화 가능한 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]에 대 한 모든 좋은 선택 항목입니다. 그러나 <xref:System.Windows.Controls.Canvas>은 콘텐츠를 절대적으로 배치 하므로 지역화 하기가 어렵기 때문에 좋은 선택이 아닙니다.  
  
 지역화할 수 있는 Ui (사용자 인터페이스)를 사용 하 여 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [자동 레이아웃 사용 개요](../advanced/use-automatic-layout-overview.md)를 참조 하세요.  
  
## <a name="see-also"></a>참조

- [연습: 내 첫 WPF 데스크톱 애플리케이션](../getting-started/walkthrough-my-first-wpf-desktop-application.md)
- [WPF 레이아웃 갤러리 샘플](https://go.microsoft.com/fwlink/?LinkID=160054)
- [레이아웃](../advanced/layout.md)
- [WPF Controls Gallery Sample](https://go.microsoft.com/fwlink/?LinkID=160053)(WPF 컨트롤 갤러리 샘플)
- [맞춤, 여백 및 안쪽 여백 개요](../advanced/alignment-margins-and-padding-overview.md)
- [사용자 지정 콘텐츠 래핑 패널 샘플 만들기](https://go.microsoft.com/fwlink/?LinkID=159979)
- [연결된 속성 개요](../advanced/attached-properties-overview.md)
- [자동 레이아웃 사용 개요](../advanced/use-automatic-layout-overview.md)
- [레이아웃 및 디자인](../advanced/optimizing-performance-layout-and-design.md)
