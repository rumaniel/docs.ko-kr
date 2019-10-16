---
title: 브러시 변환 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], transformation properties
- properties [WPF], transformation
- transformation properties of brushes [WPF]
ms.assetid: 8b9bfc09-12fd-4cd5-b445-99949f27bc39
ms.openlocfilehash: 39b3ad9bebfc56002f77ad6e9026a4446c95455b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62020678"
---
# <a name="brush-transformation-overview"></a>브러시 변환 개요
Brush 클래스는 두 개의 변환 속성을 제공 합니다. <xref:System.Windows.Media.Brush.Transform%2A> 고 <xref:System.Windows.Media.Brush.RelativeTransform%2A>입니다. 이러한 속성을 사용하여 브러시의 콘텐츠를 회전, 비율 크기 조정, 기울이기 및 변환할 수 있습니다. 이 항목에서는 이러한 두 속성 간의 차이점을 설명하고 사용 예제를 제공합니다.  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목을 이해하려면 변환하는 브러시의 기능을 이해해야 합니다. 에 대 한 <xref:System.Windows.Media.LinearGradientBrush> 하 고 <xref:System.Windows.Media.RadialGradientBrush>를 참조 합니다 [단색 및 그라데이션 개요 그리기](painting-with-solid-colors-and-gradients-overview.md)합니다. 에 대 한 <xref:System.Windows.Media.ImageBrush>, <xref:System.Windows.Media.DrawingBrush>, 또는 <xref:System.Windows.Media.VisualBrush>를 참조 하십시오 [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)합니다. [변환 개요](transforms-overview.md)에 설명된 2D 변환에도 익숙해야 합니다.  
  
<a name="transformversusrelativetransform"></a>   
## <a name="differences-between-the-transform-and-relativetransform-properties"></a>Transform 및 RelativeTransform 속성 간 차이점  
 브러시의에 변환을 적용할 때 <xref:System.Windows.Media.Brush.Transform%2A> 가운데를 중심으로 브러시 콘텐츠를 변환 하려는 경우 그려지는 영역의 크기를 알아야 할 속성입니다. 그려지는 영역의 디바이스 독립적 픽셀 크기를 너비 200, 높이 150으로 가정합니다.  사용 하는 경우는 <xref:System.Windows.Media.RotateTransform> 가운데를 중심으로 45도 출력 브러시를 회전 하려면를 지정 합니다 <xref:System.Windows.Media.RotateTransform> 는 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 100 및 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 75.  
  
 브러시의에 변환을 적용할 때 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 속성을 해당 출력이 그려지는 영역에 매핑되기 전에 해당 변환 브러시에 적용 됩니다. 다음 목록에서는 브러시 콘텐츠가 처리되고 변환되는 순서를 보여 줍니다.  
  
1. 브러시의 콘텐츠를 처리합니다. 에 대 한는 <xref:System.Windows.Media.GradientBrush>, 즉, 그라데이션 영역을 결정 합니다. 에 대 한는 <xref:System.Windows.Media.TileBrush>는 <xref:System.Windows.Media.TileBrush.Viewbox%2A> 매핑되는 <xref:System.Windows.Media.TileBrush.Viewport%2A>합니다. 이것이 브러시의 출력이 됩니다.  
  
2. 브러시의 출력을 1 x 1 변환 사각형에 프로젝션합니다.  
  
3. 브러시의 적용 <xref:System.Windows.Media.Brush.RelativeTransform%2A>하나 포함 된 경우.  
  
4. 변환된 출력을 그릴 영역에 프로젝션합니다.  
  
5. 브러시의 적용 <xref:System.Windows.Media.Transform>하나 포함 된 경우.  
  
 때문에 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 브러시의 출력이 1 x 1 사각형을 변환 중심에 매핑되고 오프셋된 값이 상대적인 것으로 표시 하는 동안 적용 됩니다. 예를 들어, 사용 하는 경우를 <xref:System.Windows.Media.RotateTransform> 가운데를 중심으로 45도 출력 브러시를 회전 하려면를 지정 합니다 <xref:System.Windows.Media.RotateTransform> 를 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 0.5의 및 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 0.5의 합니다.  
  
 다음 그림에서는를 사용 하 여 45도 회전 된 일부 브러시의 출력을 보여 줍니다.는 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 고 <xref:System.Windows.Media.Brush.Transform%2A> 속성입니다.  
  
 ![RelativeTransform 및 Transform 속성](./media/graphicsmm-brushrelativetransform-transform-small.png "graphicsmm_brushrelativetransform_transform_small")  
  
<a name="relativetransformandtilebrush"></a>   
## <a name="using-relativetransform-with-a-tilebrush"></a>TileBrush에서 RelativeTransform 사용  
 타일 브러시는 다른 브러시 보다 더 복잡 한 이기 때문에 적용 된 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 하나에 예기치 않은 결과가 발생할 수 있습니다. 예를 들어 다음 이미지를 살펴보세요.  
  
 ![소스 이미지](./media/graphicsmm-reltransform-1-original-image.jpg "graphicsmm_reltransform_1_original_image")  
  
 다음 예제에서는 <xref:System.Windows.Media.ImageBrush> 하려면 이전 이미지를 사용 하 여 사각형 영역을 그립니다. 적용 되는 <xref:System.Windows.Media.RotateTransform> 에 <xref:System.Windows.Media.ImageBrush> 개체의 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 속성 집합과 해당 <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성을 <xref:System.Windows.Media.Stretch.UniformToFill>, 완전히 사각형을 채우는 데 늘 이면 이미지의 가로 세로 비율을 유지 해야 하는.  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMRelativeTransformExample2Inline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/RelativeTransformIllustration.xaml#graphicsmmrelativetransformexample2inline)]  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
 ![변환된 출력](./media/graphicsmm-reltransform-6-output.png "graphicsmm_reltransform_6_output")  
  
 이미지가 왜곡 됩니다, 경우에 확인 브러시 <xref:System.Windows.Media.TileBrush.Stretch%2A> 로 설정 된 <xref:System.Windows.Media.Stretch.UniformToFill>합니다. 브러시의 뒤에 상대 변형 적용 되기 때문에 이것이 <xref:System.Windows.Media.TileBrush.Viewbox%2A> 매핑되는 <xref:System.Windows.Media.TileBrush.Viewport%2A>합니다. 다음 목록에서는 프로세스의 각 단계를 설명합니다.  
  
1. 브러시의 내용을 프로젝트 (<xref:System.Windows.Media.TileBrush.Viewbox%2A>) 기본 타일 (<xref:System.Windows.Media.TileBrush.Viewport%2A>) 브러시를 사용 하 여 <xref:System.Windows.Media.TileBrush.Stretch%2A> 설정 합니다.  
  
     ![Viewbox를 뷰포트에 맞게 늘이기](./media/graphicsmm-reltransform-2-viewbox-to-viewport.png "graphicsmm_reltransform_2_viewbox_to_viewport")  
  
2. 기본 타일을 1 x 1 변환 사각형에 프로젝션합니다.  
  
     ![뷰포트를 변환 사각형에 매핑](./media/graphicsmm-reltransform-3-output-to-transform.png "graphicsmm_reltransform_3_output_to_transform")  
  
3. 적용 된 <xref:System.Windows.Media.RotateTransform>합니다.  
  
     ![상대 변환 적용](./media/graphicsmm-reltransform-4-transform-rotate.png "graphicsmm_reltransform_4_transform_rotate")  
  
4. 변환된 기본 타일을 그릴 영역에 프로젝션합니다.  
  
     ![변환된 브러시를 출력 영역으로 프로젝션](./media/graphicsmm-reltransform-5-transform-to-output.png "graphicsmm_reltransform_5_transform_to_output")  
  
<a name="rotateexample"></a>   
## <a name="example-rotate-an-imagebrush-45-degrees"></a>예제: ImageBrush 회전 45도  
 적용 하는 다음 예제는 <xref:System.Windows.Media.RotateTransform> 에 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 의 속성은 <xref:System.Windows.Media.ImageBrush>합니다. 합니다 <xref:System.Windows.Media.RotateTransform> 개체의 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 고 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 속성이 모두 설정 0.5로 콘텐츠 중심의 상대 좌표 지점입니다. 결과적으로 브러시 콘텐츠는 중심을 기준으로 회전합니다.  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushrelativetransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushrelativetransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushrelativetransformexample)]  
  
 다음 예제에서는 적용 됩니다는 <xref:System.Windows.Media.RotateTransform> 에 <xref:System.Windows.Media.ImageBrush>, 같지만 <xref:System.Windows.Media.Brush.Transform%2A> 속성 대신는 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 속성. 브러시의 중심을 회전 하는 <xref:System.Windows.Media.RotateTransform> 개체의 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 고 <xref:System.Windows.Media.RotateTransform.CenterY%2A> 를 절대 좌표로 설정 해야 합니다. 브러시에 의해 그려지는 사각형은 175 x 90 픽셀이기 때문에 중심점은 (87.5, 45)입니다.  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushtransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushtransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushtransformexample)]  
  
 다음 그림과 브러시에 적용할 변환으로 변환 없이 <xref:System.Windows.Media.Brush.RelativeTransform%2A> 속성을 적용할 변환이 <xref:System.Windows.Media.Brush.Transform%2A> 속성입니다.  
  
 ![Brush RelativeTransform 및 Transform 설정](./media/wcpsdk-graphicsmm-transformandrelativetransform.png "wcpsdk_graphicsmm_transformandrelativetransform")  
  
 이 예제는 더 큰 샘플의 일부입니다. 전체 샘플을 보려면 [브러시 샘플](https://go.microsoft.com/fwlink/?LinkID=159973)을 참조하세요. 브러시에 대한 자세한 내용은 [WPF 브러시 개요](wpf-brushes-overview.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Brush.Transform%2A>
- <xref:System.Windows.Media.Brush.RelativeTransform%2A>
- <xref:System.Windows.Media.Transform>
- <xref:System.Windows.Media.Brush>
- [단색 및 그라데이션을 사용한 그리기 개요](painting-with-solid-colors-and-gradients-overview.md)
- [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)
- [Transform 개요](transforms-overview.md)
