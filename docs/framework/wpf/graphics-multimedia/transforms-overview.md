---
title: Transform 개요
ms.date: 03/30/2017
helpviewer_keywords:
- transformations [WPF], about transformations
- classes [WPF], 2-D transform
- transform classes [WPF], 2-D
- 2-D transform classes
- FrameworkElement objects [WPF], rotating
- FrameworkElement objects [WPF], skewing
- FrameworkElement objects [WPF], translating
- Transforms [WPF], about Transforms
- FrameworkElement objects [WPF], scaling
ms.assetid: 8f153d5e-ed61-4aa5-a7cd-286f0c427a13
ms.openlocfilehash: 89b781d3e5b88a66598a301a1d08cf7dfedd57a5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962895"
---
# <a name="transforms-overview"></a>Transform 개요
이 항목에서는 2 차원 <xref:System.Windows.Media.Transform> 클래스를 사용 하 여 개체를 회전, 크기 조정, 이동 (변환) 및 기울이기 <xref:System.Windows.FrameworkElement> 하는 방법에 대해 설명 합니다.  

<a name="whatIsATransformSection"></a>   
## <a name="what-is-a-transform"></a>변환이란?  
 는 <xref:System.Windows.Media.Transform> 한 좌표 공간에서 다른 좌표 공간으로 요소를 매핑하거나 변형 하는 방법을 정의 합니다. 이 매핑은 세 개의 <xref:System.Windows.Media.Matrix> <xref:System.Double> 값 열이 있는 세 개의 행 컬렉션인 변환으로 설명 됩니다.  
  
> [!NOTE]
> Windows Presentation Foundation (WPF)는 행 중심 매트릭스를 사용 합니다. 벡터는 열 벡터가 아니라 행 벡터로 표시됩니다.  
  
 다음 표에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 행렬의 구조를 보여 줍니다.  
  
### <a name="a-2-d-transformation-matrix"></a>2차원 변형 행렬  
  
||||  
|-|-|-|  
|<xref:System.Windows.Media.Matrix.M11%2A><br /><br /> 기본값: 1.0|<xref:System.Windows.Media.Matrix.M12%2A><br /><br /> 기본값: 0.0|0.0|  
|<xref:System.Windows.Media.Matrix.M21%2A><br /><br /> 기본값: 0.0|<xref:System.Windows.Media.Matrix.M22%2A><br /><br /> 기본값: 1.0|0.0|  
|<xref:System.Windows.Media.Matrix.OffsetX%2A><br /><br /> 기본값: 0.0|<xref:System.Windows.Media.Matrix.OffsetY%2A><br /><br /> 기본값: 0.0|1.0|  
  
 행렬 값을 조작하여 개체를 회전, 크기 조정, 기울이기 및 이동(변환)할 수 있습니다. 예를 들어 세 번째 행의 첫 번째 열 ( <xref:System.Windows.Media.Matrix.OffsetX%2A> 값)에 있는 값을 100로 변경 하는 경우이 값을 사용 하 여 x 축을 따라 개체 100 단위를 이동할 수 있습니다. 두 번째 행의 두 번째 열에 있는 값을 3으로 변경하는 경우 이를 사용하여 개체를 현재 높이의 3배로 늘릴 수 있습니다. 두 값을 모두 변경하는 경우 x축을 따라 100개 단위씩 개체가 이동되고 높이가 3배로 늘어납니다. Windows Presentation Foundation (WPF)는 상관 변환만 지원 하기 때문에 오른쪽 열의 값은 항상 0, 0, 1입니다.  
  
 Windows Presentation Foundation (WPF)를 사용 하면 행렬 값을 직접 조작할 수 있지만 기본 행렬 구조가 <xref:System.Windows.Media.Transform> 구성 된 방식을 몰라도 개체를 변환할 수 있는 몇 가지 클래스도 제공 됩니다. 예를 <xref:System.Windows.Media.ScaleTransform> 들어 클래스를 사용 하면 변형 행렬을 조작 하는 대신 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 및 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 속성을 설정 하 여 개체의 크기를 조정할 수 있습니다. 마찬가지로 <xref:System.Windows.Media.RotateTransform> 클래스를 사용 하면 <xref:System.Windows.Media.RotateTransform.Angle%2A> 속성을 설정 하기만 하면 개체를 회전할 수 있습니다.  
  
<a name="transformClassesSection"></a>   
## <a name="transform-classes"></a>변환 클래스  
 WPF (Windows Presentation Foundation)는 일반적인 변환 작업에 대해 <xref:System.Windows.Media.Transform> 다음과 같은 2 차원 클래스를 제공 합니다.  
  
|클래스|Description|예제|그림|  
|-----------|-----------------|-------------|------------------|  
|<xref:System.Windows.Media.RotateTransform>|지정 <xref:System.Windows.Media.RotateTransform.Angle%2A>된로 요소를 회전 합니다.|[개체 회전](how-to-rotate-an-object.md)|![회전 그림](./media/graphicsmm-thumbnails-rotate.png "graphicsmm_thumbnails_rotate")|  
|<xref:System.Windows.Media.ScaleTransform>|지정 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 된 및 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 양만큼 요소의 크기를 조정 합니다.|[요소 배율 조정](how-to-scale-an-element.md)|![배율 조정 그림](./media/graphicsmm-thumbnails-scale.png "graphicsmm_thumbnails_scale")|  
|<xref:System.Windows.Media.SkewTransform>|지정 <xref:System.Windows.Media.SkewTransform.AngleX%2A> 된 및 <xref:System.Windows.Media.SkewTransform.AngleY%2A> 양만큼 요소를 기울입니다.|[요소 기울이기](how-to-skew-an-element.md)|![기울이기 그림](./media/graphicsmm-thumbnails-skew.png "graphicsmm_thumbnails_skew")|  
|<xref:System.Windows.Media.TranslateTransform>|요소를 지정 <xref:System.Windows.Media.TranslateTransform.X%2A> 된 및 <xref:System.Windows.Media.TranslateTransform.Y%2A> 양만큼 이동 (변환) 합니다.|[요소 변환](how-to-translate-an-element.md)|![변환 그림](./media/graphicsmm-thumbnails-translate.png "graphicsmm_thumbnails_translate")|  
  
 더 복잡 한 변환을 만들기 위해 Windows Presentation Foundation (WPF)는 다음과 같은 두 가지 클래스를 제공 합니다.  
  
|클래스|Description|예제|  
|-----------|-----------------|-------------|  
|<xref:System.Windows.Media.TransformGroup>|여러 <xref:System.Windows.Media.TransformGroup> 개체를 단일 <xref:System.Windows.Media.Transform> 로 그룹화 한 다음이를 변환 속성에 적용할 수 있습니다.|[개체에 다중 변환 적용](how-to-apply-multiple-transforms-to-an-object.md)|  
|<xref:System.Windows.Media.MatrixTransform>|다른 <xref:System.Windows.Media.Transform> 클래스에서 제공 하지 않는 사용자 지정 변환을 만듭니다. 을 <xref:System.Windows.Media.MatrixTransform>사용 하는 경우 행렬을 직접 조작 합니다.|[MatrixTransform을 사용하여 사용자 지정 변환 만들기](how-to-use-a-matrixtransform-to-create-custom-transforms.md)|  
  
 WPF (Windows Presentation Foundation)도 3 차원 변환을 제공 합니다. 자세한 내용은 <xref:System.Windows.Media.Media3D.Transform3D> 클래스를 참조하세요.  
  
<a name="transformationproperties"></a>   
## <a name="common-transformation-properties"></a>사용자 지정 변환 속성  
 개체를 변환 하는 한 가지 방법은 적절 한 <xref:System.Windows.Media.Transform> 형식을 선언 하 고 개체의 변환 속성에 적용 하는 것입니다. 개체의 형식이 다르면 변환 속성 형식도 다릅니다. 다음 표에서는 자주 사용 하는 몇 가지 Windows Presentation Foundation (WPF) 형식과 해당 변환 속성을 보여 줍니다.  
  
|형식|변환 속성|  
|----------|-------------------------------|  
|<xref:System.Windows.Media.Brush>|<xref:System.Windows.Media.Brush.Transform%2A>, <xref:System.Windows.Media.Brush.RelativeTransform%2A>|  
|<xref:System.Windows.Media.ContainerVisual>|<xref:System.Windows.Media.ContainerVisual.Transform%2A>|  
|<xref:System.Windows.Media.DrawingGroup>|<xref:System.Windows.Media.DrawingGroup.Transform%2A>|  
|<xref:System.Windows.FrameworkElement>|<xref:System.Windows.UIElement.RenderTransform%2A>, <xref:System.Windows.FrameworkElement.LayoutTransform%2A>|  
|<xref:System.Windows.Media.Geometry>|<xref:System.Windows.Media.Geometry.Transform%2A>|  
|<xref:System.Windows.Media.TextEffect>|<xref:System.Windows.Media.TextEffect.Transform%2A>|  
|<xref:System.Windows.UIElement>|<xref:System.Windows.UIElement.RenderTransform%2A>|  
  
<a name="transformcenter"></a>   
## <a name="transformations-and-coordinate-systems"></a>변환 및 좌표계  
 개체를 변환하는 경우 개체만 단지 변환하는 것이 아니라 개체가 있는 좌표 공간을 변환하게 됩니다. 기본적으로 변환은 대상 개체 좌표계의 원점 가운데에 배치 됩니다. (0, 0). 유일한 예외는 이며 <xref:System.Windows.Media.TranslateTransform>,은 <xref:System.Windows.Media.TranslateTransform> 가운데에 배치 된 위치에 관계 없이 변환 효과가 동일 하기 때문에 설정 해야 하는 중심 속성이 없습니다.  
  
 다음 예제에서는를 <xref:System.Windows.Media.RotateTransform> 사용 하 여 기본 중심 (0, 0)에 대해 <xref:System.Windows.Shapes.Rectangle> <xref:System.Windows.FrameworkElement>요소를 45 각도로 회전 합니다. 다음 그림에서는 회전의 결과를 보여 줍니다.  
  
 ![0, 0 &#40;&#41; 에 대해 45도 회전 한 FrameworkElement](./media/graphicsmm-fe-rotated-about-upperleft-corner.png "graphicsmm_FE_rotated_about_upperleft_corner")  
점 (0,0)을 기준으로 45도 회전된 Rectangle 요소  
  
 [!code-xaml[Transforms_snip#TransformsFERotatedAboutTopLeft](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/CoordinateSystemExample.xaml#transformsferotatedabouttopleft)]  
  
 기본적으로 요소는 왼쪽 위 구석 (0,0)을 기준으로 회전합니다. , <xref:System.Windows.Media.RotateTransform> 및클래스<xref:System.Windows.Media.SkewTransform> 는 변환이 적용 되는 지점을 지정할 수 있는 system.windows.media.rotatetransform.centerx 및 system.windows.media.rotatetransform.centery 속성을 제공 합니다. <xref:System.Windows.Media.ScaleTransform>  
  
 또한 다음 예제에서는 <xref:System.Windows.Media.RotateTransform> 를 사용 하 여 요소를 <xref:System.Windows.Shapes.Rectangle> 45 각도로 회전 합니다. <xref:System.Windows.Media.RotateTransform.CenterX%2A> 그러나 이번에는에 <xref:System.Windows.Media.RotateTransform.CenterY%2A> <xref:System.Windows.Media.RotateTransform> (25, 25)의 중심이 있도록 및 속성이 설정 되어 있습니다. 다음 그림에서는 회전의 결과를 보여 줍니다.  
  
 ![45도 &#40;(25, 25&#41; )로 회전 된 기 하 도형](./media/graphicsmm-fe-rotated-about-center.png "graphicsmm_FE_rotated_about_center")  
점 (25, 25)를 기준으로 45도 회전된 Rectangle 요소  
  
 [!code-xaml[Transforms_snip#TransformsFERotatedAboutCenter](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/CoordinateSystemExample.xaml#transformsferotatedaboutcenter)]  
  
<a name="layoutTransformsAndRenderTransformsSection"></a>   
## <a name="transforming-a-frameworkelement"></a>FrameworkElement 변환  
 에 변환을 <xref:System.Windows.FrameworkElement>적용 하려면를 <xref:System.Windows.Media.Transform> 만들어 클래스에서 <xref:System.Windows.FrameworkElement> 제공 하는 두 속성 중 하나에 적용 합니다.  
  
- <xref:System.Windows.FrameworkElement.LayoutTransform%2A>– 레이아웃 단계 전에 적용 되는 변환입니다. 이 변환을 적용된 후 레이아웃 시스템은 요소의 변환된 크기와 위치를 처리합니다.  
  
- <xref:System.Windows.UIElement.RenderTransform%2A>– 요소의 모양을 수정 하지만 레이아웃 단계가 완료 된 후에 적용 되는 변환입니다. <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 속성 대신 <xref:System.Windows.UIElement.RenderTransform%2A> 속성을 사용 하 여 성능상의 이점을 얻을 수 있습니다.  
  
 어떤 속성을 사용해야 할까요? 제공 되는 성능상의 이점 때문에 가능 하면 특히 <xref:System.Windows.UIElement.RenderTransform%2A> 애니메이션 <xref:System.Windows.Media.Transform> 개체를 사용 하는 경우 속성을 사용 합니다. 크기 조정 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> , 회전 또는 기울이기를 수행 하는 경우에는 속성을 사용 하 고 요소의 부모는 요소의 변환 된 크기로 조정 해야 합니다. <xref:System.Windows.FrameworkElement.LayoutTransform%2A>속성과함께 사용 하는 경우 개체는요소에영향을주지않는<xref:System.Windows.Media.TranslateTransform> 것 처럼 보입니다. 레이아웃 시스템이 변환된 요소를 처리 과정의 일부로 원래 위치로 되돌리기 때문입니다.  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]의 레이아웃에 대한 추가 정보를 보려면 [레이아웃](../advanced/layout.md) 개요를 참조하세요.  
  
<a name="exampleRotateAnElement45degSection"></a>   
## <a name="example-rotate-a-frameworkelement-45-degrees"></a>예제: FrameworkElement 45도 회전  
 다음 예제에서는를 <xref:System.Windows.Media.RotateTransform> 사용 하 여 단추를 시계 방향으로 45도 회전 합니다. 단추는 두 개의 다른 단추가 <xref:System.Windows.Controls.StackPanel> 있는에 포함 되어 있습니다.  
  
 기본적으로는 <xref:System.Windows.Media.RotateTransform> 점 (0, 0)에 대해 회전 합니다. 이 예제에서는 중심 값을 지정하지 않으므로 단추는 왼쪽 위 구석에 해당하는 점 (0,0)에 대해 회전합니다. 는 <xref:System.Windows.Media.RotateTransform> 속성<xref:System.Windows.UIElement.RenderTransform%2A> 에 적용 됩니다. 다음 그림에서는 변환의 결과를 보여 줍니다.  
  
 ![RenderTransform을 사용 하 여 변환 된 단추](./media/graphicsmm-rendertransformwithdefaultcenter.png "graphicsmm_RenderTransformWithDefaultCenter")  
왼쪽 위 구석에서 시계 방향으로 45도 회전  
  
 [!code-xaml[Transforms_snip#GraphicsMMRotateButtonExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample1)]  
  
 또한 다음 예제에서는를 <xref:System.Windows.Media.RotateTransform> 사용 하 여 단추 45도 시계 방향으로 회전 하지만 단추의를 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> (0.5, 0.5)로 설정 합니다. <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 속성의 값은 단추의 크기를 기준으로 합니다. 결과적으로, 회전은 왼쪽 위 구석 대신 단추의 중심에 적용됩니다. 다음 그림에서는 변환의 결과를 보여 줍니다.  
  
 ![가운데를 중심으로 변환 된 단추](./media/graphicsmm-rendertransformrelativecenter.png "graphicsmm_RenderTransformRelativeCenter")  
중심을 기준으로 시계 방향으로 45도 회전  
  
 [!code-xaml[Transforms_snip#GraphicsMMRotateButtonExample2](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample2)]  
  
 다음 예제에서는 <xref:System.Windows.UIElement.RenderTransform%2A> 속성 대신 <xref:System.Windows.FrameworkElement.LayoutTransform%2A> 속성을 사용 하 여 단추를 회전 합니다.  그러면 변환이 단추의 레이아웃에 영향을 미쳐 레이아웃 시스템의 전체 패스를 트리거합니다. 결과적으로 크기가 변경되었기 때문에 단추는 회전한 다음 재배치됩니다. 다음 그림에서는 변환의 결과를 보여 줍니다.  
  
 ![LayoutTransform을 사용 하 여 변환 된 단추](./media/graphicsmm-layouttransform.png "graphicsmm_LayoutTransform")  
단추 회전에 사용된 LayoutTransform  
  
 [!code-xaml[Transforms_snip#GraphicsMMRotateButtonExample3](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample3)]  
  
<a name="animate_transforms"></a>   
## <a name="animating-transformations"></a>변환에 애니메이션 효과 주기  
 <xref:System.Windows.Media.Animation.Animatable> 클래스에서 상속 하기 때문에 클래스에 <xref:System.Windows.Media.Transform> 애니메이션을 적용할 수 있습니다. 에 <xref:System.Windows.Media.Transform>애니메이션 효과를 주려면 애니메이션 효과를 적용할 속성에 호환 되는 형식의 애니메이션을 적용 합니다.  
  
 다음 <xref:System.Windows.Media.Animation.Storyboard> 예제에서는 <xref:System.Windows.Media.Animation.DoubleAnimation> 와 <xref:System.Windows.Media.RotateTransform> 를 사용 하 여를 클릭할 때 <xref:System.Windows.Controls.Button> 회전을 수행 합니다.  
  
 [!code-xaml[Transforms_snip#GraphicsMMAnimatedRotateButtonExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonAnimatedRotateTransformExample.xaml#graphicsmmanimatedrotatebuttonexamplewholepage)]  
  
 전체 샘플을 보려면 [2차원 변환 샘플](https://go.microsoft.com/fwlink/?LinkID=158252)을 참조하세요. 애니메이션에 대한 자세한 내용은 [애니메이션 개요](animation-overview.md)를 참조하세요.  
  
<a name="freezable_features"></a>   
## <a name="freezable-features"></a>Freezable 기능  
 클래스 <xref:System.Windows.Freezable> 는 클래스에서 상속 하기 때문에 클래스는 여러 가지 특수 한 <xref:System.Windows.Media.Transform> 기능을 제공 합니다 <xref:System.Windows.Media.Transform> . 즉, 개체를 [리소스로](../advanced/xaml-resources.md)선언 하 고, 여러 개체 간에 공유 하 고, 읽기 전용으로 설정 하 여 성능을 향상 시키고, 복제할 수 있습니다. 스레드로부터 안전 하 게 구성 됩니다. 개체에서 <xref:System.Windows.Freezable> 제공 하는 다양 한 기능에 대 한 자세한 내용은 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Transform>
- <xref:System.Windows.Media.Matrix>
- [방법 항목](transformations-how-to-topics.md)
- [2차원 변환 샘플](https://go.microsoft.com/fwlink/?LinkID=158252)
