---
title: 단일 대량 복사 작업
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5e7ff0be-3f23-4996-a92c-bd54d65c3836
ms.openlocfilehash: 05e3cf25352e731d320061001f08a835cd520b15
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780921"
---
# <a name="single-bulk-copy-operations"></a>단일 대량 복사 작업

SQL Server 대량 복사 작업을 수행하는 가장 간단한 접근 방식은 데이터베이스에 단일 작업을 수행하는 것입니다. 기본적으로 대량 복사 작업은 격리된 작업으로 수행됩니다. 복사 작업은 롤백할 수 없는 비트랜잭트 방식으로 이루어집니다.

> [!NOTE]
> 오류가 발생할 때 대량 복사의 전체 또는 일부를 롤백해야 하는 경우에는 <xref:System.Data.SqlClient.SqlBulkCopy>에서 관리되는 트랜잭션을 사용하거나 기존 트랜잭션 내에서 대량 복사 작업을 수행할 수 있습니다. **SqlBulkCopy** 는 연결이 <xref:System.Transactions> **시스템 트랜잭션** 트랜잭션에 암시적 또는 명시적으로 참여 하는 경우에도 작동 합니다.
>
> 자세한 내용은 [트랜잭션 및 대량 복사 작업](transaction-and-bulk-copy-operations.md)을 참조 하세요.

일반적으로 대량 복사 작업을 수행하는 단계는 다음과 같습니다.

1. 소스 서버에 연결하고 복사할 데이터를 가져옵니다. 데이터를 <xref:System.Data.IDataReader> 또는 <xref:System.Data.DataTable> 개체에서 검색할 수 있으면 다른 소스에서 가져올 수도 있습니다.

2. **SqlBulkCopy** 에 대 한 연결을 설정 하지 않으려는 경우 대상 서버에 연결 합니다.

3. <xref:System.Data.SqlClient.SqlBulkCopy> 개체를 만들고 필요한 속성을 설정합니다.

4. **Destinationtablename** 속성을 설정 하 여 대량 삽입 작업의 대상 테이블을 표시 합니다.

5. **WriteToServer** 메서드 중 하나를 호출 합니다.

6. 필요에 따라 속성을 업데이트 하 고 **WriteToServer** 를 다시 호출 합니다.

7. <xref:System.Data.SqlClient.SqlBulkCopy.Close%2A>를 호출하거나 대량 복사 작업을 `Using` 문 내에 래핑합니다.

> [!CAUTION]
> 소스 열과 대상 열의 데이터 형식은 일치하는 것이 좋습니다. 데이터 형식이 일치 하지 않는 경우 **SqlBulkCopy** 는에서 <xref:System.Data.SqlClient.SqlParameter.Value%2A>사용 하는 규칙을 사용 하 여 각 원본 값을 대상 데이터 형식으로 변환 하려고 합니다. 변환을 수행하면 성능에 영향을 줄 뿐 아니라 예기치 않은 오류가 발생할 수도 있습니다. 예를 들어, `Double` 데이터 형식은 일반적으로 `Decimal` 데이터 형식으로 변환되지만 항상 그런 것은 아닙니다.

## <a name="example"></a>예제

다음 콘솔 애플리케이션에서는 <xref:System.Data.SqlClient.SqlBulkCopy> 클래스를 사용하여 데이터를 로드하는 방법을 보여 줍니다. 이 예제에서는 <xref:System.Data.SqlClient.SqlDataReader> 에서 데이터를 복사 하는 데 사용 되는 **Production.Product** SQL Server의 테이블 **AdventureWorks** 동일한 데이터베이스의 유사한 테이블에는 데이터베이스입니다.

> [!IMPORTANT]
> 이 샘플에 설명 된 대로 작업 테이블을 만든 경우가 아니면 실행 되지 것입니다 [대량 복사 예제 설정](bulk-copy-example-setup.md)합니다. 이 코드는 사용 하는 구문을 보여 주기 위해 제공 됩니다 **SqlBulkCopy** 만 합니다. 소스 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있으면 Transact-SQL `INSERT … SELECT` 문을 사용하여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.

[!code-csharp[DataWorks BulkCopy.Single#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks BulkCopy.Single/CS/source.cs#1)]
[!code-vb[DataWorks BulkCopy.Single#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks BulkCopy.Single/VB/source.vb#1)]

## <a name="performing-a-bulk-copy-operation-using-transact-sql-and-the-command-class"></a>Transact-SQL 및 Command 클래스를 사용하여 대량 복사 작업 수행

다음 예제에서는 <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> 메서드를 사용하여 BULK INSERT 문을 실행하는 방법을 보여 줍니다.

> [!NOTE]
> 데이터 소스의 파일 경로는 서버에 대해 상대적입니다. 대량 복사 작업을 올바르게 수행하려면 서버 프로세스에서 해당 경로에 액세스할 수 있어야 합니다.

```vb
Using connection As SqlConnection = New SqlConnection(connectionString)
Dim queryString As String = _
    "BULK INSERT Northwind.dbo.[Order Details] FROM " & _
    "'f:\mydata\data.tbl' WITH (FORMATFILE='f:\mydata\data.fmt' )"
connection.Open()
SqlCommand command = New SqlCommand(queryString, connection);

command.ExecuteNonQuery()
End Using
```

```csharp
using (SqlConnection connection = New SqlConnection(connectionString))
{
string queryString =  "BULK INSERT Northwind.dbo.[Order Details] " +
    "FROM 'f:\mydata\data.tbl' " +
    "WITH ( FORMATFILE='f:\mydata\data.fmt' )";
connection.Open();
SqlCommand command = new SqlCommand(queryString, connection);

command.ExecuteNonQuery();
}
```

## <a name="see-also"></a>참고자료

- [SQL Server에서 대량 복사 작업](bulk-copy-operations-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
