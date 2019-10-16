---
title: '방법: TextBox에서 줄 컬렉션 가져오기'
ms.date: 03/30/2017
helpviewer_keywords:
- lines [WPF], getting collection of
- TextBox control [WPF], getting collection of lines
ms.assetid: a12f529d-b926-47f6-92bf-cad5f17b532a
ms.openlocfilehash: b7b2f1c2e071388635fb50b1e3573fd7f44334dd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052484"
---
# <a name="how-to-get-a-collection-of-lines-from-a-textbox"></a>방법: TextBox에서 줄 컬렉션 가져오기
이 예제에서는 텍스트에서 줄 컬렉션 가져오기는 <xref:System.Windows.Controls.TextBox>합니다.  
  
## <a name="example"></a>예제  
 다음 예제는 간단한 메서드를 보여 줍니다.는 <xref:System.Windows.Controls.TextBox> 인수 및 반환을 <xref:System.Collections.Specialized.StringCollection> 의 텍스트 줄을 포함 하는 **텍스트 상자에 붙여넣습니다**합니다.  <xref:System.Windows.Controls.TextBox.LineCount%2A> 속성을 사용 하는 줄은 현재 확인 합니다 **텍스트 상자**, 및 <xref:System.Windows.Controls.TextBox.GetLineText%2A> 메서드는 다음 각 줄을 추출 하 고 선 컬렉션에 추가 하는 데 사용 됩니다.  
  
 [!code-csharp[TextBox_MiscCode#_TextBox_GetLines](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textbox_getlines)]  
  
## <a name="see-also"></a>참고자료

- [TextBox 개요](textbox-overview.md)
- [RichTextBox 개요](richtextbox-overview.md)
