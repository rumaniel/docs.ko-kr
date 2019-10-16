---
title: '방법: B의 시퀀스를 그리는&#233;zier 스플라인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- splines [Windows Forms], drawing Bezier
- Bezier splines [Windows Forms], drawing sequence of
ms.assetid: 37a0bedb-20c2-4cf0-91fa-a5509e826b30
ms.openlocfilehash: 976787f5830282a581d05a9c24d1f83dceca4b25
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62004263"
---
# <a name="how-to-draw-a-sequence-of-b233zier-splines"></a>방법: B의 시퀀스를 그리는&#233;zier 스플라인
사용할 수는 <xref:System.Drawing.Graphics.DrawBeziers%2A> 메서드는 <xref:System.Drawing.Graphics> 일련의 그리기 클래스에는 3 차원 곡선 스플라인 연결 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 연결 된 3 차원 곡선 스플라인 구성 된 곡선을 그립니다. 첫 번째 베 지 어 스플라인의 끝점에는 두 번째 베 지 어 스플라인의 시작 지점입니다.  
  
 다음 그림에는 7 개의 점이 함께 연결 된 스플라인 보여 줍니다.  
  
 ![7 개의 점이 함께 연결 된 스플라인 보여 주는 그래픽.](./media/how-to-draw-a-sequence-of-bezier-splines/bezier-spline-seven-points.png)  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [GDI+의 3차원 곡선 스플라인](bezier-splines-in-gdi.md)
- [곡선 구성 및 그리기](constructing-and-drawing-curves.md)
