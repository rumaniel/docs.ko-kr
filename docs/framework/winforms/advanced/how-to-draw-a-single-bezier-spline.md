---
title: '방법: 단일 B를 그리는&#233;zier 스플라인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Bezier splines [Windows Forms], drawing
- drawing [Windows Forms], Bezier splines
ms.assetid: f4f3fe30-f0a6-4743-ac91-11310cebea9f
ms.openlocfilehash: ebb53e7df979a553ed4a44deba34345c9ecac772
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62004237"
---
# <a name="how-to-draw-a-single-b233zier-spline"></a>방법: 단일 B를 그리는&#233;zier 스플라인
베 지 어 스플라인을 4 개의 점으로 정의: 시작점, 두 개의 제어점 및 끝점.  
  
## <a name="example"></a>예제  
 다음 예제에서는 (10, 100) 시작점 및 끝점 (200, 100)를 사용 하 여 베 지 어 스플라인을 그립니다. 컨트롤은 (100, 10) 및 (150, 150)을 가리킵니다.  
  
 다음 그림에서는 결과 베 지 어 스플라인을와 해당 시작 지점, 제어점, 끝점을 보여 줍니다. 그림에는 또한 직선을 사용 하 여 4 개의 점을 연결 하 여 형성 된 다각형 스플라인의 볼록 다각형을 보여 줍니다.  
  
 ![3 차원 곡선 스플라인 보여 줍니다.](./media/how-to-draw-a-single-bezier-spline/bezier-spline-illustration.png)  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#31)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Graphics.DrawBezier%2A>
- [GDI+의 3차원 곡선 스플라인](bezier-splines-in-gdi.md)
- [방법: 일련의 3 차원 곡선 스플라인 그리기](how-to-draw-a-sequence-of-bezier-splines.md)
