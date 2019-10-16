---
ms.openlocfilehash: 4c65cd62b2d84ef2b852d10a04e5f6ce0cc82d3a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804540"
---
### <a name="adonet-now-attempts-to-automatically-reconnect-broken-sql-connections"></a>ADO.NET가 이제 끊어진 SQL 연결을 자동으로 다시 연결 시도

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5.1부터는 .NET Framework가 끊어진 SQL 연결을 자동으로 다시 연결하려고 시도합니다. 이것은 일반적으로 응용 프로그램을 보다 안정적으로 만들지만, 연결이 끊어져서 다시 연결될 때 어떤 조치를 취할 수 있다는 것을 앱이 알아야 할 경우가 있습니다.|
|제안 해결 방법|이 기능이 호환성 문제로 인해 사용하지 않을 경우, 연결 문자열(또는 <xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=name>)의 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.ConnectRetryCount?displayProperty=name> 속성을 0으로 설정하여 비활성화할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.5.1|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Data.IDbConnection.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnection.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Configuration.ConnectionStringSettings.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbConnectionStringBuilder.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnectionStringBuilder.%23ctor?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnectionStringBuilder.%23ctor(System.String)?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbConnectionStringBuilder.%23ctor?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbConnectionStringBuilder.%23ctor(System.Boolean)?displayProperty=nameWithType></li></ul>|
