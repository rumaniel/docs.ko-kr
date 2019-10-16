---
title: '방법: Inlines 속성을 통해 유동 콘텐츠 요소 조작'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- flow content elements [WPF], manipulating through Inlines property
- documents [WPF], manipulating flow Content elements through Inlines property
- Inlines property [WPF], manipulating flow Content elements
- properties [WPF], Inlines [WPF], manipulating flow Content elements
ms.assetid: 510780d2-3da1-4360-8763-7054bda22ea3
ms.openlocfilehash: 92f23fbf44464eb7658f3382f873f3db63f7cb26
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614574"
---
# <a name="how-to-manipulate-flow-content-elements-through-the-inlines-property"></a>방법: Inlines 속성을 통해 유동 콘텐츠 요소 조작
이러한 예제는 인라인 유동 콘텐츠 요소에서 수행할 수 있는 보다 일반적인 작업 중 일부를 보여 (및 이러한 요소는 컨테이너와 같은 <xref:System.Windows.Controls.TextBlock>)를 통해 합니다 **인라인** 속성입니다. 이 속성에서 항목 추가 및 제거 하는 <xref:System.Windows.Documents.InlineCollection>합니다. 유동 콘텐츠 요소는 **인라인** 속성을 포함 합니다.  
  
- <xref:System.Windows.Documents.Bold>  
  
- <xref:System.Windows.Documents.Hyperlink>  
  
- <xref:System.Windows.Documents.Italic>  
  
- <xref:System.Windows.Documents.Paragraph>  
  
- <xref:System.Windows.Documents.Span>  
  
- <xref:System.Windows.Documents.Underline>  
  
 이러한 예제를 사용 하 여 발생할 <xref:System.Windows.Documents.Span> 흐름 콘텐츠 요소 이지만 이러한 기술에 적용할 수 있는 모든 요소나 컨트롤을 호스팅하는 <xref:System.Windows.Documents.InlineCollection> 컬렉션입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 새 <xref:System.Windows.Documents.Span> 개체를 사용 하 여 다음을 **추가** 두 텍스트를 추가 하는 방법의 콘텐츠 자식으로 실행 되는 <xref:System.Windows.Documents.Span>합니다.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesAdd](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesadd)]
 [!code-vb[SpanSnippets#_SpanInlinesAdd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesadd)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 새 <xref:System.Windows.Documents.Run> 요소 부분에 삽입 하는 <xref:System.Windows.Documents.Span>합니다.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesInsert](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesinsert)]
 [!code-vb[SpanSnippets#_SpanInlinesInsert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesinsert)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 최상위 개수를 가져옵니다 <xref:System.Windows.Documents.Inline> 에 포함 된 요소는 <xref:System.Windows.Documents.Span>합니다.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesCount](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinescount)]
 [!code-vb[SpanSnippets#_SpanInlinesCount](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinescount)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 마지막 삭제 <xref:System.Windows.Documents.Inline> 요소에는 <xref:System.Windows.Documents.Span>합니다.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesremovelast)]
 [!code-vb[SpanSnippets#_SpanInlinesRemoveLast](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesremovelast)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 모든 콘텐츠를 지웁니다 (<xref:System.Windows.Documents.Inline> 요소)에서 <xref:System.Windows.Documents.Span>합니다.  
  
 [!code-csharp[SpanSnippets#_SpanInlinesClear](~/samples/snippets/csharp/VS_Snippets_Wpf/SpanSnippets/CSharp/Window1.xaml.cs#_spaninlinesclear)]
 [!code-vb[SpanSnippets#_SpanInlinesClear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SpanSnippets/visualbasic/window1.xaml.vb#_spaninlinesclear)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Documents.BlockCollection>
- <xref:System.Windows.Documents.InlineCollection>
- <xref:System.Windows.Documents.ListItemCollection>
- [유동 문서 개요](flow-document-overview.md)
- [Blocks 속성을 통한 FlowDocument 조작](how-to-manipulate-a-flowdocument-through-the-blocks-property.md)
- [Columns 속성을 통해 테이블의 열 조작](how-to-manipulate-table-columns-through-the-columns-property.md)
- [RowGroups 속성을 통한 테이블의 행 그룹 조작](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
