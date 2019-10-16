---
title: ADO.NET의 데이터 추적
ms.date: 03/30/2017
ms.assetid: a6a752a5-d2a9-4335-a382-b58690ccb79f
ms.openlocfilehash: 1b2ee679ce4b0d39b993b9081f428fe585ef7d92
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784895"
---
# <a name="data-tracing-in-adonet"></a>ADO.NET의 데이터 추적

ADO.NET는 SQL Server, Oracle, OLE DB 및 ODBC 용 .net 데이터 공급자 뿐만 아니라 ADO.NET <xref:System.Data.DataSet>및 SQL Server 네트워크 프로토콜에 대해 지원 되는 기본 제공 데이터 추적 기능을 제공 합니다.

데이터 액세스 API 호출을 추적하면 다음과 같은 문제를 진단할 수 있습니다.

- 클라이언트 프로그램과 데이터베이스 간의 스키마 불일치

- 데이터베이스 비가용성 또는 네트워크 라이브러리 문제

- 하드 코딩되거나 애플리케이션에서 생성된 잘못된 SQL

- 잘못된 프로그래밍 논리

- 여러 ADO.NET 구성 요소 간의 상호 작용 및 ADO.NET과 사용자 구성 요소 간의 상호 작용으로 인한 문제

다양한 추적 기술을 지원하기 위해 추적을 확장할 수 있으므로 개발자는 애플리케이션 스택의 모든 수준에서 문제를 추적할 수 있습니다. 추적이 ADO.NET에만 있는 기능은 아니지만 Microsoft 공급자에서는 일반화된 추적 및 계측 API를 사용합니다.

ADO.NET에서 관리 되는 추적을 설정 하 고 구성 하는 방법에 대 한 자세한 내용은 [데이터 액세스 추적](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10))을 참조 하세요.

## <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>확장 이벤트 로그에서 진단 정보에 액세스

SQL Server에 대 한 .NET Framework Data Provider에서 데이터 액세스 추적 ([데이터 액세스 추적](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10)))이 업데이트 되어 서버 연결에서 클라이언트 이벤트와 진단 정보 (예: 연결 오류)의 상관 관계를 보다 쉽게 변경할 수 있습니다. 확장 이벤트 로그의 링 버퍼 및 응용 프로그램 성능 정보입니다. 확장 이벤트 로그를 읽는 방법에 대 한 자세한 내용은 [이벤트 세션 데이터 보기](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/hh710068(v=sql.110))를 참조 하세요.

연결 동작의 경우 ADO.NET은 클라이언트 연결 ID를 전송합니다. 연결에 실패 하면 연결 링 버퍼 (연결[링 버퍼를 사용 하 여 SQL Server 2008의 연결 문제 해결](https://go.microsoft.com/fwlink/?LinkId=207752))에 액세스 하 고 필드 `ClientConnectionID` 를 찾아서 연결 실패에 대 한 진단 정보를 얻을 수 있습니다. 클라이언트 연결 ID는 오류가 발생한 경우에만 링 버퍼에 로그인됩니다. 사전 로그인 패킷을 전송하기 전에 연결에 실패할 경우 클라이언트 연결 ID가 생성되지 않습니다. 클라이언트 연결 ID는 16바이트 GUID입니다. `client_connection_id` 동작이 확장 이벤트 세션에서 이벤트에 추가된 경우 확장 이벤트 대상 출력에서 클라이언트 연결 ID를 찾을 수도 있습니다. 추가 클라이언트 드라이버 진단이 필요한 경우 데이터 액세스 추적을 활성화하고 연결 명령을 다시 실행하여 데이터 액세스 추적에서 `ClientConnectionID` 필드를 관찰할 수 있습니다.

`SqlConnection.ClientConnectionID` 속성을 사용하여 클라이언트 연결 ID를 프로그래밍 방식으로 가져올 수 있습니다.

`ClientConnectionID`는 연결을 성공적으로 설정하는 <xref:System.Data.SqlClient.SqlConnection> 개체에 사용할 수 있습니다. 연결 시도에 실패한 경우에는 `ClientConnectionID`을 통해 `SqlException.ToString`를 확인할 수 있습니다.

또한 ADO.NET은 스레드별 동작 ID를 전송합니다. TRACK_CAUSALITY 옵션을 사용 하 여 세션을 시작 하는 경우 활동 ID가 확장 이벤트 세션에 캡처됩니다. 활성 연결과 관련한 성능 문제의 경우 클라이언트의 데이터 액세스 추적에서 동작 ID(`ActivityID` 필드)를 가져온 다음 확장 이벤트 출력에서 동작 ID를 찾아볼 수 있습니다. 확장 이벤트의 동작 ID는16바이트 GUID(클라이언트 연결 ID의 GUID와는 다름)에 4바이트 시퀀스 번호를 추가한 것입니다. 시퀀스 번호는 스레드 내의 요청 순서를 나타내며 스레드에서 일괄 처리 및 RPC 문의 상대적인 순서를 나타냅니다. `ActivityID`는 현재 데이터 액세스 추적이 활성화된 상태이고 데이터 액세스 추적 구성 단어의 18번째 비트가 ON 상태인 경우 SQL 일괄 처리 문과 RPC 요청에 대해 선택적으로 전송됩니다.

다음은 Transact-sql을 사용 하 여 링 버퍼에 저장 되 고 RPC 및 일괄 처리 작업 시 클라이언트에서 전송 된 활동 ID를 기록 하는 확장 이벤트 세션을 시작 하는 샘플입니다.

```sql
create event session MySession on server
add event connectivity_ring_buffer_recorded,
add event sql_statement_starting (action (client_connection_id)),
add event sql_statement_completed (action (client_connection_id)),
add event rpc_starting (action (client_connection_id)),
add event rpc_completed (action (client_connection_id))
add target ring_buffer with (track_causality=on)
```

## <a name="see-also"></a>참고자료

- [.NET Framework의 네트워크 추적](../../network-programming/network-tracing.md)
- [응용 프로그램 추적 및 조율](../../debug-trace-profile/tracing-and-instrumenting-applications.md)
- [ADO.NET 개요](ado-net-overview.md)
