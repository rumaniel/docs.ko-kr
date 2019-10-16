---
title: '방법: LineGeometry를 사용하여 선 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], lines
ms.assetid: 41231b22-1f74-4c26-a8e7-a55b29f8f6bd
ms.openlocfilehash: f8c334a54f78aec7af91064a447fd18f23dcfbdc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61905205"
---
# <a name="how-to-create-a-line-using-a-linegeometry"></a>방법: LineGeometry를 사용하여 선 만들기
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.LineGeometry> 줄을 설명 하는 클래스입니다. <xref:System.Windows.Media.LineGeometry> 시작 및 끝 지점을 사용 하 여 정의 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제를 만들고 렌더링 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.LineGeometry>합니다.  <xref:System.Windows.Shapes.Path> 요소 선을 렌더링 하는 데 사용 됩니다.  선에 영역이 없는 하므로 <xref:System.Windows.Shapes.Path> 개체의 <xref:System.Windows.Shapes.Shape.Fill%2A> 지정 되지 않은 대신를 <xref:System.Windows.Shapes.Shape.Stroke%2A> 및 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 속성을 사용 합니다.  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMLineGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmlinegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmlinegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmlinegeometryexample)]  
  
 ![LineGeometry](./media/graphicsmm-line.gif "graphicsmm_line")  
(10,20)부터 (100,130)까지 그린 LineGeometry  
  
 다른 단순 기 하 도형 클래스를 포함 <xref:System.Windows.Media.LineGeometry> 고 <xref:System.Windows.Media.EllipseGeometry>입니다. 좀더 복잡 한 뿐만 아니라 이러한 기 하이 도형을 만들 수도 있습니다를 사용 하는 <xref:System.Windows.Media.PathGeometry> 또는 <xref:System.Windows.Media.StreamGeometry>합니다. 자세한 내용은 참조는 [기 하 도형 개요](geometry-overview.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [Geometry 개요](geometry-overview.md)
- [복합 도형 만들기](how-to-create-a-composite-shape.md)
- [PathGeometry를 사용하여 도형 만들기](how-to-create-a-shape-by-using-a-pathgeometry.md)
