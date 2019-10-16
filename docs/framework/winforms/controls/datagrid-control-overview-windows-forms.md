---
title: DataGrid 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- DataGrid
helpviewer_keywords:
- datasets [Windows Forms], binding to DataGrid control
- data binding [Windows Forms], DataGrid control
- columns [Windows Forms], DataGrid control
- data sources [Windows Forms], binding to DataGrid control
- tables [Windows Forms], binding to DataGrid control
- DataGrid control [Windows Forms], data binding
- DataGrid control [Windows Forms], about DataGrid control
- parent tables in DataGrid control
- tables [Windows Forms], displaying in DataGrid control
- data grids [Windows Forms], about data grids
- multiple tables in DataGrid control
- data [Windows Forms], resorting
- data [Windows Forms], navigating
- parent table navigation in DataGrid
- child tables [Windows Forms], dataGrid control
ms.assetid: 85604bce-bc03-49d9-9030-dda8896c44b1
ms.openlocfilehash: ce149ed25d3326daa9096596fe8d542a13759a96
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046206"
---
# <a name="datagrid-control-overview-windows-forms"></a>DataGrid 컨트롤 개요(Windows Forms)

> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.

Windows Forms <xref:System.Windows.Forms.DataGrid> 컨트롤은 일련의 행과 열에 데이터를 표시합니다. 가장 간단한 경우는 관계를 포함하지 않는 단일 테이블이 있는 데이터 소스에 표 형태 창이 바인딩된 경우입니다. 이 경우 스프레드시트와 같이 간단한 행과 열에 데이터가 나타납니다. 데이터를 다른 컨트롤에 바인딩하는 방법에 대한 자세한 내용은 [데이터 바인딩 및 Windows Forms](../data-binding-and-windows-forms.md)를 참조하십시오.

<xref:System.Windows.Forms.DataGrid>가 여러 개의 관련 테이블에 바인딩되어 있고 표 형태 창에서 탐색을 사용할 수 있는 경우 표 형태 창의 각 행에 확장기가 표시됩니다. 사용자는 확장기를 통해 부모 테이블에서 자식 테이블로 이동할 수 있습니다. 노드를 클릭하면 자식 테이블이 표시되고 뒤로 단추를 클릭하면 원래 부모 테이블이 표시됩니다. 이런 방식으로 표 형태 창에 테이블 간의 계층 관계가 표시됩니다.

다음 스크린샷은 여러 테이블을 가진 데이터에 바인딩된 DataGrid를 보여 줍니다.

![여러 테이블을 포함 하는 데이터에 바인딩된 DataGrid를 보여 주는 WinForms 앱입니다.](./media/datagrid-control-overview-windows-forms/datagrid-bound-multiple-tables.gif)

<xref:System.Windows.Forms.DataGrid>에서는 데이터 집합, 관련 테이블 간의 탐색, 풍부한 형식 지정 및 편집 기능을 위한 사용자 인터페이스를 제공할 수 있습니다.

데이터의 표시 및 조작은 별개의 함수입니다. 컨트롤은 사용자 인터페이스를 처리 하는 반면 데이터 업데이트는 Windows Forms 데이터 바인딩 아키텍처 및 .NET Framework 데이터 공급자에 의해 처리 됩니다. 따라서 동일한 데이터 소스에 바인딩된 여러 컨트롤이 동기화 상태로 유지됩니다.

> [!NOTE]
> Visual Basic 6.0의 DataGrid 컨트롤에 익숙한 경우 Windows Forms <xref:System.Windows.Forms.DataGrid> 컨트롤에서 몇 가지 중요한 차이점을 발견할 것입니다.

표 형태 창이 <xref:System.Data.DataSet>에 바인딩된 경우 열과 행이 자동으로 생성되고 형식이 지정되며 채워집니다. 자세한 내용은 [데이터 바인딩 및 Windows Forms](../data-binding-and-windows-forms.md)를 참조하십시오. <xref:System.Windows.Forms.DataGrid> 컨트롤을 생성한 후 요구에 따라 열과 행을 추가, 삭제 및 다시 정렬하고 형식을 지정할 수 있습니다.

## <a name="binding-data-to-the-control"></a>컨트롤에 데이터 바인딩

<xref:System.Windows.Forms.DataGrid> 컨트롤이 작동하려면 디자인 타임에 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 및 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 속성을 사용하거나 런타임에 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 메서드를 사용하여 데이터 소스에 바인딩되어야 합니다. 이 바인딩을 통해 <xref:System.Windows.Forms.DataGrid>는 인스턴스화된 데이터 소스 개체(예: <xref:System.Data.DataSet> 또는 <xref:System.Data.DataTable>)를 가리킵니다. <xref:System.Windows.Forms.DataGrid> 컨트롤은 데이터에 대해 수행된 작업의 결과를 보여 줍니다. 대부분의 데이터 관련 작업은 <xref:System.Windows.Forms.DataGrid>가 아니라 데이터 소스를 통해 수행됩니다.

바인딩된 데이터 세트의 데이터가 임의 메커니즘을 통해 업데이트되면 <xref:System.Windows.Forms.DataGrid> 컨트롤이 변경 내용을 반영합니다. 데이터 눈금과 해당 테이블 스타일과 열 스타일 `ReadOnly` 의 속성이로 `false`설정 된 경우 <xref:System.Windows.Forms.DataGrid> 컨트롤을 통해 데이터 집합의 데이터를 업데이트할 수 있습니다.

한 번에 하나의 테이블만 <xref:System.Windows.Forms.DataGrid>에 표시될 수 있습니다. 테이블 간에 부모-자식 관계가 정의된 경우 사용자가 관련 테이블 간에 이동하여 <xref:System.Windows.Forms.DataGrid> 컨트롤에 표시할 테이블을 선택할 수 있습니다. 디자인 타임 또는 런타임에 <xref:System.Windows.Forms.DataGrid> [컨트롤을 ADO.NET 데이터 소스에 바인딩하는 방법에 대 한 자세한 내용은 방법: Windows Forms DataGrid 컨트롤을 데이터 소스](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)에 바인딩합니다.

<xref:System.Windows.Forms.DataGrid>에 유효한 데이터 소스는 다음과 같습니다.

- <xref:System.Data.DataTable> 클래스

- <xref:System.Data.DataView> 클래스

- <xref:System.Data.DataSet> 클래스

- <xref:System.Data.DataViewManager> 클래스

소스가 데이터 세트인 경우 데이터 세트는 폼의 개체이거나 XML Web services에 의해 폼에 전달된 개체일 수 있습니다. 형식화된 데이터 세트나 형식화되지 않은 데이터 세트에 바인딩할 수 있습니다.

배열의 요소와 같은 구조체의 개체가 public 속성을 노출하는 경우 <xref:System.Windows.Forms.DataGrid> 컨트롤을 추가 구조체에 바인딩할 수도 있습니다. 구조체에 있는 요소의 모든 public 속성이 표 형태 창에 표시됩니다. 예를 들어 <xref:System.Windows.Forms.DataGrid> 컨트롤을 고객 개체 배열에 바인딩하는 경우 해당 고객 개체의 모든 public 속성이 표 형태 창에 표시됩니다. 이는 일부 인스턴스에서 구조체에 바인딩할 수는 있지만 결과로 바인딩된 구조체가 실용적이지 않을 수 있음을 의미합니다. 예를 들어 정수 배열에 바인딩할 수는 있지만 `Integer` 데이터 형식이 public 속성을 지원하지 않으므로 표 형태 창에서 데이터를 표시할 수 없습니다.

해당 요소가 public 속성을 노출하는 경우 다음 구조체에 바인딩할 수 있습니다.

- <xref:System.Collections.IList> 인터페이스를 구현하는 구성 요소 여기에는 1차원 배열이 포함됩니다.

- <xref:System.ComponentModel.IListSource> 인터페이스를 구현하는 구성 요소

- <xref:System.ComponentModel.IBindingList> 인터페이스를 구현하는 구성 요소

 가능한 데이터 소스에 대한 자세한 내용은 [Windows Forms에서 지원하는 데이터 소스](../data-sources-supported-by-windows-forms.md)를 참조하십시오.

## <a name="grid-display"></a>표 형태 창 표시

<xref:System.Windows.Forms.DataGrid> 컨트롤은 일반적으로 데이터 집합에서 단일 데이터 테이블을 표시하는 데 사용됩니다. 그러나 컨트롤을 사용하여 관련 테이블을 비롯한 여러 테이블을 표시할 수도 있습니다. 표 형태 창의 표시는 데이터 소스에 따라 자동으로 조정됩니다. 다음 표에서는 다양한 구성에 대해 표시되는 내용을 보여 줍니다.

|데이터 집합의 내용|표시되는 내용|
|--------------------------|-----------------------|
|단일 테이블.|테이블이 표 형태 창에 표시됩니다.|
|여러 테이블.|사용자가 표시할 테이블을 찾기 위해 탐색할 수 있는 트리 뷰가 표 형태 창에 표시될 수 있습니다.|
|관련된 여러 테이블.|테이블을 선택하는 데 사용할 트리 뷰가 표 형태 창에 표시되거나, 부모 테이블이 표 형태 창에 표시되도록 지정할 수 있습니다. 사용자는 부모 테이블의 레코드를 통해 관련된 자식 행을 탐색할 수 있습니다.|

> [!NOTE]
> 데이터 집합의 테이블은 <xref:System.Data.DataRelation>을 사용하여 관련됩니다. 또한 [데이터 집합 간의 관계 만들기](/visualstudio/data-tools/relationships-in-datasets)를 참조 하세요.

<xref:System.Windows.Forms.DataGrid> 컨트롤에서 테이블을 표시하고 <xref:System.Windows.Forms.DataGrid.AllowSorting%2A> 속성이 `true`로 설정된 경우 열 머리글을 클릭하여 데이터를 다시 정렬할 수 있습니다. 사용자가 행을 추가하고 셀을 편집할 수도 있습니다.

테이블 집합 간의 관계는 탐색의 부모/자식 구조를 사용하여 사용자에게 표시됩니다. 부모 테이블은 가장 높은 데이터 수준이고, 자식 테이블은 부모 테이블의 개별 목록에서 파생된 데이터 테이블입니다. 자식 테이블을 포함하는 각 부모 행에 확장기가 표시됩니다. 확장기를 클릭하면 자식 테이블에 대한 웹 형식의 링크 목록이 생성됩니다. 사용자가 링크를 선택하면 자식 테이블이 표시됩니다. 부모 행 표시/숨기기 아이콘을 클릭 합니다.![부모 행 표시/숨기기 아이콘](./media/datagrid-control-overview-windows-forms/show-hide-parent-rows.gif))는 부모 테이블에 대 한 정보를 숨기 거 나 사용자가 이전에 숨긴 경우 다시 표시 되도록 합니다. 사용자는 뒤로 단추를 클릭하여 이전에 표시된 테이블로 다시 이동할 수 있습니다.

## <a name="columns-and-rows"></a>열과 행

<xref:System.Windows.Forms.DataGrid>는 <xref:System.Windows.Forms.DataGrid> 컨트롤의 <xref:System.Windows.Forms.DataGrid.TableStyles%2A> 속성에 포함된 <xref:System.Windows.Forms.DataGridTableStyle> 개체의 컬렉션으로 구성됩니다. 테이블 스타일은 <xref:System.Windows.Forms.DataGridTableStyle>의 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 속성에 포함된 <xref:System.Windows.Forms.DataGridColumnStyle> 개체의 컬렉션을 포함할 수 있습니다. 속성 창을 통해 액세스 <xref:System.Windows.Forms.DataGrid.TableStyles%2A> 되는 컬렉션 편집기를 사용 하 여 및 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 속성을 편집할 수 있습니다.

<xref:System.Windows.Forms.DataGrid> 컨트롤과 연결된 <xref:System.Windows.Forms.DataGridTableStyle>은 <xref:System.Windows.Forms.GridTableStylesCollection>을 통해 모두 액세스할 수 있습니다. <xref:System.Windows.Forms.GridTableStylesCollection>은 디자이너에서 <xref:System.Windows.Forms.DataGridTableStyle> 컬렉션 편집기를 통해 또는 <xref:System.Windows.Forms.DataGrid> 컨트롤의 <xref:System.Windows.Forms.DataGrid.TableStyles%2A> 속성을 통해 프로그래밍 방식으로 편집할 수 있습니다.

다음 그림에서는 DataGrid 컨트롤에 포함 된 개체를 보여 줍니다.

![DataGrid 컨트롤에 포함 된 개체를 보여 주는 다이어그램입니다.](./media/datagrid-control-overview-windows-forms/visual-basic-columns.gif)

테이블 스타일과 열 스타일은 해당 `MappingName` 속성을 적절한 <xref:System.Data.DataTable.TableName%2A> 및 <xref:System.Data.DataColumn.ColumnName%2A> 속성으로 설정하여 <xref:System.Data.DataTable> 개체 및 <xref:System.Data.DataColumn> 개체와 동기화됩니다. 유효한 데이터 소스에 바인딩된 <xref:System.Windows.Forms.DataGrid> 컨트롤에 열 스타일이 없는 <xref:System.Windows.Forms.DataGridTableStyle>이 추가되고 해당 테이블 스타일의 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 속성이 유효한 <xref:System.Data.DataTable.TableName%2A> 속성으로 설정된 경우 해당 테이블 스타일에 대한 <xref:System.Windows.Forms.DataGridColumnStyle> 개체 컬렉션이 생성됩니다. <xref:System.Data.DataTable>의 <xref:System.Data.DataTable.Columns%2A> 컬렉션에서 발견된 각 <xref:System.Data.DataColumn>에 해당하는 <xref:System.Windows.Forms.DataGridColumnStyle>이 <xref:System.Windows.Forms.GridColumnStylesCollection>에 추가됩니다. <xref:System.Windows.Forms.GridColumnStylesCollection>은 <xref:System.Windows.Forms.DataGridTableStyle>의 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 속성을 통해 액세스됩니다. <xref:System.Windows.Forms.GridColumnStylesCollection>의 <xref:System.Windows.Forms.GridColumnStylesCollection.Add%2A> 또는 <xref:System.Windows.Forms.GridColumnStylesCollection.Remove%2A> 메서드를 사용하여 표 형태 창에서 열을 추가하거나 삭제할 수 있습니다. 자세한 내용은 [방법: Windows Forms DataGrid 컨트롤](how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md) 에 테이블과 열을 추가 하 고 [방법: Windows Forms DataGrid 컨트롤](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)에서 열을 삭제 하거나 숨깁니다.

열 형식 컬렉션은 풍부한 형식 지정 및 편집 기능을 통해 <xref:System.Windows.Forms.DataGridColumnStyle> 클래스를 확장합니다. 모든 열 형식이 <xref:System.Windows.Forms.DataGridColumnStyle> 기본 클래스에서 상속합니다. 생성되는 클래스는 <xref:System.Web.UI.WebControls.DataGridColumn>의 기반이 되는 <xref:System.Data.DataColumn>의 <xref:System.Data.DataColumn.DataType%2A> 속성에 따라 달라집니다. 예를 들어 해당 <xref:System.Data.DataColumn.DataType%2A> 속성이 <xref:System.Boolean>으로 설정된 <xref:System.Data.DataColumn>은 <xref:System.Windows.Forms.DataGridBoolColumn>에 연결됩니다. 다음 표에서는 이러한 열 형식을 각각 설명합니다.

|열 유형|설명|
|-----------------|-----------------|
|<xref:System.Windows.Forms.DataGridTextBoxColumn>|데이터를 받아서 형식이 지정된 문자열이나 형식이 지정되지 않은 문자열로 표시합니다. 편집 기능은 간단한 <xref:System.Windows.Forms.TextBox>의 데이터 편집 기능과 동일합니다. <xref:System.Windows.Forms.DataGridColumnStyle>에서 상속됩니다.|
|<xref:System.Windows.Forms.DataGridBoolColumn>|`true`, `false` 및 null 값을 받아서 표시합니다. <xref:System.Windows.Forms.DataGridColumnStyle>에서 상속됩니다.|

열 오른쪽 가장자리를 두 번 클릭하면 열 크기가 조정되어 전체 캡션과 가장 넓은 항목을 표시합니다.

## <a name="table-styles-and-column-styles"></a>테이블 스타일과 열 스타일

<xref:System.Windows.Forms.DataGrid> 컨트롤의 기본 형식을 설정하는 즉시 특정 테이블이 데이터 표에 표시될 때 사용되는 색을 사용자 지정할 수 있습니다.

이렇게 하려면 <xref:System.Windows.Forms.DataGridTableStyle> 클래스의 인스턴스를 만듭니다. 테이블 스타일은 <xref:System.Windows.Forms.DataGrid> 컨트롤 자체의 기본 형식과 별도로 특정 테이블의 형식을 지정합니다. 각 테이블에 대해 한 번에 하나의 테이블 스타일만 정의될 수 있습니다.

경우에 따라 특정 열을 특정 데이터 테이블의 나머지 열과 다르게 표시할 수 있습니다. <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 속성을 사용하여 열 스타일의 사용자 지정 집합을 만들 수 있습니다.

테이블 스타일이 데이터 테이블과 관련이 있는 것처럼 열 스타일은 데이터 세트의 열과 관련이 있습니다. 각 테이블에 대해 한 번에 하나의 테이블 스타일만 정의될 수 있는 것처럼 특정 테이블 스타일에서 각 열에 대해 하나의 열 스타일만 정의될 수 있습니다. 이 관계는 열의 <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> 속성에서 정의됩니다.

열 스타일을 추가 하지 않고 테이블 스타일을 만든 경우 런타임에 폼과 그리드를 만들 때 Visual Studio에서 기본 열 스타일을 추가 합니다. 그러나 테이블 스타일을 만들고 열 스타일을 추가한 경우에는 Visual Studio에서 열 스타일을 만들지 않습니다. 또한 열 스타일을 정의하고 표 형태 창에 표시할 열을 포함하는 매핑 이름으로 할당해야 합니다.

열 스타일을 할당하여 데이터 표에 포함할 열을 지정하며 열 스타일이 열에 할당되지 않았기 때문에 표 형태 창에 표시되지 않는 데이터 열을 데이터 세트에 포함할 수 있습니다. 그러나 데이터 열이 데이터 세트에 포함되었기 때문에 표시되지 않는 데이터를 프로그래밍 방식으로 편집할 수 있습니다.

> [!NOTE]
> 일반적으로 테이블 스타일 컬렉션에 테이블 스타일을 추가하기 전에 열 스타일을 만들고 열 스타일 컬렉션에 추가합니다. 컬렉션에 빈 테이블 스타일을 추가하는 경우 열 스타일이 자동으로 생성됩니다. 따라서 중복된 <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> 값을 가진 새로운 열 스타일을 열 스타일 컬렉션에 추가하려고 하면 예외가 발생합니다.
>
> 많은 열 중에서 하나의 열만 조정하려는 경우도 있습니다. 예를 들어 데이터 세트는 50개의 열을 포함하지만 이 중에서 49개만 조정하려고 합니다. 이 경우 50개 열을 모두 가져오고 프로그래밍 방식으로 하나를 제거하는 것이 원하는 49개의 개별 열을 프로그래밍 방식으로 각각 추가하는 것보다 더 쉽습니다.

## <a name="formatting"></a>서식

<xref:System.Windows.Forms.DataGrid> 컨트롤에 적용할 수 있는 형식 지정에는 테두리 스타일, 모눈선 스타일, 글꼴, 캡션 속성, 데이터 맞춤 및 교대로 반복되는 행의 배경색이 포함됩니다. 자세한 내용은 [방법: Windows Forms DataGrid 컨트롤](how-to-format-the-windows-forms-datagrid-control.md)의 서식을 지정 합니다.

## <a name="events"></a>이벤트

<xref:System.Windows.Forms.Control.MouseDown>, <xref:System.Windows.Forms.Control.Enter> 및 <xref:System.Windows.Forms.DataGrid.Scroll>과 같은 일반적인 컨트롤 이벤트 외에도 <xref:System.Windows.Forms.DataGrid> 컨트롤은 표 형태 창 내의 편집 및 탐색과 관련된 이벤트를 지원합니다. <xref:System.Windows.Forms.DataGrid.CurrentCell%2A> 속성은 선택된 셀을 확인합니다. 사용자가 새로운 셀로 이동하면 <xref:System.Windows.Forms.DataGrid.CurrentCellChanged> 이벤트가 발생합니다. 사용자가 부모/자식 관계를 통해 새 테이블로 이동하면 <xref:System.Windows.Forms.DataGrid.Navigate> 이벤트가 발생합니다. 사용자가 자식 테이블을 보고 있을 때 뒤로 단추를 클릭하면 <xref:System.Windows.Forms.DataGrid.BackButtonClick> 이벤트가 발생하고, 부모 행 표시/숨기기 아이콘을 클릭하면 <xref:System.Windows.Forms.DataGrid.ShowParentDetailsButtonClick> 이벤트가 발생합니다.

## <a name="see-also"></a>참고자료

- [DataGrid 컨트롤](datagrid-control-windows-forms.md)
- [방법: Windows Forms DataGrid 컨트롤을 데이터 소스에 바인딩](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)
- [방법: Windows Forms DataGrid 컨트롤에 테이블 및 열 추가](how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)
- [방법: Windows Forms DataGrid 컨트롤에서 열 삭제 또는 숨기기](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
- [방법: Windows Forms DataGrid 컨트롤 서식 지정](how-to-format-the-windows-forms-datagrid-control.md)
