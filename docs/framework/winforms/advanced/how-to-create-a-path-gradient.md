---
title: '방법: 경로 그라데이션 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- path gradients [Windows Forms], creating
- gradients [Windows Forms], creating path
- graphics paths [Windows Forms], creating gradient
ms.assetid: 1948e834-e104-481c-b71d-d8aa9e4d106e
ms.openlocfilehash: 8399a56fca87704e10456a4cf8109d7c80d4db45
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964412"
---
# <a name="how-to-create-a-path-gradient"></a>방법: 경로 그라데이션 만들기
클래스 <xref:System.Drawing.Drawing2D.PathGradientBrush> 를 사용 하 여 점차적으로 색을 변경 하는 모양을 사용자 지정할 수 있습니다. 예를 들어 경로의 중앙에 대해 한 색을 지정 하 고 경로의 경계에 대해 다른 색을 지정할 수 있습니다. 경로의 경계를 따라 여러 점에 대해 별도의 색을 지정할 수도 있습니다.  
  
> [!NOTE]
> Gdi +에서 경로는 <xref:System.Drawing.Drawing2D.GraphicsPath> 개체에 의해 유지 관리 되는 선 및 곡선의 시퀀스입니다. GDI + 경로에 대 한 자세한 내용은 [GDI +의 그래픽 경로](graphics-paths-in-gdi.md) 및 [생성 및 그리기 경로](constructing-and-drawing-paths.md)를 참조 하세요.  

이 문서의 예제는 컨트롤의 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기에서 호출 되는 메서드입니다.  

### <a name="to-fill-an-ellipse-with-a-path-gradient"></a>경로 그라데이션을 사용 하 여 타원을 채우려면  
  
- 다음 예제에서는 타원을 경로 그라데이션 브러시로 채웁니다. 가운데 색이 파란색으로 설정 되 고 경계 색이 바다색으로 설정 됩니다. 다음 그림에서는 채워진 타원을 보여 줍니다.  
  
     ![그라데이션 패스가 타원을 채웁니다.](./media/how-to-create-a-path-gradient/gradient-path-filled-ellipse.png)  
  
     기본적으로 경로 그라데이션 브러시는 경로 경계 밖으로 확장 되지 않습니다. 경로 그라데이션 브러시를 사용 하 여 경로의 경계를 벗어나 확장 되는 그림을 채울 경우 경로 밖의 화면 영역이 채워지지 않습니다.  
  
     다음 그림에서는에 대 한 <xref:System.Drawing.Graphics.FillEllipse%2A?displayProperty=nameWithType> 호출을 다음 코드로 변경 하는 경우 발생 하는 상황을 `e.Graphics.FillRectangle(pthGrBrush, 0, 10, 200, 40)`보여 줍니다.  
  
     ![경로 경계를 벗어나 확장 된 그라데이션 경로입니다.](./media/how-to-create-a-path-gradient/gradient-path-extended-beyond-boundary.png)  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#11)]
     [!code-vb[System.Drawing.UsingaGradientBrush#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#11)]  
  
     위의 코드 예제는 Windows Forms와 함께 사용 하도록 설계 되었으며의 <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Windows.Forms.PaintEventHandler>매개 변수인 e가 필요 합니다.  
  
### <a name="to-specify-points-on-the-boundary"></a>경계에서 점에 지정 하려면  
  
- 다음 예제에서는 별 모양 패스에서 경로 그라데이션 브러시를 생성 합니다. 이 코드는 별 <xref:System.Drawing.Drawing2D.PathGradientBrush.CenterColor%2A> 중심의 색을 빨강으로 설정 하는 속성을 설정 합니다. 그런 다음 코드는 <xref:System.Drawing.Drawing2D.PathGradientBrush.SurroundColors%2A> `points` 배열의 개별 지점에서 속성을 설정 하 여 `colors` 배열에 저장 된 다양 한 색을 지정 합니다. 최종 코드 문은 별 모양 경로를 경로 그라데이션 브러시로 채웁니다.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#12)]
     [!code-vb[System.Drawing.UsingaGradientBrush#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#12)]  
  
- 다음 예제에서는 코드에 <xref:System.Drawing.Drawing2D.GraphicsPath> 개체 없이 경로 그라데이션을 그립니다. 예제의 특정 <xref:System.Drawing.Drawing2D.PathGradientBrush.%23ctor%2A> 생성자는 점의 배열을 받지만 개체는 <xref:System.Drawing.Drawing2D.GraphicsPath> 필요 하지 않습니다. 또한는 <xref:System.Drawing.Drawing2D.PathGradientBrush> 경로가 아닌 사각형을 채우는 데 사용 됩니다. 사각형은 브러시를 정의 하는 데 사용 된 닫힌 경로 보다 크므로 브러시에 의해 사각형이 그려지지 않습니다. 다음 그림은 사각형 (점선) 및 경로 그라데이션 브러시로 그린 사각형의 부분을 보여 줍니다. 
  
     ![경로 그라데이션 브러시로 칠하는 그라데이션 부분입니다.](./media/how-to-create-a-path-gradient/gradient-painted-path-gradient-brush.png)  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#13](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#13)]
     [!code-vb[System.Drawing.UsingaGradientBrush#13](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#13)]  
  
### <a name="to-customize-a-path-gradient"></a>경로 그라데이션을 사용자 지정 하려면  
  
- 경로 그라데이션 브러시를 사용자 지정 하는 한 가지 방법은 해당 <xref:System.Drawing.Drawing2D.PathGradientBrush.FocusScales%2A> 속성을 설정 하는 것입니다. 포커스 배율이 주 경로 내에 있는 내부 경로를 지정 합니다. 가운데 색은 중심점 뿐만 아니라 내부 경로 내부에 표시 됩니다.  
  
     다음 예제에서는 타원형 경로를 기반으로 하는 경로 그라데이션 브러시를 만듭니다. 이 코드는 경계 색을 파랑으로 설정 하 고 가운데 색을 바다색으로 설정한 다음 경로 그라데이션 브러시를 사용 하 여 타원형 경로를 채웁니다.  
  
     그런 다음 코드는 경로 그라데이션 브러시의 포커스 배율을 설정 합니다. X 포커스 눈금은 0.3로 설정 되 고 y 포커스 눈금은 0.8로 설정 됩니다. 이 코드는에 <xref:System.Drawing.Graphics.TranslateTransform%2A> 대 <xref:System.Drawing.Graphics.FillPath%2A> 한 후속 <xref:System.Drawing.Graphics> 호출에서 첫 번째 타원의 오른쪽에 있는 타원을 채우도록 개체의 메서드를 호출 합니다.  
  
     포커스 눈금의 효과를 확인 하려면 주 타원과 중심을 공유 하는 작은 타원이 있다고 가정 합니다. 작은 (내부) 타원은 0.3의 요소를 기준으로 세로 방향으로 조정 된 주 타원 (가운데 정보) 이며, 0.8의 경우 세로로 정렬 됩니다. 외부 타원의 경계에서 안쪽 타원의 경계로 이동할 때 색은 파란색에서 바다색으로 점차 변합니다. 내부 타원의 경계에서 공유 가운데로 이동할 때 색은 바다색으로 유지 됩니다.  
  
     다음 그림에서는 다음 코드의 출력을 보여 줍니다. 왼쪽의 타원은 중심점 에서만 바다색입니다. 오른쪽의 타원은 내부 경로 내에서 바다색입니다.  
  
 ![포커스 눈금의 그라데이션 효과](./media/how-to-create-a-path-gradient/focus-scales-aqua-inner-outer-ellipse.png)  
  
 [!code-csharp[System.Drawing.UsingaGradientBrush#14](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#14)]
 [!code-vb[System.Drawing.UsingaGradientBrush#14](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#14)]  
  
### <a name="to-customize-with-interpolation"></a>보간을 사용 하 여 사용자 지정 하려면  
  
- 경로 그라데이션 브러시를 사용자 지정 하는 또 다른 방법은 보간 색 배열과 보간 위치의 배열을 지정 하는 것입니다.  
  
     다음 예제에서는 삼각형을 기반으로 하는 경로 그라데이션 브러시를 만듭니다. 이 코드는 경로 <xref:System.Drawing.Drawing2D.PathGradientBrush.InterpolationColors%2A> 그라데이션 브러시의 속성을 설정 하 여 보간 색의 배열 (진한 녹색, 바다색, 파랑) 및 보간 위치 배열 (0, 0.25, 1)을 지정 합니다. 삼각형의 경계에서 중심점으로 이동 하면 색이 진한 녹색에서 바다색으로 점진적으로 변경 된 다음 바다색에서 파랑으로 변합니다. 진한 녹색에서 바다색으로 변경 하는 경우에는 진한 녹색에서 파랑으로의 25%가 발생 합니다.  
  
     다음 그림은 사용자 지정 경로 그라데이션 브러시로 채워진 삼각형을 보여 줍니다.  
  
     ![사용자 지정 경로 그라데이션 브러시로 채운 삼각형입니다.](./media/how-to-create-a-path-gradient/gradient-brush-filled-triangle.png)  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#15](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#15)]
     [!code-vb[System.Drawing.UsingaGradientBrush#15](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#15)]  
  
### <a name="to-set-the-center-point"></a>중심점을 설정 하려면  
  
- 기본적으로 경로 그라데이션 브러시의 중심점은 브러시를 생성 하는 데 사용 되는 경로의 중심에 있습니다. 클래스의 속성을 <xref:System.Drawing.Drawing2D.PathGradientBrush.CenterPoint%2A> 설정 하 여 중심점의 위치를 변경할 수 있습니다. <xref:System.Drawing.Drawing2D.PathGradientBrush>  
  
     다음 예제에서는 타원을 기반으로 하는 경로 그라데이션 브러시를 만듭니다. 타원의 중심은 (70, 35)에 있지만 경로 그라데이션 브러시의 중심점은 (120, 40)로 설정 됩니다.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#16](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#16)]
     [!code-vb[System.Drawing.UsingaGradientBrush#16](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#16)]  
  
     다음 그림에서는 채워진 타원과 경로 그라데이션 브러시의 중심점을 보여 줍니다.  
  
     ![채워진 타원과 중심점을 사용 하는 그라데이션 경로입니다.](./media/how-to-create-a-path-gradient/gradient-path-filled-ellipse-center-point.png)  
  
- 패스 그라데이션 브러시의 중심점을 브러시를 생성 하는 데 사용 된 경로 외부의 위치로 설정할 수 있습니다. 다음 예제에서는 위의 코드에서 <xref:System.Drawing.Drawing2D.PathGradientBrush.CenterPoint%2A> 속성을 설정 하는 호출을 대체 합니다.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#17](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#17)]
     [!code-vb[System.Drawing.UsingaGradientBrush#17](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#17)]  
  
     다음 그림에서는 이러한 변경 내용의 출력을 보여 줍니다.  
  
     ![중심점을 경로 외부에 있는 그라데이션 경로입니다.](./media/how-to-create-a-path-gradient/gradient-path-center-point-outside.png)  
  
     위의 그림에서 타원의 맨 오른쪽에 있는 점은 매우 가까이 있지만 순수한 파랑은 아닙니다. 그라데이션의 색은 채우기가 순수한 파란색 (0, 0, 255) 인 점 (145, 35)에 도달 하는 것 처럼 배치 됩니다. 그러나 경로 그라데이션 브러시는 해당 경로 내부에만 그리기 때문에 채우기는 (145, 35)에 도달 하지 않습니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 위의 예제는 Windows Forms에서 사용 하도록 설계 되었으며 <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인가 필요 `e`합니다.  
  
## <a name="see-also"></a>참고자료

- [그라데이션 브러시를 사용하여 도형 채우기](using-a-gradient-brush-to-fill-shapes.md)
