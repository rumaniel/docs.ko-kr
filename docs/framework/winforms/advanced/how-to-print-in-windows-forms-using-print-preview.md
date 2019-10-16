---
title: '방법: Windows Forms에서 인쇄 미리 보기를 사용하여 인쇄'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- printing [Windows Forms], using print preview
- printing [Windows Forms], with print preview
- print preview
ms.assetid: 4a16f7e2-ae10-4485-b0ae-3d558334d0fe
ms.openlocfilehash: 07137d03dd9a20d8eab564757618e48e25b45353
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931762"
---
# <a name="how-to-print-in-windows-forms-using-print-preview"></a>방법: Windows Forms에서 인쇄 미리 보기를 사용하여 인쇄
Windows Forms 프로그래밍에서는 인쇄 서비스 외에 인쇄 미리 보기를 제공하는 것이 일반적입니다. 인쇄 미리 보기 서비스를 애플리케이션에 추가하는 편리한 방법은 파일 인쇄에 대한 <xref:System.Windows.Forms.PrintPreviewDialog> 이벤트 처리 논리와 함께 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 컨트롤을 사용하는 것입니다.  
  
### <a name="to-preview-a-text-document-with-a-printpreviewdialog-control"></a>PrintPreviewDialog 컨트롤을 사용하여 텍스트 문서를 미리 보려면  
  
1. <xref:System.Windows.Forms.PrintPreviewDialog>, <xref:System.Drawing.Printing.PrintDocument>및 두 개의 문자열을 폼에 추가합니다.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#1)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#1)]  
  
2. <xref:System.Drawing.Printing.PrintDocument.DocumentName%2A> 속성을 인쇄할 문서로 설정하고 문서를 연 다음 이전에 추가한 문자열까지 문서 내용을 읽습니다.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#2)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#2)]  
  
3. 문서를 인쇄할 때와 마찬가지로, <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트 처리기에서 <xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A> 클래스의 <xref:System.Drawing.Printing.PrintPageEventArgs> 속성과 파일 내용을 사용하여 페이지당 줄 수를 계산하고 문서 내용을 렌더링합니다. 각 페이지가 그려진 후 마지막 페이지인지 확인하고 <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A> 의 <xref:System.Drawing.Printing.PrintPageEventArgs> 속성을 적절하게 설정합니다. <xref:System.Drawing.Printing.PrintDocument.PrintPage> 가 <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A> 가 될 때까지 `false`이벤트가 발생합니다. 문서 렌더링이 완료되면 렌더링할 문자열을 다시 설정합니다. 또한 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트가 해당 이벤트 처리 메서드에 연결되어 있는지 확인합니다.  
  
    > [!NOTE]
    > 애플리케이션에서 인쇄를 구현한 경우 2단계와 3단계를 이미 완료했을 수도 있습니다.  
  
     다음 코드 예제에서 이벤트 처리기는 "testPage.txt" 파일을 폼에 사용된 것과 동일한 글꼴로 인쇄하는 데 사용됩니다.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#3)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#3)]  
  
4. <xref:System.Windows.Forms.PrintPreviewDialog.Document%2A> 컨트롤의 <xref:System.Windows.Forms.PrintPreviewDialog> 속성을 폼의 <xref:System.Drawing.Printing.PrintDocument> 구성 요소로 설정합니다.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#5)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#5)]  
  
5. <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 컨트롤에 대해 <xref:System.Windows.Forms.PrintPreviewDialog> 메서드를 호출합니다. 일반적으로 단추의 <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 이벤트 처리 메서드에서 <xref:System.Windows.Forms.Control.Click> 를 호출합니다. <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> 를 호출하면 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트가 발생하고 출력이 <xref:System.Windows.Forms.PrintPreviewDialog> 컨트롤에 렌더링됩니다. 사용자가 대화 상자에서 인쇄 아이콘을 클릭하면 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트가 다시 발생하여 미리 보기 대화 상자 대신 프린터로 출력을 보냅니다. 이 때문에 3단계에서 렌더링 프로세스가 끝날 때 문자열을 다시 설정하는 것입니다.  
  
     다음 코드 예제에서는 폼의 단추에 대한 <xref:System.Windows.Forms.Control.Click> 이벤트 처리 메서드를 보여 줍니다. 이 이벤트 처리 메서드는 문서를 읽고 인쇄 미리 보기 대화 상자를 표시하는 메서드를 호출합니다.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#4)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#4)]  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Drawing.Printing.PrintPreviewExample#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#0)]
 [!code-vb[System.Drawing.Printing.PrintPreviewExample#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#0)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Windows.Forms, System.Drawing 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- [방법: Windows Forms에서 다중 페이지 텍스트 파일 인쇄](how-to-print-a-multi-page-text-file-in-windows-forms.md)
- [Windows Forms 인쇄 지원](windows-forms-print-support.md)
- [Windows Forms의 인쇄 추가 보안](../more-secure-printing-in-windows-forms.md)
