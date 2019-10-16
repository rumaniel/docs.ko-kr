---
title: '방법: Windows Forms TextBox 컨트롤에서 삽입 지점 제어'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- TextBox control [Windows Forms], insertion point
- insertion points [Windows Forms], TextBox controls
- text boxes [Windows Forms], controlling insertion point
ms.assetid: 5bee7d34-5121-429e-ab1f-d8ff67bc74c1
ms.openlocfilehash: a9d8c02a05723814d074ff91c847471287588618
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64642966"
---
# <a name="how-to-control-the-insertion-point-in-a-windows-forms-textbox-control"></a>방법: Windows Forms TextBox 컨트롤에서 삽입 지점 제어
경우는 Windows Forms <xref:System.Windows.Forms.TextBox> 컨트롤의 포커스를 처음 받을, 기존 텍스트의 왼쪽에 텍스트 상자 내에서 기본 삽입 됩니다. 키보드 또는 마우스를 사용 하 여 커서를 이동할 수 있습니다. 텍스트 상자를 잃고 포커스를 다시 얻은 후, 하는 경우 아무 곳에 나 사용자 마지막으로 저장할 삽입 지점이 됩니다.  
  
 일부 경우에이 동작을 사용자에 게 혼란을 줄 수 있습니다. 단어의 처리 응용 프로그램을 사용자 기존 텍스트 뒤에 새 문자를 예상할 수 있습니다. 데이터 항목 응용 프로그램에서는 사용자 모든 기존 항목을 바꾸려면 새로운 문자 예상 합니다. 합니다 <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 고 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 속성을 사용 하는 목적에 맞게 동작을 수정할 수 있습니다.  
  
### <a name="to-control-the-insertion-point-in-a-textbox-control"></a>TextBox 컨트롤의 삽입 지점 제어  
  
1. <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 속성을 적절한 값으로 설정합니다. 0에 바로 첫 번째 문자의 왼쪽에 삽입 지점을 넣습니다.  
  
2. (선택 사항) 설정 된 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 속성을 선택 하려는 텍스트의 길이입니다.  
  
     아래 코드는 항상 0으로 삽입 포인터를 반환합니다. 합니다 `TextBox1_Enter` 이벤트 처리기에 대 한 자세한 내용은 컨트롤에 바인딩할 수 해야을 참조 하십시오 [Windows Forms에서 이벤트 처리기 만들기](../creating-event-handlers-in-windows-forms.md)합니다.  
  
    ```vb  
    Private Sub TextBox1_Enter(ByVal sender As Object, ByVal e As System.EventArgs) Handles TextBox1.Enter  
       TextBox1.SelectionStart = 0  
       TextBox1.SelectionLength = 0  
    End Sub  
    ```  
  
    ```csharp  
    private void textBox1_Enter(Object sender, System.EventArgs e) {  
       textBox1.SelectionStart = 0;  
       textBox1.SelectionLength = 0;  
    }  
    ```  
  
    ```cpp  
    private:  
       void textBox1_Enter(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          textBox1->SelectionStart = 0;  
          textBox1->SelectionLength = 0;  
       }  
    ```  
  
## <a name="making-the-insertion-point-visible-by-default"></a>삽입 지점에 기본적으로 표시 하기  
 <xref:System.Windows.Forms.TextBox> 삽입 지점이 새 양식만 경우에는 기본적으로 표시 되는 <xref:System.Windows.Forms.TextBox> 컨트롤은 탭 순서에서 첫 번째입니다. 삽입 지점을 제공 하는 경우에 표시 되는 고, 그렇지는 <xref:System.Windows.Forms.TextBox> 키보드 또는 마우스를 사용 하 여 포커스를 합니다.  
  
#### <a name="to-make-the-text-box-insertion-point-visible-by-default-on-a-new-form"></a>새 폼에는 기본적으로 텍스트 상자 삽입 지점을 표시 하려면  
  
- 설정 된 <xref:System.Windows.Forms.TextBox> 컨트롤의 <xref:System.Windows.Forms.Control.TabIndex%2A> 속성을 `0`입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TextBox>
- [TextBox 컨트롤 개요](textbox-control-overview-windows-forms.md)
- [방법: Windows Forms TextBox 컨트롤을 사용 하 여 암호 텍스트 상자 만들기](how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)
- [방법: 읽기 전용 텍스트 상자 만들기](how-to-create-a-read-only-text-box-windows-forms.md)
- [방법: 문자열에 인용 부호 넣기](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [방법: Windows Forms TextBox 컨트롤에서 텍스트를 선택 합니다.](how-to-select-text-in-the-windows-forms-textbox-control.md)
- [방법: Windows Forms TextBox 컨트롤에서 여러 줄 보기](how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)
- [TextBox 컨트롤](textbox-control-windows-forms.md)
