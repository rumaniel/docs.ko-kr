---
title: DependentTransaction으로 동시성 관리
ms.date: 03/30/2017
ms.assetid: b85a97d8-8e02-4555-95df-34c8af095148
ms.openlocfilehash: 62cbb8825171628b29a5519ca9e3ae31c2058a03
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662955"
---
# <a name="managing-concurrency-with-dependenttransaction"></a>DependentTransaction으로 동시성 관리
<xref:System.Transactions.Transaction> 개체는 <xref:System.Transactions.Transaction.DependentClone%2A> 메서드를 사용하여 만듭니다. 이 개체는 다른 코드 부분(예: 작업자 스레드)이 여전히 트랜잭션에서 작업을 수행하는 동안 트랜잭션이 커밋되지 않도록 하는 용도로만 사용됩니다. 복제된 트랜잭션에서 수행한 작업이 완료되어 커밋할 준비가 되면 <xref:System.Transactions.DependentTransaction.Complete%2A> 메서드를 사용하여 트랜잭션 작성자에게 알릴 수 있습니다. 따라서 데이터의 일관성과 정확성을 유지할 수 있습니다.  
  
 <xref:System.Transactions.DependentTransaction> 클래스는 비동기 작업 간의 일관성을 관리하는 데 사용할 수도 있습니다. 이 시나리오에서는 종속 복제본이 해당 작업을 수행하는 동안 부모가 계속해서 코드를 실행할 수 있습니다. 즉, 종속 복제본이 완료될 때까지 부모의 실행이 차단되지 않습니다.  
  
## <a name="creating-a-dependent-clone"></a>종속 복제본 만들기  
 종속 트랜잭션을 만들려면 <xref:System.Transactions.Transaction.DependentClone%2A> 메서드를 호출하고 <xref:System.Transactions.DependentCloneOption> 열거를 매개 변수로 전달합니다. 이 매개 변수는 종속 복제본이 `Commit` 메서드를 호출하여 트랜잭션을 커밋할 준비가 되었음을 나타내기 전에 부모 트랜잭션에서 <xref:System.Transactions.DependentTransaction.Complete%2A>이 호출된 경우의 트랜잭션 동작을 정의합니다. 이 매개 변수에 유효한 값은 다음과 같습니다.  
  
- <xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete> 축소 또는 될 때까지 부모 트랜잭션이 시간까지 부모 트랜잭션의 커밋 프로세스를 차단 하는 종속 트랜잭션을 만듭니다 <xref:System.Transactions.DependentTransaction.Complete%2A> 완료를 나타내는 모든 종속 항목에서 호출 됩니다. 이 기능은 종속 트랜잭션이 완료될 때까지 클라이언트에서 부모 트랜잭션을 커밋하지 않으려는 경우에 유용합니다. 부모가 종속 트랜잭션보다 일찍 작업을 마치고 트랜잭션에서 <xref:System.Transactions.CommittableTransaction.Commit%2A>을 호출하면 모든 종속 트랜잭션이 <xref:System.Transactions.DependentTransaction.Complete%2A>를 호출할 때까지 커밋 프로세스가 트랜잭션에 대해 추가 작업을 수행하고 새 인리스트먼트를 만들 수 있는 상태로 차단됩니다. 모든 트랜잭션이 작업을 완료하고 <xref:System.Transactions.DependentTransaction.Complete%2A>를 호출하면 즉시 트랜잭션의 커밋 프로세스가 시작됩니다.  
  
- 반면 <xref:System.Transactions.DependentCloneOption.RollbackIfNotComplete>는 <xref:System.Transactions.CommittableTransaction.Commit%2A>가 호출되기 전에 부모 트랜잭션에서 <xref:System.Transactions.DependentTransaction.Complete%2A>이 호출되는 경우 자동으로 중단되는 종속 트랜잭션을 만듭니다. 이 경우 종속 트랜잭션에서 수행된 모든 작업이 하나의 트랜잭션 수명 내에서 그대로 유지되며 아무도 작업의 일부만 커밋할 수 없습니다.  
  
 <xref:System.Transactions.DependentTransaction.Complete%2A> 메서드는 애플리케이션이 종속 트랜잭션에서 작업을 완료할 때 한 번만 호출되어야 합니다. 그렇지 않으면 <xref:System.InvalidOperationException>이 throw됩니다. 이 메서드를 호출한 후에는 트랜잭션에서 추가 작업을 시도하지 말아야 합니다. 그렇지 않으면 예외가 throw됩니다.  
  
 다음 코드 예제에서는 종속 트랜잭션을 복제하고 작업자 스레드로 전달함으로써 종속 트랜잭션을 만들어 두 개의 동시 작업을 관리하는 방법을 보여 줍니다.  
  
```csharp  
public class WorkerThread  
{  
    public void DoWork(DependentTransaction dependentTransaction)  
    {  
        Thread thread = new Thread(ThreadMethod);  
        thread.Start(dependentTransaction);   
    }  
  
    public void ThreadMethod(object transaction)   
    {   
        DependentTransaction dependentTransaction = transaction as DependentTransaction;  
        Debug.Assert(dependentTransaction != null);   
        try  
        {  
            using(TransactionScope ts = new TransactionScope(dependentTransaction))  
            {  
                /* Perform transactional work here */   
                ts.Complete();  
            }  
        }  
        finally  
        {  
            dependentTransaction.Complete();   
             dependentTransaction.Dispose();   
        }  
    }  
  
//Client code   
using(TransactionScope scope = new TransactionScope())  
{  
    Transaction currentTransaction = Transaction.Current;  
    DependentTransaction dependentTransaction;      
    dependentTransaction = currentTransaction.DependentClone(DependentCloneOption.BlockCommitUntilComplete);  
    WorkerThread workerThread = new WorkerThread();  
    workerThread.DoWork(dependentTransaction);  
    /* Do some transactional work here, then: */  
    scope.Complete();  
}  
```  
  
 클라이언트 코드에서는 앰비언트 트랜잭션도 설정하는 트랜잭션 범위를 만듭니다. 앰비언트 트랜잭션을 작업자 스레드로 전달하면 안 됩니다. 대신 현재 트랜잭션에서 <xref:System.Transactions.Transaction.DependentClone%2A> 메서드를 호출하여 현재(앰비언트) 트랜잭션을 복제하고 종속 트랜잭션을 작업자 스레드로 전달해야 합니다.  
  
 `ThreadMethod` 메서드는 새 스레드에서 실행됩니다. 클라이언트는 새 스레드를 시작하고 종속 트랜잭션을 `ThreadMethod` 매개 변수로 전달합니다.  
  
 <xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete>를 사용하여 종속 트랜잭션이 만들어지므로 두 번째 스레드에서 수행한 모든 트랜잭션 작업이 완료되고 종속 트랜잭션에서 <xref:System.Transactions.DependentTransaction.Complete%2A>가 호출될 때까지 트랜잭션을 커밋할 수 없습니다. 즉, 클라이언트의 범위가 끝나는 경우 (끝의 트랜잭션 개체를 삭제 하려고 할 때 합니다 **를 사용 하 여** 문) 새 스레드가 호출 하기 전에 <xref:System.Transactions.DependentTransaction.Complete%2A> 종속 트랜잭션에서 될때까지클라이언트코드가차단<xref:System.Transactions.DependentTransaction.Complete%2A> 종속에서 호출 됩니다. 그런 다음 트랜잭션이 커밋 또는 중단을 완료할 수 있습니다.  
  
## <a name="concurrency-issues"></a>동시성 문제  
 <xref:System.Transactions.DependentTransaction> 클래스를 사용할 때 주의해야 하는 몇 가지 추가 동시성 문제가 있습니다.  
  
- 작업자 스레드에서 트랜잭션을 롤백하지만 부모가 커밋하려고 시도하는 경우 <xref:System.Transactions.TransactionAbortedException>이 throw됩니다.  
  
- 트랜잭션의 각 작업자 스레드에 대해 새 종속 복제본을 만들어야 합니다. 동일한 종속 복제본을 여러 스레드로 전달하지 마십시오. 스레드 중 하나만 복제본에서 <xref:System.Transactions.DependentTransaction.Complete%2A>를 호출할 수 있습니다.  
  
- 작업자 스레드가 새 작업자 스레드를 생성하는 경우 종속 복제본에서 종속 복제본을 만들어 새 스레드로 전달해야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Transactions.DependentTransaction>
