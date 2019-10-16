---
title: '방법: GeometryDrawing 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- shapes [WPF], renderable
- renderable shapes [WPF]
- graphics [WPF], GeometryDrawing class
- classes [WPF], GeometryDrawing
ms.assetid: 11d3c096-91ba-4d41-9bba-aeac0db70f97
ms.openlocfilehash: f5cdcfdb68ad8030bcbd6c689f45a8baddd000e1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61904958"
---
# <a name="how-to-create-a-geometrydrawing"></a>방법: GeometryDrawing 만들기
만들고 표시 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.GeometryDrawing>합니다. A <xref:System.Windows.Media.GeometryDrawing> 셰이프를 연결 하 여 채우기 및 윤곽선을 사용 하 여 만들 수 있습니다를 <xref:System.Windows.Media.Pen> 및 <xref:System.Windows.Media.Brush> 사용 하 여는 <xref:System.Windows.Media.Geometry>합니다. <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> 셰이프 구조체에 설명 합니다 <xref:System.Windows.Media.GeometryDrawing.Brush%2A> 도형의 채우기 설명 및 <xref:System.Windows.Media.GeometryDrawing.Pen%2A> 도형의 윤곽선에 설명 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.GeometryDrawing> 셰이프를 렌더링 합니다. 설명 됩니다는 <xref:System.Windows.Media.GeometryGroup> 두 개의 <xref:System.Windows.Media.EllipseGeometry> 개체입니다. 사용 하 여 도형의 내부가 그려지는 <xref:System.Windows.Media.LinearGradientBrush> 윤곽선을 그릴 때 사용 하 고는 <xref:System.Windows.Media.Brushes.Black%2A> <xref:System.Windows.Media.Pen>합니다. 합니다 <xref:System.Windows.Media.GeometryDrawing> 를 사용 하 여 표시 되는 <xref:System.Windows.Media.ImageDrawing> 및 <xref:System.Windows.Controls.Image> 요소입니다.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GeometryDrawingExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GeometryDrawingExample.cs#geometrydrawingexamplewholepage)]
 [!code-xaml[DrawingMiscSnippets_snip#GeometryDrawingExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GeometryDrawingExample.xaml#geometrydrawingexamplewholepage)]  
  
 다음 그림에서는 결과 <xref:System.Windows.Media.GeometryDrawing>합니다.  
  
 ![타원 두 개의 GeometryDrawing](./media/graphicsmm-geodraw.jpg "graphicsmm_geodraw")  
  
 보다 복잡 한 그리기를 만들려면 여러 그리기 개체를 사용 하 여 드로잉을 단일 복합체로 결합할 수 있습니다는 <xref:System.Windows.Media.DrawingGroup>합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.DrawingGroup>
- [Drawing 개체 개요](drawing-objects-overview.md)
- [Geometry 개요](geometry-overview.md)
- [합성 그리기 만들기](how-to-create-a-composite-drawing.md)
