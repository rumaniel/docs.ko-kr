---
title: 쿼리 알림 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.openlocfilehash: 9919bad113eb11a38ce137a2cbbf6c67bd5b21ef
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794079"
---
# <a name="enabling-query-notifications"></a>쿼리 알림 사용
쿼리 알림을 사용하는 애플리케이션에는 공통적인 요구 사항이 적용됩니다. SQL 쿼리 알림을 지원하도록 데이터 소스를 올바르게 구성해야 하며, 사용자는 올바른 클라이언트측 및 서버측 권한을 가지고 있어야 합니다.  
  
 쿼리 알림을 사용하려면 다음을 수행해야 합니다.  
  
- 데이터베이스에 대해 쿼리 알림을 활성화합니다.  
  
- 데이터베이스 연결에 사용되는 사용자 ID에 필요한 권한이 있는지 확인합니다.  
  
- <xref:System.Data.SqlClient.SqlCommand> 개체를 사용하여 <xref:System.Data.SqlClient.SqlDependency> 또는 <xref:System.Data.Sql.SqlNotificationRequest>와 같은 관련된 알림 개체로 올바른 SELECT 문을 실행합니다.  
  
- 모니터링하는 데이터가 변경될 경우 알림을 처리하는 코드를 제공합니다.  
  
## <a name="query-notifications-requirements"></a>쿼리 알림 요구 사항  
 다음과 같은 요구 사항을 충족하는 SELECT 문에 대해 쿼리 알림을 사용할 수 있습니다. 다음 표에는 SQL Server 온라인 설명서의 Service Broker 및 쿼리 알림 문서에 대한 링크가 나와 있습니다.  
  
 **SQL Server 설명서**  
  
- [알림에 대 한 쿼리 만들기](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Service Broker에 대 한 보안 고려 사항](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [보안 및 보호 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [알림 서비스에 대 한 보안 고려 사항](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [쿼리 알림 사용 권한](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Service Broker에 대 한 국가별 고려 사항](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [솔루션 디자인 고려 사항 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker Developer 정보 센터](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [개발자 가이드 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>쿼리 알림 활성화 샘플 코드  
 SQL Server Management Studio를 사용 하 여 **AdventureWorks** 데이터베이스에서 Service Broker를 사용 하도록 설정 하려면 다음 transact-sql 문을 실행 합니다.  
  
 `ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
 쿼리 알림 샘플을 올바르게 실행하려면 데이터베이스 서버에서 다음 Transact-SQL 문을 실행해야 합니다.  
  
```  
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>쿼리 알림 권한  
 알림 요청 명령을 실행하는 사용자는 서버에 대해 SUBSCRIBE QUERY NOTIFICATIONS 데이터베이스 권한을 가지고 있어야 합니다.  
  
 부분 신뢰 상황에서 실행되는 클라이언트측 코드의 경우에는 <xref:System.Data.SqlClient.SqlClientPermission>이 필요합니다.  
  
 다음 코드에서는 <xref:System.Data.SqlClient.SqlClientPermission> 개체를 만들고 <xref:System.Security.Permissions.PermissionState>를 <xref:System.Security.Permissions.PermissionState.Unrestricted>로 설정합니다. <xref:System.Security.CodeAccessPermission.Demand%2A>는 호출 스택의 상위 호출자에게 권한이 없는 경우 런타임에 <xref:System.Security.SecurityException>을 발생시킵니다.  
  
 [!code-csharp[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/CS/source.cs#1)]
 [!code-vb[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/VB/source.vb#1)]  
  
## <a name="choosing-a-notification-object"></a>알림 개체 선택  
 쿼리 알림 API에서는 알림을 처리하기 위한 두 개의 개체인 <xref:System.Data.SqlClient.SqlDependency> 및 <xref:System.Data.Sql.SqlNotificationRequest>를 제공합니다. 일반적으로 대부분의 비 ASP.NET 애플리케이션에서는 <xref:System.Data.SqlClient.SqlDependency> 개체를 사용합니다. ASP.NET 애플리케이션에서는 상위 수준의 <xref:System.Web.Caching.SqlCacheDependency>를 사용하여 <xref:System.Data.SqlClient.SqlDependency>를 래핑하고 알림 및 캐시 개체를 관리하기 위한 프레임워크를 제공합니다.  
  
### <a name="using-sqldependency"></a>SqlDependency 사용  
 <xref:System.Data.SqlClient.SqlDependency>를 사용하려면 사용 중인 SQL Server 데이터베이스에 대해 Service Broker를 활성화해야 하며 사용자는 알림을 수신할 수 있는 권한이 있어야 합니다. 알림 큐 같은 Service Broker 개체는 미리 정의되어 있습니다.  
  
 또한 <xref:System.Data.SqlClient.SqlDependency>는 작업자 스레드를 자동으로 실행하여 큐에 게시되는 알림을 처리하고, Service Broker 메시지를 구문 분석하여 해당 정보를 이벤트 인수 데이터로 노출합니다. <xref:System.Data.SqlClient.SqlDependency>는 `Start` 메서드를 호출하여 데이터베이스에 대해 종속성을 설정함으로써 초기화해야 합니다. 이 메서드는 애플리케이션을 초기화하는 동안 필요한 데이터베이스 연결마다 한 번씩만 호출해야 하는 정적 메서드입니다. 만들어진 각 종속성 연결에 대해 애플리케이션이 종료될 때 `Stop` 메서드를 호출해야 합니다.  
  
### <a name="using-sqlnotificationrequest"></a>SqlNotificationRequest 사용  
 이와 반대로 <xref:System.Data.Sql.SqlNotificationRequest>를 사용하려면 전체 수신 인프라를 직접 구현해야 합니다. 또한 큐, 서비스, 큐에서 지원하는 메시지 유형 같은 모든 지원되는 Service Broker 개체를 정의해야 합니다. 이 수동 접근 방식은 애플리케이션에 특별한 알림 메시지 또는 알림 동작이 필요하거나 애플리케이션이 보다 큰 Service Broker 애플리케이션에 속해 있는 경우에 유용합니다.  
  
## <a name="see-also"></a>참고자료

- [SQL Server에서 쿼리 알림](query-notifications-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
