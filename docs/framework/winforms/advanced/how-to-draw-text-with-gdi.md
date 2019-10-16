---
title: '방법: GDI를 사용하여 텍스트 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- GDI [Windows Forms], drawing text [Windows Forms]
- text [Windows Forms], drawing with TextRenderer
- drawing [Windows Forms], text
- Windows Forms, drawing text with GDI
ms.assetid: 2a19fe5d-2ace-451c-94db-01cb1118ef7b
ms.openlocfilehash: 3ed2b5c94e4a38a5873a34e61287c4038cab5cbb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956538"
---
# <a name="how-to-draw-text-with-gdi"></a>방법: GDI를 사용하여 텍스트 그리기
클래스의 메서드를 사용 하 여 폼 이나 컨트롤에 텍스트를 그리기 위한 GDI 기능에 액세스할 수 있습니다. <xref:System.Windows.Forms.TextRenderer.DrawText%2A> <xref:System.Windows.Forms.TextRenderer> GDI 텍스트 렌더링은 일반적으로 GDI + 보다 더 나은 성능 및 보다 정확한 텍스트 측정을 제공 합니다.  
  
> [!NOTE]
> 합니다 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 의 메서드는 <xref:System.Windows.Forms.TextRenderer> 인쇄에 대 한 클래스를 사용할 수 없습니다. 인쇄 하는 경우 항상 <xref:System.Drawing.Graphics.DrawString%2A> <xref:System.Drawing.Graphics> 클래스의 메서드를 사용 합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 메서드를 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 사용 하 여 사각형 내의 여러 줄에 텍스트를 그리는 방법을 보여 줍니다.  
  
 [!code-csharp[System.Windows.Forms.TextRendererExamples#7](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/CS/Form1.cs#7)]
 [!code-vb[System.Windows.Forms.TextRendererExamples#7](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/VB/Form1.vb#7)]  
  
 <xref:System.Windows.Forms.TextRenderer> 클래스를 사용 하 여 텍스트를 렌더링 하려면 <xref:System.Drawing.Graphics> 및 <xref:System.Drawing.Font>와 같은, 텍스트를 그릴 위치 및 그려야 하는 색을 사용 <xref:System.Drawing.IDeviceContext>해야 합니다. 필요에 따라 <xref:System.Windows.Forms.TextFormatFlags> 열거를 사용 하 여 텍스트 서식을 지정할 수 있습니다.  
  
 <xref:System.Drawing.Graphics> 을[가져오는 방법에 대 한 자세한 내용은 방법: 그리기](how-to-create-graphics-objects-for-drawing.md)를 위한 그래픽 개체를 만듭니다. <xref:System.Drawing.Font> 를[구성 하는 방법에 대 한 자세한 내용은 방법: 글꼴 패밀리 및 글꼴](how-to-construct-font-families-and-fonts.md)을 생성 합니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 위의 코드 예제는 Windows Forms와 함께 사용 하도록 설계 되었으며의 <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Windows.Forms.PaintEventHandler>매개 변수인가 필요 `e`합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TextRenderer>
- <xref:System.Drawing.Font>
- <xref:System.Drawing.Color>
- [글꼴 및 텍스트 사용](using-fonts-and-text.md)
