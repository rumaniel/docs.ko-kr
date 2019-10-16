---
title: DataAdapter에서 DataSet 채우기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3fa0ac7d-e266-4954-bfac-3fbe2f913153
ms.openlocfilehash: fecc212b21fee585444db35d832894719640fd79
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783221"
---
# <a name="populating-a-dataset-from-a-dataadapter"></a>DataAdapter에서 DataSet 채우기
ADO.NET <xref:System.Data.DataSet> 는 데이터 원본에 독립적인 일관 된 관계형 프로그래밍 모델을 제공 하는 데이터의 메모리 상주 표현입니다. `DataSet` 은 테이블 및 제약 조건과 테이블 간의 관계를 포함하는 완전한 데이터 집합을 나타냅니다. `DataSet` 은 데이터 소스에 독립적입니다. 따라서 `DataSet` 은 응용 프로그램에 대해 로컬인 데이터뿐 아니라 여러 데이터 소스의 데이터도 포함할 수 있습니다. 기존 데이터 소스와의 상호 작용은 `DataAdapter`를 통해 제어됩니다.  
  
 `SelectCommand` 의 `DataAdapter` 속성은 데이터 소스에서 데이터를 검색하는 `Command` 개체입니다. `InsertCommand`의 `UpdateCommand`, `DeleteCommand` 및 `DataAdapter` 속성은 `Command` 의 데이터에 대한 수정 내용에 따라 데이터 소스의 데이터에 대한 업데이트를 관리하는 `DataSet`개체입니다. 이러한 속성은 [dataadapter를 사용 하 여 데이터 원본 업데이트](updating-data-sources-with-dataadapters.md)에 자세히 설명 되어 있습니다.  
  
 `Fill` 의 `DataAdapter` 메서드는 `DataSet` 의 `SelectCommand` 결과로 `DataAdapter`을 채우는 데 사용됩니다. `Fill` 은 채울 `DataSet` 과 `DataTable` 개체 또는 `DataTable` 에서 반환된 행으로 채울 `SelectCommand`의 이름을 인수로 사용합니다.  
  
> [!NOTE]
> `DataAdapter` 를 사용하여 모든 테이블을 검색하는 경우 시간이 많이 걸리며, 특히 테이블에 많은 행이 있는 경우 더욱 그렇습니다. 이는 데이터베이스에 액세스하여 데이터를 찾아서 처리한 다음 클라이언트로 데이터를 전송하는 데 많은 시간이 걸리기 때문입니다. 모든 테이블을 클라이언트로 가져오는 경우 서버의 모든 행이 잠기는 문제도 있습니다. 이 경우 `WHERE` 절을 사용하여 클라이언트에 반환되는 행 수를 대폭 줄이면 성능을 개선할 수 있습니다. `SELECT` 문에 필요한 열을 명시적으로 나열하여 클라이언트에 반환되는 데이터의 양을 줄일 수도 있습니다. 한 번에 몇 백 개씩 행을 일괄적으로 검색함으로써 클라이언트에서 현재 일괄 검색 작업이 완료되면 다음 일괄 검색 작업을 시작하는 것도 좋은 방법입니다.  
  
 `Fill` 메서드는 `DataReader` 개체를 암시적으로 사용하여 `DataSet`의 테이블 행을 채울 데이터와 `DataSet`에 테이블을 만드는 데 사용되는 열 이름 및 형식을 반환합니다. 테이블과 열은 없는 경우에만 만들어지고 있는 경우 `Fill` 에서 기존의 `DataSet` 스키마를 사용합니다. 열 유형은 [ADO.NET의 데이터 형식 매핑](data-type-mappings-in-ado-net.md)테이블에 따라 .NET Framework 형식으로 만들어집니다. 기본 키가 데이터 소스에 없으면 기본 키는 만들어지지 않고 `DataAdapter`**를 통해 제어됩니다.** `MissingSchemaAction` 이 `MissingSchemaAction`**를 통해 제어됩니다.** `AddWithKey`를 통해 제어됩니다. `Fill` 에서 테이블의 기본 키가 있음을 발견하면 기본 키 열 값이 데이터 소스에서 반환된 행의 값과 일치하는 행의 데이터 소스 데이터로 `DataSet` 의 데이터를 덮어씁니다. 기본 키가 없으면 해당 데이터가 `DataSet`의 테이블에 추가됩니다. `Fill`는를 `DataSet` 채울 때 있을 수 있는 모든 매핑을 사용 합니다 ( [DataAdapter DataTable 및 DataColumn 매핑](dataadapter-datatable-and-datacolumn-mappings.md)참조).  
  
> [!NOTE]
> `SelectCommand` 가 OUTER JOIN의 결과를 반환하면 `DataAdapter` 는 결과 `PrimaryKey` 에 대해 `DataTable`값을 설정하지 않습니다. 행 중복 문제를 해결하려면 `PrimaryKey` 를 직접 정의해야 합니다. 자세한 내용은 [기본 키 정의](./dataset-datatable-dataview/defining-primary-keys.md)합니다.  
  
 다음 코드 예제에서는 Microsoft SQL Server <xref:System.Data.SqlClient.SqlDataAdapter> 데이터베이스에 대한 <xref:System.Data.SqlClient.SqlConnection> 을 사용하는 `Northwind` 의 인스턴스를 만들고 <xref:System.Data.DataTable> 의 `DataSet` 을 고객 목록으로 채웁니다. <xref:System.Data.SqlClient.SqlConnection> 생성자에 전달되는 <xref:System.Data.SqlClient.SqlDataAdapter> 인수와 SQL 문은 <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> 의 <xref:System.Data.SqlClient.SqlDataAdapter>속성을 만드는 데 사용됩니다.  
  
## <a name="example"></a>예제  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim queryString As String = _  
  "SELECT CustomerID, CompanyName FROM dbo.Customers"  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  queryString, connection)  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
string queryString =   
  "SELECT CustomerID, CompanyName FROM dbo.Customers";  
SqlDataAdapter adapter = new SqlDataAdapter(queryString, connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
> 이 예제의 코드에서는 `Connection`을 명시적으로 열거나 닫지 않습니다. `Fill` 메서드는 연결이 아직 열려 있지 않으면 `Connection` 에서 사용하고 있는 `DataAdapter` 을 암시적으로 엽니다. `Fill` 에서 연결을 연 경우 `Fill` 이 완료되면 연결도 닫힙니다. `Fill` 또는 `Update`와 같은 단일 작업을 처리할 경우 이렇게 하면 코드가 간단해집니다. 그러나 연결이 열려 있어야 하는 여러 작업을 수행 중인 경우에는 `Open` 의 `Connection`메서드를 명시적으로 호출하고 데이터 소스에 대한 작업을 수행한 다음 `Close` 의 `Connection`메서드를 호출하여 애플리케이션의 성능을 향상시킬 수 있습니다. 다른 클라이언트 애플리케이션에서 사용할 리소스를 사용 가능한 상태로 만들려면 데이터 소스에 연결되어 있는 시간을 가능한 한 짧게 유지하도록 해야 합니다.  
  
## <a name="multiple-result-sets"></a>여러 결과 집합  
 `DataAdapter` 는 여러 결과 집합을 발견하면 `DataSet`에 여러 테이블을 만듭니다. 테이블에는 Table0부터 시작하는 증분 기본 이름인 Table*N*이 지정됩니다. 테이블 이름이 인수로 `Fill` 메서드에 전달되면 테이블에는 TableName0부터 시작하는 증분 기본 이름인 TableName*N*이 지정됩니다.  
  
## <a name="populating-a-dataset-from-multiple-dataadapters"></a>여러 DataAdapter에서 DataSet 채우기  
 에서 원하는 수 `DataAdapter` 의 개체를 `DataSet`사용할 수 있습니다. `DataAdapter` 는 각각 하나 이상의 `DataTable` 개체를 채우고 업데이트를 다시 관련 데이터 소스에 적용하는 데 사용할 수 있습니다. `DataRelation` 및 `Constraint` 개체를 `DataSet` 에 로컬로 추가하면 각기 다른 데이터 소스의 데이터를 연결할 수 있습니다. 예를 들어, `DataSet` 은 Microsoft SQL Server 데이터베이스, OLE DB를 통해 노출된 IBM DB2 데이터베이스, XML을 스트리밍하는 데이터 소스의 데이터를 포함할 수 있습니다. 하나 이상의 `DataAdapter` 개체에서 각 데이터 소스와의 통신을 처리할 수 있습니다.  
  
### <a name="example"></a>예제  
 다음 코드 예제에서는 Microsoft SQL Server에 있는 `Northwind` 데이터베이스의 고객 목록과 Microsoft Access 2000에 저장된 `Northwind` 데이터베이스의 주문 목록을 채웁니다. 채워진 테이블은 `DataRelation`에 연결되고 고객 목록이 해당 고객의 주문과 함께 표시됩니다. 개체에 대 한 `DataRelation` 자세한 내용은 [datarelations 추가](./dataset-datatable-dataview/adding-datarelations.md) 및 [datarelations 탐색](./dataset-datatable-dataview/navigating-datarelations.md)을 참조 하세요.  
  
```vb  
' Assumes that customerConnection is a valid SqlConnection object.  
' Assumes that orderConnection is a valid OleDbConnection object.  
Dim custAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers", customerConnection)  
  
Dim ordAdapter As OleDbDataAdapter = New OleDbDataAdapter( _  
  "SELECT * FROM Orders", orderConnection)  
  
Dim customerOrders As DataSet = New DataSet()  
custAdapter.Fill(customerOrders, "Customers")  
ordAdapter.Fill(customerOrders, "Orders")  
  
Dim relation As DataRelation = _  
  customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustomerID"), _   
  customerOrders.Tables("Orders").Columns("CustomerID"))  
  
Dim pRow, cRow As DataRow  
For Each pRow In customerOrders.Tables("Customers").Rows  
  Console.WriteLine(pRow("CustomerID").ToString())  
  
  For Each cRow In pRow.GetChildRows(relation)  
    Console.WriteLine(vbTab & cRow("OrderID").ToString())  
  Next  
Next  
```  
  
```csharp  
// Assumes that customerConnection is a valid SqlConnection object.  
// Assumes that orderConnection is a valid OleDbConnection object.  
SqlDataAdapter custAdapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers", customerConnection);  
OleDbDataAdapter ordAdapter = new OleDbDataAdapter(  
  "SELECT * FROM Orders", orderConnection);  
  
DataSet customerOrders = new DataSet();  
  
custAdapter.Fill(customerOrders, "Customers");  
ordAdapter.Fill(customerOrders, "Orders");  
  
DataRelation relation = customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustomerID"],  
  customerOrders.Tables["Orders"].Columns["CustomerID"]);  
  
foreach (DataRow pRow in customerOrders.Tables["Customers"].Rows)  
{  
  Console.WriteLine(pRow["CustomerID"]);  
   foreach (DataRow cRow in pRow.GetChildRows(relation))  
    Console.WriteLine("\t" + cRow["OrderID"]);  
}  
```  
  
## <a name="sql-server-decimal-type"></a>SQL Server Decimal 형식  
 기본적으로에서는 `DataSet` .NET Framework 데이터 형식을 사용 하 여 데이터를 저장 합니다. 대부분의 애플리케이션에서 이 형식을 사용하면 데이터 소스 정보를 간편하게 나타낼 수 있습니다. 그러나 이 표현은 데이터 소스의 데이터 형식이 SQL Server decimal 또는 숫자 데이터 형식인 경우 문제를 일으킬 수 있습니다. .NET Framework `decimal` 데이터 형식은 최대 28 개의 유효 숫자를 허용 하는 반면 SQL Server `decimal` 데이터 형식은 38 개의 유효 숫자를 허용 합니다. `SqlDataAdapter` 작업 중에 `Fill` 에서 SQL Server `decimal` 필드의 정밀도가 28자보다 크다고 판단하면 현재 행은 `DataTable`에 추가되지 않습니다. 대신 `FillError` 이벤트가 발생하므로 정밀도가 손실되는지 여부를 확인하여 적절하게 대응할 수 있습니다. `FillError` 이벤트에 대 한 자세한 내용은 [DataAdapter 이벤트 처리](handling-dataadapter-events.md)를 참조 하세요. `decimal` 개체를 사용하고 <xref:System.Data.SqlClient.SqlDataReader> 메서드를 호출하여 SQL Server <xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A> 값을 확인할 수도 있습니다.  
  
 ADO.NET 2.0에는의에 <xref:System.Data.SqlTypes> 대 한 `DataSet`향상 된 지원이 도입 되었습니다. 자세한 내용은 [SqlTypes and the DataSet](./sql/sqltypes-and-the-dataset.md)을 참조하세요.  
  
## <a name="ole-db-chapters"></a>OLE DB 장  
 계층적 행 집합 또는 장(OLE DB 형식 `DBTYPE_HCHAPTER`, ADO 형식 `adChapter`)을 사용하여 `DataSet`의 내용을 채울 수 있습니다. <xref:System.Data.OleDb.OleDbDataAdapter> 에서 `Fill` 작업 중에 장으로 나뉜 열을 발견하면 해당 열에 대해 `DataTable` 이 만들어지고 테이블은 그 장의 열과 행으로 채워집니다. 장으로 나뉜 열에 대해 만들어진 테이블은 부모 테이블 이름과 장으로 나뉜 열 이름을 모두 사용하여 "*ParentTableNameChapteredColumnName*" 형식으로 이름이 지정됩니다. 장으로 나뉜 열 이름과 일치하는 테이블이 이미 `DataSet` 에 있으면 현재 테이블이 장 데이터로 채워집니다. 장에 있는 열과 일치하는 열이 기존 테이블에 없으면 새 열이 추가됩니다.  
  
 `DataSet` 의 테이블이 장으로 나뉜 열의 데이터로 채워지기 전에 계층적 행 집합의 부모 테이블과 자식 테이블 사이에는 정수 열을 부모 테이블과 자식 테이블에 모두 추가하고 부모 열을 자동 증분으로 설정한 다음 두 테이블에서 추가된 열을 사용하여 `DataRelation` 을 만듦으로써 관계가 만들어집니다. 추가된 관계의 이름은 부모 테이블과 장의 열 이름을 사용하여 "*ParentTableNameChapterColumnName*" 형식으로 지정됩니다.  
  
 `DataSet`에는 관련 열만 있습니다. 다음에 데이터 소스에서 채우기 작업이 수행되면 변경 내용이 기존 행으로 병합되지 않고 새 행이 테이블에 추가됩니다.  
  
 또한 `DataAdapter.Fill` 을 사용하는 `DataTable`오버로드를 사용하면 해당 테이블만 채워집니다. 자동 증분 정수 열은 여전히 테이블에 추가되지만 자식 테이블이 만들어지거나 채워지지 않으며 관계도 만들어지지 않습니다.  
  
 다음 예제에서는 MSDataShape 공급자를 사용하여 고객 목록에 있는 각 고객의 주문에 대해 장 열을 생성합니다. 그런 다음 `DataSet` 이 데이터로 채워집니다.  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection( _  
  "Provider=MSDataShape;Data Provider=SQLOLEDB;" & _  
  "Data Source=(local);Integrated " & _  
  "Security=SSPI;Initial Catalog=northwind")  
  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter( _  
  "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " & _  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS Orders " & _  
  "RELATE CustomerID TO CustomerID)", connection)  
  
Dim customers As DataSet = New DataSet()  
  
adapter.Fill(customers, "Customers")  
End Using  
```  
  
```csharp  
using (OleDbConnection connection = new OleDbConnection("Provider=MSDataShape;Data Provider=SQLOLEDB;" +  
  "Data Source=(local);Integrated Security=SSPI;Initial Catalog=northwind"))  
{  
OleDbDataAdapter adapter = new OleDbDataAdapter("SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS Orders " +  
  "RELATE CustomerID TO CustomerID)", connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
}  
```  
  
 `Fill` 작업이 완료되면 `DataSet` 에 `Customers` 테이블과 `CustomersOrders`테이블이 포함됩니다. 여기서 `CustomersOrders` 는 장으로 나뉜 열을 나타냅니다. `Orders` 라는 추가 열이 `Customers` 테이블에 추가되고 `CustomersOrders` 라는 추가 열이 `CustomersOrders` 테이블에 추가됩니다. `Orders` 테이블의 `Customers` 열은 자동 증분으로 설정됩니다. `DataRelation`를 부모 테이블로 하는 테이블에 추가된 열을 사용하여 `CustomersOrders`라는 `Customers` 이 만들어집니다. 다음 표에서는 몇 가지 샘플 결과를 보여 줍니다.  
  
### <a name="tablename-customers"></a>TableName: 고객  
  
|CustomerID|CompanyName|Orders|  
|----------------|-----------------|------------|  
|ALFKI|Alfreds Futterkiste|0|  
|ANATR|Ana Trujillo Emparedados y helados|1|  
  
### <a name="tablename-customersorders"></a>TableName: CustomersOrders  
  
|CustomerID|OrderID|CustomersOrders|  
|----------------|-------------|---------------------|  
|ALFKI|10643|0|  
|ALFKI|10692|0|  
|ANATR|10308|1|  
|ANATR|10625|1|  
  
## <a name="see-also"></a>참고자료

- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [ADO.NET에서 데이터 형식 매핑](data-type-mappings-in-ado-net.md)
- [DbDataAdapter로 데이터 수정](modifying-data-with-a-dbdataadapter.md)
- [MARS(Multiple Active Result Sets)](./sql/multiple-active-result-sets-mars.md)
- [ADO.NET 개요](ado-net-overview.md)
