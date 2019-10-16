---
title: RichTextBox 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], RichTextBox
- RichTextBox control [WPF], about RichTextBox control
ms.assetid: c94548b2-c1e9-4b62-b10c-dd8740eb23d8
ms.openlocfilehash: bfed42bcf3693ef744b3ed2b54ebe070931513a9
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855741"
---
# <a name="richtextbox-overview"></a>RichTextBox 개요

<xref:System.Windows.Controls.RichTextBox> 컨트롤을 사용 하면 단락, 이미지, 테이블 등을 비롯 한 유동 콘텐츠를 표시 하거나 편집할 수 있습니다. 이 항목에서는 클래스 <xref:System.Windows.Controls.TextBox> 를 소개 하 고 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 및 C#에서이 클래스를 사용 하는 방법에 대 한 예제를 제공 합니다.

<a name="textbox_or_richtextbox"></a>

## <a name="textbox-or-richtextbox"></a>TextBox 또는 RichTextBox?

<xref:System.Windows.Controls.RichTextBox> 및<xref:System.Windows.Controls.TextBox> 둘 다 사용자가 텍스트를 편집할 수 있도록 하지만 두 컨트롤이 서로 다른 시나리오에서 사용 됩니다. 는 <xref:System.Windows.Controls.RichTextBox> 사용자가 서식 있는 텍스트, 이미지, 테이블 또는 기타 풍부한 콘텐츠를 편집 해야 하는 경우에 더 적합 합니다. 예를 들어 형식 지정, 이미지 등이 필요한 문서, 문서 또는 블로그를 편집 하려면를 <xref:System.Windows.Controls.RichTextBox>사용 하는 것이 가장 좋습니다. 에 <xref:System.Windows.Controls.TextBox> 는 보다 작은 시스템 리소스가 <xref:System.Windows.Controls.RichTextBox> 필요 하 고, 일반 텍스트를 편집 해야 하는 경우 (예: 양식에서 사용)에 이상적입니다. 에<xref:System.Windows.Controls.TextBox>대 한 자세한 내용은 [TextBox 개요](textbox-overview.md) 를 참조 하세요. 아래 표에는 및 <xref:System.Windows.Controls.TextBox> <xref:System.Windows.Controls.RichTextBox>의 주요 기능이 요약 되어 있습니다.

|컨트롤|실시간 맞춤법 검사|상황에 맞는 메뉴|명령 서식 지정 <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> (Ctr + B)|<xref:System.Windows.Documents.FlowDocument>이미지, 단락, 테이블 등의 콘텐츠|
|-------------|------------------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|<xref:System.Windows.Controls.TextBox>|예|예|아니요|아니요.|
|<xref:System.Windows.Controls.RichTextBox>|예|예|예|예|

> [!NOTE]
> 는 <xref:System.Windows.Controls.TextBox> (Ctr + B)와 같은 <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> 형식 관련 명령을 지원 하지 않지만, 등의 두 컨트롤 <xref:System.Windows.Documents.EditingCommands.MoveToLineEnd%2A>에서 많은 기본 명령을 지원 합니다.

위 테이블의 기능은 나중에 더 자세히 설명합니다.

<a name="creating_a_richtextbox"></a>

## <a name="creating-a-richtextbox"></a>RichTextBox 만들기

아래 코드에서는 사용자가에서 서식 있는 <xref:System.Windows.Controls.RichTextBox> 콘텐츠를 편집할 수 있는을 만드는 방법을 보여 줍니다.

[!code-xaml[RichTextBoxMiscSnippets_snip#BasicRichTextBoxExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/BasicRichTextBoxExample.xaml#basicrichtextboxexamplewholepage)]

특히에서 <xref:System.Windows.Controls.RichTextBox> 편집 된 콘텐츠는 유동 콘텐츠입니다. 유동 콘텐츠에는 서식 있는 텍스트, 이미지, 목록 및 테이블과 같은 다양한 요소 형식이 포함될 수 있습니다. 유동 문서에 대한 자세한 내용은 [유동 문서 개요](../advanced/flow-document-overview.md)를 참조하세요. 는 <xref:System.Windows.Controls.RichTextBox> 유동 콘텐츠를 포함 하기 위해 편집 가능한 콘텐츠 <xref:System.Windows.Documents.FlowDocument> 를 포함 하는 개체를 호스팅합니다. 에서 <xref:System.Windows.Controls.RichTextBox>유동 콘텐츠를 시연 하기 위해 다음 코드에서는 단락과 굵게 표시 된 텍스트 <xref:System.Windows.Controls.RichTextBox> 를 사용 하 여을 만드는 방법을 보여 줍니다.

[!code-xaml[RichTextBoxMiscSnippets_snip#RichTextBoxWithContentExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/RichTextBoxWithContentExample.xaml#richtextboxwithcontentexamplewholepage)]

[!code-csharp[RichTextBoxMiscSnippets_procedural_snip#BasicRichTextBoxWithContentCodeOnlyExample](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_procedural_snip/CSharp/BasicRichTextBoxWithContentExample.cs#basicrichtextboxwithcontentcodeonlyexample)]
[!code-vb[RichTextBoxMiscSnippets_procedural_snip#BasicRichTextBoxWithContentCodeOnlyExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxMiscSnippets_procedural_snip/visualbasic/basicrichtextboxwithcontentexample.vb#basicrichtextboxwithcontentcodeonlyexample)]

다음 그림은 이 샘플에서 렌더링하는 방법을 보여줍니다.

![콘텐츠가 있는 RichTextBox](./media/editing-richtextbox-with-content.png "Editing_RichTextBox_with_Content")

<xref:System.Windows.Controls.RichTextBox> 및 <xref:System.Windows.Documents.Paragraph> 와같은요소는내의콘텐츠가표시되는방법을결정합니다.<xref:System.Windows.Documents.Bold> 사용자가 콘텐츠를 <xref:System.Windows.Controls.RichTextBox> 편집 하는 경우이 유동 콘텐츠를 변경 합니다. 유동 콘텐츠의 기능 및 이를 사용하는 방법에 대한 자세한 내용은 [유동 문서 개요](../advanced/flow-document-overview.md)를 참조하세요.

> [!NOTE]
> 내의 <xref:System.Windows.Controls.RichTextBox> 유동 콘텐츠는 다른 컨트롤에 포함 된 유동 콘텐츠와 똑같이 작동 하지 않습니다. 예를 들어에 <xref:System.Windows.Controls.RichTextBox> 열이 없으므로 자동 크기 조정 동작이 없습니다. 또한 검색, 보기 모드, 페이지 탐색 및 확대/축소와 같은 기본 제공 기능은 내 <xref:System.Windows.Controls.RichTextBox>에서 사용할 수 없습니다.

<a name="realtime_spellechecking"></a>

## <a name="real-time-spell-checking"></a>실시간 맞춤법 검사

<xref:System.Windows.Controls.TextBox> 또는<xref:System.Windows.Controls.RichTextBox>에서 실시간 맞춤법 검사를 사용 하도록 설정할 수 있습니다. 맞춤법 검사 기능이 켜져 있으면 맞춤법이 틀린 단어 밑에 빨간색 선이 나타납니다(아래 그림 참조).

![맞춤법 검사 기능이 있는 Textbox](./media/editing-textbox-with-spellchecking.png "Editing_TextBox_with_Spellchecking")

맞춤법 검사를 사용하도록 설정하는 방법에 대한 자세한 내용은 [텍스트 편집 컨트롤에서 맞춤법 검사 사용](how-to-enable-spell-checking-in-a-text-editing-control.md)을 참조하세요.

<a name="context_menu"></a>

## <a name="context-menu"></a>상황에 맞는 메뉴

기본적 <xref:System.Windows.Controls.TextBox> 으로 및 <xref:System.Windows.Controls.RichTextBox> 에는 사용자가 컨트롤 내에서 마우스 오른쪽 단추를 클릭할 때 표시 되는 상황에 맞는 메뉴가 있습니다. 상황에 맞는 메뉴를 통해 사용자는 항목을 잘라내거나, 복사하거나, 붙여넣을 수 있습니다(아래 그림 참조).

![상황에 맞는 메뉴가 있는 TextBox](./media/editing-textbox-with-context-menu.png "Editing_TextBox_with_Context_Menu")

자체적인 사용자 지정 상황에 맞는 메뉴를 만들어 기본 상황에 맞는 메뉴를 재정의할 수 있습니다. 자세한 내용은 [RichTextBox에서 사용자 지정 상황에 맞는 메뉴의 위치 지정](how-to-position-a-custom-context-menu-in-a-richtextbox.md)을 참조하세요.

<a name="detect_when_content_changes"></a>

## <a name="editing-commands"></a>편집 명령

편집 명령을 사용 하면 사용자가 내에서 <xref:System.Windows.Controls.RichTextBox>편집 가능한 콘텐츠의 서식을 지정할 수 있습니다. 기본 편집 명령 외에 <xref:System.Windows.Controls.RichTextBox> 도에는 <xref:System.Windows.Controls.TextBox> 를 지원 하지 않는 서식 지정 명령이 포함 되어 있습니다. 예를 들어에서 <xref:System.Windows.Controls.RichTextBox>편집할 때 사용자가 Ctr + B를 눌러 굵은 텍스트 서식 지정을 전환할 수 있습니다. 사용 <xref:System.Windows.Documents.EditingCommands> 가능한 명령의 전체 목록은를 참조 하세요. 바로 가기 키를 사용하는 방법 외에 단추와 같은 다른 컨트롤에 명령을 연결할 수 있습니다. 다음 예제에서는 사용자가 텍스트 서식을 변경하는 데 사용할 수 있는 단추가 포함된 간단한 도구 모음을 만드는 방법을 보여 줍니다.

[!code-xaml[RichTextBox_InputPanel_snip#RichTextBoxWithToolBarExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_InputPanel_snip/CS/Window1.xaml#richtextboxwithtoolbarexamplewholepage)]

다음 그림은 이 샘플에서 표시하는 방법을 보여줍니다.

![가 있는 RichTextBox](./media/editing-richtextbox-with-toobar.gif "Editing_RichTextBox_with_TooBar")

<a name="editing_commands"></a>

## <a name="detect-when-content-changes"></a>콘텐츠가 변경되는 시점 감지

일반적으로 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 때마다 검색에 사용할 이벤트의 텍스트를 <xref:System.Windows.Controls.TextBox> 또는 <xref:System.Windows.Controls.RichTextBox> 대신 변경 <xref:System.Windows.UIElement.KeyDown> 예상할 수 있듯이. 예제를 보려면 [TextBox에서 텍스트가 변경되는 시점 감지](how-to-detect-when-text-in-a-textbox-has-changed.md)를 참조하세요.

<a name="save_load_and_print_richtextbox_content"></a>

## <a name="save-load-and-print-richtextbox-content"></a>RichTextBox 콘텐츠 저장, 로드 및 인쇄

다음 예제에서는의 <xref:System.Windows.Controls.RichTextBox> 내용을 파일에 저장 하 고, 해당 콘텐츠를 다시 <xref:System.Windows.Controls.RichTextBox>에 로드 하 고, 내용을 인쇄 하는 방법을 보여 줍니다. 예제에 대한 태그는 다음과 같습니다.

[!code-xaml[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/SaveLoadPrintRTB.xaml#saveloadprintrtbexamplewholepage)]

예제에 대한 코드 숨김은 다음과 같습니다.

[!code-csharp[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/SaveLoadPrintRTB.xaml.cs#saveloadprintrtbcodeexamplewholepage)]
[!code-vb[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/VisualBasic/SaveLoadPrintRTB.xaml.vb#saveloadprintrtbcodeexamplewholepage)]

## <a name="see-also"></a>참고자료

- [방법 항목](richtextbox-how-to-topics.md)
- [TextBox 개요](textbox-overview.md)
