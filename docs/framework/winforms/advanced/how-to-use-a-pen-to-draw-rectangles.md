---
title: '방법: 펜을 사용하여 사각형 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- rectangles [Windows Forms], drawing
- pens [Windows Forms], drawing rectangles
ms.assetid: 54a7fa14-3ad8-4d64-b424-2a12005b250c
ms.openlocfilehash: cd5d965f8b92d15cdeb3049330d9b3cc0de893b2
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590232"
---
# <a name="how-to-use-a-pen-to-draw-rectangles"></a>방법: 펜을 사용하여 사각형 그리기
사각형을 그리려면 필요는 <xref:System.Drawing.Graphics> 개체 및 <xref:System.Drawing.Pen> 개체입니다. <xref:System.Drawing.Graphics> 개체를 제공 합니다 <xref:System.Drawing.Graphics.DrawRectangle%2A> 메서드 및 <xref:System.Drawing.Pen> 개체 저장 되는 선의 색 및 두께 같은 기능입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 왼쪽 위 모퉁이가 사용 하 여 사각형을 그립니다 (10, 10). 사각형의 너비를 100 고 50 높이. 전달 된 두 번째 인수는 <xref:System.Drawing.Pen.%23ctor%2A> 생성자 펜 굵기 5 픽셀 임을 나타냅니다.  
  
 사각형을 그릴 때 펜 사각형의 경계에서 가운데 맞춤 됩니다. 사각형의 면은 그려지는 5 픽셀 펜 너비는 5 이므로 해당 1 픽셀이 그려집니다 와이드 등 자체 경계에서 2 픽셀로 내부적으로 그려지며 2 픽셀로 바깥쪽에 그려집니다. 펜 맞춤에 대 한 자세한 내용은 참조 하세요. [방법: 펜 굵기 및 맞춤 설정](how-to-set-pen-width-and-alignment.md)합니다.  
  
 다음 그림에서는 결과 사각형을 보여 줍니다. 여기서 사각형 그려지는 펜 너비는 픽 했다면 점선 보여 줍니다. 사각형의 왼쪽 위 모퉁이의 확대 된 뷰는 두꺼운 검정 선은 가운데에 이러한 점선 보여 줍니다.  
  
 ![검정 및 점선을 사용 하 여 그린된 사각형을 보여주는 스크린샷.](./media/how-to-use-a-pen-to-draw-rectangles/drawn-rectangle-black-lines-dotted-lines.gif)  
  
 [!code-csharp[System.Drawing.UsingAPen#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.UsingAPen#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#21)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- [펜을 사용하여 선과 도형 그리기](using-a-pen-to-draw-lines-and-shapes.md)
