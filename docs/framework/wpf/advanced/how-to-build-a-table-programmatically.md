---
title: '방법: 프로그래밍 방식으로 테이블 작성'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tables [WPF], creating programmatically
ms.assetid: e3ca88f3-6e94-4b61-82fc-42104c10b761
ms.openlocfilehash: 9c9061d3c4d6b3de5e1ab42a6b98c20813835ba8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964153"
---
# <a name="how-to-build-a-table-programmatically"></a>방법: 프로그래밍 방식으로 테이블 작성
다음 예제에서는 프로그래밍 방식으로를 <xref:System.Windows.Documents.Table> 만들어 콘텐츠로 채우는 방법을 보여 줍니다. 테이블의 내용은 개체 <xref:System.Windows.Documents.TableRow> <xref:System.Windows.Documents.Table.RowGroups%2A> 에 포함 된 개체로 표현 되는 5 개의 행과 <xref:System.Windows.Documents.TableColumn> 6 개의 열 (개체로 표시 됨)으로 할당 됩니다. 행은 전체 테이블의 제목을 지정하는 제목 행, 테이블의 데이터 열을 설명하는 헤더 행 및 요약 정보가 포함된 바닥글 행 등의 여러 다른 프레젠테이션 용도로 사용됩니다.  “제목”, “헤더” 및 “바닥글” 행의 개념은 테이블에 고유한 것이 아니며, 여러 다른 특성이 있는 행일 뿐입니다. 표 셀에는 텍스트, 이미지 또는 거의 모든 기타 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 요소로 구성 될 수 있는 실제 내용이 포함 되어 있습니다.  
  
## <a name="example"></a>예제  
 먼저를 <xref:System.Windows.Documents.Table> 호스트 하기 위해가 만들어지고 새가 <xref:System.Windows.Documents.FlowDocument>만들어져의 내용에 추가 됩니다. <xref:System.Windows.Documents.Table> <xref:System.Windows.Documents.FlowDocument>  
  
 [!code-csharp[TableSnippets#_TableCreate](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreate)]
 [!code-vb[TableSnippets#_TableCreate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreate)]  
  
## <a name="example"></a>예제  
 다음으로, <xref:System.Windows.Documents.TableColumn> 일부 서식이 적용 된 테이블의 <xref:System.Windows.Documents.Table.Columns%2A> 컬렉션에 6 개의 개체가 만들어지고 추가 됩니다.  
  
> [!NOTE]
> 테이블의 <xref:System.Windows.Documents.Table.Columns%2A> 컬렉션은 0부터 시작 하는 표준 인덱스를 사용 합니다.  
  
 [!code-csharp[TableSnippets#_TableCreateColumns](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreatecolumns)]
 [!code-vb[TableSnippets#_TableCreateColumns](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreatecolumns)]  
  
## <a name="example"></a>예제  
 다음으로 제목 행을 만들어 서식이 적용된 테이블에 추가합니다.  제목 행은 테이블의 6개 열에 모두 걸친 단일 셀을 포함하게 됩니다.  
  
 [!code-csharp[TableSnippets#_TableAddTitleRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddtitlerow)]
 [!code-vb[TableSnippets#_TableAddTitleRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddtitlerow)]  
  
## <a name="example"></a>예제  
 다음으로 헤더 행을 만들어 테이블에 추가하고, 헤더 행의 셀을 만들어 콘텐츠로 채웁니다.  
  
 [!code-csharp[TableSnippets#_TableAddHeaderRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddheaderrow)]
 [!code-vb[TableSnippets#_TableAddHeaderRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddheaderrow)]  
  
## <a name="example"></a>예제  
 다음으로 데이터 행을 만들어 테이블에 추가하고, 이 행의 셀을 만들어 콘텐츠로 채웁니다.  이 행을 작성하는 것은 헤더 행을 작성하는 것과 비슷합니다. 단, 약간 다른 서식이 지정됩니다.  
  
 [!code-csharp[TableSnippets#_TableAddDataRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableadddatarow)]
 [!code-vb[TableSnippets#_TableAddDataRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableadddatarow)]  
  
## <a name="example"></a>예제  
 마지막으로 바닥글 행을 만들어 추가하고 서식을 지정합니다.  제목 행과 마찬가지로 바닥글에는 테이블의 6개 열에 모두 걸친 단일 셀이 포함됩니다.  
  
 [!code-csharp[TableSnippets#_TableAddFooterRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddfooterrow)]
 [!code-vb[TableSnippets#_TableAddFooterRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddfooterrow)]  
  
## <a name="see-also"></a>참고자료

- [테이블 개요](table-overview.md)
