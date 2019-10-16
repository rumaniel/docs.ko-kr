---
title: '방법: TileBrush로 다른 바둑판식 배열 패턴 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TileBrush [WPF], creating tile patterns
- tile patterns [WPF], creating
- creating [WPF], tile patterns with TileBrush
ms.assetid: 5aa46632-3527-4668-9d8d-0375c8af28aa
ms.openlocfilehash: c1051b234961eee9ae740af2abac3d64c523656c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61905136"
---
# <a name="how-to-create-different-tile-patterns-with-a-tilebrush"></a>방법: TileBrush로 다른 바둑판식 배열 패턴 만들기
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.TileBrush.TileMode%2A> 의 속성을 <xref:System.Windows.Media.TileBrush> 패턴을 만들려면.  
  
 합니다 <xref:System.Windows.Media.TileBrush.TileMode%2A> 속성을 사용 하면 지정할 수 있습니다 하는 방법을의 콘텐츠는 <xref:System.Windows.Media.TileBrush> 반복, 즉, 출력 영역을 채우는 바둑판식으로 배열 됩니다. 설정한 패턴을 만들려면 합니다 <xref:System.Windows.Media.TileBrush.TileMode%2A> 하 <xref:System.Windows.Media.TileMode.Tile>, <xref:System.Windows.Media.TileMode.FlipX>, <xref:System.Windows.Media.TileMode.FlipY>, 또는 <xref:System.Windows.Media.TileMode.FlipXY>. 설정 해야 합니다 <xref:System.Windows.Media.TileBrush.Viewport%2A> 의 <xref:System.Windows.Media.TileBrush> 는; 사용자가 칠하고 있는 영역 보다 작은 것이 고, 그렇지 타일 하나만 생성 된 상관 없이는 <xref:System.Windows.Media.TileBrush.TileMode%2A> 설정을 사용 하면 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 5 <xref:System.Windows.Media.DrawingBrush> 개체, 다른 각각에 제공 <xref:System.Windows.Media.TileBrush.TileMode%2A> 설정과 하는 5 개의 사각형을 그리는 데 사용 합니다. 이 예제에서는 <xref:System.Windows.Media.DrawingBrush> 클래스를 보여 줍니다 <xref:System.Windows.Media.TileBrush.TileMode%2A> 동작을는 <xref:System.Windows.Media.TileBrush.TileMode%2A> 속성 모두에 대 한 동일 하 게 작동 합니다 <xref:System.Windows.Media.TileBrush> 개체, 즉,에 대 한 <xref:System.Windows.Media.ImageBrush>, <xref:System.Windows.Media.VisualBrush>, 및 <xref:System.Windows.Media.DrawingBrush>합니다.  
  
 다음 그림에서는 이 예제가 생성하는 출력을 보여 줍니다.  
  
 ![예제 출력을 바둑판식으로 배열 된 TileBrush](./media/graphicsmm-drawingbrushtilemodeexample.png "graphicsmm_DrawingBrushTileModeExample")  
TileMode 속성을 사용 하 여 만든 타일 패턴  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/TileModeExample.cs#graphicsmmdrawingbrushtilemodeexample)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/tilemodeexample.vb#graphicsmmdrawingbrushtilemodeexample)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/TileModeExample.xaml#graphicsmmdrawingbrushtilemodeexample)]  
  
## <a name="see-also"></a>참고자료

- [TileBrush의 바둑판 크기 설정](how-to-set-the-tile-size-for-a-tilebrush.md)
- [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)
