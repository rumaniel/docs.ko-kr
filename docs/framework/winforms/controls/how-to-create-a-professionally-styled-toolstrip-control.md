---
title: '방법: 전문적인 스타일의 ToolStrip 컨트롤 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- toolbars [Windows Forms]
- ToolStripProfessionalRenderer class [Windows Forms]
- ToolStripRenderer class [Windows Forms]
- ToolStrip control [Windows Forms]
ms.assetid: c208b2f6-8105-474b-9075-d582e1792870
ms.openlocfilehash: 4e4e899d583eb87b3ced7161f1fd274c0bcc591c
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65586558"
---
# <a name="how-to-create-a-professionally-styled-toolstrip-control"></a>방법: 전문적인 스타일의 ToolStrip 컨트롤 만들기
<xref:System.Windows.Forms.ToolStripProfessionalRenderer> 형식에서 파생된 고유한 클래스를 작성하여 애플리케이션의 <xref:System.Windows.Forms.ToolStrip> 컨트롤에 전문적인 모양과 동작(모양 및 느낌)을 제공할 수 있습니다.  
  
 Visual Studio에서이 기능에 대해 폭넓게 지원이 됩니다.  
  
 [연습: 전문적인 스타일의 ToolStrip 컨트롤 만들기](walkthrough-creating-a-professionally-styled-toolstrip-control.md)합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에 사용 하는 방법을 보여 줍니다 <xref:System.Windows.Forms.ToolStrip> 과 비슷한 복합 컨트롤을 만들 컨트롤에는 **탐색 창** Microsoft® Outlook®에서 제공 합니다.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.StackView#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.StackView#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.StatusStrip>
- [ToolStrip 컨트롤](toolstrip-control-windows-forms.md)
- [방법: 폼에 표준 메뉴 항목 제공](how-to-provide-standard-menu-items-to-a-form.md)
