---
title: '방법: TextBox 컨트롤의 텍스트 내용 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text content [WPF], setting
- TextBox control [WPF], setting text content
ms.assetid: bcd25fc7-a52f-4453-b802-2c8d2b335ab8
ms.openlocfilehash: 2e2bc70b108991fd4e3c138bfac5bff942173e33
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856117"
---
# <a name="how-to-set-the-text-content-of-a-textbox-control"></a>방법: TextBox 컨트롤의 텍스트 내용 설정

이 예제에서는 <xref:System.Windows.Controls.TextBox.Text%2A> 속성을 사용 하 여 <xref:System.Windows.Controls.TextBox> 컨트롤의 초기 텍스트 콘텐츠를 설정 하는 방법을 보여 줍니다.

> [!NOTE]
> `<TextBox.Text>` <xref:System.Windows.Markup.ContentPropertyAttribute> <xref:System.Windows.Controls.TextBox.Text%2A> <xref:System.Windows.Controls.TextBox> 이 예제의 <xref:System.Windows.Controls.TextBox> 버전에서는 각 단추의 콘텐츠 텍스트 주위에 있는 태그를 사용할 수 있지만에서 속성에 특성을 적용 하기 때문에 필요 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 하지 않습니다. . 자세한 내용은 [XAML 개요 (WPF)](../advanced/xaml-overview-wpf.md)합니다.

## <a name="example"></a>예제

[!code-xaml[TextBox_MiscCode#_TextBoxSetTextXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxsettextxaml)]

## <a name="example"></a>예제

[!code-csharp[TextBox_MiscCode#_TextBoxSetText](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textboxsettext)]
[!code-vb[TextBox_MiscCode#_TextBoxSetText](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_textboxsettext)]

## <a name="see-also"></a>참고자료

- [TextBox 개요](textbox-overview.md)
- [RichTextBox 개요](richtextbox-overview.md)
