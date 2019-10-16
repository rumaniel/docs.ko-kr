---
title: 벡터 그래픽 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- inclusive-inclusive endpoints
- coordinate systems
- graphics [Windows Forms], vector graphics
ms.assetid: 0195df81-66be-452d-bb53-5a582ebfdc09
ms.openlocfilehash: 64bec47a186b08298a49c6f188795d1b51d234eb
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505246"
---
# <a name="vector-graphics-overview"></a>벡터 그래픽 개요
GDI +는 좌표계에 선, 사각형 및 기타 도형을 그립니다. 다양 한 좌표 시스템에서에서 선택할 수 있지만 기본 좌표계 원점 왼쪽 위 모퉁이의 x 축이 오른쪽 y 축은 아래쪽을 가리키는 합니다. 기본 좌표계의 측정 단위는 픽셀입니다.  
  
## <a name="the-building-blocks-of-gdi"></a>GDI +의 구성 요소  
 ![벡터 그래픽](./media/aboutgdip02-art01.gif "AboutGdip02_Art01")  
  
 컴퓨터 모니터의 점 그림 요소 또는 픽셀 사각형 배열에서 해당 표시를 만듭니다. 다음 모니터를 한 화면에 표시 되는 픽셀 수가 달라 집니다 있으며 각 모니터에 표시 되는 픽셀 수가 일반적으로 구성할 수 있습니다 어느 정도 까지는 사용자가 있습니다.  
  
 ![벡터 그래픽](./media/aboutgdip02-art02.gif "AboutGdip02_Art02")  
  
 선, 사각형 또는 곡선을 그릴 GDI +를 사용 하면 그릴 항목에 대 한 특정 키 정보를 제공 합니다. 예를 들어 두 점을 제공 하 여 줄을 지정할 수 있습니다 및 지점, 높이 및 너비를 제공 하 여 사각형을 지정할 수 있습니다. GDI +는 픽셀 켜야 선, 사각형 또는 곡선 표시를 확인 하는 디스플레이 드라이버 소프트웨어와 함께에서 작동 합니다. 다음 그림에서는 점 (12, 8)를 (4, 2) 지점에서 줄을 표시 하려면 켜져 있는 픽셀을 보여 줍니다.  
  
 ![벡터 그래픽](./media/aboutgdip02-art03.gif "AboutGdip02_Art03")  
  
 시간이 지남에 따라 특정 기본 빌드 블록 2 차원 그림을 만들기 위한 가장 유용한 것으로 입증 합니다. GDI +에서 지원 되며, 이러한 빌딩 블록은 다음 목록에 제공 됩니다.  
  
- 선  
  
- 사각형  
  
- 줄임표  
  
- 원호  
  
- 다각형  
  
- 카디널 스플라인  
  
- 3차원 곡선 스플라인  
  
## <a name="methods-for-drawing-with-a-graphics-object"></a>Graphics 개체를 사용 하 여 그리기 메서드  
 <xref:System.Drawing.Graphics> 위 목록의 항목을 그리기 위한 메서드를 제공 하는 GDI +의 클래스: <xref:System.Drawing.Graphics.DrawLine%2A>, <xref:System.Drawing.Graphics.DrawRectangle%2A>, <xref:System.Drawing.Graphics.DrawEllipse%2A>, <xref:System.Drawing.Graphics.DrawPolygon%2A>를 <xref:System.Drawing.Graphics.DrawArc%2A>, <xref:System.Drawing.Graphics.DrawCurve%2A> (카디널 스플라인 용) 및 <xref:System.Drawing.Graphics.DrawBezier%2A>. 이러한 각 메서드는 오버 로드 됩니다. 즉, 각 메서드는 여러 다른 매개 변수 목록을 지원합니다. 예를 들어, 하나의 변형 합니다 <xref:System.Drawing.Graphics.DrawLine%2A> 메서드는 수신를 <xref:System.Drawing.Pen> 개체 및 다른 변형 하는 동안 4 개의 정수를 <xref:System.Drawing.Graphics.DrawLine%2A> 메서드는 수신를 <xref:System.Drawing.Pen> 개체와 두 개의 <xref:System.Drawing.Point> 개체.  
  
 선, 사각형 및 3 차원 곡선 스플라인 그리기 위한 메서드는 단일 호출에서 여러 항목을 그릴 동반 메서드: <xref:System.Drawing.Graphics.DrawLines%2A>, <xref:System.Drawing.Graphics.DrawRectangles%2A>, 및 <xref:System.Drawing.Graphics.DrawBeziers%2A>합니다. 또한 합니다 <xref:System.Drawing.Graphics.DrawCurve%2A> 메서드는 도우미 메서드를 <xref:System.Drawing.Graphics.DrawClosedCurve%2A>닫히는 연결 곡선의 끝점을 시작 하 여 곡선 가리킨는 합니다.  
  
 모든 그리기 메서드를 <xref:System.Drawing.Graphics> 클래스와 함께에서 작업을 <xref:System.Drawing.Pen> 개체입니다. 아무 것도 그리지를 두 개 이상의 개체를 만들어야 합니다:는 <xref:System.Drawing.Graphics> 개체 및 <xref:System.Drawing.Pen> 개체입니다. <xref:System.Drawing.Pen> 개체 같은 선 두께 및 색을 그릴 항목의 특성을 저장 합니다. <xref:System.Drawing.Pen> 개체 그리기 메서드를 인수 중 하나로 전달 됩니다. 예를 들어, 하나의 변형 합니다 <xref:System.Drawing.Graphics.DrawLine%2A> 메서드는 수신를 <xref:System.Drawing.Pen> 개체와 네 개의 정수는 100, 50의 높이 및를 왼쪽 위 모퉁이의 너비를 사용 하 여 사각형을 그린 다음 예와에서 같이 (20, 10):  
  
 [!code-csharp[LinesCurvesAndShapes#11](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#11)]
 [!code-vb[LinesCurvesAndShapes#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#11)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Graphics?displayProperty=nameWithType>
- <xref:System.Drawing.Pen?displayProperty=nameWithType>
- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [방법: 그리는 데 필요한 그래픽 개체 만들기](how-to-create-graphics-objects-for-drawing.md)
