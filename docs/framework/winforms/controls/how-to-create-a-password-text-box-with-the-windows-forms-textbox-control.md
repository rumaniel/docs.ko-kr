---
title: '방법: Windows Forms TextBox 컨트롤을 사용하여 암호 텍스트 상자 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- TextBox control [Windows Forms], entering passwords
- password boxes [Windows Forms], creating
- PasswordChar property in text boxes
- passwords [Windows Forms], input mask
- passwords [Windows Forms], password text box
ms.assetid: d105d6b9-3d50-44cd-80d8-2c0e2f486727
ms.openlocfilehash: 56391777c75db288c33d1b2192355be0df50f7ee
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046115"
---
# <a name="how-to-create-a-password-text-box-with-the-windows-forms-textbox-control"></a>방법: Windows Forms TextBox 컨트롤을 사용하여 암호 텍스트 상자 만들기

암호 상자는 사용자가 문자열을 입력할 때 자리 표시자 문자를 표시 하는 Windows Forms 텍스트 상자입니다.

### <a name="to-create-a-password-text-box"></a>암호 텍스트 상자를 만들려면

1. 컨트롤의 속성을 특정 문자로 설정 합니다. <xref:System.Windows.Forms.TextBox.PasswordChar%2A> <xref:System.Windows.Forms.TextBox>

    속성 <xref:System.Windows.Forms.TextBox.PasswordChar%2A> 은 텍스트 상자에 표시 되는 문자를 지정 합니다. 예를 들어, 암호 상자에 별표를 표시 하려면 속성 창에서 <xref:System.Windows.Forms.TextBox.PasswordChar%2A> 속성에 *를 지정 합니다. 그러면 사용자가 텍스트 상자에 입력 하는 문자에 관계 없이 별표가 표시 됩니다.

2. 필드 속성을 <xref:System.Windows.Forms.TextBoxBase.MaxLength%2A> 설정 합니다. 속성은 텍스트 상자에 입력할 수 있는 문자 수를 결정 합니다. 최대 길이를 초과 하면 시스템에서 경고음을 발생 하 고 텍스트 상자에 더 이상 문자를 사용할 수 없습니다. 암호를 추측 하려는 해커에 게 암호의 최대 길이를 사용할 수 있으므로이 작업을 수행 하지 않는 것이 좋습니다.

    다음 코드 예제에서는 최대 14 자 길이의 문자열을 허용 하 고 문자열 대신 별표를 표시 하는 입력란을 초기화 하는 방법을 보여 줍니다. 프로시저 `InitializeMyControl` 는 자동으로 실행 되지 않습니다 .이 프로시저는 호출 되어야 합니다.

    > [!IMPORTANT]
    > 텍스트 상자 <xref:System.Windows.Forms.TextBox.PasswordChar%2A> 에 속성을 사용 하면 사용자가 입력을 관찰 하는 경우 다른 사용자가 사용자의 암호를 확인할 수 없게 됩니다. 이 보안 조치는 응용 프로그램 논리로 인해 발생할 수 있는 암호의 저장소 또는 전송 종류를 포함 하지 않습니다. 입력 한 텍스트는 어떤 방식으로든 암호화 되지 않으므로 다른 기밀 데이터와 동일 하 게 처리 해야 합니다. 이와 같이 표시 되지 않지만 몇 가지 추가 보안 조치를 구현 하지 않은 경우에도 암호는 일반 텍스트 문자열로 처리 됩니다.

    ```vb
    Private Sub InitializeMyControl()
       ' Set to no text.
       TextBox1.Text = ""
       ' The password character is an asterisk.
       TextBox1.PasswordChar = "*"
       ' The control will allow no more than 14 characters.
       TextBox1.MaxLength = 14
    End Sub
    ```

    ```csharp
    private void InitializeMyControl()
    {
       // Set to no text.
       textBox1.Text = "";
       // The password character is an asterisk.
       textBox1.PasswordChar = '*';
       // The control will allow no more than 14 characters.
       textBox1.MaxLength = 14;
    }
    ```

    ```cpp
    private:
       void InitializeMyControl()
       {
          // Set to no text.
          textBox1->Text = "";
          // The password character is an asterisk.
          textBox1->PasswordChar = '*';
          // The control will allow no more than 14 characters.
          textBox1->MaxLength = 14;
       }
    ```

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TextBox>
- [TextBox 컨트롤 개요](textbox-control-overview-windows-forms.md)
- [방법: Windows Forms TextBox 컨트롤에서 삽입 지점 제어](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [방법: 읽기 전용 텍스트 상자 만들기](how-to-create-a-read-only-text-box-windows-forms.md)
- [방법: 문자열에 따옴표를 추가 합니다.](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [방법: Windows Forms TextBox 컨트롤에서 텍스트 선택](how-to-select-text-in-the-windows-forms-textbox-control.md)
- [방법: Windows Forms TextBox 컨트롤에서 여러 줄 보기](how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)
- [TextBox 컨트롤](textbox-control-windows-forms.md)
