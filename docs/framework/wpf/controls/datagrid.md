---
title: DataGrid
ms.date: 03/30/2017
helpviewer_keywords:
- DataGrid column types [WPF]
- DataGrid scenarios [WPF]
- DataGrid control [WPF]
- controls [WPF], DataGrid
- DataGrid [WPF], common tasks for
- DataGrid [WPF], customizing the appearance of
- DataGrid columns [WPF], using
ms.assetid: bf89ea63-79b6-422b-bc9f-0485ad803216
ms.openlocfilehash: dda712d58a4ff956de074ecd416402ba0aece5f4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61912238"
---
# <a name="datagrid"></a>DataGrid
<xref:System.Windows.Controls.DataGrid> 컨트롤 표시 하 고 SQL database, LINQ 쿼리 또는 다른 바인딩 가능한 데이터 원본에서와 같은 다양 한 원본의 데이터를 편집할 수 있습니다. 자세한 내용은 [바인딩 소스 개요](../data/binding-sources-overview.md)를 참조하세요.  
  
 열과 같은 텍스트 컨트롤을 표시할 수 있습니다는 <xref:System.Windows.Controls.ComboBox>, 또는 템플릿에 포함 된 콘텐츠 이미지, 단추 등의 기타 WPF 콘텐츠가 있습니다. 사용할 수는 <xref:System.Windows.Controls.DataGridTemplateColumn> 템플릿에 정의 된 데이터를 표시 합니다. 다음 표에서 기본적으로 제공 되는 열 유형을 나열 합니다.  
  
|생성 된 열 형식|데이터 형식|  
|---------------------------|---------------|  
|<xref:System.Windows.Controls.DataGridTextColumn>|<xref:System.String>|  
|<xref:System.Windows.Controls.DataGridCheckBoxColumn>|<xref:System.Boolean>|  
|<xref:System.Windows.Controls.DataGridComboBoxColumn>|<xref:System.Enum>|  
|<xref:System.Windows.Controls.DataGridHyperlinkColumn>|<xref:System.Uri>|  
  
 <xref:System.Windows.Controls.DataGrid> 셀의 글꼴, 색 및 크기와 같은 모양이 사용자 지정할 수 있습니다. <xref:System.Windows.Controls.DataGrid> 다른 WPF 컨트롤의 스타일 지정 및 템플릿 기능을 모두 지원합니다. <xref:System.Windows.Controls.DataGrid> 기본 및 편집, 정렬 및 유효성 검사에 대 한 사용자 지정 가능한 동작에도 포함 됩니다.  
  
 다음 표에서 대 한 일반적인 작업 중 일부 <xref:System.Windows.Controls.DataGrid> 및 작업을 수행 하는 방법입니다. 관련된 된 API를 확인 하 여 자세한 내용 및 샘플 코드를 찾을 수 있습니다.  
  
|시나리오|방식|  
|--------------|--------------|  
|교대로 반복 되는 배경색|설정를 <xref:System.Windows.Controls.ItemsControl.AlternationIndex%2A> 속성을 2 이상 할당을 <xref:System.Windows.Media.Brush> 에 <xref:System.Windows.Controls.DataGrid.RowBackground%2A> 및 <xref:System.Windows.Controls.DataGrid.AlternatingRowBackground%2A> 속성.|  
|셀 및 행 선택 동작을 정의 합니다.|<xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 및 <xref:System.Windows.Controls.DataGrid.SelectionUnit%2A> 속성을 설정합니다.|  
|헤더, 셀 및 행의 시각적 모양을 사용자 지정|새 적용 <xref:System.Windows.Style> 에 <xref:System.Windows.Controls.DataGrid.ColumnHeaderStyle%2A>를 <xref:System.Windows.Controls.DataGrid.RowHeaderStyle%2A>를 <xref:System.Windows.Controls.DataGrid.CellStyle%2A>, 또는 <xref:System.Windows.Controls.DataGrid.RowStyle%2A> 속성입니다.|  
|크기 조정 옵션 설정|설정 합니다 <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.MaxHeight%2A>, <xref:System.Windows.FrameworkElement.MinHeight%2A>, <xref:System.Windows.FrameworkElement.Width%2A>를 <xref:System.Windows.FrameworkElement.MaxWidth%2A>, 또는 <xref:System.Windows.FrameworkElement.MinWidth%2A> 속성입니다. 자세한 내용은 [DataGrid 컨트롤의 크기 조정 옵션](sizing-options-in-the-datagrid-control.md)합니다.|  
|선택한 항목에 액세스|확인 합니다 <xref:System.Windows.Controls.DataGrid.SelectedCells%2A> 선택한 셀을 가져올 속성 및 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems%2A> 선택한 행을 가져올 속성입니다. 자세한 내용은 <xref:System.Windows.Controls.DataGrid.SelectedCells%2A>을 참조하세요.|  
|최종 사용자 상호 작용을 사용자 지정|설정 합니다 <xref:System.Windows.Controls.DataGrid.CanUserAddRows%2A>, <xref:System.Windows.Controls.DataGrid.CanUserDeleteRows%2A>, <xref:System.Windows.Controls.DataGrid.CanUserReorderColumns%2A>, <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A>를 <xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A>, 및 <xref:System.Windows.Controls.DataGrid.CanUserSortColumns%2A> 속성입니다.|  
|취소 또는 자동으로 생성 된 열 변경|처리는 <xref:System.Windows.Controls.DataGrid.AutoGeneratingColumn> 이벤트입니다.|  
|열 고정|설정 된 <xref:System.Windows.Controls.DataGrid.FrozenColumnCount%2A> 속성을 1로 설정 하 여 맨 왼쪽 위치로 이동 열은 <xref:System.Windows.Controls.DataGridColumn.DisplayIndex%2A> 속성을 0입니다.|  
|데이터 원본으로 사용 하 여 XML 데이터|바인딩하는 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 에 <xref:System.Windows.Controls.DataGrid> 항목의 컬렉션을 나타내는 XPath 쿼리를 합니다. 각 열을 만들기는 <xref:System.Windows.Controls.DataGrid>합니다. XPath 쿼리 항목 소스에서 속성을 가져옵니다를 바인딩할을 설정 하 여 각 열을 바인딩하십시오. 예제를 보려면 <xref:System.Windows.Controls.DataGridTextColumn>를 참조하십시오.|  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[연습: DataGrid 컨트롤에는 SQL Server 데이터베이스에서 데이터를 표시 합니다.](walkthrough-display-data-from-a-sql-server-database-in-a-datagrid-control.md)|엔터티 프레임 워크 요소를 추가할 새 WPF 프로젝트를 설정, 소스를 설정 및 데이터를 표시 하는 방법을 설명는 <xref:System.Windows.Controls.DataGrid>합니다.|  
|[방법: DataGrid 컨트롤에 행 세부 정보 추가](how-to-add-row-details-to-a-datagrid-control.md)|행 세부 정보를 만드는 방법에 설명 된 <xref:System.Windows.Controls.DataGrid>합니다.|  
|[방법: DataGrid 컨트롤을 사용 하 여 유효성 검사 구현](how-to-implement-validation-with-the-datagrid-control.md)|값의 유효성을 검사 하는 방법에 설명 <xref:System.Windows.Controls.DataGrid> 셀 및 행 및 유효성 검사 피드백을 표시 합니다.|  
|[DataGrid 컨트롤에서의 기본 키보드 및 마우스 동작](default-keyboard-and-mouse-behavior-in-the-datagrid-control.md)|상호 작용 하는 방법에 설명 합니다 <xref:System.Windows.Controls.DataGrid> 키보드 및 마우스를 사용 하 여 제어 합니다.|  
|[방법: 그룹, 정렬 및 DataGrid 컨트롤에서 데이터 필터링](how-to-group-sort-and-filter-data-in-the-datagrid-control.md)|데이터를 보는 방법에 설명 합니다.는 <xref:System.Windows.Controls.DataGrid> 그룹화, 정렬 및 데이터를 필터링 하 여 다양 한 방식에서입니다.|  
|[DataGrid 컨트롤의 크기 조정 옵션](sizing-options-in-the-datagrid-control.md)|절대 및 자동 크기 조정 제어 하는 방법에 설명 합니다 <xref:System.Windows.Controls.DataGrid>합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.DataGrid>
- [스타일 지정 및 템플릿](styling-and-templating.md)
- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [데이터 템플릿 개요](../data/data-templating-overview.md)
- [컨트롤](index.md)
- [WPF 콘텐츠 모델](wpf-content-model.md)
