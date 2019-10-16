---
title: GDI+의 펜, 선 및 사각형
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lines
- GDI+, lines
- drawing [Windows Forms], rectangles
- rectangles
- drawing [Windows Forms], lines
- GDI+, pens
- examples [Windows Forms], drawing lines and shapes
- examples [Windows Forms], pens
- GDI+, rectangles
- examples [Windows Forms], GDI+
- lines [Windows Forms], dashed
ms.assetid: 30b25aae-e3eb-4479-bdb8-187cf651fc84
ms.openlocfilehash: 06d2351ffa7d7f009d7b049f4689df7038b4d202
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505344"
---
# <a name="pens-lines-and-rectangles-in-gdi"></a>GDI+의 펜, 선 및 사각형
GDI + 만들 필요가 있는 선을 그리려면를 <xref:System.Drawing.Graphics> 개체 및 <xref:System.Drawing.Pen> 개체입니다. 합니다 <xref:System.Drawing.Graphics> 실제로 그리기를 수행 하는 메서드를 제공 하는 개체 및 <xref:System.Drawing.Pen> 개체 선 색, 너비 및 스타일 같은 특성을 저장 합니다.  
  
## <a name="drawing-a-line"></a>선 그리기  
 선 그리기를 호출 합니다 <xref:System.Drawing.Graphics.DrawLine%2A> 메서드는 <xref:System.Drawing.Graphics> 개체. 합니다 <xref:System.Drawing.Pen> 개체에 대 한 인수 중 하나로 전달 되는 <xref:System.Drawing.Graphics.DrawLine%2A> 메서드. 다음 예제에서는 점 (12, 6) 줄 (4, 2) 지점에서 그립니다.  
  
 [!code-csharp[LinesCurvesAndShapes#41](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#41)]
 [!code-vb[LinesCurvesAndShapes#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#41)]  
  
 <xref:System.Drawing.Graphics.DrawLine%2A> 오버 로드 메서드도 <xref:System.Drawing.Graphics> 클래스를 여러 가지 인수를 사용 하 여 제공할 수 있습니다. 예를 들어 두 생성할 수 있습니다 <xref:System.Drawing.Point> 개체를 전달 합니다 <xref:System.Drawing.Point> 개체에 대 한 인수로 <xref:System.Drawing.Graphics.DrawLine%2A> 메서드:  
  
 [!code-csharp[LinesCurvesAndShapes#42](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#42)]
 [!code-vb[LinesCurvesAndShapes#42](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#42)]  
  
## <a name="constructing-a-pen"></a>펜 생성  
 생성 하는 경우에 특정 특성을 지정할 수 있습니다는 <xref:System.Drawing.Pen> 개체입니다. 예를 들어 하나 `Pen` 생성자를 사용 하면 색 및 두께 지정할 수 있습니다. 다음 예제에서는 2에서 너비의 파란색 선을 그립니다 (0, 0)를 (60, 30):  
  
 [!code-csharp[LinesCurvesAndShapes#43](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#43)]
 [!code-vb[LinesCurvesAndShapes#43](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#43)]  
  
## <a name="dashed-lines-and-line-caps"></a>파선 및 선 끝  
 <xref:System.Drawing.Pen> 개체도 노출 속성을 같은 <xref:System.Drawing.Pen.DashStyle%2A>, 줄의 기능을 지정 하려면 사용할 수 있습니다. 다음 예제에서는 그리는 파선에서 (100, 50)에 (300, 80):  
  
 [!code-csharp[LinesCurvesAndShapes#44](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#44)]
 [!code-vb[LinesCurvesAndShapes#44](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#44)]  
  
 속성을 사용할 수는 <xref:System.Drawing.Pen> 줄의 다양 한 특성을 설정할 개체입니다. 합니다 <xref:System.Drawing.Pen.StartCap%2A> 및 <xref:System.Drawing.Pen.EndCap%2A> 속성 선 끝 모양을 지정; 플랫, 사각형, 둥근, 삼각형, 끝 수 또는 사용자 지정 셰이프. <xref:System.Drawing.Pen.LineJoin%2A> 속성 또는 지정할 수 있습니다 있는지 여부를 연결 된 선 됩니다 (날카로운 모퉁이 사용 하 여 조인) 음, 경사진, 반올림 잘립니다. 다음 그림에서는 한도 및 조인에 대 한 다양 한 스타일을 사용 하 여 줄을 보여 줍니다.  
  
 ![Lines](./media/aboutgdip02-art04.gif "Aboutgdip02_art04")  
  
## <a name="drawing-a-rectangle"></a>사각형 그리기  
 GDI +를 사용 하 여 사각형 그리기 선을 그릴와 비슷합니다. 사각형을 그리려면 하려면를 <xref:System.Drawing.Graphics> 개체 및 <xref:System.Drawing.Pen> 개체입니다. <xref:System.Drawing.Graphics> 개체를 제공을 <xref:System.Drawing.Graphics.DrawRectangle%2A> 메서드 및 <xref:System.Drawing.Pen> 개체 선 두께 색 같은 특성을 저장 합니다. 합니다 <xref:System.Drawing.Pen> 개체에 대 한 인수 중 하나로 전달 되는 <xref:System.Drawing.Graphics.DrawRectangle%2A> 메서드. 다음 예제에서는 왼쪽 위 모퉁이가 사용 하 여 사각형을 그립니다 (100, 50), 80, 너비 및 높이가 40:  
  
 [!code-csharp[LinesCurvesAndShapes#45](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#45)]
 [!code-vb[LinesCurvesAndShapes#45](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#45)]  
  
 <xref:System.Drawing.Graphics.DrawRectangle%2A> 오버 로드 메서드도 <xref:System.Drawing.Graphics> 클래스를 여러 가지 인수를 사용 하 여 제공할 수 있습니다. 예를 들어, 생성할 수 있습니다는 <xref:System.Drawing.Rectangle> 개체를 전달 합니다 <xref:System.Drawing.Rectangle> 개체는 <xref:System.Drawing.Graphics.DrawRectangle%2A> 메서드에 인수로:  
  
 [!code-csharp[LinesCurvesAndShapes#46](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#46)]
 [!code-vb[LinesCurvesAndShapes#46](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#46)]  
  
 <xref:System.Drawing.Rectangle> 개체에 메서드와 속성을 조작 하 고 사각형에 대 한 정보를 수집 합니다. 예를 들어 합니다 <xref:System.Drawing.Rectangle.Inflate%2A> 및 <xref:System.Drawing.Rectangle.Offset%2A> 메서드 사각형의 위치와 크기를 변경 합니다. 합니다 <xref:System.Drawing.Rectangle.IntersectsWith%2A> 메서드를 알려 사각형 다른 인스턴스와 교차 하는지 여부 사각형을 지정 및 <xref:System.Drawing.Rectangle.Contains%2A> 메서드 알려 사각형 내에서 지정된 된 지점 인지 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Graphics?displayProperty=nameWithType>
- <xref:System.Drawing.Pen?displayProperty=nameWithType>
- <xref:System.Drawing.Rectangle?displayProperty=nameWithType>
- [방법: 펜 만들기](how-to-create-a-pen.md)
- [방법: Windows Form에 선 그리기](how-to-draw-a-line-on-a-windows-form.md)
- [방법: 윤곽선이 있는 도형 그리기](how-to-draw-an-outlined-shape.md)
