---
title: GetSchema 및 Schema 컬렉션
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7ab93b89-1221-427c-84ad-04803b3c64b4
ms.openlocfilehash: 4ac0216ce2965d555f7283ba66a085ea9d7cac3c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783843"
---
# <a name="getschema-and-schema-collections"></a>GetSchema 및 Schema 컬렉션
관리 되는 각 .NET Framework의 **연결** 클래스는 현재 연결 되어 있는 데이터베이스에 대 한 스키마 정보 및에서 **반환 된 스키마 정보를 검색 하는 데 사용 되는 GetSchema 메서드를 구현 합니다. GetSchema** 메서드는 <xref:System.Data.DataTable>의 형식으로 제공 됩니다. **GetSchema** 메서드는 반환할 스키마 컬렉션을 지정 하 고 반환 되는 정보의 양을 제한 하는 선택적 매개 변수를 제공 하는 오버 로드 된 메서드입니다.  
  
## <a name="specifying-the-schema-collections"></a>스키마 컬렉션 지정  
 **GetSchema** 메서드의 첫 번째 선택적 매개 변수는 문자열로 지정 되는 컬렉션 이름입니다. 스키마 컬렉션에는 모든 공급자에 공통되는 공통 스키마 컬렉션과 공급자마다 다른 특정 스키마 컬렉션의 두 가지 유형이 있습니다.  
  
 인수를 사용 하지 않거나 스키마 컬렉션 이름 "MetaDataCollections"를 사용 하 여 **GetSchema** 메서드를 호출 하 여 지원 되는 스키마 컬렉션 목록을 확인 하려면 .NET Framework 관리 공급자를 쿼리할 수 있습니다. 그러면 지원되는 스키마 컬렉션의 목록, 각자 지원하는 제약 조건 수 및 사용하는 식별자 부분 수가 포함된 <xref:System.Data.DataTable>이 반환됩니다.  
  
### <a name="retrieving-schema-collections-example"></a>스키마 컬렉션 검색 예제  
 다음 예에서는 SQL Server <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> <xref:System.Data.SqlClient.SqlConnection> 클래스에 대해 .NET Framework Data Provider의 메서드를 사용 하 여 **AdventureWorks** 예제 데이터베이스에 포함 된 모든 테이블에 대 한 스키마 정보를 검색 하는 방법을 보여 줍니다.  
  
```vb  
Imports System.Data.SqlClient  
  
Module Module1  
   Sub Main()  
      Dim connectionString As String = GetConnectionString()  
      Using connection As New SqlConnection(connectionString)  
         'Connect to the database then retrieve the schema information.  
         connection.Open()  
         Dim table As DataTable = connection.GetSchema("Tables")  
  
         ' Display the contents of the table.  
         DisplayData(table)  
         Console.WriteLine("Press any key to continue.")  
         Console.ReadKey()  
      End Using  
   End Sub  
  
   Private Function GetConnectionString() As String  
      ' To avoid storing the connection string in your code,    
      ' you can retrieve it from a configuration file.  
      Return "Data Source=(local);Database=AdventureWorks;" _  
         & "Integrated Security=true;"  
   End Function  
  
   Private Sub DisplayData(ByVal table As DataTable)  
      For Each row As DataRow In table.Rows  
         For Each col As DataColumn In table.Columns  
            Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
         Next  
         Console.WriteLine("============================")  
      Next  
   End Sub  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
class Program  
{  
  static void Main()  
  {  
  string connectionString = GetConnectionString();  
  using (SqlConnection connection = new SqlConnection(connectionString))  
  {  
   // Connect to the database then retrieve the schema information.  
   connection.Open();  
   DataTable table = connection.GetSchema("Tables");  
  
   // Display the contents of the table.  
   DisplayData(table);  
   Console.WriteLine("Press any key to continue.");  
   Console.ReadKey();  
   }  
 }  
  
  private static string GetConnectionString()  
  {  
   // To avoid storing the connection string in your code,  
   // you can retrieve it from a configuration file.  
   return "Data Source=(local);Database=AdventureWorks;" +  
      "Integrated Security=true;";  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
     foreach (System.Data.DataRow row in table.Rows)  
     {  
        foreach (System.Data.DataColumn col in table.Columns)  
        {  
           Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
        }  
     Console.WriteLine("============================");  
     }  
  }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [데이터베이스 스키마 정보 검색](retrieving-database-schema-information.md)
- [ADO.NET 개요](ado-net-overview.md)
