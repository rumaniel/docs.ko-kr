---
title: SQL Server에서 데이터베이스 미러링
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.openlocfilehash: 81e8bd5ba9274c84ffe18f617978b61238ebeff2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782434"
---
# <a name="database-mirroring-in-sql-server"></a>SQL Server에서 데이터베이스 미러링
SQL Server의 데이터베이스 미러링을 사용하면 대기 서버에서 SQL Server 데이터베이스의 복사본, 즉 미러를 유지할 수 있습니다. 미러링을 사용하면 항상 두 개의 개별 데이터 복사본을 가질 수 있으므로 고가용성 및 완벽한 데이터 중복이 제공됩니다. .NET Data Provider for SQL Server에서는 데이터베이스 미러링을 암시적으로 지원하므로 SQL Server 데이터베이스에 대해 미러링이 구성되고 나면 개발자가 별도의 동작을 수행하거나 코드를 작성할 필요가 없습니다. 또한 <xref:System.Data.SqlClient.SqlConnection> 개체는 장애 조치 파트너 서버의 이름을 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>에 제공할 수 있는 명시적인 연결 모드를 지원합니다.  
  
 미러링이 구성된 데이터베이스를 대상으로 하는 <xref:System.Data.SqlClient.SqlConnection> 개체에 대해 발생하는 이벤트는 다음과 같이 간단합니다.  
  
1. 클라이언트 애플리케이션이 주 데이터베이스에 연결되고 나면 서버에서 파트너 서버의 이름을 다시 전송합니다. 그러면 이 이름이 클라이언트에 캐시됩니다.  
  
2. 주 데이터베이스를 포함하는 서버가 실패하거나 연결이 중단되면 연결 및 트랜잭션 상태를 잃게 됩니다. 클라이언트 애플리케이션에서 주 데이터베이스에 대한 연결을 다시 설정하지만 실패합니다.  
  
3. 그런 다음 클라이언트 애플리케이션에서 파트너 서버에 있는 미러 데이터베이스에 대한 연결을 투명하게 시도합니다. 연결이 설정되면 연결이 미러 데이터베이스로 리디렉션됩니다. 그리고 나면 이 데이터베이스는 새로운 주 데이터베이스가 됩니다.  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>연결 문자열에 장애 조치 파트너 지정  
 연결 문자열에 장애 조치 파트너 서버의 이름을 제공하면 클라이언트에서는 클라이언트 애플리케이션이 처음 연결될 때 주 데이터베이스를 사용할 수 없을 경우 장애 조치 파트너와의 연결을 투명하게 시도합니다.  
  
```  
";Failover Partner=PartnerServerName"  
```  
  
 장애 조치 파트너 서버의 이름을 생략하면 클라이언트 애플리케이션이 처음 연결될 때 주 데이터베이스를 사용할 수 없을 경우 <xref:System.Data.SqlClient.SqlException>이 발생합니다.  
  
 <xref:System.Data.SqlClient.SqlConnection>이 열리면 서버에서 장애 조치 파트너 이름이 반환되어 연결 문자열에 제공된 모든 값을 대신합니다.  
  
> [!NOTE]
> 데이터베이스 미러링 시나리오에서는 연결 문자열에 초기 카탈로그 또는 데이터베이스 이름을 명시적으로 지정해야 합니다. 클라이언트에서 명시적으로 지정된 초기 카탈로그 또는 데이터베이스가 없는 연결에 대한 장애 조치 정보를 받으면 장애 조치 정보가 캐시되지 않고 주 서버가 실패해도 애플리케이션에서 장애 조치를 시도하지 않습니다. 연결 문자열에 장애 조치 파트너의 값은 있지만 초기 카탈로그 또는 데이터베이스 값이 없으면 `InvalidArgumentException`이 발생합니다.  
  
## <a name="retrieving-the-current-server-name"></a>현재 서버 이름 검색  
 장애 조치가 발생하는 경우 <xref:System.Data.SqlClient.SqlConnection.DataSource%2A> 개체의 <xref:System.Data.SqlClient.SqlConnection> 속성을 사용하여 현재 연결이 실제로 연결되어 있는 서버의 이름을 검색할 수 있습니다. 다음 코드 조각에서는 연결 변수가 열린 <xref:System.Data.SqlClient.SqlConnection>을 참조한다고 가정하고 활성 서버의 이름을 검색합니다.  
  
 장애 조치 이벤트가 발생 하 고 연결이 미러 서버로 전환 되 면 **DataSource** 속성은 미러 이름을 반영 하도록 업데이트 됩니다.  
  
```vb  
Dim activeServer As String = connection.DataSource  
```  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>SqlClient 미러링 동작  
 클라이언트는 항상 현재의 주 서버에 대해 연결을 시도합니다. 연결에 실패하면 장애 조치 파트너에 대해 연결을 시도합니다. 미러 데이터베이스가 파트너 서버의 주 역할로 전환된 경우 연결이 성공하며 새 주-미러 매핑이 클라이언트로 전송되고 호출하는 <xref:System.AppDomain>의 수명 동안 캐시됩니다. 영구 저장소에 저장 되지 않으며 다른 **AppDomain** 또는 프로세스의 후속 연결에 사용할 수 없습니다. 그러나 동일한 **AppDomain**내의 후속 연결에는 사용할 수 있습니다. 동일한 컴퓨터 또는 다른 컴퓨터에서 실행 중인 다른 **AppDomain** 또는 프로세스는 항상 연결 풀을 갖고 있으며 이러한 연결은 다시 설정 되지 않습니다. 이 경우 주 데이터베이스가 다운 되 면 각 프로세스나 **AppDomain** 이 한 번 실패 하 고 풀이 자동으로 지워집니다.  
  
> [!NOTE]
> 서버에서의 미러링 지원은 데이터베이스별로 구성됩니다. multipart 이름을 사용하거나 현재 데이터베이스를 변경하여 주/미러 집합에 포함되지 않은 다른 데이터베이스에 대한 데이터 조작 작업이 실행되는 경우에 오류가 발생하면 이러한 다른 데이터베이스에 대한 변경 내용이 전파되지 않습니다. 미러링되지 않은 데이터베이스에서 데이터가 수정되는 경우에는 오류가 발생하지 않습니다. 개발자는 이러한 작업의 영향을 평가해야 합니다.  
  
## <a name="database-mirroring-resources"></a>데이터베이스 미러링 리소스  
 미러링 구성, 배포 및 관리에 대 한 개념 설명서 및 정보는 SQL Server 설명서에서 다음 리소스를 참조 하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[데이터베이스 미러링](/sql/database-engine/database-mirroring/database-mirroring-sql-server)|SQL Server에서 미러링을 설정 및 구성하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](../ado-net-overview.md)
