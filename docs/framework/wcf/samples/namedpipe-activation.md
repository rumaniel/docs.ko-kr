---
title: NamedPipe 활성화
ms.date: 03/30/2017
ms.assetid: f3c0437d-006c-442e-bfb0-6b29216e4e29
ms.openlocfilehash: a7d940d6be56160945ca0f8697361314af96bc0b
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487547"
---
# <a name="namedpipe-activation"></a>NamedPipe 활성화

이 샘플에서는 WAS(Windows Process Activation Service)를 사용하는 서비스를 호스트하여 이름 파이프를 통해 통신하는 서비스를 활성화하는 방법을 보여 줍니다. 이 샘플은 기반 합니다 [Getting Started](../../../../docs/framework/wcf/samples/getting-started-sample.md) 하며 [!INCLUDE[wv](../../../../includes/wv-md.md)] 실행 합니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WASHost\NamedPipeActivation`

## <a name="sample-details"></a>샘플 세부 정보

이 샘플은 WAS(Windows Process Activation Services)에 의해 활성화된 작업자 프로세스에서 호스트되는 서비스 라이브러리(.dll) 및 클라이언트 콘솔 프로그램(.exe)으로 구성됩니다. 콘솔 창에는 클라이언트 동작이 표시됩니다.

이 서비스는 요청-회신 통신 패턴을 정의하는 계약을 구현합니다. 계약은 다음 샘플 코드처럼 수학 연산(더하기, 빼기, 곱하기 및 나누기)을 노출시키는 `ICalculator` 인터페이스에서 정의됩니다.

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    [OperationContract]
    double Subtract(double n1, double n2);
    [OperationContract]
    double Multiply(double n1, double n2);
    [OperationContract]
    double Divide(double n1, double n2);
}
```

클라이언트에서는 지정된 수학 연산을 동기적으로 요청하고 서비스 구현에서는 계산을 통해 올바른 결과를 반환합니다.

```csharp
// Service class that implements the service contract.
public class CalculatorService : ICalculator
{
    public double Add(double n1, double n2)
    {
        return n1 + n2;
    }
    public double Subtract(double n1, double n2)
    {
        return n1 - n2;
    }
    public double Multiply(double n1, double n2)
    {
        return n1 * n2;
    }
    public double Divide(double n1, double n2)
    {
        return n1 / n2;
    }
}
```

샘플에서는 보안 없이 수정된 `netNamedPipeBinding` 바인딩을 사용합니다. 클라이언트 및 서비스 구성 파일에 바인딩이 지정됩니다. 서비스의 바인딩 형식은 다음 샘플 구성과 같이 엔드포인트 요소의 `binding` 특성에 지정됩니다.

보안이 설정된 명명된 파이프 바인딩을 사용하려면 서버의 보안 모드를 원하는 보안 설정으로 변경하고 클라이언트에서 svcutil.exe를 다시 실행하여 업데이트된 클라이언트 구성 파일을 가져옵니다.

```xml
<system.serviceModel>
        <services>
            <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">

        <!-- This endpoint is exposed at the base address provided by host: net.pipe://localhost/servicemodelsamples/service.svc  -->
        <endpoint address=""
                  binding="netNamedPipeBinding"
                  bindingConfiguration="Binding1"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
        <!-- the mex endpoint is exposed at net.pipe://localhost/servicemodelsamples/service.svc/mex -->
        <endpoint address="mex"
                  binding="mexNamedPipeBinding"
                  contract="IMetadataExchange" />
      </service>
        </services>
        <bindings>
            <netNamedPipeBinding>
                <binding name="Binding1" >
                    <security mode = "None">
                    </security>
                </binding >
            </netNamedPipeBinding>
        </bindings>

    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceMetadata />
          <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
      </serviceBehaviors>
    </behaviors>

  </system.serviceModel>
```

클라이언트의 엔드포인트 정보는 다음 샘플 코드와 같이 구성됩니다.

```xml
<system.serviceModel>

    <client>
      <endpoint name=""
                          address="net.pipe://localhost/servicemodelsamples/service.svc"
                          binding="netNamedPipeBinding"
                          bindingConfiguration="Binding1"
                          contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </client>

    <bindings>

      <!--  Following is the expanded configuration section for a NetNamedPipeBinding.
            Each property is configured with the default value. -->

      <netNamedPipeBinding>
        <binding name="Binding1"
                         maxBufferSize="65536"
                         maxConnections="10">
          <security mode = "None">
          </security>
        </binding >

      </netNamedPipeBinding>
    </bindings>

  </system.serviceModel>
```

샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. IIS 7.0이 설치 되어 있는지 확인 합니다. IIS 7.0은 WAS 활성화에 필요 합니다.

2. 수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)합니다.

    또한 WCF NON-HTTP activation 구성 요소를 설치 해야 합니다.

    1. **시작** 메뉴에서 **제어판**을 선택합니다.

    2. 선택 **프로그램 및 기능**합니다.

    3. 클릭 **Windows 구성 요소를 켜거나 끄려면**합니다.

    4. 확장을 **Microsoft.NET Framework 3.0** 노드와 확인 합니다 **Windows Communication Foundation 비 HTTP 활성화** 기능입니다.

3. 명명된 파이프 활성화를 지원하도록 WAS(Windows Process Activation Service)를 구성합니다.

    편의를 위해 다음 두 단계는 샘플 디렉터리에 있는 AddNetPipeSiteBinding.cmd라는 배치 파일에서 구현합니다.

    1. net. pipe 활성화를 지원하려면 먼저 기본 웹 사이트를 net. pipe 프로토콜에 바인딩해야 합니다. 이 작업은 IIS 7.0 관리 도구 집합과 함께 설치되는 appcmd.exe를 사용하여 수행할 수 있습니다. 권한이 높은 명령 프롬프트에서 다음 명령을 실행합니다.

        ```
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        -+bindings.[protocol='net.pipe',bindingInformation='*']
        ```

        > [!NOTE]
        > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.

        이 명령은 기본 웹 사이트에 net.pipe 사이트 바인딩을 추가합니다.

    2. 사이트 내의 모든 애플리케이션에서 공통된 net.pipe 바인딩을 공유하지만 각 애플리케이션에서 net.pipe 지원을 개별적으로 사용하도록 설정할 수 있습니다. /servicemodelsamples 애플리케이션에서 net.pipe를 사용하도록 설정하려면 권한이 높은 명령 프롬프트에서 다음 명령을 실행합니다.

        ```
        %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples" /enabledProtocols:http,net.pipe
        ```

        > [!NOTE]
        > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.

        이 명령을 사용 하 여 /servicemodelsamples 응용 프로그램에 모두 사용 하 여 액세스할 수 `http://localhost/servicemodelsamples` 고 `net.tcp://localhost/servicemodelsamples`입니다.

4. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

5. 이 샘플에 대해 추가한 net. pipe 사이트 바인딩을 제거합니다.

    편의를 위해 다음 두 단계는 샘플 디렉터리에 있는 RemoveNetPipeSiteBinding.cmd라는 배치 파일에서 구현합니다.

    1. 권한이 높은 명령 프롬프트에서 다음 명령을 실행하여 사용된 프로토콜 목록에서 net.tcp를 제거합니다.

        ```
        %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples" /enabledProtocols:http
        ```

        > [!NOTE]
        > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.

    2. 권한이 높은 명령 프롬프트에서 다음 명령을 실행하여 net.tcp 사이트 바인딩을 제거합니다.

        ```
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" --bindings.[protocol='net.pipe',bindingInformation='*']
        ```

        > [!NOTE]
        > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.

## <a name="see-also"></a>참고자료

- [AppFabric 호스팅 및 지 속성 샘플](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))
