---
title: '방법: 런타임에 PrintDialog에서 사용자 입력 캡처'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- print options [Windows Forms], changing at run time
- printing [Windows Forms], options
- print options
- run time [Windows Forms], changing print options
ms.assetid: 438501d8-9a70-4fb3-aae6-e46579aba0c6
ms.openlocfilehash: 2aaf988f362baf9cd80eb16e4a08f7f65a5077bb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61937802"
---
# <a name="how-to-capture-user-input-from-a-printdialog-at-run-time"></a>방법: 런타임에 PrintDialog에서 사용자 입력 캡처
디자인 타임에 인쇄 관련 옵션을 설정할 수 있지만 가능성이 가장 높은 사용자의 선택으로 인해 런타임에 이러한 옵션을 변경 하려는 경우가 있습니다. 사용 하 여 문서를 인쇄 하는 것에 대 한 사용자 입력을 캡처할 수 있습니다 합니다 <xref:System.Windows.Forms.PrintDialog> 하며 <xref:System.Drawing.Printing.PrintDocument> 구성 요소입니다.  
  
### <a name="to-change-print-options-programmatically"></a>인쇄 옵션을 프로그래밍 방식으로 변경 하려면  
  
1. 추가 된 <xref:System.Windows.Forms.PrintDialog> 및 <xref:System.Drawing.Printing.PrintDocument> 폼에 구성 요소입니다.  
  
2. 설정 합니다 <xref:System.Windows.Forms.PrintDialog.Document%2A> 의 속성을 <xref:System.Windows.Forms.PrintDialog> 에 <xref:System.Drawing.Printing.PrintDocument> 폼에 추가 합니다.  
  
    ```vb  
    PrintDialog1.Document = PrintDocument1  
    ```  
  
    ```csharp  
    printDialog1.Document = PrintDocument1;  
    ```  
  
    ```cpp  
    printDialog1->Document = PrintDocument1;  
    ```  
  
3. 표시 된 <xref:System.Windows.Forms.PrintDialog> 를 사용 하 여 구성 요소는 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 메서드.  
  
    ```vb  
    PrintDialog1.ShowDialog()  
    ```  
  
    ```csharp  
    printDialog1.ShowDialog();  
    ```  
  
    ```cpp  
    printDialog1->ShowDialog();  
    ```  
  
4. 사용자의 인쇄 선택 대화 상자에서 복사할 수는 <xref:System.Drawing.Printing.PrinterSettings> 의 속성을 <xref:System.Drawing.Printing.PrintDocument> 구성 요소입니다.  
  
## <a name="see-also"></a>참고자료

- [방법: Windows Forms에서 다중 페이지 텍스트 파일 인쇄](how-to-print-a-multi-page-text-file-in-windows-forms.md)
- [Windows Forms 인쇄 지원](windows-forms-print-support.md)
