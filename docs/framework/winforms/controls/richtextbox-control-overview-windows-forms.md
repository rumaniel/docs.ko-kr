---
title: RichTextBox 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- RichTextBox
helpviewer_keywords:
- RichTextBox control [Windows Forms], about RichTextBox control
- text boxes [Windows Forms], about text boxes
ms.assetid: 95081194-3dd4-4b84-9545-dd373e491eca
ms.openlocfilehash: 0827c1919597e9eb85bfa41721676008b76564d9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61902501"
---
# <a name="richtextbox-control-overview-windows-forms"></a>RichTextBox 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.RichTextBox> 표시, 입력 및 서식 있는 텍스트를 조작에 대 한 컨트롤을 사용 합니다. 합니다 <xref:System.Windows.Forms.RichTextBox> 모든 작업을 수행 하는 컨트롤을 <xref:System.Windows.Forms.TextBox> 제어 하지만 또한 글꼴, 색 및 링크를 표시, 텍스트 및 포함 된 이미지 파일에서 로드 및 지정 된 문자를 찾습니다. <xref:System.Windows.Forms.RichTextBox> 컨트롤은 일반적으로 텍스트를 조작 하 고 Microsoft Word와 같은 워드 프로세싱 응용 프로그램과 유사한 기능을 표시 하는 데 사용 됩니다. 같은 <xref:System.Windows.Forms.TextBox> 컨트롤을 <xref:System.Windows.Forms.RichTextBox> 컨트롤에서 스크롤 막대를 표시할 수 있습니다 달리 있지만 <xref:System.Windows.Forms.TextBox> 필요에 따라 가로 및 세로 스크롤 막대를 표시 하는 컨트롤을 기본 설정인 것 있고 추가 스크롤 막대.  
  
## <a name="working-with-the-richtextbox-control"></a>RichTextBox 컨트롤 작업  
 와 마찬가지로 합니다 <xref:System.Windows.Forms.TextBox> 컨트롤 표시할 텍스트를 설정 합니다 <xref:System.Windows.Forms.RichTextBox.Text%2A> 속성입니다. <xref:System.Windows.Forms.RichTextBox> 컨트롤에 텍스트 서식을 지정 하려면 다양 한 속성이 있습니다. 이러한 속성에 대 한 자세한 내용은 참조 하세요. [방법: Windows Forms RichTextBox 컨트롤에 대 한 글꼴 특성 설정](how-to-set-font-attributes-for-the-windows-forms-richtextbox-control.md) 고 [방법: 들여쓰기, 내어쓰기 및 글머리 기호 단락 Windows Forms RichTextBox 컨트롤을 사용 하 여 설정](set-indents-hanging-indents-bulleted-paragraphs-with-wf-richtextbox.md)합니다. 파일을 조작 하는 <xref:System.Windows.Forms.RichTextBox.LoadFile%2A> 및 <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> 메서드를 표시 하 고 일반 텍스트, 유니코드 일반 텍스트 및 RTF 서식 있는 텍스트 ()를 포함 하 여 여러 파일 형식을 작성할 수 있습니다. 가능한 파일 형식은 나오는 <xref:System.Windows.Forms.RichTextBoxStreamType>합니다. 사용할 수는 <xref:System.Windows.Forms.RichTextBox.Find%2A> 메서드를 특정 문자 또는 텍스트 문자열을 찾습니다.  
  
 사용할 수도 있습니다는 <xref:System.Windows.Forms.RichTextBox> 설정 하 여 웹 스타일 링크에 대 한 제어를 <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A> 속성을 `true` 처리 하는 코드를 작성 하 고는 <xref:System.Windows.Forms.RichTextBox.LinkClicked> 이벤트입니다. 자세한 내용은 [방법: Windows 사용 하 여 웹 스타일 링크 표시 Forms RichTextBox 컨트롤](how-to-display-web-style-links-with-the-windows-forms-richtextbox-control.md)합니다. 일부 또는 모든 컨트롤의 텍스트를 설정 하 여 조작에서 사용자를 방지할 수 있습니다 합니다 <xref:System.Windows.Forms.RichTextBox.SelectionProtected%2A> 속성을 `true`입니다.  
  
 실행 취소 및 대부분의 편집 작업을 다시 실행할 수는 <xref:System.Windows.Forms.RichTextBox> 호출 하 여 컨트롤을 <xref:System.Windows.Forms.TextBoxBase.Undo%2A> 및 <xref:System.Windows.Forms.RichTextBox.Redo%2A> 메서드. <xref:System.Windows.Forms.RichTextBox.CanRedo%2A> 메서드를 사용 하면 사용자가 실행 취소 한 마지막 작업 컨트롤에 다시 적용할 수 있는지 여부를 확인할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox 컨트롤](richtextbox-control-windows-forms.md)
- [TextBox 컨트롤 개요](textbox-control-overview-windows-forms.md)
