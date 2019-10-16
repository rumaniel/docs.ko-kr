---
title: 서비스 및 트랜잭션
ms.date: 03/30/2017
helpviewer_keywords:
- service contracts [WCF], designing services and transactions
ms.assetid: 864813ff-2709-4376-912d-f5c8d318c460
ms.openlocfilehash: 9dfe34406bfda2c16bd2f0cd53796b2fcef07b57
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61967923"
---
# <a name="services-and-transactions"></a>서비스 및 트랜잭션
Windows Communication Foundation (WCF) 응용 프로그램 클라이언트 내에서 트랜잭션을 시작 하 고 서비스 작업 내에서 트랜잭션을 조정할 수 있습니다. 클라이언트는 트랜잭션을 초기화하고 여러 서비스 작업을 호출하며 서비스 작업이 하나의 단위로 커밋되는지 또는 롤백되는지 확인합니다.  
  
 클라이언트 트랜잭션이 필요한 서비스 작업에 대해 <xref:System.ServiceModel.ServiceBehaviorAttribute>를 지정하고 해당 <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> 및 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 속성을 설정하여 서비스 계약에 트랜잭션 동작을 사용하도록 설정할 수 있습니다. <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> 매개 변수는 처리되지 않은 예외가 throw되지 않을 경우 메서드가 실행하는 트랜잭션을 자동으로 완료할지 여부를 지정합니다. 이러한 특성에 대 한 자세한 내용은 참조 하세요. [ServiceModel 트랜잭션 특성](../../../docs/framework/wcf/feature-details/servicemodel-transaction-attributes.md)합니다.  
  
 데이터베이스 업데이트 기록처럼 서비스 작업에서 수행되고 리소스 관리자가 관리하는 작업은 클라이언트의 트랜잭션에 포함됩니다.  
  
 다음 샘플에서는 <xref:System.ServiceModel.ServiceBehaviorAttribute> 및 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성을 사용하여 서비스 측 트랜잭션 동작을 제어하는 방법을 보여 줍니다.  
  
```csharp
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CalculatorService: ICalculatorLog  
{  
    [OperationBehavior(TransactionScopeRequired = true,  
                           TransactionAutoComplete = true)]  
    public double Add(double n1, double n2)  
    {  
        recordToLog($"Added {n1} to {n2}");
        return n1 + n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,   
                               TransactionAutoComplete = true)]  
    public double Subtract(double n1, double n2)  
    {  
        recordToLog($"Subtracted {n1} from {n2}");
        return n1 - n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,   
                                       TransactionAutoComplete = true)]  
    public double Multiply(double n1, double n2)  
    {  
        recordToLog($"Multiplied {n1} by {n2}");
        return n1 * n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,   
                                       TransactionAutoComplete = true)]  
    public double Divide(double n1, double n2)  
    {  
        recordToLog($"Divided {n1} by {n2}", n1, n2);
        return n1 / n2;  
    }  
  
}  
```  
  
 트랜잭션을 설정할 수 있으며 트랜잭션 클라이언트를 구성 하 여 흐름 및 WS-AtomicTransaction 프로토콜을 사용 하는 바인딩 및 설정을 서비스는 [ \<transactionFlow >](../../../docs/framework/configure-apps/file-schema/wcf/transactionflow.md) 요소를 `true`표시 된 것 처럼 다음 샘플 구성 합니다.  
  
```xml  
<client>  
    <endpoint address="net.tcp://localhost/ServiceModelSamples/service"   
          binding="netTcpBinding"   
          bindingConfiguration="netTcpBindingWSAT"   
          contract="Microsoft.ServiceModel.Samples.ICalculatorLog" />  
</client>  
  
<bindings>  
    <netTcpBinding>  
        <binding name="netTcpBindingWSAT"  
                transactionFlow="true"  
                transactionProtocol="WSAtomicTransactionOctober2004" />  
     </netTcpBinding>  
</bindings>  
```  
  
 클라이언트는 <xref:System.Transactions.TransactionScope>를 만들고 트랜잭션 범위 내에서 서비스 작업을 호출하여 트랜잭션을 시작할 수 있습니다.  
  
```csharp
using (TransactionScope ts = new TransactionScope(TransactionScopeOption.RequiresNew))  
{  
    //Do work here  
    ts.Complete();  
}  
```  
  
## <a name="see-also"></a>참고자료

- [System.ServiceModel의 트랜잭션 지원](../../../docs/framework/wcf/feature-details/transactional-support-in-system-servicemodel.md)
- [트랜잭션 모델](../../../docs/framework/wcf/feature-details/transaction-models.md)
- [WS 트랜잭션 흐름](../../../docs/framework/wcf/samples/ws-transaction-flow.md)
