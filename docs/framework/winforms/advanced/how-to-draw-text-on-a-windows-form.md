---
title: '방법: Windows Form에서 텍스트 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- forms [Windows Forms], drawing text
- text [Windows Forms], drawing
ms.assetid: 5d2447a9-21a1-4adc-b954-5516f2bb9b2c
ms.openlocfilehash: dc99a863765cd617c2ab4a636286f42f5e8daf79
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64626189"
---
# <a name="how-to-draw-text-on-a-windows-form"></a>방법: Windows Form에서 텍스트 그리기
다음 코드 예제를 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Drawing.Graphics.DrawString%2A> 메서드는 <xref:System.Drawing.Graphics> 폼에 텍스트를 그리는 합니다. 사용할 수 있습니다 <xref:System.Windows.Forms.TextRenderer> 폼에 텍스트를 그리기 위한 합니다. 자세한 내용은 [방법: GDI 사용 하 여 텍스트 그리기](how-to-draw-text-with-gdi.md)합니다.  
  
## <a name="example"></a>예제  
 [!code-cpp[System.Drawing.ConceptualHowTos#7](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#7)]
 [!code-csharp[System.Drawing.ConceptualHowTos#7](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#7)]
 [!code-vb[System.Drawing.ConceptualHowTos#7](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#7)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 호출할 수 없습니다는 <xref:System.Drawing.Graphics.DrawString%2A> 의 메서드는 <xref:System.Windows.Forms.Form.Load> 이벤트 처리기입니다. 그려지는 콘텐츠 비활성 폼 크기가 조정 되거나 다른 양식으로 하는 경우. 재정의 해야 하는 자동으로 다시 그리기 콘텐츠를 확인 하는 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서 예외가 발생합니다.  
  
- Arial 글꼴이 설치 되지 않았습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Graphics.DrawString%2A>
- <xref:System.Windows.Forms.TextRenderer.DrawText%2A>
- <xref:System.Drawing.StringFormat.FormatFlags%2A>
- <xref:System.Drawing.StringFormatFlags>
- <xref:System.Windows.Forms.TextFormatFlags>
- <xref:System.Windows.Forms.Control.OnPaint%2A>
- [그래픽 프로그래밍 시작](getting-started-with-graphics-programming.md)
- [방법: GDI 사용 하 여 텍스트 그리기](how-to-draw-text-with-gdi.md)
