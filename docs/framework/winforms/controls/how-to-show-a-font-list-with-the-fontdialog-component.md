---
title: '방법: FontDialog 구성 요소를 사용하여 글꼴 목록 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- fonts [Windows Forms], showing list
- FontDialog component [Windows Forms]
- fonts [Windows Forms], attributes
- Font property [Windows Forms], setting with FontDialog component
- Font dialog box [Windows Forms], displaying
- fonts [Windows Forms], selecting
ms.assetid: 35692c1b-0937-4b7a-9207-1ae6bdc244a0
ms.openlocfilehash: 05e9b5e1280d0318354b0d47f4d78f7ec1c5f4e7
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66053443"
---
# <a name="how-to-show-a-font-list-with-the-fontdialog-component"></a>방법: FontDialog 구성 요소를 사용하여 글꼴 목록 표시
합니다 [FontDialog](fontdialog-component-windows-forms.md) 구성 요소 글꼴을 선택할 수 있을 뿐만 아니라 해당 가중치 및 크기와 같은 표시 요소를 변경할 수 있습니다.  
  
 대화 상자에서 선택한 글꼴에 반환 되는 <xref:System.Windows.Forms.FontDialog.Font%2A> 속성입니다. 따라서 사용자가 선택한 글꼴의 활용 속성 읽기 하기만 됩니다.  
  
### <a name="to-select-font-properties-using-the-fontdialog-component"></a>FontDialog 구성 요소를 사용 하 여 글꼴 속성을 선택 하려면  
  
1. 사용 하 여 대화 상자를 표시 합니다 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 메서드.  
  
2. 사용 된 <xref:System.Windows.Forms.DialogResult> 속성 대화 상자를 닫은 방법을 확인 하려면.  
  
3. 사용 된 <xref:System.Windows.Forms.FontDialog.Font%2A> 원하는 글꼴을 설정 하는 속성입니다.  
  
     아래 예제에서는 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기가 열립니다는 <xref:System.Windows.Forms.FontDialog> 구성 요소입니다. 경우 글꼴을 선택 하 고 사용자가 **확인**, <xref:System.Windows.Forms.FontDialog.Font%2A> 의 속성을 <xref:System.Windows.Forms.TextBox> 선택한 글꼴 폼에는 컨트롤 설정 됩니다. 이 예제에서는 폼에 가정를 <xref:System.Windows.Forms.Button> 컨트롤을 <xref:System.Windows.Forms.TextBox> 컨트롤 및 <xref:System.Windows.Forms.FontDialog> 구성 요소입니다.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       If FontDialog1.ShowDialog() = DialogResult.OK Then  
          TextBox1.Font = FontDialog1.Font  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(fontDialog1.ShowDialog() == DialogResult.OK)  
       {  
          textBox1.Font = fontDialog1.Font;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if(fontDialog1->ShowDialog() == DialogResult::OK)  
          {  
             textBox1->Font = fontDialog1->Font;  
          }  
       }  
    ```  
  
     (Visual C# 및 시각적 C++) 이벤트 처리기를 등록 하려면 폼의 생성자에 다음 코드를 추가 합니다.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.FontDialog>
- [FontDialog 구성 요소](fontdialog-component-windows-forms.md)
