---
title: 테이블 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- flow content elements [WPF], Table
- documents [WPF], tables
- tables [WPF]
ms.assetid: 5e1105f4-8fc4-473a-ba55-88c8e71386e6
ms.openlocfilehash: fa7106207c69f19b647ba80ab7e724e9aad174c1
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005084"
---
# <a name="table-overview"></a>테이블 개요
<xref:System.Windows.Documents.Table>은 유동 문서 콘텐츠의 그리드 기반 프레젠테이션을 지 원하는 블록 수준 요소입니다. 이 요소의 유연성 덕분에 이 요소는 매우 유용하지만 이해하고 제대로 사용하기가 더 복잡합니다.  
  
 이 항목에는 다음 섹션이 수록되어 있습니다.  
  
- [테이블 기본 사항](#table_basics)  
  
- [Table은 Grid와 어떻게 다를까요?](#table_vs_Grid)  
  
- [기본 테이블 구조](#basic_table_structure)  
  
- [테이블 포함](#table_containment)  
  
- [행 그룹](#row_groupings)  
  
- [백그라운드 렌더링 우선 순위](#rendering_precedence)  
  
- [행 및 열 확장](#spanning_rows_or_columns)  
  
- [코드로 테이블 빌드](#building_a_table_with_code)  
  
- [관련 항목] 
  
<a name="table_basics"></a>   
## <a name="table-basics"></a>테이블 기본 사항  
  
<a name="table_vs_Grid"></a>   
### <a name="how-is-table-different-then-grid"></a>Table은 Grid와 어떻게 다를까요?  
 <xref:System.Windows.Documents.Table> 및 <xref:System.Windows.Controls.Grid>은 몇 가지 일반적인 기능을 공유 하지만 각각 서로 다른 시나리오에 가장 적합 합니다. @No__t-0은 유동 콘텐츠 내에서 사용 하도록 설계 되었습니다 (유동 콘텐츠에 대 한 자세한 내용은 [유동 문서 개요](flow-document-overview.md) 참조). 그리드는 폼 내부에서 사용하는 것이 적합합니다(기본적으로 유동 콘텐츠 외부의 모든 위치). @No__t-0에서 <xref:System.Windows.Documents.Table>은 페이지 매김, 열 리플로우 및 내용 선택과 같은 유동 콘텐츠 동작을 지원 하지만 <xref:System.Windows.Controls.Grid>는 그렇지 않습니다. 반면에 <xref:System.Windows.Controls.Grid>은 <xref:System.Windows.Controls.Grid>를 포함 하 여 행 및 열 인덱스를 기반으로 하는 요소를 추가 하는 등의 다양 한 이유로 <xref:System.Windows.Documents.FlowDocument>의 외부에서 가장 잘 사용 되며, <xref:System.Windows.Documents.Table>은 그렇지 않습니다. @No__t-0 요소를 사용 하면 자식 콘텐츠를 계층화 하 여 단일 "셀"에 두 개 이상의 요소가 있을 수 있습니다. <xref:System.Windows.Documents.Table> 레이어를 지원 하지 않습니다. @No__t의 자식 요소는 "셀" 경계 영역을 기준으로 절대적으로 배치 될 수 있습니다. <xref:System.Windows.Documents.Table> 이 기능을 지원 하지 않습니다. 마지막으로 <xref:System.Windows.Controls.Grid>에는 더 낮은 리소스가 필요 합니다. <xref:System.Windows.Documents.Table>은 <xref:System.Windows.Controls.Grid>를 사용 하 여 성능을 향상 시키는 것이 좋습니다.  
  
<a name="basic_table_structure"></a>   
### <a name="basic-table-structure"></a>기본 테이블 구조  
 <xref:System.Windows.Documents.Table>은 열 (@no__t 1 요소로 표시) 및 행 (@no__t 2 요소로 표시 됨)으로 구성 된 그리드 기반 프레젠테이션을 제공 합니다. <xref:System.Windows.Documents.TableColumn> 요소는 콘텐츠를 호스팅하지 않습니다. 열과 특성의 특성을 정의 하기만 하면 됩니다. <xref:System.Windows.Documents.TableRow> 요소는 테이블의 행 그룹을 정의 하는 <xref:System.Windows.Documents.TableRowGroup> 요소에서 호스팅되어야 합니다. 테이블이 제공 하는 실제 콘텐츠를 포함 하는 <xref:System.Windows.Documents.TableCell> 요소는 <xref:System.Windows.Documents.TableRow> 요소에서 호스팅되어야 합니다. <xref:System.Windows.Documents.TableCell>은 <xref:System.Windows.Documents.Block>에서 파생 된 요소만 포함할 수 있습니다.  @No__t-0에 대 한 유효한 자식 요소는입니다.  
  
- <xref:System.Windows.Documents.BlockUIContainer>  
  
- <xref:System.Windows.Documents.List>  
  
- <xref:System.Windows.Documents.Paragraph>  
  
- <xref:System.Windows.Documents.Section>  
  
- <xref:System.Windows.Documents.Table>  
  
> [!NOTE]
> <xref:System.Windows.Documents.TableCell> 요소는 텍스트 콘텐츠를 직접 호스팅할 수 없습니다. @No__t-0과 같은 유동 콘텐츠 요소에 대 한 포함 규칙에 대 한 자세한 내용은 [유동 문서 개요](flow-document-overview.md)를 참조 하세요.  
  
> [!NOTE]
> <xref:System.Windows.Documents.Table> 비슷합니다는 <xref:System.Windows.Controls.Grid> 요소 하지만 더 많은 기능을 큰 리소스 오버 헤드가 필요 합니다.  
  
 다음 예제에서는 XAML을 사용 하 여 간단한 2 x 3 테이블을 정의 합니다.  
  
 [!code-xaml[TableSnippets2#_Table_BasicLayout](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_basiclayout)]  
  
 다음 그림은 이 예제에서 렌더링하는 방법을 보여줍니다.  
  
 ![기본 테이블을 렌더링 하는 방법을 보여 주는 스크린샷](./media/table-overview/basic-table-render-example.png)  
  
<a name="table_containment"></a>   
### <a name="table-containment"></a>테이블 포함  
 <xref:System.Windows.Documents.Table>은 <xref:System.Windows.Documents.Block> 요소에서 파생 되며 @no__t 2 수준 요소에 대 한 일반 규칙을 따릅니다.  <xref:System.Windows.Documents.Table> 다음 요소 중 하나에서 요소를 포함 될 수 있습니다.  
  
- <xref:System.Windows.Documents.FlowDocument>  
  
- <xref:System.Windows.Documents.TableCell>  
  
- <xref:System.Windows.Controls.ListBoxItem>  
  
- <xref:System.Windows.Controls.ListViewItem>  
  
- <xref:System.Windows.Documents.Section>  
  
- <xref:System.Windows.Documents.Floater>  
  
- <xref:System.Windows.Documents.Figure>  
  
<a name="row_groupings"></a>   
### <a name="row-groupings"></a>행 그룹  
 @No__t-0 요소는 테이블 내에서 행을 임의로 그룹화 하는 방법을 제공 합니다. 테이블의 모든 행은 행 그룹에 속해야 합니다.  행 그룹 내의 행은 보통 공통 의도를 공유하고 그룹으로 스타일을 지정할 수 있습니다.  행 그룹은 공통적으로 제목, 헤더 및 바닥글 행과 같은 특수 용도 행을 테이블에 포함된 기본 콘텐츠에서 구분하는 데 사용됩니다.  
  
 다음 예제에서는 XAML을 사용 하 여 스타일이 지정 된 머리글 및 바닥글 행이 있는 테이블을 정의 합니다.  
  
 [!code-xaml[TableSnippets2#_Table_RowGroups](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_rowgroups)]  
  
 다음 그림은 이 예제에서 렌더링하는 방법을 보여줍니다.  
  
 ![Screenshot: 테이블 행 그룹 @ no__t-0(./media/table-rowgroups.png "Table_RowGroups")  
  
<a name="rendering_precedence"></a>   
### <a name="background-rendering-precedence"></a>백그라운드 렌더링 우선 순위  
 테이블 요소는 다음 순서로 렌더링됩니다(최저부터 최고까지 z 순서). 이 순서는 변경할 수 없습니다. 예를 들어 설정된 순서를 재정의하는 데 사용할 수 있는 다음 요소에 대한 "Z 순서" 속성은 없습니다.  
  
1. <xref:System.Windows.Documents.Table>  
  
2. <xref:System.Windows.Documents.TableColumn>  
  
3. <xref:System.Windows.Documents.TableRowGroup>  
  
4. <xref:System.Windows.Documents.TableRow>  
  
5. <xref:System.Windows.Documents.TableCell>  
  
 테이블에서 이러한 각 요소의 배경색을 정의하는 다음 예제를 살펴보겠습니다.  
  
 [!code-xaml[TableSnippets2#_Table_ZOrder](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_zorder)]  
  
 다음 그림은 이 예제가 렌더링되는 방법을 보여 줍니다(배경색만 표시).  
  
 ![Screenshot: 테이블 z&#45;순서 @ no__t-1(./media/table-zorder.png "Table_ZOrder")  
  
<a name="spanning_rows_or_columns"></a>   
### <a name="spanning-rows-or-columns"></a>행 및 열 확장  
 각각 <xref:System.Windows.Documents.TableCell.RowSpan%2A> 또는 <xref:System.Windows.Documents.TableCell.ColumnSpan%2A> 특성을 사용 하 여 여러 행 또는 열에 걸쳐 테이블 셀을 구성할 수 있습니다.  
  
 셀이 세 개의 열에 걸쳐 있는 다음 예제를 살펴보겠습니다.  
  
 [!code-xaml[TableSnippets2#_Table_ColumnSpan](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_columnspan)]  
  
 다음 그림은 이 예제에서 렌더링하는 방법을 보여줍니다.  
  
 ![Screenshot: 3 개의 열을 모두 확장 하는 셀 @ no__t-0(./media/table-columnspan.png "Table_ColumnSpan")  
  
<a name="building_a_table_with_code"></a>   
## <a name="building-a-table-with-code"></a>코드로 테이블 빌드  
 다음 예제에서는 <xref:System.Windows.Documents.Table>을 프로그래밍 방식으로 만들고 콘텐츠로 채우는 방법을 보여 줍니다. 테이블의 내용은 5 개의 행으로 할당 됩니다 (@no__t 1 개체에 포함 된 @no__t 0 개체로 표시 됨), 6 개 열 (<xref:System.Windows.Documents.TableColumn> 개체로 표시 됨). 행은 전체 테이블의 제목을 지정하는 제목 행, 테이블의 데이터 열을 설명하는 헤더 행 및 요약 정보가 포함된 바닥글 행 등의 여러 다른 프레젠테이션 용도로 사용됩니다.  “제목”, “헤더” 및 “바닥글” 행의 개념은 테이블에 고유한 것이 아니며, 여러 다른 특성이 있는 행일 뿐입니다. 표 셀에는 텍스트, 이미지 또는 거의 모든 기타 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 요소로 구성 될 수 있는 실제 내용이 포함 되어 있습니다.  
  
 먼저 <xref:System.Windows.Documents.Table>을 호스팅하기 위해 <xref:System.Windows.Documents.FlowDocument>이 만들어지고 새 <xref:System.Windows.Documents.Table>가 만들어지고 <xref:System.Windows.Documents.FlowDocument>의 내용에 추가 됩니다.  
  
 [!code-csharp[TableSnippets#_TableCreate](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreate)]
 [!code-vb[TableSnippets#_TableCreate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreate)]  
  
 다음으로, 몇 가지 <xref:System.Windows.Documents.TableColumn> 개의 개체가 만들어지고 테이블의 @no__t 1 컬렉션에 추가 되 고 일부 서식이 적용 됩니다.  
  
> [!NOTE]
> 테이블의 @no__t 컬렉션은 0부터 시작 하는 표준 인덱스를 사용 합니다.  
  
 [!code-csharp[TableSnippets#_TableCreateColumns](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreatecolumns)]
 [!code-vb[TableSnippets#_TableCreateColumns](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreatecolumns)]  
  
 다음으로 제목 행을 만들어 서식이 적용된 테이블에 추가합니다.  제목 행은 테이블의 6개 열에 모두 걸친 단일 셀을 포함하게 됩니다.  
  
 [!code-csharp[TableSnippets#_TableAddTitleRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddtitlerow)]
 [!code-vb[TableSnippets#_TableAddTitleRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddtitlerow)]  
  
 다음으로 헤더 행을 만들어 테이블에 추가하고, 헤더 행의 셀을 만들어 콘텐츠로 채웁니다.  
  
 [!code-csharp[TableSnippets#_TableAddHeaderRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddheaderrow)]
 [!code-vb[TableSnippets#_TableAddHeaderRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddheaderrow)]  
  
 다음으로 데이터 행을 만들어 테이블에 추가하고, 이 행의 셀을 만들어 콘텐츠로 채웁니다.  이 행을 작성하는 것은 헤더 행을 작성하는 것과 비슷합니다. 단, 약간 다른 서식이 지정됩니다.  
  
 [!code-csharp[TableSnippets#_TableAddDataRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableadddatarow)]
 [!code-vb[TableSnippets#_TableAddDataRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableadddatarow)]  
  
 마지막으로 바닥글 행을 만들어 추가하고 서식을 지정합니다.  제목 행과 마찬가지로 바닥글에는 테이블의 6개 열에 모두 걸친 단일 셀이 포함됩니다.  
  
 [!code-csharp[TableSnippets#_TableAddFooterRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddfooterrow)]
 [!code-vb[TableSnippets#_TableAddFooterRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddfooterrow)]  
  
## <a name="see-also"></a>참조

- [유동 문서 개요](flow-document-overview.md)
- [XAML로 테이블 정의](how-to-define-a-table-with-xaml.md)
- [WPF의 문서](documents-in-wpf.md)
- [유동 콘텐츠 요소 사용](how-to-use-flow-content-elements.md)
