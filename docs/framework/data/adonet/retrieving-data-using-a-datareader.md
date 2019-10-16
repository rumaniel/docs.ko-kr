---
title: DataReader를 사용하여 데이터 검색
ms.date: 10/29/2018
dev_langs:
- csharp
- vb
ms.assetid: 97afc121-fb8b-465b-bab3-6d844420badb
ms.openlocfilehash: f3add49d48a569664d4cbb6b5c26d5f3379b6f18
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794405"
---
# <a name="retrieve-data-using-a-datareader"></a>DataReader를 사용 하 여 데이터 검색
**DataReader**를 사용 하 여 데이터를 검색 하려면 **command** 개체의 인스턴스를 만든 다음 **ExecuteReader** 를 호출 하 여 데이터 원본에서 행을 검색 하 여 **DataReader** 를 만듭니다. **DataReader** 는 데이터 원본에서 순차적으로 결과를 효율적으로 처리 하는 절차적 논리를 허용 하는 버퍼링 되지 않은 데이터 스트림을 제공 합니다. **DataReader** 는 데이터가 메모리에 캐시 되지 않기 때문에 대량의 데이터를 검색 하는 경우에 적합 합니다.

다음 예제에서는 **datareader**를 사용 하는 방법을 `reader` 보여 줍니다. 여기서은 `command` 유효한 datareader를 나타내고는 유효한 명령 개체를 나타냅니다.  

```csharp
reader = command.ExecuteReader();  
```

```vb
reader = command.ExecuteReader()
```  

**DataReader** 메서드를 사용 하 여 쿼리 결과에서 행을 가져옵니다. 열의 이름 또는 서 수를 **DataReader**에 전달 하 여 반환 된 행의 각 열에 액세스할 수 있습니다. 그러나 최상의 성능을 위해 **DataReader** 는 네이티브 데이터 형식 (**getdatetime**, **getdatetime**, **getdatetime**, **GetInt32**등)의 열 값에 액세스할 수 있도록 하는 일련의 메서드를 제공 합니다. 데이터 공급자별 데이터 **판독기**의 형식화 된 접근자 메서드 목록은 및 <xref:System.Data.OleDb.OleDbDataReader> <xref:System.Data.SqlClient.SqlDataReader>를 참조 하십시오. 기본 데이터 형식을 알고 있는 경우 형식화 된 접근자 메서드를 사용 하면 열 값을 검색할 때 필요한 형식 변환의 양이 줄어듭니다.  
  
 다음 예에서는 **DataReader** 개체를 반복 하 고 각 행에서 두 개의 열을 반환 합니다.  
  
 [!code-csharp[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/VB/source.vb#1)]  
  
## <a name="closing-the-datareader"></a>DataReader 닫기  
 **DataReader** 개체 사용을 완료 한 후에는 항상 **Close** 메서드를 호출 합니다.  
  
 **명령** 에 출력 매개 변수 또는 반환 값이 포함 된 경우 **DataReader** 를 닫을 때까지 해당 값을 사용할 수 없습니다.  
  
 **Datareader** 가 열려 있는 동안에는 해당 **datareader**에서 단독으로 **연결** 을 사용 합니다. 원본 **datareader** 가 닫힐 때까지 다른 **datareader**만들기를 포함 하 여 **연결**에 대 한 명령을 실행할 수 없습니다.  
  
> [!NOTE]
> 클래스의 **Finalize** 메서드에서 **Connection**, **DataReader**또는 기타 관리 되는 개체에 대해 **Close** 또는 **Dispose** 를 호출 하지 마세요. 종료자에서는 클래스에 직접 속한 관리되지 않는 리소스만 해제합니다. 클래스는 관리 되지 않는 리소스를 소유 하지 않습니다, 경우 포함 되지 않습니다는 **Finalize** 클래스 정의에 메서드. 자세한 내용은 [가비지 수집](../../../standard/garbage-collection/index.md)합니다.  
  
## <a name="retrieving-multiple-result-sets-using-nextresult"></a>NextResult를 사용 하 여 여러 결과 집합 검색  
 **DataReader** 에서 여러 결과 집합을 반환 하는 경우 **nextresult** 메서드를 호출 하 여 결과 집합을 순차적으로 반복 합니다. 다음 예제에서는 <xref:System.Data.SqlClient.SqlDataReader>가 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 메서드를 사용하여 두 가지 SELECT 문 결과를 처리하는 방법을 보여 줍니다.  
  
 [!code-csharp[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/VB/source.vb#1)]  
  
## <a name="getting-schema-information-from-the-datareader"></a>DataReader에서 스키마 정보 가져오기  
 **DataReader** 가 열려 있는 동안에는 **getschematable** 수 있는 메서드를 사용 하 여 현재 결과 집합에 대 한 스키마 정보를 검색할 수 있습니다. **Getschematable** 은 현재 <xref:System.Data.DataTable> 결과 집합에 대 한 스키마 정보를 포함 하는 행과 열로 채워진 개체를 반환 합니다. **DataTable** 은 결과 집합의 각 열에 대해 하나의 행을 포함 합니다. 스키마 테이블의 각 열은 결과 집합의 행에 반환 된 열의 속성에 매핑됩니다. 여기서 **ColumnName** 은 속성의 이름이 고 열 값은 속성의 값입니다. 다음 예제에서는 **DataReader**의 스키마 정보를 작성 합니다.  
  
 [!code-csharp[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/VB/source.vb#1)]  
  
## <a name="working-with-ole-db-chapters"></a>OLE DB 챕터 사용  
 계층적 행 집합 또는 챕터 (OLE DB 형식 **DBTYPE_HCHAPTER**, ADO 유형 **adchapter**)는를 <xref:System.Data.OleDb.OleDbDataReader>사용 하 여 검색할 수 있습니다. 챕터를 포함 하는 쿼리가 **datareader**로 반환 되는 경우이 장은 **datareader** 에서 열로 반환 되 고 **datareader** 개체로 노출 됩니다.  
  
 ADO.NET **데이터 집합** 을 사용 하 여 테이블 간 부모-자식 관계를 사용 하 여 계층적 행 집합을 나타낼 수도 있습니다. 자세한 내용은 [데이터 집합, datatable 및 DataViews](./dataset-datatable-dataview/index.md)를 참조 하세요.  
  
 다음 코드 예제에서는 MSDataShape 공급자를 사용하여 고객 목록에 있는 각 고객의 주문에 대해 장 열을 생성합니다.  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection(
    "Provider=MSDataShape;Data Provider=SQLOLEDB;" &
    "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind")

    Using custCMD As OleDbCommand = New OleDbCommand(
        "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " &
        "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " &
        "RELATE CustomerID TO CustomerID)", connection)

        connection.Open()

        Using custReader As OleDbDataReader = custCMD.ExecuteReader()

            Do While custReader.Read()
                Console.WriteLine("Orders for " & custReader.GetString(1))
                ' custReader.GetString(1) = CompanyName  

                Using orderReader As OleDbDataReader = custReader.GetValue(2)
                    ' custReader.GetValue(2) = Orders chapter as DataReader  

                    Do While orderReader.Read()
                        Console.WriteLine(vbTab & orderReader.GetInt32(1))
                        ' orderReader.GetInt32(1) = OrderID  
                    Loop
                    orderReader.Close()
                End Using
            Loop
            ' Make sure to always close readers and connections.  
            custReader.Close()
        End Using
    End Using
End Using
```  
  
```csharp  
using (OleDbConnection connection = new OleDbConnection(
    "Provider=MSDataShape;Data Provider=SQLOLEDB;" +
    "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind"))
{
    using (OleDbCommand custCMD = new OleDbCommand(
        "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +
        "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " +
        "RELATE CustomerID TO CustomerID)", connection))
    {
        connection.Open();

        using (OleDbDataReader custReader = custCMD.ExecuteReader())
        {

            while (custReader.Read())
            {
                Console.WriteLine("Orders for " + custReader.GetString(1));
                // custReader.GetString(1) = CompanyName  

                using (OleDbDataReader orderReader = (OleDbDataReader)custReader.GetValue(2))
                {
                    // custReader.GetValue(2) = Orders chapter as DataReader  

                    while (orderReader.Read())
                        Console.WriteLine("\t" + orderReader.GetInt32(1));
                    // orderReader.GetInt32(1) = OrderID  
                    orderReader.Close();
                }
            }
            // Make sure to always close readers and connections.  
            custReader.Close();
        }
    }
}
```  
  
## <a name="returning-results-with-oracle-ref-cursors"></a>Oracle REF Cursor를 사용 하 여 결과 반환  
 .NET Framework Data Provider for Oracle을 사용하면 Oracle REF CURSOR를 사용하여 쿼리 결과를 반환할 수 있습니다. Oracle REF CURSOR는 <xref:System.Data.OracleClient.OracleDataReader>로 반환됩니다.  
  
 메서드를 <xref:System.Data.OracleClient.OracleDataReader> <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A> 사용 하 여 Oracle REF CURSOR를 나타내는 개체를 검색할 수 있습니다. 하나 이상의 Oracle REF cursor <xref:System.Data.OracleClient.OracleCommand> 를를 <xref:System.Data.DataSet>채우는 <xref:System.Data.OracleClient.OracleDataAdapter> 데 사용 되는의 **SelectCommand** 로 반환 하는를 지정할 수도 있습니다.  
  
 Oracle 데이터 원본에서 반환 된 ref 커서에 액세스 하려면 쿼리에 <xref:System.Data.OracleClient.OracleCommand> 대해를 만들고 ref 커서를 참조 하는 출력 매개 변수를의 <xref:System.Data.OracleClient.OracleCommand.Parameters> <xref:System.Data.OracleClient.OracleCommand>컬렉션에 추가 합니다. 매개 변수 이름은 쿼리의 REF CURSOR 매개 변수 이름과 일치해야 합니다. 매개 변수의 형식을로 <xref:System.Data.OracleClient.OracleType.Cursor?displayProperty=nameWithType>설정 합니다. 의 메서드는 <xref:System.Data.OracleClient.OracleCommand.ExecuteReader?displayProperty=nameWithType> REF 커서 <xref:System.Data.OracleClient.OracleDataReader> 에 대해를 반환합니다.<xref:System.Data.OracleClient.OracleCommand>  
  
 에서 <xref:System.Data.OracleClient.OracleCommand> 여러 REF cursor를 반환 하는 경우 여러 출력 매개 변수를 추가 합니다. 메서드를 <xref:System.Data.OracleClient.OracleCommand.ExecuteReader?displayProperty=nameWithType> 호출 하 여 다른 REF cursor에 액세스할 수 있습니다. 를 호출 하면 <xref:System.Data.OracleClient.OracleCommand.ExecuteReader> 첫 번째 <xref:System.Data.OracleClient.OracleDataReader> REF 커서를 참조 하는이 반환 됩니다. 그런 다음 메서드를 <xref:System.Data.OracleClient.OracleDataReader.NextResult?displayProperty=nameWithType> 호출 하 여 후속 REF 커서에 액세스할 수 있습니다. <xref:System.Data.OracleClient.OracleCommand.Parameters?displayProperty=nameWithType> 컬렉션의 매개 변수가 이름으로 REF CURSOR 출력 매개 변수와 일치 하더라도는 <xref:System.Data.OracleClient.OracleCommand.Parameters> 컬렉션에 <xref:System.Data.OracleClient.OracleDataReader> 추가 된 순서 대로 해당 매개 변수를 액세스 합니다.  
  
 예를 들어, 다음과 같은 Oracle 패키지 및 패키지 본문이 있을 수 있습니다.  
  
```sql
CREATE OR REPLACE PACKAGE CURSPKG AS   
  TYPE T_CURSOR IS REF CURSOR;   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR);   
END CURSPKG;  
  
CREATE OR REPLACE PACKAGE BODY CURSPKG AS   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR)   
  IS   
  BEGIN   
    OPEN EMPCURSOR FOR SELECT * FROM DEMO.EMPLOYEE;   
    OPEN DEPTCURSOR FOR SELECT * FROM DEMO.DEPARTMENT;   
  END OPEN_TWO_CURSORS;   
END CURSPKG;   
```  
  
 다음 코드에서는 <xref:System.Data.OracleClient.OracleCommand> <xref:System.Data.OracleClient.OracleCommand.Parameters?displayProperty=nameWithType> 컬렉션에 형식의 <xref:System.Data.OracleClient.OracleType.Cursor?displayProperty=nameWithType> 매개 변수 두 개를 추가 하 여 이전 Oracle 패키지에서 REF cursor를 반환 하는를 만듭니다.  
  
```vb  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
```  
  
```csharp  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
```  
  
 다음 코드는의 <xref:System.Data.OracleClient.OracleDataReader.Read> <xref:System.Data.OracleClient.OracleDataReader.NextResult> 및 메서드를 사용 하 여 이전 명령의 결과를 반환 합니다 <xref:System.Data.OracleClient.OracleDataReader>. REF CURSOR 매개 변수가 순서대로 반환됩니다.  
  
```vb  
oraConn.Open()  
  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.CommandType = CommandType.StoredProcedure  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
  
Dim reader As OracleDataReader = cursCmd.ExecuteReader()  
  
Console.WriteLine(vbCrLf & "Emp ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2))  
Loop  
  
reader.NextResult()  
  
Console.WriteLine(vbCrLf & "Dept ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}", reader.GetOracleNumber(0), reader.GetString(1))  
Loop  
' Make sure to always close readers and connections.  
reader.Close()  
oraConn.Close()  
```  
  
```csharp  
oraConn.Open();  
  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.CommandType = CommandType.StoredProcedure;  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
  
OracleDataReader reader = cursCmd.ExecuteReader();  
  
Console.WriteLine("\nEmp ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2));  
  
reader.NextResult();  
  
Console.WriteLine("\nDept ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}", reader.GetOracleNumber(0), reader.GetString(1));  
// Make sure to always close readers and connections.  
reader.Close();  
oraConn.Close();  
```  
  
 다음 예에서는 이전 명령을 사용 하 여를 <xref:System.Data.DataSet> Oracle 패키지의 결과로 채웁니다.  
  
```vb  
Dim ds As DataSet = New DataSet()  
  
Dim adapter As OracleDataAdapter = New OracleDataAdapter(cursCmd)  
adapter.TableMappings.Add("Table", "Employees")  
adapter.TableMappings.Add("Table1", "Departments")  
  
adapter.Fill(ds)  
```  
  
```csharp  
DataSet ds = new DataSet();  
  
OracleDataAdapter adapter = new OracleDataAdapter(cursCmd);  
adapter.TableMappings.Add("Table", "Employees");  
adapter.TableMappings.Add("Table1", "Departments");  
  
adapter.Fill(ds);  
```

> [!NOTE]
> **OverflowException**을 방지 하려면에 <xref:System.Data.DataRow>값을 저장 하기 전에 Oracle 숫자 형식에서 유효한 .NET Framework 형식으로의 변환을 처리 하는 것이 좋습니다. 이벤트를 <xref:System.Data.Common.DataAdapter.FillError> 사용 하 여 **OverflowException** 발생 했는지 여부를 확인할 수 있습니다. <xref:System.Data.Common.DataAdapter.FillError> 이벤트에 대 한 자세한 내용은 [DataAdapter 이벤트 처리](handling-dataadapter-events.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [명령 및 매개 변수](commands-and-parameters.md)
- [데이터베이스 스키마 정보 검색](retrieving-database-schema-information.md)
- [ADO.NET 개요](ado-net-overview.md)
