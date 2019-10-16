---
title: 오류 계약
ms.date: 03/30/2017
ms.assetid: b31b140e-dc3b-408b-b3c7-10b6fe769725
ms.openlocfilehash: 907497101c13e1f62ff2abb5da563178c9643c6c
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70039654"
---
# <a name="fault-contract"></a>오류 계약
Fault Contract 샘플은 오류 정보를 서비스에서 클라이언트로 전달하는 방법을 보여 줍니다. 이 샘플은 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 하며 내부 예외를 오류로 변환 하기 위해 몇 가지 추가 코드를 서비스에 추가 했습니다. 클라이언트는 서비스에서 오류 조건을 강제하기 위해 0으로 나누기를 시도합니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 다음 샘플 코드와 같이 계산기 계약은 <xref:System.ServiceModel.FaultContractAttribute>를 포함하도록 수정되었습니다.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract]  
    int Add(int n1, int n2);  
    [OperationContract]  
    int Subtract(int n1, int n2);  
    [OperationContract]  
    int Multiply(int n1, int n2);  
    [OperationContract]  
    [FaultContract(typeof(MathFault))]  
    int Divide(int n1, int n2);  
}  
```  
  
 <xref:System.ServiceModel.FaultContractAttribute> 특성은 `Divide` 작업이 `MathFault` 형식의 오류를 반환할 수 있다는 것을 나타냅니다. 오류는 serialize할 수 있는 모든 형식이 될 수 있습니다. 이 경우 `MathFault`는 다음과 같이 데이터 계약입니다.  
  
```csharp
[DataContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public class MathFault  
{      
    private string operation;  
    private string problemType;  
  
    [DataMember]  
    public string Operation  
    {  
        get { return operation; }  
        set { operation = value; }  
    }  
  
    [DataMember]          
    public string ProblemType  
    {  
        get { return problemType; }  
        set { problemType = value; }  
    }  
}  
```  
  
 다음 샘플 코드와 같이 0으로 나누기 예외가 발생할 경우 `Divide` 메서드는 <xref:System.ServiceModel.FaultException%601> 예외를 throw합니다. 이 예외로 인해 오류가 클라이언트에게 보내집니다.  
  
```csharp
public int Divide(int n1, int n2)  
{  
    try  
    {  
        return n1 / n2;  
    }  
    catch (DivideByZeroException)  
    {  
        MathFault mf = new MathFault();  
        mf.operation = "division";  
        mf.problemType = "divide by zero";  
        throw new FaultException<MathFault>(mf);  
    }  
}  
```  
  
 클라이언트 코드는 0으로 나누기를 요청하여 오류를 강제합니다. 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 0으로 나누기가 오류로 보고되는 것을 볼 수 있습니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```console  
Add(15,3) = 18  
Subtract(145,76) = 69  
Multiply(9,81) = 729  
FaultException<MathFault>: Math fault while doing division. Problem: divide by zero  
  
Press <ENTER> to terminate client.  
```  
  
 클라이언트는 해당 `FaultException<MathFault>` 예외를 catch하여 이를 수행합니다.  
  
```csharp
catch (FaultException<MathFault> e)  
{  
    Console.WriteLine("FaultException<MathFault>: Math fault while doing " + e.Detail.operation + ". Problem: " + e.Detail.problemType);  
    client.Abort();  
}  
```  
  
 서비스 구현의 세부 정보가 서비스의 보안 경계를 벗어나는 것을 방지하기 위해 기본적으로 예기치 않은 예외의 세부 정보는 클라이언트에게 보내지지 않습니다. `FaultContract`는 계약의 오류를 설명하고 특정 형식의 예외를 클라이언트에게 전송하기 적합한 것으로 표시하는 방법을 제공합니다. `FaultException<T>`는 오류를 소비자에게 보내기 위한 런타임 메커니즘을 제공합니다.  
  
 그러나 디버깅 시에 서비스 오류의 내부 정보를 확인하는 것이 유용합니다. 위에 설명된 보안 동작을 해제하려면 서버에서 처리되지 않은 모든 예외의 세부 정보를 클라이언트에게 보내는 오류에 포함해야 한다는 것을 지정합니다. 이렇게 하려면 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A>를 `true`로 설정합니다. 다음 샘플과 같이 구성이나 코드에서 이를 설정할 수 있습니다.  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="True" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 또한 구성 파일에서 서비스의 `behaviorConfiguration` 특성을 "CalculatorServiceBehavior"로 설정 하 여 동작을 서비스와 연결 해야 합니다.  
  
 클라이언트에서 이러한 오류를 catch하려면 제네릭이 아닌 <xref:System.ServiceModel.FaultException>을 catch해야 합니다.  
  
 이 동작은 디버깅 목적으로만 사용해야 하고 프로덕션 환경에서 사용하면 안 됩니다.  
  
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
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Faults`  
