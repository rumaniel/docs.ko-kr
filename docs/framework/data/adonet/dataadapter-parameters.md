---
title: DataAdapter 매개 변수
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f21e6aba-b76d-46ad-a83e-2ad8e0af1e12
ms.openlocfilehash: 83fc3101b0eb428def6cbc446e634e9bb45de350
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785601"
---
# <a name="dataadapter-parameters"></a>DataAdapter 매개 변수
<xref:System.Data.Common.DbDataAdapter>에는 데이터 소스에서 데이터를 검색하고 업데이트하는 데 사용되는 다음과 같은 네 가지 속성이 있습니다. <xref:System.Data.Common.DbDataAdapter.SelectCommand%2A> 속성은 데이터 소스에서 데이터를 반환하며 <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A> , <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 및 <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> 속성은 데이터 소스에서 변경 내용을 관리하는 데 사용됩니다. `SelectCommand` 속성은 `Fill`의 `DataAdapter` 메서드를 호출하기 전에 설정해야 합니다. `InsertCommand`, `UpdateCommand` 또는 `DeleteCommand` 속성은 `Update`의 `DataAdapter` 메서드가 호출되기 전에 설정해야 하며, <xref:System.Data.DataTable>의 데이터에 적용된 변경 내용에 따라 설정 값이 달라집니다. 예를 들어, 행이 추가되었으면 `InsertCommand`를 호출하기 전에 `Update`를 설정해야 합니다. `Update`가 삽입, 업데이트 또는 삭제된 행을 처리하는 동안 `DataAdapter`는 해당 `Command` 속성을 사용하여 동작을 처리합니다. 수정된 행에 대한 현재 정보는 `Command` 컬렉션을 통해 `Parameters` 개체에 전달됩니다.  
  
 데이터 원본에서 행을 업데이트 하는 경우 업데이트할 테이블의 행을 식별 하는 고유 식별자를 사용 하는 UPDATE 문을 호출 합니다. 고유 식별자란 대개 기본 키 필드의 값을 말합니다. UPDATE 문은 다음의 Transact-SQL 문과 같이 고유 식별자와 업데이트된 열 및 값을 모두 포함하는 매개 변수를 사용합니다.  
  
```sql
UPDATE Customers SET CompanyName = @CompanyName   
  WHERE CustomerID = @CustomerID  
```  
  
> [!NOTE]
> 매개 변수 자리 표시자의 구문은 데이터 소스에 따라 다릅니다. 이 예제에서는 SQL Server 데이터 소스용 자리 표시자를 보여 줍니다. <xref:System.Data.OleDb> 및 <xref:System.Data.Odbc> 매개 변수의 경우 물음표(?) 자리 표시자를 사용합니다.  
  
 이 Visual Basic 예제에서 필드는 `CompanyName` `@CustomerID` 매개 변수의 값과 `CustomerID` 같은 행의 `@CompanyName` 매개 변수 값으로 업데이트 됩니다. 매개 변수는 <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A> <xref:System.Data.SqlClient.SqlParameter> 개체의 속성을 사용 하 여 수정 된 행에서 정보를 검색 합니다. 다음은 앞에 나온 샘플 UPDATE 문에 대한 매개 변수입니다. 이 코드에서는 `adapter` 변수가 올바른 <xref:System.Data.SqlClient.SqlDataAdapter> 개체를 나타낸다고 가정합니다.  
  
```vb
adapter.Parameters.Add( _  
  "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
Dim parameter As SqlParameter = _  
  adapter.UpdateCommand.Parameters.Add("@CustomerID", _  
  SqlDbType.NChar, 5, "CustomerID")  
parameter.SourceVersion = DataRowVersion.Original  
```  
  
 `Add` 컬렉션의 `Parameters` 메서드는 매개 변수 이름, 데이터 형식, 크기(해당 형식에 적용되는 경우) 및 <xref:System.Data.Common.DbParameter.SourceColumn%2A>의 `DataTable` 이름을 사용합니다. <xref:System.Data.Common.DbParameter.SourceVersion%2A> 매개 변수의 `@CustomerID`은 `Original`로 설정됩니다. 그러면 식별하는 열 값이 수정된 <xref:System.Data.DataRow>에서 변경된 경우 데이터 소스의 기존 행이 업데이트됩니다. 이 경우 `Original` 행 값은 데이터 소스의 현재 값과 일치하고 `Current` 행 값에는 업데이트된 값이 포함됩니다. `SourceVersion` 매개 변수의 `@CompanyName`은 설정되어 있지 않으므로 기본값인 `Current` 행 값을 사용합니다.  
  
> [!NOTE]
> 의 `Fill` 작업과 `DataAdapter` 의 메서드`DataReader`모두.NET Framework 형식은 .NET Framework 데이터 공급자에서 반환 된 형식에서 유추 됩니다. `Get` Microsoft SQL Server, OLE DB 및 ODBC 데이터 형식에 대 한 유추 된 .NET Framework 형식 및 접근자 메서드는 [ADO.NET의 데이터 형식 매핑](data-type-mappings-in-ado-net.md)에 설명 되어 있습니다.  
  
## <a name="parametersourcecolumn-parametersourceversion"></a>Parameter.SourceColumn, Parameter.SourceVersion  
 `SourceColumn` 및 `SourceVersion`은 `Parameter` 생성자에 인수로 전달되거나 기존 `Parameter`의 속성으로 설정될 수 있습니다. `SourceColumn`은 <xref:System.Data.DataColumn> 값이 검색될 <xref:System.Data.DataRow>의 `Parameter` 이름입니다. `SourceVersion`에서는 `DataRow`가 값을 검색하기 위해 사용하는 `DataAdapter` 버전을 지정합니다.  
  
 다음 표에서는 <xref:System.Data.DataRowVersion>에 사용할 수 있는 `SourceVersion` 열거형 값을 보여 줍니다.  
  
|DataRowVersion 열거형|Description|  
|--------------------------------|-----------------|  
|`Current`|열의 현재 값을 사용하는 매개 변수입니다. 기본값입니다.|  
|`Default`|열의 `DefaultValue`를 사용하는 매개 변수입니다.|  
|`Original`|열의 원래 값을 사용하는 매개 변수입니다.|  
|`Proposed`|제안된 값을 사용하는 매개 변수입니다.|  
  
 다음 단원의 `SqlClient` 코드 예제에서는 <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 열이 두 매개 변수 `CustomerID`(`SourceColumn`) 및 `@CustomerID` (`SET CustomerID = @CustomerID`)에 대한 `@OldCustomerID`으로 사용되는 `WHERE CustomerID = @OldCustomerID`의 매개 변수를 정의합니다. 매개 변수는 **CustomerID** 열을의 `DataRow`현재 값으로 업데이트 하는 데 사용 됩니다. `@CustomerID` 결과적 `CustomerID` 으로이`Current` 인 이`SourceVersion`사용됩니다. `SourceColumn` `@OldCustomerID` 매개 변수는 데이터 소스에서 현재 행을 식별 하는 데 사용 됩니다. 행의 `Original` 버전에 일치하는 열 값이 있으므로 `SourceColumn`이 `CustomerID`인 동일한 `SourceVersion`(`Original`)이 사용됩니다.  
  
## <a name="working-with-sqlclient-parameters"></a>SqlClient 매개 변수 사용  
 다음 예제에서는 데이터베이스에서 추가적인 스키마 정보를 검색하기 위해 <xref:System.Data.SqlClient.SqlDataAdapter>를 만들고 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A>을 <xref:System.Data.MissingSchemaAction.AddWithKey>로 설정하는 방법을 보여 줍니다. <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> 및 <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> 속성이 설정되고 해당 <xref:System.Data.SqlClient.SqlParameter> 개체가 <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> 컬렉션에 추가됩니다. 메서드에서 `SqlDataAdapter` 개체를 반환합니다.  
  
 [!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/CS/source.cs#1)]
 [!code-vb[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/VB/source.vb#1)]  
  
## <a name="oledb-parameter-placeholders"></a>OleDb 매개 변수 자리 표시자  
 <xref:System.Data.OleDb.OleDbDataAdapter> 및 <xref:System.Data.Odbc.OdbcDataAdapter> 개체의 경우 물음표(?) 자리 표시자를 사용하여 매개 변수를 식별해야 합니다.  
  
```vb  
Dim selectSQL As String = _  
  "SELECT CustomerID, CompanyName FROM Customers " & _  
  "WHERE CountryRegion = ? AND City = ?"  
Dim insertSQL AS String = _  
  "INSERT INTO Customers (CustomerID, CompanyName) VALUES (?, ?)"  
Dim updateSQL AS String = _  
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " & _  
  WHERE CustomerID = ?"  
Dim deleteSQL As String = "DELETE FROM Customers WHERE CustomerID = ?"  
```  
  
```csharp  
string selectSQL =   
  "SELECT CustomerID, CompanyName FROM Customers " +  
  "WHERE CountryRegion = ? AND City = ?";  
string insertSQL =   
  "INSERT INTO Customers (CustomerID, CompanyName) " +  
  "VALUES (?, ?)";  
string updateSQL =   
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " +  
  "WHERE CustomerID = ? ";  
string deleteSQL = "DELETE FROM Customers WHERE CustomerID = ?";  
```  
  
 매개 변수가 있는 쿼리 문에서는 만들어야 할 입력 및 출력 매개 변수를 정의합니다. 매개 변수를 만들려면 `Parameters.Add` 메서드나 `Parameter` 생성자를 사용하여 열 이름, 데이터 형식 및 크기를 지정합니다. `Integer`와 같은 내장 데이터 형식의 경우 크기를 포함할 필요가 없거나 기본 크기를 지정할 수 있습니다.  
  
 다음 코드 예제에서는 SQL 문에 대한 매개 변수를 만들고 `DataSet`을 채웁니다.  
  
## <a name="oledb-example"></a>OleDb 예제  
  
```vb  
' Assumes that connection is a valid OleDbConnection object.  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter   
  
Dim selectCMD AS OleDbCommand = New OleDbCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add parameters and set values.  
selectCMD.Parameters.Add( _  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add( _  
  "@City", OleDbType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
```  
  
```csharp  
// Assumes that connection is a valid OleDbConnection object.  
OleDbDataAdapter adapter = new OleDbDataAdapter();  
  
OleDbCommand selectCMD = new OleDbCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
// Add parameters and set values.  
selectCMD.Parameters.Add(  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add(  
  "@City", OleDbType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
## <a name="odbc-parameters"></a>Odbc 매개 변수  
  
```vb  
' Assumes that connection is a valid OdbcConnection object.  
Dim adapter As OdbcDataAdapter = New OdbcDataAdapter  
  
Dim selectCMD AS OdbcCommand = New OdbcCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
```  
  
```csharp  
// Assumes that connection is a valid OdbcConnection object.  
OdbcDataAdapter adapter = new OdbcDataAdapter();  
  
OdbcCommand selectCMD = new OdbcCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
//Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
> 매개 변수에 대 한 매개 변수 이름을 제공 하지 않으면 매개 변수에는 "Parameter1"로 시작 *하* 는 매개 변수*N* 의 증분 기본 이름이 지정 됩니다. 매개 변수 이름을 제공 하는 경우 매개 변수*N* 명명 규칙을 사용 하지 않는 것이 좋습니다 `ParameterCollection`.이 경우 사용자가 제공 하는 이름이의 기존 기본 매개 변수 이름과 충돌할 수 있기 때문입니다. 이미 있는 이름을 입력하면 예외가 throw됩니다.  
  
## <a name="see-also"></a>참고자료

- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [명령 및 매개 변수](commands-and-parameters.md)
- [DataAdapter로 데이터 원본 업데이트](updating-data-sources-with-dataadapters.md)
- [저장 프로시저로 데이터 수정](modifying-data-with-stored-procedures.md)
- [ADO.NET에서 데이터 형식 매핑](data-type-mappings-in-ado-net.md)
- [ADO.NET 개요](ado-net-overview.md)
