---
title: PrintDialog 구성 요소를 표시 하는 방법
ms.date: 03/30/2017
helpviewer_keywords:
- Print dialog box [Windows Forms], displaying
- PrintDialog component [Windows Forms], displaying
- printing [Windows Forms], displaying print dialog box
ms.assetid: 745a8db7-0526-4b21-b09d-18e13ed32014
ms.openlocfilehash: de0acc655bbcf0cfc017d594545fae56cc27f981
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65637449"
---
# <a name="how-to-display-the-printdialog-component"></a>PrintDialog 구성 요소를 표시 하는 방법

<xref:System.Windows.Forms.PrintDialog> 구성 요소는 쉽게 익힐 수 많은 사용자는 표준 Windows 인쇄 대화 상자. 사용자가 즉시 익숙해 때문에 좋을 것을 사용 하 여 <xref:System.Windows.Forms.PrintDialog> 구성 요소입니다.

## <a name="to-display-the-printdialog-component"></a>PrintDialog 구성 요소를 표시하려면

- 호출 된 <xref:System.Windows.Forms.Form.ShowDialog%2A> 응용 프로그램의 코드 내에서 메서드.

     구성 요소가 표시되면 사용자가 이 구성 요소와 상호 작용하여 인쇄 작업의 속성을 설정합니다. 에 저장 된 이러한 합니다 <xref:System.Drawing.Printing.PrinterSettings> 클래스 (및 <xref:System.Drawing.Printing.PageSettings> 클래스를 사용자가 액세스 하는 경우를 [PageSetupDialog 구성 요소](pagesetupdialog-component-windows-forms.md) 를 통해를 <xref:System.Windows.Forms.PrintDialog> 구성 요소) 인쇄 작업에 연결 된. 그런 다음 설정한 속성을 호출하여 인쇄 작업의 세부 사항을 결정할 수 있습니다.

## <a name="see-also"></a>참고자료

- [방법: 표준 Windows Forms 인쇄 작업 만들기](../advanced/how-to-create-standard-windows-forms-print-jobs.md)
- [방법: 런타임에 PrintDialog에서 사용자 입력 캡처](../advanced/how-to-capture-user-input-from-a-printdialog-at-run-time.md)
- [PrintPreviewDialog 컨트롤](printpreviewdialog-control-windows-forms.md)
- [PrintDialog 구성 요소](printdialog-component-windows-forms.md)
- [Windows Forms 인쇄 지원](../advanced/windows-forms-print-support.md)
- [Windows Forms 컨트롤](index.md)
