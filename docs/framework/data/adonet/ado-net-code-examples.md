---
title: ADO.NET 코드 예제
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c119657a-9ce6-4940-91e4-ac1d5f0d9584
ms.openlocfilehash: 86d5fc63168330502f81dfa464fcd2c04f014760
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785056"
---
# <a name="adonet-code-examples"></a>ADO.NET 코드 예제
이 항목에 나열된 코드에서는 다음과 같은 ADO.NET 기술을 사용하여 데이터베이스에서 데이터를 검색하는 방법을 보여 줍니다.

- ADO.NET 데이터 공급자

  - [SqlClient](#sqlclient) (`System.Data.SqlClient`)

  - [OleDb](#oledb) (`System.Data.OleDb`)

  - [Odbc](#odbc) (`System.Data.Odbc`)

  - [OracleClient](#oracleclient) (`System.Data.OracleClient`)

- ADO.NET Entity Framework:

  - [LINQ to Entities](#linq-to-entities)

  - [형식화 된 ObjectQuery](#typed-objectquery)

  - [EntityClient](#entityclient) (`System.Data.EntityClient`)

- [LINQ to SQL](#linq-to-sql)

## <a name="adonet-data-provider-examples"></a>ADO.NET 데이터 공급자 예제
다음에 나열된 코드에서는 ADO.NET 데이터 공급자를 사용하여 데이터베이스에서 데이터를 검색하는 방법을 보여 줍니다. 데이터는 `DataReader`에서 반환됩니다. 자세한 내용은 [DataReader를 사용 하 여 데이터 검색](retrieving-data-using-a-datareader.md)을 참조 하세요.

### <a name="sqlclient"></a>SqlClient
이 예제의 코드는 Microsoft SQL Server에서 `Northwind` 예제 데이터베이스에 연결할 수 있다고 가정 합니다. 이 코드에서는 Products 테이블에서 행을 선택하는 <xref:System.Data.SqlClient.SqlCommand>를 만들고 <xref:System.Data.SqlClient.SqlParameter>를 추가하여 UnitPrice가 지정한 매개 변수 값(이 경우 5)보다 큰 행만 반환되도록 제한합니다. 는 <xref:System.Data.SqlClient.SqlConnection> 블록`using` 내에서 열리므로 코드가 종료 될 때 리소스가 닫히고 삭제 되도록 합니다. 이 코드에서는 <xref:System.Data.SqlClient.SqlDataReader>를 사용하여 명령을 실행하고 결과를 콘솔 창에 표시합니다.

 [!code-csharp[DataWorks SampleApp.SqlClient#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.SqlClient/CS/source.cs#1)]
 [!code-vb[DataWorks SampleApp.SqlClient#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.SqlClient/VB/source.vb#1)]

### <a name="oledb"></a>OleDb
이 예제 코드에서는 Microsoft Access Northwind 샘플 데이터베이스에 연결할 수 있다고 가정합니다. 이 코드에서는 Products 테이블에서 행을 선택하는 <xref:System.Data.OleDb.OleDbCommand>를 만들고 <xref:System.Data.OleDb.OleDbParameter>를 추가하여 UnitPrice가 지정한 매개 변수 값(이 경우 5)보다 큰 행만 반환되도록 제한합니다. 코드가 종료될 때 리소스가 닫히고 삭제되도록 <xref:System.Data.OleDb.OleDbConnection>이 `using` 블록 안에서 열립니다. 이 코드에서는 <xref:System.Data.OleDb.OleDbDataReader>를 사용하여 명령을 실행하고 결과를 콘솔 창에 표시합니다.

 [!code-csharp[DataWorks SampleApp.OleDb#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.OleDb/CS/source.cs#1)]
 [!code-vb[DataWorks SampleApp.OleDb#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.OleDb/VB/source.vb#1)]

### <a name="odbc"></a>Odbc
이 예제 코드에서는 Microsoft Access Northwind 샘플 데이터베이스에 연결할 수 있다고 가정합니다. 이 코드에서는 Products 테이블에서 행을 선택하는 <xref:System.Data.Odbc.OdbcCommand>를 만들고 <xref:System.Data.Odbc.OdbcParameter>를 추가하여 UnitPrice가 지정한 매개 변수 값(이 경우 5)보다 큰 행만 반환되도록 제한합니다. 는 <xref:System.Data.Odbc.OdbcConnection> 블록`using` 내에서 열리므로 코드가 종료 될 때 리소스가 닫히고 삭제 되도록 합니다. 이 코드에서는 <xref:System.Data.Odbc.OdbcDataReader>를 사용하여 명령을 실행하고 결과를 콘솔 창에 표시합니다.

[!code-csharp[DataWorks SampleApp.Odbc#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.Odbc/CS/source.cs#1)] 
[!code-vb[DataWorks SampleApp.Odbc#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.Odbc/VB/source.vb#1)] 

### <a name="oracleclient"></a>OracleClient
이 예제 코드에서는 Oracle 서버에서 DEMO.CUSTOMER에 연결할 수 있다고 가정합니다. 또한 System.Data.OracleClient.dll에 대한 참조를 추가해야 합니다. 이 코드는 <xref:System.Data.OracleClient.OracleDataReader>에 데이터를 반환합니다.

 [!code-csharp[DataWorks SampleApp.Oracle#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.Oracle/CS/source.cs#1)]
 [!code-vb[DataWorks SampleApp.Oracle#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.Oracle/VB/source.vb#1)]

## <a name="entity-framework-examples"></a>Entity Framework 예제
다음에 나열된 코드에서는 EDM(엔터티 데이터 모델)의 엔터티를 쿼리하여 데이터 소스에서 데이터를 검색하는 방법을 보여 줍니다. 이 예에서는 Northwind 샘플 데이터베이스를 기반으로 하는 모델을 사용 합니다. Entity Framework에 대 한 자세한 내용은 [Entity Framework 개요](./ef/overview.md)를 참조 하세요.

### <a name="linq-to-entities"></a>LINQ to Entities
이 예제 코드에서는 LINQ 쿼리를 사용하여 CategoryID와 CategoryName 속성만 포함된 익명 형식으로 프로젝션된 Categories 개체로 데이터를 반환합니다. 자세한 내용은 [LINQ to Entities 개요](./ef/language-reference/linq-to-entities.md)를 참조 하세요.

```csharp
using System;
using System.Linq;
using System.Data.Objects;
using NorthwindModel;

class LinqSample
{
    public static void ExecuteQuery()
    {
        using (NorthwindEntities context = new NorthwindEntities())
        {
            try
            {
                var query = from category in context.Categories
                            select new
                            {
                                categoryID = category.CategoryID,
                                categoryName = category.CategoryName
                            };

                foreach (var categoryInfo in query)
                {
                    Console.WriteLine("\t{0}\t{1}",
                        categoryInfo.categoryID, categoryInfo.categoryName);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

```vb
Option Explicit On
Option Strict On

Imports System
Imports System.Linq
Imports System.Data.Objects
Imports NorthwindModel

Class LinqSample
    Public Shared Sub ExecuteQuery()
        Using context As NorthwindEntities = New NorthwindEntities()
            Try
                Dim query = From category In context.Categories _
                            Select New With _
                            { _
                                .categoryID = category.CategoryID, _
                                .categoryName = category.CategoryName _
                            }

                For Each categoryInfo In query
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                        categoryInfo.categoryID, categoryInfo.categoryName)
                Next
            Catch ex As Exception
                Console.WriteLine(ex.Message)
            End Try
        End Using
    End Sub
End Class
```

### <a name="typed-objectquery"></a>형식화된 ObjectQuery
이 예제 코드에서는 <xref:System.Data.Objects.ObjectQuery%601>을 사용하여 데이터를 Categories 개체로 반환합니다. 자세한 내용은 [개체 쿼리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896241(v=vs.100))합니다.

```csharp
using System;
using System.Data.Objects;
using NorthwindModel;

class ObjectQuerySample
{
    public static void ExecuteQuery()
    {
        using (NorthwindEntities context = new NorthwindEntities())
        {
            ObjectQuery<Categories> categoryQuery = context.Categories;

            foreach (Categories category in 
                categoryQuery.Execute(MergeOption.AppendOnly))
            {
                Console.WriteLine("\t{0}\t{1}",
                    category.CategoryID, category.CategoryName);
            }
        }
    }
}
```

```vb
Option Explicit On
Option Strict On

Imports System
Imports System.Data.Objects
Imports NorthwindModel

Class ObjectQuerySample
    Public Shared Sub ExecuteQuery()
        Using context As NorthwindEntities = New NorthwindEntities()
            Dim categoryQuery As ObjectQuery(Of Categories) = context.Categories

            For Each category As Categories In _
                categoryQuery.Execute(MergeOption.AppendOnly)
                Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                    category.CategoryID, category.CategoryName)
            Next
        End Using
    End Sub
End Class
```

### <a name="entityclient"></a>EntityClient
이 예제 코드에서는 <xref:System.Data.EntityClient.EntityCommand>를 사용하여 Entity SQL 쿼리를 실행합니다. 이 쿼리는 Categories 엔터티 형식의 인스턴스를 나타내는 레코드 목록을 반환합니다. <xref:System.Data.EntityClient.EntityDataReader>를 사용하여 결과 집합의 데이터 레코드에 액세스합니다. 자세한 내용은 [Entity Framework에 대 한 EntityClient 공급자](./ef/entityclient-provider-for-the-entity-framework.md)를 참조 하세요.

```csharp
using System;
using System.Data;
using System.Data.Common;
using System.Data.EntityClient;
using NorthwindModel;

class EntityClientSample
{
    public static void ExecuteQuery()
    {
        string queryString =
            @"SELECT c.CategoryID, c.CategoryName 
                FROM NorthwindEntities.Categories AS c";

        using (EntityConnection conn =
            new EntityConnection("name=NorthwindEntities"))
        {
            try
            {
                conn.Open();
                using (EntityCommand query = new EntityCommand(queryString, conn))
                {
                    using (DbDataReader rdr = 
                        query.ExecuteReader(CommandBehavior.SequentialAccess))
                    {
                        while (rdr.Read())
                        {
                            Console.WriteLine("\t{0}\t{1}", rdr[0], rdr[1]);
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

```vb
Option Explicit On
Option Strict On

Imports System
Imports System.Data
Imports System.Data.Common
Imports System.Data.EntityClient
Imports NorthwindModel

Class EntityClientSample
    Public Shared Sub ExecuteQuery()
        Dim queryString As String = _
            "SELECT c.CategoryID, c.CategoryName " & _
                "FROM NorthwindEntities.Categories AS c"

        Using conn As EntityConnection = _
            New EntityConnection("name=NorthwindEntities")

            Try
                conn.Open()
                Using query As EntityCommand = _
                New EntityCommand(queryString, conn)
                    Using rdr As DbDataReader = _
                        query.ExecuteReader(CommandBehavior.SequentialAccess)
                        While rdr.Read()
                            Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                                              rdr(0), rdr(1))
                        End While
                    End Using
                End Using
            Catch ex As Exception
                Console.WriteLine(ex.Message)
            End Try
        End Using 
    End Sub
End Class
```

## <a name="linq-to-sql"></a>LINQ to SQL
이 예제 코드에서는 LINQ 쿼리를 사용하여 CategoryID와 CategoryName 속성만 포함된 익명 형식으로 프로젝션된 Categories 개체로 데이터를 반환합니다. 이 예제는 Northwind 데이터 컨텍스트를 기반으로 합니다. 자세한 내용은 [시작](./sql/linq/getting-started.md)을 참조하십시오.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Northwind;

    class LinqSqlSample
    {
        public static void ExecuteQuery()
        {
            using (NorthwindDataContext db = new NorthwindDataContext())
            {
                try
                {
                    var query = from category in db.Categories
                                select new
                                {
                                    categoryID = category.CategoryID,
                                    categoryName = category.CategoryName
                                };

                    foreach (var categoryInfo in query)
                    {
                        Console.WriteLine("vbTab {0} vbTab {1}",
                            categoryInfo.categoryID, categoryInfo.categoryName);
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine(ex.Message);
                }
            }
        }
    }
```

```vb
Option Explicit On
Option Strict On

Imports System
Imports System.Collections.Generic
Imports System.Linq
Imports System.Text
Imports Northwind

Class LinqSqlSample
    Public Shared Sub ExecuteQuery()
        Using db As NorthwindDataContext = New NorthwindDataContext()
            Try
                Dim query = From category In db.Categories _
                                Select New With _
                                { _
                                    .categoryID = category.CategoryID, _
                                    .categoryName = category.CategoryName _
                                }

                For Each categoryInfo In query
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                            categoryInfo.categoryID, categoryInfo.categoryName)
                Next
            Catch ex As Exception
                Console.WriteLine(ex.Message)
            End Try
            End Using 
    End Sub
End Class
```

## <a name="see-also"></a>참고자료

- [ADO.NET 개요](ado-net-overview.md)
- [ADO.NET에서 데이터 검색 및 수정](retrieving-and-modifying-data.md)
- [데이터 응용 프로그램 만들기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/h0y4a0f6(v=vs.120))
- [엔터티 데이터 모델 쿼리 (Entity Framework 작업)](https://docs.microsoft.com/previous-versions/bb738455(v=vs.90))
- [방법: 익명 형식 개체를 반환 하는 쿼리 실행](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738512(v=vs.100))
