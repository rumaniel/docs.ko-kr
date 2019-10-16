---
title: WCF 클라이언트를 사용하여 서비스 액세스
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- clients [WCF], consuming services
ms.assetid: d780af9f-73c5-42db-9e52-077a5e4de7fe
ms.openlocfilehash: ae589e1c418b1cf13fe9f5b34648bdf7a2210eed
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855664"
---
# <a name="accessing-services-using-a-wcf-client"></a>WCF 클라이언트를 사용하여 서비스 액세스

서비스를 만든 후 다음 단계는 WCF 클라이언트 프록시를 만드는 것입니다. 클라이언트 응용 프로그램은 WCF 클라이언트 프록시를 사용 하 여 서비스와 통신 합니다. 클라이언트 응용 프로그램은 일반적으로 서비스의 메타 데이터를 가져와 서비스를 호출 하는 데 사용할 수 있는 WCF 클라이언트 코드를 생성 합니다.

 WCF 클라이언트를 만드는 기본 단계는 다음과 같습니다.

1. 서비스 코드를 컴파일합니다.

2. WCF 클라이언트 프록시를 생성 합니다.

3. WCF 클라이언트 프록시를 인스턴스화합니다.

WCF 클라이언트 프록시는 서비스 모델 메타 데이터 유틸리티 도구 (Svcutil.exe)를 사용 하 여 수동으로 생성할 수 있습니다. 자세한 내용은 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)를 참조 하세요. WCF 클라이언트 프록시는 **서비스 참조 추가** 기능을 사용 하 여 Visual Studio 내에서 생성할 수도 있습니다. 어떤 방법으로 WCF 클라이언트 프록시를 생성하더라도 서비스가 실행되고 있어야 합니다. 자체 호스팅 서비스의 경우 호스트를 실행해야 합니다. 서비스가 IIS/WAS에서 호스트되는 경우에는 별도의 작업이 필요하지 않습니다.

## <a name="servicemodel-metadata-utility-tool"></a>ServiceModel Metadata 유틸리티 도구
 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 는 메타 데이터에서 코드를 생성 하는 명령줄 도구입니다. 다음 사용은 기본 Svcutil.exe 명령 예제입니다.

```console
Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>
```

 또는 Svcutil.exe에 파일 시스템의 WSDL(웹 서비스 기술 언어) 및 XSD(XML 스키마 정의 언어) 파일을 사용할 수도 있습니다.

```console
Svcutil.exe <list of WSDL and XSD files on file system>
```

 결과는 클라이언트 응용 프로그램이 서비스를 호출 하는 데 사용할 수 있는 WCF 클라이언트 코드를 포함 하는 코드 파일입니다.

 이 도구를 사용하여 구성 파일을 생성할 수도 있습니다.

```console
Svcutil.exe <file1 [,file2]>
```

 파일 이름을 제공하면 해당 이름이 출력 파일의 이름이 됩니다. 두 개의 파일 이름을 제공하면 첫 번째 파일은 입력 구성 파일로, 해당 내용이 생성된 구성과 병합되어 두 번째 파일에 기록됩니다. 구성에 대 한 자세한 내용은 [서비스에 대 한 바인딩 구성](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md)을 참조 하세요.

> [!IMPORTANT]
> 보안 되지 않은 메타 데이터 요청은 보안 되지 않은 네트워크 요청에서 수행 하는 것과 동일한 방식으로 특정 위험을 발생 시킵니다. 통신 하는 끝점이 누구 인지 확실 하지 않은 경우 검색 한 정보는 악성 서비스의 메타 데이터 일 수 있습니다.

## <a name="add-service-reference-in-visual-studio"></a>Visual Studio의 서비스 참조 추가

 서비스를 실행 하는 동안 WCF 클라이언트 프록시를 포함할 프로젝트를 마우스 오른쪽 단추로 클릭 하 고**서비스 참조** **추가** > 를 선택 합니다. **서비스 참조 추가 대화 상자**에서 호출 하려는 서비스에 대 한 URL을 입력 하 고 **이동** 단추를 클릭 합니다. 대화 상자에 지정한 주소에서 사용할 수 있는 서비스 목록이 표시됩니다. 서비스를 두 번 클릭 하 여 사용할 수 있는 계약 및 작업을 확인 하 고 생성 된 코드의 네임 스페이스를 지정한 다음 **확인** 단추를 클릭 합니다.

## <a name="example"></a>예제
 다음 코드 예제에서는 서비스에 대해 만들어진 서비스 계약을 보여 줍니다.

```csharp
// Define a service contract.
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    // Other methods are not shown here.
}
```

```vb
' Define a service contract.
<ServiceContract(Namespace:="http://Microsoft.ServiceModel.Samples")> _
Public Interface ICalculator
    <OperationContract()>  _
    Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double
    ' Other methods are not shown here.
End Interface
```

 ServiceModel Metadata 유틸리티 도구와 Visual Studio의 **서비스 참조 추가** 는 다음과 같은 WCF 클라이언트 클래스를 생성 합니다. 클래스는 제네릭 <xref:System.ServiceModel.ClientBase%601> 클래스에서 상속되며 `ICalculator` 인터페이스를 구현합니다. 또한 이 도구는 여기에 표시되지 않은 `ICalculator` 인터페이스를 생성합니다.

```csharp
public partial class CalculatorClient : System.ServiceModel.ClientBase<ICalculator>, ICalculator
{
    public CalculatorClient()
    {}

    public CalculatorClient(string endpointConfigurationName) :
            base(endpointConfigurationName)
    {}

    public CalculatorClient(string endpointConfigurationName, string remoteAddress) :
            base(endpointConfigurationName, remoteAddress)
    {}

    public CalculatorClient(string endpointConfigurationName,
        System.ServiceModel.EndpointAddress remoteAddress) :
            base(endpointConfigurationName, remoteAddress)
    {}

    public CalculatorClient(System.ServiceModel.Channels.Binding binding,
        System.ServiceModel.EndpointAddress remoteAddress) :
            base(binding, remoteAddress)
    {}

    public double Add(double n1, double n2)
    {
        return base.Channel.Add(n1, n2);
    }
}
```

```vb
Partial Public Class CalculatorClient
    Inherits System.ServiceModel.ClientBase(Of ICalculator)
    Implements ICalculator

    Public Sub New()
        MyBase.New
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String)
        MyBase.New(endpointConfigurationName)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String, ByVal remoteAddress As String)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal binding As System.ServiceModel.Channels.Binding,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(binding, remoteAddress)
    End Sub

    Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double
        Implements ICalculator.Add
        Return MyBase.Channel.Add(n1, n2)
    End Function
End Class
```

## <a name="using-the-wcf-client"></a>WCF 클라이언트 사용
 WCF 클라이언트를 사용 하려면 다음 코드에 표시 된 것 처럼 WCF 클라이언트의 인스턴스를 만들고 해당 메서드를 호출 합니다.

```csharp
// Create a client object with the given client endpoint configuration.
CalculatorClient calcClient = new CalculatorClient("CalculatorEndpoint"));
// Call the Add service operation.
double value1 = 100.00D;
double value2 = 15.99D;
double result = calcClient.Add(value1, value2);
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);
```

```vb
' Create a client object with the given client endpoint configuration.
Dim calcClient As CalculatorClient = _
New CalculatorClient("CalculatorEndpoint")

' Call the Add service operation.
Dim value1 As Double = 100.00D
Dim value2 As Double = 15.99D
Dim result As Double = calcClient.Add(value1, value2)
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result)
```

## <a name="debugging-exceptions-thrown-by-a-client"></a>클라이언트에서 Throw된 예외 디버깅

WCF 클라이언트에서 throw 된 많은 예외는 서비스의 예외로 인해 발생 합니다. 다음은 이를 보여 주는 몇 가지 예입니다.

- <xref:System.Net.Sockets.SocketException>: 현재 연결은 원격 호스트에 의해 강제로 끊겼습니다.

- <xref:System.ServiceModel.CommunicationException>: 기본 연결이 예기치 않게 닫혔습니다.

- <xref:System.ServiceModel.CommunicationObjectAbortedException>: 소켓 연결이 중단 되었습니다. 이는 메시지 처리 오류, 원격 호스트에 의해 초과되는 수신 제한 시간 또는 기본 네트워크 리소스 문제로 인해 발생할 수 있습니다.

이러한 형식의 예외가 발생할 때 가장 좋은 문제 해결 방법은 서비스측에 추적 기능을 설정하고 발생한 예외를 확인하는 것입니다. 추적에 대 한 자세한 내용은 추적 및 [사용 하 여 응용 프로그램 문제 해결](../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)을 [참조 하세요.](../../../docs/framework/wcf/diagnostics/tracing/index.md)

## <a name="see-also"></a>참고자료

- [방법: 클라이언트 만들기](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)
- [방법: 이중 계약을 사용 하 여 서비스 액세스](../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)
- [방법: 비동기적으로 서비스 작업 호출](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)
- [방법: 단방향 및 요청-회신 계약을 사용 하 여 서비스 액세스](../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)
- [방법: WSE 3.0 서비스 액세스](../../../docs/framework/wcf/feature-details/how-to-access-a-wse-3-0-service-with-a-wcf-client.md)
- [생성된 클라이언트 코드 이해](../../../docs/framework/wcf/feature-details/understanding-generated-client-code.md)
- [방법: XmlSerializer를 사용 하 여 WCF 클라이언트 응용 프로그램의 시작 시간 개선](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)
- [클라이언트 런타임 동작 지정](../../../docs/framework/wcf/specifying-client-run-time-behavior.md)
- [클라이언트 동작 구성](../../../docs/framework/wcf/configuring-client-behaviors.md)
