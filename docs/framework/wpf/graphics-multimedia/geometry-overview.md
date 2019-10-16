---
title: Geometry 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- geometry classes [WPF]
- graphics [WPF], geometry classes
ms.assetid: 9fba8934-98b7-4af6-82f6-f4ef887f963a
ms.openlocfilehash: 5545e89f744c3874840a773556e0670abc0a46a9
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348064"
---
# <a name="geometry-overview"></a>Geometry 개요
이 개요에서는 사용 하는 방법을 설명 합니다 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Media.Geometry> 도형을 설명 하는 클래스입니다. 이 항목의 차이점도 비교해 서 설명 <xref:System.Windows.Media.Geometry> 개체 및 <xref:System.Windows.Shapes.Shape> 요소입니다.  

<a name="wcpsdk_graphics_geometry_introduction"></a>   
## <a name="what-is-a-geometry"></a>기하 도형이란?  
 합니다 <xref:System.Windows.Media.Geometry> 클래스와 같은에서 파생 되는 클래스 <xref:System.Windows.Media.EllipseGeometry>를 <xref:System.Windows.Media.PathGeometry>, 및 <xref:System.Windows.Media.CombinedGeometry>, 2 차원 도형의 기 하 도형을 설명 하는 데 사용 합니다. 이러한 기하학적 설명은 화면에 그릴 도형 정의 또는 적중 테스트 및 클립 영역을 정의와 같은 다양한 용도로 사용됩니다. 애니메이션 경로를 정의하는 데도 기하 도형을 사용할 수 있습니다.  
  
 <xref:System.Windows.Media.Geometry> 개체는 사각형 및 원과 또는 복합 기 하 도형 개체를 두 개 이상에서 만든 같은 간단할 수 있습니다.  더 복잡 한 기 하 도형을 사용 하 여 만들 수 있습니다 합니다 <xref:System.Windows.Media.PathGeometry> 및 <xref:System.Windows.Media.StreamGeometry> 호와 곡선을 설명 하는 데 사용 하는 클래스입니다.  
  
 때문에 <xref:System.Windows.Media.Geometry> 유형의 <xref:System.Windows.Freezable>, <xref:System.Windows.Media.Geometry> 몇 가지 특별 한 기능을 제공 하는 개체:로 선언할 수 있습니다 [리소스](../advanced/xaml-resources.md)읽기 전용 복제 성능 향상을 위해 여러 개체 간에 공유 하 고 스레드로부터 안전한 수 있습니다. 제공 하는 다른 기능에 대 한 자세한 <xref:System.Windows.Freezable> 개체를 참조 합니다 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)합니다.  
  
<a name="wcpsdk_graphics_geometry_geometryandshapes"></a>   
## <a name="geometries-vs-shapes"></a>기하 도형 및 도형  
 합니다 <xref:System.Windows.Media.Geometry> 하 고 <xref:System.Windows.Shapes.Shape> 클래스에서 비슷해 보이지만 2 차원 도형을 설명 둘 (비교 <xref:System.Windows.Media.EllipseGeometry> 및 <xref:System.Windows.Shapes.Ellipse> 예를 들어), 중요 한 차이점이 있지만.  
  
 <xref:System.Windows.Media.Geometry> 클래스에서 상속 합니다 <xref:System.Windows.Freezable> 동안 클래스는 <xref:System.Windows.Shapes.Shape> 클래스에서 상속 <xref:System.Windows.FrameworkElement>합니다. 요소 이므로 <xref:System.Windows.Shapes.Shape> 자신을 렌더링할 개체를 레이아웃 시스템에 참여 하는 동안 <xref:System.Windows.Media.Geometry> 개체 수 없습니다.  
  
 하지만 <xref:System.Windows.Shapes.Shape> 개체 보다 더 쉽게 사용할 수 <xref:System.Windows.Media.Geometry> 개체를 <xref:System.Windows.Media.Geometry> 개체는 융통성이 더 뛰어납니다. 하는 동안를 <xref:System.Windows.Shapes.Shape> 개체는 2 차원 그래픽을 렌더링 하는 데는 <xref:System.Windows.Media.Geometry> 2 차원 그래픽에 대 한 기하학적 영역을 정의 클리핑에 대 한 영역을 정의 또는 적중 횟수 테스트에 대 한 영역을 예를 들어 정의 개체를 사용할 수 있습니다.  
  
### <a name="the-path-shape"></a>경로 도형  
 하나의 <xref:System.Windows.Shapes.Shape>는 <xref:System.Windows.Shapes.Path> 클래스를 사용 하 여 실제로 <xref:System.Windows.Media.Geometry> 해당 콘텐츠를 설명 합니다. 설정 하 여는 <xref:System.Windows.Shapes.Path.Data%2A> 의 속성을 <xref:System.Windows.Shapes.Path> 사용 하 여를 <xref:System.Windows.Media.Geometry> 설정 해당 <xref:System.Windows.Shapes.Shape.Fill%2A> 및 <xref:System.Windows.Shapes.Shape.Stroke%2A> 렌더링할 수 속성을를 <xref:System.Windows.Media.Geometry>.  
  
<a name="commonproperties"></a>   
## <a name="common-properties-that-take-a-geometry"></a>Geometry를 사용하는 공용 속성  
 이전 섹션에서는 Geometry 개체를 도형 그리기, 애니메이션 효과 적용, 클리핑 등의 다양한 용도로 다른 개체와 함께 사용할 수 있다는 사실을 설명했습니다. 다음 표에서 속성을 가진 여러 클래스를 <xref:System.Windows.Media.Geometry> 개체입니다.  
  
|형식|속성|  
|----------|--------------|  
|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.PathGeometry%2A>|  
|<xref:System.Windows.Media.DrawingGroup>|<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>|  
|<xref:System.Windows.Media.GeometryDrawing>|<xref:System.Windows.Media.GeometryDrawing.Geometry%2A>|  
|<xref:System.Windows.Shapes.Path>|<xref:System.Windows.Shapes.Path.Data%2A>|  
|<xref:System.Windows.UIElement>|<xref:System.Windows.UIElement.Clip%2A>|  
  
<a name="wcpsdk_graphics_geometry_geometrytypes"></a>   
## <a name="simple-geometry-types"></a>단순 기하 도형 형식  
 모든 기 하 도형에 대 한 기본 클래스는 추상 클래스 <xref:System.Windows.Media.Geometry>합니다.  파생 되는 클래스는 <xref:System.Windows.Media.Geometry> 클래스 약 세 가지 범주로 그룹화 할 수 있습니다: 단순 기 하 도형, 경로 기 하 도형 및 복합 기 하 도형입니다.  
  
 단순 기 하 도형 클래스를 포함 <xref:System.Windows.Media.LineGeometry>, <xref:System.Windows.Media.RectangleGeometry>, 및 <xref:System.Windows.Media.EllipseGeometry> 줄, 사각형, 원 등 기본 도형을 만드는 데 사용 되 고 있습니다.  
  
- <xref:System.Windows.Media.LineGeometry> 줄 고 끝점의 시작점을 지정 하 여 정의 됩니다.  
  
- A <xref:System.Windows.Media.RectangleGeometry> 으로 정의 됩니다는 <xref:System.Windows.Rect> 상대 위치 및 해당 높이 너비를 지정 하는 구조입니다. 모퉁이가 둥근된 사각형을 설정 하 여 만들 수 있습니다 합니다 <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> 고 <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> 속성입니다.  
  
- <xref:System.Windows.Media.EllipseGeometry> 중심점, x 반지름 및 y 반지름으로 정의 됩니다.  다음 예제에서는 렌더링 및 클리핑을 위한 단순 기하 도형을 만드는 방법을 보여 줍니다.  
  
 더 복잡 한 도형을 뿐만 아니라 이러한 동일한 셰이프를 만들 수 있습니다를 <xref:System.Windows.Media.PathGeometry> 또는 함께 기 하 도형 개체는 있지만 이러한 클래스를 결합 하 여 이러한 기본 도형을 생성 하는 것에 대 한 간단한 수단을 제공 합니다.  
  
 다음 예제를 만들고 렌더링 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.LineGeometry>합니다.  이전에 설명한 것 처럼를 <xref:System.Windows.Media.Geometry> 개체에서 자신을 그릴 수 없는 <xref:System.Windows.Shapes.Path> 모양 선을 렌더링 합니다.  선에 영역이 없는, 때문에 설정를 <xref:System.Windows.Shapes.Shape.Fill%2A> 의 속성을 <xref:System.Windows.Shapes.Path> 해도 아무런 효과가 없습니다 대신만 <xref:System.Windows.Shapes.Shape.Stroke%2A> 및 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 속성을 지정 합니다. 다음 그림에서는 예제의 출력을 보여 줍니다.  
  
 ![LineGeometry](./media/graphicsmm-line.gif "graphicsmm_line")  
(10,20)부터 (100,130)까지 그린 LineGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMLineGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmlinegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmlinegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmlinegeometryexample)]  
  
 다음 예제를 만들고 렌더링 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.EllipseGeometry>합니다.  예제에서는 합니다 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 의 합니다 <xref:System.Windows.Media.EllipseGeometry> 지점으로 설정 됩니다 `50,50` x 반지름 및 y 반지름 둘 다로 설정 되 고 `50`, 지름이 100 인 원을 만듭니다.  이 경우에 Path 요소의 Fill 속성에 값을 할당 하 여 타원의 내부 그려집니다 <xref:System.Windows.Media.Brushes.Gold%2A>합니다. 다음 그림에서는 예제의 출력을 보여 줍니다.  
  
 ![EllipseGeometry](./media/graphicsmm-ellipse.gif "graphicsmm_ellipse")  
(50,50)에 그린 EllipseGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMEllipseGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmellipsegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMEllipseGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmellipsegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMEllipseGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmellipsegeometryexample)]  
  
 다음 예제를 만들고 렌더링 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.RectangleGeometry>합니다.  정의 된 위치와 사각형의 크기는 <xref:System.Windows.Rect> 구조입니다. 위치는 `50,50`이고 높이 및 너비 둘 다 `25`이므로 정사각형을 만듭니다. 다음 그림에서는 예제의 출력을 보여 줍니다.  
  
 ![RectangleGeometry](./media/graphicsmm-rectangle.gif "graphicsmm_rectangle")  
50,50에 그린 RectangleGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmrectanglegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmrectanglegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmrectanglegeometryexample)]  
  
 다음 예제에서는 사용 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.EllipseGeometry> 이미지의 클립 영역으로 합니다.  <xref:System.Windows.Controls.Image> 으로 정의 된 개체를 <xref:System.Windows.FrameworkElement.Width%2A> 200 및 <xref:System.Windows.FrameworkElement.Height%2A> 150입니다.  <xref:System.Windows.Media.EllipseGeometry> 사용 하 여는 <xref:System.Windows.Media.EllipseGeometry.RadiusX%2A> 100의 값을 <xref:System.Windows.Media.EllipseGeometry.RadiusY%2A> 75 값 및 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 100,75의 값으로 설정 됩니다는 <xref:System.Windows.UIElement.Clip%2A> 이미지의 속성입니다.  타원 영역 내의 이미지 부분만 표시됩니다. 다음 그림에서는 예제의 출력을 보여 줍니다.  
  
 ![이미지와 없는 클리핑](./media/graphicsmm-clipexample.png "graphicsmm_clipexample")  
Image 컨트롤 클리핑에 사용되는 EllipseGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMImageClipGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmimageclipgeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMImageClipGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmimageclipgeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMImageClipGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmimageclipgeometryexample)]  
  
<a name="wcpsdk_graphics_geometry_pathgeometry"></a>   
## <a name="path-geometries"></a>경로 기하 도형  
 합니다 <xref:System.Windows.Media.PathGeometry> 클래스 및 간단한 동등한은 <xref:System.Windows.Media.StreamGeometry> 클래스, 원호, 곡선 및 선 구성 된 여러 복잡 한 그림을 설명 하는 수단을 제공 합니다.  
  
 핵심을 <xref:System.Windows.Media.PathGeometry> 컬렉션인 <xref:System.Windows.Media.PathFigure> 그렇게 각 그림의 개별 도형을 설명 하기 때문에 명명 된 개체는 <xref:System.Windows.Media.PathGeometry>합니다. 각 <xref:System.Windows.Media.PathFigure> 자체는 하나 이상의 구성 <xref:System.Windows.Media.PathSegment> 그림의 세그먼트를 설명 하는 각 개체입니다.  
  
 세그먼트 형식은 다양합니다.  
  
|세그먼트 형식|설명|예제|  
|------------------|-----------------|-------------|  
|<xref:System.Windows.Media.ArcSegment>|두 점 사이에 타원형 호를 만듭니다.|[타원형 원호 만들기](how-to-create-an-elliptical-arc.md).|  
|<xref:System.Windows.Media.BezierSegment>|두 점 사이에 입방형 3차원 곡선을 만듭니다.|[입방형 3차원 곡선 만들기](how-to-create-a-cubic-bezier-curve.md).|  
|<xref:System.Windows.Media.LineSegment>|두 점 사이에 선을 만듭니다.|[PathGeometry에 LineSegment 만들기](how-to-create-a-linesegment-in-a-pathgeometry.md)|  
|<xref:System.Windows.Media.PolyBezierSegment>|일련의 입방형 3차원 곡선을 만듭니다.|참조 된 <xref:System.Windows.Media.PolyBezierSegment> 유형 페이지입니다.|  
|<xref:System.Windows.Media.PolyLineSegment>|일련의 줄을 만듭니다.|참조 된 <xref:System.Windows.Media.PolyLineSegment> 유형 페이지입니다.|  
|<xref:System.Windows.Media.PolyQuadraticBezierSegment>|일련의 정방형 3차원 곡선을 만듭니다.|참조 된 <xref:System.Windows.Media.PolyQuadraticBezierSegment> 페이지입니다.|  
|<xref:System.Windows.Media.QuadraticBezierSegment>|정방형 3차원 곡선을 만듭니다.|[정방형 3차원 곡선 만들기](how-to-create-a-quadratic-bezier-curve.md).|  
  
 내 세그먼트는 <xref:System.Windows.Media.PathFigure> 다음 세그먼트의 시작점이 됩니다 각 세그먼트의 끝점을 사용 하 여 단일 기 하 도형으로 결합 됩니다. 합니다 <xref:System.Windows.Media.PathFigure.StartPoint%2A> 의 속성을 <xref:System.Windows.Media.PathFigure> 첫 번째 세그먼트를 그릴 점을 지정 합니다. 각 후속 세그먼트는 이전 세그먼트의 끝점에서 시작합니다. 세로 줄을 예를 들어 `10,50` 를 `10,150` 설정 하 여 정의할 수 있습니다 합니다 <xref:System.Windows.Media.PathFigure.StartPoint%2A> 속성을 `10,50` 만들고를 <xref:System.Windows.Media.LineSegment> 사용 하 여를 <xref:System.Windows.Media.LineSegment.Point%2A> 의 속성 설정을 `10,150`.  
  
 다음 예제에서는 간단한 <xref:System.Windows.Media.PathGeometry> 단일 이루어져 <xref:System.Windows.Media.PathFigure> 사용 하 여를 <xref:System.Windows.Media.LineSegment> 사용 하 여 표시를 <xref:System.Windows.Shapes.Path> 요소입니다. <xref:System.Windows.Media.PathFigure> 개체의 <xref:System.Windows.Media.PathFigure.StartPoint%2A> 로 설정 되어 `10,20` 와 <xref:System.Windows.Media.LineSegment> 끝점을 사용 하 여 정의 `100,130`합니다. 다음 그림에 표시 된 <xref:System.Windows.Media.PathGeometry> 이 예제에서 생성 합니다.  
  
 ![LineGeometry](./media/graphicsmm-line.gif "graphicsmm_line")  
단일 LineSegment를 포함하는 PathGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMPathGeometryLineExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmpathgeometrylineexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryLineExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmpathgeometrylineexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryLineExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmpathgeometrylineexample)]  
  
 이 예제에서는 앞으로 비교해 보는 것이 <xref:System.Windows.Media.LineGeometry> 예제입니다.  에 대 한 구문과 <xref:System.Windows.Media.PathGeometry> 단순 보다 훨씬 더 복잡 <xref:System.Windows.Media.LineGeometry>, 하 고 사용 하는 것을 만들 수는 <xref:System.Windows.Media.LineGeometry> verbose 구문의 있지만 경우 클래스는 <xref:System.Windows.Media.PathGeometry> 매우 복잡 하 고 복잡 한 허용 기하학적 영역입니다.  
  
 더 복잡 한 기 하 도형의 조합을 사용 하 여 만들 수 있습니다 <xref:System.Windows.Media.PathSegment> 개체입니다.  
  
 다음 예제에서는 한 <xref:System.Windows.Media.BezierSegment>, <xref:System.Windows.Media.LineSegment>, 및 <xref:System.Windows.Media.ArcSegment> 도형을 만들어야 합니다. 이 예에서는 먼저 입방 형 3 차원 곡선 점이 4 개를 정의 하는 것을 만듭니다: 시작점, 끝점은 이전 세그먼트의 끝 지점 (<xref:System.Windows.Media.BezierSegment.Point3%2A>), 그리고 두 개의 제어점 (<xref:System.Windows.Media.BezierSegment.Point1%2A> 및 <xref:System.Windows.Media.BezierSegment.Point2%2A>).  입방형 3차원 곡선의 두 제어점은 자석처럼 동작하여 서로를 향해서 직선 방향에 놓일 부분을 잡아당겨 곡선을 형성합니다. 첫 번째 제어점 <xref:System.Windows.Media.BezierSegment.Point1%2A>, 시작 부분에 영향을 줍니다 곡선의 부분, 두 번째 제어점 <xref:System.Windows.Media.BezierSegment.Point2%2A>, 곡선의 끝 부분에 영향을 줍니다.  
  
 예제에서는 그런를 <xref:System.Windows.Media.LineSegment>는 앞의 끝점 간에 그려지는 <xref:System.Windows.Media.BezierSegment> 하 여 지정 된 지점 앞에 있는 해당 <xref:System.Windows.Media.LineSegment> 속성입니다.  
  
 예제에서는 그런를 <xref:System.Windows.Media.ArcSegment>, 앞의 끝점에서 출발 하는 <xref:System.Windows.Media.LineSegment> 로 지정 된 지점에 해당 <xref:System.Windows.Media.ArcSegment.Point%2A> 속성입니다. 또한이 예제에서는 호의 x 및 y 반경을 지정 (<xref:System.Windows.Media.ArcSegment.Size%2A>), 회전 각도 (<xref:System.Windows.Media.ArcSegment.RotationAngle%2A>), 결과 원호의 각도 크기 수 해야 함을 나타내는 플래그 (<xref:System.Windows.Media.ArcSegment.IsLargeArc%2A>), 호를 그릴 방향을 나타내는 값 (<xref:System.Windows.Media.ArcSegment.SweepDirection%2A>). 다음 그림은 이 예제에서 만들어지는 도형을 보여 줍니다.  
  
 ![PathGeometry](./media/graphicsmm-path2.gif "graphicsmm_path2")  
PathGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMPathGeometryComplexExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmpathgeometrycomplexexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmpathgeometrycomplexexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmpathgeometrycomplexexample)]  
  
 여러 개 사용 하면 훨씬 더 복잡 한 기 하 도형을 만들 수 있습니다 <xref:System.Windows.Media.PathFigure> 내에서 개체를 <xref:System.Windows.Media.PathGeometry>입니다.  
  
 다음 예제에서는 한 <xref:System.Windows.Media.PathGeometry> 두 개의 <xref:System.Windows.Media.PathFigure> 개체를 여러 개 포함 된 각 <xref:System.Windows.Media.PathSegment> 개체입니다.  <xref:System.Windows.Media.PathFigure> 위의 예제에서와 <xref:System.Windows.Media.PathFigure> 사용 하 여를 <xref:System.Windows.Media.PolyLineSegment> 및 <xref:System.Windows.Media.QuadraticBezierSegment> 사용 됩니다.  A <xref:System.Windows.Media.PolyLineSegment> 점의 배열을 사용 하 여 정의 및 <xref:System.Windows.Media.QuadraticBezierSegment> 제어점과 끝점으로 정의 됩니다. 다음 그림은 이 예제에서 만들어지는 도형을 보여 줍니다.  
  
 ![PathGeometry](./media/graphicsmm-path.gif "graphicsmm_path")  
여러 그림이 있는 PathGeometry  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMPathGeometryComplexMultiExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmpathgeometrycomplexmultiexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexMultiExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmpathgeometrycomplexmultiexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMPathGeometryComplexMultiExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmpathgeometrycomplexmultiexample)]  
  
### <a name="streamgeometry"></a>StreamGeometry  
 같은 합니다 <xref:System.Windows.Media.PathGeometry> 클래스는 <xref:System.Windows.Media.StreamGeometry> 곡선, 호 및 선을 포함할 수 있는 복잡 한 기 하 도형을 정의 합니다. 와 달리를 <xref:System.Windows.Media.PathGeometry>, 내용의 <xref:System.Windows.Media.StreamGeometry> 데이터 바인딩, 애니메이션 또는 수정을 지원 하지 않습니다. 사용 하 여는 <xref:System.Windows.Media.StreamGeometry> 복잡 한 기 하 도형을 설명 해야 하지만 데이터 바인딩, 애니메이션 또는 수정을 지원 오버 헤드를 원하지 않는 합니다. 효율성으로 인해는 <xref:System.Windows.Media.StreamGeometry> 클래스는 표시기 (adorner)를 설명 하는 데 적합 합니다.  
  
 예제를 보려면 [StreamGeometry를 사용하여 도형 만들기](how-to-create-a-shape-using-a-streamgeometry.md)를 참조하세요.  
  
### <a name="path-markup-syntax"></a>경로 태그 구문  
 합니다 <xref:System.Windows.Media.PathGeometry> 및 <xref:System.Windows.Media.StreamGeometry> 형식은 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 구문 이동의 특별 시리즈를 사용 하 여 특성 및 그리기 명령을 합니다. 자세한 내용은 [경로 태그 구문](path-markup-syntax.md)을 참조하세요.  
  
<a name="wcpsdk_graphics_geometry_introduction2"></a>   
## <a name="composite-geometries"></a>복합 기하 도형  
 사용 하 여 복합 기 하 도형 개체를 만들 수 있습니다는 <xref:System.Windows.Media.GeometryGroup>, <xref:System.Windows.Media.CombinedGeometry>, 또는 정적 호출 하 여 <xref:System.Windows.Media.Geometry> 메서드 <xref:System.Windows.Media.Geometry.Combine%2A>합니다.  
  
- 합니다 <xref:System.Windows.Media.CombinedGeometry> 개체 및 <xref:System.Windows.Media.Geometry.Combine%2A> 메서드 두 기 하 도형으로 정의 되는 영역을 결합 하 여 부울 연산을 수행 합니다. <xref:System.Windows.Media.Geometry> 영역이 없는 개체 삭제 됩니다. 두 개의 <xref:System.Windows.Media.Geometry> (있지만 이러한 두 기 하 도형도 복합 기 하 도형) 개체를 결합할 수 있습니다.  
  
- 합니다 <xref:System.Windows.Media.GeometryGroup> 클래스의 융 화를 만듭니다는 <xref:System.Windows.Media.Geometry> 해당 영역을 결합 하지 않고 포함 된 개체입니다. 임의 개수의 <xref:System.Windows.Media.Geometry> 개체를 추가할 수는 <xref:System.Windows.Media.GeometryGroup>합니다. 예제를 보려면 [복합 도형 만들기](how-to-create-a-composite-shape.md)를 참조하세요.  
  
 결합 작업을 수행 하지 않는 때문에 사용 하 여 <xref:System.Windows.Media.GeometryGroup> 개체가 사용 하 여 성능상의 이점을 제공 <xref:System.Windows.Media.CombinedGeometry> 개체 또는 <xref:System.Windows.Media.Geometry.Combine%2A> 메서드.  
  
<a name="combindgeometriessection"></a>   
## <a name="combined-geometries"></a>결합된 기하 도형  
 언급 한 이전 섹션의 <xref:System.Windows.Media.CombinedGeometry> 개체 및 <xref:System.Windows.Media.Geometry.Combine%2A> 메서드 포함 하는 기 하 도형으로 정의 되는 영역을 결합 합니다. <xref:System.Windows.Media.GeometryCombineMode> 열거형 기 하 도형을 결합 하는 방법을 지정 합니다. 가능한 값은 <xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A> 속성은: <xref:System.Windows.Media.GeometryCombineMode.Union>를 <xref:System.Windows.Media.GeometryCombineMode.Intersect>, <xref:System.Windows.Media.GeometryCombineMode.Exclude>, 및 <xref:System.Windows.Media.GeometryCombineMode.Xor>합니다.  
  
 다음 예제에서는 <xref:System.Windows.Media.CombinedGeometry> 결합 모드 Union 사용 하 여 정의 됩니다.  둘 다 <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 하며 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 50 여 원 동일한 반지름의 원이지만 중심 오프셋으로 정의 됩니다.  
  
 [!code-xaml[GeometrySample#23](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![Union 결합 모드의 결과](./media/mil-task-combined-geometry-union.PNG "mil_task_combined_geometry_union")  
  
 다음 예제에서는 <xref:System.Windows.Media.CombinedGeometry> 결합 모드를 사용 하 여 정의 <xref:System.Windows.Media.GeometryCombineMode.Xor>합니다.  둘 다 <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 하며 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 50 여 원 동일한 반지름의 원이지만 중심 오프셋으로 정의 됩니다.  
  
 [!code-xaml[GeometrySample#24](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Xor 결합 모드의 결과](./media/mil-task-combined-geometry-xor.PNG "mil_task_combined_geometry_union")  
  
 추가 예제를 보려면 [복합 도형 만들기](how-to-create-a-composite-shape.md) 및 [결합된 기하 도형 만들기](how-to-create-a-combined-geometry.md)를 참조하세요.  
  
<a name="freezable_features"></a>   
## <a name="freezable-features"></a>Freezable 기능  
 상속 하므로 합니다 <xref:System.Windows.Freezable> 클래스를 <xref:System.Windows.Media.Geometry> 몇 가지 특별 한 기능을 제공 하는 클래스: <xref:System.Windows.Media.Geometry> 로 개체를 선언할 수 있습니다 [XAML 리소스](../advanced/xaml-resources.md)개선 하기 위해 읽기 전용으로, 여러 개체 간에 공유 성능, 복제 하 고 스레드로부터 안전 합니다. 제공 하는 다른 기능에 대 한 자세한 <xref:System.Windows.Freezable> 개체를 참조 합니다 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)합니다.  
  
<a name="othergeometryfeatures"></a>   
## <a name="other-geometry-features"></a>기타 기하 도형 기능  
 <xref:System.Windows.Media.Geometry> 클래스에는 또한 다음과 같은 유용한 유틸리티 메서드도 제공 합니다.  
  
- <xref:System.Windows.Media.Geometry.GetArea%2A> -의 영역을 가져옵니다는 <xref:System.Windows.Media.Geometry>합니다.  
  
- <xref:System.Windows.Media.Geometry.FillContains%2A> -다른 기 하 도형을 포함 되는지 여부를 결정 <xref:System.Windows.Media.Geometry>합니다.  
  
- <xref:System.Windows.Media.Geometry.StrokeContains%2A> -결정 하는지 여부를의 스트로크를 <xref:System.Windows.Media.Geometry> 지정된 된 지점이 포함 됩니다.  
  
 참조 된 <xref:System.Windows.Media.Geometry> 메서드의 전체 목록은 클래스입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Geometry>
- <xref:System.Windows.Media.PathGeometry>
- <xref:System.Windows.Shapes.Path>
- <xref:System.Windows.Media.GeometryDrawing>
- [2차원 그래픽 및 이미징](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [경로 태그 구문](path-markup-syntax.md)
- [방법 항목](geometries-how-to-topics.md)
- [애니메이션 개요](animation-overview.md)
- [WPF에서 Shape 및 기본 그리기 개요](shapes-and-basic-drawing-in-wpf-overview.md)
- [Drawing 개체 개요](drawing-objects-overview.md)
