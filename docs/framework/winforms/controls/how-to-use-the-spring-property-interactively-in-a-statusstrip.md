---
title: '방법: StatusStrip에서 대화형으로 Spring 속성 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- StatusStrip control [Windows Forms]
- ToolStrip control [Windows Forms]
- status bars [Windows Forms], examples
- Spring property [Windows Forms]
ms.assetid: 18bde842-a93c-48dd-9db3-15738a1775ce
ms.openlocfilehash: 8750c48d08161260a1dba6ab69098980f25a5d55
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65589644"
---
# <a name="how-to-use-the-spring-property-interactively-in-a-statusstrip"></a>방법: StatusStrip에서 대화형으로 Spring 속성 사용
<xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> 속성을 사용하여 <xref:System.Windows.Forms.ToolStripStatusLabel> 컨트롤을 <xref:System.Windows.Forms.StatusStrip> 컨트롤에 배치할 수 있습니다. <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> 속성은 <xref:System.Windows.Forms.ToolStripStatusLabel> 컨트롤이 <xref:System.Windows.Forms.StatusStrip> 컨트롤에서 사용 가능한 공간을 자동으로 채울지 여부를 결정합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> 속성을 사용하여 <xref:System.Windows.Forms.ToolStripStatusLabel> 컨트롤을 <xref:System.Windows.Forms.StatusStrip> 컨트롤에 배치하는 방법을 보여 줍니다. <xref:System.Windows.Forms.ToolStripItem.Click> 이벤트 처리기는 XOR(배타적 OR) 연산을 수행하여 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> 속성의 값을 전환합니다.  
  
 이 코드 예제를 사용 하려면 컴파일하고 응용 프로그램을 실행 한 다음 클릭 **중간 (Spring)** 에 <xref:System.Windows.Forms.StatusStrip> 컨트롤의 값을 전환 합니다 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> 속성입니다.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#1)]  
[!code-csharp[System.Windows.Forms.ToolStrip.Misc#50](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#50)]
[!code-vb[System.Windows.Forms.ToolStrip.Misc#50](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#50)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System.Design, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStripStatusLabel>
- <xref:System.Windows.Forms.StatusStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.ToolStripItem>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [ToolStrip 컨트롤](toolstrip-control-windows-forms.md)
