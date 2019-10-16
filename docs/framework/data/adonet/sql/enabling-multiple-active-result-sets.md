---
title: MARS(Multiple Active Result Sets) 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.openlocfilehash: 1f8cb573d051970414f3962057f6329683eea5bd
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782400"
---
# <a name="enabling-multiple-active-result-sets"></a>MARS(Multiple Active Result Sets) 사용
MARS(Multiple Active Result Sets)는 단일 연결에서 여러 배치를 실행할 수 있도록 하는 SQL Server의 기능입니다. SQL Server에 MARS가 활성화되어 있으면 명령 개체를 사용할 때마다 연결에 세션이 추가됩니다.  
  
> [!NOTE]
> 단일 MARS 세션은 사용할 MARS에 대해 하나의 논리적 연결을 연 다음 각 활성 명령에 대해 논리적 연결을 하나씩 엽니다.  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>연결 문자열에서 MARS 활성화 및 비활성화  
  
> [!NOTE]
> 다음 연결 문자열은 SQL Server에 포함 된 샘플 **AdventureWorks** 데이터베이스를 사용 합니다. 제공된 연결 문자열은 데이터베이스가 MSSQL1이라는 서버에 설치되었다고 가정합니다. 사용자 환경의 필요에 따라 연결 문자열을 수정합니다.  
  
 MARS 기능은 기본적으로 비활성화되어 있으며 연결 문자열에 "MultipleActiveResultSets=True" 키워드 쌍을 추가하여 활성화할 수 있습니다. MARS를 활성화하는 유일한 유효 값은 "True"입니다. 다음 예제에서는 SQL Server의 인스턴스에 연결하는 방법과 MARS를 활성화하도록 지정하는 방법을 설명합니다.  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=True"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
 연결 문자열에 "MultipleActiveResultSets=False" 키워드 쌍을 추가하면 MARS를 비활성화할 수 있습니다. MARS를 비활성화하는 유일한 유효 값은 "False"입니다. 다음 연결 문자열에서는 MARS를 비활성화하는 방법을 보여 줍니다.  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=False"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>MARS를 사용할 때 특별히 고려할 사항  
 일반적으로 MARS 사용 연결을 사용하기 위해 기존 애플리케이션을 수정할 필요는 없습니다. 그러나 애플리케이션에서 MARS 기능을 사용하려면 다음의 특별히 고려할 사항을 알아 두어야 합니다.  
  
### <a name="statement-interleaving"></a>문 인터리빙  
 MARS 작업은 서버에서 동기적으로 실행됩니다. 또한 SELECT 및 BULK INSERT 문의 문 인터리빙이 허용됩니다. 그러나 DML(데이터 조작 언어) 및 DDL(데이터 정의 언어) 문은 원자적으로 실행됩니다. 원자 배치가 실행되는 동안 실행하려는 문은 모두 차단됩니다. 서버에서의 병렬 실행은 MARS 기능이 아닙니다.  
  
 MARS 연결에서 두 개의 배치, 즉 SELECT 문이 포함된 배치와 DML 문이 포함된 배치를 전송하면 DML은 SELECT 문을 실행하는 동안 실행을 시작할 수 있습니다. 그러나 SELECT 문을 계속 실행하려면 반드시 DML 문의 실행을 완료해야 합니다. 두 문이 모두 동일한 트랜잭션에서 실행되는 경우 SELECT 문이 실행을 시작한 후 DML 문에서 변경한 모든 내용은 읽기 작업에 표시되지 않습니다.  
  
 SELECT 문 내부의 WAITFOR 문은 첫 번째 행이 생성될 때까지 기다리는 동안 트랜잭션을 만들지 않습니다. 즉, WAITFOR 문이 대기 중인 경우에는 동일한 연결에서 다른 배치를 실행할 수 없습니다.  
  
### <a name="mars-session-cache"></a>MARS 세션 캐시  
 MARS가 활성화된 연결이 열리면 논리 세션이 만들어져 오버헤드가 추가됩니다. 오버 헤드를 최소화 하 고 성능을 향상 시키기 위해 **SqlClient** 는 연결 내에서 MARS 세션을 캐시 합니다. 캐시에는 최대 10개의 MARS 세션이 포함되며 이 값은 사용자가 조정할 수 없습니다. 세션 제한에 도달하면 새 세션이 만들어지며, 이때 오류는 생성되지 않습니다. 캐시와 캐시에 포함된 세션은 각 연결을 기준으로 하므로 여러 연결에서 공유되지 않습니다. 세션이 해제되면 풀의 상한에 도달할 때까지 풀로 반환됩니다. 캐시 풀이 꽉 차면 세션이 닫힙니다. MARS 세션은 만료되지 않으며 연결 개체가 삭제될 때 정리되기만 합니다. MARS 세션 캐시는 미리 로드되지 않고 애플리케이션에 추가 세션이 필요할 때 로드됩니다.  
  
### <a name="thread-safety"></a>스레드 보안  
 MARS 작업은 스레드로부터 안전하지 않습니다.  
  
### <a name="connection-pooling"></a>연결 풀링  
 MARS 사용 연결도 다른 모든 연결과 마찬가지로 풀링됩니다. 애플리케이션에서 두 개의 연결, 즉 MARS가 활성화되어 있는 연결과 MARS가 비활성화되어 있는 연결을 여는 경우 이 두 연결은 개별 풀에 위치합니다. 자세한 내용은 [SQL Server 연결 풀링(ADO.NET)](../sql-server-connection-pooling.md)을 참조하세요.  
  
### <a name="sql-server-batch-execution-environment"></a>SQL Server 배치 실행 환경  
 연결이 열리면 기본 환경이 정의됩니다. 그런 다음 이 환경은 논리 MARS 세션에 복사됩니다.  
  
 배치 실행 환경에는 다음 구성 요소가 들어 있습니다.  
  
- 설정 옵션(예: ANSI_NULLS, DATE_FORMAT, LANGUAGE, TEXTSIZE)  
  
- 보안 컨텍스트(사용자/애플리케이션 역할)  
  
- 데이터베이스 컨텍스트(현재 데이터베이스)  
  
- 실행 상태 변수 (@ERROR예: @, @@ROWCOUNT, @@FETCH_STATUS @@IDENTITY)  
  
- 최상위 임시 테이블  
  
 MARS가 활성화되면 기본 실행 환경이 연결에 지정됩니다. 지정된 연결에서 새 배치가 실행을 시작할 때마다 기본 환경의 복사본을 받습니다. 지정된 배치에서 코드가 실행될 때마다 해당 환경의 모든 변경 내용은 특정 배치로 범위가 지정됩니다. 실행이 종료되면 실행 설정은 기본 환경에 복사됩니다. 동일한 트랜잭션에서 여러 개의 명령을 실행하는 단일 배치를 순차적으로 실행하는 경우 의미 체계는 이전 클라이언트 또는 서버와 관련된 연결에서 노출한 의미 체계와 동일합니다.  
  
### <a name="parallel-execution"></a>병렬 실행  
 MARS를 사용하더라도 한 애플리케이션의 여러 연결에 대한 모든 요구 사항은 유지됩니다. 애플리케이션에서 서버에 대한 명령의 실질적인 병렬 실행이 필요한 경우에는 여러 개의 연결을 사용해야 합니다.  
  
 예를 들어, 다음과 같은 시나리오를 가정해 봅시다. 두 개의 명령 개체, 즉 결과 집합을 처리하기 위한 명령 개체와 데이터를 업데이트하기 위한 명령 개체를 만듭니다. 이들 개체는 MARS를 통해 일반 연결을 공유합니다. 이 시나리오 `Transaction`에서는입니다.`Commit` 는 첫 번째 명령 개체에서 모든 결과를 읽을 때까지 업데이트에 실패 하 여 다음 예외를 생성 합니다.  
  
 메시지: 다른 세션에서 사용 중인 트랜잭션 컨텍스트  
  
 소스: .NET SqlClient Data Provider  
  
 예상: (null)  
  
 받았을 System.Data.SqlClient.SqlException  
  
 다음은 이 시나리오를 처리하기 위한 세 가지 옵션입니다.  
  
1. 판독기를 만든 후 트랜잭션을 시작하여 트랜잭션의 일부가 되지 않도록 합니다. 그러면 모든 업데이트 작업이 고유한 트랜잭션이 됩니다.  
  
2. 판독기가 닫히면 모든 작업을 커밋합니다. 그러면 배치가 상당 부분 업데이트될 수 있습니다.  
  
3. MARS를 사용하는 대신 명령 개체마다 개별 연결을 사용하세요.  
  
### <a name="detecting-mars-support"></a>MARS 지원 검색  
 애플리케이션에서는 `SqlConnection.ServerVersion` 값을 읽어 MARS 지원 여부를 확인할 수 있습니다. SQL Server 2005의 주 번호는 9이고 SQL Server 2008의 주 번호는 10입니다.  
  
## <a name="see-also"></a>참고자료

- [MARS(Multiple Active Result Sets)](multiple-active-result-sets-mars.md)
- [ADO.NET 개요](../ado-net-overview.md)
