---
title: DataAdapter 이벤트 처리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 11515b25-ee49-4b1d-9294-a142147c1ec5
ms.openlocfilehash: 8438a7b54ca19625687ab96386384cf62ae62d11
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783802"
---
# <a name="handling-dataadapter-events"></a>DataAdapter 이벤트 처리
ADO.NET <xref:System.Data.Common.DataAdapter>는 데이터 소스의 데이터가 변경되었을 때 응답하는 데 사용할 수 있는 세 가지 이벤트를 제공합니다. 다음 표에서는 `DataAdapter` 이벤트를 보여 줍니다.  
  
|이벤트|Description|  
|-----------|-----------------|  
|`RowUpdating`|`Update` 메서드 중 하나를 호출하여 행에 대해 UPDATE, INSERT 또는 DELETE 작업을 시작하려고 합니다.|  
|`RowUpdated`|`Update` 메서드 중 하나를 호출하여 행에 대한 UPDATE, INSERT 또는 DELETE 작업을 완료합니다.|  
|`FillError`|`Fill` 작업 중에 오류가 발생했습니다.|  
  
## <a name="rowupdating-and-rowupdated"></a>RowUpdating 및 RowUpdated  
 `RowUpdating`은 <xref:System.Data.DataSet>의 행 업데이트가 데이터 소스에서 처리되기 전에 발생합니다. `RowUpdated`는 `DataSet`의 행 업데이트가 데이터 소스에서 처리된 후에 발생합니다. 결과적으로 `RowUpdating`을 사용하면 업데이트가 발생하기 전에 업데이트 동작을 수정하거나, 업데이트가 발생할 경우 추가 처리 방법을 제공하거나, 업데이트된 행에 대한 참조를 유지하거나, 현재 업데이트를 취소하고 일괄 프로세스로 나중에 처리하도록 예약하는 것과 같은 작업을 수행할 수 있습니다. `RowUpdated`는 업데이트 중에 발생하는 오류와 예외에 응답하는 데 유용합니다. 재시도 논리 등은 물론이고 오류 정보도 `DataSet`에 추가할 수 있습니다.  
  
 <xref:System.Data.Common.RowUpdatingEventArgs> 및 <xref:System.Data.Common.RowUpdatedEventArgs> 이벤트로 전달되는 `RowUpdating` 및 `RowUpdated` 인수에는 업데이트를 수행하는 데 사용되는 `Command` 개체를 참조하는 `Command` 속성, 업데이트된 정보가 포함된 `Row` 개체를 참조하는 `DataRow` 속성, 수행되는 업데이트 형식을 나타내는 `StatementType` 속성, `TableMapping` 속성(해당되는 경우) 및 작업의 `Status` 속성이 있습니다.  
  
 `Status` 속성을 사용하면 작업 중에 오류가 발생했는지 확인하여 필요할 경우 현재 행 및 결과 행에 대한 동작을 제어할 수 있습니다. 이벤트가 발생할 때 `Status` 속성은 `Continue` 또는 `ErrorsOccurred`와 같습니다. 다음 표에서는 업데이트하는 동안 후속 동작을 제어하기 위해 설정할 수 있는 `Status` 속성 값을 보여 줍니다.  
  
|Status|Description|  
|------------|-----------------|  
|`Continue`|업데이트 작업을 계속합니다.|  
|`ErrorsOccurred`|업데이트 작업을 중단하고 예외를 throw합니다.|  
|`SkipCurrentRow`|현재 행을 무시하고 업데이트 작업을 계속합니다.|  
|`SkipAllRemainingRows`|업데이트 작업을 중단하지만 예외를 throw하지 않습니다.|  
  
 `Status` 속성을 `ErrorsOccurred`로 설정하면 예외가 throw됩니다. `Errors` 속성을 설정하면 원하는 예외를 throw하도록 제어할 수 있습니다. `Status`에 대해 다른 값 중 하나를 사용하면 예외가 throw되지 않습니다.  
  
 또한 `ContinueUpdateOnError` 속성을 사용하여 업데이트된 행의 오류를 처리할 수 있습니다. `DataAdapter.ContinueUpdateOnError`가 `true`인 경우 행을 업데이트한 결과로 예외가 throw되면 예외 텍스트가 특정 행의 `RowError` 정보에 배치되고 예외가 throw되지 않은 상태에서 계속 처리됩니다. 이렇게 하면 오류 발생 시 이에 응답할 수 있도록 하는 `RowUpdated``Update`와는 달리, 가 완료될 때 오류에 응답할 수 있습니다.  
  
 다음 코드 샘플에서는 이벤트 처리기를 추가 및 제거하는 방법을 보여 줍니다. `RowUpdating` 이벤트 처리기는 타임스탬프를 사용하여 삭제된 모든 레코드의 로그를 기록합니다. 이벤트 `RowUpdated` 처리기는에서 행 `DataSet`의 `RowError` 속성에 오류 정보를 추가 하 고 예외를 표시 하지 않으며 처리 (의 `ContinueUpdateOnError`  =  `true`동작 미러링)를 계속 합니다.  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim custAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers", connection)  
  
' Add handlers.  
AddHandler custAdapter.RowUpdating, New SqlRowUpdatingEventHandler( _  
  AddressOf OnRowUpdating)  
AddHandler custAdapter.RowUpdated, New SqlRowUpdatedEventHandler(  
  AddressOf OnRowUpdated)  
  
' Set DataAdapter command properties, fill DataSet, and modify DataSet.  
  
custAdapter.Update(custDS, "Customers")  
  
' Remove handlers.  
RemoveHandler custAdapter.RowUpdating, _  
  New SqlRowUpdatingEventHandler(AddressOf OnRowUpdating)  
RemoveHandler custAdapter.RowUpdated, _  
  New SqlRowUpdatedEventHandler(AddressOf OnRowUpdated)  
  
Private Shared Sub OnRowUpdating(sender As Object, _  
  args As SqlRowUpdatingEventArgs)  
  If args.StatementType = StatementType.Delete Then  
    Dim tw As System.IO.TextWriter = _  
  System.IO.File.AppendText("Deletes.log")  
    tw.WriteLine( _  
      "{0}: Customer {1} Deleted.", DateTime.Now, args.Row(_  
      "CustomerID", DataRowVersion.Original))  
    tw.Close()  
  End If  
End Sub  
  
Private Shared Sub OnRowUpdated( _  
  sender As Object, args As SqlRowUpdatedEventArgs)  
  If args.Status = UpdateStatus.ErrorsOccurred  
    args.Status = UpdateStatus.SkipCurrentRow  
    args.Row.RowError = args.Errors.Message  
  End If  
End Sub  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
SqlDataAdapter custAdapter = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers", connection);  
  
// Add handlers.  
custAdapter.RowUpdating += new SqlRowUpdatingEventHandler(OnRowUpdating);  
custAdapter.RowUpdated += new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
// Set DataAdapter command properties, fill DataSet, modify DataSet.  
  
custAdapter.Update(custDS, "Customers");  
  
// Remove handlers.  
custAdapter.RowUpdating -= new SqlRowUpdatingEventHandler(OnRowUpdating);  
custAdapter.RowUpdated -= new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
protected static void OnRowUpdating(  
  object sender, SqlRowUpdatingEventArgs args)  
{  
  if (args.StatementType == StatementType.Delete)  
  {  
    System.IO.TextWriter tw = System.IO.File.AppendText("Deletes.log");  
    tw.WriteLine(  
      "{0}: Customer {1} Deleted.", DateTime.Now,   
       args.Row["CustomerID", DataRowVersion.Original]);  
    tw.Close();  
  }  
}  
  
protected static void OnRowUpdated(  
  object sender, SqlRowUpdatedEventArgs args)  
{  
  if (args.Status == UpdateStatus.ErrorsOccurred)  
  {  
    args.Row.RowError = args.Errors.Message;  
    args.Status = UpdateStatus.SkipCurrentRow;  
  }  
}  
```  
  
## <a name="fillerror"></a>FillError  
 `FillError``DataAdapter`는 `Fill` 작업 중에 오류가 발생하면  이벤트를 발생시킵니다. 이런 형식의 오류는 추가 중인 행의 데이터를 정밀도의 손실 없이 .NET Framework 형식으로 변환할 수 없을 때 흔히 발생합니다.  
  
 `DataTable``Fill` 작업 중에 오류가 발생하면 현재 행이 에 추가되지 않습니다. `FillError` 이벤트를 사용하여 오류를 해결하고 행을 추가하거나, 제외된 행을 무시하고 `Fill` 작업을 계속할 수 있습니다.  
  
 `FillError``FillErrorEventArgs` 이벤트에 전달된 에는 오류에 응답하고 오류를 해결할 수 있는 몇 가지 속성이 포함될 수 있습니다. 다음 표에서는 `FillErrorEventArgs` 개체의 속성을 보여 줍니다.  
  
|속성|Description|  
|--------------|-----------------|  
|`Errors`|발생한 `Exception`입니다.|  
|`DataTable`|오류가 발생했을 때 채워지고 있던 `DataTable` 개체입니다.|  
|`Values`|오류가 발생했을 때 추가되고 있던 행의 값을 포함하는 개체 배열입니다. `Values` 배열의 서수 참조는 추가되고 있던 행의 열에 대한 서수 참조에 해당합니다. 예를 들어, `Values[0]`은 행의 첫째 열로 추가되고 있던 값입니다.|  
|`Continue`|예외를 throw할 것인지 여부를 선택하도록 합니다. `false``Continue` 속성을 `Fill`로 설정하면 현재  작업이 중단되고 예외가 throw됩니다. `Continue`를 `true`로 설정하면 오류가 발생하더라도 `Fill` 작업이 계속됩니다.|  
  
 다음 코드 예제에서는 `FillError`의 `DataAdapter` 이벤트에 이벤트 처리기를 추가합니다. 이 예제에서는 `FillError` 이벤트 코드에서 정밀도가 손실될 가능성이 있는지 확인하여 예외에 응답할 수 있도록 합니다.  
  
```vb  
AddHandler adapter.FillError, New FillErrorEventHandler( _  
  AddressOf FillError)  
  
Dim dataSet As DataSet = New DataSet  
adapter.Fill(dataSet, "ThisTable")  
  
Private Shared Sub FillError(sender As Object, _  
  args As FillErrorEventArgs)  
  If args.Errors.GetType() Is Type.GetType("System.OverflowException") Then  
    ' Code to handle precision loss.  
    ' Add a row to table using the values from the first two columns.  
    DataRow myRow = args.DataTable.Rows.Add(New Object() _  
      {args.Values(0), args.Values(1), DBNull.Value})  
    ' Set the RowError containing the value for the third column.  
    myRow.RowError = _  
      "OverflowException encountered. Value from data source: " & _  
      args.Values(2)  
    args.Continue = True  
  End If  
End Sub  
```  
  
```csharp  
adapter.FillError += new FillErrorEventHandler(FillError);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "ThisTable");  
  
protected static void FillError(object sender, FillErrorEventArgs args)  
{  
  if (args.Errors.GetType() == typeof(System.OverflowException))  
  {  
    // Code to handle precision loss.  
    //Add a row to table using the values from the first two columns.  
    DataRow myRow = args.DataTable.Rows.Add(new object[]  
       {args.Values[0], args.Values[1], DBNull.Value});  
    //Set the RowError containing the value for the third column.  
    myRow.RowError =   
       "OverflowException Encountered. Value from data source: " +  
       args.Values[2];  
    args.Continue = true;  
  }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [데이터 집합 이벤트 처리](./dataset-datatable-dataview/handling-dataset-events.md)
- [DataTable 이벤트 처리](./dataset-datatable-dataview/handling-datatable-events.md)
- [이벤트](../../../standard/events/index.md)
- [ADO.NET 개요](ado-net-overview.md)
