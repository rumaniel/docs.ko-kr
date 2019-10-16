---
title: '방법: DataGrid 컨트롤에 행 세부 정보 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataTemplate [WPF], DataGrid
- row details [WPF], DataGrid
- DataGrid [WPF], row details
ms.assetid: 0bdc6f50-9b4c-483f-9df6-a47a1fde998b
ms.openlocfilehash: d5b6539f3d379088528b9654861267988b6fc69b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911395"
---
# <a name="how-to-add-row-details-to-a-datagrid-control"></a>방법: DataGrid 컨트롤에 행 세부 정보 추가
사용 하는 경우는 <xref:System.Windows.Controls.DataGrid> 컨트롤을 사용자 지정할 수 있습니다 데이터 프레젠테이션 행 세부 정보 섹션을 추가 합니다. 행 세부 정보 섹션을 추가 하는 필요에 따라 표시 또는 축소 하는 서식 파일의 일부 데이터를 그룹화 할 수 있습니다. 예를 들어, 행 세부 정보를 추가할 수 있습니다는 <xref:System.Windows.Controls.DataGrid> 의 각 행에 대 한 데이터의 요약만을 표시 하는 <xref:System.Windows.Controls.DataGrid>, 행을 선택 하면 더 많은 데이터 필드를 표시 하지만 합니다. 행 세부 정보 섹션의 템플릿을 정의 합니다 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 속성입니다. 다음 그림에서는 행 세부 정보 섹션의 예를 보여 줍니다.  
  
 ![행 세부 정보를 사용 하 여 표시 된 DataGrid](./media/ndp-rowdetails.png "NDP_RowDetails")  
  
 리소스 또는 인라인으로 XAML로 행 세부 정보 템플릿을 정의 합니다. 두 방법 모두 다음 절차에 나와 있습니다. 리소스로 추가 되는 데이터 템플릿은 다시 서식 파일을 만들지 않고 프로젝트 전체에서 사용할 수 있습니다. 인라인 XAML 컨트롤에서 액세스할 수만 정의 된 대로 추가 되는 데이터 템플릿.  
  
### <a name="to-display-row-details-by-using-inline-xaml"></a>인라인 XAML을 사용 하 여 행 정보를 표시 하려면  
  
1. 만들기는 <xref:System.Windows.Controls.DataGrid> 데이터 원본에서 데이터를 표시 하는 합니다.  
  
2. <xref:System.Windows.Controls.DataGrid> 요소에서 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 요소를 추가합니다.  
  
3. 만들기는 <xref:System.Windows.DataTemplate> 행 세부 정보 섹션의 모양을 정의 합니다.  
  
     다음 XAML은 <xref:System.Windows.Controls.DataGrid> 정의 하는 방법과 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 인라인 합니다. <xref:System.Windows.Controls.DataGrid> 표시 3 값 3 각 행에 더 많은 값 행을 선택 합니다.  
  
     [!code-xaml[DataGrid_RowDetails#1](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml#1)]  
  
     다음 코드에 표시 되는 데이터를 선택 하는 데 사용 되는 쿼리를 보여 줍니다.는 <xref:System.Windows.Controls.DataGrid>합니다. 이 예에서 쿼리는 고객 정보가 포함 된 엔터티에서 데이터를 선택 합니다.  
  
     [!code-csharp[DataGrid_RowDetails#2](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml.cs#2)]
     [!code-vb[DataGrid_RowDetails#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_rowdetails/vb/mainwindow.xaml.vb#2)]  
  
### <a name="to-display-row-details-by-using-a-resource"></a>리소스를 사용 하 여 행 정보를 표시 하려면  
  
1. 만들기는 <xref:System.Windows.Controls.DataGrid> 데이터 원본에서 데이터를 표시 하는 합니다.  
  
2. 추가 <xref:System.Windows.FrameworkElement.Resources%2A> 루트 요소에 요소와 같은 <xref:System.Windows.Window> 컨트롤 또는 <xref:System.Windows.Controls.Page> , 제어 하거나 추가 <xref:System.Windows.Application.Resources%2A> 요소를는 <xref:System.Windows.Application> App.xaml (또는 Application.xaml) 파일에서 클래스.  
  
3. 리소스 요소를 만듭니다를 <xref:System.Windows.DataTemplate> 행 세부 정보 섹션의 모양을 정의 합니다.  
  
     다음 XAML은 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 에 정의 된는 <xref:System.Windows.Application> 클래스입니다.  
  
     [!code-xaml[DataGrid_RowDetails#3](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/app.xaml#3)]  
  
4. 에 <xref:System.Windows.DataTemplate>설정 합니다 [X:key 지시문](../../xaml-services/x-key-directive.md) 데이터 서식 파일을 고유 하 게 식별 하는 값을 합니다.  
  
5. 에 <xref:System.Windows.Controls.DataGrid> 요소를 설정 합니다 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 이전 단계에서 정의한 리소스 속성입니다. 정적 리소스와 리소스를 할당 합니다.  
  
     에서는 다음 XAML <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 앞의 예제에서 리소스에 설정 된 속성입니다.  
  
     [!code-xaml[DataGrid_RowDetails#4](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/window2.xaml#4)]  
  
### <a name="to-set-visibility-and-prevent-horizontal-scrolling-for-row-details"></a>표시 유형을 설정 하 고 행 세부 정보에 대 한 가로 스크롤을 방지 하려면  
  
1. 필요한 경우 설정 합니다 <xref:System.Windows.Controls.DataGrid.RowDetailsVisibilityMode%2A> 속성을 <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode> 값입니다.  
  
     기본적으로 값 설정할지 <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.VisibleWhenSelected>합니다. 설정할 수 있습니다 <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.Visible> 의 모든 행에 대 한 세부 정보를 표시 하거나 <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.Collapsed> 모든 행에 대 한 세부 정보를 숨기려면 합니다.  
  
2. 필요한 경우 설정 합니다 <xref:System.Windows.Controls.DataGrid.AreRowDetailsFrozen%2A> 속성을 `true` 행을 방지 하기 위해 가로로 스크롤할 섹션에 자세히 설명 합니다.
