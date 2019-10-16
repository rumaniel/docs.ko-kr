---
title: Windows Forms 및 컨트롤의 국제 글꼴
ms.date: 03/30/2017
helpviewer_keywords:
- fonts [Windows Forms], international
- international applications [Windows Forms], character display
- fonts [Windows Forms], globalization considerations
- localization [Windows Forms], fonts
- Windows Forms controls, labels
- font fallback in Windows Forms
- globalization [Windows Forms], character sets
dev_langs:
- csharp
- vb
ms.assetid: 2c3066df-9bac-479a-82b2-79e484b346a3
ms.openlocfilehash: 0ddbd6d7a1b614d588a2572b410957a5ed3b768c
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956911"
---
# <a name="international-fonts-in-windows-forms-and-controls"></a>Windows Forms 및 컨트롤의 국제 글꼴

국가별 응용 프로그램에서는 가능한 경우 글꼴 대체를 사용 하는 것이 좋습니다. 글꼴 대체 (fallback)는 시스템에서 문자가 속하는 스크립트를 결정 함을 의미 합니다.

## <a name="using-font-fallback"></a>글꼴 대체 사용

이 기능을 활용 하려면 폼 또는 다른 요소에 대 한 <xref:System.Drawing.Font> 속성을 설정 하지 마세요. 응용 프로그램은 운영 체제의 지역화 된 언어와 다른 언어의 기본 시스템 글꼴을 자동으로 사용 합니다. 응용 프로그램이 실행 되 면 운영 체제에서 선택한 문화권에 맞는 글꼴이 자동으로 제공 됩니다.

글꼴을 설정 하는 것이 아니라 글꼴 스타일을 변경 하는 경우에는 예외가 발생 합니다. 사용자가 단추를 클릭 하 여 텍스트 상자의 텍스트를 굵게 표시 하는 응용 프로그램의 경우에는이 작업을 수행 하는 것이 중요할 수 있습니다. 이렇게 하려면 폼의 글꼴이 무엇 인지에 따라 텍스트 상자의 글꼴 스타일을 굵게 변경 하는 함수를 작성 합니다. 단추의 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기와 <xref:System.Windows.Forms.Control.FontChanged> 이벤트 처리기의 두 위치에서이 함수를 호출 하는 것이 중요 합니다. @No__t-0 이벤트 처리기 에서만 함수를 호출 하 고 일부 코드 조각이 전체 폼의 글꼴 패밀리를 변경 하는 경우 텍스트 상자는 폼의 나머지 부분으로 변경 되지 않습니다.

```vb
Private Sub MakeBold()
   ' Change the TextBox to a bold version of the form font
   TextBox1.Font = New Font(Me.Font, FontStyle.Bold)
End Sub

Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
   ' Clicking this button makes the TextBox bold
   MakeBold()
End Sub

Private Sub Form1_FontChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.FontChanged
   ' If the TextBox is already bold and the form's font changes,
   ' change the TextBox to a bold version of the new form font
   If (TextBox1.Font.Style = FontStyle.Bold) Then
      MakeBold()
   End If
End Sub
```

```csharp
private void button1_Click(object sender, System.EventArgs e)
{
   // Clicking this button makes the TextBox bold
   MakeBold();
}

private void MakeBold()
{
   // Change the TextBox to a bold version of the form's font
   textBox1.Font = new Font(this.Font, FontStyle.Bold);
}

private void Form1_FontChanged(object sender, System.EventArgs e)
{
   // If the TextBox is already bold and the form's font changes,
   // change the TextBox to a bold version of the new form font
   if (textBox1.Font.Style == FontStyle.Bold)
   {
      MakeBold();
   }
}
```

그러나 응용 프로그램을 지역화할 때 굵은 글꼴이 특정 언어에 대해 제대로 표시 되지 않을 수 있습니다. 이 경우 지역화 담당자에 게 글꼴을 굵게 전환 하 여 일반 텍스트로 전환 하는 옵션이 필요 합니다. 지역화 담당자는 일반적으로 개발자가 아니라 소스 코드에 대 한 액세스 권한이 없기 때문에 리소스 파일에이 옵션을 설정 해야 합니다. 이렇게 하려면 <xref:System.Drawing.Font.Bold%2A> 속성을 `true`로 설정 합니다. 그 결과, 지역화 담당자가 편집할 수 있는 리소스 파일에 글꼴 설정이 기록 됩니다. 그런 다음 `InitializeComponent` 메서드 뒤에 코드를 작성 하 여 폼의 글꼴에 관계 없이 리소스 파일에 지정 된 글꼴 스타일을 사용 하 여 글꼴을 다시 설정 합니다.

```vb
TextBox1.Font = New System.Drawing.Font(Me.Font, TextBox1.Font.Style)
```

```csharp
textBox1.Font = new System.Drawing.Font(this.Font, textBox1.Font.Style);
```
  
## <a name="see-also"></a>참조

- [글꼴 및 텍스트 사용](using-fonts-and-text.md)
