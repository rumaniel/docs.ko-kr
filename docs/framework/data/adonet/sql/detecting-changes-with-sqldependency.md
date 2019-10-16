---
title: SqlDependency로 변경 내용 감지
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
ms.openlocfilehash: 3719188064388b00c756dd037d4a475ca6debd13
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782428"
---
# <a name="detecting-changes-with-sqldependency"></a>SqlDependency로 변경 내용 감지

<xref:System.Data.SqlClient.SqlDependency> 개체를 <xref:System.Data.SqlClient.SqlCommand>와 연결하여 쿼리 결과가 원래 검색한 결과와 달라지는 시기를 검색할 수 있습니다. 또한 연결된 명령에 대한 결과가 변경될 때 발생하는 `OnChange` 이벤트에 대리자를 할당할 수도 있습니다. 명령을 실행하기 전에 먼저 <xref:System.Data.SqlClient.SqlDependency>와 해당 명령을 연결해야 합니다. `HasChanges`의 <xref:System.Data.SqlClient.SqlDependency> 속성을 사용하여 쿼리 결과가 데이터를 처음 검색했을 때의 결과와 달라졌는지 확인할 수도 있습니다.

## <a name="security-considerations"></a>보안 고려 사항

종속성 인프라는 원본으로 사용하는 데이터가 특정 명령에 대해 변경된 경우 알림을 받기 위해 <xref:System.Data.SqlClient.SqlConnection>가 호출되면 열리는 <xref:System.Data.SqlClient.SqlDependency.Start%2A>을 사용합니다. 클라이언트가 `SqlDependency.Start` 호출을 시작할 수 있는지 여부는 <xref:System.Data.SqlClient.SqlClientPermission>의 사용 및 코드 액세스 보안 특성을 통해 제어됩니다. 자세한 내용은 [쿼리 알림 사용](enabling-query-notifications.md) 및 [코드 액세스 보안 및 ADO.NET](../code-access-security.md)을 참조 하세요.

### <a name="example"></a>예제

다음 단계에서는 종속성을 선언하고, 명령을 실행하고, 결과 집합이 변경될 때 알림을 받는 방법을 설명합니다.

1. 서버에 대한 `SqlDependency` 연결을 시작합니다.

2. <xref:System.Data.SqlClient.SqlConnection> 및 <xref:System.Data.SqlClient.SqlCommand> 개체를 만들어 서버에 연결하고 Transact-SQL 문을 정의합니다.

3. 새 `SqlDependency` 개체를 만들거나 기존 개체를 사용하여 `SqlCommand` 개체에 바인딩합니다. 그러면 내부적으로 <xref:System.Data.Sql.SqlNotificationRequest> 개체가 만들어져 필요에 따라 명령 개체에 바인딩됩니다. 이 알림 요청에는 이 `SqlDependency` 개체를 고유하게 식별하는 내부 ID가 포함됩니다. 또한 이를 통해 아직 활성화되지 않은 클라이언트 수신기가 시작됩니다.

4. `OnChange` 개체의 `SqlDependency` 이벤트에 이벤트 처리기를 등록합니다.

5. `Execute` 개체의 `SqlCommand` 메서드를 사용하여 명령을 실행합니다. 명령이 알림 개체에 바인딩되기 때문에 서버에서는 알림을 생성해야 하는 것으로 인식하며 대기열 정보는 종속성 대기열을 가리킵니다.

6. 서버에 대한 `SqlDependency` 연결을 중지합니다.

사용자가 나중에 원본으로 사용하는 데이터를 변경하는 경우 Microsoft SQL Server에서는 해당 변경 내용에 대해 알림이 보류 중인 것을 감지하고 처리 후 `SqlConnection`를 호출하여 만들어진 기본 `SqlDependency.Start`을 통해 클라이언트로 전달되는 알림을 게시합니다. 클라이언트 수신기는 무효화 메시지를 받습니다. 그러면 클라이언트 수신기는 연결된 `SqlDependency` 개체를 찾아 `OnChange` 이벤트를 발생시킵니다.

다음 코드 조각에서는 샘플 애플리케이션을 만드는 데 사용할 수 있는 디자인 패턴을 보여 줍니다.

```vb
Sub Initialization()
    ' Create a dependency connection.
    SqlDependency.Start(connectionString, queueName)
End Sub

Sub SomeMethod()
    ' Assume connection is an open SqlConnection.
    ' Create a new SqlCommand object.
    Using command As New SqlCommand( _
      "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", _
      connection)

        ' Create a dependency and associate it with the SqlCommand.
        Dim dependency As New SqlDependency(command)
        ' Maintain the refernce in a class member.
        ' Subscribe to the SqlDependency event.
        AddHandler dependency.OnChange, AddressOf OnDependencyChange

        ' Execute the command.
        Using reader = command.ExecuteReader()
            ' Process the DataReader.
        End Using
    End Using
End Sub

' Handler method
Sub OnDependencyChange(ByVal sender As Object, _
    ByVal e As SqlNotificationEventArgs)
    ' Handle the event (for example, invalidate this cache entry).
End Sub

Sub Termination()
    ' Release the dependency
    SqlDependency.Stop(connectionString, queueName)
End Sub
```

```csharp
void Initialization()
{
    // Create a dependency connection.
    SqlDependency.Start(connectionString, queueName);
}

void SomeMethod()
{
    // Assume connection is an open SqlConnection.

    // Create a new SqlCommand object.
    using (SqlCommand command=new SqlCommand(
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",
        connection))
    {

        // Create a dependency and associate it with the SqlCommand.
        SqlDependency dependency=new SqlDependency(command);
        // Maintain the reference in a class member.

        // Subscribe to the SqlDependency event.
        dependency.OnChange+=new
           OnChangeEventHandler(OnDependencyChange);

        // Execute the command.
        using (SqlDataReader reader = command.ExecuteReader())
        {
            // Process the DataReader.
        }
    }
}

// Handler method
void OnDependencyChange(object sender,
   SqlNotificationEventArgs e )
{
  // Handle the event (for example, invalidate this cache entry).
}

void Termination()
{
    // Release the dependency.
    SqlDependency.Stop(connectionString, queueName);
}
```

## <a name="see-also"></a>참고자료

- [SQL Server에서 쿼리 알림](query-notifications-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
