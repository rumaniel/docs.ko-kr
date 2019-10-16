---
title: '방법: 여러 줄 TextBox 컨트롤 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- TextBox control [WPF], multiple lines of text
ms.assetid: 05914a93-d0ea-4a9a-b693-09df7d4e2ac2
ms.openlocfilehash: 29fb4c9498fe163c36e71680242d3ef8cf98c089
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001275"
---
# <a name="how-to-create-a-multiline-textbox-control"></a>방법: 여러 줄 TextBox 컨트롤 만들기
이 예제에 사용 하는 방법을 보여 줍니다 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 정의 하는 <xref:System.Windows.Controls.TextBox> 컨트롤을 여러 줄의 텍스트에 맞게 자동으로 확장 됩니다.  
  
## <a name="example"></a>예제  
 설정 합니다 <xref:System.Windows.Controls.TextBox.TextWrapping%2A> 특성을 **줄 바꿈** 입력 한 텍스트를 새 줄 바꿈이 발생 할 때 줄 가장자리를 <xref:System.Windows.Controls.TextBox> 컨트롤에 도달 하면 자동으로 확장 되는 <xref:System.Windows.Controls.TextBox> 제어 하는 경우 새 줄에 대 한 공간을 포함 하도록 필요 합니다.  
  
 설정 합니다 <xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsReturn%2A> 특성을 **true** RETURN 키를 누르면 자동으로 다시 한 번 확장 삽입할 새 줄을 <xref:System.Windows.Controls.TextBox> 필요한 경우 새 줄에 대 한 공간을 포함 하도록 합니다.  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.VerticalScrollBarVisibility%2A> 특성에 있는 스크롤 막대를 추가 합니다 <xref:System.Windows.Controls.TextBox>되도록 내용의 <xref:System.Windows.Controls.TextBox> 경우 스크롤할 수를 <xref:System.Windows.Controls.TextBox> 포함 하는 창 프레임의 크기 이상으로 확장.  
  
 [!code-xaml[TextBox_MiscCode#_MultilineTextBoxXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_multilinetextboxxaml)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.TextWrapping>
- [TextBox 개요](textbox-overview.md)
- [RichTextBox 개요](richtextbox-overview.md)
