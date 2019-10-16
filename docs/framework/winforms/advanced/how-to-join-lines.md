---
title: '방법: 선 조인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- miter line join style
- bevel line join style
- line join
- drawing [Windows Forms], joining lines
- GraphicsPath object
- round line join style
- lines [Windows Forms], joining
- graphics [Windows Forms], joining lines
ms.assetid: 9fc480c2-3c75-4fd1-8ab5-296a99e820e2
ms.openlocfilehash: 362ce0c701d6e5f640fecd143a60cf471045629c
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505873"
---
# <a name="how-to-join-lines"></a>방법: 선 조인
선 조인에 끝 부분이 만나거나 겹치는 두 줄으로 구성 되는 일반적인 영역입니다. GDI +-세 선 조인 스타일을 제공 하는 중: 마이터, 빗면 및 반올림 합니다. 선 조인 스타일의 속성인는 <xref:System.Drawing.Pen> 클래스입니다. 선 조인 스타일을 지정 하는 경우는 <xref:System.Drawing.Pen> 개체에 연결 된 모든 줄에 조인 스타일을 적용할 <xref:System.Drawing.Drawing2D.GraphicsPath> 개체는 펜을 사용 하 여 그려집니다.  
  
 다음 그림에서는 빗면된 선 조인 예제 결과 보여 줍니다.  
  
 ![조인된 선을 보여 주는 그림입니다.](./media/how-to-join-lines/joined-beveled-lines.gif)  
  
## <a name="example"></a>예제  
 사용 하 여 선 조인 스타일을 지정할 수 있습니다는 <xref:System.Drawing.Pen.LineJoin%2A> 의 속성을 <xref:System.Drawing.Pen> 클래스입니다. 이 예제에서는 빗면된 선 조인을 가로 줄 사이의 세로 줄을 보여 줍니다. 다음 코드에서 값 <xref:System.Drawing.Drawing2D.LineJoin.Bevel> 에 할당 합니다 <xref:System.Drawing.Pen.LineJoin%2A> 속성이 멤버인은 <xref:System.Drawing.Drawing2D.LineJoin> 열거형. 다른 멤버를 <xref:System.Drawing.Drawing2D.LineJoin> 열거 <xref:System.Drawing.Drawing2D.LineJoin.Miter> 고 <xref:System.Drawing.Drawing2D.LineJoin.Round>입니다.  
  
 [!code-csharp[System.Drawing.UsingAPen#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingAPen#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#31)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- [펜을 사용하여 선과 도형 그리기](using-a-pen-to-draw-lines-and-shapes.md)
