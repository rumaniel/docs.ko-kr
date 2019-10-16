---
title: ADO.NET 및 LINQ to SQL
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49ac6da0-f2e1-46fa-963e-1b6dcb63fef7
ms.openlocfilehash: 0bebc8d890325ec4ab090470952e11b90d0e37ef
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248113"
---
# <a name="adonet-and-linq-to-sql"></a>ADO.NET 및 LINQ to SQL
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]는 ADO.NET 기술 제품군의 일부입니다. ADO.NET 공급자 모델에서 제공 하는 서비스를 기반으로 합니다. 따라서 기존 ADO.NET 응용 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 프로그램과 코드를 혼합 하 고 현재 ADO.NET 솔루션을로 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]마이그레이션할 수 있습니다. 다음 그림에서는 이 관계를 간략하게 보여 줍니다.  
  
 ![LINQ to SQL 및 ADO.NET](./media/dlinq-3.png "DLinq_3")  
  
## <a name="connections"></a>Connections  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 를<xref:System.Data.Linq.DataContext>만들 때 기존 ADO.NET 연결을 제공할 수 있습니다. 쿼리를 포함한 <xref:System.Data.Linq.DataContext>에 대한 모든 작업은 제공된 이 연결을 사용합니다. 연결이 이미 열려 있는 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 사용자의 작업이 끝났을 때 연결을 그대로 둡니다.  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#4)]
 [!code-vb[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#4)]  
  
 다음 코드와 같이 <xref:System.Data.Linq.DataContext.Connection%2A> 속성을 사용하여 항상 연결에 액세스하고 연결을 닫을 수 있습니다.  
  
 [!code-csharp[DLinqAdoNet#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#1)]
 [!code-vb[DLinqAdoNet#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#1)]  
  
## <a name="transactions"></a>의  
 애플리케이션에서 이미 고유한 데이터베이스 트랜잭션을 시작했으며 <xref:System.Data.Linq.DataContext>를 관련시키려는 경우 해당 트랜잭션을 <xref:System.Data.Linq.DataContext>에 제공할 수 있습니다.  
  
 .NET Framework를 사용 하 여 트랜잭션을 수행 하는 기본 방법은 <xref:System.Transactions.TransactionScope> 개체를 사용 하는 것입니다. 이 방법을 사용하면 데이터베이스 및 다른 메모리 상주 리소스 관리자 사이에서 작동하는 분산 트랜잭션을 만들 수 있습니다. 트랜잭션 범위는 시작하는 데 리소스가 거의 필요하지 않습니다. 트랜잭션 범위는 해당 범위 내에 여러 연결이 있는 경우에만 분산 트랜잭션으로 승격됩니다.  
  
 [!code-csharp[DLinqAdoNet#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#2)]
 [!code-vb[DLinqAdoNet#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#2)]  
  
 이 방법을 모든 데이터베이스에 사용할 수 있는 것은 아닙니다. 예를 들어 SQL Server 2000 서버에 대해 작동 하는 경우 SqlClient 연결은 시스템 트랜잭션을 승격할 수 없습니다. 대신에 사용 중인 트랜잭션 범위가 있을 때마다 완전한 분산 트랜잭션에 자동으로 참여합니다.  
  
## <a name="direct-sql-commands"></a>SQL 명령 직접 실행  
 <xref:System.Data.Linq.DataContext>를 사용하여 변경 내용을 쿼리하거나 전송하는 기능으로는 원하는 특수한 작업을 수행할 수 없는 경우가 종종 있습니다. 이러한 상황에서는 <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> 메서드를 사용하여 SQL 명령을 데이터베이스에 대해 실행하고 쿼리 결과를 개체로 변환할 수 있습니다.  
  
 예를 들어 `Customer` 클래스의 데이터가 두 개의 테이블(customer1 및 customer2)에 퍼져 있다고 가정해 봅니다. 다음 쿼리는 `Customer` 개체의 시퀀스를 반환합니다.  
  
 [!code-csharp[DLinqAdoNet#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#3)]
 [!code-vb[DLinqAdoNet#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#3)]  
  
 표 형식 결과의 열 이름이 엔터티 클래스의 열 속성과 일치할 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 모든 SQL 쿼리에서 개체를 만듭니다.  
  
### <a name="parameters"></a>매개 변수  
 <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> 메서드에서는 매개 변수가 허용됩니다. 다음 코드는 매개 변수화된 쿼리를 실행합니다.  
  
 [!code-csharp[DlinqAdoNet#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#4)]
 [!code-vb[DlinqAdoNet#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#4)]  
  
> [!NOTE]
> 매개 변수는 `Console.WriteLine()` 및 `String.Format()`에서 사용되는 동일한 중괄호 표기법을 사용하여 쿼리 텍스트에서 표현됩니다. `String.Format()`은 제공된 쿼리 문자열을 가지며 중괄호로 묶인 매개 변수를 `@p0`, `@p1` …, `@p(n)` 등과 같은 생성된 매개 변수 이름으로 대체합니다.  
  
## <a name="see-also"></a>참고자료

- [배경 정보](background-information.md)
- [방법: ADO.NET 명령과 DataContext 사이에 연결 다시 사용](how-to-reuse-a-connection-between-an-ado-net-command-and-a-datacontext.md)
