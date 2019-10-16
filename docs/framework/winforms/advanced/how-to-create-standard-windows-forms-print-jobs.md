---
title: '방법: 표준 Windows Forms 인쇄 작업 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- printing [Windows Forms]
- printing [Windows Forms], creating print jobs
- printing [Visual Basic], in Windows applications
ms.assetid: 03342b90-9cfe-40b2-838b-b479a13c5dea
ms.openlocfilehash: 44673e6b26f088e71813aaac26c4b9a03429597a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69938238"
---
# <a name="how-to-create-standard-windows-forms-print-jobs"></a>방법: 표준 Windows Forms 인쇄 작업 만들기
Windows Forms의 인쇄 기초는 <xref:System.Drawing.Printing.PrintDocument> 구성 요소 이며 <xref:System.Drawing.Printing.PrintDocument.PrintPage> , 더 구체적으로 이벤트입니다. 이벤트를 처리 하는 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 코드를 작성 하 여 인쇄할 항목과 인쇄 방법을 지정할 수 있습니다.  
  
### <a name="to-create-a-print-job"></a>인쇄 작업을 만들려면  
  
1. <xref:System.Drawing.Printing.PrintDocument> 구성 요소를 폼에 추가 합니다.  
  
2. <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트를 처리할 코드를 작성합니다.  
  
     사용자 고유의 인쇄 논리를 코딩 해야 합니다. 또한 인쇄할 재질을 지정 해야 합니다.  
  
     다음 코드 예제에서는 인쇄할 재질의 역할을 하는 빨간색 사각형 모양의 샘플 그래픽이 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트 처리기에 생성 됩니다.  
  
    ```vb  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillRectangle(Brushes.Red, New Rectangle(500, 500, 500, 500))  
    End Sub  
    ```  
  
    ```csharp  
    private void printDocument1_PrintPage(object sender,   
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Red,   
         new Rectangle(500, 500, 500, 500));  
    }  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_PrintPage(System::Object ^ sender,  
          System::Drawing::Printing::PrintPageEventArgs ^ e)  
       {  
          e->Graphics->FillRectangle(Brushes::Red,  
             Rectangle(500, 500, 500, 500));  
       }  
    ```  
  
     (시각적 C# 개체 및 C++시각적 개체) 폼의 생성자에 다음 코드를 추가 하 여 이벤트 처리기를 등록 합니다.  
  
    ```csharp  
    this.printDocument1.PrintPage += new  
       System.Drawing.Printing.PrintPageEventHandler  
       (this.printDocument1_PrintPage);  
    ```  
  
    ```cpp  
    printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    ```  
  
     또한 <xref:System.Drawing.Printing.PrintDocument.BeginPrint> 및<xref:System.Drawing.Printing.PrintDocument.EndPrint> 이벤트에 대 한 코드를 작성할 수 있습니다 .이 경우 인쇄 되는 페이지의 총 수를 나타내는 정수를 포함 하 여 각 페이지가 인쇄 될 때 줄어듭니다.  
  
    > [!NOTE]
    > 폼에 구성 요소 <xref:System.Windows.Forms.PrintDialog> 를 추가 하 여 사용자에 게 명확 하 고 효율적인 UI (사용자 인터페이스)를 제공할 수 있습니다. <xref:System.Windows.Forms.PrintDialog> 구성 요소의 <xref:System.Windows.Forms.PrintDialog.Document%2A> 속성을 설정 하 여 양식에서 작업 중인 인쇄 문서와 관련 된 속성을 설정할 수 있습니다. <xref:System.Windows.Forms.PrintDialog> 구성 요소에 대 한 자세한 내용은 [PrintDialog 구성 요소](../controls/printdialog-component-windows-forms.md)를 참조 하세요.  
  
     프로그래밍 방식으로 인쇄 작업을 만드는 방법을 비롯 하 여 Windows Forms 인쇄 작업의 세부 정보에 대 한 자세한 <xref:System.Drawing.Printing.PrintPageEventArgs>내용은을 참조 하십시오.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Printing.PrintDocument>
- [Windows Forms 인쇄 지원](windows-forms-print-support.md)
