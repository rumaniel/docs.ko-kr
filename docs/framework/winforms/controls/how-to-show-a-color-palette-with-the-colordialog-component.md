---
title: '방법: ColorDialog 구성 요소를 사용하여 색상표 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- palettes [Windows Forms], showing color
- color dialog box [Windows Forms], showing color palettes
- colors [Windows Forms], allowing users to select
- color palettes [Windows Forms], dialog box
- ColorDialog component [Windows Forms], showing color palettes
- color palettes [Windows Forms], showing in ColorDialog component
- colors [Windows Forms], showing palettes
ms.assetid: ee050f61-dbc8-4436-ba22-51360981ab48
ms.openlocfilehash: ff29df4ecfc90eabe8e3be0e5a6a126858799c16
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66053416"
---
# <a name="how-to-show-a-color-palette-with-the-colordialog-component"></a>방법: ColorDialog 구성 요소를 사용하여 색상표 표시
합니다 [ColorDialog](colordialog-component-windows-forms.md) 색상표를 표시 하 고 사용자가 선택한 색을 포함 하는 속성을 반환 하는 구성 요소입니다.  
  
### <a name="to-choose-a-color-using-the-colordialog-component"></a>ColorDialog 구성 요소를 사용 하 여 색을 선택 하려면  
  
1. 사용 하 여 대화 상자를 표시 합니다 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 메서드.  
  
2. 사용 된 <xref:System.Windows.Forms.DialogResult> 속성 대화 상자를 닫은 방법을 확인 하려면.  
  
3. 사용 하 여 합니다 <xref:System.Windows.Forms.ColorDialog.Color%2A> 의 속성을 <xref:System.Windows.Forms.ColorDialog> 선택한 색을 설정 하려면 구성 요소입니다.  
  
     아래 예제에서는 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기가 열립니다는 <xref:System.Windows.Forms.ColorDialog> 구성 요소입니다. 색을 선택 하 고 사용자가 클릭할 **확인**, <xref:System.Windows.Forms.Button> 컨트롤의 배경 색 선택한 색으로 설정 됩니다. 이 예제에서는 폼에 가정를 <xref:System.Windows.Forms.Button> 컨트롤 및 <xref:System.Windows.Forms.ColorDialog> 구성 요소입니다.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button1.Click  
       If ColorDialog1.ShowDialog() = DialogResult.OK Then  
          Button1.BackColor = ColorDialog1.Color  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(colorDialog1.ShowDialog() == DialogResult.OK)  
       {  
          button1.BackColor = colorDialog1.Color;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,   
          System::EventArgs ^ e)  
       {  
          if(colorDialog1->ShowDialog() == DialogResult::OK)  
          {  
             button1->BackColor = colorDialog1->Color;  
          }  
       }  
    ```  
  
     (Visual C#, Visual C++) 이벤트 처리기를 등록 하려면 폼의 생성자에 다음 코드를 추가 합니다.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->button1->Click +=   
       gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ColorDialog>
- [ColorDialog 구성 요소](colordialog-component-windows-forms.md)
