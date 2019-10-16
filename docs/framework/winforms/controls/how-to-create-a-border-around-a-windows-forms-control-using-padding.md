---
title: '방법: 안쪽 여백을 사용하여 Windows Forms 컨트롤 주위에 테두리 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- margins
- controls [Windows Forms], Margin property
- padding [Windows Forms], Windows Forms
- controls [Windows Forms], Padding property
- controls [Windows Forms], outlining
- Padding property [Windows Forms]
- margins [Windows Forms], Windows Forms
- Margin property [Windows Forms]
ms.assetid: bac7ed4d-a163-4259-98bd-155a36345890
ms.openlocfilehash: e3bbf43dbe45e675df172a6c3e1db16a3ba9caa8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61746881"
---
# <a name="how-to-create-a-border-around-a-windows-forms-control-using-padding"></a>방법: 안쪽 여백을 사용하여 Windows Forms 컨트롤 주위에 테두리 만들기
다음 코드 예제에 테두리 만들기 관련 간략하게 설명 하는 방법을 보여 줍니다는 <xref:System.Windows.Forms.RichTextBox> 제어 합니다. 값을 설정 하는 예제는 <xref:System.Windows.Forms.Panel> 컨트롤의 <xref:System.Windows.Forms.Padding> 속성을 5로 설정 합니다 <xref:System.Windows.Forms.Control.Dock%2A> 자식 속성 <xref:System.Windows.Forms.RichTextBox> 컨트롤을 <xref:System.Windows.Forms.DockStyle.Fill>입니다. <xref:System.Windows.Forms.Control.BackColor%2A> 의 합니다 <xref:System.Windows.Forms.Panel> 로 설정 되어 <xref:System.Drawing.Color.Blue%2A>, 주위에 파란색 테두리가 만듭니다는 <xref:System.Windows.Forms.RichTextBox> 컨트롤입니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.Padding#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Padding/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.Padding#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Padding/VB/Form1.vb#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Padding>
- [Windows Forms 컨트롤의 여백 및 안쪽 여백](margin-and-padding-in-windows-forms-controls.md)
