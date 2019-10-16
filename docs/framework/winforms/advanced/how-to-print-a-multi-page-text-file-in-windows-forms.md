---
title: '방법: Windows Forms에서 다중 페이지 텍스트 파일 인쇄'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- printing [Windows Forms], printing multiple pages
- text [Windows Forms], printing Windows Forms
- Windows Forms, printing text
- printing [Windows Forms], text
ms.assetid: 362427f8-03d4-4826-b49f-60ab066ad322
ms.openlocfilehash: bd858279a4d8a3509a91bcd1c62fb1f61d6d2bb9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931783"
---
# <a name="how-to-print-a-multi-page-text-file-in-windows-forms"></a>방법: Windows Forms에서 다중 페이지 텍스트 파일 인쇄
Windows 기반 애플리케이션에서 텍스트를 인쇄하는 것은 매우 일반적입니다. <xref:System.Drawing.Graphics> 클래스는 화면이나 프린터와 같은 장치에 개체(그래픽 또는 텍스트)를 그리기 위한 메서드를 제공합니다.  
  
> [!NOTE]
> <xref:System.Windows.Forms.TextRenderer>의 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 메서드는 인쇄에 지원되지 않습니다. 인쇄용 텍스트를 그리려면 다음 코드 예제와 같이 항상 <xref:System.Drawing.Graphics>의 <xref:System.Drawing.Graphics.DrawString%2A> 메서드를 사용해야 합니다.  
  
### <a name="to-print-text"></a>텍스트를 인쇄하려면  
  
1. <xref:System.Drawing.Printing.PrintDocument> 구성 요소와 문자열을 폼에 추가합니다.  
  
     [!code-csharp[System.Drawing.Printing.PrintExamples#8](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/CS/Form1.cs#8)]
     [!code-vb[System.Drawing.Printing.PrintExamples#8](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/VB/Form1.vb#8)]  
  
2. 문서를 인쇄하는 경우 <xref:System.Drawing.Printing.PrintDocument.DocumentName%2A> 속성을 인쇄할 문서로 설정하고 문서를 연 다음 이전에 추가한 문자열까지 문서 내용을 읽습니다.  
  
     [!code-csharp[System.Drawing.Printing.PrintExamples#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/CS/Form1.cs#1)]
     [!code-vb[System.Drawing.Printing.PrintExamples#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/VB/Form1.vb#1)]  
  
3. <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트 처리기에서 <xref:System.Drawing.Printing.PrintPageEventArgs> 클래스의 <xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A> 속성과 문서 내용을 사용하여 줄 길이와 페이지당 줄 수를 계산합니다. 각 페이지가 그려진 후 마지막 페이지인지 확인하고 <xref:System.Drawing.Printing.PrintPageEventArgs>의 <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A> 속성을 적절하게 설정합니다. <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A>가 `false`가 될 때까지 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트가 발생합니다. 또한 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트가 해당 이벤트 처리 메서드에 연결되어 있는지 확인합니다.  
  
     다음 코드 예제에서 이벤트 처리기는 "testPage.txt" 파일의 내용을 폼에 사용된 것과 동일한 글꼴로 인쇄하는 데 사용됩니다.  
  
     [!code-csharp[System.Drawing.Printing.PrintExamples#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/CS/Form1.cs#2)]
     [!code-vb[System.Drawing.Printing.PrintExamples#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/VB/Form1.vb#2)]  
  
4. <xref:System.Drawing.Printing.PrintDocument.Print%2A> 메서드를 호출하여 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트를 발생시킵니다.  
  
     [!code-csharp[System.Drawing.Printing.PrintExamples#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/CS/Form1.cs#5)]
     [!code-vb[System.Drawing.Printing.PrintExamples#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/VB/Form1.vb#5)]  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Drawing.Printing.PrintExamples#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/CS/Form1.cs#0)]
 [!code-vb[System.Drawing.Printing.PrintExamples#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintExamples/VB/Form1.vb#0)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- C:\\ 드라이브의 루트에 있는, 인쇄할 텍스트를 포함하는 testPage.txt라는 텍스트 파일 다른 파일을 인쇄하려면 코드를 편집합니다.  
  
- System, System.Windows.Forms, System.Drawing 어셈블리에 대한 참조  
  
- Visual Basic 또는 시각적 개체 C#에 대 한 명령줄에서이 예제를 빌드하는 방법에 대 한 자세한 내용은 [명령줄에서 빌드](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md) 또는 [csc.exe를 사용 하 여 명령줄 빌드](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)를 참조 하세요. 코드를 새 프로젝트에 붙여넣어 Visual Studio에서이 예제를 빌드할 수도 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Graphics>
- <xref:System.Drawing.Brush>
- [Windows Forms 인쇄 지원](windows-forms-print-support.md)
