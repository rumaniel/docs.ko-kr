---
title: SqlNotificationRequest를 사용하여 SqlCommand 실행
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.openlocfilehash: 3115bfb80d4e5e61ed49da11e36eaa37bc24334f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791539"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>SqlNotificationRequest를 사용하여 SqlCommand 실행

데이터가 서버에서 반입된 후 변경될 때 알림을 생성하도록 <xref:System.Data.SqlClient.SqlCommand>를 구성할 수 있으며 쿼리가 다시 실행된 경우 결과 집합은 달라질 수 있습니다. 이 기능은 서버에 사용자 지정 알림 큐를 사용하려는 경우나 활성 개체를 유지하지 않으려는 경우에 유용합니다.

## <a name="creating-the-notification-request"></a>Notification 요청 만들기

<xref:System.Data.Sql.SqlNotificationRequest> 개체를 사용하여 `SqlCommand`개체에 바인딩하여 알림 요청을 만들 수 있습니다. 요청이 만들어지면 `SqlNotificationRequest` 개체는 더 이상 필요하지 않습니다. 알림에 대해 큐를 쿼리하여 적절하게 응답할 수 있습니다. 애플리케이션이 종료된 후 나중에 다시 시작하더라도 알림이 발생할 수 있습니다.

연결된 알림에 대한 명령이 실행될 때 원래 결과 집합에 대한 변경 사항이 있으면 알림 요청에 구성되어 있는 SQL Server 큐로 메시지를 보내는 작업이 트리거됩니다.

SQL Server 큐를 폴링하고 메시지를 해석하는 방법은 애플리케이션에 따라 다릅니다. 애플리케이션에서는 큐를 폴링하고 메시지의 내용에 따라 반응하는 작업을 수행합니다.

> [!NOTE]
> <xref:System.Data.SqlClient.SqlDependency>를 사용하여 SQL Server 알림 요청을 사용하는 경우 기본 서비스 이름을 사용하는 대신 사용자 고유의 큐 이름을 만드세요.

<xref:System.Data.Sql.SqlNotificationRequest>에 대한 새로운 클라이언트측 보안 요소는 없습니다. 이는 대부분 서버 기능이며 서버에는 사용자가 알림을 요청하기 위해 가져야 하는 특별한 권한이 만들어져 있습니다.

### <a name="example"></a>예제

다음 코드 조각에서는 <xref:System.Data.Sql.SqlNotificationRequest>를 만들어 <xref:System.Data.SqlClient.SqlCommand>에 연결하는 방법을 보여 줍니다.

```vb
' Assume connection is an open SqlConnection.
' Create a new SqlCommand object.
Dim command As New SqlCommand( _
  "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection)

' Create a SqlNotificationRequest object.
Dim notifcationRequest As New SqlNotificationRequest()
notificationRequest.id = "NotificationID"
notificationRequest.Service = "mySSBQueue"

' Associate the notification request with the command.
command.Notification = notificationRequest
' Execute the command.
command.ExecuteReader()
' Process the DataReader.
' You can use Transact-SQL syntax to periodically poll the
' SQL Server queue to see if you have a new message.
```

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="see-also"></a>참고자료

- [SQL Server에서 쿼리 알림](query-notifications-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
