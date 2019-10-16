---
title: TextElement 콘텐츠 모델 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- documents [WPF], flow documents
- TextElement content model [WPF]
- flow content elements [WPF], TextElement content model
ms.assetid: d0a7791c-b090-438c-812f-b9d009d83ee9
ms.openlocfilehash: 21df7228f8dca884c5f36be23ae1aced7b31cc9a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69942210"
---
# <a name="textelement-content-model-overview"></a>TextElement 콘텐츠 모델 개요
이 콘텐츠 모델 개요에서는에 대해 <xref:System.Windows.Documents.TextElement>지원 되는 콘텐츠를 설명 합니다. 클래스는의 <xref:System.Windows.Documents.TextElement>형식입니다. <xref:System.Windows.Documents.Paragraph> 콘텐츠 모델은 어떤 개체/요소가 다른 개체/요소에 포함될 수 있는지를 설명합니다. 이 개요에서는에서 <xref:System.Windows.Documents.TextElement>파생 된 개체에 사용 되는 콘텐츠 모델을 요약 합니다. 자세한 내용은 [유동 문서 개요](flow-document-overview.md)를 참조 하세요.  

<a name="text_element_classes"></a>   
## <a name="content-model-diagram"></a>콘텐츠 모델 다이어그램  
 다음 다이어그램에서는에서 <xref:System.Windows.Documents.TextElement> 파생 된 클래스에 대 한 콘텐츠 모델과 다른 `TextElement` 비 클래스를이 모델에 맞추는 방법에 대해 간략하게 설명 합니다.  
  
 ![다이어그램: 유동 콘텐츠 포함 스키마](./media/flow-content-schema.png "Flow_Content_Schema")  
  
 위의 다이어그램에서 볼 수 있듯이 요소에 대해 허용 되는 자식은 클래스가 <xref:System.Windows.Documents.Block> 클래스에서 파생 되었는지 <xref:System.Windows.Documents.Inline> 아니면 클래스에서 파생 되는지에 따라 결정 되지 않을 수도 있습니다. 예를 들어 <xref:System.Windows.Documents.Inline>( <xref:System.Windows.Documents.Span> 파생 클래스)에는 <xref:System.Windows.Documents.Inline>자식 요소만 있을 <xref:System.Windows.Documents.Inline> 수 있지만 (파생 클래스) <xref:System.Windows.Documents.Figure> 에는 자식 요소만 있을 <xref:System.Windows.Documents.Block> 수 있습니다. 그러므로 이 다이어그램은 다른 요소에 포함될 수 있는 요소를 신속하게 판별하는 데 유용합니다. 예를 들어 다이어그램을 사용 하 여의 <xref:System.Windows.Controls.RichTextBox>유동 콘텐츠를 생성 하는 방법을 결정 하겠습니다.  
  
1. 에는가 <xref:System.Windows.Documents.FlowDocument> 포함 <xref:System.Windows.Documents.Block>되어야 하며,이는 차례로 파생 된 개체를 포함 해야 합니다. <xref:System.Windows.Controls.RichTextBox> 이전 다이어그램에 해당하는 세그먼트는 다음과 같습니다.  
  
     ![다이어그램: RichTextBox 포함 규칙](./media/flow-ovw-schemawalkthrough1.png "Flow_Ovw_SchemaWalkThrough1")  
  
     따라서 지금까지 태그는 다음과 같을 수 있습니다.  
  
     [!code-xaml[FlowOvwSnippets_snip#SchemaWalkThrough1](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough1)]  
  
2. 다이어그램에 따라 <xref:System.Windows.Documents.Block> ,, <xref:System.Windows.Documents.Section> <xref:System.Windows.Documents.Table> <xref:System.Windows.Documents.Paragraph>, 및<xref:System.Windows.Documents.List>를 포함 하 여 선택할 수 있는 몇 가지 요소가 있습니다 (위의 다이어그램에서 블록 파생 클래스 참조). <xref:System.Windows.Documents.BlockUIContainer> 을 사용 하려는 경우를 <xref:System.Windows.Documents.Table>가정해 보겠습니다. 위의 다이어그램에 <xref:System.Windows.Documents.Table> 따라에 <xref:System.Windows.Documents.TableRowGroup> 는 파생 개체가 포함 <xref:System.Windows.Documents.Block>된 <xref:System.Windows.Documents.TableRow> 요소가 포함 <xref:System.Windows.Documents.TableCell> 된 포함 요소가 포함 됩니다. 다음은 앞의 다이어그램에서 <xref:System.Windows.Documents.Table> 가져온 해당 세그먼트입니다.  
  
     ![다이어그램: &#47;테이블](./media/flow-ovw-schemawalkthrough2.png "Flow_Ovw_SchemaWalkThrough2") 부모 자식 스키마  
  
     다음은 해당 태그입니다.  
  
     [!code-xaml[FlowOvwSnippets_snip#SchemaWalkThrough2](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/MiscSnippets.xaml#schemawalkthrough2)]  
  
3. 아래에는 <xref:System.Windows.Documents.Block> <xref:System.Windows.Documents.TableCell>하나 이상의 요소가 필요 합니다. 간단하게 셀 안에 텍스트를 배치해 보겠습니다. 요소와 함께를 <xref:System.Windows.Documents.Paragraph> 사용 하 여이 작업을 수행할 수 있습니다. <xref:System.Windows.Documents.Run> 다음 <xref:System.Windows.Documents.Paragraph> 은가 <xref:System.Windows.Documents.Inline> 요소를 사용 하 <xref:System.Windows.Documents.Inline> 고 <xref:System.Windows.Documents.Run> (요소)가 일반 텍스트를 사용할 수 있음을 보여 주는 다이어그램의 해당 세그먼트입니다.  
  
     ![다이어그램: &#47;단락](./media/flow-ovw-schemawalkthrough3.png "Flow_Ovw_SchemaWalkThrough3") 부모 자식 스키마  
  
     ![다이어그램: &#47;](./media/flow-ovw-schemawalkthrough4.png "Flow_Ovw_SchemaWalkThrough4") 실행에 대 한 부모 자식 스키마  
  
 다음은 태그의 전체 예제입니다.  
  
 [!code-xaml[FlowOvwSnippets_snip#SchemaExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowOvwSnippets_snip/CS/SchemaExample.xaml#schemaexamplewholepage)]  
  
<a name="Using_the_Content_Property"></a>   
## <a name="working-with-textelement-content-programmatically"></a>프로그래밍 방식으로 TextElement 콘텐츠 작업  
 의 <xref:System.Windows.Documents.TextElement> 콘텐츠는 컬렉션으로 구성 되므로 개체의 <xref:System.Windows.Documents.TextElement> 콘텐츠를 프로그래밍 방식으로 조작 하는 작업은 이러한 컬렉션을 사용 하 여 수행 됩니다. 파생 클래스에서 <xref:System.Windows.Documents.TextElement> 사용 되는 세 가지 컬렉션이 있습니다.  
  
- <xref:System.Windows.Documents.InlineCollection>: <xref:System.Windows.Documents.Inline> 요소의 컬렉션을 나타냅니다. <xref:System.Windows.Documents.InlineCollection>는 <xref:System.Windows.Documents.Paragraph>, <xref:System.Windows.Documents.Span> 및 <xref:System.Windows.Controls.TextBlock> 요소의 사용할 수 있는 자식 콘텐츠를 정의합니다.  
  
- <xref:System.Windows.Documents.BlockCollection>: <xref:System.Windows.Documents.Block> 요소의 컬렉션을 나타냅니다. <xref:System.Windows.Documents.BlockCollection>은 <xref:System.Windows.Documents.FlowDocument>, <xref:System.Windows.Documents.Section>, <xref:System.Windows.Documents.ListItem>, <xref:System.Windows.Documents.TableCell>, <xref:System.Windows.Documents.Floater> 및 <xref:System.Windows.Documents.Figure> 요소의 사용할 수 있는 자식 콘텐츠를 정의합니다.  
  
- <xref:System.Windows.Documents.ListItemCollection>: 순서가 지정 특정 콘텐츠 항목을 나타내는 유동 콘텐츠 요소 또는 순서가 지정 되지 않은 <xref:System.Windows.Documents.List>합니다.  
  
 **Inlines**, **Blocks**및 **ListItems**의 각 속성을 사용 하 여 이러한 컬렉션에서 항목을 조작 (추가 또는 제거) 할 수 있습니다. 다음 예제에서는 **Inlines** 속성을 사용 하 여 범위의 콘텐츠를 조작 하는 방법을 보여 줍니다.  
  
> [!NOTE]
> 테이블에서는 콘텐츠를 조작하는 데 여러 컬렉션을 사용하지만 이러한 컬렉션은 여기에서 다루지 않습니다. 자세한 내용은 [테이블 개요](table-overview.md)를 참조 하세요.  
  
 다음 예제에서는 새 <xref:System.Windows.Documents.Span> 개체를 만든 다음 `Add` 메서드를 사용 하 여의 콘텐츠 자식 <xref:System.Windows.Documents.Span>으로 두 개의 텍스트 실행을 추가 합니다.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesAdd](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesadd)]
 [!code-vb[SpanSnippets#_SpanInlinesAdd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesadd)]  
  
 다음 예제에서는 새 <xref:System.Windows.Documents.Run> 요소를 만들어 <xref:System.Windows.Documents.Span>의 시작 부분에 삽입 합니다.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesInsert](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesinsert)]
 [!code-vb[SpanSnippets#_SpanInlinesInsert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesinsert)]  
  
 다음 예에서는 <xref:System.Windows.Documents.Inline> <xref:System.Windows.Documents.Span>에서 마지막 요소를 삭제 합니다.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
 [!code-vb[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]  
  
 다음 예제에서는<xref:System.Windows.Documents.Inline> <xref:System.Windows.Documents.Span>에서 모든 콘텐츠 (요소)를 지웁니다.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesClear](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
 [!code-vb[SpanSnippets#_SpanInlinesClear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]  
  
<a name="Types_that_Share_this_Content_Model"></a>   
## <a name="types-that-share-this-content-model"></a>이 콘텐츠 모델을 공유하는 형식  
 다음 형식은 <xref:System.Windows.Documents.TextElement> 클래스에서 상속 되며이 개요에 설명 된 콘텐츠를 표시 하는 데 사용할 수 있습니다.  
  
 <xref:System.Windows.Documents.Bold>, <xref:System.Windows.Documents.Figure>, <xref:System.Windows.Documents.Floater>, <xref:System.Windows.Documents.Hyperlink>, <xref:System.Windows.Documents.InlineUIContainer>, <xref:System.Windows.Documents.Italic>, <xref:System.Windows.Documents.LineBreak>, <xref:System.Windows.Documents.List>, <xref:System.Windows.Documents.ListItem>, <xref:System.Windows.Documents.Paragraph>, <xref:System.Windows.Documents.Run>, <xref:System.Windows.Documents.Section>, <xref:System.Windows.Documents.Span>, <xref:System.Windows.Documents.Table>, <xref:System.Windows.Documents.Underline>.  
  
 이 목록에는 [!INCLUDE[TLA2#tla_winfxsdk](../../../../includes/tla2sharptla-winfxsdk-md.md)]를 사용 하 여 배포 된 비추상 유형만 포함 됩니다. 에서 <xref:System.Windows.Documents.TextElement>상속 되는 다른 형식을 사용할 수 있습니다.  
  
<a name="Types_that_Can_Contain_ContentControl_Objects"></a>   
## <a name="types-that-can-contain-textelement-objects"></a>TextElement 개체를 포함할 수 있는 형식  
 [WPF 콘텐츠 모델](../controls/wpf-content-model.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [Blocks 속성을 통한 FlowDocument 조작](how-to-manipulate-a-flowdocument-through-the-blocks-property.md)
- [Blocks 속성을 통한 유동 콘텐츠 요소 조작](how-to-manipulate-flow-content-elements-through-the-blocks-property.md)
- [Blocks 속성을 통한 FlowDocument 조작](how-to-manipulate-a-flowdocument-through-the-blocks-property.md)
- [Columns 속성을 통해 테이블의 열 조작](how-to-manipulate-table-columns-through-the-columns-property.md)
- [RowGroups 속성을 통한 테이블의 행 그룹 조작](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
