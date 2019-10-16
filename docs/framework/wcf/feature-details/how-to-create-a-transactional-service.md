---
title: '방법: 트랜잭션 서비스 만들기'
ms.date: 03/30/2017
ms.assetid: 1bd2e4ed-a557-43f9-ba98-4c70cb75c154
ms.openlocfilehash: be364e7638394a30c199b05dd15ef4c44e18e688
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964013"
---
# <a name="how-to-create-a-transactional-service"></a>방법: 트랜잭션 서비스 만들기
이 샘플에서는 트랜잭션 서비스 만들기의 다양한 측면과 함께, 클라이언트에서 시작한 트랜잭션을 사용하여 서비스 작업을 조정하는 방법을 보여 줍니다.  
  
### <a name="creating-a-transactional-service"></a>트랜잭션 서비스 만들기  
  
1. 서비스 계약을 만들고 <xref:System.ServiceModel.TransactionFlowOption> 열거형에서 원하는 설정으로 작업에 주석을 달고 들어오는 트랜잭션의 요구 사항을 지정합니다. 구현 중인 서비스 클래스에도 <xref:System.ServiceModel.TransactionFlowAttribute>를 배치할 수 있습니다. 이렇게 하면 트랜잭션 설정을 모든 구현에서 사용하는 대신 단일 구현에서만 사용하게 됩니다.  
  
    ```csharp
    [ServiceContract]  
    public interface ICalculator  
    {  
        [OperationContract]  
        // Use this to require an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Mandatory)]  
        double Add(double n1, double n2);  
        [OperationContract]  
        // Use this to permit an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        double Subtract(double n1, double n2);  
    }  
    ```  
  
2. 구현 클래스를 만들고 <xref:System.ServiceModel.ServiceBehaviorAttribute>를 사용하여 필요한 경우 <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> 및 <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A>을 지정할 수 있습니다. 대부분의 경우 <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A>의 기본값은 60초, <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A>의 기본값은 `Unspecified`가 적절합니다. 각 작업에 대해 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성을 사용하여, 메서드 내에서 수행된 작업이 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 특성의 값에 따라 트랜잭션 범위 내에서 수행되어야 하는지 여부를 지정할 수 있습니다. 이 경우 `Add` 메서드에 사용된 트랜잭션은 클라이언트로부터 들어오는 필수 트랜잭션과 동일하며, `Subtract` 메서드에 사용된 트랜잭션은 트랜잭션이 클라이언트로부터 들어오는 경우 해당 트랜잭션과 동일하며, 그렇지 않은 경우 암시적으로 로컬에서 만들어진 새 트랜잭션과 동일합니다.  
  
    ```csharp
    [ServiceBehavior(  
        TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable,  
        TransactionTimeout = "00:00:45")]  
    public class CalculatorService : ICalculator  
    {  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog($"Adding {n1} to {n2}");
            return n1 + n2;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog($"Subtracting {n2} from {n1}");
            return n1 - n2;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
            // This is where the transaction provides specific benefit  
            // - changes to the database will be committed only when  
            // the transaction completes.  
        }  
    }  
    ```  
  
3. 트랜잭션 컨텍스트를 이동하도록 지정하고 이 작업에 사용할 프로토콜을 지정하여 구성 파일에서 바인딩을 구성합니다. 자세한 내용은 [ServiceModel 트랜잭션 구성](servicemodel-transaction-configuration.md)을 참조 하세요. 특히 바인딩 형식은 엔드포인트 요소의 `binding` 특성에서 지정합니다. 끝점 > 요소에는 다음 `bindingConfiguration` 샘플 구성에 표시 된 것과 `transactionalOleTransactionsTcpBinding`같이 이라는 바인딩 구성을 참조 하는 특성이 포함 되어 있습니다. [ \<](../../configure-apps/file-schema/wcf/endpoint-element.md)  
  
    ```xml  
    <service name="CalculatorService">  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     트랜잭션 흐름은 `transactionFlow` 특성을 사용하여 구성 수준에서 사용하도록 설정하며, 트랜잭션 프로토콜은 다음 구성에서처럼 `transactionProtocol` 특성을 사용하여 지정합니다.  
  
    ```xml  
    <bindings>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### <a name="supporting-multiple-transaction-protocols"></a>여러 트랜잭션 프로토콜 지원  
  
1. 최적의 성능을 위해 WCF (Windows Communication Foundation)를 사용 하 여 작성 된 클라이언트 및 서비스와 관련 된 시나리오에 OleTransactions 프로토콜을 사용 해야 합니다. 단, 타사 프로토콜 스택과의 상호 운용성이 필요한 시나리오의 경우에는 WS-AT(WS-AtomicTransaction) 프로토콜이 유용합니다. 다음 샘플 구성에 표시 된 것 처럼 적절 한 프로토콜 관련 바인딩으로 여러 끝점을 제공 하 여 두 프로토콜을 모두 허용 하도록 WCF 서비스를 구성할 수 있습니다.  
  
    ```xml  
    <service name="CalculatorService">  
      <endpoint address="http://localhost:8000/CalcService"  
        binding="wsHttpBinding"  
        bindingConfiguration="transactionalWsatHttpBinding"  
        contract="ICalculator"  
        name="WSAtomicTransaction_endpoint" />  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     트랜잭션 프로토콜은 `transactionProtocol` 특성을 사용하여 지정합니다. 그러나 이 바인딩에서는 WS-AT 프로토콜만 사용할 수 있으므로 이 특성은 시스템 제공 `wsHttpBinding`에 없습니다.  
  
    ```xml  
    <bindings>  
      <wsHttpBinding>  
        <binding name="transactionalWsatHttpBinding"  
          transactionFlow="true" />  
      </wsHttpBinding>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### <a name="controlling-the-completion-of-a-transaction"></a>트랜잭션 완료 제어  
  
1. 기본적으로 WCF 작업은 처리 되지 않은 예외가 throw 되지 않는 경우 트랜잭션을 자동으로 완료 합니다. <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> 속성 및 <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> 메서드를 사용하면 이 동작을 수정할 수 있습니다. debit 및 credit 연산 등 다른 연산과 동일한 트랜잭션 내에서 연산을 수행해야 하는 경우 다음 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> 연산 예제에서처럼 `false` 속성을 `Debit`로 설정하여 autocomplete 동작을 비활성화할 수 있습니다. `Debit` 연산에서 사용하는 트랜잭션은 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> 연산에서처럼 `true`로 설정된 `Credit1` 속성을 가진 메서드가 호출될 때까지 또는 <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> 연산에서처럼 트랜잭션 완료를 명시적으로 표시하기 위해 `Credit2` 메서드가 호출될 때까지 완료되지 않습니다. 설명의 목적으로 두 개의 credit 연산을 예로 들었지만 하나의 credit 연산이 보다 일반적입니다.  
  
    ```csharp
    [ServiceBehavior]  
    public class CalculatorService : IAccount  
    {  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Debit(double n)  
        {  
            // Perform debit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = true)]  
        public void Credit1(double n)  
        {  
            // Perform credit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Credit2(double n)  
        {  
            // Perform alternate credit operation  
  
            OperationContext.Current.SetTransactionComplete();  
            return;  
        }  
    }  
    ```  
  
2. 트랜잭션의 상관 관계를 위해 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> 속성을 `false`로 설정하려면 세션 바인딩을 사용해야 합니다. 이 요구 사항은 `SessionMode`의 <xref:System.ServiceModel.ServiceContractAttribute> 속성을 사용하여 지정합니다.  
  
    ```csharp
    [ServiceContract(SessionMode = SessionMode.Required)]  
    public interface IAccount  
    {  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Debit(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit1(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit2(double n);  
    }  
    ```  
  
### <a name="controlling-the-lifetime-of-a-transactional-service-instance"></a>트랜잭션 서비스 인스턴스의 수명 제어  
  
1. WCF는 <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> 속성을 사용 하 여 트랜잭션이 완료 될 때 기본 서비스 인스턴스가 해제 되는지 여부를 지정 합니다. 이는 기본적으로 `true`로 구성 되지 않은 한, 달리 구성 되지 않은 경우 WCF는 효율적이 고 예측 가능한 "just-in-time" 활성화 동작을 보여 주므로 후속 트랜잭션에서의 서비스에 대한 호출은 이전 트랜잭션 상태가 남아 있지 않은 새 서비스 인스턴스가 됩니다. 이는 대개의 경우에 유용하지만 때로는 트랜잭션 완료와 관계없이 서비스 인스턴스 내의 상태를 유지해야 하는 경우가 있습니다. 예를 들면 필요한 상태 또는 리소스에 대한 핸들을 검색하거나 다시 구성하는 데 비용이 많이 드는 경우입니다. <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> 속성을 `false`로 설정하면 서비스 인스턴스 내의 상태를 유지할 수 있습니다. 이렇게 설정하면 인스턴스 및 그와 관련된 모든 상태를 후속 호출에서 사용할 수 있습니다. 이 설정을 사용하는 경우에는 상태 및 트랜잭션을 지우고 완료하는 시기와 방법에 대해 주의 깊게 고려해야 합니다. 다음 샘플에서는 `runningTotal` 변수를 사용하여 인스턴스를 유지 관리함으로써 이 작업을 수행하는 방법을 보여 줍니다.  
  
    ```csharp
    [ServiceBehavior(TransactionIsolationLevel = [ServiceBehavior(  
        ReleaseServiceInstanceOnTransactionComplete = false)]  
    public class CalculatorService : ICalculator  
    {  
        double runningTotal = 0;  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n)  
        {  
            // Perform transactional operation  
            RecordToLog($"Adding {n} to {runningTotal}");
            runningTotal = runningTotal + n;  
            return runningTotal;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n)  
        {  
            // Perform transactional operation  
            RecordToLog($"Subtracting {n} from {runningTotal}");
            runningTotal = runningTotal - n;  
            return runningTotal;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
        }  
    }  
    ```  
  
    > [!NOTE]
    > 인스턴스 수명이 서비스의 내부 동작이며 <xref:System.ServiceModel.ServiceBehaviorAttribute> 속성을 통해 제어되므로, 인스턴스 동작을 설정하기 위해 서비스 구성이나 서비스 계약을 수정할 필요가 없습니다. 또한 연결에도 이에 대한 표현이 포함되지 않습니다.
