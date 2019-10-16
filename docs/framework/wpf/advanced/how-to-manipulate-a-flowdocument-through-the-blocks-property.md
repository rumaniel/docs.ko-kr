---
title: '방법: Blocks 속성을 통해 FlowDocument 조작'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 'documents [WPF], manipulating FlowDocuments through Blocks property [WPF], , '
- ', '
ms.assetid: cbb7291e-3f1b-433e-9e16-f4d93ced14e8
ms.openlocfilehash: c307d85bf24e2d8a20226856181e0758758d40c0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051509"
---
# <a name="how-to-manipulate-a-flowdocument-through-the-blocks-property"></a>방법: Blocks 속성을 통해 FlowDocument 조작
이 예제에서 수행할 수 있는 보다 일반적인 작업 중 일부를 보여를 <xref:System.Windows.Documents.FlowDocument> 를 통해를 <xref:System.Windows.Documents.FlowDocument.Blocks%2A> 속성입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 새 <xref:System.Windows.Documents.FlowDocument> 한 다음 새를 추가 <xref:System.Windows.Documents.Paragraph> 요소는 <xref:System.Windows.Documents.FlowDocument>합니다.  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksAdd](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblocksadd)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksAdd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblocksadd)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 새 <xref:System.Windows.Documents.Paragraph> 요소 부분에 삽입 하는 <xref:System.Windows.Documents.FlowDocument>합니다.  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksInsert](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblocksinsert)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksInsert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblocksinsert)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 최상위 개수를 가져옵니다 <xref:System.Windows.Documents.Block> 에 포함 된 요소는 <xref:System.Windows.Documents.FlowDocument>합니다.  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksCount](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblockscount)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksCount](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblockscount)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 마지막 삭제 <xref:System.Windows.Documents.Block> 요소에는 <xref:System.Windows.Documents.FlowDocument>합니다.  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksRemoveLast](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblocksremovelast)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksRemoveLast](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblocksremovelast)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 모든 콘텐츠를 지웁니다 (<xref:System.Windows.Documents.Block> 요소)에서 <xref:System.Windows.Documents.FlowDocument>합니다.  
  
 [!code-csharp[FlowDocumentSnippets#_FlowDocumentBlocksClear](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_flowdocumentblocksclear)]
 [!code-vb[FlowDocumentSnippets#_FlowDocumentBlocksClear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_flowdocumentblocksclear)]  
  
## <a name="see-also"></a>참고자료

- [RowGroups 속성을 통한 테이블의 행 그룹 조작](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
- [Columns 속성을 통해 테이블의 열 조작](how-to-manipulate-table-columns-through-the-columns-property.md)
- [RowGroups 속성을 통한 테이블의 행 그룹 조작](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
