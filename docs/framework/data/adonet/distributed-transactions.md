---
title: 분산 트랜잭션
ms.date: 03/30/2017
ms.assetid: 718b257c-bcb2-408e-b004-a7b0adb1c176
ms.openlocfilehash: 143d39356f444bfc3c899164c43c9608a4aab335
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795205"
---
# <a name="distributed-transactions"></a>분산 트랜잭션
트랜잭션은 하나의 단위로 성공(커밋)하거나 실패(중단)한 관련 작업의 집합입니다. *분산 트랜잭션은* 여러 리소스에 영향을 주는 트랜잭션입니다. 분산 트랜잭션을 커밋하는 경우 모든 참가자는 데이터의 모든 변경 내용이 영구적으로 유지된다는 것을 보증해야 합니다. 시스템 작동이 중단되거나 다른 예측할 수 없는 이벤트가 발생해도 변경 내용이 지속되어야 합니다. 참가자 중 하나라도 이러한 보증을 이행하지 못하면 전체 트랜잭션이 실패하게 되며 트랜잭션 범위 내의 모든 데이터 변경 내용이 롤백됩니다.  
  
> [!NOTE]
> 트랜잭션이 활성화된 상태에서 `DataReader`를 시작하는 경우 트랜잭션을 커밋하거나 롤백하면 예외가 throw됩니다.  
  
## <a name="working-with-systemtransactions"></a>System.Transactions 사용  
 .NET Framework에서는 <xref:System.Transactions> 네임스페이스의 API를 통해 분산 트랜잭션을 관리합니다. 여러 영구 리소스 관리자가 관련되어 있는 경우 <xref:System.Transactions> API는 MS DTC(Microsoft Distributed Transaction Coordinator)와 같은 트랜잭션 모니터에 분산 트랜잭션 처리를 위임하게 됩니다. 자세한 내용은 [트랜잭션 기본 사항](../transactions/transaction-fundamentals.md)을 참조 하세요.  
  
 ADO.NET 2.0에서는 연결을 `EnlistTransaction` 인스턴스에 기록하는 <xref:System.Transactions.Transaction> 메서드를 사용하여 분산 트랜잭션에 기록하는 새로운 기능을 지원합니다. 이전 버전의 ADO.NET에서는 연결의 `EnlistDistributedTransaction` 메서드를 사용하여 연결을 이전 버전과의 호환성이 지원되는 <xref:System.EnterpriseServices.ITransaction> 인스턴스에 인리스트먼트함으로써 분산 트랜잭션에 명시적으로 인리스트먼트했습니다. 엔터프라이즈 서비스 트랜잭션에 대 한 자세한 내용은 [엔터프라이즈 서비스 및 COM + 트랜잭션과의 상호 운용성](../transactions/interoperability-with-enterprise-services-and-com-transactions.md)을 참조 하세요.  
  
 .NET Framework Provider for SQL Server를 사용하여 SQL Server 데이터베이스에서 <xref:System.Transactions> 트랜잭션을 실행하는 경우 간단한 <xref:System.Transactions.Transaction>이 자동으로 사용됩니다. 그러면 필요할 때만 트랜잭션을 완전 분산 트랜잭션으로 승격시킬 수 있습니다. 자세한 내용은 [SQL Server와의 시스템 트랜잭션 통합](system-transactions-integration-with-sql-server.md)을 참조 하세요.  
  
> [!NOTE]
> Oracle 데이터베이스가 한 번에 참여할 수 있는 분산 트랜잭션의 최대 수는 기본적으로 10으로 설정되어 있습니다. Oracle 데이터베이스에 연결되어 있을 때 10번째 트랜잭션을 초과하면 예외가 throw됩니다. Oracle은 분산 트랜잭션 내에서 `DDL`을 지원하지 않습니다.  
  
## <a name="automatically-enlisting-in-a-distributed-transaction"></a>자동으로 분산 트랜잭션에 인리스트먼트  
 자동 인리스트먼트는 ADO.NET 연결과 `System.Transactions`를 통합하는 기본 방식입니다. 연결 개체는 트랜잭션이 활성화되어 있음을 인지하는 경우 기존 분산 트랜잭션에 자동으로 인리스트먼트합니다. `System.Transaction`의 측면에서 볼 때 트랜잭션이 활성화되어 있다는 것은 `Transaction.Current`가 null이 아님을 의미합니다. 자동 트랜잭션 인리스트먼트는 연결이 열려 있을 때 발생하며 그 이후에는 트랜잭션 범위 내에서 명령이 실행되더라도 발생하지 않습니다. `Enlist=false`에 대한 연결 문자열 매개 변수로 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType>를 지정하거나 `OLE DB Services=-7`에 대한 연결 문자열 매개 변수로 <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A?displayProperty=nameWithType>을 지정하면 기존 트랜잭션에 대한 자동 인리스트먼트를 비활성화할 수 있습니다. Oracle 및 ODBC 연결 문자열 매개 변수에 대한 자세한 내용은 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A?displayProperty=nameWithType> 및 <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A?displayProperty=nameWithType>을 참조하세요.  
  
## <a name="manually-enlisting-in-a-distributed-transaction"></a>수동으로 분산 트랜잭션에 인리스트먼트  
 자동 인리스트먼트가 비활성화되어 있거나 연결이 열린 후 시작된 트랜잭션에 인리스트먼트해야 하는 경우에는 사용 중인 공급자에 대한 `EnlistTransaction` 개체의 <xref:System.Data.Common.DbConnection> 메서드를 사용하여 기존 분산 트랜잭션에 인리스트먼트할 수 있습니다. 기존 분산 트랜잭션에 인리스트먼트하면 트랜잭션이 커밋되거나 롤백되는 경우 데이터 소스 코드에서 변경된 내용도 함께 커밋되거나 롤백됩니다.  
  
 분산 트랜잭션 인리스트먼트는 특히 비즈니스 개체를 풀링할 때 적용할 수 있습니다. 비즈니스 개체가 열린 연결로 풀링되는 경우 해당 연결이 열리면 자동 트랜잭션 인리스트먼트만 발생합니다. 풀링된 비즈니스 개체를 사용하여 여러 트랜잭션을 수행하는 경우 해당 개체에 대해 열린 연결은 새로 초기화된 트랜잭션에 자동으로 인리스트먼트하지 않습니다. 이 경우 연결에 대해 자동 트랜잭션 인리스트먼트를 비활성화한 다음 `EnlistTransaction`을 사용하여 연결을 트랜잭션에 인리스트먼트할 수 있습니다.  
  
 `EnlistTransaction`기존 트랜잭션에 대 한 참조 인 <xref:System.Transactions.Transaction> 형식의 단일 인수를 사용 합니다. 연결의 `EnlistTransaction` 메서드를 호출한 후에는 해당 연결을 통해 데이터 소스에서 수정된 모든 내용이 트랜잭션에 포함됩니다. null 값을 전달하면 현재 분산 트랜잭션 인리스트먼트에서 연결의 인리스트먼트가 취소됩니다. 연결은 `EnlistTransaction`을 호출하기 전에 열려야 합니다.  
  
> [!NOTE]
> 트랜잭션에 연결을 명시적으로 인리스트먼트하면 첫 번째 트랜잭션이 종료될 때까지 인리스트먼트를 취소하거나 다른 트랜잭션에 인리스트먼트할 수 없습니다.  
  
> [!CAUTION]
> 연결의 `EnlistTransaction` 메서드를 사용하여 연결에서 트랜잭션이 이미 시작된 경우에는 <xref:System.Data.Common.DbConnection.BeginTransaction%2A>이 예외를 throw합니다. 그러나 트랜잭션이 데이터 소스에서 시작된 로컬 트랜잭션(예: <xref:System.Data.SqlClient.SqlCommand>를 사용하여 명시적으로 BEGIN TRANSACTION 문 실행)인 경우에는 `EnlistTransaction`이 로컬 트랜잭션을 롤백하고 요청 시 기존 분산 트랜잭션에 인리스트먼트합니다. 로컬 트랜잭션이 롤백되었다는 알림은 전송되지 않으므로 <xref:System.Data.Common.DbConnection.BeginTransaction%2A>을 사용하여 시작되지 않은 로컬 트랜잭션을 관리해야 합니다. SQL Server에서 .NET Framework Data Provider for SQL Server(`SqlClient`)를 사용하는 경우 등록하려고 시도하면 예외가 throw됩니다. 다른 모든 경우는 탐지되지 않습니다.  
  
## <a name="promotable-transactions-in-sql-server"></a>SQL Server의 승격 가능한 트랜잭션  
 SQL Server에서는 필요한 경우에만 간단한 로컬 트랜잭션을 분산 트랜잭션으로 자동 승격시킬 수 있는 승격 가능한 트랜잭션을 지원합니다. 승격 가능한 트랜잭션은 추가 오버헤드가 필요한 경우를 제외하고 분산 트랜잭션의 추가 오버헤드를 호출하지 않습니다. 자세한 내용 및 코드 샘플은 [SQL Server와의 시스템 트랜잭션 통합](system-transactions-integration-with-sql-server.md)을 참조 하세요.  
  
## <a name="configuring-distributed-transactions"></a>분산 트랜잭션 구성  
 분산 트랜잭션을 사용하기 위해 네트워크에서 MS DTC를 사용해야 할 수도 있습니다. Windows 방화벽이 활성화되어 있는 경우 MS DTC 서비스에서 네트워크를 사용하거나 MS DTC 포트를 열 수 있도록 허용해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [트랜잭션 및 동시성](transactions-and-concurrency.md)
- [SQL Server와의 System.Transactions 통합](system-transactions-integration-with-sql-server.md)
- [ADO.NET 개요](ado-net-overview.md)
