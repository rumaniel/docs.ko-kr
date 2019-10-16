---
title: '방법: 텍스트 잘라내기 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [WPF], trimming
- documents [WPF], trimming text
- trimming text [WPF]
ms.assetid: dd8c9191-d2be-45fd-9fb4-3c75b65578c5
ms.openlocfilehash: 25fff566868e792004a915fee195485c4a1f385f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776130"
---
# <a name="how-to-enable-text-trimming"></a>방법: 텍스트 잘라내기 사용

사용 및 사용 가능한 값의 효과 보여 주는이 예제는 <xref:System.Windows.TextTrimming> 열거형입니다.

## <a name="example"></a>예제

다음 예제에서는 정의 <xref:System.Windows.Controls.TextBlock> 요소는 <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> 특성이 설정 합니다.

[!code-xaml[TextTrimmingSnippets#_TextTrimmingXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml#_texttrimmingxaml)]

해당 설정 <xref:System.Windows.TextTrimming> 코드에서 속성은 아래에 나와 있습니다.

[!code-csharp[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](~/samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml.cs#_texttrimmingsettexttrimming)]
[!code-vb[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextTrimmingSnippets/VisualBasic/Window1.xaml.vb#_texttrimmingsettexttrimming)]

현재 세 가지 방법으로 텍스트 잘라내기에 있습니다. **CharacterEllipsis**하십시오 **WordEllipsis**, 및 **None**합니다.

때 <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> 로 설정 된 **CharacterEllipsis**, 텍스트는 잘리고 잘리는 가장자리에서 가장 가까운 문자에 줄임표가 사용 됩니다.  이 설정은 잘리는 경계에 좀 더 가깝게 맞추어 텍스트를 잘라내기 때문에 단어가 부분적으로 잘릴 수 있습니다.  다음 그림에서이 설정의 효과 <xref:System.Windows.Controls.TextBlock> 위에 정의 된 것과 비슷합니다.

![예제: TextTrimming.CharacterEllipsis](./media/texttrimming-character.png "TextTrimming_Character")

때 <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> 로 설정 된 **WordEllipsis**, 텍스트는 잘리고 잘리는 가장자리에서 가장 가까운 첫 번째 전체 단어 끝에 줄임표가 사용 합니다.  이 설정은 부분적으로 잘라낸된 단어를 표시 하지 것입니다 하지만 잘라낸 가장자리와 가깝게 텍스트 트리밍 필요가 합니다 **CharacterEllipsis** 설정 합니다.  다음 그림에서이 설정의 효과 <xref:System.Windows.Controls.TextBlock> 위에 정의 된 합니다.

![예제: TextTrimming.WordEllipsis](./media/texttrimming-word.png "TextTrimming_Word")

때 <xref:System.Windows.Controls.TextBlock.TextTrimming%2A> 로 설정 된 **없음**, 없는 텍스트 잘라내기 수행 됩니다.  이 경우 텍스트가 부모 텍스트 컨테이너의 경계로 잘릴 뿐입니다.  다음 그림에서이 설정의 효과 <xref:System.Windows.Controls.TextBlock> 위에 정의 된 것과 비슷합니다.

![예제: TextTrimming.None](./media/texttrimming-none.png "TextTrimming_None")
