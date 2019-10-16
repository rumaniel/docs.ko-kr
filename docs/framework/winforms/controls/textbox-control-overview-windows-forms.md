---
title: TextBox 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- TextBox
helpviewer_keywords:
- TextBox control [Windows Forms], about TextBox controls
- text boxes [Windows Forms], adding
ms.assetid: d1a9c7f5-fa53-480a-a75c-158f8649ea2f
ms.openlocfilehash: a91b67df1071c79707bb20a68efb4d5e6f083ae0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61932550"
---
# <a name="textbox-control-overview-windows-forms"></a>TextBox 컨트롤 개요(Windows Forms)
Windows Forms 텍스트 상자에는 사용자 로부터 입력 하거나 텍스트를 표시 하도록 사용 됩니다. <xref:System.Windows.Forms.TextBox> 컨트롤은 일반적으로 편집 가능한 텍스트에 사용 하도 설정할 수 있지만 읽기 전용입니다. 입력란 수 여러 줄을 표시, 텍스트 컨트롤의 크기를 래핑하고 기본 서식을 추가 합니다. <xref:System.Windows.Forms.TextBox> 컨트롤은 컨트롤에 표시 되거나 입력 텍스트에 대 한 단일 형식 스타일을 제공 합니다. 여러 유형의 서식 있는 텍스트를 표시 하려면 사용 된 <xref:System.Windows.Forms.RichTextBox> 제어 합니다. 자세한 내용은 [RichTextBox 컨트롤 개요](richtextbox-control-overview-windows-forms.md)합니다.  
  
## <a name="working-with-the-textbox-control"></a>TextBox 컨트롤 사용  
 컨트롤에서 표시 되는 텍스트에 포함 된 <xref:System.Windows.Forms.TextBox.Text%2A> 속성입니다. 기본적으로 최대 2048 자의 텍스트 상자에 입력할 수 있습니다. 설정한 경우에 <xref:System.Windows.Forms.TextBox.Multiline%2A> 속성을 `true`, 최대 32KB의 텍스트를 입력할 수 있습니다. <xref:System.Windows.Forms.TextBox.Text%2A> 런타임 시 사용자 입력에 따라 또는 코드에서 런타임에 속성 창을 사용 하 여 디자인 타임에 속성을 설정할 수 있습니다. 입력란의 현재 내용을 참조 하 여 런타임 시 검색할 수 있습니다는 <xref:System.Windows.Forms.TextBox.Text%2A> 속성입니다.  
  
 다음 코드 예제는 런타임 시 컨트롤의 텍스트를 설정합니다. `InitializeMyControl` 프로시저는 자동으로 실행 되지 않으면 호출 해야 합니다.  
  
```vb  
Private Sub InitializeMyControl()  
   ' Put some text into the control first.  
   TextBox1.Text = "This is a TextBox control."  
End Sub  
```  
  
```csharp  
private void InitializeMyControl() {  
   // Put some text into the control first.  
   textBox1.Text = "This is a TextBox control.";  
}  
```  
  
```cpp  
private:  
   void InitializeMyControl()  
   {  
      // Put some text into the control first.  
      textBox1->Text = "This is a TextBox control.";  
   }  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TextBox>
- [방법: Windows Forms TextBox 컨트롤의 삽입 지점 제어](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [방법: Windows Forms TextBox 컨트롤을 사용 하 여 암호 텍스트 상자 만들기](how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)
- [방법: 읽기 전용 텍스트 상자 만들기](how-to-create-a-read-only-text-box-windows-forms.md)
- [방법: 문자열에 인용 부호 넣기](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [방법: Windows Forms TextBox 컨트롤에서 텍스트를 선택 합니다.](how-to-select-text-in-the-windows-forms-textbox-control.md)
- [방법: Windows Forms TextBox 컨트롤에서 여러 줄 보기](how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)
- [TextBox 컨트롤](textbox-control-windows-forms.md)
