---
title: '방법: Blocks 속성을 통해 유동 콘텐츠 요소 조작'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- documents [WPF], manipulating flow content elements through Blocks property
- flow content elements [WPF], manipulating through Blocks property
- properties [WPF], Blocks [WPF], manipulating flow content elements
- Blocks property [WPF], manipulating flow content elements
ms.assetid: aeda4ece-b979-4818-a093-ef938e908751
ms.openlocfilehash: 3ca05590bd1adf7f9c486382a08cb334b4731ac9
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614611"
---
# <a name="how-to-manipulate-flow-content-elements-through-the-blocks-property"></a>방법: Blocks 속성을 통해 유동 콘텐츠 요소 조작
이러한 예제를 보여 줍니다을 통한 유동 콘텐츠 요소에서 수행할 수 있는 보다 일반적인 작업 중 일부는 **블록** 속성입니다. 이 속성에서 항목 추가 및 제거 하는 <xref:System.Windows.Documents.BlockCollection>합니다. 유동 콘텐츠 요소를 **블록** 속성을 포함 합니다.  
  
- <xref:System.Windows.Documents.Figure>  
  
- <xref:System.Windows.Documents.Floater>  
  
- <xref:System.Windows.Documents.ListItem>  
  
- <xref:System.Windows.Documents.Section>  
  
- <xref:System.Windows.Documents.TableCell>  
  
 이 예제에서 사용 하 여 오류가 발생 <xref:System.Windows.Documents.Section> 흐름 콘텐츠 요소 하지만 이러한 방법은 유동 콘텐츠 요소 컬렉션을 호스트 하는 모든 요소에 적용 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 새 <xref:System.Windows.Documents.Section> 를 사용 하 여는 **추가** 새 단락을 추가 하는 방법의 **섹션** 콘텐츠입니다.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksAdd](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksadd)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksAdd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksadd)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 새 <xref:System.Windows.Documents.Paragraph> 요소 부분에 삽입 하는 <xref:System.Windows.Documents.Section>합니다.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksInsert](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksinsert)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksInsert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksinsert)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 최상위 개수를 가져옵니다 <xref:System.Windows.Documents.Block> 에 포함 된 요소는 <xref:System.Windows.Documents.Section>합니다.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksCount](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblockscount)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksCount](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblockscount)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 마지막 삭제 <xref:System.Windows.Documents.Block> 요소에는 <xref:System.Windows.Documents.Section>합니다.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksRemoveLast](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksremovelast)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksRemoveLast](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksremovelast)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 모든 콘텐츠를 지웁니다 (<xref:System.Windows.Documents.Block> 요소)에서 <xref:System.Windows.Documents.Section>합니다.  
  
 [!code-csharp[FlowDocumentSnippets#_SectionBlocksClear](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml.cs#_sectionblocksclear)]
 [!code-vb[FlowDocumentSnippets#_SectionBlocksClear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentSnippets/visualbasic/window1.xaml.vb#_sectionblocksclear)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Documents.BlockCollection>
- <xref:System.Windows.Documents.InlineCollection>
- <xref:System.Windows.Documents.ListItemCollection>
- [유동 문서 개요](flow-document-overview.md)
- [RowGroups 속성을 통한 테이블의 행 그룹 조작](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
- [Columns 속성을 통해 테이블의 열 조작](how-to-manipulate-table-columns-through-the-columns-property.md)
- [RowGroups 속성을 통한 테이블의 행 그룹 조작](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
