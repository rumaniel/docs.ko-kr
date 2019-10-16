---
title: 이미지, 그림 및 시각적 표시로 그리기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], painting with drawings
- painting [WPF], with drawings
- painting [WPF], with images
- painting with visuals [WPF]
- brushes [WPF], painting with images
- brushes [WPF], painting with visuals
ms.assetid: 779aac3f-8d41-49d8-8130-768244aa2240
ms.openlocfilehash: e80132a5467f932e5569787f43427044ba2be256
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929605"
---
# <a name="painting-with-images-drawings-and-visuals"></a>이미지, 그림 및 시각적 표시로 그리기
이 항목 <xref:System.Windows.Media.ImageBrush>에서는, <xref:System.Windows.Media.DrawingBrush>및 <xref:System.Windows.Media.VisualBrush> 개체를 사용 하 여 이미지, <xref:System.Windows.Media.Drawing>또는를 사용 하 <xref:System.Windows.Media.Visual>여 영역을 그리는 방법을 설명 합니다.  

<a name="prereqs"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목을 이해하려면 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서 제공하는 다양한 형식의 브러시와 해당 기본 기능에 대해 잘 알고 있어야 합니다. 소개 내용을 보려면 [WPF 브러시 개요](wpf-brushes-overview.md)를 참조하세요.  
  
<a name="image"></a>   
## <a name="paint-an-area-with-an-image"></a>이미지로 영역 그리기  
 <xref:System.Windows.Media.ImageBrush> 영역을 그립니다는 <xref:System.Windows.Media.ImageSource>합니다. 가장 일반적인 유형의 <xref:System.Windows.Media.ImageSource> 를 사용 하는 <xref:System.Windows.Media.ImageBrush> 는 <xref:System.Windows.Media.Imaging.BitmapImage>, 비트맵 그래픽을 설명 하는 합니다. 사용할 수는 <xref:System.Windows.Media.DrawingImage> 를 사용 하 여 그릴를 <xref:System.Windows.Media.Drawing> 개체 이며 간단 하 게 사용을 <xref:System.Windows.Media.DrawingBrush> 대신 합니다. 개체에 대 한 <xref:System.Windows.Media.ImageSource> 자세한 내용은 [이미징 개요](imaging-overview.md)를 참조 하세요.  
  
 를 사용 하 여 <xref:System.Windows.Media.ImageBrush>그리려면를 <xref:System.Windows.Media.Imaging.BitmapImage> 만든 다음 비트맵 콘텐츠를 로드 하는 데 사용 합니다. 그런 다음를 사용 <xref:System.Windows.Media.Imaging.BitmapImage> 하 여의 <xref:System.Windows.Media.ImageBrush.ImageSource%2A> <xref:System.Windows.Media.ImageBrush>속성을 설정 합니다. 마지막으로 그리기를 <xref:System.Windows.Media.ImageBrush> 하려는 개체에를 적용 합니다.  에서는 로드할 이미지의 경로로의 속성 <xref:System.Windows.Media.ImageBrush> 을 <xref:System.Windows.Media.ImageBrush.ImageSource%2A> 설정할 수도 있습니다. [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]  
  
 모든 <xref:System.Windows.Media.Brush> 개체<xref:System.Windows.Media.ImageBrush> 와 마찬가지로를 사용 하 여 도형, 패널, 컨트롤 및 텍스트와 같은 개체를 그릴 수 있습니다. 다음 그림에서는를 사용 <xref:System.Windows.Media.ImageBrush>하 여 수행할 수 있는 몇 가지 효과를 보여 줍니다.  
  
 ![ImageBrush 출력 예제](./media/wcpsdk-mmgraphics-imagebrushexamples.gif "wcpsdk_mmgraphics_imagebrushexamples")  
ImageBrush로 그린 개체  
  
 기본적으로는 <xref:System.Windows.Media.ImageBrush> 이미지를 늘려 그릴 영역을 완전히 채우도록 하며, 그려지는 영역의 가로 세로 비율이 이미지와 다른 경우 이미지를 왜곡 시킬 수 있습니다. <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성을의 <xref:System.Windows.Media.Stretch.Fill> 기본값에서, <xref:System.Windows.Media.Stretch.None> <xref:System.Windows.Media.Stretch.Uniform>또는 로변경하여이동작을변경할수있습니다.<xref:System.Windows.Media.Stretch.UniformToFill> 는 <xref:System.Windows.Media.ImageBrush> 의<xref:System.Windows.Media.TileBrush>형식 이므로 이미지 브러시가 출력 영역을 채우는 방법과 패턴을 만드는 방법을 정확 하 게 지정할 수 있습니다. 고급 <xref:System.Windows.Media.TileBrush> 기능에 대 한 자세한 내용은 [TileBrush 개요](tilebrush-overview.md)를 참조 하세요.  
  
<a name="fillingpanelwithimage"></a>   
## <a name="example-paint-an-object-with-a-bitmap-image"></a>예제: 비트맵 이미지를 사용 하 여 개체 그리기  
 다음 예제에서는를 사용 <xref:System.Windows.Media.ImageBrush> 하 여의 <xref:System.Windows.Controls.Panel.Background%2A> <xref:System.Windows.Controls.Canvas>를 그립니다.  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/ImageBrushExample.xaml#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/ImageBrushExample.cs#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/imagebrushexample.vb#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]  
  
<a name="drawingbrushintro"></a>   
## <a name="paint-an-area-with-a-drawing"></a>Drawing으로 영역 그리기  
 를 <xref:System.Windows.Media.DrawingBrush> 사용 하면 도형, 텍스트, 이미지 및 비디오를 사용 하 여 영역을 그릴 수 있습니다. 드로잉 브러시 안에 있는 셰이프는 단색, 그라데이션, 이미지 또는 다른 <xref:System.Windows.Media.DrawingBrush>색으로 그릴 수 있습니다. 다음 그림에서는의 <xref:System.Windows.Media.DrawingBrush>몇 가지 사용 방법을 보여 줍니다.  
  
 ![DrawingBrush 출력 예제](./media/wcpsdk-mmgraphics-drawingbrushexamples.png "wcpsdk_mmgraphics_drawingbrushexamples")  
DrawingBrush로 그린 개체  
  
 는 <xref:System.Windows.Media.DrawingBrush> <xref:System.Windows.Media.Drawing> 개체를 사용 하 여 영역을 그립니다. 개체 <xref:System.Windows.Media.Drawing> 는 모양, 비트맵, 비디오 또는 텍스트 줄과 같은 표시 되는 콘텐츠를 설명 합니다. 그리기 형식마다 다른 콘텐츠 형식을 설명합니다. 다음은 여러 그리기 개체 형식을 보여 주는 목록입니다.  
  
- <xref:System.Windows.Media.GeometryDrawing>– 모양을 그립니다.  
  
- <xref:System.Windows.Media.ImageDrawing>– 이미지를 그립니다.  
  
- <xref:System.Windows.Media.GlyphRunDrawing>– 텍스트를 그립니다.  
  
- <xref:System.Windows.Media.VideoDrawing>– 오디오 또는 비디오 파일을 재생 합니다.  
  
- <xref:System.Windows.Media.DrawingGroup>– 다른 그리기를 그립니다. 다른 그리기를 단일 합성 그리기로 결합하려면 그리기 그룹을 사용합니다.  
  
 개체에 대 한 <xref:System.Windows.Media.Drawing> 자세한 내용은 [Drawing 개체 개요](drawing-objects-overview.md)를 참조 하세요.  
  
 와 마찬가지로는 <xref:System.Windows.Media.DrawingBrush> 를 확장 <xref:System.Windows.Media.DrawingBrush.Drawing%2A> 하 여 해당 출력 영역을 채웁니다. <xref:System.Windows.Media.ImageBrush> <xref:System.Windows.Media.TileBrush.Stretch%2A> 의<xref:System.Windows.Media.Stretch.Fill>기본 설정에서 속성을 변경 하 여이 동작을 재정의할 수 있습니다. 자세한 내용은 <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성을 참조하세요.  
  
<a name="fillingareawithdrawingbrushexample"></a>   
## <a name="example-paint-an-object-with-a-drawing"></a>예제: Drawing으로 개체 그리기  
 다음 예제에서는 3개의 타원 그림으로 개체를 그리는 방법을 보여 줍니다. 는 <xref:System.Windows.Media.GeometryDrawing> 줄임표를 설명 하는 데 사용 됩니다.  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/DrawingBrushExample.xaml#graphicsmmdrawingbrushasbuttonbackgroundexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/DrawingBrushExample.cs#graphicsmmdrawingbrushasbuttonbackgroundexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/drawingbrushexample.vb#graphicsmmdrawingbrushasbuttonbackgroundexample1)]  
  
<a name="visualbrushsection"></a>   
## <a name="paint-an-area-with-a-visual"></a>시각적 표시로 영역 그리기  
 에서 <xref:System.Windows.Media.VisualBrush> 가장 유연 하 고 강력한 모든 브러시는 <xref:System.Windows.Media.Visual>로 영역을 그립니다. 는 <xref:System.Windows.Media.Visual> 많은 유용한 그래픽 구성 요소의 상위 항목으로 사용 되는 하위 수준 그래픽 형식입니다. 예 <xref:System.Windows.Window> <xref:System.Windows.Controls.Control> <xref:System.Windows.Media.Visual> 를 들어,, 및 클래스는 모든 형식의 개체입니다. <xref:System.Windows.FrameworkElement> 를 사용 하면 거의 모든 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 그래픽 개체를 사용 하 여 영역 을그릴수있습니다.<xref:System.Windows.Media.VisualBrush>  
  
> [!NOTE]
> 는 <xref:System.Windows.Media.VisualBrush> 개체의 <xref:System.Windows.Freezable> 형식 이지만 <xref:System.Windows.Media.VisualBrush.Visual%2A> 속성이 이외의 `null`값으로 설정 된 경우에는 고정할 수 없습니다 (읽기 전용으로 설정 됨).  
  
 두 가지 방법으로 지정할 수는 <xref:System.Windows.Media.VisualBrush.Visual%2A> 의 콘텐츠는 <xref:System.Windows.Media.VisualBrush>합니다.  
  
- 새 <xref:System.Windows.Media.Visual> 를 설정 하는 데 사용 합니다 <xref:System.Windows.Media.VisualBrush.Visual%2A> 의 속성을 <xref:System.Windows.Media.VisualBrush>합니다. 예제는 [다음 예제를 참조 하세요. 뒤에 나오는 시각적](#examplevisualbrush1) 섹션을 사용 하 여 개체를 그립니다.  
  
- 기존 항목 사용 <xref:System.Windows.Media.Visual>, 대상의 중복 이미지를 만드는 <xref:System.Windows.Media.Visual>합니다. 사용할 수 있습니다는 <xref:System.Windows.Media.VisualBrush> 리플렉션 및 확대와 같은 흥미로운 효과 만들 수 있습니다. 예제는 [다음 예제를 참조 하세요. 리플렉션](#examplevisualbrush2) 섹션을 만듭니다.  
  
 정의 하는 경우 새 <xref:System.Windows.Media.VisualBrush.Visual%2A> 에 대 한는 <xref:System.Windows.Media.VisualBrush> 하 고 <xref:System.Windows.Media.Visual> 는 <xref:System.Windows.UIElement> (예: 패널 또는 컨트롤)에서 실행 되는 레이아웃 시스템을 <xref:System.Windows.UIElement> 와 해당 자식 요소 때를 <xref:System.Windows.Media.VisualBrush.AutoLayoutContent%2A> 속성이 `true`. 그러나 루트 <xref:System.Windows.UIElement> 는 기본적으로 시스템의 나머지 부분에서 분리 되며 외부 레이아웃은이 경계를 넘어갈 수 없습니다. 루트의 크기를 명시적으로 지정 해야 하므로 <xref:System.Windows.UIElement>만 부모 이기 때문은 <xref:System.Windows.Media.VisualBrush> 하므로 해당 수 없습니다. 자동으로 크기가 조정 자체 그려지는 영역 및 합니다. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]의 레이아웃에 대한 자세한 내용은 [레이아웃](../advanced/layout.md)을 참조하세요.  
  
 및 <xref:System.Windows.Media.ImageBrush> <xref:System.Windows.Media.VisualBrush> 와 마찬가지로는 해당 콘텐츠를 확장 하 여 해당 출력 영역을 채웁니다. <xref:System.Windows.Media.DrawingBrush> <xref:System.Windows.Media.TileBrush.Stretch%2A> 의<xref:System.Windows.Media.Stretch.Fill>기본 설정에서 속성을 변경 하 여이 동작을 재정의할 수 있습니다. 자세한 내용은 <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성을 참조하세요.  
  
<a name="examplevisualbrush1"></a>   
## <a name="example-paint-an-object-with-a-visual"></a>예제: 시각적 개체를 사용 하 여 개체 그리기  
 다음 예제에서는 여러 컨트롤과 패널을 사용해서 사각형을 그립니다.  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/VisualBrushExample.xaml#graphicsmmvisualbrushasrectanglebackgroundexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/VisualBrushExample.cs#graphicsmmvisualbrushasrectanglebackgroundexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/visualbrushexample.vb#graphicsmmvisualbrushasrectanglebackgroundexample1)]  
  
<a name="examplevisualbrush2"></a>   
## <a name="example-create-a-reflection"></a>예제: 리플렉션 만들기  
 앞의 예제에서는 배경으로 사용할 새 <xref:System.Windows.Media.Visual> 를 만드는 방법을 살펴보았습니다. 를 <xref:System.Windows.Media.VisualBrush> 사용 하 여 기존 시각적 개체를 표시할 수도 있습니다 .이 기능을 사용 하면 반사 및 확대와 같은 흥미로운 시각적 효과를 얻을 수 있습니다. 다음 예제에서는를 <xref:System.Windows.Media.VisualBrush> 사용 하 여 여러 요소를 포함 <xref:System.Windows.Controls.Border> 하는의 리플렉션을 만듭니다. 다음 그림에서는 이 예제가 생성하는 출력을 보여 줍니다.  
  
 ![반영 된 시각적 개체] 입니다. (./media/graphicsmm-visualbrush-reflection-small.jpg "graphicsmm_visualbrush_reflection_small")  
반사된 표시 개체  
  
 [!code-csharp[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/ReflectionExample.cs#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-vb[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/reflectionexample.vb#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-xaml[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/ReflectionExample.xaml#graphicsmmvisualbrushreflectionexamplewholepage)]  
  
 화면의 일부를 확대하는 방법 및 리플렉션을 만드는 방법을 보여 주는 추가 예제를 보려면 [VisualBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160049)을 참조하세요.  
  
<a name="tilebrush"></a>   
## <a name="tilebrush-features"></a>TileBrush 기능  
 <xref:System.Windows.Media.ImageBrush>, <xref:System.Windows.Media.DrawingBrush> <xref:System.Windows.Media.TileBrush> 및 <xref:System.Windows.Media.VisualBrush> 는 개체의 형식입니다. <xref:System.Windows.Media.TileBrush>개체를 사용 하면 이미지, 그리기 또는 시각적 개체를 사용 하 여 영역을 그리는 방법을 다양 하 게 제어할 수 있습니다. 예를 들어 늘어난 이미지만으로 영역을 그리기보다, 패턴을 만드는 일련의 이미지 타일을 사용하여 영역을 그릴 수 있습니다.  
  
 에 <xref:System.Windows.Media.TileBrush> 는 세 가지 주요 구성 요소인 콘텐츠, 타일 및 출력 영역이 있습니다.  
  
 ![TileBrush 구성 요소](./media/wcpsdk-mmgraphics-defaultcontentprojection2.png "wcpsdk_mmgraphics_defaultcontentprojection2")  
단일 타일이 있는 TileBrush의 구성 요소  
  
 ![바둑판식으로 배열 된 TileBrush의 구성 요소](./media/graphicsmm-tiledprojection.png "graphicsmm_tiledprojection")  
여러 타일이 있는 TileBrush의 구성 요소  
  
 개체의 <xref:System.Windows.Media.TileBrush> 바둑판식 배열 기능에 대 한 자세한 내용은 [TileBrush 개요](tilebrush-overview.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.ImageBrush>
- <xref:System.Windows.Media.DrawingBrush>
- <xref:System.Windows.Media.VisualBrush>
- <xref:System.Windows.Media.TileBrush>
- [TileBrush 개요](tilebrush-overview.md)
- [WPF 브러시 개요](wpf-brushes-overview.md)
- [이미징 개요](imaging-overview.md)
- [Drawing 개체 개요](drawing-objects-overview.md)
- [불투명 마스크 개요](opacity-masks-overview.md)
- [WPF 그래픽 렌더링 개요](wpf-graphics-rendering-overview.md)
- [ImageBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160005)
- [VisualBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160049)
