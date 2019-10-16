---
title: '방법: TextBox에 워터마크 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- displaying a background image inside a text box to aid user input [WPF]
- aid usability of a TextBox using a background image [WPF]
ms.assetid: df89bdd8-a0fb-45e0-b312-dd53332d01a8
ms.openlocfilehash: abe276c686d394ded13ec03f08deae65e4098d03
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923572"
---
# <a name="how-to-add-a-watermark-to-a-textbox"></a>방법: TextBox에 워터마크 추가
다음 예제에서는 사용자가 텍스트를 입력 한 후 <xref:System.Windows.Controls.TextBox> 이미지가 제거 <xref:System.Windows.Controls.TextBox> 될 때까지의 설명 배경 이미지를 표시 하 여의 유용성을 지 원하는 방법을 보여 줍니다. 또한 사용자가 입력을 제거 하면 배경 이미지가 다시 복원 됩니다. 아래 그림을 참조 하세요.  
  
 ![배경 이미지가 있는 입력란](./media/editing-textbox-using-background-image.png "Editing_TextBox_using_background_image")  
  
> [!NOTE]
> 이 예에서 배경 이미지를 사용 하는 이유는 단순히의 <xref:System.Windows.Controls.TextBox.Text%2A> <xref:System.Windows.Controls.TextBox>속성을 조작 하는 것입니다. 즉, 배경 이미지가 데이터 바인딩을 방해 하지 않습니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[TextBoxMiscSnippets_snip#TextBoxBackgroundExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/textbox_with_background_image.xaml#textboxbackgroundexamplewholepage)]  
  
 [!code-csharp[TextBoxMiscSnippets_snip#TextBoxBackgroundCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/textbox_with_background_image.xaml.cs#textboxbackgroundcodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_snip#TextBoxBackgroundCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/visualbasic/textbox_with_background_image.xaml.vb#textboxbackgroundcodeexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- [TextBox 개요](textbox-overview.md)
- [RichTextBox 개요](richtextbox-overview.md)
