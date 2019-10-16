---
title: '방법: 선형 그라데이션 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- linear gradients [Windows Forms], creating
- gradients [Windows Forms], creating linear
- colors [Windows Forms], creating linear gradients
- gradients
ms.assetid: 6c88e1cc-1217-4399-ac12-cb37592b9f01
ms.openlocfilehash: e55d27b454579268658192ae56daa52e0b28bb83
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65876067"
---
# <a name="how-to-create-a-linear-gradient"></a>방법: 선형 그라데이션 만들기
GDI + 가로, 세로 및 대각선 선형 그라데이션 제공합니다. 기본적으로 선형 그라데이션에 색이 균일 하 게 변경 합니다. 그러나 균일 하지 않은 방식으로 색이 변경 되도록 선형 그라데이션을 사용자 지정할 수 있습니다.  

> [!NOTE]
> 이 문서의 예제에서는 컨트롤에서 호출 되는 메서드는 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기입니다.  

다음 예제에서는 선, 타원, 및 가로 선형 그라데이션 브러시를 사용 하 여 사각형을 채웁니다.  
  
<xref:System.Drawing.Drawing2D.LinearGradientBrush.%23ctor%2A> 생성자는 네 개의 인수를 받습니다: 두 색으로 및 두 점입니다. 첫 번째 지점 (0, 10) 첫 번째 색 (빨강)에 연결 되며 두 번째 점 (200, 10)는 두 번째 색 (파란색)를 사용 하 여 연결 합니다. 예상한 대로에서 가져온 줄 (0, 10)를 (200, 10) 빨간색에서 파란색 점진적으로 변경 합니다.  
  
 점 (0, 10) 및 (200, 10)에서 10 중요 하지 않습니다. 두 점 동일한 두 번째 좌표에는 중요 한 것-연결 선은 가로입니다. 타원 및 사각형 변경할 수도 점진적으로 빨간색에서 가로 좌표 이동 0에서 200으로 파란색입니다.  
  
 다음 그림은 선, 타원 및 사각형을 나타냅니다. 참고는 색 그라데이션 반복 하는 가로 좌표는 200 개 이상 증가 합니다.  
  
 ![선, 타원 및 사각형 색 그라데이션을 사용 하 여 채워집니다.](./media/how-to-create-a-linear-gradient/gradient-line-ellipse-rectangle.png)  
  
## <a name="to-use-horizontal-linear-gradients"></a>가로 선형 그라데이션 사용 하려면  
  
- 불투명 한 빨강 및 불투명 파란색 세 번째와 네 번째 인수로 각각 전달 합니다.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#21)]
     [!code-vb[System.Drawing.UsingaGradientBrush#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#21)]  
  
 앞의 예제에서 200에서 가로 좌표 0 가로 좌표에서 이동 색 구성 요소 선형적으로 변경 합니다. 예를 들어, 첫 번째 좌표가 0과 200 사이의 중간 지점 0과 255 사이의 중간에 있는 파란색 구성 요소를 갖습니다.  
  
 GDI + 다른 색이 변하는 그라데이션의 한쪽 가장자리에서 방식을 조정할 수 있습니다. 검정에서 다음 표에 따라 빨강으로 변경 하는 그라데이션 브러시를 만들려고 한다고 가정 합니다.  
  
|가로 좌표|RGB 구성 요소|  
|---------------------------|--------------------|  
|0|(0, 0, 0)|  
|40|(128, 0, 0)|  
|200|(255, 0, 0)|  
  
 빨강 구성 요소는 농도가 절반 경우 가로 좌표는 0에서 방법 200의 20%만 note 합니다.  
  
 다음 예제에서는 <xref:System.Drawing.Drawing2D.LinearGradientBrush.Blend%2A?displayProperty=nameWithType> 세 가지 상대 위치를 사용 하 여 세 가지 상대 강도 연결할 속성입니다. 앞의 표에서 같이 0.5의 상대 강도 0.2의 상대적 위치와 연결 됩니다. 그라데이션 브러시를 사용 하 여 사각형 및 타원을 채웁니다.  
  
 다음 그림에서는 결과 타원 및 사각형을 보여 줍니다.  
  
 ![타원 및 사각형 가로 색 그라데이션을 사용 하 여 채워집니다.](./media/how-to-create-a-linear-gradient/gradient-ellipse-rectangle.png)  

## <a name="to-customize-linear-gradients"></a>선형 그라데이션 사용자 지정 하려면  
  
- 불투명 한 검정 픽셀과 불투명 한 빨강의 세 번째 및 네 번째 인수로 각각 전달 합니다.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#22](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#22)]
     [!code-vb[System.Drawing.UsingaGradientBrush#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#22)]  
  
 이전 예제의 그라데이션 가로; 되었습니다. 즉, 색 가로 줄에 따라 점진적으로 변경 합니다. 세로 그라데이션 및 대각선 그라데이션을 정의할 수 있습니다.  
  
 에 점 (0, 0) 및 (200, 100)를 전달 하는 다음 예제는 <xref:System.Drawing.Drawing2D.LinearGradientBrush.%23ctor%2A> 생성자입니다. 파란색 연관 된 (0, 0)와 연결 되는 녹색 (200, 100). (펜 굵기 10)이 있는 선 및 타원 선형 그라데이션 브러시를 사용 하 여 채워집니다.  
  
 다음 그림에서는 줄 및 타원을 보여 줍니다. 참고는 타원 변경에서 색 점진적으로 하나를 따라 이동 하면 줄을 통과 하는 줄에 병렬 되 (0, 0) 및 (200, 100).  
  
 ![줄 및 타원 대각선 색 그라데이션을 사용 하 여 채워집니다.](./media/how-to-create-a-linear-gradient/gradient-line-ellipse.png)  
  
## <a name="to-create-diagonal-linear-gradients"></a>대각선 선형 그라데이션을 만들려면  
  
- 불투명 파란색 픽셀과 불투명 한 녹색 세 번째와 네 번째 인수로 각각 전달 합니다.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#23](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#23)]
     [!code-vb[System.Drawing.UsingaGradientBrush#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#23)]  
  
## <a name="see-also"></a>참고자료

- [그라데이션 브러시를 사용하여 도형 채우기](using-a-gradient-brush-to-fill-shapes.md)
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
