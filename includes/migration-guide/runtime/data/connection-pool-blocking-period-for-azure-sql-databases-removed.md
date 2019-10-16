---
ms.openlocfilehash: 9605352c66f85b6942ba24942cb07c88bdd81f2a
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67857516"
---
### <a name="connection-pool-blocking-period-for-azure-sql-databases-is-removed"></a>Azure SQL 데이터베이스에 대한 연결 풀 차단 기간이 제거되었습니다.

|   |   |
|---|---|
|설명|.NET Framework 4.6.2부터는 알려진 Azure SQL 데이터베이스(*.database.windows.net, *.database.chinacloudapi.cn, *.database.usgovcloudapi.net, *.database.cloudapi.de)에 대한 연결 열기 요청의 경우 연결 풀 차단이 제거되고 연결 열기 오류가 캐시되지 않습니다. 연결 열기 요청 다시 시도는 일시적인 연결 오류 발생 직후에 수행됩니다. 이 변경은 Azure SQL 데이터베이스에 대한 연결 열기 시도를 즉시 다시 시도하도록 하여 클라우드 지원 응용 프로그램의 성능을 향상시킵니다. 다른 모든 연결 시도의 경우 연결 풀 차단 기간이 계속 적용됩니다.<p/>.NET Framework 4.6.1 및 이전 버전에서 데이터베이스에 연결할 때 응용 프로그램에 일시적인 연결 오류가 발생할 경우, 연결 풀이 오류를 캐시하고 5초에서 1분 동안 다시 throw하기 때문에 연결 시도는 신속하게 다시 시도될 수 없습니다. 자세한 내용은 [SQL Server 연결 풀링(ADO.NET)](~/docs/framework/data/adonet/sql-server-connection-pooling.md)을 참조하세요. 이 동작은 일반적으로 몇 초 내에 복구되는 일시적인 오류가 자주 발생하는 Azure SQL 데이터베이스에 대한 연결 문제가 있습니다. 연결 풀 차단 기능은 데이터베이스를 사용할 수 있고 앱을 몇 초 안에 렌더링해야 하더라도 광범위한 기간 동안 응용 프로그램 데이터베이스에 연결할 수 없다는 것을 의미합니다.|
|제안 해결 방법|이 동작이 필요 없는 경우 .NET Framework 4.6.2에서 새로 추가된 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=name> 속성을 설정하여 연결 풀 차단 기간을 구성할 수 있습니다. 속성의 값은 다음의 세 값 중 하나를 사용할 수 있는 <xref:System.Data.SqlClient.PoolBlockingPeriod?displayProperty=name> 열거형의 멤버입니다.<ul><li><xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock></li><li><xref:System.Data.SqlClient.PoolBlockingPeriod.Auto></li><li><xref:System.Data.SqlClient.PoolBlockingPeriod.NeverBlock></li></ul><xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=name> 속성을 <xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock>으로 설정하여 이전 동작을 복원할 수 있습니다.|
|범위|부|
|버전|4.6.2|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Data.Common.DbConnection.OpenAsync?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnection.Open?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnection.OpenAsync(System.Threading.CancellationToken)?displayProperty=nameWithType></li></ul>|

