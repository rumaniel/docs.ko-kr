---
title: '방법: TextBox에서 텍스트가 변경되는 시점 감지'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TextBox control [WPF], detecting text change
- text change [WPF], detecting
- detecting text change [WPF]
ms.assetid: 1c39ee14-e37f-49fb-a0d1-a9824ca13584
ms.openlocfilehash: 8c7744e9e61b8ba796802e54435c0bf9fdbee50e
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855613"
---
# <a name="how-to-detect-when-text-in-a-textbox-has-changed"></a>방법: TextBox에서 텍스트가 변경되는 시점 감지

이 예제에서는 <xref:System.Windows.Controls.TextBox> 컨트롤의 텍스트가 변경 될 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 때마다 이벤트를 사용 하 여 메서드를 실행 하는 한 가지 방법을 보여 줍니다.

변경 내용을 모니터링 하려는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] <xref:System.Windows.Controls.TextBox> 컨트롤이 포함 된의 코드 숨김이 클래스에서 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 이벤트가 발생할 때마다 호출할 메서드를 삽입 합니다.  이 메서드에는 <xref:System.Windows.Controls.TextChangedEventHandler> 대리자가 예상 하는 시그니처와 일치 하는 시그니처가 있어야 합니다.

사용자 또는 프로그래밍 방식으로 <xref:System.Windows.Controls.TextBox> 컨트롤의 내용이 변경 될 때마다 이벤트 처리기가 호출 됩니다.

> [!NOTE]
> 이 이벤트는 <xref:System.Windows.Controls.TextBox> 컨트롤이 만들어지고 처음에 텍스트로 채워질 때 발생 합니다.

## <a name="example"></a>예제

컨트롤을 정의 하는에서 이벤트 처리기 메서드 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 이름과 일치 하는 값을 사용 하 여 특성을 지정 합니다. [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] <xref:System.Windows.Controls.TextBox>

[!code-xaml[TextBox_MiscCode#_TextChangedXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textchangedxaml)]

## <a name="example"></a>예제

변경 내용을 모니터링 하려는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] <xref:System.Windows.Controls.TextBox> 컨트롤이 포함 된의 코드 숨김이 클래스에서 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 이벤트가 발생할 때마다 호출할 메서드를 삽입 합니다.  이 메서드에는 <xref:System.Windows.Controls.TextChangedEventHandler> 대리자가 예상 하는 시그니처와 일치 하는 시그니처가 있어야 합니다.

[!code-csharp[TextBox_MiscCode#_TextChangedEventHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textchangedeventhandler)]
[!code-vb[TextBox_MiscCode#_TextChangedEventHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_textchangedeventhandler)]

사용자 또는 프로그래밍 방식으로 <xref:System.Windows.Controls.TextBox> 컨트롤의 내용이 변경 될 때마다 이벤트 처리기가 호출 됩니다.

> [!NOTE]
> 이 이벤트는 <xref:System.Windows.Controls.TextBox> 컨트롤이 만들어지고 처음에 텍스트로 채워질 때 발생 합니다.

주석

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.TextChangedEventArgs>
- [TextBox 개요](textbox-overview.md)
- [RichTextBox 개요](richtextbox-overview.md)
