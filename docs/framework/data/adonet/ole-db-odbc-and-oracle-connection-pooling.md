---
title: OLE DB, ODBC 및 Oracle 연결 풀링
ms.date: 03/30/2017
ms.assetid: 2bd83b1e-3ea9-43c4-bade-d9cdb9bbbb04
ms.openlocfilehash: b83b53550964b3149f3bc711eaf119e749d1834b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794697"
---
# <a name="ole-db-odbc-and-oracle-connection-pooling"></a>OLE DB, ODBC 및 Oracle 연결 풀링
연결 풀링을 사용하면 응용 프로그램의 성능 및 확장성을 대폭 향상시킬 수 있습니다. 이 단원에서는 OLE DB, ODBC 및 Oracle용 .NET Framework 데이터 공급자에 대한 연결 풀링에 대해 설명합니다.  
  
## <a name="connection-pooling-for-oledb"></a>OleDb에 대한 연결 풀링  
 .NET Framework Data Provider for OLE DB에서는 OLE DB 세션 풀링을 사용하여 자동으로 연결을 풀링합니다. 연결 문자열 인수를 사용하면 풀링이 포함된 OLE DB 서비스를 활성화하거나 비활성화할 수 있습니다. 예를 들어, 다음 연결 문자열은 OLE DB 세션 풀링과 자동 트랜잭션 인리스트먼트를 비활성화합니다.  
  
```  
Provider=SQLOLEDB;OLE DB Services=-4;Data Source=localhost;Integrated Security=SSPI;  
```  
  
 연결의 사용을 끝내면 연결이 풀로 반환되도록 항상 연결을 닫거나 삭제하는 것이 좋습니다. 명시적으로 닫히지 않는 연결은 풀에 반환되지 않을 수 있습니다. 예를 들어, 범위를 벗어났지만 명시적으로 닫히지 않은 연결은 최대 풀 크기에 도달했으며 여전히 유효한 경우에만 연결 풀로 반환됩니다.  
  
 OLE DB 공급자 서비스 기본값을 재정의 하 여 풀링을 사용 하지 않도록 설정 하는 방법 뿐만 아니라 OLE DB 세션 또는 리소스 풀링에 대 한 자세한 내용은 [OLE DB 프로그래머 가이드](https://go.microsoft.com/fwlink/?linkid=45232)를 참조 하세요.  
  
## <a name="connection-pooling-for-odbc"></a>Odbc에 대한 연결 풀링  
 .NET Framework Data Provider for ODBC의 연결 풀링은 연결에 사용되는 ODBC 드라이버 관리자에서 관리하며 .NET Framework Data Provider for ODBC에 의해 영향을 받지 않습니다.  
  
 연결 풀링을 사용 하거나 사용 하지 않도록 설정 하려면 제어판의 관리 도구 폴더에서 **ODBC 데이터 원본 관리자** 를 엽니다. **연결 풀링** 탭에서는 설치 된 각 ODBC 드라이버에 대 한 연결 풀링 매개 변수를 지정할 수 있습니다. 특정 ODBC 드라이버에 대해 연결 풀링이 변경되면 해당 ODBC 드라이버를 사용하는 모든 애플리케이션에 영향을 줍니다.  
  
## <a name="connection-pooling-for-oracleclient"></a>OracleClient에 대한 연결 풀링  
 .NET Framework Data Provider for Oracle에서는 ADO.NET 클라이언트 애플리케이션에 대한 연결 풀링을 자동으로 제공합니다. 또한 여러 개의 연결 풀링 한정자를 지정하여 연결 풀링 동작을 제어할 수 있습니다(이 항목 뒷부분의 "연결 문자열 키워드를 사용하여 연결 풀링 제어" 참조).  
  
### <a name="pool-creation-and-assignment"></a>풀 만들기 및 할당  
 연결이 열리면 연결에서 풀과 연결 문자열을 연결하는 정확한 일치 알고리즘에 따라 연결 풀이 만들어집니다. 각 연결 풀은 고유한 연결 문자열과 연결됩니다. 새 연결이 열릴 때 연결 문자열이 기존 풀과 정확히 일치하지 않으면 새 풀이 만들어집니다.  
  
 만들어진 연결 풀은 활성 프로세스가 종료될 때까지 제거되지 않습니다. 비활성 또는 빈 풀을 유지 관리하는 데에는 매우 적은 시스템 리소스만 사용됩니다.  
  
### <a name="connection-addition"></a>연결 추가  
 각각의 고유 연결 문자열에 대해 연결 풀이 만들어집니다. 풀이 만들어지면 최소 풀 크기 요구 사항이 충족되도록 여러 개의 연결 개체가 만들어져 풀에 추가됩니다. 연결은 최대 풀 크기 이하로 필요한 만큼 풀에 추가됩니다.  
  
 <xref:System.Data.OracleClient.OracleConnection> 개체가 요청될 때 사용 가능한 연결이 있으면 풀에서 해당 개체를 가져올 수 있습니다. 연결을 사용하려면 연결이 현재 사용되고 있지 않고, 일치하는 트랜잭션 컨텍스트가 있거나 트랜잭션 컨텍스트와 연결되어 있지 않아야 하며, 서버에 대한 올바른 링크가 있어야 합니다.  
  
 최대 풀 크기에 도달했는데 사용 가능한 연결이 없으면 요청이 대기됩니다. 연결 풀러는 연결이 다시 풀로 회수될 때 연결을 다시 할당하여 이러한 요청을 충족합니다. 연결이 닫히거나 삭제되면 다시 풀로 회수됩니다.  
  
### <a name="connection-removal"></a>연결 제거  
 연결이 오랫동안 유휴 상태였거나 풀러에서 서버와 연결하기 어렵다는 것을 감지하면 연결 풀러는 풀에서 연결을 제거합니다. 이러한 연결은 서버와 통신하려는 시도가 있어야만 감지할 수 있습니다. 서버에 더 이상 연결되지 않는 연결이 있으면 그 연결은 잘못된 연결로 표시됩니다. 연결 풀러는 정기적으로 연결 풀을 검색하여 풀로 회수되었거나 잘못된 것으로 표시된 개체를 찾습니다. 그러면 이러한 연결은 영구적으로 제거됩니다.  
  
 네트워크에 존재하지 않는 서버에 대한 연결이 있는 경우 연결 풀러에서 이 연결을 검색하지 못하고 잘못된 연결로 표시하지 못해도 풀에서 선택할 수는 있습니다. 이 경우 예외가 발생합니다. 그러나 연결을 풀로 회수하려면 계속해서 연결을 닫아야 합니다.  
  
 클래스의 `Close` 메서드에 있는 `Dispose`, `Connection` 또는 다른 관리 개체에 `DataReader` 또는 `Finalize`를 호출해서는 안 됩니다. 종료자에서는 클래스에 직접 속한 관리되지 않는 리소스만 해제합니다. 클래스에 관리되지 않는 리소스가 없는 경우 클래스 정의에 `Finalize` 메서드를 포함하지 마세요. 자세한 내용은 [가비지 수집](../../../standard/garbage-collection/index.md)합니다.  
  
### <a name="transaction-support"></a>트랜잭션 지원  
 연결은 트랜잭션 컨텍스트에 따라 풀에서 선택되어 할당됩니다. 요청하는 스레드의 컨텍스트와 할당된 연결의 컨텍스트는 반드시 일치해야 합니다. 따라서 각 연결 풀은 실제로 연결 된 트랜잭션 컨텍스트가 없는 연결로 나뉜 다음, 각각 특정 트랜잭션 컨텍스트의 연결을 포함 하는 *N* 개의 하위 분류로 나뉩니다.  
  
 연결이 닫힐 때는 풀로 다시 회수되고 트랜잭션 컨텍스트에 따라 적절한 분할로 회수됩니다. 따라서 분산 트랜잭션이 여전히 보류 중이더라도 오류를 생성하지 않고 연결을 닫을 수 있습니다. 이렇게 하여 분산 트랜잭션을 나중에 커밋하거나 취소할 수 있습니다.  
  
### <a name="controlling-connection-pooling-with-connection-string-keywords"></a>연결 문자열 키워드를 사용하여 연결 풀링 제어  
 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> 개체의 <xref:System.Data.OracleClient.OracleConnection> 속성에서는 연결 문자열 키/값 쌍을 사용하여 연결 풀링 논리의 동작을 조정할 수 있습니다.  
  
 다음 표에서는 연결 풀링 동작을 조정하는 데 사용할 수 있는 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> 값을 설명합니다.  
  
|이름|기본|Description|  
|----------|-------------|-----------------|  
|`Connection Lifetime`|0|연결이 풀로 반환되면 연결을 만든 시간을 현재 시간과 비교하여 이 시간 간격(초)이 `Connection Lifetime`에서 지정한 값을 초과하는 경우 연결이 제거됩니다. 이는 클러스터링된 구성에서 실행 중인 서버와 방금 온라인 상태가 된 서버 사이에 로드 균형 조정을 강제로 조정하는 데 유용합니다.<br /><br /> 값 0은 풀링된 연결이 최대 시간 제한을 갖도록 합니다.|  
|`Enlist`|'true'|`true`이면 풀러는 트랜잭션 컨텍스트가 존재하는 경우 해당 연결을 만들기 스레드의 현재 트랜잭션 컨텍스트에 자동으로 인리스트먼트합니다.|  
|`Max Pool Size`|100|풀에 허용되는 최대 연결 수입니다.|  
|`Min Pool Size`|0|풀에서 유지되는 최소 연결 수입니다.|  
|`Pooling`|'true'|`true`이면 연결이 적절한 풀에서 선택되거나 필요한 경우 연결이 만들어져 적절한 풀에 추가됩니다.|  
  
## <a name="see-also"></a>참고자료

- [연결 풀링](connection-pooling.md)
- [성능 카운터](performance-counters.md)
- [ADO.NET 개요](ado-net-overview.md)
