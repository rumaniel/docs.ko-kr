---
title: ADO.NET의 새로운 기능
ms.date: 03/30/2017
ms.assetid: 3bb65d38-cce2-46f5-b979-e5c505e95e10
ms.openlocfilehash: 0a02ca3885524c5fcf8def603acdce33a972d283
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791266"
---
# <a name="whats-new-in-adonet"></a>ADO.NET의 새로운 기능

.NET Framework 4.5에서 ADO.NET의 새로운 기능은 다음과 같습니다.

## <a name="sqlclient-data-provider"></a>SqlClient Data Provider

다음은 .NET Framework 4.5의 SQL Server에 대 한 .NET Framework Data Provider의 새로운 기능입니다.

- ConnectRetryCount 및 ConnectRetryInterval 연결 문자열 키워드(<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>)를 사용하면 유휴 연결 복원 기능을 제어할 수 있습니다.

- SQL Server에서 응용 프로그램으로의 스트리밍 지원은 서버의 데이터가 구조화 되지 않은 시나리오를 지원 합니다.  자세한 내용은 [SqlClient 스트리밍 지원](sqlclient-streaming-support.md) 을 참조 하세요.

- 비동기 프로그래밍에 대한 지원이 추가되었습니다.  자세한 내용은 [비동기 프로그래밍](asynchronous-programming.md) 을 참조 하세요.

- 이제 연결 실패가 확장 이벤트 로그에 기록됩니다. 자세한 내용은 [ADO.NET의 데이터 추적](data-tracing.md)을 참조하세요.

- SqlClient는 이제 SQL Server의 고가용성, 재해 복구 기능, AlwaysOn을 지원 합니다. 자세한 내용은 [고가용성, 재해 복구에 대 한 SqlClient 지원](./sql/sqlclient-support-for-high-availability-disaster-recovery.md)을 참조 하세요.

- SQL Server 인증을 사용 하는 <xref:System.Security.SecureString> 경우 암호를으로 전달할 수 있습니다. 자세한 내용은 <xref:System.Data.SqlClient.SqlCredential>를 참조하세요.

- 가 false이 고 `Encrypt` 가 true 이면 SQL Server SSL 인증서의 서버 이름 (또는 ip 주소)이 연결 문자열에 지정 된 서버 이름 (또는 ip 주소)과 정확 하 게 일치 해야 합니다. `TrustServerCertificate` 그렇지 않으면 연결을 시도할 경우 실패합니다. 자세한 내용은 `Encrypt`의 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 연결 옵션에 대한 설명을 참조하세요.

  이러한 변경으로 인해 기존 애플리케이션이 더 이상 연결되지 않는 경우 다음 중 하나를 사용하여 애플리케이션을 수정하면 됩니다.

  - CN(일반 이름) 또는 SAN(주체 대체 이름) 필드에 약식 이름을 지정하는 인증서를 발급합니다. 이 방법은 데이터베이스 미러링에 적용됩니다.

  - 정규화된 도메인 이름에 약식 이름을 매핑하는 별칭을 추가합니다.

  - 연결 문자열에서 정규화된 도메인 이름을 사용합니다.

- SqlClient는 확장된 보호를 지원합니다. 확장 된 보호에 대 한 자세한 내용은 [확장 된 보호를 사용 하 여 데이터베이스 엔진에 연결](https://go.microsoft.com/fwlink/?LinkId=219978)을 참조 하세요.

- SqlClient는 LocalDB 데이터베이스에 대한 연결을 지원합니다. 자세한 내용은 [LocalDB에 대 한 SqlClient 지원](./sql/sqlclient-support-for-localdb.md)을 참조 하세요.

- `Type System Version=SQL Server 2012;`는 `Type System Version` 연결 속성에 전달되는 새로운 값입니다. `Type System Version=Latest;` 값은 더 이상 사용되지 않으며 `Type System Version=SQL Server 2008;`과 동일해졌습니다. 자세한 내용은 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>을 참조하세요.

- SqlClient에서는 SQL Server 2008에 추가된 기능인 스파스 열에 대한 추가 지원을 제공합니다. 애플리케이션이 이미 스파스 열을 사용하는 테이블의 데이터에 액세스하는 경우 성능이 향상됩니다. <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>의 IsColumnSet 열은 해당 열이 열 집합의 멤버인 스파스 열인지 여부를 나타냅니다. <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A>열이 스파스 열인지 여부를 나타냅니다. 자세한 내용은 [SQL Server 스키마 컬렉션](sql-server-schema-collections.md) 을 참조 하십시오. 스파스 열에 대 한 자세한 내용은 [스파스 열 사용](https://go.microsoft.com/fwlink/?LinkId=224244)을 참조 하세요.

- 공간 데이터 형식이 포함되어 있는 Microsoft.SqlServer.Types.dll 어셈블리가 버전 10.0에서 버전 11.0으로 업그레이드되었습니다. 이 어셈블리를 참조하는 애플리케이션은 제대로 실행되지 않을 수 있습니다. 자세한 내용은 [데이터베이스 엔진 기능에 대 한 주요 변경 내용](https://go.microsoft.com/fwlink/?LinkId=224367)을 참조 하세요.

## <a name="adonet-entity-framework"></a>ADO.NET Entity Framework

.NET Framework 4.5는 Entity Framework 5.0로 작업할 때 새로운 시나리오를 사용할 수 있도록 하는 Api를 추가 합니다. Entity Framework 5.0에 추가 된 향상 된 기능 및 기능에 대 한 자세한 내용은 다음 항목을 참조 하십시오. [새로운](https://go.microsoft.com/fwlink/?LinkID=251106) 기능과 [Entity Framework 릴리스 및 버전 관리](https://go.microsoft.com/fwlink/?LinkId=234899)를 제공 합니다.

## <a name="see-also"></a>참고자료

- [ADO.NET](index.md)
- [ADO.NET 개요](ado-net-overview.md)
- [SQL Server 및 ADO.NET](./sql/index.md)
- [WCF Data Services 5.0의 새로운 기능](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/ee373845(v=vs.103))
