---
title: '방법: 상황에 맞는 메뉴에서 맞춤법 검사 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enabling spell checking in a text box [WPF]
- reenabling spell checking in a text box [WPF]
- spell checking with a context menu [WPF]
ms.assetid: 61f69a20-2ff3-4056-9060-e32f4483ec5e
ms.openlocfilehash: 72b24c386eb99140c9c2729688994b81f92e1a6f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61699151"
---
# <a name="how-to-use-spell-checking-with-a-context-menu"></a>방법: 상황에 맞는 메뉴에서 맞춤법 검사 사용
기본적으로 편집 컨트롤에서 맞춤법 검사를 사용 하도록 설정 하면 같은 <xref:System.Windows.Controls.TextBox> 또는 <xref:System.Windows.Controls.RichTextBox>, 맞춤법 검사 옵션이 상황에 맞는 메뉴에 표시 합니다. 예를 들어 사용자가 맞춤법이 틀린된 단어를 마우스 오른쪽 단추로 받게 추천 또는 옵션 집합이 **모두 무시**합니다. 그러나 사용자 고유의 사용자 지정 상황에 맞는 메뉴를 사용 하 여 기본 상황에 맞는 메뉴를 재정의 하는 경우이 기능 손실 되 고 상황에 맞는 메뉴에서 맞춤법 검사 기능을 다시 사용 하도록 설정 하는 코드를 작성 해야 합니다. 다음 예제에서이 사용 하도록 설정 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.TextBox>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 만들어지는 <xref:System.Windows.Controls.TextBox> 상황에 맞는 메뉴를 구현 하는 데 사용 되는 일부 이벤트를 사용 하 여 합니다.  
  
 [!code-xaml[TextBoxMiscSnippets_snip#SpellerCustomContextMenuExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml#spellercustomcontextmenuexamplewholepage)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 상황에 맞는 메뉴를 구현 하는 코드를 보여 줍니다.  
  
 [!code-csharp[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml.cs#spellercustomcontextmenucodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/visualbasic/speller_custom_context_menu.xaml.vb#spellercustomcontextmenucodeexamplewholepage)]  
  
 사용 하 여이 작업을 수행 하는 데 사용 하는 코드는 <xref:System.Windows.Controls.RichTextBox> 비슷합니다. 주요 차이점은 전달 된 매개 변수는 `GetSpellingError` 메서드. 에 대 한는 <xref:System.Windows.Controls.TextBox>, 캐럿 위치의 정수 인덱스를 전달 합니다.  
  
 `spellingError = myTextBox.GetSpellingError(caretIndex);`  
  
 에 대 한는 <xref:System.Windows.Controls.RichTextBox>에 전달 합니다 <xref:System.Windows.Documents.TextPointer> 캐럿 위치를 지정 하는:  
  
 `spellingError = myRichTextBox.GetSpellingError(myRichTextBox.CaretPosition);`  
  
## <a name="see-also"></a>참고자료

- [TextBox 개요](textbox-overview.md)
- [RichTextBox 개요](richtextbox-overview.md)
- [텍스트 편집 컨트롤에서 맞춤법 검사 사용](how-to-enable-spell-checking-in-a-text-editing-control.md)
- [TextBox에 사용자 지정 컨텍스트 메뉴 사용](how-to-use-a-custom-context-menu-with-a-textbox.md)
