---
title: '방법: RichTextBox 컨트롤에 끌어 놓은 파일 열기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- drag-and-drop [WPF], RichTextBox
- RichTextBox [WPF], drag-and-drop
- drag-and-drop [WPF], open a dropped file
ms.assetid: 6bb8bb54-f576-41db-a9a7-24102ddeb490
ms.openlocfilehash: 408d48856362fa8a77a44e2cc97cb2d5ff608dcf
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046348"
---
# <a name="how-to-open-a-file-that-is-dropped-on-a-richtextbox-control"></a>방법: RichTextBox 컨트롤에 끌어 놓은 파일 열기

에서 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], 및 <xref:System.Windows.Controls.TextBox>컨트롤은모두 끌어서 놓기 기능을 <xref:System.Windows.Controls.RichTextBox>기본적으로 제공 합니다. <xref:System.Windows.Documents.FlowDocument> 기본 제공 기능을 사용 하면 컨트롤 내부와 컨트롤 사이에서 텍스트를 끌어서 놓을 수 있습니다. 그러나 컨트롤에 파일을 놓으면 파일을 열 수 없습니다. 이러한 컨트롤은 또한 끌어서 놓기 이벤트를 처리 된 것으로 표시 합니다. 결과적으로, 사용자 고유의 이벤트 처리기를 추가 하 여 삭제 된 파일을 여는 기능을 제공할 수 없습니다.

이러한 컨트롤에서 끌어서 놓기 이벤트에 대 한 추가 처리를 추가 하려면 <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 메서드를 사용 하 여 끌어서 놓기 이벤트에 대 한 이벤트 처리기를 추가 합니다. 매개 변수를로 `true` 설정 하 여 이벤트 경로를 따라 다른 요소에 의해 이미 처리 된 것으로 표시 된 라우트된 이벤트에 대해 지정 된 처리기를 호출 합니다. `handledEventsToo`

> [!TIP]
> 끌어서 놓기 이벤트의 미리 보기 버전을 처리 하 고 미리 보기 이벤트 <xref:System.Windows.Controls.TextBox>를 <xref:System.Windows.Controls.RichTextBox>처리 된 <xref:System.Windows.Documents.FlowDocument> 것으로 표시 하 여, 및의 기본 제공 끌어서 놓기 기능을 바꿀 수 있습니다. 그러나 기본 제공 끌어서 놓기 기능을 사용 하지 않도록 설정 하므로 권장 되지 않습니다.

## <a name="example"></a>예제

다음 예제에서는의 <xref:System.Windows.DragDrop.DragOver> 및 <xref:System.Windows.DragDrop.Drop> 이벤트 <xref:System.Windows.Controls.RichTextBox>에 대 한 처리기를 추가 하는 방법을 보여 줍니다. 이 예제에서는 메서드 <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 를 사용 하 고 `handledEventsToo` 매개 변수 `true` 를로 설정 하 여 <xref:System.Windows.Controls.RichTextBox> 이 이벤트를 처리 된 것으로 표시 하는 경우에도 이벤트 처리기가 호출 되도록 합니다. 이벤트 처리기의 코드는에 끌어 놓은 텍스트 파일을 여는 <xref:System.Windows.Controls.RichTextBox>기능을 추가 합니다.

이 예를 테스트 하려면 Windows 탐색기에서로 <xref:System.Windows.Controls.RichTextBox>텍스트 파일 또는 rtf (서식 있는 텍스트) 파일을 끌어 옵니다. 이 파일은에서 <xref:System.Windows.Controls.RichTextBox>열립니다. 파일을 삭제 하기 전에 SHIFT 키를 누르면 파일이 일반 텍스트로 열립니다.

[!code-xaml[DragDropSnippets#RtbXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml#rtbxaml)]

[!code-csharp[DragDropSnippets#RtbHandlers](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#rtbhandlers)]
[!code-vb[DragDropSnippets#RtbHandlers](~/samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#rtbhandlers)]
