---
title: 기본 서비스 동작
ms.date: 03/30/2017
helpviewer_keywords:
- service behaviors, defaults
- Default Service Behavior Sample [Windows Communication Foundation]
ms.assetid: 442d4f71-c64e-4c62-816a-a66c38e7d3ec
ms.openlocfilehash: 3728d9808eb0ad90d24a894b18857e414906f9f3
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045033"
---
# <a name="default-service-behavior"></a>기본 서비스 동작
이 샘플에서는 서비스 동작 설정을 구성하는 방법을 보여 줍니다. 이 샘플은 `ICalculator` 서비스 계약을 구현 하는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다. 이 샘플에서는 <xref:System.ServiceModel.ServiceBehaviorAttribute> 및 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성을 사용하여 서비스 동작 및 작업 동작을 명시적으로 정의합니다. 동작은 구성 파일에서 구성할 수도 있고 코드에서 명령적으로 구성할 수도 있습니다. 이 샘플에서는 코드에서 명령적으로 구성하는 방법을 보여 줍니다.  
  
 이 샘플에서 클라이언트는 콘솔 응용 프로그램(.exe)이고 서비스는 IIS(인터넷 정보 서비스)를 통해 호스트됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 서비스 클래스에서는 다음 코드 샘플에 표시된 것과 같이 <xref:System.ServiceModel.ServiceBehaviorAttribute> 및 <xref:System.ServiceModel.OperationBehaviorAttribute>에 동작을 지정합니다. 지정된 모든 값은 기본값입니다.  
  
```csharp
[ServiceBehavior(  
    AutomaticSessionShutdown=true,  
    ConcurrencyMode=ConcurrencyMode.Single,  
    InstanceContextMode=InstanceContextMode.PerSession,  
    IncludeExceptionDetailInFaults=false,  
    UseSynchronizationContext=true,  
    ValidateMustUnderstand=true)]  
public class CalculatorService : ICalculator  
{  
    [OperationBehavior(  
        TransactionAutoComplete=true,  
        TransactionScopeRequired=false,  
        Impersonation=ImpersonationOption.NotAllowed)]  
    public double Add(double n1, double n2)  
    {  
        System.Threading.Thread.Sleep(1600);  
        return n1 + n2;  
    }  
    ...  
}  
```  
  
 서비스 동작은 <xref:System.ServiceModel.ServiceBehaviorAttribute> 특성으로 지정됩니다. 다음 표에서는 이러한 일부 동작에 대해 설명합니다.  
  
|서비스 동작|설명|  
|----------------------|-----------------|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.AutomaticSessionShutdown%2A>|클라이언트 요청에 따라 세션을 자동으로 종료합니다.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>|각 서비스 인스턴스의 동시성 모드를 지정합니다.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>|인스턴스 컨텍스트 모드를 지정합니다.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.UseSynchronizationContext%2A>|입력된 동기화 컨텍스트가 설정된 경우 사용 여부를 결정합니다. Windows Forms 애플리케이션에서 `WindowsFormsSynchronizationContext`의 사용 여부를 제어하려는 경우에 사용합니다.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A>|처리되지 않은 일반적인 실행 예외를 `Fault<string>`로 변환하고 오류 메시지로 보내는지 여부를 결정합니다.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A>|트랜잭션의 격리 수준을 지정합니다.|  
|<xref:System.ServiceModel.ServiceBehaviorAttribute.ValidateMustUnderstand%2A>|예기치 않은 메시지 헤더가 오류 발생 조건이 되는지 여부를 결정합니다.|  
  
 작업 동작은 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성을 사용하여 지정합니다. 다음 표에서는 이러한 일부 동작에 대해 설명합니다.  
  
|작업 동작|Description|  
|------------------------|-----------------|  
|<xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A>|서비스 작업이 완료되면 현재 트랜잭션이 커밋되는지 여부를 결정합니다.|  
|<xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A>|서비스 작업이 클라이언트 흐름 트랜잭션에 참여하는지 여부를 결정합니다.|  
|<xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A>|서비스 작업에서 호출자의 ID를 가장하는지 여부를 결정합니다.|  
|<xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A>|서비스 작업 호출을 시작하거나 끝낼 때 서비스 인스턴스가 재생되는지 여부를 결정합니다.|  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 호출 사이의 지연은 서비스 작업에서 `System.Threading.Thread.Sleep()`에 대한 호출이 이루어진 결과로 발생합니다. 나머지 동작 샘플에서는 이런 동작에 대해 더 자세히 설명합니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```console  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Default`  
