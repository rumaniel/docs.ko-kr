---
title: '방법: 카디널 스플라인 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cardinal splines [Windows Forms], drawing
- drawing [Windows Forms], cardinal splines
- graphics [Windows Forms], cardinal splines
ms.assetid: a4a41e80-4461-4b47-b6bd-2c5e68881994
ms.openlocfilehash: 12e938567d529b33ead93e081d380a650a803f23
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64626213"
---
# <a name="how-to-draw-cardinal-splines"></a>방법: 카디널 스플라인 그리기
카디널 스플라인 곡선이 요소의 지정 된 집합을 통해 원활 하 게 전달 합니다. 카디널 스플라인 그리기를 만들려면를 <xref:System.Drawing.Graphics> 개체 및 배열 요소의 주소를 전달 합니다 <xref:System.Drawing.Graphics.DrawCurve%2A> 메서드.  
  
### <a name="drawing-a-bell-shaped-cardinal-spline"></a>종 모양의 카디널 스플라인 그리기  
  
- 다음 예제에서는 5 개의 지정 된 지점을 통과 하는 종 모양의 카디널 스플라인을 그립니다. 다음 그림에서는 5 점과 곡선을 보여 줍니다.  
  
     ![종 모양의 카디널 스플라인 보여 주는 다이어그램입니다.](./media/how-to-draw-cardinal-splines/bell-shaped-cardinal-spline.png)  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#21)]  
  
### <a name="drawing-a-closed-cardinal-spline"></a>폐쇄형된 카디널 스플라인 그리기  
  
- 사용 합니다 <xref:System.Drawing.Graphics.DrawClosedCurve%2A> 메서드는 <xref:System.Drawing.Graphics> 클래스는 폐쇄형된 카디널 스플라인을 그립니다. 폐쇄형된 카디널 스플라인 곡선 배열의 마지막 요소를 계속 하 고 배열의 첫 번째 지점과 연결 합니다. 다음 예제에서는 6 개의 지정 된 지점을 통과 하는 폐쇄형된 카디널 스플라인을 그립니다. 다음 그림에서는 6 포인트에 따라 닫힌된 스플라인 보여 줍니다.  
  
 ![폐쇄형된 카디널 스플라인을 보여 주는 다이어그램입니다.](./media/how-to-draw-cardinal-splines/closed-cardinal-spine.png)  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#22](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#22)]  
  
### <a name="changing-the-bend-of-a-cardinal-spline"></a>카디널 스플라인의 굴곡 변경  
  
- 카디널 스플라인의 장력 인수를 전달 하 여 굴곡 방법을 변경 하 여 <xref:System.Drawing.Graphics.DrawCurve%2A> 메서드. 다음 예제에서는 동일한 점 집합을 통과 하는 세 개의 카디널 스플라인을 그립니다. 다음 그림에서는 세 가지 스플라인 해당 장력 값과 함께 보여 줍니다. 참고 장력 0 인 점 직선으로 연결 됩니다.  
  
 ![카디널 스플라인 세 가지를 보여 주는 다이어그램입니다.](./media/how-to-draw-cardinal-splines/three-cardinal-splines.png)  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#23](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#23)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제에서는 Windows Forms에서 사용 하도록 설계 되었으며 필요할 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수는 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기입니다.  
  
## <a name="see-also"></a>참고자료

- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [곡선 구성 및 그리기](constructing-and-drawing-curves.md)
