---
title: '방법: 복합 도형 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- shapes [WPF], composite
- composite shapes [WPF]
- graphics [WPF], composite shapes
ms.assetid: 8e5c7ef4-d7ed-4c43-afc9-ca01325c300b
ms.openlocfilehash: de9f7972c7a51ea623c3630fe62bb48f6109317e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052900"
---
# <a name="how-to-create-a-composite-shape"></a>방법: 복합 도형 만들기
이 예제에 사용 하 여 복합 셰이프를 만드는 방법을 보여 줍니다 <xref:System.Windows.Media.Geometry> 개체 및 표시를 사용 하 여를 <xref:System.Windows.Shapes.Path> 요소입니다. 다음 예에서 <xref:System.Windows.Media.LineGeometry>, <xref:System.Windows.Media.EllipseGeometry>, 및 <xref:System.Windows.Media.RectangleGeometry> 사용 되는 <xref:System.Windows.Media.GeometryGroup> 복합 도형 만들기를 합니다. 사용 하 여 하 도형이 그려지는 다음을 <xref:System.Windows.Shapes.Path> 요소입니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[GeometrySample#19](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#19)]  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#CompositeShapeCodeExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/CompositeShapeExample.cs#compositeshapecodeexampleinline1)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#CompositeShapeCodeExampleInline1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/compositeshapeexample.vb#compositeshapecodeexampleinline1)]  
  
 다음 그림은 이전 예제에서 만든 도형을 보여 줍니다.  
  
 ![GeometryGroup을 사용 하 여 만든 복합 기 하 도형을](./media/wcpsdk-graphicsmm-compositegeometryexample1.jpg "wcpsdk_graphicsmm_compositegeometryexample1")  
복합 기 하 도형  
  
 사용 하 여 곡선된 세그먼트를 사용 하 여 도형 다각형 등 보다 복잡 한 도형을 만들 수는 <xref:System.Windows.Media.PathGeometry>합니다. 사용 하 여 도형을 만드는 방법을 보여 주는 예제는 <xref:System.Windows.Media.PathGeometry>를 참조 하세요 [PathGeometry를 사용 하 여 도형 만들기](how-to-create-a-shape-by-using-a-pathgeometry.md)합니다.  이 예제에서 사용 하 여 화면 모양을 렌더링 하지만 <xref:System.Windows.Shapes.Path> 요소인 <xref:System.Windows.Media.Geometry> 개체의 내용을 설명 하기 위해 사용할 수도 있습니다는 <xref:System.Windows.Media.GeometryDrawing> 또는 <xref:System.Windows.Media.DrawingContext>합니다. 자르기 및 적중 테스트에 사용할 수도 있습니다.  
  
 이 예제는 더 큰 샘플에 속합니다. 전체 샘플을 보려면 [기하 도형 샘플](https://go.microsoft.com/fwlink/?LinkID=159989)을 참조하세요.
