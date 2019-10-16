---
title: 행 상태 및 행 버전
ms.date: 07/19/2018
dev_langs:
- csharp
- vb
ms.assetid: 2e6642c9-bfc6-425c-b3a7-e4912ffa6c1f
ms.openlocfilehash: 70596d6acb62fa01092e5e55dd3b6c84eb162b5d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784334"
---
# <a name="row-states-and-row-versions"></a>행 상태 및 행 버전
ADO.NET에서는 행 상태 및 버전을 사용하여 테이블의 행을 관리합니다. 행 상태는 행의 상태를 나타내며, 행 버전에서는 현재 값, 원래 값 및 기본값 등과 같이 수정될 때 행에 저장된 값을 관리합니다. 예를 들어, 행에서 열을 수정한 경우 이 행의 상태는 `Modified`가 되고 두 개의 행 버전이 존재하게 됩니다. 즉, `Current` 버전에는 현재의 행 값이 포함되고 `Original` 버전에는 열이 수정되기 전의 행 값이 포함됩니다.  
  
 각 <xref:System.Data.DataRow> 개체에는 <xref:System.Data.DataRow.RowState%2A> 속성이 있어서 사용자는 이 속성을 검사하여 행의 현재 상태를 결정합니다. 다음 표에서는 각 `RowState` 열거형 값에 대해 간략하게 설명합니다.  
  
|RowState 값|Description|  
|--------------------|-----------------|  
|<xref:System.Data.DataRowState.Unchanged>|`AcceptChanges`를 마지막으로 호출한 이후 또는 `DataAdapter.Fill`에 의해서 행이 만들어진 이후로 변경된 내용이 없습니다.|  
|<xref:System.Data.DataRowState.Added>|테이블에 행이 추가되었지만 `AcceptChanges`가 호출되지 않았습니다.|  
|<xref:System.Data.DataRowState.Modified>|일부 행 요소가 변경되었습니다.|  
|<xref:System.Data.DataRowState.Deleted>|행이 테이블에서 삭제되었으며 `AcceptChanges`가 호출되지 않았습니다.|  
|<xref:System.Data.DataRowState.Detached>|행이 `DataRowCollection`의 일부가 아닙니다. 새로 만든 행의 `RowState`가 `Detached`로 설정됩니다. `DataRow` 메서드를 호출하여 새 `DataRowCollection`를 `Add`에 추가한 후에는 `RowState` 속성 값이 `Added`로 설정됩니다.<br /><br /> `Detached` 메서드를 사용하거나 `DataRowCollection` 메서드를 사용한 후 `Remove` 메서드를 사용하여 `Delete`에서 제거된 행에 대해서도 이 속성이 `AcceptChanges`로 설정됩니다.|  
  
 `AcceptChanges`, <xref:System.Data.DataSet> 또는 <xref:System.Data.DataTable>에 대해 <xref:System.Data.DataRow>가 호출되는 경우 행 상태가 `Deleted`인 행은 모두 제거됩니다. 나머지 행의 상태는 `Unchanged`로 지정되며 `Original` 행 버전의 값은 `Current` 행 버전의 값으로 덮어쓰여집니다. `RejectChanges`가 호출되는 경우 행 상태가 `Added`인 행은 모두 제거됩니다. 나머지 행의 상태는 `Unchanged`로 지정되며 `Current` 행 버전의 값은 `Original` 행 버전의 값으로 덮어쓰여집니다.  
  
 다음 예제와 같이 열 참조와 함께 <xref:System.Data.DataRowVersion> 매개 변수를 전달하면 행의 다른 행 버전을 볼 수 있습니다.  
  
```vb  
Dim custRow As DataRow = custTable.Rows(0)  
Dim custID As String = custRow("CustomerID", DataRowVersion.Original).ToString()  
```  
  
```csharp  
DataRow custRow = custTable.Rows[0];  
string custID = custRow["CustomerID", DataRowVersion.Original].ToString();  
```  
  
 다음 표에서는 각 `DataRowVersion` 열거형 값에 대해 간략하게 설명합니다.  
  
|DataRowVersion 값|Description|  
|--------------------------|-----------------|  
|<xref:System.Data.DataRowVersion.Current>|행의 현재 값입니다. `RowState`가 `Deleted`인 행에는 이 행 버전이 존재하지 않습니다.|  
|<xref:System.Data.DataRowVersion.Default>|특정 행에 대한 기본 행 버전입니다. `Added`, `Modified` 또는 `Deleted` 행의 기본 행 버전은 `Current`이고, `Detached` 행의 기본 행 버전은 `Proposed`입니다.|  
|<xref:System.Data.DataRowVersion.Original>|행의 원래 값입니다. `RowState`가 `Added`인 행에는 이 행 버전이 존재하지 않습니다.|  
|<xref:System.Data.DataRowVersion.Proposed>|행에 제안된 값입니다. 이 행 버전은 행에서 편집 작업을 수행하는 동안 존재하거나 `DataRowCollection`의 일부가 아닌 행에 대해 존재합니다.|  
  
 `DataRow`을 인수로 전달하여 <xref:System.Data.DataRow.HasVersion%2A> 메서드를 호출하면 `DataRowVersion`에 특정 행 버전이 있는지 여부를 테스트할 수 있습니다. 예를 들어, `DataRow.HasVersion(DataRowVersion.Original)`은 `false`가 호출되기 전에 새로 추가된 행에 대해 `AcceptChanges`를 반환합니다.  
  
 다음 코드 예제에서는 테이블에서 삭제된 모든 행의 값을 표시합니다. `Deleted` 행에는 `Current` 행 버전이 없으므로 해당 열 값에 액세스할 때는 `DataRowVersion.Original`을 전달해야 합니다.  
  
```vb  
Dim catTable As DataTable = catDS.Tables("Categories")  
  
Dim delRows() As DataRow = catTable.Select(Nothing, Nothing, DataViewRowState.Deleted)  
  
Console.WriteLine("Deleted rows:" & vbCrLf)  
  
Dim catCol As DataColumn  
Dim delRow As DataRow  
  
For Each catCol In catTable.Columns  
  Console.Write(catCol.ColumnName & vbTab)  
Next  
Console.WriteLine()  
  
For Each delRow In delRows  
  For Each catCol In catTable.Columns  
    Console.Write(delRow(catCol, DataRowVersion.Original) & vbTab)  
  Next  
  Console.WriteLine()  
Next  
```  
  
```csharp  
DataTable catTable = catDS.Tables["Categories"];  
  
DataRow[] delRows = catTable.Select(null, null, DataViewRowState.Deleted);  
  
Console.WriteLine("Deleted rows:\n");  
  
foreach (DataColumn catCol in catTable.Columns)  
  Console.Write(catCol.ColumnName + "\t");  
Console.WriteLine();  
  
foreach (DataRow delRow in delRows)  
{  
  foreach (DataColumn catCol in catTable.Columns)  
    Console.Write(delRow[catCol, DataRowVersion.Original] + "\t");  
  Console.WriteLine();  
}  
```  
  
## <a name="see-also"></a>참고자료

- [DataTable에서 데이터 조작](manipulating-data-in-a-datatable.md)
- [DataSet, DataTable 및 DataView](index.md)
- [DataAdapter 및 DataReader](../dataadapters-and-datareaders.md)
- [ADO.NET 개요](../ado-net-overview.md)
