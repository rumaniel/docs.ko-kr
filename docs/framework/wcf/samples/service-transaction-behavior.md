---
title: 서비스 트랜잭션 동작
ms.date: 03/30/2017
helpviewer_keywords:
- Service Transaction Behavior Sample [Windows Communication Foundation]
ms.assetid: 1a9842a3-e84d-427c-b6ac-6999cbbc2612
ms.openlocfilehash: bfdf0c9ddb8654bf7a6736bcccb0d9350e9a12a6
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198473"
---
# <a name="service-transaction-behavior"></a>서비스 트랜잭션 동작
이 샘플에서는 클라이언트에서 조정하는 트랜잭션과 ServiceBehaviorAttribute 및 OperationBehaviorAttribute의 설정을 사용하여 서비스 트랜잭션 동작을 제어하는 방법을 보여 줍니다. 이 샘플은 기반 합니다 [Getting Started](../../../../docs/framework/wcf/samples/getting-started-sample.md) 계산기 서비스를 구현 하는 동시 데이터베이스 테이블에서 상태 저장 계산기 작업에 대 한 누계에 수행된 된 작업의 서버 로그를 유지 하기 위해 확장 됩니다. 서버 로그 테이블에 대한 지속적인 쓰기는 클라이언트에서 조정하는 트랜잭션의 결과에 영향을 받습니다. 즉, 클라이언트 트랜잭션이 완료되지 않은 경우 웹 서비스 트랜잭션은 데이터베이스의 업데이트가 커밋되지 않도록 합니다.  
  
> [!NOTE]
>  이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 다음 서비스 계약에서는 모든 작업을 수행하려면 트랜잭션이 요청과 함께 이동해야 한다고 정의하고 있습니다.  
  
```csharp
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples",  
                    SessionMode = SessionMode.Required)]  
public interface ICalculator  
{  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Add(double n);  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Subtract(double n);  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Multiply(double n);  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Divide(double n);  
}  
```  
  
 들어오는 트랜잭션 흐름을 사용하도록 설정하기 위해 서비스는 transactionFlow 특성이 `true`로 설정된 시스템 제공 wsHttpBinding으로 구성됩니다. 이 바인딩은 상호 운용 가능한 WSAtomicTransactionOctober2004 프로토콜을 사용합니다.  
  
```xml  
<bindings>  
  <wsHttpBinding>  
    <binding name="transactionalBinding" transactionFlow="true" />  
  </wsHttpBinding>  
</bindings>  
```  
  
 서비스와 트랜잭션에 대한 연결을 모두 시작한 후에 클라이언트는 이 트랜잭션 범위 내의 몇몇 서비스 작업에 액세스한 다음 트랜잭션을 완료하고 연결을 닫습니다.  
  
```csharp
// Create a client  
CalculatorClient client = new CalculatorClient();  
  
// Create a transaction scope with the default isolation level of Serializable  
using (TransactionScope tx = new TransactionScope())  
{  
    Console.WriteLine("Starting transaction");  
  
    // Call the Add service operation.  
    double value = 100.00D;  
    Console.WriteLine("  Adding {0}, running total={1}",  
                                        value, client.Add(value));  
  
    // Call the Subtract service operation.  
    value = 45.00D;  
    Console.WriteLine("  Subtracting {0}, running total={1}",  
                                        value, client.Subtract(value));  
  
    // Call the Multiply service operation.  
    value = 9.00D;  
    Console.WriteLine("  Multiplying by {0}, running total={1}",  
                                        value, client.Multiply(value));  
  
    // Call the Divide service operation.  
    value = 15.00D;  
    Console.WriteLine("  Dividing by {0}, running total={1}",  
                                        value, client.Divide(value));  
  
    Console.WriteLine("  Completing transaction");  
    tx.Complete();  
}  
  
Console.WriteLine("Transaction committed");  
  
// Closing the client gracefully closes the connection and cleans up resources  
client.Close();  
```  
  
 서비스에는 서비스 트랜잭션 동작에 영향을 주는 세 가지 특성이 있으며 영향을 주는 방식은 다음과 같습니다.  
  
-   `ServiceBehaviorAttribute`:  
  
    -   `TransactionTimeout` 속성은 트랜잭션을 완료해야 하는 시간을 지정합니다. 이 샘플에서는 30초로 설정되어 있습니다.  
  
    -   `TransactionIsolationLevel` 속성은 서비스가 지원하는 격리 수준을 지정합니다. 이 속성은 클라이언트의 격리 수준을 일치시키는 데 필요합니다.  
  
    -   `ReleaseServiceInstanceOnTransactionComplete` 속성은 트랜잭션이 완료될 때 서비스 인스턴스를 재활용할지 여부를 지정합니다. 이 속성을 `false`로 설정하면 서비스는 전체 작업 요청에 대해 동일한 서비스 인스턴스를 유지합니다. 이 설정은 누계를 유지 관리하는 데 필요합니다. 이 속성을 `true`로 설정하면 각 작업이 완료된 후에 새 인스턴스가 생성됩니다.  
  
    -   `TransactionAutoCompleteOnSessionClose` 속성에서는 세션을 닫을 때 처리되지 않은 트랜잭션을 완료할 것인지 여부를 지정합니다. 로 설정 하 여 `false`, 개별 작업을 설정 하는 데 필요한 합니다 `OperationBehaviorAttribute``TransactionAutoComplete` 속성을 `true` 또는 명시적으로 호출을 요구 하는 `SetTransactionComplete` 거래를 완료 하는 방법. 이 샘플에서는 두 가지 접근 방식을 모두 보여 줍니다.  
  
-   `ServiceContractAttribute`:  
  
    -   `SessionMode` 속성은 서비스가 적절한 요청을 논리 세션에 상호 연결시킬지 여부를 지정합니다. 이 서비스에는 OperationBehaviorAttribute TransactionAutoComplete 속성이 `false`로 설정된 작업(Multiply 및 Divide)이 포함되기 때문에 `SessionMode.Required`를 지정해야 합니다. 예를 들어 Multiply 작업은 트랜잭션을 완료하는 대신 `SetTransactionComplete` 메서드를 사용하여 완료할 Divide에 대한 이후의 호출에 의존합니다. 서비스는 이러한 작업이 동일한 세션 내에서 발생하는지 확인할 수 있어야 합니다.  
  
-   `OperationBehaviorAttribute`:  
  
    -   `TransactionScopeRequired` 속성은 작업의 동작이 트랜잭션 범위 내에서 실행되어야 하는지 여부를 지정합니다. 이 속성은 이 샘플의 모든 작업에 대해 `true`로 설정되며, 클라이언트는 해당 트랜잭션을 모든 작업으로 이동하므로 동작은 해당 클라이언트 트랜잭션의 범위 내에서 발생합니다.  
  
    -   `TransactionAutoComplete` 속성은 처리되지 않은 예외가 발생하지 않는 경우 메서드가 실행되는 트랜잭션을 자동으로 완료할지 여부를 지정합니다. 이전에 설명한 대로 이 속성은 Add 및 Subtract 작업에 대해 `true`로 설정되지만 Multiply 및 Divide 작업에 대해서는 `false`로 설정됩니다. Add 및 Subtract 작업은 자동으로 동작을 완료하고, Divide는 `SetTransactionComplete` 메서드에 대한 명시적 호출을 통해 동작을 완료하며, Multiply는 동작을 완료하는 대신 Divide와 같은 이후의 호출에 의존하고 요청하여 동작을 완료합니다.  
  
 특성을 사용하는 서비스 구현은 다음과 같습니다.  
  
```csharp
[ServiceBehavior(  
    TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable,  
    TransactionTimeout = "00:00:30",  
    ReleaseServiceInstanceOnTransactionComplete = false,  
    TransactionAutoCompleteOnSessionClose = false)]  
public class CalculatorService : ICalculator  
{  
    double runningTotal;  
  
    public CalculatorService()  
    {  
        Console.WriteLine("Creating new service instance...");  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
    public double Add(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Adding {0} to {1}", n, runningTotal));  
        runningTotal = runningTotal + n;  
        return runningTotal;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
    public double Subtract(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Subtracting {0} from {1}", n, runningTotal));  
        runningTotal = runningTotal - n;  
        return runningTotal;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = false)]  
    public double Multiply(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Multiplying {0} by {1}", runningTotal, n));  
        runningTotal = runningTotal * n;  
        return runningTotal;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = false)]  
    public double Divide(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Dividing {0} by {1}", runningTotal, n));  
        runningTotal = runningTotal / n;  
        OperationContext.Current.SetTransactionComplete();  
        return runningTotal;  
    }  
  
    // Logging method ommitted for brevity  
}   
```  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```console  
Starting transaction  
Performing calculations...  
  Adding 100, running total=100  
  Subtracting 45, running total=55  
  Multiplying by 9, running total=495  
  Dividing by 15, running total=33  
  Completing transaction  
Transaction committed  
Press <ENTER> to terminate client.  
```  
  
 서비스 작업 요청의 로깅은 서비스의 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```console  
Press <ENTER> to terminate service.  
Creating new service instance...  
  Writing row 1 to database: Adding 100 to 0  
  Writing row 2 to database: Subtracting 45 from 100  
  Writing row 3 to database: Multiplying 55 by 9  
  Writing row 4 to database: Dividing 495 by 15  
```  
  
 서비스는 계산의 누계를 유지하는 것 외에도 인스턴스 만들기를 보고하고(이 샘플의 경우 인스턴스 하나) 작업 요청을 데이터베이스에 기록합니다. 모든 요청이 클라이언트의 트랜잭션으로 이동하기 때문에 트랜잭션을 완료하지 못하면 모든 데이터베이스 작업이 롤백됩니다. 이에 대해서는 다음과 같은 여러 가지 방법을 통해 설명할 수 있습니다.  
  
-   `tx.Complete`()에 대한 클라이언트의 호출을 주석으로 처리하고 다시 실행 - 그러면 클라이언트가 트랜잭션을 완료하지 않고 트랜잭션 범위를 끝냅니다.  
  
-   Divide 서비스 작업에 대한 호출을 주석으로 처리 - 그러면 Multiply 작업에서 시작된 작업이 완료되지 못하고 결과적으로 클라이언트의 트랜잭션도 완료되지 못합니다.  
  
-   클라이언트의 트랜잭션 범위 내 임의의 위치에서 처리되지 않은 예외 throw - 마찬가지로 클라이언트가 트랜잭션을 완료하지 못합니다.  
  
 이 중 어느 방법을 사용해도 해당 범위 내에서 수행된 작업이 커밋되지 않으며 데이터베이스와 연결된 행 수가 증가하지 않습니다.  
  
> [!NOTE]
>  빌드 프로세스의 일부로 데이터베이스 파일이 bin 폴더에 복사됩니다. 데이터베이스 파일의 이 복사본을 확인하여 Visual Studio 프로젝트에 포함된 파일이 아닌 로그와 관련된 행을 살펴보아야 합니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1.  SQL Server 2005 Express Edition 또는 SQL Server 2005를 설치했는지 확인합니다. 서비스의 App.config 파일에서 데이터베이스 `connectionString` 을 설정하거나 appSettings `usingSql` 값을 `false`로 설정하여 데이터베이스 상호 작용을 비활성화할 수 있습니다.  
  
2.  C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3.  단일 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)합니다.  
  
 컴퓨터에서 샘플을 실행 하는 MSDTC Microsoft Distributed Transaction Coordinator () 네트워크 트랜잭션 흐름을 사용 하 여 WsatConfig.exe 도구를 사용 하 여 Windows Communication Foundation (WCF) 트랜잭션이 네트워크를 사용 하도록 설정 하려면 구성 해야 합니다. 이 옵션을 지원 합니다.  
  
### <a name="to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-to-support-running-the-sample-across-machines"></a>여러 컴퓨터에서 샘플을 실행할 수 있도록 MSDTC(Microsoft Distributed Transaction Coordinator)를 구성하려면  
  
1.  서비스 컴퓨터에서 들어오는 네트워크 트랜잭션을 허용하도록 MSDTC를 구성합니다.  
  
    1.  **시작** 메뉴에서 이동할 **제어판**, 다음 **관리 도구**를 차례로 **구성 요소 서비스**.  
  
    2.  마우스 오른쪽 단추로 클릭 **내 컴퓨터** 선택한 **속성**합니다.  
  
    3.  에 **MSDTC** 탭을 클릭 **보안 구성**합니다.  
  
    4.  확인할 **네트워크 DTC 액세스** 하 고 **허용 인바운드**합니다.  
  
    5.  클릭 **Yes** MS DTC 서비스를 다시 시작을 클릭 한 다음 **확인**합니다.  
  
    6.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
2.  서비스 컴퓨터와 클라이언트 컴퓨터에서 예외 응용 프로그램 목록에 Microsoft Distributed Transaction Coordinator(MSDTC)가 포함되도록 Windows 방화벽을 구성합니다.  
  
    1.  제어판에서 Windows 방화벽 응용 프로그램을 실행합니다.  
  
    2.  **예외** 탭을 클릭 **추가 프로그램**합니다.  
  
    3.  C:\WINDOWS\System32 폴더로 이동합니다.  
  
    4.  Msdtc.exe를 선택 하 고 클릭 **열려**합니다.  
  
    5.  클릭 **확인** 닫으려면 합니다 **프로그램 추가** 대화 상자를 클릭 **확인** Windows 방화벽 애플릿을 닫습니다를 다시 합니다.  
  
3.  클라이언트 컴퓨터에서 나가는 네트워크 트랜잭션을 허용하도록 MSDTC를 구성합니다.  
  
    1.  **시작** 메뉴에서 이동할 **제어판**, 다음 **관리 도구**를 차례로 **구성 요소 서비스**.  
  
    2.  마우스 오른쪽 단추로 클릭 **내 컴퓨터** 선택한 **속성**합니다.  
  
    3.  에 **MSDTC** 탭을 클릭 **보안 구성**합니다.  
  
    4.  확인할 **네트워크 DTC 액세스** 하 고 **아웃 바운드 허용**합니다.  
  
    5.  클릭 **Yes** MS DTC 서비스를 다시 시작을 클릭 한 다음 **확인**합니다.  
  
    6.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Transactions`  
  
## <a name="see-also"></a>참고 항목
