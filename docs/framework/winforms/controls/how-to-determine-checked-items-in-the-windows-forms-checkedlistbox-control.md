---
title: '방법: Windows Forms CheckedListBox 컨트롤에서 선택한 항목 확인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- check boxes [Windows Forms], determining checked state
- CheckedListBox control [Windows Forms], determining checked state
ms.assetid: 178b477d-27c9-489c-8914-44a9623a4d41
ms.openlocfilehash: 10793053934dce0bb83113004a79f1c265f5f267
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010919"
---
# <a name="how-to-determine-checked-items-in-the-windows-forms-checkedlistbox-control"></a>방법: Windows Forms CheckedListBox 컨트롤에서 선택한 항목 확인
Windows Forms에서 데이터를 표시할 때 <xref:System.Windows.Forms.CheckedListBox> 컨트롤을 반복할 수 있습니다 하거나 컬렉션에 저장 합니다 <xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A> 속성 또는 사용 하 여 목록을 단계별로 <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> 선택한 항목을 확인 하는 방법. 합니다 <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> 메서드 항목 인덱스 번호를 인수로 받아서 반환 `true` 또는 `false`합니다. 예상 하는 것을 달리 합니다 <xref:System.Windows.Forms.ListBox.SelectedItems%2A> 및 <xref:System.Windows.Forms.ListBox.SelectedIndices%2A> 결정 하는 항목 강조 표시 되어; 속성에서 선택한 항목을 결정 하지 않습니다.  
  
### <a name="to-determine-checked-items-in-a-checkedlistbox-control"></a>CheckedListBox 컨트롤에서 선택한 항목을 확인 하려면  
  
1. 반복 된 <xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A> 컬렉션, 컬렉션은 0부터 시작 하므로 0부터 시작 합니다. 이 메서드는 전체 목록이 아니라 선택 된 항목의 목록에서 항목 수를 알려 참고 합니다. 아래 코드와 같은 텍스트를 표시 되 목록에서 첫 번째 항목을 선택 하지 않으면 두 번째 항목을 선택 하는 경우 "선택한 항목 1 = MyListItem2"입니다.  
  
    ```vb  
    ' Determine if there are any items checked.  
    If CheckedListBox1.CheckedItems.Count <> 0 Then  
       ' If so, loop through all checked items and print results.  
       Dim x As Integer  
       Dim s As String = ""  
       For x = 0 To CheckedListBox1.CheckedItems.Count - 1  
          s = s & "Checked Item " & (x + 1).ToString & " = " & CheckedListBox1.CheckedItems(x).ToString & ControlChars.CrLf  
       Next x  
       MessageBox.Show(s)  
    End If  
    ```  
  
    ```csharp  
    // Determine if there are any items checked.  
    if(checkedListBox1.CheckedItems.Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       string s = "";  
       for(int x = 0; x < checkedListBox1.CheckedItems.Count ; x++)  
       {  
          s = s + "Checked Item " + (x+1).ToString() + " = " + checkedListBox1.CheckedItems[x].ToString() + "\n";  
       }  
       MessageBox.Show(s);  
    }  
    ```  
  
    ```cpp  
    // Determine if there are any items checked.  
    if(checkedListBox1->CheckedItems->Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       String ^ s = "";  
       for(int x = 0; x < checkedListBox1->CheckedItems->Count; x++)  
       {  
          s = String::Concat(s, "Checked Item ", (x+1).ToString(),  
             " = ", checkedListBox1->CheckedItems[x]->ToString(),  
             "\n");  
       }  
       MessageBox::Show(s);  
    }  
    ```  
  
     - 또는  
  
2. 단계별로 실행 합니다 <xref:System.Windows.Forms.CheckedListBox.Items%2A> 부터 컬렉션 이므로 0부터 시작 하는 컬렉션 및 호출을 <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> 각 항목에 대 한 메서드. 이 메서드를 알려 항목 번호 전체 목록에서 첫 번째 항목 목록 확인 하지 않습니다 있도록 및 두 번째 항목을 체크을 비슷하게 표시 됩니다 "항목 2 = MyListItem2"입니다.  
  
    ```vb  
    Dim i As Integer  
    Dim s As String  
    s = "Checked Items:" & ControlChars.CrLf  
    For i = 0 To (CheckedListBox1.Items.Count - 1)  
       If CheckedListBox1.GetItemChecked(i) = True Then  
          s = s & "Item " & (i + 1).ToString & " = " & CheckedListBox1.Items(i).ToString & ControlChars.CrLf  
       End If  
    Next  
    MessageBox.Show(s)  
    ```  
  
    ```csharp  
    int i;  
    string s;   
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1.Items.Count-1); i++)  
    {  
       if (checkedListBox1.GetItemChecked(i))  
       {  
          s = s + "Item " + (i+1).ToString() + " = " + checkedListBox1.Items[i].ToString() + "\n";  
       }  
    }  
    MessageBox.Show (s);  
    ```  
  
    ```cpp  
    int i;  
    String ^ s;   
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1->Items->Count-1); i++)  
    {  
       if (checkedListBox1->GetItemChecked(i))  
       {  
          s = String::Concat(s, "Item ", (i+1).ToString(), " = ",  
             checkedListBox1->Item[i]->ToString(), "\n");  
       }  
    }  
    MessageBox::Show(s);  
    ```  
  
## <a name="see-also"></a>참고자료

- [옵션 목록 표시에 사용된 Windows Forms 컨트롤](windows-forms-controls-used-to-list-options.md)
