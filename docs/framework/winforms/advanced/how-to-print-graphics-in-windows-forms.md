---
title: '방법: Windows Forms에서 그래픽 인쇄'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- graphics [Windows Forms], printing
- printing [Windows Forms], graphics
ms.assetid: 32b891e6-52ff-4fea-a9ff-2ce5db20a4c6
ms.openlocfilehash: 347c7064c199e953b496c9505f08c9e12c1ae670
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66052808"
---
# <a name="how-to-print-graphics-in-windows-forms"></a>방법: Windows Forms에서 그래픽 인쇄
대부분의 경우 Windows 기반 응용 프로그램의 그래픽 인쇄 하려고 합니다. <xref:System.Drawing.Graphics> 클래스는 화면이 나 프린터와 같은 장치에 개체를 그리기 위한 메서드를 제공 합니다.  
  
### <a name="to-print-graphics"></a>그래픽을 인쇄 하려면  
  
1. 추가 된 <xref:System.Drawing.Printing.PrintDocument> 폼에 구성 요소입니다.  
  
2. 에 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트 처리기를 사용 하 여는 <xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A> 의 속성은 <xref:System.Drawing.Printing.PrintPageEventArgs> 프린터에 인쇄 하는 그래픽의 종류에 지시 하는 클래스입니다.  
  
     다음 코드 예제는 경계 사각형 내에서 파란색 타원을 만드는 데 사용 하는 이벤트 처리기를 보여줍니다. 다음 위치와 크기를 사각형에: 100부터 150 250의 너비와 높이 250.  
  
    ```vb  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillEllipse(Brushes.Blue, New Rectangle(100, 150, 250, 250))  
    End Sub  
    ```  
  
    ```csharp  
    private void printDocument1_PrintPage(object sender,   
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Blue,   
         new Rectangle(100, 150, 250, 250));  
    }  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_PrintPage(System::Object ^ sender,  
          System::Drawing::Printing::PrintPageEventArgs ^ e)  
       {  
          e->Graphics->FillRectangle(Brushes::Blue,  
             Rectangle(100, 150, 250, 250));  
       }  
    ```  
  
     (Visual C# 및 시각적 C++) 이벤트 처리기를 등록 하려면 폼의 생성자에 다음 코드를 추가 합니다.  
  
    ```csharp  
    this.printDocument1.PrintPage += new  
       System.Drawing.Printing.PrintPageEventHandler  
       (this.printDocument1_PrintPage);  
    ```  
  
    ```cpp  
    this->printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Graphics>
- <xref:System.Drawing.Brush>
- [Windows Forms 인쇄 지원](windows-forms-print-support.md)
