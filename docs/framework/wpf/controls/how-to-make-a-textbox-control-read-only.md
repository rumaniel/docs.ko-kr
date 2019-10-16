---
title: '방법: TextBox 컨트롤을 읽기 전용으로 설정'
ms.date: 03/30/2017
helpviewer_keywords:
- read-only TextBox controls [WPF]
- TextBox control read-only
ms.assetid: e707ec59-8b22-473e-b77c-3060a237517a
ms.openlocfilehash: 7f24458eb98bd669d59f15c49d1d9e3beb6833b1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770944"
---
# <a name="how-to-make-a-textbox-control-read-only"></a>방법: TextBox 컨트롤을 읽기 전용으로 설정
구성 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.TextBox> 컨트롤이 사용자 입력 또는 수정할 수 없습니다.  
  
## <a name="example"></a>예제  
 내용을 수정 하지 못하게 하려면를 <xref:System.Windows.Controls.TextBox> 컨트롤을 설정 합니다 <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> 특성을 **true**합니다.  
  
 [!code-xaml[TextBox_MiscCode#_ReadOnlyTextBoxXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_readonlytextboxxaml)]  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> 특성에 사용자 입력에만 영향을 줍니다;에 설정 된 텍스트에는 영향을 주지 않습니다를 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 설명은 <xref:System.Windows.Controls.TextBox> 컨트롤 또는 통해 프로그래밍 방식으로 설정 하는 텍스트를 <xref:System.Windows.Controls.TextBox.Text%2A> 속성.  
  
 기본값인 <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> 됩니다 **false**합니다.  
  
## <a name="see-also"></a>참고자료

- [TextBox 개요](textbox-overview.md)
- [RichTextBox 개요](richtextbox-overview.md)
