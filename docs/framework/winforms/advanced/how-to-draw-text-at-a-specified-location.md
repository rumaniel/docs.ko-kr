---
title: '방법: 지정된 위치에 텍스트 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [Windows Forms], drawing at specified locations [Windows Forms]
- drawing text
- drawing text [Windows Forms], specified locations [Windows Forms]
- Windows Forms, drawing text at a specified location
ms.assetid: 60816423-1c38-465e-980d-2c2b64d74086
ms.openlocfilehash: 0c36b00e4f6f71f0ecf8042853bb8e99e57854da
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64912421"
---
# <a name="how-to-draw-text-at-a-specified-location"></a>방법: 지정된 위치에 텍스트 그리기
사용자 지정 그리기를 수행 하면 지정된 된 지점부터 한 가로 줄의 텍스트를 그릴 수 있습니다. 사용 하 여 이러한 방식으로 텍스트를 그릴 수 있습니다는 <xref:System.Drawing.Graphics.DrawString%2A> 메서드의 오버 로드는 <xref:System.Drawing.Graphics> 사용 하는 클래스를 <xref:System.Drawing.Point> 또는 <xref:System.Drawing.PointF> 매개 변수입니다. 합니다 <xref:System.Drawing.Graphics.DrawString%2A> 방법을 사용 하려면를 <xref:System.Drawing.Brush> 및 <xref:System.Drawing.Font>  
  
 사용할 수도 있습니다는 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 메서드의 오버 로드는 <xref:System.Windows.Forms.TextRenderer> 를 사용 하는 <xref:System.Drawing.Point>합니다. <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 또한 필요는 <xref:System.Drawing.Color> 및 <xref:System.Drawing.Font>합니다.  
  
 다음 그림에서는 사용 하는 경우 지정된 된 지점에 그려지는 텍스트의 출력을 보여 줍니다.는 <xref:System.Drawing.Graphics.DrawString%2A> 메서드 오버 로드 합니다.  
  
 ![지정된 된 위치에서 텍스트의 출력을 보여 주는 스크린샷.](./media/how-to-draw-text-at-a-specified-location/font-text-specified-point.png)  
  
### <a name="to-draw-a-line-of-text-with-gdi"></a>GDI +를 사용 하 여 텍스트의 선을 그리려면  
  
1. 사용 하 여는 <xref:System.Drawing.Graphics.DrawString%2A> 메서드를 원하는 텍스트를 전달 <xref:System.Drawing.Point> 또는 <xref:System.Drawing.PointF>, <xref:System.Drawing.Font>, 및 <xref:System.Drawing.Brush>합니다.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#30)]
     [!code-vb[System.Drawing.AlignDrawnText#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#30)]  
  
### <a name="to-draw-a-line-of-text-with-gdi"></a>GDI 사용 하 여 텍스트의 선을 그리려면  
  
1. 사용 하 여는 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 메서드를 원하는 텍스트를 전달 <xref:System.Drawing.Point>, <xref:System.Drawing.Font>, 및 <xref:System.Drawing.Color>합니다.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#40](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#40)]
     [!code-vb[System.Drawing.AlignDrawnText#40](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#40)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제에서는 필요합니다.  
  
- <xref:System.Windows.Forms.PaintEventArgs>  `e`에서의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- [방법: GDI 사용 하 여 텍스트 그리기](how-to-draw-text-with-gdi.md)
- [글꼴 및 텍스트 사용](using-fonts-and-text.md)
- [방법: 글꼴 패밀리 및 글꼴 만들기](how-to-construct-font-families-and-fonts.md)
- [방법: 사각형 안에 줄 바꿈된 텍스트 그리기](how-to-draw-wrapped-text-in-a-rectangle.md)
