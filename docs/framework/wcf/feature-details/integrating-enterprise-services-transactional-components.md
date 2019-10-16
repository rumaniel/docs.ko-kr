---
title: 엔터프라이즈 서비스 트랜잭션 구성 요소 통합
ms.date: 03/30/2017
ms.assetid: 05dab277-b8b2-48cf-b40c-826be128b175
ms.openlocfilehash: c73be31bef67f1de818f7b04181a3540bbd7caa8
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991543"
---
# <a name="integrating-enterprise-services-transactional-components"></a>엔터프라이즈 서비스 트랜잭션 구성 요소 통합
WCF (Windows Communication Foundation)는 엔터프라이즈 서비스와 통합 하기 위한 자동 메커니즘을 제공 합니다 ( [COM + 응용 프로그램과 통합](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)참조). 하지만 엔터프라이즈 서비스에 호스팅된 트랜잭션 구성 요소를 내부적으로 사용하는 서비스를 개발하기 위한 유연성이 필요할 수 있습니다. Wcf 트랜잭션 기능은 <xref:System.Transactions> 인프라를 기반으로 하기 때문에, 엔터프라이즈 서비스와 wcf를 통합 하는 프로세스는 다음에 설명 된 대로 및 <xref:System.Transactions> 엔터프라이즈 서비스 간의 상호 운용성을 지정 하는 프로세스와 동일 합니다. [엔터프라이즈 서비스 및 COM + 트랜잭션과의 상호 운용성](https://go.microsoft.com/fwlink/?LinkId=94949)  
  
 들어오는 흐름의 트랜잭션과 COM+ 컨텍스트 트랜잭션 간에 필요한 수준의 상호 운용성을 제공하려면 서비스 구현에서 <xref:System.Transactions.TransactionScope> 인스턴스를 만들고 적절한 <xref:System.Transactions.EnterpriseServicesInteropOption> 열거형 값을 사용해야 합니다.  
  
## <a name="integrating-enterprise-services-with-a-service-operation"></a>엔터프라이즈 서비스와 서비스 작업 통합  
 다음 코드에서는 <xref:System.Transactions.TransactionScope> 옵션으로 <xref:System.Transactions.EnterpriseServicesInteropOption.Full>을 만드는 트랜잭션 흐름이 Allowed인 작업을 보여 줍니다. 이 시나리오에는 다음 조건이 적용됩니다.  
  
- 클라이언트에서 트랜잭션을 이동하면 엔터프라이즈 서비스 구성 요소 호출을 비롯한 작업이 해당 트랜잭션 범위 내에서 실행됩니다. <xref:System.Transactions.EnterpriseServicesInteropOption.Full>을 사용하면 트랜잭션이 <xref:System.EnterpriseServices> 컨텍스트와 동기화되어 <xref:System.Transactions>에 대한 앰비언트 트랜잭션과 <xref:System.EnterpriseServices>가 같게 됩니다.  
  
- 클라이언트에서 트랜잭션을 이동하지 않을 때 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A>를 `true`로 설정하면 작업에 대한 새 트랜잭션 범위가 만들어집니다. 마찬가지로 <xref:System.Transactions.EnterpriseServicesInteropOption.Full>을 사용하면 작업의 트랜잭션이 <xref:System.EnterpriseServices> 구성 요소의 컨텍스트 내부에 사용되는 트랜잭션과 같게 됩니다.  
  
 동일한 작업의 트랜잭션 범위 내에서는 추가적인 메서드 호출도 발생합니다.  
  
```csharp
[ServiceContract()]  
public interface ICustomerServiceContract  
{  
   [OperationContract]  
   [TransactionFlow(TransactionFlowOption.Allowed)]  
   void UpdateCustomerNameOperation(int customerID, string newCustomerName);  
}  
  
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CustomerService : ICustomerServiceContract  
{  
   [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
   public void UpdateCustomerNameOperation(int customerID, string newCustomerName)  
   {  
   // Create a transaction scope with full ES interop  
      using (TransactionScope ts = new TransactionScope(  
                     TransactionScopeOption.Required,  
                     new TransactionOptions(),  
                     EnterpriseServicesInteropOption.Full))  
      {  
         // Create an Enterprise Services component  
         // Call UpdateCustomer method on an Enterprise Services   
         // component   
  
         // Call UpdateOtherCustomerData method on an Enterprise   
         // Services component   
         ts.Complete();  
      }  
  
      // Do UpdateAdditionalData on an non-Enterprise Services  
      // component  
   }  
}  
```  
  
 작업의 현재 트랜잭션과 트랜잭션 엔터프라이즈 서비스 구성 요소 호출 간에 동기화가 필요하지 않을 때에는 <xref:System.Transactions.EnterpriseServicesInteropOption.None> 인스턴스를 인스턴스화할 때 <xref:System.Transactions.TransactionScope> 옵션을 사용합니다.  
  
## <a name="integrating-enterprise-services-with-a-client"></a>엔터프라이즈 서비스와 클라이언트 통합  
 다음 코드에서는 <xref:System.Transactions.TransactionScope> 설정 상태인 <xref:System.Transactions.EnterpriseServicesInteropOption.Full>인스턴스를 사용하는 클라이언트 코드를 보여줍니다. 이 시나리오에서 트랜잭션 흐름을 지원하는 서비스 작업에 대한 호출은 엔터프라이즈 서비스 구성 요소 호출과 동일한 트랜잭션 범위 내에서 발생합니다.  
  
```csharp
static void Main()  
{  
    // Create a client  
    CalculatorClient client = new CalculatorClient();  
  
    // Create a transaction scope with full ES interop  
    using (TransactionScope ts = new TransactionScope(  
          TransactionScopeOption.Required,  
          new TransactionOptions(),  
          EnterpriseServicesInteropOption.Full))  
    {  
        // Call Add calculator service operation  
  
        // Create an Enterprise Services component  
  
        // Call UpdateCustomer method on an Enterprise Services   
        // component   
  
        ts.Complete();  
    }  
  
    // Closing the client gracefully closes the connection and   
    // cleans up resources  
    client.Close();  
}  
```  
  
## <a name="see-also"></a>참고자료

- [COM+ 애플리케이션과 통합](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)
- [COM 애플리케이션과 통합](../../../../docs/framework/wcf/feature-details/integrating-with-com-applications.md)
