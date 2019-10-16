---
title: PrintDocument 구성 요소 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- PrintDocument
helpviewer_keywords:
- PrintDocument component [Windows Forms], about PrintDocument component
- printing [Windows Forms], PrintDocument component
ms.assetid: b59b4b60-dce5-42ca-8421-3a54a2f7bab0
ms.openlocfilehash: 16a7f3a34ccb280f7bf91c52e29b20edc22130b9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69928987"
---
# <a name="printdocument-component-overview-windows-forms"></a>PrintDocument 구성 요소 개요(Windows Forms)

Windows Forms [PrintDocument](printdocument-component-windows-forms.md) 구성 요소는 인쇄 대상 및 Windows 기반 애플리케이션 내에서 문서를 인쇄하는 기능을 설명하는 속성을 설정하는 데 사용됩니다. 모든 문서 인쇄 측면의 제어에 포함되도록 [PrintDialog](printdialog-component-windows-forms.md) 구성 요소와 함께 사용할 수 있습니다.

## <a name="working-with-the-printdocument-component"></a>PrintDocument 구성 요소 작업

구성 요소와 <xref:System.Drawing.Printing.PrintDocument> 관련 된 두 가지 주요 시나리오는 다음과 같습니다.

- 개별 텍스트 파일 인쇄 등의 간단한 인쇄 작업. 이 경우 Windows Form에 <xref:System.Drawing.Printing.PrintDocument> 구성 요소를 추가한 다음 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트 처리기에 파일을 인쇄 하는 프로그래밍 논리를 추가 합니다. 프로그래밍 논리는 문서를 인쇄 하 <xref:System.Drawing.Printing.PrintDocument.Print%2A> 는 메서드와 식은 됩니다. 이 메서드는 <xref:System.Drawing.Graphics> <xref:System.Drawing.Printing.PrintPageEventArgs> 클래스의 <xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A> 속성에 포함 된 개체를 프린터로 보냅니다. <xref:System.Drawing.Printing.PrintDocument> 구성 요소[를 사용 하 여 텍스트 문서를 인쇄 하는 방법을 보여 주는 예제는 방법: Windows Forms](../advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)에서 다중 페이지 텍스트 파일을 인쇄 합니다.

- 작성한 인쇄 논리를 다시 사용하려는 상황과 같은 좀 더 복잡한 인쇄 작업. 이러한 경우에는 <xref:System.Drawing.Printing.PrintDocument> 구성 요소에서 새 구성 요소를 파생 시키고 (Visual Basic에 대한 [재정의](../../../visual-basic/language-reference/modifiers/overrides.md) 또는 [재정의](../../../csharp/language-reference/keywords/override.md) C#참조) <xref:System.Drawing.Printing.PrintDocument.PrintPage> 이벤트를 재정의합니다.

폼에 추가 되 면 구성 요소는 <xref:System.Drawing.Printing.PrintDocument> Visual Studio의 Windows Forms 디자이너 아래쪽에 있는 트레이에 표시 됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Graphics>
- <xref:System.Drawing.Printing.PrintDocument>
- [Windows Forms 인쇄 지원](../advanced/windows-forms-print-support.md)
- [PrintDocument 구성 요소](printdocument-component-windows-forms.md)
