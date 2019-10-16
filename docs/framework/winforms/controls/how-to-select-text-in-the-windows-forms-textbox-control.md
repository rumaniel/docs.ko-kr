---
title: '방법: Windows Forms TextBox 컨트롤에서 텍스트 선택'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- TextBox control [Windows Forms], selecting text programmatically
- text boxes [Windows Forms], selecting text programmatically
- text [Windows Forms], selecting in text boxes programmatically
ms.assetid: 8c591546-6a01-45c7-8e03-f78431f903b1
ms.openlocfilehash: 3bb1245cd47084935d632ff345a32058db6074e1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62013298"
---
# <a name="how-to-select-text-in-the-windows-forms-textbox-control"></a>방법: Windows Forms TextBox 컨트롤에서 텍스트 선택
Windows Forms에서 프로그래밍 방식으로 텍스트를 선택할 수 있습니다 <xref:System.Windows.Forms.TextBox> 제어 합니다. 예를 들어, 특정 문자열에 대 한 텍스트를 검색 하는 함수를 만드는 경우에 텍스트 판독기는 검색된 된 문자열의 위치를 시각적으로 경고를 선택할 수 있습니다.  
  
### <a name="to-select-text-programmatically"></a>프로그래밍 방식으로 텍스트를 선택 하려면  
  
1. 설정 된 <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 선택 하려는 텍스트의 시작 부분에는 속성입니다.  
  
     <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 되 고 가장 왼쪽에 위치 0을 사용 하 여, 속성이 텍스트 문자열 내에 삽입 지점을 나타내는 숫자입니다. 경우는 <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> 속성 값의 문자 수보다 크거나 같은 텍스트 상자에, 삽입 지점을 마지막 문자 뒤에 배치 됩니다.  
  
2. 설정 된 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 속성을 선택 하려는 텍스트의 길이입니다.  
  
     <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 속성이 삽입 포인터의 너비를 설정 하는 숫자 값입니다. 설정 된 <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> 큰 수로 해당 선택할 문자 수를 0 보다 시작에서 현재 삽입 지점입니다.  
  
3. (선택 사항) 선택한 텍스트를 통해 액세스 된 <xref:System.Windows.Forms.TextBoxBase.SelectedText%2A> 속성입니다.  
  
     선택 아래 코드는 텍스트 내용의 상자 컨트롤의 <xref:System.Windows.Forms.Control.Enter> 이벤트가 발생 합니다. 이 예제에서는 텍스트 상자에 대 한 값에 있는지를 확인 합니다 <xref:System.Windows.Forms.TextBox.Text%2A> 하지 않은 속성에 `null` 또는 빈 문자열입니다. 텍스트 상자에 포커스를 받으면 텍스트 상자의 현재 텍스트 선택 됩니다. 합니다 `TextBox1_Enter` 이벤트 처리기 합니다 자세한 내용은 컨트롤에 바인딩할 수 내용은 [방법: 런타임에 Windows Forms에 대 한 이벤트 처리기를 만들](../how-to-create-event-handlers-at-run-time-for-windows-forms.md)합니다.  
  
     이 예제를 테스트 하려면 텍스트 상자에 포커스가 놓일 때까지 Tab 키를 누릅니다. 텍스트 상자를 클릭 하면 텍스트 선택이 취소 됩니다.  
  
    ```vb  
    Private Sub TextBox1_Enter(ByVal sender As Object, ByVal e As System.EventArgs) Handles TextBox1.Enter  
       If (Not String.IsNullOrEmpty(TextBox1.Text)) Then  
          TextBox1.SelectionStart = 0  
          TextBox1.SelectionLength = TextBox1.Text.Length  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void textBox1_Enter(object sender, System.EventArgs e){  
       if (!String.IsNullOrEmpty(textBox1.Text))  
       {  
          textBox1.SelectionStart = 0;  
          textBox1.SelectionLength = textBox1.Text.Length;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void textBox1_Enter(System::Object ^ sender,  
          System::EventArgs ^ e) {  
       if (!System::String::IsNullOrEmpty(textBox1->Text))  
       {  
          textBox1->SelectionStart = 0;  
          textBox1->SelectionLength = textBox1->Text->Length;  
       }  
    }  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TextBox>
- [TextBox 컨트롤 개요](textbox-control-overview-windows-forms.md)
- [방법: Windows Forms TextBox 컨트롤의 삽입 지점 제어](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [방법: Windows Forms TextBox 컨트롤을 사용 하 여 암호 텍스트 상자 만들기](how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)
- [방법: 읽기 전용 텍스트 상자 만들기](how-to-create-a-read-only-text-box-windows-forms.md)
- [방법: 문자열에 인용 부호 넣기](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [방법: Windows Forms TextBox 컨트롤에서 여러 줄 보기](how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)
- [TextBox 컨트롤](textbox-control-windows-forms.md)
