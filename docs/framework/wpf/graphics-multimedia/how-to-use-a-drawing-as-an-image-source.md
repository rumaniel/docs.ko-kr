---
title: '방법: Drawing을 이미지 원본으로 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], drawings [WPF], as image sources
- image sources [WPF], drawings
- drawings [WPF], as image sources
ms.assetid: dcf71c7b-9e86-4b8e-8e39-0d0ce0389ef4
ms.openlocfilehash: d4b91a6495e1c54400d5fbfe43b6311d908565a7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769353"
---
# <a name="how-to-use-a-drawing-as-an-image-source"></a>방법: Drawing을 이미지 원본으로 사용
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.Drawing> 으로 <xref:System.Windows.Controls.Image.Source%2A> 에 대 한는 <xref:System.Windows.Controls.Image> 제어 합니다. 표시할를 <xref:System.Windows.Media.Drawing> 사용 하 여는 <xref:System.Windows.Controls.Image> 컨트롤을 사용 하 여를 <xref:System.Windows.Media.DrawingImage> 으로 <xref:System.Windows.Controls.Image> 컨트롤의 <xref:System.Windows.Controls.Image.Source%2A> 설정 합니다 <xref:System.Windows.Media.DrawingImage> 개체의 <xref:System.Windows.Media.DrawingImage.Drawing%2A?displayProperty=nameWithType> 속성을 표시 하려는 그리기.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.DrawingImage> 와 <xref:System.Windows.Controls.Image> 표시할 컨트롤을 <xref:System.Windows.Media.GeometryDrawing>입니다. 이 예제는 다음과 같은 출력을 생성합니다.  
  
 ![타원 두 개의 GeometryDrawing](./media/graphicsmm-geodraw.jpg "graphicsmm_geodraw")  
DrawingImage  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingImageExample.cs#drawingimageexamplewholepage)]
 [!code-xaml[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingImageExample.xaml#drawingimageexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Freezable.Freeze%2A>
- [ImageDrawing을 사용하여 이미지 그리기](how-to-draw-an-image-using-imagedrawing.md)
- [Drawing 개체 개요](drawing-objects-overview.md)
- [Freezable 개체 개요](../advanced/freezable-objects-overview.md)
- [PresentationOptions:Freeze 특성](../advanced/presentationoptions-freeze-attribute.md)
