---
title: Windows Forms 인쇄 지원
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, printing
- printing [Windows Forms]
- forms [Windows Forms], printing (using designer)
- printing [Windows Forms], Windows Forms, support
- printing [Windows Forms], print support
ms.assetid: a4a2960c-eb70-48e2-b641-cfb222704e46
ms.openlocfilehash: 8e008f2cb4b2f32cdba676e68d9fd790530e2b06
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62011855"
---
# <a name="windows-forms-print-support"></a>Windows Forms 인쇄 지원
Windows Forms의 인쇄를 사용 하는 주로 구성 합니다 [PrintDocument 구성 요소](../controls/printdocument-component-windows-forms.md) 를 인쇄 하려면 사용자를 사용 하도록 설정 하려면 구성 요소 및 [PrintPreviewDialog 컨트롤](../controls/printpreviewdialog-control-windows-forms.md) 컨트롤 [PrintDialog 구성 요소](../controls/printdialog-component-windows-forms.md) 하 고 [PageSetupDialog 구성 요소](../controls/pagesetupdialog-component-windows-forms.md) 구성 요소는 Windows 운영 체제에 익숙한 사용자에 게 친숙 한 그래픽 인터페이스를 제공 합니다.  
  
 새 인스턴스를 만들고 일반적으로 <xref:System.Drawing.Printing.PrintDocument> 구성 요소를 사용 하 여 인쇄 대상을 설명 하는 속성을 설정 합니다 <xref:System.Drawing.Printing.PrinterSettings> 및 <xref:System.Drawing.Printing.PageSettings> 클래스 및 호출을 <xref:System.Drawing.Printing.PrintDocument.Print%2A> 실제 문서를 인쇄 하는 방법입니다.  
  
 Windows 기반 응용 프로그램에서 인쇄 하는 동안는 <xref:System.Drawing.Printing.PrintDocument> 구성 요소는 알림을 사용자에 게 인쇄 발생 함을 팩트에 인쇄 작업을 취소할 중단 인쇄 대화 상자를 표시 됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: 표준 Windows Forms 인쇄 작업 만들기](how-to-create-standard-windows-forms-print-jobs.md)  
 사용 하는 방법에 설명 합니다 <xref:System.Drawing.Printing.PrintDocument> 구성 요소를 Windows Form에서 인쇄 합니다.  
  
 [방법: 런타임에 PrintDialog에서 사용자 입력 캡처](how-to-capture-user-input-from-a-printdialog-at-run-time.md)  
 프로그래밍 방식으로 사용 하 여 선택한 인쇄 옵션을 수정 하는 방법에 설명 합니다 <xref:System.Windows.Forms.PrintDialog> 구성 요소입니다.  
  
 [방법: Windows Forms에서 사용자의 컴퓨터에 연결 된 프린터를 선택 합니다.](how-to-choose-the-printers-attached-to-user-computer-in-windows-forms.md)  
 프린터를 사용 하 여 인쇄할 변경에 대해 설명 합니다 <xref:System.Windows.Forms.PrintDialog> 런타임에 구성 요소입니다.  
  
 [방법: Windows Forms의 그래픽 인쇄](how-to-print-graphics-in-windows-forms.md)  
 프린터에 보내는 그래픽을 설명합니다.  
  
 [방법: Windows Forms에서 다중 페이지 텍스트 파일 인쇄](how-to-print-a-multi-page-text-file-in-windows-forms.md)  
 프린터에 보내는 텍스트를 설명합니다.  
  
 [방법: 전체 Windows Forms 인쇄 작업](how-to-complete-windows-forms-print-jobs.md)  
 인쇄 작업을 완료 하는 사용자를 경고 하는 방법에 설명 합니다.  
  
 [방법: Windows Form 인쇄](how-to-print-a-windows-form.md)  
 현재 폼의 복사본을 인쇄 하는 방법을 보여 줍니다.  
  
 [방법: 인쇄 미리 보기를 사용 하 여 Windows Forms에서 인쇄](how-to-print-in-windows-forms-using-print-preview.md)  
 사용 하는 방법을 보여 줍니다는 <xref:System.Windows.Forms.PrintPreviewDialog> 문서를 인쇄 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [PrintDocument 구성 요소](../controls/printdocument-component-windows-forms.md)  
 사용법을 설명 합니다 <xref:System.Drawing.Printing.PrintDocument> 구성 요소입니다.  
  
 [PrintDialog 구성 요소](../controls/printdialog-component-windows-forms.md)  
 사용법을 설명 합니다 <xref:System.Windows.Forms.PrintDialog> 구성 요소입니다.  
  
 [PrintPreviewDialog 컨트롤](../controls/printpreviewdialog-control-windows-forms.md)  
 사용법을 설명 합니다 <xref:System.Windows.Forms.PrintPreviewDialog> 제어 합니다.  
  
 [PageSetupDialog 구성 요소](../controls/pagesetupdialog-component-windows-forms.md)  
 사용법을 설명 합니다 <xref:System.Windows.Forms.PageSetupDialog> 구성 요소입니다.  
  
 <xref:System.Drawing.Printing>  
 클래스를 설명 합니다 <xref:System.Drawing.Printing> 네임 스페이스입니다.
