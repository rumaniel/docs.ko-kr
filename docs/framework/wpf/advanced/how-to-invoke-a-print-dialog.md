---
title: '방법: 인쇄 대화 상자 호출'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- invoking print dialogs [WPF]
- print dialogs [WPF], invoking
ms.assetid: e3a2c84c-74fe-45a4-8501-5813f9dbfed2
ms.openlocfilehash: 4bad8158925fea8af529f70f92aad74e2a6bbec0
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70254107"
---
# <a name="how-to-invoke-a-print-dialog"></a>방법: 인쇄 대화 상자 호출
응용 프로그램에서 인쇄 하는 기능을 제공 하기 위해 단순히 개체를 <xref:System.Windows.Controls.PrintDialog> 만들고 열 수 있습니다.  
  
## <a name="example"></a>예제  
 컨트롤 <xref:System.Windows.Controls.PrintDialog> 은, 구성 및 XPS 작업 제출을 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]위한 단일 진입점을 제공 합니다. 컨트롤은 사용 하기 쉬우며 태그 또는 코드를 사용 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 하 여 인스턴스화할 수 있습니다. 다음 예제에서는 코드에서 컨트롤을 인스턴스화하고 여는 방법과 인쇄 하는 방법을 보여 줍니다. 또한 대화 상자에서 사용자에 게 특정 페이지 범위를 설정 하는 옵션을 제공 하도록 하는 방법을 보여 줍니다. 예제 코드는 C: 드라이브의 루트에 FixedDocumentSequence 파일이 있다고 가정 합니다.  
  
 [!code-csharp[printdialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintDialog/CSharp/Window1.xaml.cs#1)]
 [!code-vb[printdialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintDialog/visualbasic/window1.xaml.vb#1)]  
  
 대화 상자가 열리면 사용자는 컴퓨터에 설치 된 프린터에서 선택할 수 있습니다. 또한 인쇄 대신 XPS (XML Paper Specification) 파일을 만들 수 있도록 [MICROSOFT Xps Document Writer](https://go.microsoft.com/fwlink/?LinkId=147319) 를 선택 하는 옵션도 있습니다.  
  
> [!NOTE]
> 이 <xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType> 항목에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]설명 하는의 컨트롤은 Windows Forms <xref:System.Windows.Forms.PrintDialog?displayProperty=nameWithType> 구성 요소와 혼동 해서는 안 됩니다.  
  
 엄격히 말해, 사용할 수 있습니다는 <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> 적이 대화 상자를 열지 않고 메서드. 이런 의미에서 컨트롤이 보이지 않는 인쇄 구성 요소로 사용할 수 있습니다. 하지만 성능상의 이유로 사용 하 여 더 나은 것은 <xref:System.Printing.PrintQueue.AddJob%2A> 메서드 또는 다양 한 <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> 및 <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> 의 메서드는 <xref:System.Windows.Xps.XpsDocumentWriter>합니다. 이에 대 한 자세한 내용은 [프로그래밍 방식으로 XPS 파일 인쇄](how-to-programmatically-print-xps-files.md) 및를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.PrintDialog>
- [WPF의 문서](documents-in-wpf.md)
- [인쇄 개요](printing-overview.md)
- [Microsoft XPS Document Writer](https://go.microsoft.com/fwlink/?LinkId=147319)
