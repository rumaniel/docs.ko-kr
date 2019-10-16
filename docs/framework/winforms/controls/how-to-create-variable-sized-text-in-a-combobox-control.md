---
title: '방법: ComboBox 컨트롤에서 가변 크기 텍스트 만들기'
ms.date: 03/30/2017
dev_langs:
- vb
helpviewer_keywords:
- text [Windows Forms], drawing in combo boxes
- examples [Windows Forms], ComboBox control
- combo boxes [Windows Forms], drawing text
- ComboBox control [Windows Forms], examples [C#]
- ComboBox control [Windows Forms], drawing custom text
ms.assetid: ce39b9ea-e626-49fe-bd5a-f567f6d157df
ms.openlocfilehash: acc5ee47536772d98fcfe98849335933c24a41d7
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015901"
---
# <a name="how-to-create-variable-sized-text-in-a-combobox-control"></a>방법: ComboBox 컨트롤에서 가변 크기 텍스트 만들기
이 예제에서는 <xref:System.Windows.Forms.ComboBox> 컨트롤의 텍스트에 대 한 사용자 지정 그리기를 보여 줍니다. 특정 조건을 충족 하는 항목은 더 큰 글꼴로 그려지고 빨간색으로 설정 됩니다.

## <a name="example"></a>예제

```vb
Private Sub ComboBox1_MeasureItem(ByVal sender As Object, ByVal e As _
System.Windows.Forms.MeasureItemEventArgs) Handles ComboBox1.MeasureItem
    Dim bFont As New Font("Arial", 8, FontStyle.Bold)
    Dim lFont As New Font("Arial", 12, FontStyle.Bold)
    Dim siText As SizeF

    If ComboBox1.Items().Item(e.Index) = "Two" Then
        siText = e.Graphics.MeasureString(ComboBox1.Items().Item(e.Index), _
lFont)
    Else
        siText = e.Graphics.MeasureString(ComboBox1.Items().Item(e.Index), bFont)
    End If

    e.ItemHeight = siText.Height
    e.ItemWidth = siText.Width
End Sub

Private Sub ComboBox1_DrawItem(ByVal sender As Object, ByVal e As _
System.Windows.Forms.DrawItemEventArgs) Handles ComboBox1.DrawItem
    Dim g As Graphics = e.Graphics
    Dim bFont As New Font("Arial", 8, FontStyle.Bold)
    Dim lFont As New Font("Arial", 12, FontStyle.Bold)

    If ComboBox1.Items().Item(e.Index) = "Two" Then
        g.DrawString(ComboBox1.Items.Item(e.Index), lfont, Brushes.Red, _
e.Bounds.X, e.Bounds.Y)
    Else
        g.DrawString(ComboBox1.Items.Item(e.Index), bFont, Brushes.Black, e.Bounds.X, e.Bounds.Y)
    End If
End Sub
```

## <a name="compiling-the-code"></a>코드 컴파일
 이 예제에는 다음 사항이 필요합니다.

- Windows 폼입니다.

- 속성에 세 `ListBox1` 개의 항목이 <xref:System.Windows.Forms.ComboBox> 있는 이라는 <xref:System.Windows.Forms.ComboBox.Items%2A> 컨트롤입니다. 이 예제에서는 세 개의 항목에 이름이 지정 `"One", Two", and Three"`됩니다. 의 <xref:System.Windows.Forms.ComboBox.DrawMode%2A> <xref:System.Windows.Forms.DrawMode.OwnerDrawVariable>속성은로 설정 해야 합니다. `ComboBox1`

    > [!NOTE]
    > 이 기술은 <xref:System.Windows.Forms.ListBox> 컨트롤에도 적용 됩니다 <xref:System.Windows.Forms.ComboBox>.를로 <xref:System.Windows.Forms.ListBox> 대체할 수 있습니다.

- <xref:System.Windows.Forms?displayProperty=nameWithType> 및 <xref:System.Drawing?displayProperty=nameWithType> 네임스페이스에 대한 참조

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ComboBox.DrawItem>
- <xref:System.Windows.Forms.DrawItemEventArgs>
- <xref:System.Windows.Forms.ComboBox.MeasureItem>
- [소유자 그리기 지원이 기본 제공되는 컨트롤](controls-with-built-in-owner-drawing-support.md)
- [ListBox 컨트롤](listbox-control-windows-forms.md)
- [ComboBox 컨트롤](combobox-control-windows-forms.md)
