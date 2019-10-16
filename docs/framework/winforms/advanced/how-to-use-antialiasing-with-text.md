---
title: '방법: 텍스트에 앤티 앨리어싱 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [Windows Forms], smoothing drawn
- antialiasing [Windows Forms], using with text
- text [Windows Forms], smoothing
- text [Windows Forms], antialiasing
- strings [Windows Forms], antialiasing when drawing
ms.assetid: 48fc34f3-f236-4b01-a0cb-f0752e6d22ae
ms.openlocfilehash: 080d946bd72da8b76ed846efdf149eb328d66336
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505721"
---
# <a name="how-to-use-antialiasing-with-text"></a>방법: 텍스트에 앤티 앨리어싱 사용
*앤티 앨리어싱* 그려지는 그래픽 및 텍스트의 모양을 가독성을 향상 시키는 거친 다듬기 가리킵니다. 관리 되는 GDI + 클래스를 사용 하 여 고품질 앤티 앨리어싱된 텍스트 뿐만 아니라 낮은 품질의 텍스트를 렌더링할 수 있습니다. 일반적으로 더 높은 품질 렌더링 낮은 품질 렌더링 보다 처리 시간이 사용 합니다. 텍스트 품질 수준을 설정 하려면 설정 합니다 <xref:System.Drawing.Graphics.TextRenderingHint%2A> 의 속성을 <xref:System.Drawing.Graphics> 의 요소 중 하나에 <xref:System.Drawing.Text.TextRenderingHint> 열거형  
  
## <a name="example"></a>예제  
 다음 코드 예제는 두 개의 다른 품질 설정으로 텍스트를 그립니다.  
  
 [!code-csharp[System.Drawing.FontsAndText#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.FontsAndText#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#21)]  
 
 다음 그림에서는 예제 코드의 출력을 보여 줍니다.  
  
 ![두 개의 다른 품질 설정으로 텍스트를 보여 주는 스크린샷.](./media/how-to-use-antialiasing-with-text/antialiasing-text-quality-settings.png)  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 코드 예제는 Windows Forms에서 사용 하도록 설계 되었으며 필요 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- [글꼴 및 텍스트 사용](using-fonts-and-text.md)
