---
title: '방법: Windows Forms RichTextBox 컨트롤에서 서식 특성의 변경 시기 확인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], text boxes
- RichTextBox control [Windows Forms], determining font changes
- text boxes [Windows Forms], determining font changes
- SelChange event
ms.assetid: bdfed015-f77a-41e5-b38f-f8629b2fa166
ms.openlocfilehash: a90affde9de36f1c83d5b7c21b40580cdf53402e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61972291"
---
# <a name="how-to-determine-when-formatting-attributes-change-in-the-windows-forms-richtextbox-control"></a>방법: Windows Forms RichTextBox 컨트롤에서 서식 특성의 변경 시기 확인
Windows Forms의 일반적인 용도 <xref:System.Windows.Forms.RichTextBox> 글꼴 옵션 등 단락 스타일 특성을 사용 하 여 텍스트 서식을 제어 하는 합니다. 응용 프로그램 대부분의 워드프로세싱 응용 프로그램과 마찬가지로 도구 모음을 표시 하기 위해 서식 지정 하는 텍스트의 모든 변경 내용을 추적할 수 해야 합니다.  
  
### <a name="to-respond-to-changes-in-formatting-attributes"></a>서식 특성의 변경 내용에 응답  
  
1. 코드를 작성 합니다 <xref:System.Windows.Forms.RichTextBox.SelectionChanged> 특성의 값에 따라 적절 한 작업을 수행 하려면 이벤트 처리기입니다. 다음 예제에서는 값에 따라 도구 모음 단추의 모양을 변경 합니다 <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A> 속성입니다. 도구 모음 단추 컨트롤에서 삽입 지점을 이동 하는 경우에 업데이트 됩니다.  
  
     아래 예제에서는 가정 된 폼을 <xref:System.Windows.Forms.RichTextBox> 컨트롤 및 <xref:System.Windows.Forms.ToolBar> 도구 모음 단추를 포함 하는 컨트롤입니다. 도구 모음 및 도구 모음 단추에 대 한 자세한 내용은 참조 하세요. [방법: ToolBar 컨트롤에 단추 추가](how-to-add-buttons-to-a-toolbar-control.md)합니다.  
  
    ```vb  
    ' The following code assumes the existence of a toolbar control  
    ' with at least one toolbar button.  
    Private Sub RichTextBox1_SelectionChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles RichTextBox1.SelectionChanged  
       If RichTextBox1.SelectionBullet = True Then  
          ' Bullet button on toolbar should appear pressed  
          ToolBarButton1.Pushed = True  
       Else  
           ' Bullet button on toolbar should appear unpressed  
           ToolBarButton1.Pushed = False  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    // The following code assumes the existence of a toolbar control  
    // with at least one toolbar button.  
    private void richTextBox1_SelectionChanged(object sender,  
    System.EventArgs e)  
    {  
       if (richTextBox1.SelectionBullet == true)   
       {  
          // Bullet button on toolbar should appear pressed  
          toolBarButton1.Pushed = true;  
       }  
       else   
       {  
          // Bullet button on toolbar should appear unpressed  
          toolBarButton1.Pushed = false;  
       }  
    }  
    ```  
  
    ```cpp  
    // The following code assumes the existence of a toolbar control  
    // with at least one toolbar button.  
    private:  
       System::Void richTextBox1_SelectionChanged(  
          System::Object ^  sender, System::EventArgs ^  e)  
       {  
          if (richTextBox1->SelectionBullet == true)  
          {  
             // Bullet button on toolbar should appear pressed  
             toolBarButton1->Pushed = true;  
          }  
          else  
          {  
             // Bullet button on toolbar should appear unpressed  
             toolBarButton1->Pushed = false;  
          }  
       }  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.RichTextBox.SelectionChanged>
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox 컨트롤](richtextbox-control-windows-forms.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
