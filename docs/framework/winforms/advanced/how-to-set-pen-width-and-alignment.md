---
title: '방법: 펜 굵기 및 맞춤 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pens [Windows Forms], setting width
- pens [Windows Forms], setting alignment
ms.assetid: a202af36-4d31-4401-a126-b232f51db581
ms.openlocfilehash: 1f1ea6e8ef0b94aa46a4bf8177d59e59297d6e3f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64605829"
---
# <a name="how-to-set-pen-width-and-alignment"></a>방법: 펜 굵기 및 맞춤 설정
만들 때를 <xref:System.Drawing.Pen>를 생성자에 인수 중 하나로 펜 굵기를 제공할 수 있습니다. 펜 너비를 변경할 수도 있습니다는 <xref:System.Drawing.Pen.Width%2A> 의 속성을 <xref:System.Drawing.Pen> 클래스입니다.  
  
 이론적인 선의 너비를 0에 있습니다. 1 픽셀 너비는 줄을 그릴 때 픽셀에 이론적인 선의 가운데 맞춥니다. 둘 이상의 픽셀로 선에 그리면 픽셀 하거나 이론적인 선의에 주안점을 둡니다 또는 이론적인 선의 한쪽에 표시 됩니다. 펜 맞춤 속성을 설정할 수는 <xref:System.Drawing.Pen> 이론적인 선을 기준으로 해당 펜을 사용 하 여 그린 픽셀을 배치 하는 방식을 확인 하려면.  
  
 값 <xref:System.Drawing.Drawing2D.PenAlignment.Center>, <xref:System.Drawing.Drawing2D.PenAlignment.Outset>, 및 <xref:System.Drawing.Drawing2D.PenAlignment.Inset> 다음에 나타나는 코드 예제는의 멤버는 <xref:System.Drawing.Drawing2D.PenAlignment> 열거형입니다.  
  
 다음 코드 예제에서는 두 번 줄을 그립니다: 한 번 너비가 10의 녹색 펜 너비 1의 검은색 펜으로 한 번입니다.  
  
### <a name="to-vary-the-width-of-a-pen"></a>펜의 너비를 변경 하려면  
  
- 값을 설정 합니다 <xref:System.Drawing.Pen.Alignment%2A> 속성을 <xref:System.Drawing.Drawing2D.PenAlignment.Center> (기본값)는 녹색 펜을 사용 하 여 그린 픽셀 중심에 위치 합니다 이론적인 선의 지정 합니다. 다음 그림에서는 결과 줄을 표시 합니다.  
  
     ![녹색 강조 표시를 사용 하 여 black 얇은 선입니다.](./media/how-to-set-pen-width-and-alignment/green-pixels-centered-line.gif)  
  
     다음 코드 예제에서는 두 번 사각형을 그립니다: 한 번 너비가 10의 녹색 펜 너비 1의 검은색 펜으로 한 번입니다.  
  
     [!code-csharp[System.Drawing.UsingAPen#41](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#41)]
     [!code-vb[System.Drawing.UsingAPen#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#41)]  
  
### <a name="to-change-the-alignment-of-a-pen"></a>펜의 맞춤을 변경 하려면  
  
- 값을 설정 합니다 <xref:System.Drawing.Pen.Alignment%2A> 속성을 <xref:System.Drawing.Drawing2D.PenAlignment.Center> 녹색 펜을 사용 하 여 그린 픽셀 사각형의 경계에서 가운데 맞춤 될는 지정 합니다.  
  
     다음 그림에서는 결과 사각형을 보여 줍니다.
  
     ![녹색 강조 표시가 검정 씬 줄을 사용 하 여 그린 사각형입니다.](./media/how-to-set-pen-width-and-alignment/green-pixels-centered-rectangle.gif)  
  
     [!code-csharp[System.Drawing.UsingAPen#42](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#42)]
     [!code-vb[System.Drawing.UsingAPen#42](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#42)]  
  
### <a name="to-create-an-inset-pen"></a>삽입 펜을 만들려면  
  
- 앞의 코드 예제에서 세 번째 문은 다음과 같이 수정 하 여 녹색 펜의 맞춤을 변경 합니다.  
  
     [!code-csharp[System.Drawing.UsingAPen#43](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#43)]
     [!code-vb[System.Drawing.UsingAPen#43](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#43)]  
  
     이제 다음 그림과에서 같이 와이드 녹색 선은 픽셀 사각형의 내부에 나타납니다.
  
     ![검정 선 내에서 전체 녹색 줄을 사용 하 여 그린 사각형입니다.](./media/how-to-set-pen-width-and-alignment/green-pixels-inside-rectangle.gif)  
  
## <a name="see-also"></a>참고자료

- [펜을 사용하여 선과 도형 그리기](using-a-pen-to-draw-lines-and-shapes.md)
- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
