---
title: '방법: 배경으로 사용된 이미지의 가로 세로 비율 유지'
ms.date: 03/30/2017
helpviewer_keywords:
- aspect ratios of background images [WPF], preserving
- brushes [WPF], preserving aspect ratios of background images
- background images [WPF], preserving aspect ratios
ms.assetid: 28c39478-13d7-4011-80a3-8b9cc3e54478
ms.openlocfilehash: 4ae6f1242548038bcd54b7218783e5063fa67872
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61921765"
---
# <a name="how-to-preserve-the-aspect-ratio-of-an-image-used-as-a-background"></a>방법: 배경으로 사용된 이미지의 가로 세로 비율 유지
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.TileBrush.Stretch%2A> 의 속성을 <xref:System.Windows.Media.ImageBrush> 이미지의 가로 세로 비율을 유지 하기 위해.  
  
 기본적으로 사용 하는 경우는 <xref:System.Windows.Media.ImageBrush> 영역을 그리려면, 해당 콘텐츠가 출력 영역을 완전히 확장 합니다. 출력 영역과 이미지의 가로 세로 비율이 다르면 이미지가 확장되면서 왜곡됩니다.  
  
 있도록는 <xref:System.Windows.Media.ImageBrush> 이미지의 가로 세로 비율 유지를 설정 합니다 <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성을 <xref:System.Windows.Media.Stretch.Uniform> 또는 <xref:System.Windows.Media.Stretch.UniformToFill>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 <xref:System.Windows.Media.ImageBrush> 두 개의 사각형을 그릴 개체입니다. 각 사각형은 300 × 150픽셀 크기이며 각각 300 x 300픽셀 이미지를 포함합니다. 합니다 <xref:System.Windows.Media.TileBrush.Stretch%2A> 첫 번째 브러시의 속성이로 설정 되어 <xref:System.Windows.Media.Stretch.Uniform>, 및 <xref:System.Windows.Media.TileBrush.Stretch%2A> 두 번째 브러시의 속성이 <xref:System.Windows.Media.Stretch.UniformToFill>합니다.  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushStretchModesExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/StretchModes.cs#imagebrushstretchmodesexamplewholepage)]  
  
 다음 그림에 나와 있는 첫 번째 브러시의 출력을 <xref:System.Windows.Media.TileBrush.Stretch%2A> 설정은 <xref:System.Windows.Media.Stretch.Uniform>합니다.  
  
 ![Uniform 늘이기를 사용한 ImageBrush](./media/graphicsmm-imagebrushuniformstretch.jpg "graphicsmm_ImageBrushUniformStretch")  
  
 다음 그림에서는 있는 두 번째 브러시의 출력을 <xref:System.Windows.Media.TileBrush.Stretch%2A> 설정 <xref:System.Windows.Media.Stretch.UniformToFill>.  
  
 ![UniformToFill 늘이기를 사용한 ImageBrush](./media/graphicsmm-imagebrushuniformtofillstretch.jpg "graphicsmm_ImageBrushUniformToFillStretch")  
  
 합니다 <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성을 다른 동일 하 게 동작 <xref:System.Windows.Media.TileBrush> 개체, 즉,에 대 한 <xref:System.Windows.Media.DrawingBrush> 및 <xref:System.Windows.Media.VisualBrush>합니다. 에 대 한 자세한 내용은 <xref:System.Windows.Media.ImageBrush> 집합과 <xref:System.Windows.Media.TileBrush> 개체를 참조 하세요 [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)합니다.  
  
 또한 있지만 합니다 <xref:System.Windows.Media.TileBrush.Stretch%2A> 속성이 표시 되도록 하는 방법을 <xref:System.Windows.Media.TileBrush> 콘텐츠가 출력 영역에 맞게 확장, 실제로 지정 하는 방법을 <xref:System.Windows.Media.TileBrush> 콘텐츠 기본 타일에 맞게 늘어납니다. 자세한 내용은 <xref:System.Windows.Media.TileBrush>을 참조하세요.  
  
 이 코드 예제는 제공 된 큰 예제의 일부는 <xref:System.Windows.Media.ImageBrush> 클래스입니다. 전체 샘플을 참조 하세요 [ImageBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160005)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.TileBrush>
- [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)
