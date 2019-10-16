---
title: '방법: RectangleGeometry를 사용하여 사각형 정의'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rectangles
- rectangles [WPF], creating with RectangleGeometry class
ms.assetid: e40b8a8e-54b8-416b-a9f2-be6dca9fdf0b
ms.openlocfilehash: 146ca7017ee38ad5c1065e59662ac441e7bfbfe2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61965414"
---
# <a name="how-to-define-a-rectangle-using-a-rectanglegeometry"></a>방법: RectangleGeometry를 사용하여 사각형 정의
이 예제를 사용 하는 방법에 설명 합니다 <xref:System.Windows.Media.RectangleGeometry> 사각형을 설명 하는 클래스입니다.  
  
## <a name="example"></a>예제  
 다음 예제를 만들고 렌더링 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.RectangleGeometry>합니다.  정의 된 상대 위치와 사각형의 크기는 <xref:System.Windows.Rect> 구조입니다. 상대 위치가 `50,50` 높이 너비를 모두 및 `25` 여 정사각형을 만듭니다. 칠할 사각형의 내부를 <xref:System.Windows.Media.Brushes.LemonChiffon%2A> 로 브러시 및 윤곽선을 그리는 <xref:System.Windows.Media.Brushes.Black%2A> 두께의 스트로크 `1`합니다.  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmrectanglegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmrectanglegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmrectanglegeometryexample)]  
  
 ![RectangleGeometry](./media/graphicsmm-rectangle.gif "graphicsmm_rectangle")  
RectangleGeometry  
  
 이 예제에서는 사용 되지만 <xref:System.Windows.Shapes.Path> 요소를 렌더링 하는 <xref:System.Windows.Media.RectangleGeometry>, 여러 가지 다른 방법으로 사용 하도록 <xref:System.Windows.Media.RectangleGeometry> 개체입니다. 예를 들어,를 <xref:System.Windows.Media.RectangleGeometry> 사용을 지정할 수 있습니다 합니다 <xref:System.Windows.UIElement.Clip%2A> 의 <xref:System.Windows.UIElement> 또는 <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> 의 <xref:System.Windows.Media.GeometryDrawing>.  
  
 다른 단순 기 하 도형 클래스를 포함 <xref:System.Windows.Media.LineGeometry> 고 <xref:System.Windows.Media.EllipseGeometry>입니다. 좀더 복잡 한 뿐만 아니라 이러한 기 하이 도형을 만들 수도 있습니다를 사용 하는 <xref:System.Windows.Media.PathGeometry> 또는 <xref:System.Windows.Media.StreamGeometry>합니다.  
  
## <a name="see-also"></a>참고자료

- [Geometry 개요](geometry-overview.md)
- [복합 도형 만들기](how-to-create-a-composite-shape.md)
- [PathGeometry를 사용하여 도형 만들기](how-to-create-a-shape-by-using-a-pathgeometry.md)
