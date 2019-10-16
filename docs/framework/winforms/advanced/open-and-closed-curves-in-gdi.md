---
title: GDI+의 개곡선 및 폐곡선
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- curves [Windows Forms], filling
- GDI+, curves
- curves [Windows Forms], drawing
- curves
ms.assetid: 08d2cc9a-dc9d-4eed-bcbb-2c8e2ca5d3ae
ms.openlocfilehash: 06afdc4549f7c3c9b0636e5c7052dcca87a153f1
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505458"
---
# <a name="open-and-closed-curves-in-gdi"></a>GDI+의 개곡선 및 폐곡선
다음 그림에서는 두 곡선으로 분할: 개곡선 및 닫힙니다.  
  
 ![개곡선 및 폐곡선](./media/aboutgdip02-art24.gif "Aboutgdip02_art24")  
  
## <a name="managed-interface-for-curves"></a>곡선에 대 한 관리 되는 인터페이스  
 닫힌된 곡선 내부 있고 브러시를 사용 하 여 채울 수 있습니다. <xref:System.Drawing.Graphics> 닫힌된 도형 및 곡선을 채우기 위한 메서드를 제공 하는 GDI +의 클래스: <xref:System.Drawing.Graphics.FillRectangle%2A>, <xref:System.Drawing.Graphics.FillEllipse%2A>, <xref:System.Drawing.Graphics.FillPie%2A>를 <xref:System.Drawing.Graphics.FillPolygon%2A>를 <xref:System.Drawing.Graphics.FillClosedCurve%2A>, <xref:System.Drawing.Graphics.FillPath%2A>, 및 <xref:System.Drawing.Graphics.FillRegion%2A>합니다. 다음이 방법 중 하나를 호출할 때마다 특정 브러시 형식 중 하나를 전달 해야 합니다 있습니다 (<xref:System.Drawing.SolidBrush>, <xref:System.Drawing.Drawing2D.HatchBrush>를 <xref:System.Drawing.TextureBrush>, <xref:System.Drawing.Drawing2D.LinearGradientBrush>, 또는 <xref:System.Drawing.Drawing2D.PathGradientBrush>) 인수로 합니다.  
  
 <xref:System.Drawing.Graphics.FillPie%2A> 메서드를 함께 제공 되는 <xref:System.Drawing.Graphics.DrawArc%2A> 메서드. 처럼 합니다 <xref:System.Drawing.Graphics.DrawArc%2A> 메서드는 타원 윤곽선의 부분을 그리는 <xref:System.Drawing.Graphics.FillPie%2A> 메서드는 타원의 내부를 채웁니다. 다음 예제에서는 원호를 그리는 데 및 타원의 내부의 해당 부분을 채웁니다.  
  
 [!code-csharp[LinesCurvesAndShapes#21](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#21)]
 [!code-vb[LinesCurvesAndShapes#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#21)]  
  
 다음 그림은 원호 및 채워진된 원형 차트를 보여 줍니다.  
  
 ![개곡선 및 폐곡선](./media/aboutgdip02-art25.gif "Aboutgdip02_art25")  
  
 <xref:System.Drawing.Graphics.FillClosedCurve%2A> 메서드를 함께 제공 되는 <xref:System.Drawing.Graphics.DrawClosedCurve%2A> 메서드. 두 메서드는 자동으로 끝점 시작 지점에 연결 하 여 곡선을 닫습니다. 다음 예제에서는 통과 하는 곡선을 그리는 데 (0, 0), (60, 20) 및 (40, 50). 그런 다음 곡선을 자동으로 연결 닫힙니다 (40, 50) 시작 지점 (0, 0) 및 내부 단색으로 채워집니다.  
  
 [!code-csharp[LinesCurvesAndShapes#22](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#22)]
 [!code-vb[LinesCurvesAndShapes#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#22)]  
  
 <xref:System.Drawing.Graphics.FillPath%2A> 메서드는 별도 경로 가지의 내부를 채웁니다. 닫힌된 곡선 또는 셰이프, 부분 경로 형성 하지 않으면 경우는 <xref:System.Drawing.Graphics.FillPath%2A> 메서드 채우기 전에 경로의 일부를 자동으로 닫힙니다. 다음 예제에서는 그리고 호, 카디널 스플라인을, 문자열 및 원형 구성 되는 경로 채웁니다.  
  
 [!code-csharp[LinesCurvesAndShapes#23](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#23)]
 [!code-vb[LinesCurvesAndShapes#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#23)]  
  
 다음 그림은 단색 하지 않고 사용 하 여 경로 보여 줍니다. 문자열의 텍스트 윤곽선은 있지만 채워지지를 여는 <xref:System.Drawing.Graphics.DrawPath%2A> 메서드. 것은 <xref:System.Drawing.Graphics.FillPath%2A> 내부 문자열의 문자를 색칠 하는 메서드.  
  
 ![경로 문자열](./media/aboutgdip02-art26.gif "Aboutgdip02_art26")  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=nameWithType>
- <xref:System.Drawing.Pen?displayProperty=nameWithType>
- <xref:System.Drawing.Point?displayProperty=nameWithType>
- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [방법: 그리는 데 필요한 그래픽 개체 만들기](how-to-create-graphics-objects-for-drawing.md)
- [경로 구성 및 그리기](constructing-and-drawing-paths.md)
