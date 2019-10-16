---
title: '방법: PageSetupDialog 구성 요소를 사용하여 페이지 속성 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- page properties
- page setup
- PageSetupDialog component
ms.assetid: 6dae05bc-c0fd-4357-bb93-841a1631d98f
ms.openlocfilehash: 306e0dbf7fb819d1214d7d5d93d335b5d2db75e6
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66053612"
---
# <a name="how-to-determine-page-properties-using-the-pagesetupdialog-component"></a>방법: PageSetupDialog 구성 요소를 사용하여 페이지 속성 설정
[PageSetupDialog](pagesetupdialog-component-windows-forms.md) 구성 요소는 문서의 사용자에게 레이아웃, 용지 크기 및 기타 페이지 레이아웃 옵션을 표시합니다.  
  
 <xref:System.Drawing.Printing.PrintDocument> 클래스의 인스턴스를 지정해야 합니다(인쇄할 문서). 또한 사용자 컴퓨터에 로컬로 또는 네트워크를 통해 프린터가 설치되어 있어야 합니다. 부분적으로 이것이 <xref:System.Windows.Forms.PageSetupDialog> 구성 요소가 사용자에게 표시되는 페이지 서식 지정 옵션을 결정하는 방법이기 때문입니다.  
  
 <xref:System.Windows.Forms.PageSetupDialog> 구성 요소 작업의 중요한 측면은 <xref:System.Drawing.Printing.PageSettings> 클래스와의 상호 작용 방법입니다. <xref:System.Drawing.Printing.PageSettings> 클래스는 용지 방향, 페이지의 크기, 여백 등 페이지가 인쇄되는 방법을 수정하는 설정을 지정하는 데 사용됩니다. 이러한 각 설정은 <xref:System.Drawing.Printing.PageSettings> 클래스의 속성으로 표시됩니다. <xref:System.Windows.Forms.PageSetupDialog> 클래스는 문서와 연결된(그리고 <xref:System.Drawing.Printing.PageSettings> 속성으로 표시되는) <xref:System.Drawing.Printing.PrintDocument.DefaultPageSettings%2A> 클래스의 지정된 인스턴스에 대해 이러한 속성 값을 수정합니다.  
  
### <a name="to-set-page-properties-using-the-pagesetupdialog-component"></a>PageSetupDialog 구성 요소를 사용하여 페이지 속성을 설정하려면  
  
1. <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 메서드를 사용하여 대화 상자를 표시하고, 사용할 <xref:System.Drawing.Printing.PrintDocument> 를 지정합니다.  
  
     다음 예제에는 <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기가 <xref:System.Windows.Forms.PageSetupDialog> 구성 요소의 인스턴스를 엽니다. <xref:System.Windows.Forms.PageSetupDialog.Document%2A> 속성에서 기존 문서가 지정되고, 해당 <xref:System.Drawing.Printing.PageSettings.Color%2A?displayProperty=nameWithType> 속성은 `false`로 설정됩니다.  
  
     이 예제에서는 폼에 가정를 <xref:System.Windows.Forms.Button> 컨트롤을 <xref:System.Drawing.Printing.PrintDocument> 라는 구성 요소 `myDocument`, 및 <xref:System.Windows.Forms.PageSetupDialog> 구성 요소.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button1.Click  
       ' The print document 'myDocument' used below  
       ' is merely for an example.  
       'You will have to specify your own print document.  
       PageSetupDialog1.Document = myDocument  
       ' Sets the print document's color setting to false,  
       ' so that the page will not be printed in color.  
       PageSetupDialog1.Document.DefaultPageSettings.Color = False  
       PageSetupDialog1.ShowDialog()  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // The print document 'myDocument' used below  
       // is merely for an example.  
       // You will have to specify your own print document.  
       pageSetupDialog1.Document = myDocument;  
       // Sets the print document's color setting to false,  
       // so that the page will not be printed in color.  
       pageSetupDialog1.Document.DefaultPageSettings.Color = false;  
       pageSetupDialog1.ShowDialog();  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void button1_Click(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          // The print document 'myDocument' used below  
          // is merely for an example.  
          // You will have to specify your own print document.  
          pageSetupDialog1->Document = myDocument;  
          // Sets the print document's color setting to false,  
          // so that the page will not be printed in color.  
          pageSetupDialog1->Document->DefaultPageSettings->Color = false;  
          pageSetupDialog1->ShowDialog();  
       }  
    ```  
  
     (Visual C# 및 시각적 C++) 이벤트 처리기를 등록 하려면 폼의 생성자에 다음 코드를 추가 합니다.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew   
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.PageSetupDialog>
- [방법: 표준 Windows Forms 인쇄 작업 만들기](../advanced/how-to-create-standard-windows-forms-print-jobs.md)
- [PageSetupDialog 구성 요소](pagesetupdialog-component-windows-forms.md)
