---
title: '방법: 활성 MDI 자식으로 데이터 보내기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- child forms
- MDI [Windows Forms], sending data to forms
- Clipboard [Windows Forms], pasting
- Clipboard [Windows Forms], getting data from
ms.assetid: 1047d2fe-1235-46db-aad9-563aea1d743b
ms.openlocfilehash: 0a7a2475891488d1fdd60f0db4a483c144a73f0d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69947842"
---
# <a name="how-to-send-data-to-the-active-mdi-child"></a>방법: 활성 MDI 자식으로 데이터 보내기
[Mdi (다중 문서 인터페이스) 응용 프로그램](multiple-document-interface-mdi-applications.md)의 컨텍스트 내에서 사용자가 클립보드의 데이터를 mdi 응용 프로그램으로 붙여넣을 때 처럼 활성 자식 창에 데이터를 보내야 하는 경우가 종종 있습니다.  
  
> [!NOTE]
> 포커스가 있는 자식 창을 확인 하 고 해당 콘텐츠를 클립보드로 보내는 방법에 대 한 자세한 내용은 [활성 MDI 자식 확인](how-to-determine-the-active-mdi-child.md)을 참조 하세요.  
  
### <a name="to-send-data-to-the-active-mdi-child-window-from-the-clipboard"></a>클립보드의 활성 MDI 자식 창에 데이터를 보내려면  
  
1. 메서드 내에서 클립보드의 텍스트를 활성 자식 폼의 활성 컨트롤로 복사 합니다.  
  
    > [!NOTE]
    > 이 예제에서는 컨트롤을`Form1` <xref:System.Windows.Forms.RichTextBox> 포함 하는 mdi 자식 창이 하나 이상 있는 mdi 부모 폼 ()이 있다고 가정 합니다. 자세한 내용은 [MDI 부모 폼 만들기](how-to-create-mdi-parent-forms.md)를 참조 하세요.  
  
    ```vb  
    Public Sub mniPaste_Click(ByVal sender As Object, _  
       ByVal e As System.EventArgs) Handles mniPaste.Click  
  
       ' Determine the active child form.  
       Dim activeChild As Form = Me.ParentForm.ActiveMDIChild  
  
       ' If there is an active child form, find the active control, which  
       ' in this example should be a RichTextBox.  
       If (Not activeChild Is Nothing) Then  
          Try  
             Dim theBox As RichTextBox = Ctype(activeChild.ActiveControl, RichTextBox)  
             If (Not theBox Is Nothing) Then  
                ' Create a new instance of the DataObject interface.  
                Dim data As IDataObject = Clipboard.GetDataObject()  
                ' If the data is text, then set the text of the   
                ' RichTextBox to the text in the clipboard.  
                If (data.GetDataPresent(DataFormats.Text)) Then  
                   theBox.SelectedText = data.GetData(DataFormats.Text).ToString()  
                End If  
             End If  
          Catch  
             MessageBox.Show("You need to select a RichTextBox.")  
          End Try  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    protected void mniPaste_Click (object sender, System.EventArgs e)  
    {  
      // Determine the active child form.  
       Form activeChild = this.ParentForm.ActiveMdiChild;  
  
       // If there is an active child form, find the active control, which  
       // in this example should be a RichTextBox.  
       if (activeChild != null)  
       {  
          try   
          {  
             RichTextBox theBox = (RichTextBox)activeChild.ActiveControl;  
             if (theBox != null)  
             {  
                // Create a new instance of the DataObject interface.  
                IDataObject data = Clipboard.GetDataObject();  
                // If the data is text, then set the text of the   
                // RichTextBox to the text in the clipboard.  
                if (data.GetDataPresent(DataFormats.Text))  
                {  
                   theBox.SelectedText = data.GetData(DataFormats.Text).ToString();                 
                }  
             }  
          }  
          catch   
          {  
             MessageBox.Show("You need to select a RichTextBox.");  
          }  
       }  
    }  
    ```  
  
## <a name="see-also"></a>참고자료

- [MDI(다중 문서 인터페이스) 응용 프로그램](multiple-document-interface-mdi-applications.md)
- [방법: MDI 부모 폼 만들기](how-to-create-mdi-parent-forms.md)
- [방법: MDI 자식 폼 만들기](how-to-create-mdi-child-forms.md)
- [방법: 활성 MDI 자식 확인](how-to-determine-the-active-mdi-child.md)
- [방법: MDI 자식 폼 정렬](how-to-arrange-mdi-child-forms.md)
