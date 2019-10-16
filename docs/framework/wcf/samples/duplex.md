---
title: 이중
ms.date: 03/30/2017
helpviewer_keywords:
- Duplex Service Contract
ms.assetid: bc5de6b6-1a63-42a3-919a-67d21bae24e0
ms.openlocfilehash: b00f5dd31ba572a2c8fb5301cc7ae9ddda77f0e5
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045046"
---
# <a name="duplex"></a>이중

Duplex 샘플은 이중 계약을 정의 및 구현하는 방법을 보여 줍니다. 이중 통신은 클라이언트가 서비스와의 세션을 설정할 때 이루어지며, 서비스가 클라이언트로 메시지를 다시 보낼 수 있는 채널을 제공합니다. 이 샘플은 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다. 이중 계약은 클라이언트에서 서비스로의 기본 인터페이스와 서비스에서 클라이언트의 콜백 인터페이스의 쌍으로 정의됩니다. 이 샘플에서 `ICalculatorDuplex` 인터페이스를 사용하여 클라이언트는 수학 연산을 수행하고 세션 도중 결과를 계산할 수 있습니다. 서비스는 `ICalculatorDuplexCallback` 인터페이스에서 결과를 반환합니다. 클라이언트와 서비스 간에 전송되는 메시지 집합을 서로 연결하기 위해 컨텍스트를 설정해야 하므로 이중 계약에는 세션이 필요합니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

이 샘플에서 클라이언트는 콘솔 응용 프로그램(.exe)이고 서비스는 IIS(인터넷 정보 서비스)를 통해 호스트됩니다. 이중 계약은 다음과 같이 정의됩니다.

```csharp
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples", SessionMode=SessionMode.Required,
                 CallbackContract=typeof(ICalculatorDuplexCallback))]
public interface ICalculatorDuplex
{
    [OperationContract(IsOneWay = true)]
    void Clear();
    [OperationContract(IsOneWay = true)]
    void AddTo(double n);
    [OperationContract(IsOneWay = true)]
    void SubtractFrom(double n);
    [OperationContract(IsOneWay = true)]
    void MultiplyBy(double n);
    [OperationContract(IsOneWay = true)]
    void DivideBy(double n);
}

public interface ICalculatorDuplexCallback
{
    [OperationContract(IsOneWay = true)]
    void Result(double result);
    [OperationContract(IsOneWay = true)]
    void Equation(string eqn);
}
```

`CalculatorService` 클래스는 기본 `ICalculatorDuplex` 인터페이스를 구현합니다. 서비스는 <xref:System.ServiceModel.InstanceContextMode.PerSession> 인스턴스 모드를 사용하여 각 세션의 결과를 유지합니다. `Callback`이라는 private 속성은 클라이언트에 대한 콜백 채널에 액세스하는 데 사용됩니다. 서비스는 콜백 인터페이스를 통해 클라이언트에 메시지를 다시 전송하기 위해 콜백을 사용합니다.

```csharp
[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]
public class CalculatorService : ICalculatorDuplex
{
    double result = 0.0D;
    string equation;

    public CalculatorService()
    {
        equation = result.ToString();
    }

    public void Clear()
    {
        Callback.Equation($"{equation} = {result}");
        equation = result.ToString();
    }

    public void AddTo(double n)
    {
        result += n;
        equation += $" + {n}";
        Callback.Result(result);
    }

    //...

    ICalculatorDuplexCallback Callback
    {
        get
        {
            return OperationContext.Current.GetCallbackChannel<ICalculatorDuplexCallback>();
        }
    }
}
```

클라이언트는 서비스에서 메시지를 수신하기 위해 이중 계약의 콜백 인터페이스를 구현하는 클래스를 제공해야 합니다. 이 샘플에서는 `CallbackHandler` 인터페이스를 구현하기 위해 `ICalculatorDuplexCallback` 클래스가 정의됩니다.

```csharp
public class CallbackHandler : ICalculatorDuplexCallback
{
   public void Result(double result)
   {
      Console.WriteLine("Result({0})", result);
   }

   public void Equation(string equation)
   {
      Console.WriteLine("Equation({0}", equation);
   }
}
```

이중 계약에 대해 생성된 프록시의 경우 생성 시 <xref:System.ServiceModel.InstanceContext>를 제공해야 합니다. 이 <xref:System.ServiceModel.InstanceContext>는 콜백 인터페이스를 구현하는 개체의 사이트로 사용되고 서비스에서 다시 전송된 메시지를 처리합니다. <xref:System.ServiceModel.InstanceContext>는 `CallbackHandler` 클래스의 인스턴스를 사용하여 생성됩니다. 이 개체는 콜백 인터페이스를 통해 서비스에서 클라이언트로 전송된 메시지를 처리합니다.

```csharp
// Construct InstanceContext to handle messages on callback interface.
InstanceContext instanceContext = new InstanceContext(new CallbackHandler());

// Create a client.
CalculatorDuplexClient client = new CalculatorDuplexClient(instanceContext);

Console.WriteLine("Press <ENTER> to terminate client once the output is displayed.");
Console.WriteLine();

// Call the AddTo service operation.
double value = 100.00D;
client.AddTo(value);

// Call the SubtractFrom service operation.
value = 50.00D;
client.SubtractFrom(value);

// Call the MultiplyBy service operation.
value = 17.65D;
client.MultiplyBy(value);

// Call the DivideBy service operation.
value = 2.00D;
client.DivideBy(value);

// Complete equation.
client.Clear();

Console.ReadLine();

//Closing the client gracefully closes the connection and cleans up resources.
client.Close();
```

세션 통신 및 이중 통신 모두를 지원하는 바인딩을 제공하도록 구성이 수정되었습니다. `wsDualHttpBinding`은 세션 통신을 지원하며 각 방향에 대해 하나씩, 이중 HTTP 연결을 제공하여 이중 통신을 허용합니다. 서비스에서 유일한 구성 차이는 사용되는 바인딩입니다. 클라이언트에서는 다음 샘플 구성과 같이 서버가 클라이언트에 연결하는 데 사용할 수 있는 주소를 구성해야 합니다.

```xml
<client>
  <endpoint name=""
            address="http://localhost/servicemodelsamples/service.svc"
            binding="wsDualHttpBinding"
            bindingConfiguration="DuplexBinding"
            contract="Microsoft.ServiceModel.Samples.ICalculatorDuplex" />
</client>

<bindings>
  <!-- Configure a binding that support duplex communication. -->
  <wsDualHttpBinding>
    <binding name="DuplexBinding"
             clientBaseAddress="http://localhost:8000/myClient/">
    </binding>
  </wsDualHttpBinding>
</bindings>
```

샘플을 실행하면 서비스에서 전송된 콜백 인터페이스에서 클라이언트에 반환된 메시지를 볼 수 있습니다. 각 중간 결과가 표시된 다음 모든 작업이 완료되면 전체 수식이 표시됩니다. 클라이언트를 종료하려면 Enter 키를 누릅니다.

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. 솔루션의 C#, C++또는 Visual Basic .net 버전을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.

3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.

    > [!IMPORTANT]
    > 다중 컴퓨터 구성에서 클라이언트를 실행 하는 경우에는 `address` [ \< \<](../../configure-apps/file-schema/wcf/endpoint-of-client.md) `clientBaseAddress` [ 클라이언트>요소의끝점>의특성및의특성에서"localhost"를바꾸어야합니다.다음\<](../../../../docs/framework/misc/binding.md) 에 표시 된 것과 같이 적절 한 컴퓨터의 이름을 사용 하 여 [ \<wsDualHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md) 요소의 > 요소를 바인딩합니다.

    ```xml
    <client>
        <endpoint name = ""
        address="http://service_machine_name/servicemodelsamples/service.svc"
        ... />
    </client>
    ...
    <wsDualHttpBinding>
        <binding name="DuplexBinding" clientBaseAddress="http://client_machine_name:8000/myClient/">
        </binding>
    </wsDualHttpBinding>
    ```

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Duplex`
