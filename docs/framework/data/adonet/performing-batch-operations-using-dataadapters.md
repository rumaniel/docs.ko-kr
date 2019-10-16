---
title: DataAdapter를 사용하여 일괄 작업 수행
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e72ed5af-b24f-486c-8429-c8fd2208f844
ms.openlocfilehash: 8667cffb032daf0043915d3bee7127ef9b70756b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794511"
---
# <a name="performing-batch-operations-using-dataadapters"></a>DataAdapter를 사용하여 일괄 작업 수행
ADO.NET의 배치 지원을 사용하면 <xref:System.Data.Common.DataAdapter>를 통해 INSERT, UPDATE 및 DELETE 작업을 한 번에 하나씩 보내지 않고 <xref:System.Data.DataSet> 또는 <xref:System.Data.DataTable>에서 서버로 그룹화할 수 있습니다. 서버로의 라운드트립 횟수가 줄어들면 일반적으로 성능이 크게 개선됩니다. 배치 업데이트는 SQL Server(<xref:System.Data.SqlClient>) 및 Oracle(<xref:System.Data.OracleClient>)용 .NET 데이터 공급자에서 지원됩니다.  
  
 이전 버전의 ADO.NET에서는 데이터베이스를 <xref:System.Data.DataSet>의 변경 내용으로 업데이트하는 경우 `Update`의 `DataAdapter` 메서드에서 데이터베이스에 대해 한 번에 한 행씩 업데이트를 수행했습니다. 또한 지정한 <xref:System.Data.DataTable>의 행에서 반복될 때 수정되었는지 여부를 확인하기 위해 각 <xref:System.Data.DataRow>를 검사했습니다. 행이 수정된 경우에는 해당 행의 `UpdateCommand` 속성 값에 따라 적절한 `InsertCommand`, `DeleteCommand` 또는 <xref:System.Data.DataRow.RowState%2A>를 호출했습니다. 그리고 행을 업데이트할 때마다 데이터베이스에 대한 네트워크 라운드트립이 수반되었습니다.  
  
 ADO.NET 2.0부터는 <xref:System.Data.Common.DbDataAdapter>가 <xref:System.Data.Common.DbDataAdapter.UpdateBatchSize%2A> 속성을 노출합니다. `UpdateBatchSize`를 양의 정수 값으로 설정하면 데이터베이스에 대한 업데이트가 지정된 크기의 배치로 전송됩니다. 예를 들어 `UpdateBatchSize`를 10으로 설정하면 10개의 개별적인 문을 그룹화하여 하나의 배치로 제출합니다. `UpdateBatchSize`를 0으로 설정하면 <xref:System.Data.Common.DataAdapter>가 서버에서 처리할 수 있는 최대 배치 크기를 사용합니다. 1로 설정할 경우에는 행이 한 번에 하나씩 전송되므로 배치 업데이트를 사용할 수 없습니다.  
  
 너무 큰 배치를 실행하면 성능이 저하될 수 있습니다. 따라서 애플리케이션을 구현하기 전에 최적의 배치 크기 설정을 테스트해야 합니다.  
  
## <a name="using-the-updatebatchsize-property"></a>UpdateBatchSize 속성 사용  
 배치 업데이트를 사용할 수 있을 때는 DataAdapter <xref:System.Data.IDbCommand.UpdatedRowSource%2A>, `UpdateCommand` 및 `InsertCommand`의 `DeleteCommand` 속성 값을 <xref:System.Data.UpdateRowSource.None> 또는 <xref:System.Data.UpdateRowSource.OutputParameters>로 설정해야 합니다. 배치 업데이트를 수행하는 경우 명령의 <xref:System.Data.IDbCommand.UpdatedRowSource%2A> 속성 값 <xref:System.Data.UpdateRowSource.FirstReturnedRecord> 또는 <xref:System.Data.UpdateRowSource.Both>는 유효하지 않습니다.  
  
 다음 프로시저에서는 `UpdateBatchSize` 속성을 사용하는 방법을 보여 줍니다. 이 프로시저는 두 개의 인수, <xref:System.Data.DataSet> 즉 **Production category** 테이블의 **제품 categoryid** 및 **Name** 필드를 나타내는 열을 포함 하는 개체와 일괄 처리 크기를 나타내는 정수 ( 일괄 처리의 행). 이 코드에서는 <xref:System.Data.SqlClient.SqlDataAdapter>, <xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> 및 <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> 속성을 설정하여 새 <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> 개체를 만듭니다. 또한 <xref:System.Data.DataSet> 개체에 수정된 행이 있다고 가정합니다. 그리고 `UpdateBatchSize` 속성을 설정한 다음 업데이트를 실행합니다.  
  
```vb  
Public Sub BatchUpdate( _  
  ByVal dataTable As DataTable, ByVal batchSize As Int32)  
    ' Assumes GetConnectionString() returns a valid connection string.  
    Dim connectionString As String = GetConnectionString()  
  
    ' Connect to the AdventureWorks database.  
    Using connection As New SqlConnection(connectionString)  
        ' Create a SqlDataAdapter.  
        Dim adapter As New SqlDataAdapter()  
  
        'Set the UPDATE command and parameters.  
        adapter.UpdateCommand = New SqlCommand( _  
          "UPDATE Production.ProductCategory SET " _  
          & "Name=@Name WHERE ProductCategoryID=@ProdCatID;", _  
          connection)  
        adapter.UpdateCommand.Parameters.Add("@Name", _  
          SqlDbType.NVarChar, 50, "Name")  
        adapter.UpdateCommand.Parameters.Add("@ProdCatID",  _  
          SqlDbType.Int, 4, " ProductCategoryID ")  
        adapter.UpdateCommand.UpdatedRowSource = _  
          UpdateRowSource.None  
  
        'Set the INSERT command and parameter.  
        adapter.InsertCommand = New SqlCommand( _  
          "INSERT INTO Production.ProductCategory (Name) VALUES (@Name);", _  
  connection)  
        adapter.InsertCommand.Parameters.Add("@Name", _  
          SqlDbType.NVarChar, 50, "Name")  
        adapter.InsertCommand.UpdatedRowSource = _  
          UpdateRowSource.None  
  
        'Set the DELETE command and parameter.  
        adapter.DeleteCommand = New SqlCommand( _  
          "DELETE FROM Production.ProductCategory " _  
          & "WHERE ProductCategoryID=@ProdCatID;", connection)  
        adapter.DeleteCommand.Parameters.Add("@ProdCatID", _  
           SqlDbType.Int, 4, " ProductCategoryID ")  
        adapter.DeleteCommand.UpdatedRowSource = UpdateRowSource.None  
  
        ' Set the batch size.  
        adapter.UpdateBatchSize = batchSize  
  
        ' Execute the update.  
        adapter.Update(dataTable)  
    End Using  
End Sub  
```  
  
```csharp  
public static void BatchUpdate(DataTable dataTable,Int32 batchSize)  
{  
    // Assumes GetConnectionString() returns a valid connection string.  
    string connectionString = GetConnectionString();  
  
    // Connect to the AdventureWorks database.  
    using (SqlConnection connection = new   
      SqlConnection(connectionString))  
    {  
  
        // Create a SqlDataAdapter.  
        SqlDataAdapter adapter = new SqlDataAdapter();  
  
        // Set the UPDATE command and parameters.  
        adapter.UpdateCommand = new SqlCommand(  
            "UPDATE Production.ProductCategory SET "  
            + "Name=@Name WHERE ProductCategoryID=@ProdCatID;",   
            connection);  
        adapter.UpdateCommand.Parameters.Add("@Name",   
           SqlDbType.NVarChar, 50, "Name");  
        adapter.UpdateCommand.Parameters.Add("@ProdCatID",   
           SqlDbType.Int, 4, "ProductCategoryID");  
         adapter.UpdateCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the INSERT command and parameter.  
        adapter.InsertCommand = new SqlCommand(  
            "INSERT INTO Production.ProductCategory (Name) VALUES (@Name);",   
            connection);  
        adapter.InsertCommand.Parameters.Add("@Name",   
          SqlDbType.NVarChar, 50, "Name");  
        adapter.InsertCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the DELETE command and parameter.  
        adapter.DeleteCommand = new SqlCommand(  
            "DELETE FROM Production.ProductCategory "  
            + "WHERE ProductCategoryID=@ProdCatID;", connection);  
        adapter.DeleteCommand.Parameters.Add("@ProdCatID",   
          SqlDbType.Int, 4, "ProductCategoryID");  
        adapter.DeleteCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the batch size.  
        adapter.UpdateBatchSize = batchSize;  
  
        // Execute the update.  
        adapter.Update(dataTable);  
    }  
}  
```  
  
## <a name="handling-batch-update-related-events-and-errors"></a>배치 업데이트 관련 이벤트 및 오류 처리  
 **DataAdapter** 에는 두 가지 업데이트 관련 이벤트가 있습니다. **RowUpdating** 및 **RowUpdated**. 이전 버전의 ADO.NET에서 일괄 처리가 비활성화되어 있는 경우 각 이벤트는 처리되는 각 행마다 생성됩니다. 업데이트를 수행 하기 전에 **RowUpdating** 이 생성 되 고 데이터베이스 업데이트가 완료 된 후 **RowUpdated** 이 생성 됩니다.  
  
### <a name="event-behavior-changes-with-batch-updates"></a>배치 업데이트에 따른 이벤트 동작 변경  
 일괄 처리가 활성화되면 한 번의 데이터베이스 동작으로 여러 개의 행이 업데이트됩니다. 따라서 `RowUpdated` 이벤트는 배치마다 한 번씩만 발생하지만 `RowUpdating` 이벤트는 행이 처리될 때마다 발생합니다. 일괄 처리가 비활성화되면 일대일 인터리빙으로 두 개의 이벤트가 발생합니다. 이 경우 `RowUpdating` 이벤트 하나와 `RowUpdated` 이벤트 하나가 한 행에 대해 발생한 후 모든 행이 처리될 때까지 `RowUpdating` 및 `RowUpdated` 이벤트가 다음 행에 대해 하나씩 발생합니다.  
  
### <a name="accessing-updated-rows"></a>업데이트된 행 액세스  
 일괄 처리가 비활성화되면 <xref:System.Data.Common.RowUpdatedEventArgs.Row%2A> 클래스의 <xref:System.Data.Common.RowUpdatedEventArgs> 속성을 사용하여 업데이트되는 행에 액세스할 수 있습니다.  
  
 일괄 처리가 활성화되면 여러 행에 대해 하나의 `RowUpdated` 이벤트가 생성됩니다. 따라서 각 행에 대한 `Row` 속성 값은 null입니다. `RowUpdating` 이벤트는 계속해서 각 행에 대해 생성됩니다. <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A> 클래스의 <xref:System.Data.Common.RowUpdatedEventArgs> 메서드를 사용하면 행에 대한 참조를 배열에 복사하여 처리된 행에 액세스할 수 있습니다. 처리 중인 행이 없으면 `CopyToRows`에서 <xref:System.ArgumentNullException>이 throw됩니다. <xref:System.Data.Common.RowUpdatedEventArgs.RowCount%2A> 메서드를 호출하기 전에 <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A> 속성을 사용하여 처리된 행 수를 반환합니다.  
  
### <a name="handling-data-errors"></a>데이터 오류 처리  
 배치를 실행하면 각각의 개별 문을 실행하는 것과 동일한 효과가 나타납니다. 문은 배치에 추가된 순서대로 실행됩니다. 오류는 배치 모드가 비활성화되어 있는 상태와 동일하게 처리됩니다. 행은 각각 개별적으로 처리됩니다. 데이터베이스에서 성공적으로 처리된 행만 <xref:System.Data.DataRow> 내의 해당 <xref:System.Data.DataTable>에서 업데이트됩니다.  
  
 데이터 공급자 및 백 엔드 데이터베이스 서버는 배치 실행에 지원되는 SQL 구문을 결정합니다. 실행을 위해 지원되지 않는 문을 전송하면 예외가 throw될 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [DataAdapter로 데이터 원본 업데이트](updating-data-sources-with-dataadapters.md)
- [DataAdapter 이벤트 처리](handling-dataadapter-events.md)
- [ADO.NET 개요](ado-net-overview.md)
