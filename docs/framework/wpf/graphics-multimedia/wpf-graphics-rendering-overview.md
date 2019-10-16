---
title: WPF 그래픽 렌더링 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rendering
- rendering graphics [WPF]
ms.assetid: 6dec9657-4d8c-4e46-8c54-40fb80008265
ms.openlocfilehash: 09f5f026ed320aaa253d8cdf6e0b271235aff604
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004174"
---
# <a name="wpf-graphics-rendering-overview"></a>WPF 그래픽 렌더링 개요
이 항목에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시각적 계층에 대해 간략하게 설명합니다. @No__t-1 모델에서 렌더링을 지원 하기 위해 <xref:System.Windows.Media.Visual> 클래스의 역할에 중점을 둘 수 있습니다.  

<a name="role_of_visual_object"></a>   
## <a name="role-of-the-visual-object"></a>시각적 개체의 역할  
 합니다 <xref:System.Windows.Media.Visual> 클래스는 기본 추상화는 모든 <xref:System.Windows.FrameworkElement> 개체에서 파생 됩니다. 또한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 새 컨트롤을 작성하기 위한 진입점으로도 사용되며, Win32 애플리케이션 모델에서는 여러 가지 측면에서 창 핸들(HWND)로도 간주될 수 있습니다.  
  
 합니다 <xref:System.Windows.Media.Visual> 개체는 핵심 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 개체를 렌더링 지원을 제공 하는 역할입니다. @No__t-0 및 <xref:System.Windows.Controls.TextBox>과 같은 사용자 인터페이스 컨트롤은 <xref:System.Windows.Media.Visual> 클래스에서 파생 되 고 렌더링 데이터를 유지 하는 데 사용 됩니다. @No__t-0 개체는 다음에 대 한 지원을 제공 합니다.  
  
- 출력 표시: 시각적 개체의 serialize 된 지속형 그리기 콘텐츠를 렌더링 합니다.  
  
- 변형 시각적 개체에 대 한 변환 수행  
  
- 캡처하거나 시각적 개체에 대 한 클리핑 영역 지원 제공  
  
- 적중 횟수 테스트: 좌표 또는 기 하 도형이 시각적 개체의 범위 내에 포함 되어 있는지 여부를 확인 합니다.  
  
- 경계 상자 계산: 시각적 개체의 경계 사각형을 결정 합니다.  
  
 그러나 <xref:System.Windows.Media.Visual> 개체에는 다음과 같은 비 렌더링 기능에 대 한 지원이 포함 되지 않습니다.  
  
- 이벤트 처리  
  
- 레이아웃  
  
- 스타일  
  
- 데이터 바인딩  
  
- 전역화  
  
 <xref:System.Windows.Media.Visual>은 자식 클래스가 파생 되어야 하는 공용 추상 클래스로 노출 됩니다. 다음 그림에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 노출되는 시각적 개체의 계층 구조를 보여 줍니다.  
  
 ![시각적 개체에서 파생된 클래스의 다이어그램](./media/wpf-graphics-rendering-overview/classes-derived-visual-object.png)    
  
### <a name="drawingvisual-class"></a>DrawingVisual 클래스  
 @No__t-0은 도형, 이미지 또는 텍스트를 렌더링 하는 데 사용 되는 간단한 그리기 클래스입니다. 이 클래스는 런타임 성능을 향상시키는 레이아웃이나 이벤트 처리를 제공하지 않으므로 간단한 클래스로 간주됩니다. 이러한 이유 때문에 그리기는 배경 및 클립 아트에 적합합니다. @No__t-0은 사용자 지정 시각적 개체를 만드는 데 사용할 수 있습니다. 자세한 내용은 [DrawingVisual 개체 사용](using-drawingvisual-objects.md)을 참조하세요.  
  
### <a name="viewport3dvisual-class"></a>Viewport3DVisual 클래스  
 @No__t-0은 2D <xref:System.Windows.Media.Visual>과 <xref:System.Windows.Media.Media3D.Visual3D> 개체 간의 브리지를 제공 합니다. @No__t-0 클래스는 모든 3D 시각적 요소의 기본 클래스입니다. @No__t-0을 사용 하려면 <xref:System.Windows.Media.Media3D.Viewport3DVisual.Camera%2A> 값과 <xref:System.Windows.Media.Media3D.Viewport3DVisual.Viewport%2A> 값을 정의 해야 합니다. 카메라를 사용하면 장면을 볼 수 있습니다. 뷰포트는 프로젝션이 2D 표면에 매핑되는 위치를 설정합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 3D에 대한 자세한 내용은 [3차원 그래픽 개요](3-d-graphics-overview.md)를 참조하세요.  
  
### <a name="containervisual-class"></a>ContainerVisual 클래스  
 합니다 <xref:System.Windows.Media.ContainerVisual> 클래스의 컬렉션에 대 한 컨테이너로 사용 됩니다 <xref:System.Windows.Media.Visual> 개체입니다. @No__t-0 클래스는 <xref:System.Windows.Media.ContainerVisual> 클래스에서 파생 되므로 시각적 개체의 컬렉션을 포함할 수 있습니다.  
  
### <a name="drawing-content-in-visual-objects"></a>시각적 개체의 그리기 콘텐츠  
 @No__t-0 개체는 해당 렌더링 데이터를 **벡터 그래픽 명령 목록**으로 저장 합니다. 명령 목록의 각 항목은 그래픽 데이터 및 연결된 리소스의 하위 수준 집합을 serialize된 형식으로 나타냅니다. 그리기 콘텐츠를 포함할 수 있는 렌더링 데이터 형식에는 네 가지가 있습니다.  
  
|그리기 콘텐츠 형식|설명|  
|--------------------------|-----------------|  
|벡터 그래픽|벡터 그래픽 데이터와 관련 <xref:System.Windows.Media.Brush> 및 @no__t 정보를 나타냅니다.|  
|이미지|@No__t-0으로 정의 된 영역 내의 이미지를 나타냅니다.|  
|문자 모양|지정 된 글꼴 리소스에서 문자 모양의 시퀀스인 <xref:System.Windows.Media.GlyphRun>을 렌더링 하는 그리기를 나타냅니다. 이 방식에 따라 텍스트가 표시됩니다.|  
|비디오|비디오를 렌더링하는 그리기를 나타냅니다.|  
  
 @No__t-0을 사용 하면 <xref:System.Windows.Media.Visual>을 시각적 콘텐츠로 채울 수 있습니다. @No__t-0 개체의 그리기 명령을 사용 하는 경우 나중에 그래픽 시스템에서 사용할 렌더링 데이터 집합을 저장 하 게 됩니다. 화면에 실시간으로 그리지 않습니다.  
  
 @No__t-1과 같은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤을 만들 때 컨트롤은 자체적으로 그리기 위해 렌더링 데이터를 암시적으로 생성 합니다. 예를 들어 @no__t <xref:System.Windows.Controls.Button>의 속성을 설정 하면 컨트롤에서 문자 모양의 렌더링 표현을 저장 합니다.  
  
 @No__t-0은 <xref:System.Windows.Media.DrawingGroup> 내에 포함 된 하나 이상의 <xref:System.Windows.Media.Drawing> 개체로 콘텐츠를 설명 합니다. @No__t-0은 불투명 마스크, 변환, 비트맵 효과 및 해당 내용에 적용 되는 기타 작업에 대해서도 설명 합니다. @no__t 0 작업은 콘텐츠가 렌더링 될 때 (<xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>, <xref:System.Windows.Media.DrawingGroup.Opacity%2A>, <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>, <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>, <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>) 다음 순서로 적용 됩니다.  
  
 다음 그림에서는 <xref:System.Windows.Media.DrawingGroup> 연산이 렌더링 시퀀스 중에 적용 되는 순서를 보여 줍니다.  
  
 ![작업 Graphcismm_drawinggroup_order DrawingGroup 순서](./media/graphcismm-drawinggroup-order.png "")  
DrawingGroup 작업의 순서  
  
 자세한 내용은 [그리기 개체 개요](drawing-objects-overview.md)를 참조하세요.  
  
#### <a name="drawing-content-at-the-visual-layer"></a>시각적 계층에서 그리기 콘텐츠  
 절대 직접 인스턴스화하지를 <xref:System.Windows.Media.DrawingContext>; 얻을 수 있습니다, 있지만 특정 메서드에서 그리기 컨텍스트 등 <xref:System.Windows.Media.DrawingGroup.Open%2A?displayProperty=nameWithType> 고 <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A?displayProperty=nameWithType>입니다. 다음 예제에서는 검색 된 <xref:System.Windows.Media.DrawingContext> 에서 <xref:System.Windows.Media.DrawingVisual> 사각형 그리기를 사용 하 여 합니다.  
  
 [!code-csharp[drawingvisualsample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#101)]
 [!code-vb[drawingvisualsample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#101)]  
  
#### <a name="enumerating-drawing-content-at-the-visual-layer"></a>시각적 계층에서 그리기 콘텐츠 열거  
 @No__t-0 개체는 다른 용도 외에도-1 @no__t의 콘텐츠를 열거 하는 개체 모델을 제공 합니다.  
  
> [!NOTE]
> 시각적 개체의 콘텐츠를 열거 하는 경우 렌더링 데이터의 기본 표현이 벡터 그래픽 명령 목록으로 아니라 <xref:System.Windows.Media.Drawing> 개체를 검색 합니다.  
  
 다음 예제에서는 <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> 메서드를 사용 하 여 <xref:System.Windows.Media.Visual>의 <xref:System.Windows.Media.DrawingGroup> 값을 검색 하 고이를 열거 합니다.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
<a name="how_visual_objects_are_used_to_build_controls"></a>   
## <a name="how-visual-objects-are-used-to-build-controls"></a>컨트롤 빌드에 시각적 개체를 사용하는 방법  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 많은 개체는 다른 시각적 개체로 구성됩니다. 즉, 다양한 하위 개체 계층 구조를 포함할 수 있습니다. 컨트롤과 같은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 많은 사용자 인터페이스 요소는 여러 다른 형식의 렌더링 요소를 나타내는 다양한 시각적 개체로 구성됩니다. 예를 들어 <xref:System.Windows.Controls.Button> 컨트롤에는 <xref:Microsoft.Windows.Themes.ClassicBorderDecorator>, <xref:System.Windows.Controls.ContentPresenter> 및 <xref:System.Windows.Controls.TextBlock>을 비롯 한 여러 개체가 포함 될 수 있습니다.  
  
 다음 코드에서는 태그에 정의 된 <xref:System.Windows.Controls.Button> 컨트롤을 보여 줍니다.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet1)]  
  
 기본 <xref:System.Windows.Controls.Button> 컨트롤을 구성 하는 시각적 개체를 열거 하는 경우 아래에 나와 있는 시각적 개체의 계층 구조를 찾을 수 있습니다.  
  
 ![시각적 트리 계층 구조의 다이어그램](./media/wpf-graphics-rendering-overview/visual-object-diagram.gif) 
  
 @No__t-0 컨트롤은 <xref:System.Windows.Controls.ContentPresenter> 요소를 포함 하는 <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> 요소를 포함 합니다. @No__t-0 요소는 <xref:System.Windows.Controls.Button>의 테두리와 배경색을 그리는 역할을 합니다. @No__t-0 요소는-1 @no__t의 내용을 표시 합니다. 이 경우 텍스트를 표시 하기 때문에 <xref:System.Windows.Controls.ContentPresenter> 요소는 <xref:System.Windows.Controls.TextBlock> 요소를 포함 합니다. @No__t-0 컨트롤은 @no__t를 사용 함을 의미 합니다.-1은 @no__t 2 또는 기 하 도형 (예: <xref:System.Windows.Media.EllipseGeometry>)과 같은 다른 요소로 콘텐츠를 나타낼 수 있음을 의미 합니다.  
  
### <a name="control-templates"></a>컨트롤 템플릿  
 컨트롤을 컨트롤의 계층으로 확장 하는 것에 대 한 핵심은 <xref:System.Windows.Controls.ControlTemplate>입니다. 컨트롤 템플릿은 컨트롤에 대한 기본 시각적 개체 계층 구조를 지정합니다. 컨트롤을 명시적으로 참조할 때는 해당 시각적 개체 계층 구조를 암시적으로 참조하게 됩니다. 컨트롤 템플릿에 대한 기본값을 재정의하여 컨트롤의 사용자 지정된 시각적 모양을 만들 수 있습니다. 예를 들어 단색 값 대신 선형 그라데이션 색 값을 사용 하도록 <xref:System.Windows.Controls.Button> 컨트롤의 배경색 값을 수정할 수 있습니다. 자세한 내용은 [단추 스타일 및 템플릿](../controls/button-styles-and-templates.md)을 참조하세요.  
  
 @No__t-0 컨트롤과 같은 사용자 인터페이스 요소는 컨트롤의 전체 렌더링 정의를 설명 하는 몇 가지 벡터 그래픽 명령 목록을 포함 합니다. 다음 코드에서는 태그에 정의 된 <xref:System.Windows.Controls.Button> 컨트롤을 보여 줍니다.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet2)]  
  
 @No__t-0 컨트롤을 구성 하는 시각적 개체 및 벡터 그래픽 명령 목록을 열거 하는 경우 아래에 나와 있는 개체의 계층 구조를 찾을 수 있습니다.  
  
 ![시각적 트리 및 렌더링 데이터의 다이어그램](./media/wpf-graphics-rendering-overview/visual-tree-rendering-data.png)  
  
 @No__t-0 컨트롤은 <xref:System.Windows.Controls.ContentPresenter> 요소를 포함 하는 <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> 요소를 포함 합니다. @No__t-0 요소는 단추의 테두리와 배경을 구성 하는 모든 불연속 그래픽 요소를 그리는 작업을 담당 합니다. @No__t-0 요소는-1 @no__t의 내용을 표시 합니다. 이 경우 이미지를 표시 하기 때문에 <xref:System.Windows.Controls.ContentPresenter> 요소는 <xref:System.Windows.Controls.Image> 요소를 포함 합니다.  
  
 시각적 개체 및 벡터 그래픽 명령 목록의 계층 구조에 대해 다음과 같은 사항을 명심해야 합니다.  
  
- 계층 구조의 순서는 그리기 정보의 렌더링 순서를 나타냅니다. 루트 시각적 요소에서 자식 요소는 왼쪽에서 오른쪽, 위쪽에서 아래쪽으로 트래버스됩니다. 요소에 시각적 자식 요소가 있으면 요소의 형제 요소보다 먼저 트래버스됩니다.  
  
- 계층 구조에서 리프가 아닌 노드 요소 (예: <xref:System.Windows.Controls.ContentPresenter>)는 자식 요소를 포함 하는 데 사용 되며 명령 목록을 포함 하지 않습니다.  
  
- 시각적 요소가 벡터 그래픽 명령 목록과 시각적 자식 개체를 모두 포함하는 경우 시각적 자식 개체의 그리기 작업 전에 시각적 부모 요소의 명령 목록이 먼저 렌더링됩니다.  
  
- 벡터 그래픽 명령 목록에 있는 항목은 왼쪽에서 오른쪽으로 렌더링됩니다.  
  
<a name="visual_tree"></a>   
## <a name="visual-tree"></a>표시 트리  
 시각적 트리에는 애플리케이션의 사용자 인터페이스에서 사용되는 모든 시각적 요소가 포함됩니다. 시각적 요소에는 지속형 그리기 정보가 포함되어 있으므로 시각적 트리를 디스플레이 디바이스에 대한 출력을 작성하는 데 필요한 모든 렌더링 정보를 포함하는 장면 그래프로 간주할 수 있습니다. 이 트리는 코드 또는 태그를 통해 애플리케이션에서 직접 만든 모든 시각적 요소가 누적된 것입니다. 또한 시각적 트리는 컨트롤 및 데이터 개체와 같은 요소의 템플릿 확장을 통해 만들어진 모든 시각적 요소도 포함합니다.  
  
 다음 코드에서는 태그에 정의 된 <xref:System.Windows.Controls.StackPanel> 요소를 보여 줍니다.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet3)]  
  
 태그 예제에서 <xref:System.Windows.Controls.StackPanel> 요소를 구성 하는 시각적 개체를 열거 하는 경우 아래에 표시 된 시각적 개체의 계층 구조를 찾을 수 있습니다.  
  
 ![시각적 트리 계층 구조의 다이어그램](./media/wpf-graphics-rendering-overview/visual-tree-hierarchy.gif)  
  
### <a name="rendering-order"></a>렌더링 순서  
 시각적 트리는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시각적 및 그리기 개체의 렌더링 순서를 결정합니다. 트래버스 순서는 시각적 트리의 최상위 노드를 나타내는 루트 시각적 개체에서 시작됩니다. 그런 후에 루트 시각적 개체의 자식이 왼쪽에서 오른쪽으로 트래버스됩니다. 시각적 개체에 자식이 있으면 해당 자식은 시각적 요소의 형제보다 먼저 트래버스됩니다. 즉, 시각적 자식 개체의 콘텐츠는 시각적 개체 자체의 콘텐츠보다 먼저 렌더링됩니다.  
  
 ![시각적 트리 렌더링 순서의 다이어그램](./media/wpf-graphics-rendering-overview/visual-tree-rendering-order.gif) 
  
### <a name="root-visual"></a>루트 시각적 개체  
 **루트 시각적 개체**는 시각적 트리 계층의 최상위 요소입니다. 대부분의 응용 프로그램에서 루트 시각적 개체의 기본 클래스는 <xref:System.Windows.Window> 또는 <xref:System.Windows.Navigation.NavigationWindow>입니다. 그러나 Win32 애플리케이션에서 시각적 개체를 호스트한다면 루트 시각적 개체가 Win32 창에서 호스트한 최상위 시각적 개체가 될 것입니다. 자세한 내용은 [자습서: Win32 응용 프로그램에서 시각적 개체 호스팅 @ no__t-0  
  
### <a name="relationship-to-the-logical-tree"></a>논리적 트리와의 관계  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 논리적 트리는 런타임의 애플리케이션 요소를 나타냅니다. 이 트리를 직접 조작하지는 않지만 애플리케이션의 이 보기는 속성 상속 및 이벤트 라우팅을 이해하는 데 유용합니다. 시각적 트리와 달리 논리적 트리는 <xref:System.Windows.Documents.ListItem>과 같은 비시각적 데이터 개체를 나타낼 수 있습니다. 대부분의 경우 논리적 트리는 애플리케이션의 태그 정의에 매우 밀접하게 매핑됩니다. 다음 코드에서는 태그에 정의 된 <xref:System.Windows.Controls.DockPanel> 요소를 보여 줍니다.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet5)]  
  
 태그 예제에서 <xref:System.Windows.Controls.DockPanel> 요소를 구성 하는 논리 개체를 열거 하는 경우 아래에 나와 있는 논리 개체의 계층 구조를 찾을 수 있습니다.  
  
 ![트리 다이어그램](./media/tree1-wcp.gif "Tree1_wcp")  
논리적 트리 다이어그램  
  
 시각적 트리와 논리적 트리 둘 다 현재의 애플리케이션 요소 집합과 동기화되므로 요소의 모든 추가, 삭제 또는 수정이 반영됩니다. 그러나 트리는 애플리케이션의 여러 다른 보기를 나타냅니다. 시각적 트리와 달리 논리적 트리는 컨트롤의 <xref:System.Windows.Controls.ContentPresenter> 요소를 확장 하지 않습니다. 즉, 동일한 집합에 대한 논리적 트리와 시각적 트리 간에 직접적인 일대일 대응은 없습니다. 실제로 **LogicalTreeHelper** 개체의 @no__t 메서드를 호출 하 고 **VisualTreeHelper** 개체의 <xref:System.Windows.Media.VisualTreeHelper.GetChild%2A> 메서드를 매개 변수와 동일한 요소를 사용 하 여 호출 하면 결과가 다릅니다.  
  
 논리적 트리에 대한 자세한 내용은 [WPF의 트리](../advanced/trees-in-wpf.md)를 참조하세요.  
  
### <a name="viewing-the-visual-tree-with-xamlpad"></a>XamlPad에서 시각적 트리 보기  
 @No__t-0 도구인 XamlPad는 현재 정의 된 XAML 콘텐츠에 해당 하는 시각적 트리를 보고 탐색 하는 옵션을 제공 합니다. 메뉴 모음에서 **시각적 트리 표시** 단추를 클릭하여 시각적 트리를 표시합니다. 다음은 XamlPad의 **시각적 트리 탐색기** 패널에서 XAML 콘텐츠를 시각적 트리 노드로 확장 하는 방법을 보여 줍니다.  
  
 ![XamlPad의 시각적 트리 탐색기 패널](./media/wpf-graphics-rendering-overview/visual-tree-explorer.png)  

 XamlPad의 **시각적 트리 탐색기** 패널에 <xref:System.Windows.Controls.Label>, <xref:System.Windows.Controls.TextBox> 및 @no__t 컨트롤이 각각 별도의 시각적 개체 계층 구조를 표시 하는 방법을 확인 합니다. 이는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤에는 해당 컨트롤의 시각적 트리를 포함 하는 @no__t 1이 있기 때문입니다. 컨트롤을 명시적으로 참조할 때는 해당 시각적 개체 계층 구조를 암시적으로 참조하게 됩니다.  
  
### <a name="profiling-visual-performance"></a>시각적 성능 프로파일링  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 애플리케이션의 런타임 동작을 분석할 수 있고 적용할 수 있는 성능 최적화 형식을 판별하는 성능 프로파일링 도구 제품군을 제공합니다. Visual Profiler 도구는 애플리케이션의 시각적 트리에 직접 매핑하여 성능 데이터의 다양한 그래픽 보기를 제공합니다. 이 스크린 샷에서 Visual Profiler의 **CPU 사용량** 섹션에서는 렌더링 및 레이아웃과 같은 개체의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 서비스 사용을 정확히 분석할 수 있습니다.  
  
 ![시각적 프로파일러 표시 출력](./media/wpfperf-visualprofiler-04.png "WPFPerf_VisualProfiler_04")  
Visual Profiler 표시 출력  
  
<a name="visual_rendering_behavior"></a>   
## <a name="visual-rendering-behavior"></a>시각적 개체 렌더링 동작  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 시각적 개체의 렌더링 동작에 영향을 주는 여러 기능이 도입되었습니다. 여기에는 유지 모드 그래픽, 벡터 그래픽 및 디바이스 독립적 그래픽이 포함됩니다.  
  
### <a name="retained-mode-graphics"></a>유지 모드 그래픽  
 시각적 개체의 역할을 이해하기 위해서는 **직접 실행 모드**와 **유지 모드** 그래픽 시스템 간 차이를 이해하는 것이 중요합니다. GDI 또는 GDI+를 기준으로 하는 표준 Win32 애플리케이션은 직접 실행 모드 그래픽 시스템을 사용합니다. 즉, 이 애플리케이션은 창의 크기 조정이나 개체의 시각적 모양 변경과 같은 동작으로 인해 무효화되는 클라이언트 영역의 부분을 다시 그립니다.  
  
 ![Win32 렌더링 시퀀스의 다이어그램](./media/wpf-graphics-rendering-overview/win32-rendering-squence.png)  
  
 반면, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 유지 모드 시스템을 사용합니다. 즉, 시각적 모양을 갖는 애플리케이션 개체는 serialize된 그리기 데이터 집합을 정의합니다. 그리기 데이터가 정의되면 시스템은 애플리케이션 개체 렌더링을 위한 모든 다시 그리기 요청에 응답합니다. 런타임에도 애플리케이션 개체를 수정하거나 만들 수 있으며 그리기 요청에 응답하기 위해 해당 시스템에 의존할 수 있습니다. 유지 모드 그래픽 시스템의 강점은 그리기 정보가 항상 애플리케이션에서 serialize된 상태로 지속되지만 렌더링 책임은 시스템에 남아 있다는 것입니다. 다음 다이어그램에서는 애플리케이션이 그리기 요청에 응답하기 위해 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에 의존하는 방식을 보여 줍니다.  
  
 ![WPF 렌더링 시퀀스의 다이어그램](./media/wpf-graphics-rendering-overview/wpf-rendering-sequence.png)  

#### <a name="intelligent-redrawing"></a>지능형 다시 그리기  
 유지 모드 그래픽을 사용할 때는 가장 큰 장점 중 하나는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]가 애플리케이션에서 다시 그려야 하는 항목을 효율적으로 최적화할 수 있다는 것입니다. 다양한 수준의 불투명도를 갖는 복잡한 장면이 있더라도 다시 그리기를 최적화하기 위해 특수한 용도의 코드를 작성할 필요가 없습니다. 이러한 특성을 업데이트 영역의 다시 그리기 작업량을 최소화하여 적은 노력으로 애플리케이션을 최적화할 수 있는 Win32 프로그래밍 작업과 비교해 보세요. Win32 애플리케이션의 다시 그리기 최적화와 관련된 복잡성 형식의 예제를 보려면 [업데이트 영역의 다시 그리기](/windows/desktop/gdi/redrawing-in-the-update-region)를 참조하세요.  
  
### <a name="vector-graphics"></a>벡터 그래픽  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 **벡터 그래픽**을 해당 렌더링 데이터 형식으로 사용합니다. SVG(Scalable Vector Graphics), Windows 메타파일(.wmf) 및 트루타입 글꼴을 포함하는 벡터 그래픽은 렌더링 데이터를 저장하고 그래픽 기본형을 사용하여 이미지를 다시 만드는 방법을 설명하는 명령 목록으로 전송합니다. 예를 들어 트루타입 글꼴은 픽셀 배열이 아니라, 선, 곡선 및 명령 집합을 설명하는 윤곽선 글꼴입니다. 벡터 그래픽의 주요 이점 중 하나는 어떤 크기 및 해상도로도 조정이 가능하다는 것입니다.  
  
 벡터 그래픽과 달리, 비트맵 그래픽은 렌더링 데이터를 특정 해상도로 미리 렌더링된 이미지의 픽셀 단위 표현으로 저장합니다. 비트맵 그래픽과 벡터 그래픽 형식 간의 주요 차이점 중 하나에 원본 소스 이미지에 대한 충실도입니다. 예를 들어 소스 이미지의 크기를 수정한 경우 비트맵 그래픽 시스템은 이미지를 늘이지만 벡터 그래픽 시스템은 이미지의 충실도를 보존하면서 이미지 배율을 조정합니다.  
  
 다음 그림에서는 300%만큼 크기가 조정된 소스 이미지를 보여 줍니다. 소스 이미지가 벡터 그래픽 이미지처럼 배율이 조정되지 않고 비트맵 그래픽 이미지처럼 확장됩니다.  
  
 ![래스터 그래픽과 벡터 그래프의 차이](./media/wpf-graphics-rendering-overview/raster-vector-differences.png)  
  
 다음 태그는 정의 된 두 개의 @no__t 요소를 보여 줍니다. 두 번째 요소는 <xref:System.Windows.Media.ScaleTransform>을 사용 하 여 첫 번째 요소의 그리기 지침을 300%로 조정 합니다. @No__t-0 요소의 그리기 명령은 변경 되지 않고 그대로 유지 됩니다.  
  
 [!code-xaml[VectorGraphicsSnippets#VectorGraphicsSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VectorGraphicsSnippets/CS/PageOne.xaml#vectorgraphicssnippet1)]  
  
### <a name="about-resolution-and-device-independent-graphics"></a>해상도 및 디바이스 독립적인 그래픽 정보  
 화면에서 텍스트 및 그래픽의 크기를 결정하는 두 시스템 요소는 바로 해상도와 DPI입니다. 해상도는 화면에 표시되는 픽셀 수를 설명합니다. 해상도가 더 높을수록 픽셀은 더 작아지므로 그래픽 및 텍스트가 더 작게 표시됩니다. 1024 x 768로 설정된 모니터에 표시되는 그래픽은 해상도를 1600 x 1200으로 변경하면 훨씬 더 작게 나타납니다.  
  
 다른 시스템 설정인 DPI는 화면 인치 크기(픽셀)를 설명합니다. 대부분의 Windows 시스템에는 DPI 96가 있습니다. 즉, 화면 인치가 96 픽셀 임을 의미 합니다. DPI 설정을 늘리면 화면 인치가 더 커지고 DPI를 줄이면 화면 인치가 더 작아집니다. 즉, 화면 인치가 실제 인치와 같지 않음을 의미합니다. 대부분의 시스템에서 같지 않을 수 있습니다. DPI를 늘리면 화면 인치 크기도 늘어났을 것이므로 DPI 인식 그래픽 및 텍스트가 더 커집니다. 특히 고해상도에서 DPI를 늘리면 텍스트 읽기가 훨씬 더 쉬워집니다.  
  
 모든 애플리케이션이 DPI를 인식하는 것은 아닙니다. 일부에서는 하드웨어 픽셀을 측정의 기본 단위로 사용합니다. 시스템 DPI를 변경해도 이러한 애플리케이션에는 영향이 없습니다. 많은 다른 애플리케이션에서 DPI 인식 단위를 사용하여 글꼴 크기를 설명하지만 다른 요소를 설명할 때는 픽셀을 사용합니다. 이러한 애플리케이션의 텍스트는 시스템의 DPI 설정에 따라 확장되지만 UI는 그렇지 않으므로 DPI를 너무 작거나 너무 크게 지정하면 이러한 애플리케이션에서 레이아웃 문제가 발생할 수 있습니다. 이 문제는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 사용하여 개발된 애플리케이션에서는 해결되었습니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 하드웨어 픽셀이 아닌 디바이스 독립적 픽셀을 기본 측정 단위로 사용하여 자동 크기 조정을 지원합니다. 그래픽 및 텍스트는 애플리케이션 개발자의 추가 작업 없이 적절히 확장됩니다. 다음 그림에는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 텍스트와 그래픽이 다른 DPI 설정으로 표시되는 방식의 예가 나와 있습니다.  
  
 ![여러 DPI 설정의 그래픽과 텍스트](./media/graphicsmm-dpi-setting-examples.png "graphicsmm_dpi_setting_examples")  
서로 다른 DPI 설정에서의 그래픽과 텍스트  
  
<a name="visualtreehelper_class"></a>   
## <a name="visualtreehelper-class"></a>VisualTreeHelper 클래스  
 @No__t-0 클래스는 시각적 개체 수준에서 프로그래밍 하는 데 필요한 하위 수준 기능을 제공 하는 정적 도우미 클래스입니다 .이 클래스는 고성능 사용자 지정 컨트롤 개발과 같은 매우 구체적인 시나리오에서 유용 합니다. 대부분의 경우 <xref:System.Windows.Controls.Canvas> 및 <xref:System.Windows.Controls.TextBlock>와 같은 더 높은 수준의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 프레임 워크 개체를 사용 하면 유연성과 사용 편의성을 높일 수 있습니다.  
  
### <a name="hit-testing"></a>적중 테스트  
 @No__t-0 클래스는 기본 적중 테스트 지원이 사용자의 요구를 충족 하지 않는 경우 시각적 개체에 대 한 적중 테스트를 위한 메서드를 제공 합니다. @No__t-1 클래스에서 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 메서드를 사용 하 여 geometry 또는 point 좌표 값이 컨트롤이 나 그래픽 요소와 같은 지정 된 개체의 경계 내에 있는지 여부를 확인할 수 있습니다. 예를 들어 적중 테스트를 사용하여 개체의 경계 사각형 안을 마우스로 클릭할 때 원 기하 도형 내부를 클릭한 것인지 여부를 결정할 수 있습니다. 또한 적중 테스트의 기본 구현을 재정의하여 사용자 고유의 적중 테스트 계산을 사용자 지정하도록 선택할 수도 있습니다.  
  
 적중 테스트에 대한 자세한 내용은 [시각적 계층에서 테스트 적중](hit-testing-in-the-visual-layer.md)를 참조하세요.  
  
### <a name="enumerating-the-visual-tree"></a>시각적 트리 열거  
 @No__t-0 클래스는 시각적 트리의 멤버를 열거 하는 기능을 제공 합니다. 부모를 검색 하려면 <xref:System.Windows.Media.VisualTreeHelper.GetParent%2A> 메서드를 호출 합니다. 시각적 개체의 자식 또는 직계 하위 항목을 검색 하려면 <xref:System.Windows.Media.VisualTreeHelper.GetChild%2A> 메서드를 호출 합니다. 이 메서드는 지정 된 인덱스에서 부모의 자식 <xref:System.Windows.Media.Visual>을 반환 합니다.  
  
 다음 예제에서는 시각적 개체의 모든 하위 항목을 열거하는 방법을 보여 줍니다. 이 방법은 시각적 개체 계층 구조의 모든 렌더링 정보를 serialize하려는 경우에 사용할 수 있습니다.  
  
 [!code-csharp[VisualsOverview#101](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#101)]
 [!code-vb[VisualsOverview#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#101)]  
  
 대부분의 경우에서 논리적 트리는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애플리케이션의 요소를 좀 더 유용하게 나타낸 것입니다. 논리적 트리를 직접 수정하지는 않지만 애플리케이션의 이 보기는 속성 상속 및 이벤트 라우팅을 이해하는 데 유용합니다. 시각적 트리와 달리 논리적 트리는 <xref:System.Windows.Documents.ListItem>과 같은 비시각적 데이터 개체를 나타낼 수 있습니다. 논리적 트리에 대한 자세한 내용은 [WPF의 트리](../advanced/trees-in-wpf.md)를 참조하세요.  
  
 @No__t-0 클래스는 시각적 개체의 경계 사각형을 반환 하는 메서드를 제공 합니다. @No__t-0을 호출 하 여 시각적 개체의 경계 사각형을 반환할 수 있습니다. @No__t-0을 호출 하 여 시각적 개체 자체를 포함 하 여 시각적 개체의 모든 하위 항목에 대 한 경계 사각형을 반환할 수 있습니다. 다음 코드에서는 시각적 개체 및 모든 하위 개체의 경계 사각형을 계산하는 방법을 보여 줍니다.  
  
 [!code-csharp[VisualsOverview#102](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#102)]
 [!code-vb[VisualsOverview#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#102)]  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.Media.VisualTreeHelper>
- <xref:System.Windows.Media.DrawingVisual>
- [2차원 그래픽 및 이미징](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [시각적 계층에서 적중 테스트](hit-testing-in-the-visual-layer.md)
- [DrawingVisual 개체 사용](using-drawingvisual-objects.md)
- [자습서: Win32 응용 프로그램에서 시각적 개체 호스팅 @ no__t-0
- [WPF 애플리케이션 성능 최적화](../advanced/optimizing-wpf-application-performance.md)
