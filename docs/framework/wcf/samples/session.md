---
title: 세션
ms.date: 03/30/2017
helpviewer_keywords:
- Sessions
ms.assetid: 36e1db50-008c-4b32-8d09-b56e790b8417
ms.openlocfilehash: d197c68d12eff0df9d79847349ffd65cd2a437ae
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038834"
---
# <a name="session"></a>세션
Session 샘플에서는 세션이 필요한 계약을 구현하는 방법을 보여 줍니다. 세션에서는 여러 작업을 수행하기 위한 컨텍스트를 제공합니다. 그러면 서비스에서 상태를 특정 세션에 연결하여 이후의 작업에서 이전 작업의 상태를 사용할 수 있게 만들 수 있습니다. 이 샘플은 계산기 서비스를 구현 하는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다. `ICalculator` 계약은 실행 결과를 유지하면서 일련의 산술 작업을 수행할 수 있도록 수정되었습니다. 이 기능은 `ICalculatorSession` 계약에 의해 정의됩니다. 서비스에서는 계산 수행을 위해 여러 서비스 작업이 호출되는 동안 클라이언트의 상태를 유지 관리합니다. 클라이언트에서는 `Result()`를 호출하여 현재 결과를 검색하고 `Clear()`를 호출하여 결과를 0으로 지울 수 있습니다.  
  
 이 샘플에서 클라이언트는 콘솔 응용 프로그램(.exe)이고 서비스는 IIS(인터넷 정보 서비스)를 통해 호스트됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 계약의 <xref:System.ServiceModel.SessionMode>를 `Required`로 설정하면 특정 바인딩을 통해 계약이 노출된 경우에 바인딩에서 세션이 지원됩니다. 바인딩에서 세션을 지원하지 않으면 예외가 발생합니다. `ICalculatorSession` 인터페이스는 다음 샘플 코드에 표시된 것과 같이 실행 결과를 수정하는 하나 이상의 작업을 호출할 수 있도록 정의됩니다.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples", SessionMode=SessionMode.Required)]  
public interface ICalculatorSession  
{  
    [OperationContract(IsOneWay=true)]  
    void Clear();  
    [OperationContract(IsOneWay = true)]  
    void AddTo(double n);  
    [OperationContract(IsOneWay = true)]  
    void SubtractFrom(double n);  
    [OperationContract(IsOneWay = true)]  
    void MultiplyBy(double n);  
    [OperationContract(IsOneWay = true)]  
    void DivideBy(double n);  
    [OperationContract]  
    double Result();  
}  
```  
  
 서비스에서는 <xref:System.ServiceModel.InstanceContextMode>의 <xref:System.ServiceModel.InstanceContextMode.PerSession>를 사용하여 특정 서비스 인스턴스 컨텍스트를 들어오는 각 세션에 바인드합니다. 그러면 서비스에서 각 세션의 결과를 로컬 멤버 변수에서 유지 관리할 수 있습니다.  
  
```csharp
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
public class CalculatorService : ICalculatorSession  
{  
    double result = 0.0D;  
  
    public void Clear()  
    {  result = 0.0D; }  
  
    public void AddTo(double n)  
    {  result += n;   }  
  
    public void SubtractFrom(double n)  
    {  result -= n;   }  
  
    public void MultiplyBy(double n)  
    {  result *= n;   }  
  
    public void DivideBy(double n)  
    {  result /= n;   }  
  
    public double Result()  
    {  return result; }  
}  
```  
  
 샘플을 실행하면 클라이언트에서 서버에 대한 몇 개의 요청을 수행하고 결과를 요청하며, 그러면 결과가 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```console  
(((0 + 100) - 50) * 17.65) / 2 = 441.25  
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
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Session`  
