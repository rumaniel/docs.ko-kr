---
title: '방법: 질감으로 채워진 선 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- drawing [Windows Forms], lines
- lines [Windows Forms], texture
- drawing lines [Windows Forms], texture
ms.assetid: dc9118cc-f3c2-42e5-8173-f46d41d18fd5
ms.openlocfilehash: c0f90c298f48aeb96893bb09241faddc08d8a49d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62004289"
---
# <a name="how-to-draw-a-line-filled-with-a-texture"></a>방법: 질감으로 채워진 선 그리기
대신 단색을 사용 하 여 줄을 그릴 텍스처를 사용 하 여 줄을 그릴 수 있습니다. 선 및 곡선 질감으로 그릴 만들기를 <xref:System.Drawing.TextureBrush> 개체를 전달 <xref:System.Drawing.TextureBrush> 개체를 <xref:System.Drawing.Pen.%23ctor%2A> 생성자. 질감 브러시와 연결 된 비트맵은 평면 (눈에 보이지 않게) 타일을 사용 하 고 스트로크 펜의 바둑판식으로 배열 된 질감의 특정 픽셀을 얻는 펜은 직선이 나 곡선을 그릴 때 키를 누릅니다.  
  
## <a name="example"></a>예제  
 다음 예제는 <xref:System.Drawing.Bitmap> 파일에서 개체 `Texture1.jpg`합니다. 해당 비트맵 생성 되는 <xref:System.Drawing.TextureBrush> 개체 및 <xref:System.Drawing.TextureBrush> 개체를 생성 하는 <xref:System.Drawing.Pen> 개체입니다. 에 대 한 호출 <xref:System.Drawing.Graphics.DrawImage%2A> 왼쪽 위 모퉁이가 사용 하 여 비트맵을 그립니다 (0, 0). 에 대 한 호출 <xref:System.Drawing.Graphics.DrawEllipse%2A> 사용 하는 <xref:System.Drawing.Pen> 질감된 타원을 그릴 개체입니다.  
  
 다음 그림에서는 비트맵 및 질감된 타원을 보여 줍니다.  
  
 ![비트맵 및 질감된 타원을 보여 주는 스크린샷.](./media/how-to-draw-a-line-filled-with-a-texture/bitmap-textured-ellipse.png)  
  
 [!code-csharp[System.Drawing.UsingAPen#61](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.UsingAPen#61](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#61)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 Windows Form 만들기 및 폼의 처리 <xref:System.Windows.Forms.Control.Paint> 이벤트입니다. 앞의 코드를 붙여를 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기입니다. 대체 `Texture.jpg` 를 시스템에서 사용할 이미지를 사용 하 여 합니다.  
  
## <a name="see-also"></a>참고자료

- [펜을 사용하여 선과 도형 그리기](using-a-pen-to-draw-lines-and-shapes.md)
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
