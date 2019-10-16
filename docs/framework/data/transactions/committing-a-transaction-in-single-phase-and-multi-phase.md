---
title: 단일 단계 및 다단계에서 트랜잭션 커밋
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 694ea153-e4db-41ae-96ac-9ac66dcb69a9
ms.openlocfilehash: 2abb9c13e9b0cb394546252e0e51e53c8ff9eefb
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70206006"
---
# <a name="committing-a-transaction-in-single-phase-and-multi-phase"></a>단일 단계 및 다단계에서 트랜잭션 커밋
트랜잭션에 사용되는 각 리소스는 RM(리소스 관리자)에 의해 관리되고, RM의 작업은 TM(트랜잭션 관리자)에 의해 조정됩니다. [트랜잭션 항목에서 리소스를 참가자로 참여](enlisting-resources-as-participants-in-a-transaction.md) 항목은 리소스 (또는 여러 리소스)가 트랜잭션에 참여할 수 있는 방법에 대해 설명 합니다. 이 항목에서는 참여하는 리소스에서 트랜잭션 커밋을 조정하는 방법에 대해 설명합니다.  
  
 트랜잭션이 끝나면 애플리케이션이 트랜잭션을 커밋 또는 롤백하도록 요청합니다. 트랜잭션 관리자는 다른 리소스 관리자가 트랜잭션을 롤백하도록 응답하는 동안 일부 리소스 관리자가 커밋하도록 응답하는 경우와 같은 위험을 제거해야 합니다.  
  
 트랜잭션에 둘 이상의 리소스가 관련된 경우 2PC(2단계 커밋)를 수행해야 합니다. 2단계 커밋 프로토콜(준비 단계 및 커밋 단계)은 트랜잭션이 끝날 때 모든 리소스에 대한 모든 변경 내용이 함께 커밋 또는 롤백되도록 합니다. 그런 다음 모든 참가자에게 최종 결과를 알립니다. 2 단계 커밋 프로토콜에 대 한 자세한 내용은 "*트랜잭션 처리: 개념 및 기술 (데이터 관리 시스템의 Morgan kaufmann 시리즈) ISBN: 1558601902*"(승)  
  
 단일 단계 커밋 프로토콜에 참여하여 트랜잭션의 성능을 최적화할 수도 있습니다. 자세한 내용은 [단일 단계 커밋 및 승격 가능한 단일 단계 알림을 사용한 최적화](optimization-spc-and-promotable-spn.md)를 참조 하세요.  
  
 트랜잭션의 결과에 대한 알림만 받고 응답에 참여하지 않으려면 <xref:System.Transactions.Transaction.TransactionCompleted> 이벤트에 등록해야 합니다.  
  
## <a name="two-phase-commit-2pc"></a>2PC(2단계 커밋)  
 첫 번째 트랜잭션 단계에서는 트랜잭션 관리자가 각 리소스를 쿼리하여 트랜잭션을 커밋 또는 롤백할지 결정합니다. 두 번째 트랜잭션 단계에서는 트랜잭션 관리자가 각 리소스에 쿼리 결과를 알리고 필요한 정리 작업을 수행할 수 있게 합니다.  
  
 이러한 종류의 트랜잭션에 참여하려면 리소스 관리자가 <xref:System.Transactions.IEnlistmentNotification> 인터페이스를 구현해야 합니다. 이 인터페이스는 2PC 중에 TM에서 알림으로 호출되는 메서드를 제공합니다.  다음 코드 샘플에서는 이러한 구현 예를 보여 줍니다.  
  
 [!code-csharp[Tx_Enlist#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/tx_enlist/cs/enlist.cs#2)]
 [!code-vb[Tx_Enlist#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/tx_enlist/vb/enlist.vb#2)]  
  
### <a name="prepare-phase-phase-1"></a>준비 단계(1단계)  
 애플리케이션에서 <xref:System.Transactions.CommittableTransaction.Commit%2A> 요청을 받으면 트랜잭션 관리자는 트랜잭션에 대한 각 리소스의 응답을 얻기 위해 참여하는 각 리소스에서 <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> 메서드를 호출하여 참여하는 모든 참가자의 준비 단계를 시작합니다.  
  
 <xref:System.Transactions.IEnlistmentNotification> 인터페이스를 구현하는 리소스 관리자는 먼저 다음의 단순한 예제와 같이 <xref:System.Transactions.IEnlistmentNotification.Prepare%28System.Transactions.PreparingEnlistment%29>를 구현해야 합니다.  
  
```csharp
public void Prepare(PreparingEnlistment preparingEnlistment)  
{  
     Console.WriteLine("Prepare notification received");  
     //Perform work  
  
     Console.Write("reply with prepared? [Y|N] ");  
     c = Console.ReadKey();  
     Console.WriteLine();  
  
     //If work finished correctly, reply with prepared  
     if ((c.KeyChar == 'Y') || (c.KeyChar == 'y'))  
     {  
          preparingEnlistment.Prepared();  
          break;  
     }  
  
     // otherwise, do a ForceRollback  
     else if ((c.KeyChar == 'N') || (c.KeyChar == 'n'))  
     {  
          preparingEnlistment.ForceRollback();  
          break;  
     }  
}  
```  
  
 지속적인 리소스 관리자는 이 호출을 받을 경우 <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> 속성을 검색하여 얻을 수 있는 트랜잭션의 복구 정보와 커밋 시 트랜잭션을 완료하는 데 필요한 모든 정보를 기록해야 합니다. RM이 작업자 스레드에서 이 작업을 수행할 수 있으므로 <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> 메서드 내에서 이 작업을 수행할 필요는 없습니다.  
  
 RM은 준비 작업을 완료할 경우 <xref:System.Transactions.PreparingEnlistment.Prepared%2A> 또는 <xref:System.Transactions.PreparingEnlistment.ForceRollback%2A> 메서드를 호출하여 커밋 또는 롤백하도록 응답해야 합니다. <xref:System.Transactions.PreparingEnlistment> 클래스는 <xref:System.Transactions.Enlistment.Done%2A> 클래스에서 <xref:System.Transactions.Enlistment> 메서드를 상속합니다. 준비 단계 중에 <xref:System.Transactions.PreparingEnlistment> 콜백에서 이 메서드를 호출하면 메서드가 TM에 읽기 전용 인리스트먼트(즉, 트랜잭션에서 보호된 데이터를 읽을 수는 있지만 업데이트할 수 없는 리소스 관리자)임을 알리고 2단계의 트랜잭션 결과와 관련해서 RM이 트랜잭션 관리자로부터 더 이상 알림을 받지 않습니다.  
  
 모든 리소스 관리자가 <xref:System.Transactions.PreparingEnlistment.Prepared%2A>를 응답한 후 애플리케이션에 트랜잭션 커밋 성공을 알립니다.  
  
### <a name="commit-phase-phase-2"></a>커밋 단계(2단계)  
 트랜잭션의 두 번째 단계에서 트랜잭션 관리자는 모든 리소스 관리자로부터 준비 성공을 받을 경우(1단계가 끝날 때 모든 리소스 관리자가 <xref:System.Transactions.PreparingEnlistment.Prepared%2A>를 호출한 경우) 각 리소스 관리자에 대해 <xref:System.Transactions.IEnlistmentNotification.Commit%2A> 메서드를 호출합니다. 그런 다음 리소스 관리자가 변경 내용을 지속적으로 설정하고 커밋을 완료할 수 있습니다.  
  
 리소스 관리자가 1단계에서 준비 실패를 보고한 경우 트랜잭션 관리자는 각 리소스 관리자에 대해 <xref:System.Transactions.IEnlistmentNotification.Rollback%2A>을 호출하고 애플리케이션에 커밋 실패를 나타냅니다.  
  
 따라서 리소스 관리자는 다음 메서드를 구현해야 합니다.  
  
```csharp
public void Commit (Enlistment enlistment)  
{  
     // Do any work necessary when commit notification is received  
  
     // Declare done on the enlistment  
     enlistment.Done();  
}  
  
public void Rollback (Enlistment enlistment)  
{  
     // Do any work necessary when rollback notification is received  
  
     // Declare done on the enlistment    
     enlistment.Done();    
}  
```  
  
 RM은 알림 유형을 기반으로 트랜잭션을 끝내는 데 필요한 작업을 수행하고 <xref:System.Transactions.Enlistment.Done%2A> 매개 변수에서 <xref:System.Transactions.Enlistment> 메서드를 호출하여 트랜잭션이 끝났음을 TM에 알려야 합니다. 작업자 스레드에서 이 작업을 수행할 수 있습니다. 2단계 알림이 1단계에서 <xref:System.Transactions.PreparingEnlistment.Prepared%2A> 메서드를 호출한 스레드와 동일한 스레드에서 인라인으로 발생할 수 있습니다. 따라서 <xref:System.Transactions.PreparingEnlistment.Prepared%2A> 호출 후에는 잠금 해제를 비롯하여 2단계 알림을 받기 전에 끝내야 하는 어떤 작업도 수행하면 안 됩니다.  
  
### <a name="implementing-indoubt"></a>InDoubt 구현  
 마지막으로 일시적인 리소스 관리자에 대해 <xref:System.Transactions.IEnlistmentNotification.InDoubt%2A> 메서드를 구현해야 합니다. 이 메서드는 트랜잭션 관리자가 하나 이상의 참가자와 연결이 끊어져 해당 상태를 알 수 없는 경우에 호출됩니다. 이 경우 트랜잭션 참가자의 상태가 일치하지 않는지 나중에 조사할 수 있도록 이 사실을 기록해야 합니다.  
  
```csharp
public void InDoubt (Enlistment enlistment)  
{  
     // log this  
     enlistment.Done();  
}  
```  
  
## <a name="single-phase-commit-optimization"></a>단일 단계 커밋 최적화  
 단일 단계 커밋 프로토콜은 모든 업데이트가 명시적 코디네이션 없이 수행되므로 런타임에 보다 효율적입니다. 이 프로토콜에 대 한 자세한 내용은 [단일 단계 커밋 및 승격 가능한 단일 단계 알림을 사용한 최적화](optimization-spc-and-promotable-spn.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [단일 단계 커밋 및 승격 가능한 단일 단계 알림을 사용한 최적화](optimization-spc-and-promotable-spn.md)
- [리소스를 트랜잭션에 참가 요소로 등록](enlisting-resources-as-participants-in-a-transaction.md)
