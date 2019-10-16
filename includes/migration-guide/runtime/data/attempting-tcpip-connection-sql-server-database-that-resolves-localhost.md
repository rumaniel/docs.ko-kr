---
ms.openlocfilehash: e36dac19beb6251debef100656670a6623344eea
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68237830"
---
### <a name="attempting-a-tcpip-connection-to-a-sql-server-database-that-resolves-to-localhost-fails"></a>`localhost`로 확인된 SQL Server 데이터베이스에 대한 TCP/IP 연결 시도 실패

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6 및 4.6.1에서 <code>localhost</code>로 확인된 SQL Server 데이터베이스에 대한 TCP/IP 연결 시도가 오류와 함께 실패합니다. &quot;SQL Server에 연결을 설정하는 동안 네트워크 관련 또는 인스턴스 관련 오류가 발생했습니다. 서버를 찾을 수 없거나 액세스할 수 없습니다. 인스턴스 이름이 올바르고 SQL Server가 원격 연결을 허용하도록 구성되어 있는지 확인합니다. (공급자: SQL 네트워크 인터페이스, 오류: 26 - 지정된 서버/인스턴스 찾기 오류)&quot;|
|제안 해결 방법|이 문제가 해결되었으며 이전 동작은 .NET Framework 4.6.2에서 복원되었습니다. <code>localhost</code>로 확인된 SQL Server 데이터베이스에 연결하려면 .NET Framework 4.6.2로 업그레이드합니다.|
|범위|부|
|버전|4.6|
|형식|런타임|
