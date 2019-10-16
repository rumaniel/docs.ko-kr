---
title: '방법: 읽기 전용 텍스트 상자 만들기 (Windows Forms)'
ms.date: 03/30/2017
helpviewer_keywords:
- TextBox control [Windows Forms], read-only
- read-only text boxes
- text boxes [Windows Forms], read-only
ms.assetid: 60baa9ab-fa57-44ad-bb7c-61b05aa64296
ms.openlocfilehash: 18d2f5ed2530957487ac25c3eb6240f8bc50a938
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971937"
---
# <a name="how-to-create-a-read-only-text-box-windows-forms"></a>방법: 읽기 전용 텍스트 상자 만들기 (Windows Forms)

편집 가능한 Windows Forms 텍스트 상자를 읽기 전용 컨트롤로 변환할 수 있습니다. 예를 들어 텍스트 상자에는 일반적으로 편집 되지만 응용 프로그램의 상태로 인해 현재는 표시 되지 않는 값이 표시 될 수 있습니다.

## <a name="to-create-a-read-only-text-box"></a>읽기 전용 텍스트 상자를 만들려면

1. 컨트롤의 <xref:System.Windows.Forms.TextBoxBase.ReadOnly%2A> 속성을로 `true`설정 합니다. <xref:System.Windows.Forms.TextBox> 속성이로 `true`설정 된 경우 사용자는 변경 내용을 허용 하지 않고 텍스트 상자의 텍스트를 계속 스크롤하고 강조 표시할 수 있습니다. 텍스트 상자에서 **복사** 명령이 작동 하지만 **잘라내기** 및 **붙여넣기** 명령은 사용할 수 없습니다.

    > [!NOTE]
    > 속성 <xref:System.Windows.Forms.TextBoxBase.ReadOnly%2A> 은 런타임에 사용자 상호 작용에만 영향을 줍니다. 런타임에 텍스트 상자의 속성을 <xref:System.Windows.Forms.TextBox.Text%2A> 변경 하 여 텍스트 상자 콘텐츠를 프로그래밍 방식으로 변경할 수 있습니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TextBox>
- [TextBox 컨트롤 개요](textbox-control-overview-windows-forms.md)
- [방법: Windows Forms TextBox 컨트롤에서 삽입 지점 제어](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [방법: Windows Forms TextBox 컨트롤을 사용 하 여 암호 텍스트 상자 만들기](how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)
- [방법: 문자열에 따옴표를 추가 합니다.](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [방법: Windows Forms TextBox 컨트롤에서 텍스트 선택](how-to-select-text-in-the-windows-forms-textbox-control.md)
- [방법: Windows Forms TextBox 컨트롤에서 여러 줄 보기](how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)
- [TextBox 컨트롤](textbox-control-windows-forms.md)
