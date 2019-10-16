---
title: '방법: 텍스트 선택 검색'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [WPF], retrieving
- TextBox control [WPF], retrieving text
- retrieving text [WPF]
ms.assetid: d5793172-1e11-4a39-9be0-73f336ed858d
ms.openlocfilehash: b7f0b9ee02a7ace717787fc8eeb6e15649829a49
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770788"
---
# <a name="how-to-retrieve-a-text-selection"></a>방법: 텍스트 선택 검색
이 예제에 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Controls.TextBox.SelectedText%2A> 에서 사용자가 선택한 텍스트를 검색할 속성을 <xref:System.Windows.Controls.TextBox> 컨트롤입니다.  
  
## <a name="example"></a>예제  
 다음 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 예제에서는 정의 보여 줍니다.을 <xref:System.Windows.Controls.TextBox> 를 선택 하려면 몇 가지 텍스트가 포함 된 컨트롤 및 <xref:System.Windows.Controls.Button> 지정 된 컨트롤 <xref:System.Windows.Controls.Button.OnClick%2A> 메서드.  
  
 이 예제에서는 연결 된 단추 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 선택한 텍스트를 검색할 이벤트 처리기를 사용 합니다. 사용자가 단추를 클릭 합니다 <xref:System.Windows.Controls.Button.OnClick%2A> 메서드 문자열에 텍스트 상자에 선택한 텍스트를 복사 합니다. 특정 상황 텍스트 선택은 검색 하는 (단추 클릭) 뿐만 아니라 해당 선택 (문자열로 텍스트 선택 영역 복사)를 사용 하 여 수행 되는 동작 다양 한 시나리오에 맞게 쉽게 수정할 수 있습니다.  
  
 [!code-xaml[TextBox_MiscCode#_TextBoxSelectTextXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxselecttextxaml)]  
  
## <a name="example"></a>예제  
 다음 C# 예제는 <xref:System.Windows.Controls.Button.OnClick%2A> 에 정의 된 단추에 대 한 이벤트 처리기를 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 예입니다.  
  
 [!code-csharp[TextBox_MiscCode#_SelectText](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_selecttext)]
 [!code-vb[TextBox_MiscCode#_SelectText](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_selecttext)]  
  
## <a name="see-also"></a>참고자료

- [TextBox 개요](textbox-overview.md)
- [RichTextBox 개요](richtextbox-overview.md)
