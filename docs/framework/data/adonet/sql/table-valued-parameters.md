---
title: 테이블 반환 매개 변수
ms.date: 10/12/2018
dev_langs:
- csharp
- vb
ms.assetid: 370c16d5-db7b-43e3-945b-ccaab35b739b
ms.openlocfilehash: 6c01453556a71925c322e9f9aef8065cbddb3540
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894385"
---
# <a name="table-valued-parameters"></a>테이블 반환 매개 변수
테이블 반환 매개 변수를 사용하면 클라이언트 애플리케이션에서 여러 행 데이터를 반복적인 라운드트립이나 데이터 처리를 위한 특수한 서버측 논리를 사용하지 않고도 SQL Server로 쉽게 마샬링할 수 있습니다. 또한 테이블 반환 매개 변수를 사용하면 클라이언트 애플리케이션에서 데이터 행을 캡슐화하여 매개 변수화된 단일 명령을 통해 데이터를 서버에 보낼 수 있습니다. 들어오는 데이터 행은 테이블 변수에 저장되며, 이러한 테이블 변수에 대해서는 Transact-SQL을 사용하여 작업할 수 있습니다.  
  
 테이블 반환 매개 변수의 열 값은 표준 Transact-SQL SELECT 문을 사용하여 액세스할 수 있습니다. 테이블 반환 매개 변수는 강력한 형식이며 해당 구조체의 유효성은 자동으로 검사됩니다. 테이블 반환 매개 변수의 크기는 서버 메모리 크기의 제한만 받습니다.  
  
> [!NOTE]
> 데이터를 테이블 반환 매개 변수로 반환할 수 없습니다. 테이블 반환 매개 변수는 입력 전용이며 OUTPUT 키워드를 지원하지 않습니다.  
  
 테이블 반환 매개 변수에 대한 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|SQL Server 온라인 설명서의 [테이블 반환 매개 변수 (데이터베이스 엔진)](https://go.microsoft.com/fwlink/?LinkId=98363)|테이블 반환 매개 변수를 만들고 사용하는 방법에 대해 설명합니다.|  
|SQL Server 온라인 설명서의 [사용자 정의 테이블 형식](https://go.microsoft.com/fwlink/?LinkId=98364)|테이블 반환 매개 변수를 선언하는 데 사용되는 사용자 정의 테이블 형식에 대해 설명합니다.|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>이전 버전의 SQL Server에서 여러 행 전달  
 SQL Server 2008에 대 한 테이블 반환 매개 변수가 도입 되기 전에는 여러 행의 데이터를 저장 프로시저나 매개 변수화 된 SQL 명령에 전달 하는 옵션이 제한 되었습니다. 개발자는 서버에 여러 행을 전달하기 위해 다음 옵션 중에서 선택할 수 있었습니다.  
  
- 여러 데이터 열과 행의 값을 나타내는 일련의 개별 매개 변수를 사용합니다. 이 방법을 사용하여 전달할 수 있는 데이터의 양은 허용되는 매개 변수 수로 제한됩니다. SQL Server 프로시저에는 매개 변수를 2100개까지 사용할 수 있습니다. 이러한 개별 값을 테이블 변수 또는 처리를 위한 임시 테이블로 어셈블하기 위한 서버측 논리가 필요합니다.  
  
- 여러 데이터 값을 구분된 문자열 또는 XML 문서로 묶은 후 이러한 텍스트 값을 프로시저나 문에 전달합니다. 이렇게 하려면 데이터 구조의 유효성을 검사하고 묶인 값을 해제하는 논리를 프로시저나 문에 포함해야 합니다.  
  
- `Update`의 <xref:System.Data.SqlClient.SqlDataAdapter> 메서드를 호출하여 생성된 것과 같이 여러 행에 영향을 주는 데이터 수정을 위한 일련의 개별 SQL 문을 만듭니다. 변경 내용은 서버에 개별적으로 제출하거나 그룹으로 일괄 처리할 수 있습니다. 그러나 문이 여러 개 포함된 일괄 처리로 제출하더라도 각 문은 서버에서 개별적으로 실행됩니다.  
  
- `bcp` 유틸리티 프로그램이나 <xref:System.Data.SqlClient.SqlBulkCopy> 개체를 사용하여 여러 데이터 행을 테이블에 로드합니다. 이 기술은 매우 효율적이기는 하지만 데이터를 임시 테이블이나 테이블 변수에 로드해야만 서버측 처리가 지원됩니다.  
  
## <a name="creating-table-valued-parameter-types"></a>테이블 반환 매개 변수 형식 만들기  
 테이블 반환 매개 변수는 Transact-SQL CREATE TYPE 문을 사용하여 정의된 강력한 형식의 테이블 구조를 기반으로 합니다. 클라이언트 애플리케이션에서 테이블 반환 매개 변수를 사용할 수 있으려면 먼저 SQL Server에서 테이블 형식을 만들고 구조를 정의해야 합니다. 테이블 형식을 만드는 방법에 대 한 자세한 내용은 SQL Server 온라인 설명서에서 [사용자 정의 테이블 형식](https://go.microsoft.com/fwlink/?LinkID=98364) 을 참조 하세요.  
  
 다음 문은 이름이 CategoryTableType이고 CategoryID 및 CategoryName 열로 구성된 테이블 형식을 만듭니다.  
  
```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 테이블 형식을 만든 후에는 해당 형식에 기반하여 테이블 반환 매개 변수를 선언할 수 있습니다. 다음 Transact-SQL 조각은 저장 프로시저 정의에 테이블 반환 매개 변수를 선언하는 방법을 보여 줍니다. READONLY 키워드는 테이블 반환 매개 변수를 선언하는 데 필요합니다.  
  
```sql
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>테이블 반환 매개 변수를 사용하여 데이터 수정(Transact-SQL)  
 단일 문을 실행하여 여러 행에 영향을 주는 집합 기반 데이터 수정 작업에 테이블 반환 매개 변수를 사용할 수 있습니다. 예를 들어 테이블 반환 매개 변수에서 모든 행을 선택하여 데이터베이스 테이블에 삽입하거나 테이블 반환 매개 변수를 업데이트하려는 테이블에 조인하여 업데이트 문을 만들 수 있습니다.  
  
 다음 Transact-SQL UPDATE 문은 테이블 반환 매개 변수를 Categories 테이블에 조인하여 사용하는 방법을 보여 줍니다. 테이블 반환 매개 변수를 FROM 절에 JOIN과 함께 사용할 경우에는 다음과 같이 별칭을 지정해야 합니다. 이 경우에는 테이블 반환 매개 변수의 별칭을 "ec"로 지정했습니다.  
  
```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 이 Transact-SQL 예제에서는 테이블 반환 매개 변수에서 행을 선택하여 단일 집합 기반 작업으로 INSERT를 수행하는 방법을 보여 줍니다.  
  
```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>테이블 반환 매개 변수의 제한 사항  
 테이블 반환 매개 변수에는 다음의 몇 가지 제한 사항이 적용됩니다.  
  
- [CLR 사용자 정의 함수](/sql/relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions)에는 테이블 반환 매개 변수를 전달할 수 없습니다.  
  
- 테이블 반환 매개 변수는 UNIQUE 또는 PRIMARY KEY 제약 조건을 지원하도록 인덱싱만 수행할 수 있습니다. SQL Server에서는 테이블 반환 매개 변수에 대한 통계가 유지되지 않습니다.  
  
- 테이블 반환 매개 변수는 Transact-SQL 코드에서 읽기 전용입니다. 테이블 반환 매개 변수의 행에서 열 값을 업데이트하거나, 행을 삽입 또는 삭제할 수 없습니다. 테이블 반환 매개 변수를 사용하여 저장 프로시저나 매개 변수화된 문에 전달된 데이터를 수정하려면 데이터를 임시 테이블이나 테이블 변수에 삽입해야 합니다.  
  
- ALTER TABLE 문을 사용하여 테이블 반환 매개 변수의 디자인을 수정할 수 없습니다.  
  
## <a name="configuring-a-sqlparameter-example"></a>SqlParameter 예제 구성  
 <xref:System.Data.SqlClient><xref:System.Data.DataTable>는, <xref:System.Data.Common.DbDataReader> 또는 개체의<xref:System.Collections.Generic.IEnumerable%601> 테이블 반환 매개 변수 채우기를 지원 합니다.  \  <xref:Microsoft.SqlServer.Server.SqlDataRecord> 이 경우 <xref:System.Data.SqlClient.SqlParameter.TypeName%2A>의 <xref:System.Data.SqlClient.SqlParameter> 속성을 사용하여 테이블 반환 매개 변수의 형식 이름을 지정해야 합니다. `TypeName`은 이전에 서버에서 만든 호환 가능한 형식의 이름과 일치해야 합니다. 다음 코드 조각에서는 <xref:System.Data.SqlClient.SqlParameter>를 구성하여 데이터를 삽입하는 방법을 보여 줍니다.  
 
다음 예제에서 `addedCategories` 변수에는 <xref:System.Data.DataTable>이 포함 됩니다. 변수가 채워지는 방법을 확인 하려면 다음 섹션의 예제를 참조 하 여 [테이블 반환 매개 변수를 저장 프로시저에 전달](#passing)합니다.

```csharp  
// Configure the command and parameter.  
SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
tvpParam.TypeName = "dbo.CategoryTableType";  
```  
  
```vb  
' Configure the command and parameter.  
Dim insertCommand As New SqlCommand(sqlInsert, connection)  
Dim tvpParam As SqlParameter = _  
   insertCommand.Parameters.AddWithValue( _  
  "@tvpNewCategories", addedCategories)  
tvpParam.SqlDbType = SqlDbType.Structured  
tvpParam.TypeName = "dbo.CategoryTableType"  
```  
  
 다음 코드 조각에서 볼 수 있는 것처럼 <xref:System.Data.Common.DbDataReader>에서 파생된 개체를 사용하여 데이터 행을 테이블 반환 매개 변수로 스트리밍할 수도 있습니다.  
  
```csharp  
// Configure the SqlCommand and table-valued parameter.  
SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
insertCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", dataReader);  
tvpParam.SqlDbType = SqlDbType.Structured;  
```  
  
```vb  
' Configure the SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  dataReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
```  
  
## <a name="passing"></a>저장 프로시저에 테이블 반환 매개 변수 전달  
 다음 예제에서는 테이블 반환 매개 변수 데이터를 저장 프로시저에 전달하는 방법을 보여 줍니다. 이 코드에서는 추가된 행을 <xref:System.Data.DataTable> 메서드를 사용하여 새 <xref:System.Data.DataTable.GetChanges%2A>에 추출합니다. 그런 다음 <xref:System.Data.SqlClient.SqlCommand> 속성을 <xref:System.Data.SqlClient.SqlCommand.CommandType%2A>로 설정하여 <xref:System.Data.CommandType.StoredProcedure>를 정의합니다. <xref:System.Data.SqlClient.SqlParameter> 메서드를 사용하여 <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A>가 채워지고 <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A>이 `Structured`로 설정됩니다. 그런 다음 <xref:System.Data.SqlClient.SqlCommand> 메서드를 사용하여 <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>가 실행됩니다.  
  
```csharp  
// Assumes connection is an open SqlConnection object.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Configure the SqlCommand and SqlParameter.  
  SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
  insertCommand.CommandType = CommandType.StoredProcedure;  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection object.  
Using connection  
   '  Create a DataTable with the modified rows.  
   Dim addedCategories As DataTable = _  
     CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Configure the SqlCommand and SqlParameter.  
   Dim insertCommand As New SqlCommand( _  
     "usp_InsertCategories", connection)  
   insertCommand.CommandType = CommandType.StoredProcedure  
   Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
     "@tvpNewCategories", addedCategories)  
   tvpParam.SqlDbType = SqlDbType.Structured  
  
   '  Execute the command.  
   insertCommand.ExecuteNonQuery()  
End Using  
```  
  
### <a name="passing-a-table-valued-parameter-to-a-parameterized-sql-statement"></a>매개 변수화된 SQL 문에 테이블 반환 매개 변수 전달  
 다음 예제에서는 테이블 반환 매개 변수를 데이터 소스로 사용하는 SELECT 하위 쿼리가 포함된 INSERT 문을 사용하여 dbo.Categories 테이블에 데이터를 삽입하는 방법을 보여 줍니다. 테이블 반환 매개 변수를 매개 변수화된 SQL 문에 전달할 때는 <xref:System.Data.SqlClient.SqlParameter.TypeName%2A>의 새 <xref:System.Data.SqlClient.SqlParameter> 속성을 사용하여 테이블 반환 매개 변수의 형식 이름을 지정해야 합니다. 이 `TypeName`은 이전에 서버에서 만든 호환 가능한 형식의 이름과 일치해야 합니다. 이 예제의 코드는 `TypeName` 속성을 사용하여 dbo.CategoryTableType에 정의된 형식 구조를 참조합니다.  
  
> [!NOTE]
> 테이블 반환 매개 변수에 ID 열의 값을 제공하면 세션에 대해 SET IDENTITY_INSERT 문을 실행해야 합니다.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Define the INSERT-SELECT statement.  
  string sqlInsert =   
      "INSERT INTO dbo.Categories (CategoryID, CategoryName)"  
      + " SELECT nc.CategoryID, nc.CategoryName"  
      + " FROM @tvpNewCategories AS nc;"  

  // Configure the command and parameter.  
  SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  
  tvpParam.TypeName = "dbo.CategoryTableType";  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
Using connection  
  ' Create a DataTable with the modified rows.  
  Dim addedCategories As DataTable = _  
    CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Define the INSERT-SELECT statement.  
  Dim sqlInsert As String = _  
  "INSERT INTO dbo.Categories (CategoryID, CategoryName)" _  
  & " SELECT nc.CategoryID, nc.CategoryName" _  
  & " FROM @tvpNewCategories AS nc;"  
  
  ' Configure the command and parameter.  
  Dim insertCommand As New SqlCommand(sqlInsert, connection)  
  Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
    "@tvpNewCategories", addedCategories)  
  tvpParam.SqlDbType = SqlDbType.Structured  
  tvpParam.TypeName = "dbo.CategoryTableType"  
  
  ' Execute the query  
  insertCommand.ExecuteNonQuery()  
End Using  
```  
  
## <a name="streaming-rows-with-a-datareader"></a>DataReader를 사용하여 행 스트리밍  
 <xref:System.Data.Common.DbDataReader>에서 파생된 개체를 사용하여 데이터 행을 테이블 반환 매개 변수로 스트리밍할 수 있습니다. 다음 코드 조각에서는 <xref:System.Data.OracleClient.OracleCommand> 및 <xref:System.Data.OracleClient.OracleDataReader>를 사용하여 Oracle 데이터베이스에서 데이터를 검색하는 방법을 보여 줍니다. 그러면 코드에서는 단일 입력 매개 변수를 사용하여 저장 프로시저를 호출하는 <xref:System.Data.SqlClient.SqlCommand>를 구성합니다. <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A>의 <xref:System.Data.SqlClient.SqlParameter> 속성은 `Structured`로 설정됩니다. <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A>는 `OracleDataReader` 결과 집합을 저장 프로시저에 테이블 반환 매개 변수로 전달합니다.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
// Retrieve data from Oracle.  
OracleCommand selectCommand = new OracleCommand(  
   "Select CategoryID, CategoryName FROM Categories;",  
   oracleConnection);  
OracleDataReader oracleReader = selectCommand.ExecuteReader(  
   CommandBehavior.CloseConnection);  
  
 // Configure the SqlCommand and table-valued parameter.  
 SqlCommand insertCommand = new SqlCommand(  
   "usp_InsertCategories", connection);  
 insertCommand.CommandType = CommandType.StoredProcedure;  
 SqlParameter tvpParam =  
    insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", oracleReader);  
 tvpParam.SqlDbType = SqlDbType.Structured;  
  
 // Execute the command.  
 insertCommand.ExecuteNonQuery();  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
' Retrieve data from Oracle.  
Dim selectCommand As New OracleCommand( _  
  "Select CategoryID, CategoryName FROM Categories;", _  
  oracleConnection)  
Dim oracleReader As OracleDataReader = _  
  selectCommand.ExecuteReader(CommandBehavior.CloseConnection)  
  
' Configure SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  oracleReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
  
' Execute the command.  
insertCommand.ExecuteNonQuery()  
```  
  
## <a name="see-also"></a>참고자료

- [매개 변수 및 매개 변수 데이터 형식 구성](../configuring-parameters-and-parameter-data-types.md)
- [명령 및 매개 변수](../commands-and-parameters.md)
- [DataAdapter 매개 변수](../dataadapter-parameters.md)
- [ADO.NET에서 SQL Server 데이터 작업](sql-server-data-operations.md)
- [ADO.NET 개요](../ado-net-overview.md)
