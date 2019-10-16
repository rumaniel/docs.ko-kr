---
title: SQL Server용 공급자 통계
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
ms.openlocfilehash: b6fa4207531e86cbde8657d0c47596f22c886f89
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791877"
---
# <a name="provider-statistics-for-sql-server"></a>SQL Server용 공급자 통계
.NET Framework 버전 2.0부터는 .NET Framework Data Provider for SQL Server에 런타임 통계가 지원됩니다. 유효한 연결 개체를 만든 후 <xref:System.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> 개체의 <xref:System.Data.SqlClient.SqlConnection> 속성을 `True`로 설정하여 통계를 활성화해야 합니다. 통계를 활성화한 후에는 <xref:System.Collections.IDictionary> 개체의 <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 메서드를 통해 <xref:System.Data.SqlClient.SqlConnection> 참조를 검색하여 통계를 "적시 스냅샷"으로 검토할 수 있습니다. 이름/값 쌍 사전 항목의 집합으로 목록을 열거합니다. 이러한 이름/값 쌍은 순서가 정해져 있지 않습니다. 언제라도 <xref:System.Data.SqlClient.SqlConnection.ResetStatistics%2A> 개체의 <xref:System.Data.SqlClient.SqlConnection> 메서드를 호출하여 카운터를 다시 설정할 수 있습니다. 통계 수집을 활성화하지 않으면 예외가 생성되지 않습니다. 또한 <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A>를 먼저 호출하지 않은 상태에서 <xref:System.Data.SqlClient.SqlConnection.StatisticsEnabled%2A>를 호출한 경우 각 항목의 초기 값이 검색됩니다. 통계를 활성화하고 나서 잠시 동안 애플리케이션을 실행했다가 통계를 비활성화하면 검색된 값은 통계가 사용되지 않은 지점까지 수집된 값을 반영합니다. 모든 통계 값은 각 연결 단위로 수집됩니다.  
  
## <a name="statistical-values-available"></a>사용 가능한 통계 값  
 현재 Microsoft SQL Server 공급자는 18가지 다양한 항목을 제공합니다. 사용할 수 있는 항목의 수는에서 <xref:System.Data.SqlClient.SqlConnection.RetrieveStatistics%2A>반환 된 <xref:System.Collections.IDictionary> 인터페이스 참조의 Count 속성을 통해 액세스할 수 있습니다. 공급자 통계에 대 한 모든 카운터는 64 비트 너비의 <xref:System.Int64> 공용 언어 런타임 형식 C# (**long** in 및 Visual Basic)을 사용 합니다. Int64에서 정의한 **int64** 데이터 형식의 최대값입니다 **. Int32.maxvalue** field, is ((2 ^ 63)-1)). 카운터의 값이 최대값에 도달하면 더 이상 정확한 값으로 간주하지 않습니다. 이는 int64 임을 의미 **합니다. Int32.maxvalue**-1 ((2 ^ 63)-2)은 효과적으로 모든 통계에 유효한 값입니다.  
  
> [!NOTE]
> 나중에 반환된 통계의 수, 이름 및 순서가 변경될 수 있으므로 공급자 통계를 반환하는 데 사전을 사용합니다. 애플리케이션에서는 사전에서 검색된 특정 값에 의존해서는 안 되지만, 값이 사전과 해당 분기에 있는지 확인해야 합니다.  
  
 다음 표에서는 현재 사용할 수 있는 통계 값에 대해 설명합니다. 개별 값의 키 이름은 Microsoft .NET Framework의 국가별 버전에서 지역화되어 있지 않습니다.  
  
|키 이름|Description|  
|--------------|-----------------|  
|`BuffersReceived`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 SQL Server에서 공급자가 받은 TDS(Tabular Data Stream) 패킷의 수를 반환합니다.|  
|`BuffersSent`|통계를 활성화한 후 공급자가 SQL Server로 보낸 TDS 패킷의 수를 반환합니다. 긴 명령의 경우 버퍼가 여러 개 필요할 수 있습니다. 예를 들어, 긴 명령이 서버로 전송되고 6개의 패킷이 필요한 경우 `ServerRoundtrips`는 1개씩 증가하며 `BuffersSent`는 6개씩 증가합니다.|  
|`BytesReceived`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 SQL Server에서 공급자가 받은 TDS 패킷의 데이터 바이트 수를 반환합니다.|  
|`BytesSent`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 TDS 패킷의 SQL Server로 전송된 데이터 바이트 수를 반환합니다.|  
|`ConnectionTime`|통계가 활성화된 후 연결이 열려 있던 시간(밀리초)입니다(연결을 열기 전에 통계를 활성화한 경우에는 총 연결 시간).|  
|`CursorOpens`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 연결을 통해 커서가 열린 횟수를 반환합니다.<br /><br /> SELECT 문이 반환하는 정방향 읽기 전용 결과는 커서로 간주되지 않으므로 이 카운터에 영향을 주지 않습니다.|  
|`ExecutionTime`|통계가 활성화된 후 서버의 응답을 기다린 시간과 공급자 자체에서 코드를 실행하는 데 걸린 시간을 포함하여 공급자에서 처리에 소요된 누적 시간(밀리초)을 반환합니다.<br /><br /> 타이밍 코드를 포함하는 클래스는 다음과 같습니다.<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> 성능이 중요한 멤버를 가능한 작게 유지하려면 다음 멤버는 적합하지 않습니다.<br /><br /> SqlDataReader<br /><br /> 이 [] 연산자(모든 오버로드)<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 연결을 통해 실행되는 INSERT, DELETE 및 UPDATE 문의 총 수를 반환합니다.|  
|`IduRows`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 연결을 통해 실행되는 INSERT, DELETE 및 UPDATE 문에 영향을 받은 전체 행 수를 반환합니다.|  
|`NetworkServerTime`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 공급자에서 서버의 응답을 기다리는 데 소요된 누적 시간(밀리초)을 반환합니다.|  
|`PreparedExecs`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 연결을 통해 실행되는 준비된 명령 수를 반환합니다.|  
|`Prepares`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 연결을 통해 준비된 문 수를 반환합니다.|  
|`SelectCount`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 연결을 통해 실행된 SELECT 문의 수를 반환합니다. 여기에는 커서에서 행을 검색하는 FETCH 문이 포함되며 <xref:System.Data.SqlClient.SqlDataReader>의 끝에 도달하면 SELECT 문의 수가 업데이트됩니다.|  
|`SelectRows`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 선택된 행 수를 반환합니다. 이 카운터는 호출자가 실제로 사용하지 않은 행을 포함해서 SQL 문에서 생성된 모든 행을 나타냅니다. 예를 들어, 전체 결과 집합을 읽기 전에 데이터 판독기를 닫으면 개수가 달라지지 않습니다. 여기에는 FETCH 문을 통해 커서에서 검색한 행도 포함됩니다.|  
|`ServerRoundtrips`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 연결에서 서버로 명령을 보내고 응답을 받은 횟수를 반환합니다.|  
|`SumResultSets`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 사용된 결과 집합의 수를 반환합니다. 예를 들어, 여기에는 클라이언트로 반환된 모든 결과 집합이 포함됩니다. 커서의 경우 각 반입 또는 블록 반입 작업은 개별 결과 집합으로 간주됩니다.|  
|`Transactions`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 시작된 사용자 트랜잭션의 수를 반환합니다. 자동 커밋 기능이 작동되는 상태에서 연결을 실행하면 각 명령은 트랜잭션으로 간주됩니다.<br /><br /> 이 카운터는 트랜잭션이 나중에 커밋되든 롤백되든 상관없이 BEGIN TRAN 문이 실행되는 즉시 트랜잭션 수를 증가시킵니다.|  
|`UnpreparedExecs`|애플리케이션에서 공급자 사용을 시작하고 통계를 활성화한 후 실행된 준비되지 않은 문의 수를 반환합니다.|  
  
### <a name="retrieving-a-value"></a>값 검색  
 다음 콘솔 애플리케이션에서는 연결에서 통계를 활성화하고 네 가지 개별 통계 값을 검색하여 콘솔 창에 쓰는 방법을 보여 줍니다.  
  
> [!NOTE]
> 다음 예에서는 SQL Server에 포함 된 샘플 **AdventureWorks** 데이터베이스를 사용 합니다. 샘플 코드에 제공된 연결 문자열은 데이터베이스가 로컬 컴퓨터에 설치되었으며 사용 가능하다고 가정합니다. 사용자 환경의 필요에 따라 연결 문자열을 수정합니다.  
  
```vb  
Option Strict On  
  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim connectionString As String = GetConnectionString()  
  
    Using awConnection As New SqlConnection(connectionString)  
      ' StatisticsEnabled is False by default.  
      ' It must be set to True to start the   
      ' statistic collection process.  
      awConnection.StatisticsEnabled = True  
  
      Dim productSQL As String = "SELECT * FROM Production.Product"  
      Dim productAdapter As _  
          New SqlDataAdapter(productSQL, awConnection)  
  
      Dim awDataSet As New DataSet()  
  
      awConnection.Open()  
  
      productAdapter.Fill(awDataSet, "ProductTable")  
  
      ' Retrieve the current statistics as  
      ' a collection of values at this point  
      ' and time.  
      Dim currentStatistics As IDictionary = _  
          awConnection.RetrieveStatistics()  
  
      Console.WriteLine("Total Counters: " & _  
          currentStatistics.Count.ToString())  
      Console.WriteLine()  
  
      ' Retrieve a few individual values  
      ' related to the previous command.  
      Dim bytesReceived As Long = _  
          CLng(currentStatistics.Item("BytesReceived"))  
      Dim bytesSent As Long = _  
          CLng(currentStatistics.Item("BytesSent"))  
      Dim selectCount As Long = _  
          CLng(currentStatistics.Item("SelectCount"))  
      Dim selectRows As Long = _  
          CLng(currentStatistics.Item("SelectRows"))  
  
      Console.WriteLine("BytesReceived: " & bytesReceived.ToString())  
      Console.WriteLine("BytesSent: " & bytesSent.ToString())  
      Console.WriteLine("SelectCount: " & selectCount.ToString())  
      Console.WriteLine("SelectRows: " & selectRows.ToString())  
  
      Console.WriteLine()  
      Console.WriteLine("Press any key to continue")  
      Console.ReadLine()  
    End Using  
  
  End Sub  
  
  Function GetConnectionString() As String  
    ' To avoid storing the connection string in your code,  
    ' you can retrieve it from a configuration file.  
    Return "Data Source=localhost;Integrated Security=SSPI;" & _  
      "Initial Catalog=AdventureWorks"  
  End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace CS_Stats_Console_GetValue  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =   
          new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
          awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
          currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        // Retrieve a few individual values  
        // related to the previous command.  
        long bytesReceived =  
            (long) currentStatistics["BytesReceived"];  
        long bytesSent =  
            (long) currentStatistics["BytesSent"];  
        long selectCount =  
            (long) currentStatistics["SelectCount"];  
        long selectRows =  
            (long) currentStatistics["SelectRows"];  
  
        Console.WriteLine("BytesReceived: " +  
            bytesReceived.ToString());  
        Console.WriteLine("BytesSent: " +  
            bytesSent.ToString());  
        Console.WriteLine("SelectCount: " +  
            selectCount.ToString());  
        Console.WriteLine("SelectRows: " +  
            selectRows.ToString());  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
### <a name="retrieving-all-values"></a>모든 값 검색  
 다음 콘솔 애플리케이션에서는 연결에서 통계를 활성화하고 열거자를 사용하여 모든 사용 가능한 통계 값을 검색한 후 콘솔 창에 쓰는 방법을 보여 줍니다.  
  
> [!NOTE]
> 다음 예에서는 SQL Server에 포함 된 샘플 **AdventureWorks** 데이터베이스를 사용 합니다. 샘플 코드에 제공된 연결 문자열은 데이터베이스가 로컬 컴퓨터에 설치되었으며 사용 가능하다고 가정합니다. 사용자 환경의 필요에 따라 연결 문자열을 수정합니다.  
  
```vb  
Option Strict On  
  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  Sub Main()  
    Dim connectionString As String = GetConnectionString()  
  
    Using awConnection As New SqlConnection(connectionString)  
      ' StatisticsEnabled is False by default.  
      ' It must be set to True to start the   
      ' statistic collection process.  
      awConnection.StatisticsEnabled = True  
  
      Dim productSQL As String = "SELECT * FROM Production.Product"  
      Dim productAdapter As _  
          New SqlDataAdapter(productSQL, awConnection)  
  
      Dim awDataSet As New DataSet()  
  
      awConnection.Open()  
  
      productAdapter.Fill(awDataSet, "ProductTable")  
  
      ' Retrieve the current statistics as  
      ' a collection of values at this point  
      ' and time.  
      Dim currentStatistics As IDictionary = _  
          awConnection.RetrieveStatistics()  
  
      Console.WriteLine("Total Counters: " & _  
          currentStatistics.Count.ToString())  
      Console.WriteLine()  
  
      Console.WriteLine("Key Name and Value")  
  
      ' Note the entries are unsorted.  
      For Each entry As DictionaryEntry In currentStatistics  
        Console.WriteLine(entry.Key.ToString() & _  
            ": " & entry.Value.ToString())  
      Next  
  
      Console.WriteLine()  
      Console.WriteLine("Press any key to continue")  
      Console.ReadLine()  
    End Using  
  
  End Sub  
  
  Function GetConnectionString() As String  
    ' To avoid storing the connection string in your code,  
    ' you can retrieve it from a configuration file.  
    Return "Data Source=localhost;Integrated Security=SSPI;" & _  
      "Initial Catalog=AdventureWorks"  
  End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace CS_Stats_Console_GetAll  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =  
            new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
            awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
            currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        Console.WriteLine("Key Name and Value");  
  
        // Note the entries are unsorted.  
        foreach (DictionaryEntry entry in currentStatistics)  
        {  
          Console.WriteLine(entry.Key.ToString() +  
              ": " + entry.Value.ToString());  
        }  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [SQL Server 및 ADO.NET](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
