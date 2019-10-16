---
title: GDI+의 그래픽 경로
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [Windows Forms], paths
- GDI+, drawing paths
- paths [Windows Forms], drawing
- drawing [Windows Forms], paths
ms.assetid: a5500dec-666c-41fd-9da3-2169dd89c5eb
ms.openlocfilehash: 8e06032d145eb8c1aaf9bfcd1f205f8c6583634a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64581376"
---
# <a name="graphics-paths-in-gdi"></a>GDI+의 그래픽 경로
경로 선, 사각형 및 간단한 곡선을 결합 하 여 구성 됩니다. 설명한 대로 합니다 [벡터 그래픽 개요](vector-graphics-overview.md) 기본 구성 요소는 다음 그림을 그리기 위한 가장 유용한 것으로 입증는:  
  
- 선  
  
- 사각형  
  
- 줄임표  
  
- 원호  
  
- 다각형  
  
- 카디널 스플라인  
  
- 3 차원 곡선 스플라인  
  
 GDI +에서 <xref:System.Drawing.Drawing2D.GraphicsPath> 개체를 사용 하면 단일 단위로 이러한 빌딩 블록의 시퀀스를 수집할 수 있습니다. 선, 사각형, 다각형 및 곡선의 전체 시퀀스를 한 번 호출을 사용 하 여 그릴 수 있습니다 합니다 <xref:System.Drawing.Graphics.DrawPath%2A> 메서드는 <xref:System.Drawing.Graphics> 클래스입니다. 다음 그림에서는 줄, 호, 3 차원 곡선 스플라인, 및 카디널 스플라인 결합 하 여 만든 경로 보여 줍니다.  
  
 ![Path](./media/aboutgdip02-art14.gif "Aboutgdip02_art14")  
  
## <a name="using-a-path"></a>경로 사용 하 여  
 <xref:System.Drawing.Drawing2D.GraphicsPath> 그릴 항목의 시퀀스를 만들기 위한 다음 메서드를 제공 하는 클래스: <xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddRectangle%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddEllipse%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddArc%2A>를 <xref:System.Drawing.Drawing2D.GraphicsPath.AddPolygon%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddCurve%2A> (카디널 스플라인 용) 및 <xref:System.Drawing.Drawing2D.GraphicsPath.AddBezier%2A>합니다. 이러한 각 메서드는 오버 로드 됩니다. 즉, 각 메서드는 여러 다른 매개 변수 목록을 지원합니다. 한 변형 된 예를 들어,를 <xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A> 메서드 네 개의 정수를 받고 다른 변형이 합니다 <xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A> 메서드는 두 개의 수신 <xref:System.Drawing.Point> 개체입니다.  
  
 선, 사각형 및 3 차원 곡선 스플라인 경로 추가 하기 위한 메서드는 한 번의 호출 경로에 여러 항목을 추가 하는 동반 메서드를 갖습니다: <xref:System.Drawing.Drawing2D.GraphicsPath.AddLines%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddRectangles%2A>, 및 <xref:System.Drawing.Drawing2D.GraphicsPath.AddBeziers%2A>합니다. 또한 합니다 <xref:System.Drawing.Drawing2D.GraphicsPath.AddCurve%2A> 하 고 <xref:System.Drawing.Drawing2D.GraphicsPath.AddArc%2A> 도우미 메서드를 갖습니다 <xref:System.Drawing.Drawing2D.GraphicsPath.AddClosedCurve%2A> 및 <xref:System.Drawing.Drawing2D.GraphicsPath.AddPie%2A>, 닫힌된 곡선 또는 원형 경로에 추가 하는.  
  
 필요한 경로 그릴를 <xref:System.Drawing.Graphics> 개체를 <xref:System.Drawing.Pen> 개체 및 <xref:System.Drawing.Drawing2D.GraphicsPath> 개체입니다. <xref:System.Drawing.Graphics> 개체를 제공 합니다 <xref:System.Drawing.Graphics.DrawPath%2A> 메서드를 및 <xref:System.Drawing.Pen> 개체 경로 렌더링 하는 데 선의 색과 두께 같은 특성을 저장 합니다. <xref:System.Drawing.Drawing2D.GraphicsPath> 일련의 선과 곡선 경로 구성 하는 개체를 저장 합니다. 합니다 <xref:System.Drawing.Pen> 개체와 <xref:System.Drawing.Drawing2D.GraphicsPath> 개체에 대 한 인수로 전달 되는 <xref:System.Drawing.Graphics.DrawPath%2A> 메서드. 다음 예제에서는 선, 타원, 및 베 지 어 스플라인을 구성 되는 경로 그립니다.  
  
 [!code-csharp[LinesCurvesAndShapes#101](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#101)]
 [!code-vb[LinesCurvesAndShapes#101](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#101)]  
  
 다음 그림에서는 경로 보여 줍니다.  
  
 ![Path](./media/aboutgdip02-art15.gif "Aboutgdip02_art15")  
  
 선, 사각형 및 곡선 경로 추가할 뿐만 아니라 경로에 경로 추가할 수 있습니다. 이 옵션을 사용 하면 대규모의 복잡 한 경로 구성 하기 위해 기존 경로 결합할 수 있습니다.  
  
 [!code-csharp[LinesCurvesAndShapes#102](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#102)]
 [!code-vb[LinesCurvesAndShapes#102](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#102)]  
  
 항목이 두 가지 다른 경로 추가할 수 있습니다: 문자열과 원형입니다. 원형은 타원의 내부의 일부입니다. 다음 예에서는 원호, 카디널 스플라인을, 문자열 및 원형 경로 만듭니다.  
  
 [!code-csharp[LinesCurvesAndShapes#103](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#103)]
 [!code-vb[LinesCurvesAndShapes#103](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#103)]  
  
 다음 그림에서는 경로 보여 줍니다. 참고; 연결 되지 않은 경로 호, 카디널 스플라인, 문자열 및 원형 구분 됩니다.  
  
 ![Paths](./media/aboutgdip02-art16.gif "Aboutgdip02_Art16")  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=nameWithType>
- <xref:System.Drawing.Point?displayProperty=nameWithType>
- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [방법: 그리는 데 필요한 그래픽 개체 만들기](how-to-create-graphics-objects-for-drawing.md)
- [경로 구성 및 그리기](constructing-and-drawing-paths.md)
