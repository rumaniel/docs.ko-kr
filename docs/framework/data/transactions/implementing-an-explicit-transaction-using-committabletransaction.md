---
title: CommittableTransaction을 사용하여 명시적 트랜잭션 구현
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 29efe5e5-897b-46c2-a35f-e599a273acc8
ms.openlocfilehash: 19b62c24d00903d1494a755dbeabb460935cdacd
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205933"
---
# <a name="implementing-an-explicit-transaction-using-committabletransaction"></a>CommittableTransaction을 사용하여 명시적 트랜잭션 구현
<xref:System.Transactions.CommittableTransaction> 클래스를 암시적으로 사용하는 경우와 달리 <xref:System.Transactions.TransactionScope> 클래스는 애플리케이션이 트랜잭션을 사용할 수 있는 명시적 방법을 제공합니다. 이 클래스는 여러 함수 호출이나 여러 스레드 호출에 같은 트랜잭션을 사용하려는 애플리케이션에 유용합니다. <xref:System.Transactions.TransactionScope> 클래스와 달리 애플리케이션 작성기에서 특별히 <xref:System.Transactions.CommittableTransaction.Commit%2A> 및 <xref:System.Transactions.Transaction.Rollback%2A> 메서드를 호출하여 트랜잭션을 커밋하거나 중단해야 합니다.  
  
## <a name="overview-of-the-committabletransaction-class"></a>CommittableTransaction 클래스 개요  
 <xref:System.Transactions.CommittableTransaction> 클래스는 <xref:System.Transactions.Transaction> 클래스에서 파생되므로 후자의 모든 기능을 제공합니다. <xref:System.Transactions.Transaction.Rollback%2A> 개체의 롤백에 사용할 수도 있는 <xref:System.Transactions.Transaction> 클래스의 <xref:System.Transactions.CommittableTransaction> 메서드는 특히 유용합니다.  
  
 <xref:System.Transactions.Transaction> 클래스는 <xref:System.Transactions.CommittableTransaction> 클래스와 유사하지만 `Commit` 메서드를 제공하지 않습니다. 이 클래스를 사용하면 트랜잭션의 커밋 시기에 대한 제어를 유지하면서 트랜잭션 개체(또는 개체의 복제본)를 다른 스레드에 있을 수도 있는 다른 메서드로 전달할 수 있습니다. 호출된 코드가 트랜잭션에 참여하고 응답할 수 있지만 <xref:System.Transactions.CommittableTransaction> 개체의 작성자만 트랜잭션을 커밋할 수 있습니다.  
  
 <xref:System.Transactions.CommittableTransaction> 클래스를 사용할 때는 다음 사항을 고려해야 합니다.  
  
- <xref:System.Transactions.CommittableTransaction> 트랜잭션을 만들면 앰비언트 트랜잭션이 설정되지 않습니다. 해당되는 경우 리소스 관리자가 올바른 트랜잭션 컨텍스트에서 작동하려면 앰비언트 트랜잭션을 구체적으로 설정하고 다시 설정해야 합니다. 현재 앰비언트 트랜잭션을 설정하려면 전역 <xref:System.Transactions.Transaction.Current%2A> 개체의 정적 <xref:System.Transactions.Transaction> 속성을 설정합니다.  
  
- <xref:System.Transactions.CommittableTransaction> 개체는 다시 사용할 수 없습니다. <xref:System.Transactions.CommittableTransaction> 개체가 커밋 또는 롤백되고 나면 다시 트랜잭션에 사용할 수 없습니다. 즉, 현재 앰비언트 트랜잭션 컨텍스트로 설정할 수 없습니다.  
  
## <a name="creating-a-committabletransaction"></a>CommittableTransaction 만들기  
 다음 샘플에서는 새 <xref:System.Transactions.CommittableTransaction>을 만들어 커밋합니다.  
  
 [!code-csharp[Tx_CommittableTx#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/tx_committabletx/cs/committabletxwithsql.cs#1)]
 [!code-vb[Tx_CommittableTx#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/tx_committabletx/vb/committabletxwithsql.vb#1)]  
  
 <xref:System.Transactions.CommittableTransaction> 인스턴스를 만드는 경우 앰비언트 트랜잭션 컨텍스트가 자동으로 설정되지 않습니다. 따라서 리소스 관리자에 대한 작업은 트랜잭션의 일부가 아닙니다. 전역 <xref:System.Transactions.Transaction.Current%2A> 개체의 <xref:System.Transactions.Transaction>  속성은 앰비언트 트랜잭션을 설정하거나 검색하는 데 사용되며 애플리케이션에서 수동으로 설정하여 리소스 관리자가 트랜잭션에 참여할 수 있도록 해야 합니다. 이전의 앰비언트 트랜잭션을 저장하고 <xref:System.Transactions.CommittableTransaction> 개체의 사용을 마칠 때 복원하는 것도 좋은 방법입니다.  
  
 트랜잭션을 커밋하려면 명시적으로 <xref:System.Transactions.CommittableTransaction.Commit%2A> 메서드를 호출해야 합니다. 트랜잭션을 롤백하는 경우 <xref:System.Transactions.Transaction.Rollback%2A> 메서드를 호출해야 합니다. <xref:System.Transactions.CommittableTransaction>이 커밋 또는 롤백될 때까지 트랜잭션에 관련된 모든 리소스가 잠겨 있습니다.  
  
 함수 호출 및 스레드에서 <xref:System.Transactions.CommittableTransaction> 개체를 사용할 수 있습니다. 그러나 예외를 처리하고 오류가 발생할 경우 구체적으로 <xref:System.Transactions.Transaction.Rollback%28System.Exception%29> 메서드를 호출하는 작업은 애플리케이션 개발자의 책임입니다.  
  
## <a name="asynchronous-commit"></a>비동기 커밋  
 <xref:System.Transactions.CommittableTransaction> 클래스는 트랜잭션의 비동기 커밋을 위한 메커니즘도 제공합니다. 트랜잭션 커밋은 여러 번의 데이터베이스 액세스와 가능한 네트워크 대기 시간을 수반하므로 시간이 오래 걸릴 수 있습니다. 처리량이 많은 애플리케이션에서 교착 상태를 방지하려는 경우 비동기 커밋을 사용하여 가능한 한 빨리 트랜잭션 작업을 완료하고 커밋 작업을 백그라운드 작업으로 실행할 수 있습니다. <xref:System.Transactions.CommittableTransaction.BeginCommit%2A> 클래스의 <xref:System.Transactions.CommittableTransaction.EndCommit%2A> 및 <xref:System.Transactions.CommittableTransaction> 메서드를 사용하여 이 작업을 수행할 수 있습니다.  
  
 <xref:System.Transactions.CommittableTransaction.BeginCommit%2A>을 호출하여 보류 중인 커밋을 스레드 풀의 스레드로 디스패치할 수 있습니다. <xref:System.Transactions.CommittableTransaction.EndCommit%2A>을 호출하여 트랜잭션이 실제로 커밋되었는지 여부를 확인할 수도 있습니다. 어떤 이유로든 트랜잭션을 커밋하지 못하면 <xref:System.Transactions.CommittableTransaction.EndCommit%2A>에서 트랜잭션 예외를 발생시킵니다. <xref:System.Transactions.CommittableTransaction.EndCommit%2A>을 호출할 때까지 트랜잭션이 아직 커밋되지 않은 경우 트랜잭션이 커밋 또는 중단될 때까지 호출자가 차단됩니다.  
  
 비동기 커밋을 수행하는 가장 쉬운 방법은 커밋이 완료될 때 호출할 콜백 메서드를 제공하는 것입니다. 그러나 호출에 사용된 원래 <xref:System.Transactions.CommittableTransaction.EndCommit%2A> 개체에서 <xref:System.Transactions.CommittableTransaction> 메서드를 호출해야 합니다. 클래스에서 <xref:System.Transactions.CommittableTransaction> 클래스를 구현 <xref:System.IAsyncResult> 하므로 해당 개체를 가져오기 위해 콜백 메서드의 *IAsyncResult* 매개 변수를 다운 캐스트할 수 있습니다.  
  
 다음 예제에서는 비동기 커밋을 수행하는 방법을 보여 줍니다.  
  
```csharp  
public void DoTransactionalWork()  
{  
     Transaction oldAmbient = Transaction.Current;  
     CommittableTransaction committableTransaction = new CommittableTransaction();  
     Transaction.Current = committableTransaction;  
  
     try  
     {  
          /* Perform transactional work here */  
          // No errors - commit transaction asynchronously  
          committableTransaction.BeginCommit(OnCommitted,null);  
     }  
     finally  
     {  
          //Restore the ambient transaction   
          Transaction.Current = oldAmbient;  
     }  
}  
void OnCommitted(IAsyncResult asyncResult)  
{  
     CommittableTransaction committableTransaction;  
     committableTransaction = asyncResult as CommittableTransaction;     
     Debug.Assert(committableTransaction != null);  
     try  
     {  
          using(committableTransaction)  
          {  
               committableTransaction.EndCommit(asyncResult);  
          }  
     }  
     catch(TransactionException e)  
     {  
          //Handle the failure to commit  
     }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [트랜잭션 범위를 사용하여 암시적 트랜잭션 구현](implementing-an-implicit-transaction-using-transaction-scope.md)
- [트랜잭션 처리](index.md)
