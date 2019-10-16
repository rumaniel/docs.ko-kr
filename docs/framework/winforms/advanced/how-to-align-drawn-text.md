---
title: '방법: 그린 텍스트 맞추기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [Windows Forms], aligning
- Windows Forms, aligning drawn text
ms.assetid: 83c10a81-1a90-4b5c-98aa-2c6c4b280079
ms.openlocfilehash: 3a569284a1c4b43fa7264e0354934436f95b8dc3
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65589386"
---
# <a name="how-to-align-drawn-text"></a>방법: 그린 텍스트 맞추기
사용자 지정 그리기를 수행 하면 폼 이나 컨트롤에서 그린된 텍스트를 가운데 하려는 경우가 많습니다. 사용 하 여 그린 텍스트를 쉽게 맞출 수 있습니다 합니다 <xref:System.Drawing.Graphics.DrawString%2A> 또는 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 올바른 서식 지정 개체를 만들고 적절 한 형식 플래그를 설정 하 여 메서드.  
  
### <a name="to-draw-centered-text-with-gdi-drawstring"></a>그릴 GDI + (DrawString)를 사용 하 여 텍스트를 가운데  
  
1. 사용 된 <xref:System.Drawing.StringFormat> 적절 한 <xref:System.Drawing.Graphics.DrawString%2A> 가운데 맞춤 된 텍스트를 지정 하는 방법입니다.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#10)]
     [!code-vb[System.Drawing.AlignDrawnText#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#10)]  
  
### <a name="to-draw-centered-text-with-gdi-drawtext"></a>그릴 GDI (DrawText)를 사용 하 여 텍스트를 가운데  
  
1. 사용 된 <xref:System.Windows.Forms.TextFormatFlags> 래핑 수 있을 뿐만 아니라 적절 한 텍스트를 가로 및 세로로 가운데 맞춤에 대 한 열거형 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 메서드.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#20)]
     [!code-vb[System.Drawing.AlignDrawnText#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#20)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 코드 예제 Windows Forms에서 사용 하도록 설계 되었으며 필요할 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- [방법: GDI 사용 하 여 텍스트 그리기](how-to-draw-text-with-gdi.md)
- [글꼴 및 텍스트 사용](using-fonts-and-text.md)
- [방법: 글꼴 패밀리 및 글꼴 만들기](how-to-construct-font-families-and-fonts.md)
