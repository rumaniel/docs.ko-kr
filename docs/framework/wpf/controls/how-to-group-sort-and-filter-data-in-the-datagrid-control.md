---
title: '방법: 그룹, 정렬 및 DataGrid 컨트롤에서 데이터를 필터링 합니다.'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], sort
- DataGrid [WPF], group
- DataGrid [WPF], filter
ms.assetid: 03345e85-89e3-4aec-9ed0-3b80759df770
ms.openlocfilehash: 81fdb0a6d5602f612c55d7e790ca9a0fe56c144e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61771095"
---
# <a name="how-to-group-sort-and-filter-data-in-the-datagrid-control"></a>방법: 그룹, 정렬 및 DataGrid 컨트롤에서 데이터 필터링

데이터를 보는 데 유용할 것을 <xref:System.Windows.Controls.DataGrid> 그룹화, 정렬 및 데이터를 필터링 하 여 다양 한 방식에서입니다. 그룹, 정렬 및 데이터를 필터링 하는 <xref:System.Windows.Controls.DataGrid>에 바인딩합니다는 <xref:System.Windows.Data.CollectionView> 이러한 함수를 지 원하는 합니다. 데이터로 작업할 수 있습니다는 <xref:System.Windows.Data.CollectionView> 원본 데이터를 영향을 주지 않고 합니다. 컬렉션 보기에 변경 내용이 반영 된 <xref:System.Windows.Controls.DataGrid> 사용자 인터페이스 (UI).

합니다 <xref:System.Windows.Data.CollectionView> 그룹화 및 정렬 기능을 구현 하는 데이터 원본에 대 한 클래스를 제공 합니다 <xref:System.Collections.IEnumerable> 인터페이스입니다. 합니다 <xref:System.Windows.Data.CollectionViewSource> 클래스의 속성을 설정할 수 있습니다는 <xref:System.Windows.Data.CollectionView> XAML에서.

이 예의 컬렉션인 `Task` 개체에 바인딩되는 <xref:System.Windows.Data.CollectionViewSource>. <xref:System.Windows.Data.CollectionViewSource> 으로 사용 되는 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 에 대 한는 <xref:System.Windows.Controls.DataGrid>합니다. 그룹화, 정렬 및 필터링에 수행 되는 <xref:System.Windows.Data.CollectionViewSource> 에 표시 됩니다는 <xref:System.Windows.Controls.DataGrid> UI입니다.

![DataGrid의 데이터 그룹화](././media/wpf-datagridgroups.png "WPF_DataGridGroups") DataGrid의 데이터를 그룹화 합니다.

## <a name="using-a-collectionviewsource-as-an-itemssource"></a>ItemsSource collectionviewsource에 바인딩하면 사용 하 여

그룹, 정렬 및 데이터를 필터링 하는 <xref:System.Windows.Controls.DataGrid> 바인딩할 컨트롤을 <xref:System.Windows.Controls.DataGrid> 에 <xref:System.Windows.Data.CollectionView> 이러한 함수를 지 원하는. 이 예제에서는 합니다 <xref:System.Windows.Controls.DataGrid> 바인딩되는 <xref:System.Windows.Data.CollectionViewSource> 에 대 한 이러한 함수를 제공 하는 <xref:System.Collections.Generic.List%601> 의 `Task` 개체입니다.

### <a name="to-bind-a-datagrid-to-a-collectionviewsource"></a>Collectionviewsource에 바인딩하면 DataGrid를 바인딩하려면

1. 구현 하는 데이터 컬렉션을 만들기는 <xref:System.Collections.IEnumerable> 인터페이스입니다.

    사용 하는 경우 <xref:System.Collections.Generic.List%601> 컬렉션을 만들려면에서 상속 되는 새 클래스를 만들어야 <xref:System.Collections.Generic.List%601> 의 인스턴스를 인스턴스화하는 대신 <xref:System.Collections.Generic.List%601>합니다. XAML의 컬렉션에 데이터 바인딩할 수 있습니다.

    > [!NOTE]
    > 컬렉션의 개체를 구현 해야 합니다는 <xref:System.ComponentModel.INotifyPropertyChanged> 변경 된 인터페이스 및 <xref:System.ComponentModel.IEditableObject> 되려면에서 인터페이스는 <xref:System.Windows.Controls.DataGrid> 속성 변경 및 편집에 올바르게 응답할 합니다. 자세한 내용은 [속성 변경 알림 구현](../data/how-to-implement-property-change-notification.md)을 참조하세요.

    [!code-csharp[DataGrid_GroupSortFilter#101](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#101)]
    [!code-vb[DataGrid_GroupSortFilter#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#101)]

2. XAML, 컬렉션 클래스의 인스턴스를 만들에 설정 된 [X:key 지시문](../../xaml-services/x-key-directive.md)합니다.

3. XAML의 인스턴스를 만들고 합니다 <xref:System.Windows.Data.CollectionViewSource> 클래스에서 [X:key 지시문](../../xaml-services/x-key-directive.md),으로 컬렉션 클래스의 인스턴스를 설정 하 고는 <xref:System.Windows.Data.CollectionViewSource.Source%2A>.

    [!code-xaml[DataGrid_GroupSortFilter#201](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/WindowSnips1.xaml#201)]

4. 인스턴스를 만듭니다는 <xref:System.Windows.Controls.DataGrid> 클래스를 설정 합니다 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 속성을는 <xref:System.Windows.Data.CollectionViewSource>합니다.

    [!code-xaml[DataGrid_GroupSortFilter#002](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#002)]

5. 액세스를 <xref:System.Windows.Data.CollectionViewSource> 코드에서 사용 하 여는 <xref:System.Windows.Data.CollectionViewSource.GetDefaultView%2A> 을 참조 하는 방법의 <xref:System.Windows.Data.CollectionViewSource>.

    [!code-csharp[DataGrid_GroupSortFilter#102](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#102)]
    [!code-vb[DataGrid_GroupSortFilter#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#102)]

## <a name="grouping-items-in-a-datagrid"></a>DataGrid의 항목 그룹화

항목 그룹화 되는 방법을 지정 하는 <xref:System.Windows.Controls.DataGrid>를 사용할는 <xref:System.Windows.Data.PropertyGroupDescription> 소스 뷰에서 항목을 그룹화 하는 형식입니다.

### <a name="to-group-items-in-a-datagrid-using-xaml"></a>XAML을 사용 하 여 DataGrid의 항목을 그룹

1. 만들기는 <xref:System.Windows.Data.PropertyGroupDescription> 그룹화 속성을 지정 하는 합니다. 코드 또는 XAML에서 속성을 지정할 수 있습니다.

   1. XAML을 설정 합니다 <xref:System.Windows.Data.PropertyGroupDescription.PropertyName%2A> 그룹화 속성의 이름입니다.

   2. 코드에서 생성자로 그룹화 할 속성의 이름을 전달 합니다.

2. 추가 된 <xref:System.Windows.Data.PropertyGroupDescription> 에 <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A?displayProperty=nameWithType> 컬렉션입니다.

3. 추가 인스턴스 <xref:System.Windows.Data.PropertyGroupDescription> 에 <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A> 더 많은 수준의 그룹화를 추가할 컬렉션입니다.

    [!code-xaml[DataGrid_GroupSortFilter#012](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#012)]
    [!code-csharp[DataGrid_GroupSortFilter#112](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#112)]
    [!code-vb[DataGrid_GroupSortFilter#112](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#112)]

4. 그룹을 제거 하려면 제거 합니다 <xref:System.Windows.Data.PropertyGroupDescription> 에서 <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A> 컬렉션입니다.

5. 모든 그룹을 제거 하려면 다음을 호출 합니다 <xref:System.Collections.ObjectModel.Collection%601.Clear%2A> 메서드는 <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A> 컬렉션입니다.

    [!code-csharp[DataGrid_GroupSortFilter#114](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#114)]
    [!code-vb[DataGrid_GroupSortFilter#114](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#114)]

항목이 그룹화 되는 경우는 <xref:System.Windows.Controls.DataGrid>를 정의할 수 있습니다는 <xref:System.Windows.Controls.GroupStyle> 각 그룹의 모양을 지정 하는 합니다. 적용 된 <xref:System.Windows.Controls.GroupStyle> 추가 하 여는 <xref:System.Windows.Controls.ItemsControl.GroupStyle%2A> DataGrid의 컬렉션입니다. 여러 가지 수준의 그룹화를 사용 하는 경우에 각 그룹 수준으로 다양 한 스타일을 적용할 수 있습니다. 스타일 정의 되는 순서 대로 적용 됩니다. 예를 들어, 두 가지 스타일을 정의 하는 경우 첫 번째 최상위 행 그룹에 적용 됩니다. 두 번째 스타일 및 하 한 두 번째 수준에서 모든 행 그룹에 적용 됩니다. <xref:System.Windows.FrameworkElement.DataContext%2A> 의 합니다 <xref:System.Windows.Controls.GroupStyle> 는 <xref:System.Windows.Data.CollectionViewGroup> 그룹을 나타내는입니다.

### <a name="to-change-the-appearance-of-row-group-headers"></a>행 그룹 머리글의 모양을 변경 하려면

1. 만들기는 <xref:System.Windows.Controls.GroupStyle> 행 그룹의 모양을 정의 합니다.

2. 배치는 <xref:System.Windows.Controls.GroupStyle> 안에 `<DataGrid.GroupStyle>` 태그입니다.

    [!code-xaml[DataGrid_GroupSortFilter#003](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#003)]

## <a name="sorting-items-in-a-datagrid"></a>DataGrid의 항목 정렬

항목 정렬 되는 방법을 지정 하는 <xref:System.Windows.Controls.DataGrid>를 사용할는 <xref:System.ComponentModel.SortDescription> 소스 뷰에서 항목을 정렬 하는 형식입니다.

### <a name="to-sort-items-in-a-datagrid"></a>DataGrid의 항목을 정렬 하려면

1. 만들기는 <xref:System.ComponentModel.SortDescription> 정렬할 속성을 지정 하는 합니다. 코드 또는 XAML에서 속성을 지정할 수 있습니다.

    1. XAML을 설정 합니다 <xref:System.ComponentModel.SortDescription.PropertyName%2A> 정렬할 속성의 이름입니다.

    2. 코드에서 정렬할 속성의 이름을 전달 하 고 <xref:System.ComponentModel.ListSortDirection> 생성자에 있습니다.

2. 추가 된 <xref:System.ComponentModel.SortDescription> 에 <xref:System.Windows.Data.CollectionViewSource.SortDescriptions%2A?displayProperty=nameWithType> 컬렉션입니다.

3. 추가 인스턴스 <xref:System.ComponentModel.SortDescription> 에 <xref:System.Windows.Data.CollectionViewSource.SortDescriptions%2A> 추가 속성으로 정렬 하는 컬렉션입니다.

    [!code-xaml[DataGrid_GroupSortFilter#011](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#011)]
    [!code-csharp[DataGrid_GroupSortFilter#211](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/WindowSnips1.xaml.cs#211)]
    [!code-vb[DataGrid_GroupSortFilter#211](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#211)]

## <a name="filtering-items-in-a-datagrid"></a>DataGrid의 항목 필터링

항목을 필터링 하는 <xref:System.Windows.Controls.DataGrid> 를 사용 하 여를 <xref:System.Windows.Data.CollectionViewSource>에 대 한 처리기에서 필터링 논리를 제공 하는 <xref:System.Windows.Data.CollectionViewSource.Filter?displayProperty=nameWithType> 이벤트.

### <a name="to-filter-items-in-a-datagrid"></a>DataGrid의 항목을 필터링 하려면

1. 에 대 한 처리기를 추가 합니다 <xref:System.Windows.Data.CollectionViewSource.Filter?displayProperty=nameWithType> 이벤트입니다.

2. 에 <xref:System.Windows.Data.CollectionViewSource.Filter> 이벤트 처리기를 필터링 논리를 정의 합니다.

    필터 뷰를 새로 고칠 때마다 적용 됩니다.

    [!code-xaml[DataGrid_GroupSortFilter#013](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#013)]
    [!code-csharp[DataGrid_GroupSortFilter#113](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#113)]
    [!code-vb[DataGrid_GroupSortFilter#113](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#113)]

또는에서 항목을 필터링 할 수 있습니다는 <xref:System.Windows.Controls.DataGrid> 필터링 논리를 설정 하는 메서드를 만들어를 <xref:System.Windows.Data.CollectionView.Filter%2A?displayProperty=nameWithType> 속성 필터를 적용 합니다. 이 방법의 예제를 보려면 [뷰에서 데이터 필터링](../data/how-to-filter-data-in-a-view.md)합니다.

## <a name="example"></a>예제

다음 예제에서는 그룹화, 정렬 및 필터링 `Task` 에서 데이터를 <xref:System.Windows.Data.CollectionViewSource> 및 정렬, 필터링 및 그룹화 된 표시 `Task` 에서 데이터를 <xref:System.Windows.Controls.DataGrid>입니다. <xref:System.Windows.Data.CollectionViewSource> 으로 사용 되는 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 에 대 한는 <xref:System.Windows.Controls.DataGrid>합니다. 그룹화, 정렬 및 필터링에 수행 되는 <xref:System.Windows.Data.CollectionViewSource> 에 표시 됩니다는 <xref:System.Windows.Controls.DataGrid> UI입니다.

이 예제를 테스트 하려면 DGGroupSortFilterExample 이름을 프로젝트 이름에 맞게 조정 해야 합니다. Visual Basic을 사용 하는 경우에 대 한 클래스 이름을 변경 해야 합니다 <xref:System.Windows.Window> 는 다음과 같습니다.

`<Window x:Class="MainWindow"`

[!code-xaml[DataGrid_GroupSortFilter#000](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#000)]
[!code-csharp[DataGrid_GroupSortFilter#100](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#100)]
[!code-vb[DataGrid_GroupSortFilter#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#100)]

## <a name="see-also"></a>참고자료

- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [ObservableCollection 만들기 및 바인딩](../data/how-to-create-and-bind-to-an-observablecollection.md)
- [뷰에서 데이터 필터링](../data/how-to-filter-data-in-a-view.md)
- [뷰의 데이터 정렬](../data/how-to-sort-data-in-a-view.md)
- [XAML 데이터 정렬 및 그룹화](../data/how-to-sort-and-group-data-using-a-view-in-xaml.md)
