---
title: '방법: 선 끝이 있는 선 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- drawing [Windows Forms], lines
- lines [Windows Forms], drawing
- pens [Windows Forms], drawing lines
- drawing lines [Windows Forms], line caps
ms.assetid: eb68c3e1-c400-4886-8a04-76978a429cb6
ms.openlocfilehash: 34abfc86e980a24ebb835cfd88d2522f8372c68d
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506030"
---
# <a name="how-to-draw-a-line-with-line-caps"></a>방법: 선 끝이 있는 선 그리기
선 끝이 호출 하는 여러 도형 중 하나에서 시작 또는 줄의 끝에 그릴 수 있습니다. GDI + 화살촉 라운드, 사각형, 다이아몬드 등 여러 선 끝이 지원합니다.  
  
## <a name="example"></a>예제  
 줄 (시작 cap), (end cap) 줄의 끝 또는 파선 (dash cap)의 대시의 시작 부분에 대 한 선 끝 모양을 지정할 수 있습니다.  
  
 다음 예제에는 한쪽 end에 있는 화살촉이와 다른 끝에 있는 둥근 단면 선을 그립니다. 그림 결과 줄을 보여 줍니다.  
  
 ![둥근 끝에 있는 줄을 보여 주는 그림입니다.](./media/how-to-draw-a-line-with-line-caps/line-cap-arrowhead-example.gif)  
  
 [!code-csharp[System.Drawing.UsingAPen#71](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#71)]
 [!code-vb[System.Drawing.UsingAPen#71](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#71)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- Windows Form 만들기 및 폼의 처리 <xref:System.Windows.Forms.Control.Paint> 이벤트입니다. 예제 코드를 붙여 합니다 <xref:System.Windows.Forms.Control.Paint> 전달 하는 이벤트 처리기 `e` 으로 <xref:System.Windows.Forms.PaintEventArgs>합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Pen?displayProperty=nameWithType>
- <xref:System.Drawing.Drawing2D.LineCap?displayProperty=nameWithType>
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [펜을 사용하여 선과 도형 그리기](using-a-pen-to-draw-lines-and-shapes.md)
