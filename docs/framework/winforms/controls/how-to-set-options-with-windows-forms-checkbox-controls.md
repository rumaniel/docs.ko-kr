---
title: '방법: Windows Forms CheckBox 컨트롤을 사용하여 옵션 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- checked
helpviewer_keywords:
- CheckBox control [Windows Forms], checked state
- check boxes [Windows Forms], using to set options
- CheckBox control [Windows Forms], using to set options
ms.assetid: 2ac70498-7e3e-4e07-8901-ccabaeb5fd3e
ms.openlocfilehash: 881996563acef36a1981ca6236c155b8fc56ef0a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62013207"
---
# <a name="how-to-set-options-with-windows-forms-checkbox-controls"></a>방법: Windows Forms CheckBox 컨트롤을 사용하여 옵션 설정
Windows Forms <xref:System.Windows.Forms.CheckBox> 컨트롤 True/False 사용자에 게 제공 하는 데 사용 됩니다 또는 예/아니요 옵션입니다. 컨트롤이 선택 될 때 확인 표시를 표시 합니다.  
  
### <a name="to-set-options-with-checkbox-controls"></a>CheckBox 컨트롤을 사용 하 여 옵션을 설정 하려면  
  
1. 값을 검사 합니다 <xref:System.Windows.Forms.CheckBox.Checked%2A> 속성을 해당 상태를 확인 하 고 해당 값을 사용 하 여 옵션을 설정 합니다.  
  
     경우 아래 코드 샘플에서는 합니다 <xref:System.Windows.Forms.CheckBox> 컨트롤의 <xref:System.Windows.Forms.CheckBox.CheckedChanged> 이벤트가 발생 양식의 <xref:System.Windows.Forms.Control.AllowDrop%2A> 속성이 `false` 확인란을 선택 하는 경우. 사용자 상호 작용을 제한 하려는 경우에 유용 합니다.  
  
    ```vb  
    Private Sub CheckBox1_CheckedChanged(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles CheckBox1.CheckedChanged  
       ' Determine the CheckState of the check box.  
       If CheckBox1.CheckState = CheckState.Checked Then  
          ' If checked, do not allow items to be dragged onto the form.  
          Me.AllowDrop = False  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_CheckedChanged(object sender, System.EventArgs e)  
    {  
       // Determine the CheckState of the check box.  
       if (checkBox1.CheckState == CheckState.Checked)   
       {  
          // If checked, do not allow items to be dragged onto the form.  
          this.AllowDrop = false;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // Determine the CheckState of the check box.  
          if (checkBox1->CheckState == CheckState::Checked)   
          {  
             // If checked, do not allow items to be dragged onto the form.  
             this->AllowDrop = false;  
          }  
       }  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.CheckBox>
- [CheckBox 컨트롤 개요](checkbox-control-overview-windows-forms.md)
- [방법: Windows Forms CheckBox 클릭에 응답](how-to-respond-to-windows-forms-checkbox-clicks.md)
- [CheckBox 컨트롤](checkbox-control-windows-forms.md)
