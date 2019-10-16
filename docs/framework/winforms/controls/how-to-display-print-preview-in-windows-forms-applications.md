---
title: '방법: Windows Forms 애플리케이션에서 인쇄 미리 보기 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- print preview [Windows Forms], displaying
- printing [Windows Forms], print preview
- examples [Windows Forms], print preview
ms.assetid: e394134c-0886-4517-bd8d-edc4a3749eb5
ms.openlocfilehash: 8252906de9a574f49617609a4cb08a1e8aa6a992
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929002"
---
# <a name="how-to-display-print-preview-in-windows-forms-applications"></a>방법: Windows Forms 애플리케이션에서 인쇄 미리 보기 표시
<xref:System.Windows.Forms.PrintPreviewDialog> 컨트롤을 사용 하면 사용자가 문서를 인쇄 하기 전에 자주 표시할 수 있습니다.  
  
 이렇게 하려면 <xref:System.Drawing.Printing.PrintDocument> 클래스의 인스턴스를 지정 해야 합니다 .이 문서는 인쇄할 문서입니다. <xref:System.Drawing.Printing.PrintDocument> 구성 요소에서 인쇄 미리 보기를 사용 하는 방법에 [대 한 자세한 내용은 방법: 인쇄 미리 보기](../advanced/how-to-print-in-windows-forms-using-print-preview.md)를 사용 하 여 Windows Forms 인쇄 합니다.  
  
> [!NOTE]
> 런타임에 <xref:System.Windows.Forms.PrintPreviewDialog> 컨트롤을 사용 하려면 컴퓨터에 로컬로 또는 네트워크를 통해 프린터가 설치 되어 있어야 합니다 .이는 <xref:System.Windows.Forms.PrintPreviewDialog> 구성 요소가 인쇄 될 때 문서의 모양을 결정 하는 방법입니다.  
  
 컨트롤 <xref:System.Windows.Forms.PrintPreviewDialog> 은 클래스를 <xref:System.Drawing.Printing.PrinterSettings> 사용 합니다. 또한 컨트롤은 <xref:System.Windows.Forms.PrintPreviewDialog> <xref:System.Windows.Forms.PrintPreviewDialog> 구성 요소가 수행 <xref:System.Drawing.Printing.PageSettings> 하는 것 처럼 클래스를 사용 합니다. <xref:System.Windows.Forms.PrintPreviewDialog> 컨트롤의 <xref:System.Windows.Forms.PrintPreviewControl.Document%2A> 속성에 지정 된 인쇄 문서는 <xref:System.Drawing.Printing.PrinterSettings> 및 <xref:System.Drawing.Printing.PageSettings> 클래스의 인스턴스를 참조 하 고 미리 보기 창에서 문서를 렌더링 하는 데 사용 됩니다.  
  
### <a name="to-view-pages-using-the-printpreviewdialog-control"></a>PrintPreviewDialog 컨트롤을 사용 하 여 페이지를 보려면  
  
- <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 메서드를 사용하여 대화 상자를 표시하고, 사용할 <xref:System.Drawing.Printing.PrintDocument> 를 지정합니다.  
  
     다음 코드 예제에서 <xref:System.Windows.Forms.Button> <xref:System.Windows.Forms.Control.Click> 컨트롤의 이벤트 처리기는 <xref:System.Windows.Forms.PrintPreviewDialog> 컨트롤의 인스턴스를 엽니다. 인쇄 문서는 <xref:System.Windows.Forms.PrintDialog.Document%2A> 속성에 지정 되어 있습니다. 아래 예제에서는 인쇄 문서를 지정 하지 않습니다.  
  
     이 <xref:System.Windows.Forms.Button> 예제에서는 폼에 컨트롤 <xref:System.Drawing.Printing.PrintDocument> , 이라는 `myDocument` <xref:System.Windows.Forms.PrintPreviewDialog> 구성 요소 및 컨트롤이 있어야 합니다.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       ' The print document 'myDocument' used below  
       ' is merely for an example.  
       ' You will have to specify your own print document.  
       PrintPreviewDialog1.Document = myDocument  
       PrintPreviewDialog1.ShowDialog()  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // The print document 'myDocument' used below  
       // is merely for an example.  
       // You will have to specify your own print document.  
       printPreviewDialog1.Document = myDocument;  
       printPreviewDialog1.ShowDialog();  
    }  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // The print document 'myDocument' used below  
          // is merely for an example.  
          // You will have to specify your own print document.  
          printPreviewDialog1->Document = myDocument;  
          printPreviewDialog1->ShowDialog();  
       }  
    ```  
  
     (시각적 C#개체, C++시각적 개체) 폼의 생성자에 다음 코드를 추가 하 여 이벤트 처리기를 등록 합니다.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## <a name="see-also"></a>참고자료

- [PrintDocument 구성 요소](printdocument-component-windows-forms.md)
- [PrintPreviewDialog 컨트롤](printpreviewdialog-control-windows-forms.md)
- [Windows Forms 인쇄 지원](../advanced/windows-forms-print-support.md)
- [Windows Forms](../index.md)
