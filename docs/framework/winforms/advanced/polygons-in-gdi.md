---
title: GDI+의 다각형
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- polygons
- drawing [Windows Forms], polygons
- GDI+, polygons
ms.assetid: a72213d2-d69a-4c2b-a75c-be7b20390c13
ms.openlocfilehash: 2b1e3d387e4d056d9187c54dcef560544206c370
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61641309"
---
# <a name="polygons-in-gdi"></a>GDI+의 다각형
다각형은 3 개 이상의 직선 면을 사용 하 여 닫힌된 도형입니다. 예를 들어 삼각형 세 변을 사용 하 여 다각형, 사각형은 네 면을 사용 하 여 다각형 이며 오각형 5 면을 사용 하 여 다각형입니다. 다음 그림에서는 여러 다각형을 보여 줍니다.  
  
 ![다각형](./media/aboutgdip02-art07.gif "Aboutgdip02_art07")  
  
## <a name="drawing-a-polygon"></a>다각형을 그리기  
 다각형을 그리려면 하려면를 <xref:System.Drawing.Graphics> 개체를 <xref:System.Drawing.Pen> 개체 및 배열을 <xref:System.Drawing.Point> (또는 <xref:System.Drawing.PointF>) 개체입니다. 합니다 <xref:System.Drawing.Graphics> 개체는 제공 된 <xref:System.Drawing.Graphics.DrawPolygon%2A> 메서드. 합니다 <xref:System.Drawing.Pen> 개체의 배열과 다각형을 렌더링 하는 데 사용 되는 선의 색과 두께 같은 특성이 저장 <xref:System.Drawing.Point> 직선으로 연결 포인트를 저장 하는 개체입니다. 합니다 <xref:System.Drawing.Pen> 개체 및 배열을 <xref:System.Drawing.Point> 개체에 대 한 인수로 전달 되는 <xref:System.Drawing.Graphics.DrawPolygon%2A> 메서드. 다음 예제에서는 3 면 다각형을 그립니다. 만 세 지점에는 `myPointArray`: (0, 0), (50, 30) 및 (30, 60). <xref:System.Drawing.Graphics.DrawPolygon%2A> 메서드는 자동으로 다각형에서 선을 그려 닫습니다 (30, 60) 시작 지점 (0, 0)으로 다시 합니다.  
  
 [!code-csharp[LinesCurvesAndShapes#111](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#111)]
 [!code-vb[LinesCurvesAndShapes#111](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#111)]  
  
 다음 그림은 다각형을 보여 줍니다.  
  
 ![Polygon](./media/aboutgdip02-art08.gif "Aboutgdip02_art08")  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Graphics?displayProperty=nameWithType>
- <xref:System.Drawing.Pen?displayProperty=nameWithType>
- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [방법: 펜 만들기](how-to-create-a-pen.md)
