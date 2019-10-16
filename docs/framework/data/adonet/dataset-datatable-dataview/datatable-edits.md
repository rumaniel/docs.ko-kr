---
title: DataTable 편집
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f08008a9-042e-4de9-94f3-4f0e502b1eb5
ms.openlocfilehash: 689a297eb5368d35c2e7dd034426edbe665e7ed2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785390"
---
# <a name="datatable-edits"></a>DataTable 편집
<xref:System.Data.DataRow>에서 열 값을 변경하는 경우, 변경된 값은 현재 상태의 행에 바로 저장됩니다. <xref:System.Data.DataRow.AcceptChanges%2A> <xref:System.Data.DataRow.RejectChanges%2A>그런 다음 가Modified로설정되고,DataRow의또는메서드를사용하여변경내용이허용되거나거부됩니다.<xref:System.Data.DataRowState> 또한 **DataRow** 는 편집 하는 동안 행의 상태를 일시 중단 하는 데 사용할 수 있는 세 가지 메서드를 제공 합니다. 이러한 메서드에는 <xref:System.Data.DataRow.BeginEdit%2A>, <xref:System.Data.DataRow.EndEdit%2A> 및 <xref:System.Data.DataRow.CancelEdit%2A>이 있습니다.  
  
 **Datarow** 의 열 값을 직접 수정 하는 경우 **datarow** 는 **현재**, **기본**및 **원래** 행 버전을 사용 하 여 열 값을 관리 합니다. 이러한 행 버전 외에도 **BeginEdit**, **EndEdit**및 **CancelEdit** 메서드는 네 번째 행 버전을 사용 합니다. **제안 됨**. 행 버전에 대 한 자세한 내용은 참조 하세요. [행 상태 및 행 버전](row-states-and-row-versions.md)합니다.  
  
 **제안** 된 행 버전은 **BeginEdit** 를 호출 하 여 시작 하 고 **EndEdit** 또는 **CancelEdit를** 사용 하거나 **AcceptChanges** 또는 **RejectChanges**를 호출 하 여 종료 되는 편집 작업 중에 존재 합니다.  
  
 편집 작업을 수행 하는 동안 **DataTable**의 **Columnchanged** 이벤트에서 **ProposedValue** 를 평가 하 여 개별 열에 유효성 검사 논리를 적용할 수 있습니다. **Columnchanged** 이벤트는를 변경 하는 열과 **ProposedValue**에 대 한 참조를 유지 하는 **DataColumnChangeEventArgs** 을 보유 합니다. 사용자는 제안된 값을 검사한 후 이 값을 수정하거나 편집을 취소할 수 있습니다. 편집이 종료 되 면 행이 **제안** 된 상태에서 제외 됩니다.  
  
 **EndEdit**를 호출 하 여 편집을 확인 하거나 **CancelEdit**를 호출 하 여 편집을 취소할 수 있습니다. **EndEdit** 에서 편집을 확인 하는 동안에는 **AcceptChanges** 가 호출 될 때까지 **데이터 집합이** 실제로 변경 내용을 수락 하지 않습니다. **EndEdit** 또는 **CancelEdit**를 사용 하 여 편집을 종료 하기 전에 **AcceptChanges** 를 호출 하는 경우에는 편집이 종료 되 고 **현재** 행과 **원래** 행 버전 모두에 대해 **제안** 된 행 값이 허용 됩니다. 동일한 방식으로 **RejectChanges** 를 호출 하면 편집이 종료 되 고 **현재** 및 **제안** 된 행 버전이 삭제 됩니다. **AcceptChanges** 또는 **RejectChanges** 를 호출한 후에는 **EndEdit** 또는 **CancelEdit** 를 호출 해도 편집이 이미 종료 되었으므로 효과가 없습니다.  
  
 다음 예제에서는 **EndEdit** 및 **CancelEdit**와 함께 **BeginEdit** 를 사용 하는 방법을 보여 줍니다. 또한이 예제에서는 **Columnchanged** 이벤트에서 **ProposedValue** 를 확인 하 고 편집을 취소할지 여부를 결정 합니다.  
  
```vb  
Dim workTable As DataTable = New DataTable  
workTable.Columns.Add("LastName", Type.GetType("System.String"))  
  
AddHandler workTable.ColumnChanged, _  
  New DataColumnChangeEventHandler(AddressOf OnColumnChanged)  
  
Dim workRow As DataRow = workTable.NewRow()  
workRow(0) = "Smith"  
workTable.Rows.Add(workRow)  
  
workRow.BeginEdit()  
' Causes the ColumnChanged event to write a message and cancel the edit.  
workRow(0) = ""       
workRow.EndEdit()  
  
' Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow(0), workRow.RowState)  
  
Private Shared Sub OnColumnChanged( _  
  sender As Object, args As DataColumnChangeEventArgs)  
  If args.Column.ColumnName = "LastName" Then  
    If args.ProposedValue.ToString() = "" Then  
      Console.WriteLine("Last Name cannot be blank.  Edit canceled.")  
      args.Row.CancelEdit()  
    End If  
  End If  
End Sub  
```  
  
```csharp  
DataTable workTable  = new DataTable();  
workTable.Columns.Add("LastName", typeof(String));  
  
workTable.ColumnChanged +=   
  new DataColumnChangeEventHandler(OnColumnChanged);  
  
DataRow workRow = workTable.NewRow();  
workRow[0] = "Smith";  
workTable.Rows.Add(workRow);  
  
workRow.BeginEdit();  
// Causes the ColumnChanged event to write a message and cancel the edit.  
workRow[0] = "";       
workRow.EndEdit();  
  
// Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow[0], workRow.RowState);    
  
protected static void OnColumnChanged(  
  Object sender, DataColumnChangeEventArgs args)  
{  
  if (args.Column.ColumnName == "LastName")  
    if (args.ProposedValue.ToString() == "")  
    {  
      Console.WriteLine("Last Name cannot be blank. Edit canceled.");  
      args.Row.CancelEdit();  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataRow>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataRowVersion>
- [DataTable에서 데이터 조작](manipulating-data-in-a-datatable.md)
- [DataTable 이벤트 처리](handling-datatable-events.md)
- [ADO.NET 개요](../ado-net-overview.md)
