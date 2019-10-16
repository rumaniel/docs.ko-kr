---
title: '방법: 사용자 지정 파선 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lines [Windows Forms], custom
- lines [Windows Forms], drawing
- lines [Windows Forms], dashed
ms.assetid: cd0ed96a-cce4-47b9-b58a-3bae2e3d1bee
ms.openlocfilehash: d2184a8d7d7f24b8f631818608ab4bcdb89857c7
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506040"
---
# <a name="how-to-draw-a-custom-dashed-line"></a>방법: 사용자 지정 파선 그리기
GDI +에 나와 있는 여러 가지 대시 스타일을 제공 합니다.는 <xref:System.Drawing.Drawing2D.DashStyle> 열거형입니다. 이러한 표준 대시 스타일 사용자 요구에 적합 하지 않는 경우 사용자 지정 대시 패턴을 만들 수 있습니다.  
  
## <a name="example"></a>예제  
 사용자 지정 파선을 그리려면 대시와 공백의 길이 배열에 배치 하 고 값으로 배열을 할당 합니다 <xref:System.Drawing.Pen.DashPattern%2A> 의 속성을 <xref:System.Drawing.Pen> 개체입니다. 다음 예제에서는 배열을 기반으로 사용자 지정 파선 그립니다 `{5, 2, 15, 4}`합니다. 배열 요소의 5의 펜 너비를 곱하면 경우 `{25, 10, 75, 20}`합니다. 25 사이의 75는 길이가 표시 된 대시 대체 하 고 길이가 10과 20 사이의 공간을 대체 합니다.  
  
 다음 그림에서는 결과 파선을 보여 줍니다. 최종 대시 줄 끝날 수 있도록 25 단위 보다 짧을 수에 (405, 5).  
  
 ![파선을 보여 주는 그림입니다. ](./media/how-to-draw-a-custom-dashed-line/dashed-line-illustration.gif "pens6")  
  
 [!code-csharp[System.Drawing.UsingAPen#51](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.UsingAPen#51](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#51)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 Windows Form 만들기 및 폼의 처리 <xref:System.Windows.Forms.Control.Paint> 이벤트입니다. 앞의 코드를 붙여를 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기입니다.  
  
## <a name="see-also"></a>참고자료

- [펜을 사용하여 선과 도형 그리기](using-a-pen-to-draw-lines-and-shapes.md)
