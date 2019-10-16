---
title: '방법: Windows Forms RichTextBox 컨트롤을 사용하여 들여쓰기, 내어쓰기 및 글머리 기호 단락 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- text boxes [Windows Forms], setting indents
- .rtf files [Windows Forms], formatting in RichTextBox control
- examples [Windows Forms], text boxes
- RTF files [Windows Forms], formatting in RichTextBox control
- RichTextBox control [Windows Forms], setting indents and bullets
- text boxes [Windows Forms], bullets
ms.assetid: abfb40e6-5642-4691-8ec1-9d9ae91688dc
ms.openlocfilehash: 9d095e3561cd346e6dbd99d1be7468f6ad5725a6
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960449"
---
# <a name="how-to-set-indents-hanging-indents-and-bulleted-paragraphs-with-the-windows-forms-richtextbox-control"></a>방법: Windows Forms RichTextBox 컨트롤을 사용하여 들여쓰기, 내어쓰기 및 글머리 기호 단락 설정
Windows Forms <xref:System.Windows.Forms.RichTextBox> 컨트롤에는 표시 되는 텍스트의 서식을 지정 하는 다양 한 옵션이 있습니다. 속성을 <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A> 설정 하 여 선택한 단락의 서식을 글머리 기호 목록으로 지정할 수 있습니다. 또한, 및 <xref:System.Windows.Forms.RichTextBox.SelectionIndent%2A> <xref:System.Windows.Forms.RichTextBox.SelectionRightIndent%2A>속성을 사용 하 여 컨트롤의 왼쪽 및 오른쪽 가장자리와 다른 텍스트 줄의 왼쪽 가장자리를 기준으로 단락의 들여쓰기를 설정할 수 있습니다. <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A>  
  
### <a name="to-format-a-paragraph-as-a-bulleted-list"></a>단락의 서식을 글머리 기호 목록으로 지정하려면  
  
1. <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A> 속성을 `true`으로 설정합니다.  
  
    ```vb  
    RichTextBox1.SelectionBullet = True  
    ```  
  
    ```csharp  
    richTextBox1.SelectionBullet = true;  
    ```  
  
    ```cpp  
    richTextBox1->SelectionBullet = true;  
    ```  
  
### <a name="to-indent-a-paragraph"></a>단락을 들여쓰려면  
  
1. 컨트롤의 왼쪽 가장자리와 텍스트의 왼쪽 가장자리 사이의 거리 (픽셀)를 나타내는 정수로 속성을설정합니다.<xref:System.Windows.Forms.RichTextBox.SelectionIndent%2A>  
  
2. 단락에 있는 첫 번째 텍스트 줄의 왼쪽 가장자리와 다음 줄의 왼쪽 가장자리 사이의 거리 (픽셀)를 나타내는 정수로 속성을설정합니다.<xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A> <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A> 속성의 값은 첫 번째 줄 아래에 래핑된 단락의 줄에만 적용 됩니다.  
  
3. 컨트롤의 오른쪽 가장자리와 텍스트의 오른쪽 가장자리 사이의 거리 (픽셀)를 나타내는 정수로 속성을설정합니다.<xref:System.Windows.Forms.RichTextBox.SelectionRightIndent%2A>  
  
    ```vb  
    RichTextBox1.SelectionIndent = 8  
    RichTextBox1.SelectionHangingIndent = 3  
    RichTextBox1.SelectionRightIndent = 12  
    ```  
  
    ```csharp  
    richTextBox1.SelectionIndent = 8;  
    richTextBox1.SelectionHangingIndent = 3;  
    richTextBox1.SelectionRightIndent = 12;  
    ```  
  
    ```cpp  
    richTextBox1->SelectionIndent = 8;  
    richTextBox1->SelectionHangingIndent = 3;  
    richTextBox1->SelectionRightIndent = 12;  
    ```  
  
    > [!NOTE]
    > 이러한 모든 속성은 선택한 텍스트가 포함된 단락에 적용되며, 현재 삽입 지점 이후로 입력된 텍스트에도 적용됩니다. 예를 들어 사용자가 단락 내의 단어를 선택한 다음 들여쓰기를 조정하면, 이 단어가 포함된 전체 단락뿐만 아니라 선택한 단락 이후에 입력되는 모든 단락에도 새 설정이 적용됩니다. 프로그래밍 방식으로 텍스트를 선택 하는 <xref:System.Windows.Forms.TextBoxBase.Select%2A>방법은을 참조 하십시오.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox 컨트롤](richtextbox-control-windows-forms.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
