---
title: 동시성
ms.date: 03/30/2017
helpviewer_keywords:
- service behaviors, concurency sample
- Concurrency Sample [Windows Communication Foundation]
ms.assetid: f8dbdfb3-6858-4f95-abe3-3a1db7878926
ms.openlocfilehash: 3a78612f679218711a81278184c16b04d6d6f802
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045673"
---
# <a name="concurrency"></a>동시성
Concurrency 샘플에서는 <xref:System.ServiceModel.ServiceBehaviorAttribute> 열거와 함께 <xref:System.ServiceModel.ConcurrencyMode>를 사용하여 서비스 인스턴스가 메시지를 순차적으로 처리하는지, 동시에 처리하는지를 제어하는 방법을 보여 줍니다. 이 샘플은 `ICalculator` 서비스 계약을 구현 하는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다. 이 샘플에서는 `ICalculatorConcurrency`에서 상속되는 새 계약 `ICalculator`를 정의하여 서비스 동시성의 상태를 검사하는 두 가지 추가 작업을 제공합니다. 동시성 설정을 변경하여 클라이언트를 실행하면 동작의 변화를 확인할 수 있습니다.  
  
 이 샘플에서 클라이언트는 콘솔 응용 프로그램(.exe)이고 서비스는 IIS(인터넷 정보 서비스)를 통해 호스트됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 다음과 같은 세 가지 동시성 모드를 사용할 수 있습니다.  
  
- `Single`: 각 서비스 인스턴스는 한 번에 하나의 메시지를 처리 합니다. 이 모드가 기본 동시성 모드입니다.  
  
- `Multiple`: 각 서비스 인스턴스는 여러 메시지를 동시에 처리 합니다. 이 동시성 모드를 사용하려면 스레드로부터 안전하게 서비스를 구현해야 합니다.  
  
- `Reentrant`: 각 서비스 인스턴스는 한 번에 하나의 메시지를 처리 하지만 재진입 호출을 허용 합니다. 서비스는 호출되는 경우에만 이러한 호출을 허용합니다. 재진입은 [ConcurrencyMode](../../../../docs/framework/wcf/samples/concurrencymode-reentrant.md) 샘플에서 보여 줍니다.  
  
 동시성 사용은 인스턴스 만들기 모드와 관련됩니다. <xref:System.ServiceModel.InstanceContextMode.PerCall> 인스턴스 만들기에서는 각 메시지가 새 서비스 인스턴스에 의해 처리되므로 동시성이 관련되지 않습니다. <xref:System.ServiceModel.InstanceContextMode.Single> 인스턴스 만들기에서는 단일 인스턴스에서 메시지를 순차적으로 처리하는지, 동시에 처리하는지에 따라 <xref:System.ServiceModel.ConcurrencyMode.Single> 또는 <xref:System.ServiceModel.ConcurrencyMode.Multiple> 동시성이 관련됩니다. <xref:System.ServiceModel.InstanceContextMode.PerSession> 인스턴스 만들기에서는 모든 동시성 모드가 관련될 수 있습니다.  
  
 서비스 클래스에서는 다음 코드 샘플과 같이 `[ServiceBehavior(ConcurrencyMode=<setting>)]` 특성을 사용하여 동시성 동작을 지정합니다. 주석으로 처리할 줄을 변경하면 `Single` 및 `Multiple` 동시성 모드를 테스트할 수 있습니다. 동시성 모드를 변경한 후에는 서비스를 다시 빌드해야 합니다.  
  
```csharp
// Single allows a single message to be processed sequentially by each service instance.  
//[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Single, InstanceContextMode = InstanceContextMode.Single)]  
  
// Multiple allows concurrent processing of multiple messages by a service instance.  
// The service implementation should be thread-safe. This can be used to increase throughput.  
[ServiceBehavior(ConcurrencyMode=ConcurrencyMode.Multiple, InstanceContextMode = InstanceContextMode.Single)]  
  
// Uses Thread.Sleep to vary the execution time of each operation.  
public class CalculatorService : ICalculatorConcurrency  
{  
    int operationCount;  
  
    public double Add(double n1, double n2)  
    {  
        operationCount++;  
        System.Threading.Thread.Sleep(180);  
        return n1 + n2;  
    }  
  
    public double Subtract(double n1, double n2)  
    {  
        operationCount++;  
        System.Threading.Thread.Sleep(100);  
        return n1 - n2;  
    }  
  
    public double Multiply(double n1, double n2)  
    {  
        operationCount++;  
        System.Threading.Thread.Sleep(150);  
        return n1 * n2;  
    }  
  
    public double Divide(double n1, double n2)  
    {  
        operationCount++;  
        System.Threading.Thread.Sleep(120);  
        return n1 / n2;  
    }  
  
    public string GetConcurrencyMode()  
    {     
        // Return the ConcurrencyMode of the service.  
        ServiceHost host = (ServiceHost)OperationContext.Current.Host;  
        ServiceBehaviorAttribute behavior = host.Description.Behaviors.Find<ServiceBehaviorAttribute>();  
        return behavior.ConcurrencyMode.ToString();  
    }  
  
    public int GetOperationCount()  
    {     
        // Return the number of operations.  
        return operationCount;  
    }  
}  
```  
  
 기본적으로 이 샘플에서는 <xref:System.ServiceModel.ConcurrencyMode.Multiple> 인스턴스 만들기에 <xref:System.ServiceModel.InstanceContextMode.Single> 동시성을 사용합니다. 비동기 프록시를 사용하도록 클라이언트 코드가 수정되었습니다. 따라서 클라이언트는 각 호출 사이에서 응답을 기다리지 않고 서비스를 여러 번 호출할 수 있습니다. 서비스 동시성 모드 동작의 차이를 확인할 수 있습니다.  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 서비스가 실행되는 동시성 모드가 표시되고 각 작업이 호출된 다음 작업 카운트가 표시됩니다. 동시성 모드가 `Multiple`이면 서비스에서 여러 메시지를 동시에 처리하므로 메시지가 호출된 방식과 다른 순서로 결과가 반환됩니다. 동시성 모드를 `Single`로 변경하면 서비스에서 각 메시지를 순차적으로 처리하므로 메시지가 호출된 순서대로 결과가 반환됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. Svcutil.exe를 사용 하 여 프록시 클라이언트를 생성 하는 경우 `/async` 옵션을 포함 해야 합니다.  
  
3. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
4. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Concurrency`  
