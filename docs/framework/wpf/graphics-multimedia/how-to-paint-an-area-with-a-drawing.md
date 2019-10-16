---
title: '방법: Drawing으로 영역 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], painting with drawings
- painting [WPF], with drawings
- drawings [WPF], painting with
ms.assetid: c10dc4b1-09b1-41e8-ad14-456b5fb377df
ms.openlocfilehash: 6b204ae631912181333e2559ebadcdc37e7693b7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010087"
---
# <a name="how-to-paint-an-area-with-a-drawing"></a>방법: Drawing으로 영역 그리기
이 예제에서는 그리기로 영역을 그리는 방법을 보여 줍니다. 그리기로 영역 그리기를 사용 하는 <xref:System.Windows.Media.DrawingBrush> 와 하나 이상의 <xref:System.Windows.Media.Drawing> 개체입니다.   다음 예제에서는 <xref:System.Windows.Media.DrawingBrush> 2 개의 타원 그리기로 개체를 그립니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[drawingbrush_snip#DrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_snip/CS/DrawingBrushExample.xaml#drawingbrushexamplewholepage)]  
  
 [!code-csharp[drawingbrush_procedural_snip#DrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_procedural_snip/CSharp/DrawingBrushExample.cs#drawingbrushexamplewholepage)]
 [!code-vb[drawingbrush_procedural_snip#DrawingBrushExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/drawingbrush_procedural_snip/VisualBasic/DrawingBrushExample.vb#drawingbrushexamplewholepage)]  
  
 다음 그림에서는 예제의 출력을 보여 줍니다.  
  
 ![DrawingBrush의 출력](./media/graphicsmm-drawingbrush-simple.png "graphicsmm_drawingbrush_simple")  
  
 (도형의 가운데에 설명 된 이유 때문에 대 한 흰색인 [복합 도형의 채우기 제어](how-to-control-the-fill-of-a-composite-shape.md).)  
  
 설정 하 여는 <xref:System.Windows.Media.DrawingBrush> 개체의 <xref:System.Windows.Media.TileBrush.Viewport%2A> 고 <xref:System.Windows.Media.TileBrush.TileMode%2A> 속성 반복 패턴을 만들 수 있습니다. 다음 예제에서는 2개의 타원 그리기로 만든 패턴으로 개체를 그립니다.  
  
 [!code-xaml[drawingbrush_snip#TiledDrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_snip/CS/TiledDrawingBrushExample.xaml#tileddrawingbrushexamplewholepage)]  
  
 [!code-csharp[drawingbrush_procedural_snip#TiledDrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_procedural_snip/CSharp/TiledDrawingBrushExample.cs#tileddrawingbrushexamplewholepage)]
 [!code-vb[drawingbrush_procedural_snip#TiledDrawingBrushExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/drawingbrush_procedural_snip/VisualBasic/TiledDrawingBrushExample.vb#tileddrawingbrushexamplewholepage)]  
  
 다음 그림과 바둑판 패턴 <xref:System.Windows.Media.DrawingBrush> 출력 합니다.  
  
 ![DrawingBrush의 바둑판식 출력](./media/graphicsmm-drawingbrush-tiled.png "graphicsmm_drawingbrush_tiled")  
  
 그리기 브러시에 대 한 자세한 내용은 참조 하세요. [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)합니다. 에 대 한 자세한 내용은 <xref:System.Windows.Media.Drawing> 개체를 참조 합니다 [Drawing 개체 개요](drawing-objects-overview.md)합니다.
