---
title: 이미징 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- metadata [WPF], images
- displaying images [WPF]
- Imaging API [WPF]
- image metadata [WPF]
- converting images [WPF]
- encoding image formats [WPF]
- format decoding for images [WPF]
- painting with images [WPF]
- stretching images [WPF]
- images [WPF], about imaging
- format encoding for images [WPF]
- cropping images [WPF]
- decoding image formats [WPF]
- rotating images [WPF]
ms.assetid: 72aad87a-e6f3-4937-94cd-a18b7766e990
ms.openlocfilehash: f8686a189883bed782cdde80e56c87ab6dbe404a
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835020"
---
# <a name="imaging-overview"></a>이미징 개요
이 항목에서는 [!INCLUDE[TLA#tla_wic](../../../../includes/tlasharptla-wic-md.md)]를 소개합니다. [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]를 사용하여 개발자는 이미지를 표시 및 변환하고 서식을 지정할 수 있습니다.  

## <a name="wpf-imaging-component"></a>WPF Imaging Component  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]에서는 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 내에서 향상된 이미징 기능을 제공합니다. 비트맵을 표시 하거나 공용 컨트롤에서 이미지를 사용 하는 등의 이미징 기능은 이전에 Microsoft Windows 그래픽 장치 인터페이스 (GDI) 또는 Microsoft Windows GDI + 라이브러리에 의존 했습니다. 이러한 API는 기본 이미징 기능을 제공 하지만 코덱 확장성 및 고화질 이미지 지원과 같은 기능을 제공 하지 않습니다. [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]은 GDI 및 GDI +의 단점을 극복 하 고 응용 프로그램 내에서 이미지를 표시 하 고 사용할 수 있는 새로운 API 집합을 제공 하도록 설계 되었습니다.  
  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] API, 관리 되는 구성 요소 및 관리 되지 않는 구성 요소에 액세스 하는 방법에는 두 가지가 있습니다. 관리되지 않는 구성 요소는 다음과 같은 기능을 제공합니다.  
  
- 새롭거나 또는 독자적인 이미지 형식에 대한 확장성 모델  
  
- 비트맵 (BMP), 이미지 JPEG (이동식 네트워크 그래픽), PNG (PNG), 태그가 지정 된 이미지 파일 형식 (TIFF), [!INCLUDE[TLA#tla_wdp](../../../../includes/tlasharptla-wdp-md.md)], GIF (그래픽 교환 형식) 및 아이콘 (.ico)을 포함 하 여 네이티브 이미지 형식에 대 한 성능 및 보안이 향상 되었습니다.  
  
- 채널당 8비트(픽셀당 32비트)까지 높은 비트 수준의 이미지 데이터 보존  
  
- 비파괴 이미지 크기 조정, 자르기 및 회전  
  
- 단순화된 색 관리  
  
- 파일 내 독점 메타데이터에 대한 지원  
  
- 관리되는 구성 요소는 관리되지 않는 인프라를 활용하여 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)], 애니메이션 및 그래픽 등의 기타 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 기능에 이미지를 원활하게 통합할 수 있도록 합니다. 또한 관리 되는 구성 요소는 응용 프로그램에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 새 이미지 형식을 자동으로 인식할 수 있도록 하는 Windows Presentation Foundation (WPF) 이미징 코덱 확장성 모델을 활용 합니다.  
  
 대부분의 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 관리 되는 API는 <xref:System.Windows.Media.Imaging?displayProperty=nameWithType> 네임 스페이스에 상주 하지만, <xref:System.Windows.Media.ImageBrush> 와 <xref:System.Windows.Media.ImageDrawing> 같은 몇 가지 중요 한 형식은 네임 <xref:System.Windows.Media?displayProperty=nameWithType> 스페이스에 상주 <xref:System.Windows.Controls.Image> 하 고에 <xref:System.Windows.Controls?displayProperty=nameWithType> 상주 합니다. 공간.  
  
 이 항목에서는 관리되는 구성 요소에 대한 추가 정보를 제공합니다. 관리 되지 않는 API에 대 한 자세한 내용은 [관리 되지 않는 WPF 이미징 구성 요소](/windows/desktop/wic/-wic-lh) 설명서를 참조 하세요.  
  
<a name="_imageformats"></a>   
## <a name="wpf-image-formats"></a>WPF 이미지 형식  
 코덱은 특정 미디어 형식을 인코딩하거나 디코딩하는 데 사용됩니다. [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]에는 BMP, JPEG, PNG, TIFF, [!INCLUDE[TLA2#tla_wdp](../../../../includes/tla2sharptla-wdp-md.md)], GIF 및 아이콘 이미지 형식에 대 한 코덱이 포함 되어 있습니다. 이러한 각 코덱을 사용하여 애플리케이션은 ICON을 제외한 해당 이미지 형식을 디코딩 및 인코딩할 수 있습니다.  
  
 <xref:System.Windows.Media.Imaging.BitmapSource>는 이미지의 디코딩 및 인코딩에 사용 되는 중요 한 클래스입니다. [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 파이프라인의 기본 구성 요소이며 픽셀의 단일 상수 집합을 특정 크기 및 해상도로 나타냅니다. 는 <xref:System.Windows.Media.Imaging.BitmapSource> 다중 프레임 이미지의 개별 프레임이 될 수도 있고 <xref:System.Windows.Media.Imaging.BitmapSource>에서 수행 되는 변환의 결과일 수도 있습니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 과<xref:System.Windows.Media.Imaging.BitmapFrame>같이 이미징에서 사용 되는 여러 기본 클래스의 부모입니다.  
  
 는 <xref:System.Windows.Media.Imaging.BitmapFrame> 이미지 형식의 실제 비트맵 데이터를 저장 하는 데 사용 됩니다. GIF 및 TIFF와 같은 형식은 이미지 당 여러 프레임을 지원 하지만 많은 이미지 형식은 단일 <xref:System.Windows.Media.Imaging.BitmapFrame>만 지원 합니다. 프레임은 디코더에서 입력 데이터로 사용되고 이미지 파일을 만들기 위해 인코더에 전달됩니다.  
  
 다음 예에서는 <xref:System.Windows.Media.Imaging.BitmapSource>에서 <xref:System.Windows.Media.Imaging.BitmapFrame>을 만든 다음 TIFF 이미지에 추가 하는 방법을 보여 줍니다.  
  
 [!code-csharp[BitmapFrameExample#10](~/samples/snippets/csharp/VS_Snippets_Wpf/BitmapFrameExample/CSharp/BitmapFrame.cs#10)]
 [!code-vb[BitmapFrameExample#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitmapFrameExample/VB/BitmapFrame.vb#10)]  
  
### <a name="image-format-decoding"></a>이미지 형식 디코딩  
 이미지 디코딩은 이미지 형식을 시스템에서 사용할 수 있는 이미지 데이터로 변환하는 것입니다. 그런 후 이미지 데이터를 다른 형식으로 표시, 처리 또는 인코딩할 수 있습니다. 디코더를 선택할 때는 이미지 형식을 고려해야 합니다. 특정 디코더를 지정하지 않으면 코덱이 자동으로 선택됩니다. [WPF로 이미지 표시](#_displayingimages) 섹션의 예제는 자동 디코딩을 보여 줍니다. 관리되지 않는 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 인터페이스를 사용하여 개발하고 시스템에 등록된 사용자 지정 형식 디코더는 디코더 선택 항목에 자동으로 포함됩니다. 이를 통해 사용자 지정 형식이 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 애플리케이션에 자동으로 표시될 수 있습니다.  
  
 다음 예제에서는 비트맵 디코더를 사용 하 여 BMP 형식 이미지를 디코딩하는 방법을 보여 줍니다.  
  
 [!code-cpp[BmpBitmapDecoderEncoder#5](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#5)]
 [!code-csharp[BmpBitmapDecoderEncoder#5](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#5)]
 [!code-vb[BmpBitmapDecoderEncoder#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#5)]  
  
### <a name="image-format-encoding"></a>이미지 형식 인코딩  
 이미지 인코딩은 이미지 데이터를 특정 이미지 형식으로 변환하는 것입니다. 인코딩된 이미지 데이터는 새 이미지 파일을 만드는 데 사용할 수 있습니다. [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]에서는 위에 설명된 각 이미지 형식에 대한 인코더를 제공합니다.  
  
 다음 예제에서는 인코더를 사용하여 새로 만든 비트맵 이미지를 저장하는 방법을 보여 줍니다.  
  
 [!code-cpp[BmpBitmapDecoderEncoder#3](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#3)]
 [!code-csharp[BmpBitmapDecoderEncoder#3](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#3)]
 [!code-vb[BmpBitmapDecoderEncoder#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#3)]  
  
<a name="_displayingimages"></a>   
## <a name="displaying-images-in-wpf"></a>WPF로 이미지 표시  
 Windows Presentation Foundation (WPF) 응용 프로그램에서 이미지를 표시 하는 방법에는 여러 가지가 있습니다. 이미지는 <xref:System.Windows.Controls.Image> 컨트롤을 사용 하 여 표시 하거나를 <xref:System.Windows.Media.ImageBrush>사용 하 여 시각적 개체에서 그리거나를 사용 <xref:System.Windows.Media.ImageDrawing>하 여 그릴 수 있습니다.  
  
### <a name="using-the-image-control"></a>Image 컨트롤 사용  
 <xref:System.Windows.Controls.Image>는 프레임 워크 요소 이며 응용 프로그램에 이미지를 표시 하는 기본 방법입니다. 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]는 <xref:System.Windows.Controls.Image> 특성 구문이 나 속성 구문 등 두 가지 방법으로 사용할 수 있습니다. 다음 예제에서는 특성 구문 및 속성 태그 구문 둘 다를 사용하여 200픽셀 너비의 이미지를 렌더링하는 방법을 보여 줍니다. 특성 구문 및 속성 구문에 대한 자세한 내용은 [종속성 속성 개요](../advanced/dependency-properties-overview.md)를 참조하세요.  
  
 [!code-xaml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
 대부분의 예제에서는 개체를 <xref:System.Windows.Media.Imaging.BitmapImage> 사용 하 여 이미지 파일을 참조 합니다. <xref:System.Windows.Media.Imaging.BitmapImage>는 로드를 <xref:System.Windows.Media.Imaging.BitmapSource> 위해 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 최적화 된 특수 이며 <xref:System.Windows.Controls.Image> 이미지를 컨트롤 <xref:System.Windows.Controls.Image.Source%2A> 의로 표시 하는 쉬운 방법입니다.  
  
 다음 예제에서는 코드를 사용하여 200픽셀 너비의 이미지를 렌더링하는 방법을 보여 줍니다.  
  
> [!NOTE]
> <xref:System.Windows.Media.Imaging.BitmapImage> 구현 된 <xref:System.ComponentModel.ISupportInitialize> 여러 속성에 대해 초기화를 최적화 하는 인터페이스입니다. 개체 초기화 동안에만 속성 변경이 발생할 수 있습니다. 호출 <xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A> 초기화가 시작 되었음을 알리기 위해 및 <xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A> 초기화가 완료 되었음을 알립니다. 일단 초기화되면 속성 변경은 무시됩니다.  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
#### <a name="rotating-converting-and-cropping-images"></a>이미지 회전, 변환 및 자르기  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]<xref:System.Windows.Media.Imaging.BitmapImage> 사용자가 또는와 <xref:System.Windows.Media.Imaging.BitmapSource> <xref:System.Windows.Media.Imaging.CroppedBitmap> 같은추가개체를사용하여또는의속성을사용하여이미지를<xref:System.Windows.Media.Imaging.FormatConvertedBitmap>변환할 수 있습니다. 이러한 이미지 변환은 이미지 크기를 조정 또는 이미지를 회전하거나, 이미지의 픽셀 형식을 변경하거나, 이미지를 잘라낼 수 있습니다.  
  
 이미지 회전은의 <xref:System.Windows.Media.Imaging.BitmapImage.Rotation%2A> <xref:System.Windows.Media.Imaging.BitmapImage>속성을 사용 하 여 수행 됩니다. 회전은 90도 단위로만 수행할 수 있습니다. 다음 예제에서 이미지는 90도 회전됩니다.  
  
 [!code-xaml[ImageElementExample#TransformedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml#transformedxaml2)]  
  
 [!code-csharp[ImageElementExample#TransformedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml.cs#transformedcsharp1)]
 [!code-vb[ImageElementExample#TransformedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/TransformedImageExample.xaml.vb#transformedcsharp1)]  
  
 이미지를 회색조와 같은 다른 픽셀 형식으로 변환 하는 작업은 <xref:System.Windows.Media.Imaging.FormatConvertedBitmap>를 사용 하 여 수행 됩니다. 다음 예제에서 이미지는로 <xref:System.Windows.Media.PixelFormats.Gray4%2A>변환 됩니다.  
  
 [!code-xaml[ImageElementExample_snip#ConvertedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml#convertedxaml2)]  
  
 [!code-csharp[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml.cs#convertedcsharp1)]
 [!code-vb[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/FormatConvertedExample.xaml.vb#convertedcsharp1)]  
  
 이미지를 자르려면 또는 <xref:System.Windows.UIElement.Clip%2A> <xref:System.Windows.Controls.Image> <xref:System.Windows.Media.Imaging.CroppedBitmap> 의 속성 중 하나를 사용할 수 있습니다. 일반적으로 이미지의 일부만 표시 하려면를 <xref:System.Windows.UIElement.Clip%2A> 사용 해야 합니다. 잘린 이미지 <xref:System.Windows.Media.Imaging.CroppedBitmap> 를 인코딩 및 저장 해야 하는 경우를 사용 해야 합니다. 다음 예제에서는를 사용 하 <xref:System.Windows.Media.EllipseGeometry>여 클립 속성을 사용 하 여 이미지를 자릅니다.  
  
 [!code-xaml[ImageElementExample_snip#CroppedXAMLUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml#croppedxamlusingclip1)]  
  
 [!code-csharp[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml.cs#croppedcsharpusingclip1)]
 [!code-vb[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/CroppedImageExample.xaml.vb#croppedcsharpusingclip1)]  
  
#### <a name="stretching-images"></a>이미지 늘이기  
 속성 <xref:System.Windows.Controls.Image.Stretch%2A> 은 이미지가 컨테이너를 채우도록 확장 되는 방식을 제어 합니다. 속성 <xref:System.Windows.Controls.Image.Stretch%2A> 은 <xref:System.Windows.Media.Stretch> 열거형으로 정의 되는 다음 값을 허용 합니다.  
  
- <xref:System.Windows.Media.Stretch.None>: 이미지가 출력 영역을 채우도록 확장 되지 않습니다. 이미지가 출력 영역보다 큰 경우 이미지가 출력 영역으로 그려지고 맞지 않는 부분은 클리핑됩니다.  
  
- <xref:System.Windows.Media.Stretch.Fill>: 이미지가 출력 영역에 맞게 조정 됩니다. 이미지의 높이 및 너비가 독립적으로 조정되므로 이미지의 원래 가로 세로 비율이 유지되지 않을 수 있습니다. 즉, 출력 컨테이너를 완전히 채우도록 이미지를 이동해야 할 수 있습니다.  
  
- <xref:System.Windows.Media.Stretch.Uniform>: 이미지가 출력 영역에 완전히 맞게 조정 됩니다. 이미지의 가로 세로 비율이 유지됩니다.  
  
- <xref:System.Windows.Media.Stretch.UniformToFill>: 이미지의 원래 가로 세로 비율을 유지 하면서 출력 영역을 완전히 채우도록 이미지 크기를 조정 합니다.  
  
 다음 예제에서는 사용 가능한 <xref:System.Windows.Media.Stretch> 각 열거형 <xref:System.Windows.Controls.Image>을에 적용 합니다.  
  
 다음 그림에서는 예제의 출력을 보여 주고, 이미지에 적용 될 때 다른 <xref:System.Windows.Controls.Image.Stretch%2A> 설정에 미치는 영향을 보여 줍니다.  
  
 ![여러 TileBrush Stretch 설정](./media/img-mmgraphics-stretchenum.jpg "img_mmgraphics_stretchenum")  
여러 늘이기 설정  
  
 [!code-xaml[ImageElementExample_snip#ImageStretchExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageStretchExample.xaml#imagestretchexamplewholepage)]  
  
### <a name="painting-with-images"></a>이미지로 그리기  
 이미지는를 <xref:System.Windows.Media.Brush>사용 하 여 그리기로 응용 프로그램에 표시 될 수도 있습니다. 브러시를 사용하여 간단한 단색부터 복잡한 패턴 및 이미지 집합에 이르는 모든 방식으로 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 개체를 그릴 수 있습니다. 이미지로 그리려면를 사용 <xref:System.Windows.Media.ImageBrush>합니다. 는 해당 콘텐츠를 비트맵 <xref:System.Windows.Media.TileBrush> 이미지로 정의 하는의 형식입니다. <xref:System.Windows.Media.ImageBrush> 는 <xref:System.Windows.Media.ImageBrush> 속성<xref:System.Windows.Media.ImageBrush.ImageSource%2A> 으로 지정 된 단일 이미지를 표시 합니다. 이미지를 늘이고, 정렬하고, 바둑판식으로 배열하는 방식을 제어하여 왜곡을 방지하고 패턴 및 기타 효과를 생성할 수 있습니다. 다음 그림에서는를 사용 <xref:System.Windows.Media.ImageBrush>하 여 수행할 수 있는 몇 가지 효과를 보여 줍니다.  
  
 ![ImageBrush 출력 예제](./media/wcpsdk-mmgraphics-imagebrushexamples.gif "wcpsdk_mmgraphics_imagebrushexamples")  
이미지 브러시로 도형, 컨트롤, 텍스트 등을 채울 수 있습니다.  
  
 다음 예제에서는를 <xref:System.Windows.Media.ImageBrush>사용 하 여 이미지를 사용 하 여 단추의 배경을 칠하는 방법을 보여 줍니다.  
  
 [!code-xaml[UsingImageBrush#4](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush/CS/PaintingWithImages.xaml#4)]  
  
 이미지 및 그리기에 <xref:System.Windows.Media.ImageBrush> 대 한 자세한 내용은 [이미지, 그림 및 시각적 표시로 그리기를](painting-with-images-drawings-and-visuals.md)참조 하세요.  
  
<a name="_metadata"></a>   
## <a name="image-metadata"></a>이미지 메타데이터  
 일부 이미지 파일에는 파일의 콘텐츠나 특성을 설명하는 메타데이터가 포함되어 있습니다. 예를 들어 대부분의 디지털 카메라는 이미지를 캡처하는 데 사용되는 카메라의 제조업체와 모델에 대한 메타데이터를 포함하는 이미지를 만듭니다. 각 이미지 형식은 메타데이터를 다르게 처리하지만 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]에서는 지원되는 각 이미지 형식에 대한 메타데이터를 저장하고 검색하는 일관된 방법을 제공합니다.  
  
 메타 데이터에 대 한 액세스는 <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A> <xref:System.Windows.Media.Imaging.BitmapSource> 개체의 속성을 통해 제공 됩니다. <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A>이미지에 <xref:System.Windows.Media.Imaging.BitmapMetadata> 포함 된 모든 메타 데이터를 포함 하는 개체를 반환 합니다. 이 데이터는 하나의 메타데이터 스키마이거나 여러 다른 스키마의 조합일 수 있습니다. [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]은 다음 이미지 메타 데이터 스키마를 지원 합니다. Exchangeable 가능한 이미지 파일 (Exif), 텍스트 (PNG 텍스트 데이터), IFD (이미지 파일 디렉터리), IPTC (국제 누름 Council) 및 [!INCLUDE[TLA#tla_xmp](../../../../includes/tlasharptla-xmp-md.md)]입니다.  
  
 메타 데이터 읽기 프로세스를 간소화 하기 <xref:System.Windows.Media.Imaging.BitmapMetadata> 위해에서는, 및 <xref:System.Windows.Media.Imaging.BitmapMetadata.CameraModel%2A>와 <xref:System.Windows.Media.Imaging.BitmapMetadata.Author%2A>같이 <xref:System.Windows.Media.Imaging.BitmapMetadata.Title%2A>쉽게 액세스할 수 있는 여러 명명 된 속성을 제공 합니다. 이러한 명명된 속성 중 대부분은 메타데이터를 작성하는 데도 사용할 수 있습니다. 메타데이터 읽기에 대한 추가 지원이 메타데이터 쿼리 판독기를 통해 제공됩니다. 메서드 <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> 는 *"/app1/exif/"* 와 같은 문자열 쿼리를 제공 하 여 메타 데이터 쿼리 판독기를 검색 하는 데 사용 됩니다. 다음 예에서는를 <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> 사용 하 여 *"/dext/Description"* 위치에 저장 된 텍스트를 가져옵니다.  
  
 [!code-cpp[BitmapMetadata#GetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#getquery)]
 [!code-csharp[BitmapMetadata#GetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#getquery)]
 [!code-vb[BitmapMetadata#GetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#getquery)]  
  
 메타데이터를 작성하기 위해 메타데이터 쿼리 작성기가 사용됩니다. <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A>쿼리 작성기를 가져오고 원하는 값을 설정 합니다. 다음 예에서는를 <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> 사용 하 여 *"/dext/Description"* 위치에 저장 된 텍스트를 작성 합니다.  
  
 [!code-cpp[BitmapMetadata#SetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#setquery)]
 [!code-csharp[BitmapMetadata#SetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#setquery)]
 [!code-vb[BitmapMetadata#SetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#setquery)]  
  
<a name="_extensibility"></a>   
## <a name="codec-extensibility"></a>코덱 확장성  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]의 핵심 기능은 새로운 이미지 코덱에 대한 확장성 모델입니다. 이러한 관리되지 않는 인터페이스를 통해 코덱 개발자들은 코덱을 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에 통합할 수 있으므로 새로운 이미지 형식이 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 애플리케이션에서 자동으로 사용될 수 있습니다.  
  
 확장성 API에 대 한 샘플은 [Win32 샘플 코덱](https://go.microsoft.com/fwlink/?LinkID=160052)을 참조 하세요. 이 샘플에는 사용자 지정 이미지 형식용 디코더 및 인코더를 만드는 방법을 보여 줍니다.  
  
> [!NOTE]
> 시스템이 코덱을 인식하려면 디지털로 서명되어야 합니다.  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Media.Imaging.BitmapSource>
- <xref:System.Windows.Media.Imaging.BitmapImage>
- <xref:System.Windows.Controls.Image>
- <xref:System.Windows.Media.Imaging.BitmapMetadata>
- [2차원 그래픽 및 이미징](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [Win32 샘플 코덱](https://go.microsoft.com/fwlink/?LinkID=160052)
