---
title: TileBrush 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TileBrush [WPF]
- brushes [WPF], TileBrush
ms.assetid: aa4a7b7e-d09d-44c2-8d61-310c50e08d68
ms.openlocfilehash: c129f902937363972e6be1a6518ae5a97e467f44
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625691"
---
# <a name="tilebrush-overview"></a>TileBrush 개요
<xref:System.Windows.Media.TileBrush> 개체를 사용 하면 다양 한 이미지를 사용 하 여 영역을 그리는 방법에 대 한 제어를 사용 하 여 얻게 <xref:System.Windows.Media.Drawing>, 또는 <xref:System.Windows.Media.Visual>합니다. 이 항목에서는 사용 하는 방법에 설명 합니다 <xref:System.Windows.Media.TileBrush> 더 잘 제어 하는 방법에 대 한 기능을 <xref:System.Windows.Media.ImageBrush>, <xref:System.Windows.Media.DrawingBrush>, 또는 <xref:System.Windows.Media.VisualBrush> 영역을 그립니다.  

<a name="prerequisite"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목을 이해 하려면의 기본 기능을 사용 하는 방법을 이해 하는 데 도움이 되는 <xref:System.Windows.Media.ImageBrush>, <xref:System.Windows.Media.DrawingBrush>, 또는 <xref:System.Windows.Media.VisualBrush> 클래스입니다. 이러한 형식에 대 한 소개를 참조 하세요. 합니다 [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)합니다.  
  
<a name="tilebrush"></a>   
## <a name="painting-an-area-with-tiles"></a>타일로 영역 그리기  
 <xref:System.Windows.Media.ImageBrush>를 <xref:System.Windows.Media.DrawingBrush>에 <xref:System.Windows.Media.VisualBrush> 종류가 <xref:System.Windows.Media.TileBrush> 개체입니다. 타일 브러시는 이미지, 그림 또는 시각적 개체로 영역을 그리는 방법을 강력하게 제어할 수 있도록 합니다. 예를 들어 늘어난 이미지만으로 영역을 그리기보다, 패턴을 만드는 일련의 이미지 타일을 사용하여 영역을 그릴 수 있습니다.  
  
 타일 브러시로 영역을 그리려면 세 가지 구성 요소인, 콘텐츠, 기본 타일 및 출력 영역이 필요합니다.  
  
 ![TileBrush 구성 요소](./media/wcpsdk-mmgraphics-defaultcontentprojection2.png "wcpsdk_mmgraphics_defaultcontentprojection2")  
단일 타일이 있는 TileBrush의 구성 요소  
  
 ![바둑판식으로 배열 된 TileBrush의 구성 요소](./media/graphicsmm-tiledprojection.png "graphicsmm_tiledprojection")  
TileMode가 Tile인 TileBrush의 구성 요소  
  
 출력 영역은 그리는 영역을 같은 합니다 <xref:System.Windows.Shapes.Shape.Fill%2A> 의 <xref:System.Windows.Shapes.Ellipse> 또는 <xref:System.Windows.Controls.Control.Background%2A> 의 <xref:System.Windows.Controls.Button>합니다. 다음 섹션에서는 설명의 다른 두 구성 요소는 <xref:System.Windows.Media.TileBrush>합니다.  
  
<a name="brushcontent"></a>   
## <a name="brush-content"></a>브러시 콘텐츠  
 세 가지 유형의 가지 <xref:System.Windows.Media.TileBrush> 다른 유형의 콘텐츠를 사용 하 여 각각을 그립니다.  
  
- 브러시가 <xref:System.Windows.Media.ImageBrush>,이 콘텐츠는 이미지를 <xref:System.Windows.Media.ImageBrush.ImageSource%2A> 속성의 내용을 지정 된 <xref:System.Windows.Media.ImageBrush>.  
  
- 브러시가 <xref:System.Windows.Media.DrawingBrush>,이 콘텐츠는 그림입니다. 합니다 <xref:System.Windows.Media.DrawingBrush.Drawing%2A> 속성의 내용을 지정 된 <xref:System.Windows.Media.DrawingBrush>합니다.  
  
- 브러시가 <xref:System.Windows.Media.VisualBrush>,이 콘텐츠는 시각적 개체입니다. <xref:System.Windows.Media.VisualBrush.Visual%2A> 속성의 내용을 지정 된 <xref:System.Windows.Media.VisualBrush>합니다.  
  
 크기와 위치를 지정할 수 있습니다 <xref:System.Windows.Media.TileBrush> 를 사용 하 여 콘텐츠를 <xref:System.Windows.Media.TileBrush.Viewbox%2A> 속성인 일반적 이지만 <xref:System.Windows.Media.TileBrush.Viewbox%2A> 기본값으로 설정 합니다. 기본적으로 <xref:System.Windows.Media.TileBrush.Viewbox%2A> 완전히 브러시의 콘텐츠를 포함 하도록 구성 합니다. 구성에 대 한 자세한 내용은 합니다 <xref:System.Windows.Controls.Viewbox>, 참조는 <xref:System.Windows.Controls.Viewbox> 속성 페이지.  
  
<a name="thebasetile"></a>   
## <a name="the-base-tile"></a>기본 타일  
 <xref:System.Windows.Media.TileBrush> 기본 타일에 해당 콘텐츠를 프로젝션 합니다. 합니다 <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성 컨트롤 어떻게 <xref:System.Windows.Media.TileBrush> 콘텐츠가 기본 타일을 채우도록 확장 됩니다. 합니다 <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성으로 정의 하는 다음 값을 허용 합니다 <xref:System.Windows.Media.Stretch> 열거형:  
  
- <xref:System.Windows.Media.Stretch.None>: 브러시의 콘텐츠가 타일을 채우도록 확장 되지 않습니다.  
  
- <xref:System.Windows.Media.Stretch.Fill>: 브러시의 콘텐츠가 타일에 맞게 크기가 조정 됩니다. 콘텐츠의 높이 및 너비가 독립적으로 조정되므로 콘텐츠의 원래 가로 세로 비율이 유지되지 않을 수 있습니다. 즉, 출력 타일을 완전히 채우도록 브러시 콘텐츠를 이동해야 할 수 있습니다.  
  
- <xref:System.Windows.Media.Stretch.Uniform>: 브러시의 콘텐츠가 타일 내에 완전히 맞도록 크기가 조정 됩니다. 콘텐츠의 가로 세로 비율이 유지됩니다.  
  
- <xref:System.Windows.Media.Stretch.UniformToFill>: 콘텐츠의 원래 가로 세로 비율을 유지 하는 동안 출력 영역을 완전히 채우도록 브러시의 콘텐츠 크기가 조정 됩니다.  
  
 다음 이미지는 다양 한 보여줍니다 <xref:System.Windows.Media.TileBrush.Stretch%2A> 설정 합니다.  
  
 ![여러 TileBrush Stretch 설정](./media/img-mmgraphics-stretchenum.jpg "img_mmgraphics_stretchenum")  
  
 다음 예에서 콘텐츠는 <xref:System.Windows.Media.ImageBrush> 출력 영역을 채우도록 늘어나지 않도록 설정 됩니다.  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMNoStretchExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/StretchExample.xaml#graphicsmmnostretchexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMNoStretchExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/StretchExample.cs#graphicsmmnostretchexample)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMNoStretchExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/stretchexample.vb#graphicsmmnostretchexample)]  
  
 기본적으로 <xref:System.Windows.Media.TileBrush> 단일 타일 (기본 타일)를 생성 하 고을 출력 영역을 완전히 채우도록 해당 타일을 확장 합니다. 설정 하 여 기본 타일의 위치와 크기를 변경할 수 있습니다 합니다 <xref:System.Windows.Media.TileBrush.Viewport%2A> 고 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 속성입니다.  
  
<a name="basetilesize"></a>   
### <a name="base-tile-size"></a>기본 타일 크기  
 <xref:System.Windows.Media.TileBrush.Viewport%2A> 크기와 기본 타일의 위치를 결정 하는 속성 및 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 속성에 따라 결정 하는지 여부를 <xref:System.Windows.Media.TileBrush.Viewport%2A> 절대 또는 상대 좌표를 사용 하 여 지정 됩니다. 상대 좌표인 경우 출력 영역의 크기를 기준으로 합니다. 점 (0,0)은 출력 영역의 왼쪽 위 구석을 나타내고 (1,1)은 출력 영역의 오른쪽 아래 구석을 나타냅니다. 지정 하는 합니다 <xref:System.Windows.Media.TileBrush.Viewport%2A> 절대 좌표를 사용 하는 속성을 설정 합니다 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 속성을 <xref:System.Windows.Media.BrushMappingMode.Absolute>입니다.  
  
 다음 그림에서는 간 출력 차이 보여 줍니다.는 <xref:System.Windows.Media.TileBrush> 절대 및 상대 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A>합니다. 각 그림은 바둑판식 배열 패턴을 보여 줍니다. 다음 섹션에서는 바둑판식 배열 패턴을 지정하는 방법을 설명합니다.  
  
 ![절대 및 상대 뷰포트 단위](./media/absolute-and-relative-viewports.png "absolute_and_relative_viewports")  
  
 다음 예제에서는 이미지를 사용하여 너비 및 높이가 50%인 타일을 만듭니다. 기본 타일은 출력 영역의 (0,0) 위치에 있습니다.  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMRelativeViewportUnitsExample1](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileSizeExample.xaml#graphicsmmrelativeviewportunitsexample1)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMRelativeViewportUnitsExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/TileSizeExample.cs#graphicsmmrelativeviewportunitsexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMRelativeViewportUnitsExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/tilesizeexample.vb#graphicsmmrelativeviewportunitsexample1)]  
  
 다음 예제에서는 설정의 타일을 <xref:System.Windows.Media.ImageBrush> 25x25 장치 독립적 픽셀을 합니다. 때문에 합니다 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 은 절대는 <xref:System.Windows.Media.ImageBrush> 타일은 항상 25 x 25 픽셀 그려지는 영역의 크기에 관계 없이 합니다.  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMAbsoluteViewportUnitsExample1](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TileSizeExample.xaml#graphicsmmabsoluteviewportunitsexample1)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMAbsoluteViewportUnitsExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/TileSizeExample.cs#graphicsmmabsoluteviewportunitsexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMAbsoluteViewportUnitsExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/tilesizeexample.vb#graphicsmmabsoluteviewportunitsexample1)]  
  
<a name="tilingbehavior"></a>   
### <a name="tiling-behavior"></a>바둑판식 배열 동작  
 A <xref:System.Windows.Media.TileBrush> 기본 타일 완전히 채우지는 못하고 출력 영역을 바둑판식 배열 모드가 이외의 경우에 바둑판식 배열된 패턴을 생성 <xref:System.Windows.Media.TileMode.None> 지정 됩니다. 완전히 타일 브러시의 타일이 출력 영역을 채우지 않고 때 해당 <xref:System.Windows.Media.TileBrush.TileMode%2A> 속성 및 여부를 지정 기본 타일이 출력 영역을 채우도록 복제 해야 할 그렇다면 어떻게 기본 타일을 복제 하는 합니다. 합니다 <xref:System.Windows.Media.TileBrush.TileMode%2A> 속성으로 정의 하는 다음 값을 허용 합니다 <xref:System.Windows.Media.TileMode> 열거형:  
  
- <xref:System.Windows.Media.TileMode.None>: 기본 타일만이 그려집니다.  
  
- <xref:System.Windows.Media.TileMode.Tile>: 기본 타일이 그려지고 나머지 영역은 반복 하 여 기본 타일 한 타일의 오른쪽 가장자리는 다음의 왼쪽된 가장자리에 인접 한 마찬가지로 아래 및 위의 채워집니다.  
  
- <xref:System.Windows.Media.TileMode.FlipX>: 동일 <xref:System.Windows.Media.TileMode.Tile>, 타일의 대체 열이 좌우로 있지만.  
  
- <xref:System.Windows.Media.TileMode.FlipY>: 동일 <xref:System.Windows.Media.TileMode.Tile>, 타일의 대체 행이 상하로 있지만.  
  
- <xref:System.Windows.Media.TileMode.FlipXY>: <xref:System.Windows.Media.TileMode.FlipX> 및 <xref:System.Windows.Media.TileMode.FlipY>의 조합입니다.  
  
 다음 이미지는 여러 다른 바둑판식 배열 모드를 보여 줍니다.  
  
 ![여러 TileBrush TileMode 설정](./media/img-mmgraphics-tilemodes.gif "img_mmgraphics_tilemodes")  
  
 다음 예제에서는 이미지를 사용하여 너비 및 높이가 100x100픽셀인 사각형을 그립니다. 브러시의을 설정 하 여 <xref:System.Windows.Media.TileBrush.Viewport%2A> 설정한 브러시의 기본 타일이 출력 영역의 1/4로 수행 되 0,0,0.25,0.25, 하 합니다. 브러시 <xref:System.Windows.Media.TileBrush.TileMode%2A> 로 설정 된 <xref:System.Windows.Media.TileMode.FlipXY>합니다. 이를 통해 타일 행으로 사각형이 채워집니다.  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMFlipXYExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/TilingExample.xaml#graphicsmmflipxyexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMFlipXYExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/TilingExample.cs#graphicsmmflipxyexample)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMFlipXYExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/tilingexample.vb#graphicsmmflipxyexample)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.ImageBrush>
- <xref:System.Windows.Media.DrawingBrush>
- <xref:System.Windows.Media.VisualBrush>
- <xref:System.Windows.Media.TileBrush>
- [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)
- [방법 항목](brushes-how-to-topics.md)
- [Freezable 개체 개요](../advanced/freezable-objects-overview.md)
- [ImageBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160005)
- [VisualBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160049)
