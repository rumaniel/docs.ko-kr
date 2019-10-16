---
title: 트랜잭션 및 대량 복사 작업
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.openlocfilehash: 73c375f9acfd193680982994ed0852454cefebe5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791448"
---
# <a name="transaction-and-bulk-copy-operations"></a>트랜잭션 및 대량 복사 작업
대량 복사 작업을 격리된 작업이나 여러 단계로 이루어진 트랜잭션의 일부로 수행할 수 있습니다. 후자를 사용하면 다른 데이터베이스 작업(삽입, 업데이트, 삭제 등)을 수행하면서 같은 트랜잭션 내에서 둘 이상의 대량 복사 작업을 수행할 수 있을 뿐만 아니라 전체 트랜잭션을 커밋하거나 롤백할 수 있습니다.  
  
 기본적으로 대량 복사 작업은 격리된 작업으로 수행됩니다. 대량 복사 작업은 롤백할 수 없는 비트랜잭트 방식으로 이루어집니다. 오류가 발생할 때 대량 복사의 전체 또는 일부를 롤백해야 하는 경우 관리 되는 <xref:System.Data.SqlClient.SqlBulkCopy>트랜잭션을 사용 하거나 기존 트랜잭션 내에서 대량 복사 작업을 수행 하거나 **시스템 트랜잭션에**<xref:System.Transactions.Transaction>참여할 수 있습니다.  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>비트랜잭트 대량 복사 작업 수행  
 다음 콘솔 애플리케이션은 비트랜잭트 대량 복사 작업에서 작업 중에 오류가 발생하는 경우를 보여 줍니다.  
  
 이 예에서는 원본 테이블과 대상 테이블에 `Identity` **ProductID**라는 열이 각각 포함 되어 있습니다. 이 코드는 먼저 모든 행을 삭제 한 다음 **ProductID** 가 원본 테이블에 있는 것으로 알려진 단일 행을 삽입 하 여 대상 테이블을 준비 합니다. 기본적으로 `Identity` 열의 새 값이 대상 테이블의 추가된 행마다 생성됩니다. 이 예제에서는 연결이 열려 있기 때문에 대량 로드 프로세스에서 소스 테이블의 `Identity` 값을 대신 강제로 사용해야 하는 경우에 옵션이 설정됩니다.  
  
 대량 복사 작업은 <xref:System.Data.SqlClient.SqlBulkCopy.BatchSize%2A> 속성을 10으로 설정하여 실행합니다. 작업 중 올바르지 않은 행이 발견되면 예외가 throw됩니다. 이 첫 번째 예제에서 대량 복사 작업은 비트랜잭트 방식입니다. 오류 지점까지 복사한 모든 배치가 커밋되어, 중복 키를 포함하는 배치가 롤백되고 다른 모든 배치가 처리될 때까지 대량 복사 작업이 중지됩니다.  
  
> [!NOTE]
> 이 샘플에 설명 된 대로 작업 테이블을 만든 경우가 아니면 실행 되지 것입니다 [대량 복사 예제 설정](bulk-copy-example-setup.md)합니다. 이 코드는 사용 하는 구문을 보여 주기 위해 제공 됩니다 **SqlBulkCopy** 만 합니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우 transact-sql`INSERT … SELECT` 문을 사용 하 여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
 [!code-csharp[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/VB/source.vb#1)]  
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>트랜잭션에서 전용 대량 복사 작업 수행  
 기본적으로 대량 복사 작업은 그 자체만으로도 고유한 트랜잭션입니다. 전용 대량 복사 작업을 수행하려면 연결 문자열을 사용하여 <xref:System.Data.SqlClient.SqlBulkCopy>의 새 인스턴스를 만들거나 활성 트랜잭션 없이 기존 <xref:System.Data.SqlClient.SqlConnection> 개체를 사용합니다. 각 시나리오에서는 대량 복사 작업이 만들어진 후 트랜잭션이 커밋되거나 롤백됩니다.  
  
 <xref:System.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> 클래스 생성자에서 <xref:System.Data.SqlClient.SqlBulkCopy> 옵션을 명시적으로 지정하여 대량 복사 작업이 자체 트랜잭션에서 실행되도록 명시적으로 지정함으로써 대량 복사 작업의 각 배치가 별도의 트랜잭션 내에서 실행되도록 할 수 있습니다.  
  
> [!NOTE]
> 배치가 실행되는 트랜잭션이 각각 다르기 때문에 대량 복사 작업 중에 오류가 발생할 경우 현재 배치 내의 모든 행이 롤백되지만 이전 배치의 행은 데이터베이스에 유지됩니다.  
  
 다음 콘솔 응용 프로그램은 다음 한 가지를 제외하면 앞의 예제와 유사합니다. 이 예제에서 대량 복사 작업은 고유 트랜잭션을 관리합니다. 오류 지점까지 복사한 모든 배치가 커밋되어, 중복 키를 포함하는 배치가 롤백되고 다른 모든 배치가 처리될 때까지 대량 복사 작업이 중지됩니다.  
  
> [!IMPORTANT]
> 이 샘플에 설명 된 대로 작업 테이블을 만든 경우가 아니면 실행 되지 것입니다 [대량 복사 예제 설정](bulk-copy-example-setup.md)합니다. 이 코드는 사용 하는 구문을 보여 주기 위해 제공 됩니다 **SqlBulkCopy** 만 합니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우 transact-sql`INSERT … SELECT` 문을 사용 하 여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
 [!code-csharp[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/VB/source.vb#1)]  
  
## <a name="using-existing-transactions"></a>기존 트랜잭션 사용  
 기존 <xref:System.Data.SqlClient.SqlTransaction> 개체를 <xref:System.Data.SqlClient.SqlBulkCopy> 생성자의 매개 변수로 지정할 수 있습니다. 이 경우, 대량 복사 작업은 기존 트랜잭션에서 수행되며 트랜잭션 상태는 변경되지 않습니다. 즉, 커밋되거나 중단되지 않습니다. 따라서 애플리케이션에서 다른 데이터베이스 작업과 함께 대량 복사 작업을 하나의 트랜잭션에 포함시킬 수 있습니다. 그러나 <xref:System.Data.SqlClient.SqlTransaction> 개체를 지정하지 않고 null 참조를 전달하며 연결에 활성 트랜잭션이 있는 경우에는 예외가 throw됩니다.  
  
 오류가 발생하여 전체 대량 복사 작업을 롤백해야 하는 경우나 롤백할 수 있는 보다 큰 프로세스의 일부로 대량 복사를 실행해야 하는 경우에는 <xref:System.Data.SqlClient.SqlTransaction> 개체를 <xref:System.Data.SqlClient.SqlBulkCopy> 생성자에 제공할 수 있습니다.  
  
 다음 콘솔 애플리케이션은 다음 한 가지를 제외하면 첫 번째(비트랜잭트 방식) 예제와 유사합니다. 이 예제에서는 대량 복사 작업이 보다 큰 외부 트랜잭션에 포함됩니다. 기본 키 위반 오류가 발생하는 경우에는 전체 트랜잭션이 롤백되고 대상 테이블에 행이 추가되지 않습니다.  
  
> [!IMPORTANT]
> 이 샘플에 설명 된 대로 작업 테이블을 만든 경우가 아니면 실행 되지 것입니다 [대량 복사 예제 설정](bulk-copy-example-setup.md)합니다. 이 코드는 사용 하는 구문을 보여 주기 위해 제공 됩니다 **SqlBulkCopy** 만 합니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우 transact-sql`INSERT … SELECT` 문을 사용 하 여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
 [!code-csharp[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/VB/source.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [SQL Server에서 대량 복사 작업](bulk-copy-operations-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
