---
title: WPF 브러시 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], about brushes
ms.assetid: ecea1955-420b-45c6-bf43-c1404c072c41
ms.openlocfilehash: 29f0bc77306df5639c188295f9f5dff7f18b4706
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962841"
---
# <a name="wpf-brushes-overview"></a>WPF 브러시 개요
화면에 표시 되는 모든 항목은 브러시로 그리기 때문에 표시 됩니다. 예를 들어 브러시를 사용 하 여 단추의 배경, 텍스트 전경 및 모양의 채우기를 설명할 수 있습니다. 이 항목에서는 브러시를 사용 하 여 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 그리는 개념을 소개 하 고 예제를 제공 합니다. 브러시를 사용하여 간단한 단색부터 복잡한 패턴 및 이미지 집합에 이르는 모든 방식으로 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 개체를 그릴 수 있습니다.  
  
<a name="paintingwithbrush"></a>   
## <a name="painting-with-a-brush"></a>브러시로 그리기  
 출력을 사용 하 여 영역을 "그립니다".<xref:System.Windows.Media.Brush> 다른 브러시는 다른 유형의 출력 합니다. 일부 브러시 그라데이션, 패턴, 이미지 또는 드로잉을 사용 하 여 다른 단색으로 영역을 그립니다. 다음 그림에서는 각각의 서로 다른 <xref:System.Windows.Media.Brush> 형식에 대 한 예를 보여 줍니다.  
  
 ![브러시 형식](./media/graphicsmm-brushtypes.jpg "graphicsmm_brushtypes")  
브러시 예제  
  
 대부분의 시각적 개체를 사용 하 여 그리는 방법을 지정할 수 있습니다. 다음 표에서는을 <xref:System.Windows.Media.Brush>사용할 수 있는 몇 가지 일반적인 개체와 속성을 보여 줍니다.  
  
|클래스|브러시 속성|  
|-----------|----------------------|  
|<xref:System.Windows.Controls.Border>|<xref:System.Windows.Controls.Border.BorderBrush%2A>, <xref:System.Windows.Controls.Border.Background%2A>|  
|<xref:System.Windows.Controls.Control>|<xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A>|  
|<xref:System.Windows.Controls.Panel>|<xref:System.Windows.Controls.Panel.Background%2A>|  
|<xref:System.Windows.Media.Pen>|<xref:System.Windows.Media.Pen.Brush%2A>|  
|<xref:System.Windows.Shapes.Shape>|<xref:System.Windows.Shapes.Shape.Fill%2A>, <xref:System.Windows.Shapes.Shape.Stroke%2A>|  
|<xref:System.Windows.Controls.TextBlock>|<xref:System.Windows.Controls.TextBlock.Background%2A>|  
  
 다음 섹션에서는 다양 <xref:System.Windows.Media.Brush> 한 형식에 대해 설명 하 고 각각의 예제를 제공 합니다.  
  
<a name="paintwithsolidcolorbrush"></a>   
## <a name="paint-with-a-solid-color"></a>단색으로 그리기  
 는 <xref:System.Windows.Media.SolidColorBrush> 단색<xref:System.Windows.Media.Color>으로 영역을 그립니다. <xref:System.Windows.Media.SolidColorBrush.Color%2A> <xref:System.Windows.Media.Colors> 의를 지정 하는 다양 한 방법이 있습니다 .예를들어알파,빨강,파랑및녹색채널을지정하거나클래스에서제공하는미리정의된색중하나를사용할수있습니다.<xref:System.Windows.Media.SolidColorBrush>  
  
 다음 예제에서는를 <xref:System.Windows.Media.SolidColorBrush> 사용 하 여의 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle>를 그립니다. 다음 그림은 칠해진 사각형을 보여 줍니다.  
  
 ![System.windows.media.solidcolorbrush>를 사용 하 여 그린 사각형](./media/graphicsmm-brush-ovw-solidcolorbrush.png "graphicsmm_brush_ovw_solidcolorbrush")  
System.windows.media.solidcolorbrush>를 사용 하 여 그린 사각형  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmsolidcolorbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmsolidcolorbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmsolidcolorbrushexampleinline)]  
  
 <xref:System.Windows.Media.SolidColorBrush> 클래스에 대 한 자세한 내용은 [단색 및 그라데이션을 사용한 그리기 개요](painting-with-solid-colors-and-gradients-overview.md)를 참조 하세요.  
  
<a name="paintwithlineargradientbrush"></a>   
## <a name="paint-with-a-linear-gradient"></a>선형 그라데이션으로 그리기  
 <xref:System.Windows.Media.LinearGradientBrush> 선형 그라데이션으로 영역을 그립니다. 선형 그라데이션은 선 전체에 걸쳐 그라데이션 축을 혼합 하 여 두 개 이상의 색을 혼합 합니다. 개체를 <xref:System.Windows.Media.GradientStop> 사용 하 여 그라데이션의 색과 위치를 지정 합니다.  
  
 다음 예제에서는를 <xref:System.Windows.Media.LinearGradientBrush> 사용 하 여의 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle>를 그립니다. 다음 그림은 칠해진 사각형을 보여 줍니다.  
  
 ![System.windows.media.lineargradientbrush.startpoint를 사용 하 여 그린 사각형](./media/graphicsmm-brush-ovw-lineargradientbrush.jpg "graphicsmm_brush_ovw_lineargradientbrush")  
System.windows.media.lineargradientbrush.startpoint를 사용 하 여 그린 사각형  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmlineargradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmlineargradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmlineargradientbrushexampleinline)]  
  
 <xref:System.Windows.Media.LinearGradientBrush> 클래스에 대 한 자세한 내용은 [단색 및 그라데이션을 사용한 그리기 개요](painting-with-solid-colors-and-gradients-overview.md)를 참조 하세요.  
  
<a name="paintwithradialgradientbrush"></a>   
## <a name="paint-with-a-radial-gradient"></a>방사형 그라데이션으로 그리기  
 는 <xref:System.Windows.Media.RadialGradientBrush> 방사형 그라데이션으로 영역을 그립니다. 방사형 그라데이션은 원에서 두 개 이상의 색을 혼합 합니다. <xref:System.Windows.Media.LinearGradientBrush> 클래스와 마찬가지로 개체를 사용 <xref:System.Windows.Media.GradientStop> 하 여 그라데이션의 색과 위치를 지정 합니다.  
  
 다음 예제에서는를 <xref:System.Windows.Media.RadialGradientBrush> 사용 하 여의 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle>를 그립니다. 다음 그림은 칠해진 사각형을 보여 줍니다.  
  
 ![RadialGradientBrush를 사용 하 여 그린 사각형](./media/graphicsmm-brush-ovw-radialgradientbrush.jpg "graphicsmm_brush_ovw_radialgradientbrush")  
RadialGradientBrush를 사용 하 여 그린 사각형  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmradialgradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmradialgradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmradialgradientbrushexampleinline)]  
  
 <xref:System.Windows.Media.RadialGradientBrush> 클래스에 대 한 자세한 내용은 [단색 및 그라데이션을 사용한 그리기 개요](painting-with-solid-colors-and-gradients-overview.md)를 참조 하세요.  
  
<a name="paintwithimage"></a>   
## <a name="paint-with-an-image"></a>이미지로 그리기  
 는 <xref:System.Windows.Media.ImageBrush> 를<xref:System.Windows.Media.ImageSource>사용 하 여 영역을 그립니다.  
  
 다음 예제에서는를 사용 <xref:System.Windows.Media.ImageBrush> 하 여의 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle>를 그립니다. 다음 그림은 칠해진 사각형을 보여 줍니다.  
  
 ![ImageBrush에서 그린 사각형](./media/graphicsmm-brush-ovw-imagebrush.jpg "graphicsmm_brush_ovw_imagebrush")  
이미지를 사용 하 여 그린 사각형  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmimagebrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmimagebrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmimagebrushexampleinline)]  
  
 <xref:System.Windows.Media.ImageBrush> 클래스에 대 한 자세한 내용은 [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)를 참조 하세요.  
  
<a name="paintwithdrawing"></a>   
## <a name="paint-with-a-drawing"></a>Drawing으로 그리기  
 는 <xref:System.Windows.Media.DrawingBrush> 를<xref:System.Windows.Media.Drawing>사용 하 여 영역을 그립니다. 에 <xref:System.Windows.Media.Drawing> 는 도형, 이미지, 텍스트 및 미디어가 포함 될 수 있습니다.  
  
 다음 예제에서는를 <xref:System.Windows.Media.DrawingBrush> 사용 하 여의 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle>를 그립니다. 다음 그림은 칠해진 사각형을 보여 줍니다.  
  
 ![DrawingBrush를 사용 하 여 그린 사각형](./media/graphicsmm-brush-ovw-drawingbrush.jpg "graphicsmm_brush_ovw_drawingbrush")  
DrawingBrush를 사용 하 여 그린 사각형  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmdrawingbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmdrawingbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmdrawingbrushexampleinline)]  
  
 <xref:System.Windows.Media.DrawingBrush> 클래스에 대 한 자세한 내용은 [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)를 참조 하세요.  
  
<a name="paintwithvisual"></a>   
## <a name="paint-with-a-visual"></a>시각적 개체를 사용 하 여 그리기  
 는 <xref:System.Windows.Media.VisualBrush> <xref:System.Windows.Media.Visual> 개체를 사용 하 여 영역을 그립니다. 시각적 개체 <xref:System.Windows.Controls.Button>의 예로는, <xref:System.Windows.Controls.Page>및 <xref:System.Windows.Controls.MediaElement>가 있습니다. <xref:System.Windows.Media.VisualBrush> 또한 응용 프로그램의 한 부분에서 다른 영역으로 콘텐츠를 프로젝션 할 수 있습니다. 리플렉션 효과를 만들고 화면의 일부를 확대 하는 데 매우 유용 합니다.  
  
 다음 예제에서는를 <xref:System.Windows.Media.VisualBrush> 사용 하 여의 <xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Rectangle>를 그립니다. 다음 그림은 칠해진 사각형을 보여 줍니다.  
  
 ![VisualBrush를 사용 하 여 그린 사각형](./media/graphicsmm-brush-ovw-visualbrush.jpg "graphicsmm_brush_ovw_visualbrush")  
VisualBrush를 사용 하 여 그린 사각형  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmvisualbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmvisualbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmvisualbrushexampleinline)]  
  
 <xref:System.Windows.Media.VisualBrush> 클래스에 대 한 자세한 내용은 [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)를 참조 하세요.  
  
<a name="paintwithpredefinedbrushesandsystemcolors"></a>   
## <a name="paint-using-predefined-and-system-brushes"></a>미리 정의 된 브러시 및 시스템 브러시를 사용 하 여 그리기  
 편의를 위해 Windows Presentation Foundation (WPF)는 개체를 그리는 데 사용할 수 있는 미리 정의 된 일련의 브러시와 시스템 브러시를 제공 합니다.  
  
- 사용 가능한 미리 정의 된 브러시 목록은 <xref:System.Windows.Media.Brushes> 클래스를 참조 하세요. 미리 정의 된 브러시를 사용 하는 방법을 보여 주는 예제는 [단색으로 영역 그리기](how-to-paint-an-area-with-a-solid-color.md)를 참조 하세요.  
  
- 사용 가능한 시스템 브러시 목록은 <xref:System.Windows.SystemColors> 클래스를 참조 하세요. 예제는 [시스템 브러시로 영역 그리기](how-to-paint-an-area-with-a-system-brush.md)를 참조 하세요.  
  
<a name="commonbrushfeatures"></a>   
## <a name="common-brush-features"></a>일반적인 브러시 기능  
 <xref:System.Windows.Media.Brush>개체는 브러시 <xref:System.Windows.Media.Brush.Opacity%2A> 를 투명 하 게 또는 부분적으로 투명 하 게 만드는 데 사용할 수 있는 속성을 제공 합니다. 값이 0 이면 브러시가 완전히 투명 해지고 <xref:System.Windows.Media.Brush.Opacity%2A> 값이 1 이면 브러시가 완전히 불투명 합니다. <xref:System.Windows.Media.Brush.Opacity%2A> 다음 예제에서는 <xref:System.Windows.Media.Brush.Opacity%2A> 속성을 사용 하 여 <xref:System.Windows.Media.SolidColorBrush> 25% 불투명 하 게 만듭니다.  
  
 [!code-xaml[BrushOverviewExamples_snip#OpacityExample1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/OpacityExample.xaml#opacityexample1xaml)]  
  
 [!code-csharp[BrushOverviewExamples_snip#OpacityExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/OpacityExample.cs#opacityexample1csharp)]  
  
 브러시에 부분적으로 투명 한 색이 포함 되어 있으면 색의 불투명도 값이 브러시의 불투명도 값을 사용 하 여 결합 됩니다. 예를 들어 브러시의 불투명도 값이 0.5이 고 브러시에 사용 된 색의 불투명도 값이 0.5 이면 출력 색의 불투명도 값은 0.25입니다.  
  
> [!NOTE]
> <xref:System.Windows.UIElement.Opacity%2A?displayProperty=nameWithType> 속성을 사용 하 여 전체 요소의 불투명도를 변경 하는 것 보다 브러시의 불투명도 값을 변경 하는 것이 더 효율적입니다.  
  
 <xref:System.Windows.Media.Brush.Transform%2A> 또는<xref:System.Windows.Media.Brush.RelativeTransform%2A> 속성을 사용 하 여 브러시의 콘텐츠를 회전, 크기 조정, 기울이기 및 변환할 수 있습니다. 자세한 내용은 [브러시 변환 개요](brush-transformation-overview.md)를 참조 하세요.  
  
 개체는 <xref:System.Windows.Media.Animation.Animatable> 개체 이기 때문 <xref:System.Windows.Media.Brush> 에 개체에 애니메이션을 적용할 수 있습니다. 자세한 내용은 [애니메이션 개요](animation-overview.md)를 참조하세요.  
  
<a name="freezable_features"></a>   
### <a name="freezable-features"></a>Freezable 기능  
 클래스는 <xref:System.Windows.Freezable> 클래스에서 상속 하기 때문에 <xref:System.Windows.Media.Brush> 클래스는 여러 가지 특수 한 <xref:System.Windows.Media.Brush> 기능을 제공 합니다. 즉, 개체를 [리소스로](../advanced/xaml-resources.md)선언 하 고, 여러 개체 간에 공유 하 고, 복제할 수 있습니다. 또한을 제외한 <xref:System.Windows.Media.Brush> <xref:System.Windows.Media.VisualBrush> 모든 형식을 읽기 전용으로 설정 하 여 성능을 향상 시키고 스레드로부터 안전 하 게 만들 수 있습니다.  
  
 제공 하는 다른 기능에 대 한 자세한 내용은 <xref:System.Windows.Freezable> 개체를 참조 하세요 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)합니다.  
  
 개체를 고정할 수 없는 <xref:System.Windows.Media.VisualBrush> 이유에 대 한 자세한 내용은 <xref:System.Windows.Media.VisualBrush> 유형 페이지를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Brush>
- <xref:System.Windows.Media.Brushes>
- [단색 및 그라데이션을 사용한 그리기 개요](painting-with-solid-colors-and-gradients-overview.md)
- [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)
- [Freezable 개체 개요](../advanced/freezable-objects-overview.md)
- [브러시 샘플](https://go.microsoft.com/fwlink/?LinkID=159973)
- [ImageBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160005)
- [VisualBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160049)
- [방법 항목](brushes-how-to-topics.md)
- [기타 성능 권장 사항](../advanced/optimizing-performance-other-recommendations.md)
