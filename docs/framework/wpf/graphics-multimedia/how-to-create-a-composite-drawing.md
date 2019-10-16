---
title: '방법: 복합 그리기 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- drawings [WPF], composite
- composite drawings [WPF]
- graphics [WPF], composite drawings
ms.assetid: 066eb0ab-5f0e-439d-85c6-dca60af269fc
ms.openlocfilehash: 0af7fbca593627ebe8cd102a02617a27eac50aa5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61909994"
---
# <a name="how-to-create-a-composite-drawing"></a>방법: 복합 그리기 만들기
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.DrawingGroup> 여러 결합 하 여 복잡 한 그리기를 만들려면 <xref:System.Windows.Media.Drawing> 를 단일 합성 그리기로 개체입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.DrawingGroup> 합성 그리기를 만들려고 합니다 <xref:System.Windows.Media.GeometryDrawing> 및 <xref:System.Windows.Media.ImageDrawing> 개체입니다. 다음 그림에서는 이 예제가 생성하는 출력을 보여 줍니다.  
  
 ![여러 있는 DrawingGroup](./media/graphicsmm-simple.jpg "graphicsmm_simple")  
DrawingGroup를 사용 하 여 만든 합성 그리기  
  
 그리기의 범위를 보여 주는 회색 테두리를 note 합니다.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmsimpledrawinggroupexample)]
 [!code-xaml[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmsimpledrawinggroupexample)]  
  
 사용할 수는 <xref:System.Windows.Media.DrawingGroup> 적용할를 <xref:System.Windows.Media.DrawingGroup.Transform%2A>, <xref:System.Windows.Media.DrawingGroup.Opacity%2A> 설정을 <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>, <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>를 <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>, 또는 <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A> 포함 그리기에. 때문에 <xref:System.Windows.Media.DrawingGroup> 이기도 <xref:System.Windows.Media.Drawing>, 기타를 포함할 수 있습니다 <xref:System.Windows.Media.DrawingGroup> 개체입니다.  
  
 다음 예제에서는 추가 사용 하 여에 앞의 예제에 비슷합니다. <xref:System.Windows.Media.DrawingGroup> 일부 그리기를 불투명 마스크 및 비트맵 효과 적용 하는 개체입니다. 다음 그림에서는 이 예제가 생성하는 출력을 보여 줍니다.  
  
 ![여러 있는 DrawingGroup](./media/graphicsmm-multiple.jpg "graphicsmm_multiple")  
합성 그리기는 여러 DrawingGroup 개체는  
  
 그리기의 범위를 보여 주는 회색 테두리를 note 합니다.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMMultipleDrawingGroupsExample](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmmultipledrawinggroupsexample)]
 [!code-xaml[DrawingMiscSnippets_snip#GraphicsMMMultipleDrawingGroupsExample](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmmultipledrawinggroupsexample)]  
  
 에 대 한 자세한 내용은 <xref:System.Windows.Media.Drawing> 개체를 참조 하세요 [Drawing 개체 개요](drawing-objects-overview.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>
- <xref:System.Windows.Media.DrawingGroup.Transform%2A>
- <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>
- <xref:System.Windows.Media.DrawingGroup.Opacity%2A>
- <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>
- <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>
- [Drawing 개체 개요](drawing-objects-overview.md)
