---
title: SQL Server의 스냅샷 격리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
ms.openlocfilehash: 6d85cc041850300d1d079b227dcb8ed9201a0502
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699070"
---
# <a name="snapshot-isolation-in-sql-server"></a>SQL Server의 스냅샷 격리
스냅샷 격리를 통해 OLTP 애플리케이션의 동시성이 향상됩니다.  
  
## <a name="understanding-snapshot-isolation-and-row-versioning"></a>스냅샷 격리 및 행 버전 관리 이해  
 스냅숏 격리가 설정 되 면 각 트랜잭션에 대해 업데이트 된 행 버전을 유지 관리 해야 합니다.  SQL Server 2019 이전 버전에서는 이러한 버전이 **tempdb**에 저장 되었습니다. SQL Server 2019에는 고유한 행 버전 집합이 필요한 새로운 기능인 ADR (가속화 된 데이터베이스 복구)가 도입 되었습니다.  따라서 SQL Server 2019에서 ADR를 사용 하지 않는 경우 행 버전은 **tempdb** 에 항상 유지 됩니다.  ADR가 사용 하도록 설정 된 경우 snapshot 격리 및 ADR와 관련 된 모든 행 버전은 사용자가 지정 하는 파일 그룹의 사용자 데이터베이스에 있는 ADR의 영구 버전 저장소 (PVS)에 보관 됩니다. 고유한 트랜잭션 시퀀스 번호가 각 트랜잭션을 식별하며 행 버전에 대해 이러한 고유 번호가 기록됩니다. 트랜잭션은 트랜잭션 시퀀스 번호 이전의 시퀀스 번호를 가진 최근 행 버전에서 작동합니다. 트랜잭션이 시작된 이후에 만들어진 새로운 행 버전은 트랜잭션에서 무시됩니다.  
  
 "스냅샷"이라는 용어는 트랜잭션의 모든 쿼리가 트랜잭션이 시작되는 시점에서 데이터베이스 상태에 따라 데이터베이스의 동일한 버전 또는 스냅샷을 표시하는 것을 의미합니다. 스냅샷 트랜잭션의 기본 데이터 행이나 데이터 페이지에서는 잠금이 인식되지 않습니다. 따라서 이전에 완료되지 않은 트랜잭션에 의해 차단되지 않고 다른 트랜잭션을 실행할 수 있습니다. 일반적으로 트랜잭션은 SQL Server의 기본 READ COMMITTED 격리 수준 아래에 있으므로 데이터를 수정하는 트랜잭션이 데이터를 읽는 트랜잭션을 차단하지 않으며 데이터를 읽는 트랜잭션이 데이터를 쓰는 트랜잭션을 차단하지 않습니다. 또한 이러한 비블로킹 동작이 복잡한 트랜잭션의 교착 상태 가능성을 크게 줄여 줍니다.  
  
 스냅샷 격리에서는 낙관적 동시성 모델을 사용합니다. 스냅샷 트랜잭션에서 트랜잭션이 시작된 이후에 변경된 데이터에 대한 수정 내용을 커밋하려는 경우 트랜잭션이 롤백되고 오류가 발생합니다. 이러한 문제를 방지하려면 수정할 데이터에 액세스하는 SELECT 문에 대해 UPDLOCK 힌트를 사용합니다. 자세한 내용은 SQL Server 온라인 설명서의 "Locking Hints"를 참조하세요.  
  
 트랜잭션에서 사용되기 전에 ALLOW_SNAPSHOT_ISOLATION ON 데이터베이스 옵션을 설정하여 스냅샷 격리를 활성화해야 합니다. 이렇게 하면 임시 데이터베이스 (**tempdb**)에 행 버전을 저장 하는 메커니즘이 활성화 됩니다. Transact-SQL ALTER DATABASE 문과 함께 사용하는 각 데이터베이스에서 스냅샷 격리를 활성화해야 합니다. 이 경우 스냅샷 격리는 구성을 필요로 하지 않는 READ COMMITTED, REPEATABLE READ, SERIALIZABLE 및 READ UNCOMMITTED와 같은 일반적인 격리 수준과 다릅니다. 다음 문은 스냅샷 격리를 활성화하고 기본 READ COMMITTED 동작을 SNAPSHOT으로 대체합니다.  
  
```sql  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
 READ_COMMITTED_SNAPSHOT ON 옵션을 설정하면 기본 READ COMMITTED 격리 수준에서 버전 관리되는 행에 액세스할 수 있습니다. READ_COMMITTED_SNAPSHOT 옵션이 OFF로 설정된 경우 버전 관리되는 행에 액세스하려면 세션마다 스냅샷 격리 수준을 명시적으로 설정해야 합니다.  
  
## <a name="managing-concurrency-with-isolation-levels"></a>격리 수준을 사용하여 동시성 관리  
 Transact-SQL 문이 실행되는 격리 수준은 해당 문의 잠금 및 행 버전 관리 동작을 결정합니다. 격리 수준은 연결 전체 범위에 적용되므로 SET TRANSACTION ISOLATION LEVEL 문을 사용하여 연결에 대해 격리 수준이 설정되고 나면 연결이 닫히거나 다른 격리 수준이 설정될 때까지 적용된 상태가 유지됩니다. 연결이 닫히고 풀로 반환되면 마지막 SET TRANSACTION ISOLATION LEVEL 문의 격리 수준이 유지됩니다. 풀링된 연결을 다시 사용하는 후속 연결은 연결이 풀링된 시점에 유효 상태였던 격리 수준을 사용합니다.  
  
 연결 내에서 실행된 개별 쿼리에는 단일 문이나 트랜잭션의 격리를 수정하는 잠금 힌트가 포함될 수 있지만 연결의 격리 수준에는 영향을 미치지 않습니다. 저장 프로시저 또는 함수에 설정된 격리 수준이나 잠금 힌트는 이러한 저장 프로시저나 함수를 호출하는 연결의 격리 수준을 변경하지 않으며 저장 프로시저 또는 함수 호출 기간에만 적용됩니다.  
  
 이전 버전의 SQL Server에서는 SQL-92 표준에 정의된 네 가지 격리 수준이 지원되었습니다.  
  
- READ UNCOMMITTED는 다른 트랜잭션에 의한 잠금을 무시하기 때문에 가장 제한이 적은 격리 수준입니다. READ UNCOMMITTED에서 실행되는 트랜잭션은 다른 트랜잭션에서 커밋하지 않은 수정된 데이터 값을 읽을 수 있습니다. 이를 "더티" 읽기라고 합니다.  
  
- READ COMMITTED는 SQL Server의 기본 격리 수준입니다. 이 격리 수준은 문에서 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 데이터 값을 읽을 수 없도록 지정하여 더티 읽기를 방지합니다. 다른 트랜잭션에서 현재 트랜잭션 내에 있는 개별 문이 실행되는 사이에 데이터를 계속해서 수정하거나 삽입 또는 삭제할 수 있기 때문에 결과적으로 반복되지 않은 읽기 또는 "팬텀" 데이터가 발생합니다.  
  
- REPEATABLE READ는 READ COMMITTED보다 좀 더 제한적인 격리 수준입니다. 이 수준은 READ COMMITTED를 포함할 뿐만 아니라 현재 트랜잭션이 커밋될 때까지 현재 트랜잭션에서 읽은 데이터를 다른 트랜잭션에서 수정하거나 삭제할 수 없도록 지정합니다. 읽은 데이터에 대한 공유 잠금이 각 문이 끝날 때 해제되지 않고 트랜잭션 기간 동안 유지되기 때문에 동시성이 READ COMMITTED의 경우보다 낮습니다.  
  
- SERIALIZABLE은 전체 키를 잠그고 트랜잭션이 완료될 때까지 잠금을 유지하기 때문에 가장 제한적인 격리 수준입니다. 이 격리 수준은 REPEATABLE READ를 포함하며 트랜잭션이 완료될 때까지 다른 트랜잭션이 해당 트랜잭션에서 읽은 범위 내에 새 행을 삽입할 수 없도록 하는 제한을 추가합니다.  
  
 자세한 내용은 [트랜잭션 잠금 및 행 버전 관리 가이드](/sql/relational-databases/sql-server-transaction-locking-and-row-versioning-guide)를 참조 하세요.  
  
### <a name="snapshot-isolation-level-extensions"></a>스냅샷 격리 수준 확장명  
 SQL Server에서는 SNAPSHOT 격리 수준을 도입하고 READ COMMITTED를 추가로 구현함으로써 SQL-92 격리 수준이 확장되었습니다. READ_COMMITTED_SNAPSHOT 격리 수준은 모든 트랜잭션에 대해 READ COMMITTED를 투명하게 대체할 수 있습니다.  
  
- SNAPSHOT 격리는 트랜잭션 내에서 읽은 데이터에 다른 동시 트랜잭션에서 발생한 변경 내용이 반영되지 않도록 지정합니다. 트랜잭션은 트랜잭션이 시작될 때 존재하는 데이터 행 버전을 사용합니다. 데이터를 읽을 때 데이터가 잠기지 않으므로 SNAPSHOT 트랜잭션이 다른 트랜잭션의 데이터 쓰기 동작을 차단하지 않습니다. 데이터를 쓰는 트랜잭션은 스냅샷 트랜잭션의 데이터 읽기 동작을 차단하지 않습니다. 스냅샷 격리를 사용하려면 ALLOW_SNAPSHOT_ISOLATION 데이터베이스 옵션을 설정하여 스냅샷 격리를 활성화해야 합니다.  
  
- READ_COMMITTED_SNAPSHOT 데이터베이스 옵션은 데이터베이스에서 스냅샷 격리를 활성화한 경우 기본 READ COMMITTED 격리 수준의 동작을 결정합니다. READ_COMMITTED_SNAPSHOT ON을 명시적으로 지정하지 않은 경우 READ COMMITTED가 모든 암시적 트랜잭션에 적용됩니다. 따라서 READ_COMMITTED_SNAPSHOT OFF(기본값)를 설정할 때와 똑같이 작동합니다. READ_COMMITTED_SNAPSHOT OFF가 적용되는 경우 데이터베이스 엔진에서 공유 잠금을 사용하여 기본 격리 수준을 적용합니다. READ_COMMITTED_SNAPSHOT 데이터베이스 옵션을 ON으로 설정하면 데이터베이스 엔진에서 잠금을 사용하는 대신에 행 버전 관리 및 스냅샷 격리를 기본값으로 사용하여 데이터를 보호합니다.  
  
## <a name="how-snapshot-isolation-and-row-versioning-work"></a>스냅샷 격리 및 행 버전 관리의 작동 방법  
 스냅숏 격리 수준을 사용 하는 경우 행이 업데이트 될 때마다 SQL Server 데이터베이스 엔진는 **tempdb**에 원래 행의 복사본을 저장 하 고 행에 트랜잭션 시퀀스 번호를 추가 합니다. 발생하는 이벤트 시퀀스는 다음과 같습니다.  
  
- 새 트랜잭션이 시작되고 트랜잭션 시퀀스 번호가 할당됩니다.  
  
- 데이터베이스 엔진은 트랜잭션 내에서 행을 읽고 시퀀스 번호가 트랜잭션 시퀀스 번호와 가장 가까운 **tempdb** 에서 행 버전을 검색 합니다.  
  
- 데이터베이스 엔진에서 스냅샷 트랜잭션이 시작되었을 때 커밋되지 않은 활성 트랜잭션의 트랜잭션 시퀀스 번호 목록에 트랜잭션 시퀀스 번호가 들어 있지 않은지 확인합니다.  
  
- 트랜잭션은 트랜잭션 시작 시의 현재 상태로 **tempdb** 에서 행의 버전을 읽습니다. 트랜잭션이 시작된 후 삽입된 새 행은 해당 시퀀스 번호 값이 트랜잭션 시퀀스 번호 값보다 높으므로 표시되지 않습니다.  
  
- **Tempdb** 에는 시퀀스 번호 값이 낮은 행 버전이 있으므로 현재 트랜잭션은 트랜잭션이 시작 된 후 삭제 된 행을 볼 수 있습니다.  
  
 스냅샷 격리의 결과로 트랜잭션에서 기본 테이블에 잠금을 고려하거나 배치하지 않고 트랜잭션을 시작할 때 존재했던 그대로 모든 데이터를 표시합니다. 따라서 경합이 있는 상황에서는 성능이 향상될 수 있습니다.  
  
 스냅샷 트랜잭션은 다른 트랜잭션에서 행이 업데이트되는 것을 방지하는 잠금을 유지하면서 항상 낙관적 동시성 제어를 사용합니다. 스냅샷 트랜잭션에서 트랜잭션이 시작된 후 변경된 행에 대한 업데이트를 커밋하려고 하면 트랜잭션이 롤백되고 오류가 발생합니다.  
  
## <a name="working-with-snapshot-isolation-in-adonet"></a>ADO.NET에서 스냅샷 격리 사용  
 스냅샷 격리는 ADO.NET에서 <xref:System.Data.SqlClient.SqlTransaction> 클래스를 통해 지원됩니다. 데이터베이스가 snapshot 격리를 사용 하도록 설정 되었지만 READ_COMMITTED_SNAPSHOT ON에 대해 구성 되지 않은 경우에는 <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> 메서드를 호출할 때 **IsolationLevel** 열거 값을 사용 하 여 <xref:System.Data.SqlClient.SqlTransaction>을 시작 해야 합니다. 이 코드 조각에서는 연결을 열려 있는 <xref:System.Data.SqlClient.SqlConnection> 개체로 가정합니다.  
  
```vb  
Dim sqlTran As SqlTransaction = _  
  connection.BeginTransaction(IsolationLevel.Snapshot)  
```  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### <a name="example"></a>예제  
 다음 예제에서는 잠겨 있는 데이터에 대한 액세스를 시도하여 다른 격리 수준이 작동하는 방법을 보여 줍니다. 이 예제는 프로덕션 코드에는 사용할 수 없습니다.  
  
 이 코드는 SQL Server의 **AdventureWorks** 예제 데이터베이스에 연결 하 고 **testsnapshot** 이라는 테이블을 만들고 데이터 행 하나를 삽입 합니다. 이 코드에서는 ALTER DATABASE Transact-SQL 문을 사용하여 데이터베이스에 스냅샷 격리 기능을 설정하지만 READ_COMMITTED_SNAPSHOT 옵션을 설정하지 않으므로 기본 READ COMMITTED 격리 수준 동작이 그대로 적용됩니다. 그런 다음 이 코드에서는 다음 작업을 수행합니다.  
  
- sqlTransaction1을 시작하지만 완료하지는 않습니다. 이 트랜잭션은 SERIALIZABLE 격리 수준을 사용하여 업데이트 트랜잭션을 시작합니다. 이렇게 하면 테이블이 잠깁니다.  
  
- 두 번째 연결을 열고 스냅숏 격리 수준을 사용 하 여 두 번째 트랜잭션을 시작 하 여 **Testsnapshot** 테이블의 데이터를 읽습니다. 스냅샷 격리가 활성화되므로 이 트랜잭션에서 sqlTransaction1이 시작되기 전에 존재하는 데이터를 읽을 수 있습니다.  
  
- 세 번째 연결을 열고 READ COMMITTED 격리 수준을 사용하여 트랜잭션을 시작함으로써 테이블의 데이터를 읽으려고 합니다. 이 경우 첫 번째 트랜잭션에서 테이블에 있는 잠금을 통과하여 읽을 수 없기 때문에 코드에서 데이터를 읽을 수 없으며 제한 시간이 초과됩니다. REPEATABLE READ 및 SERIALIZABLE 격리 수준에서도 첫 번째 트랜잭션에 있는 잠금을 통과하여 읽을 수 없으므로 이러한 격리 수준이 사용되는 경우 동일한 결과가 발생합니다.  
  
- 네 번째 연결을 열고 READ UNCOMMITTED 격리 수준을 사용하여 트랜잭션을 시작합니다. 이 격리 수준은 sqlTransaction1에서 커밋되지 않은 값의 더티 읽기를 수행합니다. 첫 번째 트랜잭션이 커밋되지 않는 경우 이 값은 데이터베이스에 실제로 존재하지 않습니다.  
  
- 첫 번째 트랜잭션을 롤백하고, **testsnapshot** 테이블을 삭제 하 고 **AdventureWorks** 데이터베이스에 대 한 스냅숏 격리를 해제 하 여 정리 합니다.  
  
> [!NOTE]
> 다음 예제에서는 연결 풀링을 해제한 상태에서 동일한 연결 문자열을 사용합니다. 연결이 풀링된 경우, 연결의 격리 수준을 재설정하더라도 서버에서는 격리 수준이 재설정되지 않습니다. 따라서 풀링된 동일한 내부 연결을 사용하는 후속 연결은 풀링된 연결의 격리 수준으로 설정된 각각의 격리 수준에서 시작됩니다. 연결 풀링을 해제하는 대신 각 연결에 대해 명시적으로 격리 수준을 설정할 수도 있습니다.  
  
 [!code-csharp[DataWorks SnapshotIsolation.Demo#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.Demo/CS/source.cs#1)]
 [!code-vb[DataWorks SnapshotIsolation.Demo#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.Demo/VB/source.vb#1)]  
  
### <a name="example"></a>예제  
 다음 예제에서는 데이터가 수정될 때 나타나는 스냅샷 격리의 동작을 보여 줍니다. 이 코드에서는 다음 작업을 수행합니다.  
  
- **AdventureWorks** 샘플 데이터베이스에 연결 하 고 스냅숏 격리를 사용 하도록 설정 합니다.  
  
- **TestSnapshotUpdate** 라는 테이블을 만들고 세 개의 샘플 데이터 행을 삽입 합니다.  
  
- SNAPSHOT 격리를 사용하여 sqlTransaction1을 시작하지만 완료하지는 않습니다. 트랜잭션에서 데이터 행 세 개가 선택됩니다.  
  
- **AdventureWorks** 에 대 한 두 번째 **SqlConnection** 을 만들고 sqlTransaction1에서 선택 된 행 중 하나에서 값을 업데이트 하는 READ COMMITTED 격리 수준을 사용 하 여 두 번째 트랜잭션을 만듭니다.  
  
- sqlTransaction2를 커밋합니다.  
  
- sqlTransaction1로 돌아가서 sqlTransaction1이 커밋된 동일한 행에 대한 업데이트를 시도합니다. 오류 3960이 발생하고 sqlTransaction1이 자동으로 롤백됩니다. **SqlException** 및 **SqlException** 가 콘솔 창에 표시 됩니다.  
  
- **AdventureWorks** 에서 스냅숏 격리를 해제 하 고 **TestSnapshotUpdate** 테이블을 삭제 하는 정리 코드를 실행 합니다.  
  
 [!code-csharp[DataWorks SnapshotIsolation.DemoUpdate#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.DemoUpdate/CS/source.cs#1)]
 [!code-vb[DataWorks SnapshotIsolation.DemoUpdate#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.DemoUpdate/VB/source.vb#1)]  
  
### <a name="using-lock-hints-with-snapshot-isolation"></a>스냅샷 격리와 함께 잠금 힌트 사용  
 앞의 예제에서는 첫 번째 트랜잭션에서 데이터를 선택한 후 첫 번째 트랜잭션이 완료되기 전에 두 번째 트랜잭션에서 데이터를 업데이트하므로 첫 번째 트랜잭션에서 동일한 행을 업데이트하려고 할 때 업데이트 충돌이 발생하게 됩니다. 트랜잭션을 시작할 때 잠금 힌트를 제공하면 장기 실행 스냅샷 트랜잭션에서 업데이트 충돌을 줄일 수 있습니다. 다음 SELECT 문에서는 UDPLOCK 힌트를 사용하여 선택한 행을 잠급니다.  
  
```sql  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
 UPDLOCK 잠금 힌트를 사용하면 첫 번째 트랜잭션이 완료되기 전에 행에 대한 업데이트 시도가 차단됩니다. 따라서 선택한 행이 트랜잭션에서 나중에 업데이트되는 경우에도 충돌이 발생하지 않습니다. SQL Server 온라인 설명서의 "Locking Hints"를 참조하세요.  
  
 애플리케이션에서 충돌이 자주 발생하는 경우 스냅샷 격리는 적합한 방법이 될 수 없습니다. 힌트는 꼭 필요한 경우에만 사용해야 합니다. 작동 시 잠금 힌트를 계속해서 사용하도록 애플리케이션을 디자인해서는 안 됩니다.  
  
## <a name="see-also"></a>참조

- [SQL Server 및 ADO.NET](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
- [트랜잭션 잠금 및 행 버전 관리 가이드](/sql/relational-databases/sql-server-transaction-locking-and-row-versioning-guide)
