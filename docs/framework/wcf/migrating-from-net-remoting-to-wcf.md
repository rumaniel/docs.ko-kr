---
title: .NET Remoting에서 WCF로 마이그레이션
ms.date: 03/30/2017
ms.assetid: 16902a42-ef80-40e9-8c4c-90e61ddfdfe5
ms.openlocfilehash: 91cbfa33c6645fbc0a8d9b513e3a59799114a710
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200100"
---
# <a name="migrating-from-net-remoting-to-wcf"></a>.NET Remoting에서 WCF로 마이그레이션
이 문서에서는 WCF(Windows Communication Foundation)를 사용하기 위해 .NET Remoting을 사용하는 응용 프로그램을 마이그레이션하는 방법을 설명합니다. 이러한 제품 간의 비슷한 개념을 비교한 다음 WCF의 몇 가지 일반적인 Remoting 시나리오를 수행하는 방법을 설명합니다.  
  
 .NET Remoting은 이전 버전과의 호환성을 위해서만 지원되는 레거시 제품입니다. 클라이언트와 서버 간에 개별 신뢰 수준을 유지할 수 없으므로 복합 신뢰 환경에서는 안전하지 않습니다. 예를 들어 .NET Remoting 엔드포인트를 인터넷 또는 신뢰할 수 없는 클라이언트에 노출하지 않아야 합니다. 기존 Remoting 응용 프로그램을 더욱 안전한 최신 기술로 마이그레이션하는 것이 좋습니다. 응용 프로그램의 디자인에서 HTTP만 사용하고 RESTful인 경우 ASP.NET Web API를 사용하는 것이 좋습니다. 자세한 내용은 ASP.NET Web API를 참조하세요. 응용 프로그램이 SOAP을 기반으로 하거나 TCP와 같이 Http가 아닌 프로토콜을 필요로 하는 경우 WCF를 사용하는 것이 좋습니다.  

## <a name="comparing-net-remoting-to-wcf"></a>.NET Remoting과 WCF 비교  
 이 섹션에서는 .NET Remoting의 기본 빌딩 블록을 해당 WCF의 빌딩 블록과 비교합니다. 나중에 이러한 빌딩 블록을 사용하여 WCF에서 몇 가지 일반적인 클라이언트-서버 시나리오를 만듭니다. 다음 차트에는 .NET Remoting과 WCF의 주요 공통점과 차이점이 요약되어 있습니다.  
  
||.NET Remoting|WCF|  
|-|-------------------|---------|  
|서버 유형|Subclass MarshalByRefObject|[ServiceContract] 특성으로 표시|  
|서비스 작업|서버 유형의 공용 메서드|[OperationContract] 특성으로 표시|  
|Serialization|ISerializable 또는 [Serializable]|DataContractSerializer 또는 XmlSerializer|  
|전달된 개체|값 방식 또는 참조 방식|값 방식만 해당|  
|오류/예외|모든 직렬화 가능 예외|FaultContract\<TDetail>|  
|클라이언트 프록시 개체|강력한 형식의 투명 프록시는 MarshalByRefObjects에서 자동으로 생성됩니다.|강력한 형식의 프록시가 생성 됩니다 ChannelFactory를 사용 하 여 주문형\<TChannel >|  
|필요한 플랫폼|클라이언트와 서버 모두 Microsoft OS 및 .NET를 사용해야 합니다.|플랫폼 간|  
|메시지 형식|전용|산업 표준(SOAP, WS-* 등)|  
  
### <a name="server-implementation-comparison"></a>서버 구현 비교  
  
#### <a name="creating-a-server-in-net-remoting"></a>.NET Remoting에서 서버 만들기  
 .NET Remoting 서버 유형은 MarshalByRefObject에서 파생되어야 하며 클라이언트가 호출할 수 있는 다음과 같은 메서드를 정의해야 합니다.  
  
```csharp
public class RemotingServer : MarshalByRefObject  
{  
    public Customer GetCustomer(int customerId) { … }  
}  
```  
  
 이 서버 유형의 공용 메서드가 클라이언트에서 사용할 수 있는 공용 계약이 됩니다.  서버의 공용 인터페이스와 구현은 분리되지 않습니다. 하나의 형식이 둘 다를 처리합니다.  
  
 서버 유형을 정의한 후 다음 예제와 같이 클라이언트에서 사용 가능하게 만들 수 있습니다.  
  
```csharp
TcpChannel channel = new TcpChannel(8080);  
ChannelServices.RegisterChannel(channel, ensureSecurity : true);  
RemotingConfiguration.RegisterWellKnownServiceType(  
    typeof(RemotingServer),   
    "RemotingServer",   
    WellKnownObjectMode.Singleton);  
Console.WriteLine("RemotingServer is running.  Press ENTER to terminate...");  
Console.ReadLine();  
```  
  
 Remoting 유형을 서버로 사용 가능하게 하는 방법은 구성 파일 사용을 비롯하여 여러 가지가 있습니다. 이것은 한 가지 예일 뿐입니다.  
  
#### <a name="creating-a-server-in-wcf"></a>WCF에서 서버 만들기  
 WCF의 해당 단계에서는 두 가지 유형, 즉 공용 "서비스 계약"과 구체적인 구현을 만듭니다. 첫 번째는 [ServiceContract]로 표시된 인터페이스로 선언됩니다. 클라이언트에 사용할 수 있는 메서드는 [OperationContract]로 표시됩니다.  
  
```csharp
[ServiceContract]  
public interface IWCFServer  
{  
    [OperationContract]  
    Customer GetCustomer(int customerId);  
}  
```  
  
 서버 구현은 다음 예제와 같이 별도의 구체적인 클래스에서 정의됩니다.  
  
```csharp
public class WCFServer : IWCFServer  
{  
    public Customer GetCustomer(int customerId) { … }  
}  
```  
  
 이러한 형식이 정의되고 나면 다음 예제와 같이 클라이언트에서 WCF 서버를 사용 가능하게 만들 수 있습니다.  
  
```csharp
NetTcpBinding binding = new NetTcpBinding();  
Uri baseAddress = new Uri("net.tcp://localhost:8000/wcfserver");  
  
using (ServiceHost serviceHost = new ServiceHost(typeof(WCFServer), baseAddress))  
{  
    serviceHost.AddServiceEndpoint(typeof(IWCFServer), binding, baseAddress);  
    serviceHost.Open();  
  
    Console.WriteLine(String.Format("The WCF server is ready at {0}.",  
                                    baseAddress));  
    Console.WriteLine("Press <ENTER> to terminate service...");  
    Console.WriteLine();  
    Console.ReadLine();  
}  
```  
  
> [!NOTE]
>  최대한 비슷하게 유지하기 위해 두 예제에서 모두 TCP가 사용됩니다. HTTP를 사용하는 예제를 보려면 이 항목의 뒷부분에 있는 시나리오 연습을 참조하세요.  
  
 WCF 서비스를 구성하고 호스트하는 방법에는 여러 가지가 있습니다. 다음은 "자체 호스트"라는 한 가지 예제에 불과합니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [방법: 서비스 계약 정의](how-to-define-a-wcf-service-contract.md)  
  
-   [구성 파일을 사용하여 서비스 구성](configuring-services-using-configuration-files.md)  
  
-   [서비스 호스팅](hosting-services.md)  
  
### <a name="client-implementation-comparison"></a>클라이언트 구현 비교  
  
#### <a name="creating-a-client-in-net-remoting"></a>.NET Remoting에서 클라이언트 만들기  
 .NET Remoting 서버 개체가 사용 가능하게 되면 다음 예제와 같이 클라이언트에서 사용할 수 있습니다.  
  
```csharp
TcpChannel channel = new TcpChannel();  
ChannelServices.RegisterChannel(channel, ensureSecurity : true);  
RemotingServer server = (RemotingServer)Activator.GetObject(  
                            typeof(RemotingServer),   
                            "tcp://localhost:8080/RemotingServer");  
  
RemotingCustomer customer = server.GetCustomer(42);  
Console.WriteLine(String.Format("Customer {0} {1} received.",   
                                 customer.FirstName, customer.LastName));  
```  
  
 Activator.GetObject()에서 반환된 RemotingServer 인스턴스는 "투명 프록시"라고 합니다. 클라이언트에 RemotingServer 형식의 공용 API를 구현하지만, 모든 메서드에서 다른 프로세스나 컴퓨터에서 실행 중인 서버 개체를 호출합니다.  
  
#### <a name="creating-a-client-in-wcf"></a>WCF에서 클라이언트 만들기  
 WCF의 해당 단계에서는 채널 팩터리를 사용하여 명시적으로 프록시를 만듭니다. Remoting과 마찬가지로 프록시 개체는 다음 예제와 같이 서버에서 작업을 호출하는 데 사용할 수 있습니다.  
  
```csharp
NetTcpBinding binding = new NetTcpBinding();  
String url = "net.tcp://localhost:8000/wcfserver";  
EndpointAddress address = new EndpointAddress(url);  
ChannelFactory<IWCFServer> channelFactory =   
    new ChannelFactory<IWCFServer>(binding, address);  
IWCFServer server = channelFactory.CreateChannel();  
  
Customer customer = server.GetCustomer(42);  
Console.WriteLine(String.Format("  Customer {0} {1} received.",  
                    customer.FirstName, customer.LastName));  
```  
  
 이 예제는 Remoting 예제와 가장 비슷하므로 채널 수준의 프로그래밍을 보여 줍니다. 또한 사용할 수 있습니다는 **서비스 참조 추가** 클라이언트 프로그래밍을 간소화 하는 코드를 생성 하는 Visual Studio의 접근 방식입니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [클라이언트 채널 수준 프로그래밍](./extending/client-channel-level-programming.md)  
  
-   [방법: 추가, 업데이트 또는 서비스 참조를 제거 합니다.](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference)  
  
### <a name="serialization-usage"></a>직렬화 사용  
 .NET Remoting과 WCF 둘 다 직렬화를 사용하여 클라이언트와 서버 간에 개체를 전송하지만 다음과 같은 중요한 차이점이 있습니다.  
  
1.  서로 다른 직렬 변환기 및 규칙을 사용하여 직렬화할 사항을 표시합니다.  
  
2.  .NET Remoting에서는 “참조 방식" 직렬화를 지원하여 한 계층에 있는 메서드나 속성 액세스에서 보안 경계 건너편 다른 계층에 있는 코드를 실행할 수 있게 합니다.  이 기능을 사용하면 보안 취약성이 노출되며, 따라서 신뢰할 수 없는 클라이언트에 Remoting 엔드포인트를 절대 노출해서는 안 되는 주요 이유 중 하나입니다.  
  
3.  Remoting에서 사용하는 직렬화는 옵트아웃(직렬화하지 않을 사항을 명시적으로 제외)이고 WCF 직렬화는 옵트인(직렬화할 멤버를 명시적으로 표시)입니다.  
  
#### <a name="serialization-in-net-remoting"></a>.NET Remoting의 직렬화  
 .NET Remoting에서는 클라이언트와 서버 간에 개체를 직렬화하고 역직렬화하는 다음 두 가지 방법을 지원합니다.  
  
-   *값으로* – 계층 경계를 넘어 개체의 값이 serialize 되 고 해당 개체의 새 인스턴스를 다른 계층에 생성 됩니다. 새 인스턴스의 속성 또는 메소드를 호출하면 로컬에서만 실행되며 원래 개체나 계층에는 영향을 미치지 않습니다.  
  
-   *참조로* – 특별 한 "개체 참조가" 계층 경계를 넘어 직렬화 됩니다. 한 계층에서 해당 개체의 메서드나 속성과 상호 작용하는 경우 원래 계층의 원본 개체와 다시 통신합니다. 참조 방식 개체는 양방향, 즉 서버에서 클라이언트 또는 클라이언트에서 서버로 전달될 수 있습니다.  
  
 Remoting에서 값 방식 유형은 [Serializable] 특성으로 표시되거나 다음 예제와 같이 ISerializable을 구현합니다.  
  
```csharp
[Serializable]  
public class RemotingCustomer  
{  
    public string FirstName { get; set; }  
    public string LastName { get; set; }  
    public int CustomerId { get; set; }  
}  
```  
  
 참조 방식 유형은 다음 예제와 같이 MarshalByRefObject 클래스에서 파생됩니다.  
  
```csharp
public class RemotingCustomerReference : MarshalByRefObject  
{  
    public string FirstName { get; set; }  
    public string LastName { get; set; }  
    public int CustomerId { get; set; }  
}  
```  
  
 Remoting의 참조 방식 개체의 의미를 이해하는 것이 매우 중요합니다. 두 계층(클라이언트 또는 서버) 중 하나에서 다른 계층에 참조 방식 개체를 전송하는 경우, 개체를 소유하는 계층에서 모든 메서드 호출이 다시 실행됩니다. 예를 들어 서버에서 반환한 참조 방식 개체에서 메서드를 호출하는 클라이언트가 서버에서 코드를 실행합니다. 마찬가지로, 클라이언트에서 제공한 참조 방식 개체에서 메서드를 호출하는 서버는 다시 클라이언트에서 코드를 실행합니다. 따라서 .NET Remoting은 완전히 신뢰할 수 있는 환경에서만 사용하는 것이 좋습니다. 신뢰할 수 없는 클라이언트에 공용 .NET Remoting 엔드포인트를 노출하면 Remoting 서버가 공격에 취약하게 됩니다.  
  
#### <a name="serialization-in-wcf"></a>WCF의 직렬화  
 WCF에서는 값 방식 직렬화만 지원합니다. 클라이언트와 서버 간에 교환할 형식을 정의하는 가장 일반적인 방법은 다음 예제와 같습니다.  
  
```csharp
[DataContract]  
public class WCFCustomer  
{  
    [DataMember]  
    public string FirstName { get; set; }  
  
    [DataMember]  
    public string LastName { get; set; }  
  
    [DataMember]  
    public int CustomerId { get; set; }  
}  
```  
  
 [DataContract] 특성에서는 클라이언트와 서버 간에 직렬화 및 역직렬화할 수 있는 형식으로 이 형식을 식별합니다. [DataMember] 특성을 통해서는 직렬화할 개별 속성 또는 필드를 식별합니다.  
  
 WCF는 계층 전체에 개체를 전송할 때 값만 직렬화하고 다른 계층에 새로운 개체 인스턴스를 만듭니다. 개체 값과의 상호 작용은 로컬에서만 발생합니다. .NET Remoting 참조 방식 개체와는 달리 다른 계층과 통신하지 않습니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [Serialization 및 Deserialization](./feature-details/serialization-and-deserialization.md)  
  
-   [Windows Communication Foundation 직렬화](https://msdn.microsoft.com/magazine/cc163569.aspx)  
  
### <a name="exception-handling-capabilities"></a>예외 처리 기능  
  
#### <a name="exceptions-in-net-remoting"></a>.NET Remoting의 예외  
 Remoting 서버에서 발생한 예외는 직렬화되어 클라이언트에 전송되고, 다른 예외와 마찬가지로 클라이언트에서 로컬로 발생합니다. 사용자 지정 예외는 Exception 유형을 하위 클래스로 생성하고 [Serializable]로 표시하여 만들 수 있습니다.   대부분의 프레임워크 예외는 이미 이 방식으로 표시되므로, 대부분 서버에서 발생하여, 직렬화되고 클라이언트에서 다시 발생할 수 있습니다. 이 디자인은 개발 중에는 편리하지만 서버 측 정보가 클라이언트에 실수로 공개될 수 있습니다. 이것이 완전히 신뢰할 수 있는 환경에서만 Remoting을 사용해야 하는 많은 이유 중 하나입니다.  
  
#### <a name="exceptions-and-faults-in-wcf"></a>WCF의 예외 및 결함  
 임의의 예외 형식을 서버에서 반환하면 의도하지 않게 정보가 공개될 수 있으므로 WCF에서는 허용되지 않습니다. 서비스 작업에서 예기치 않은 예외가 발생하면 클라이언트에서 범용 FaultException이 발생합니다. 이 예외는 문제점이 발생한 이유 또는 위치에 관한 정보를 포함하지 않습니다. 일부 응용 프로그램에서는 이것만으로도 충분합니다. 클라이언트에 자세한 오류 정보를 전달해야 하는 응용 프로그램에서는 오류 계약을 정의하여 해결합니다.  
  
 이 작업을 수행하려면 먼저 오류 정보를 포함할 [DataContract] 형식을 만듭니다.  
  
```csharp
[DataContract]  
public class CustomerServiceFault  
{  
    [DataMember]  
    public string ErrorMessage { get; set; }  
  
    [DataMember]  
    public int CustomerId {get;set;}  
}  
```  
  
 각 서비스 작업에 사용할 오류 계약을 지정합니다.  
  
```csharp
[ServiceContract]  
public interface IWCFServer  
{  
    [OperationContract]  
    [FaultContract(typeof(CustomerServiceFault))]  
    Customer GetCustomer(int customerId);  
}  
```  
  
 서버에서 FaultException을 발생시켜 오류 상태를 보고합니다.  
  
```csharp
throw new FaultException<CustomerServiceFault>(  
    new CustomerServiceFault() {   
        CustomerId = customerId,   
        ErrorMessage = "Illegal customer Id"   
    });  
```  
  
 클라이언트에서 서버에 요청할 때마다 결함을 일반 예외로 catch할 수 있습니다.  
  
```csharp
try  
{  
    Customer customer = server.GetCustomer(-1);  
}  
catch (FaultException<CustomerServiceFault> fault)  
{  
    Console.WriteLine(String.Format("Fault received: {0}",  
    fault.Detail.ErrorMessage));  
}  
```  
  
 오류 계약에 대한 자세한 내용은 <xref:System.ServiceModel.FaultException>을 참조하세요.  
  
### <a name="security-considerations"></a>보안 고려 사항  
  
#### <a name="security-in-net-remoting"></a>.NET Remoting의 보안  
 일부.NET Remoting 채널에서는 채널 계층의 인증 및 암호화(IPC 및 TCP)와 같은 보안 기능을 지원합니다. HTTP 채널은 IIS(인터넷 정보 서비스)를 사용하여 인증과 암호화를 모두 수행합니다. 이와 같은 지원이 있어도, 보안되지 않은 통신 프로토콜에 대해 .NET Remoting을 고려하고 완전히 신뢰할 수 있는 환경에서만 사용해야 합니다. 공용 Remoting 엔드포인트를 인터넷이나 신뢰할 수 없는 클라이언트에 노출하지 마세요.  
  
#### <a name="security-in-wcf"></a>WCF에서 보안  
 WCF는.NET Remoting에서 발견된 유형의 취약성을 해결하기 위해 보안을 염두에 두고 설계되었습니다. WCF에서는 전송 및 메시지 수준 모두에서 보안을 제공하고, 인증, 권한 부여, 암호화 등에 대한 다양한 옵션을 제공합니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [보안](./feature-details/security.md)  
  
-   [WCF 보안 지침](./feature-details/security-guidance-and-best-practices.md)  
  
## <a name="migrating-to-wcf"></a>WCF로 마이그레이션  
  
### <a name="why-migrate-from-remoting-to-wcf"></a>Remoting에서 WCF로 마이그레이션하는 이유  
  
-   **.NET remoting은 레거시 제품입니다.** 에 설명 된 대로 [.NET Remoting](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507%28v=vs.100%29), 레거시 제품으로 간주 되 고 새로운 개발에 권장 되지 않습니다. 신규 및 기존 응용 프로그램에는 WCF 또는 ASP.NET Web API를 사용하는 것이 좋습니다.  
  
-   **WCF는 플랫폼 간 표준을 사용합니다.** WCF는 플랫폼 간 상호 운용성을 염두에 두고 설계되었으며, 많은 업계 표준(SOAP, WS-Security, WS-Trust 등)을 지원합니다. WCF 서비스는 Windows 이외의 운영 체제에서 실행되는 클라이언트와 상호 운용할 수 있습니다. Remoting은 Windows 운영 체제에서 .NET 프레임워크를 사용하여 서버와 클라이언트 응용 프로그램이 모두 실행되는 환경에서 주로 사용하도록 설계되었습니다.  
  
-   **WCF는 기본 제공 보안.** WCF 보안을 염두에 두고 설계되었으며, 인증, 전송 수준 보안, 메시지 수준 보안 등에 대한 여러 옵션을 제공합니다. Remoting은 응용 프로그램이 더 쉽게 상호 운용하도록 설계되었지만, 신뢰할 수 없는 환경에서 보안이 유지되도록 설계되지는 않았습니다. WCF는 신뢰할 수 있는 환경과 신뢰할 수 없는 환경 모두에서 작동하도록 설계되었습니다.  
  
### <a name="migration-recommendations"></a>마이그레이션 권장 사항  
 다음은 .NET Remoting에서 WCF로 마이그레이션하기 위해 권장되는 단계입니다.  
  
-   **서비스 계약을 만듭니다.** 서비스 인터페이스 형식을 정의한 다음 [ServiceContract] 특성으로 표시합니다. 클라이언트에서 호출할 수 있는 모든 메서드를 [OperationContract]로 표시합니다.  
  
-   **데이터 계약을 만듭니다.** 서버와 클라이언트 간에 교환할 데이터 형식을 정의한 다음 [DataContract] 특성으로 표시합니다. 클라이언트에서 사용할 수 있는 모든 필드와 속성을 [DataMember]로 표시합니다.  
  
-   **(선택 사항) 오류 계약을 만듭니다.** 오류가 발생하면 서버와 클라이언트 간에 교환될 유형을 만듭니다. 이러한 형식을 직렬화할 수 있도록 [DataContract] 및 [DataMember]로 표시합니다. [OperationContract]로 표시한 모든 서비스 작업도 [FaultContract]로 표시하여 해당 작업에서 반환할 수 있는 오류를 표시합니다.  
  
-   **구성 하 고 서비스를 호스트 합니다.** 서비스 계약이 생성되면 다음 단계는 엔드포인트에 서비스를 노출하도록 바인딩을 구성하는 것입니다. 자세한 내용은 [끝점: 주소, 바인딩 및 계약](./feature-details/endpoints-addresses-bindings-and-contracts.md)합니다.  
  
 Remoting 응용 프로그램이 WCF로 마이그레이션된 후에도 .NET Remoting에서 종속성을 제거하는 것이 중요합니다. 그러면 응용 프로그램에서 Remoting의 취약성이 제거됩니다. 이 단계에는 다음이 포함됩니다.  
  
-   **MarshalByRefObject 사용을 중단 합니다.** MarshalByRefObject 형식은 Remoting용으로만 제공되며 WCF에서는 사용하지 않습니다. MarshalByRefObject를 하위 클래스로 분류하는 모든 응용 프로그램 형식은 제거하거나 변경해야 합니다. MarshalByRefObject 형식은 Remoting용으로만 제공되며 WCF에서는 사용하지 않습니다. MarshalByRefObject를 하위 클래스로 분류하는 모든 응용 프로그램 형식은 제거하거나 변경해야 합니다.  
  
-   **[Serializable] 및 ISerializable을 중단 합니다.** [Serializable] 특성과 ISerializable 인터페이스는 원래 신뢰할 수 있는 환경에서 형식을 직렬화하도록 설계되었으며 Remoting에서 사용됩니다. WCF 직렬화를 수행하려면 [DataContract]와 [DataMember]가 표시된 형식이 필요합니다. 응용 프로그램에서 사용하는 데이터 형식은 [DataContract]를 사용하고 ISerializable이나 [Serializable]은 사용하지 않도록 수정해야 합니다. [Serializable] 특성과 ISerializable 인터페이스는 원래 신뢰할 수 있는 환경에서 형식을 직렬화하도록 설계되었으며 Remoting에서 사용됩니다. WCF 직렬화를 수행하려면 [DataContract]와 [DataMember]가 표시된 형식이 필요합니다. 응용 프로그램에서 사용하는 데이터 형식은 [DataContract]를 사용하고 ISerializable이나 [Serializable]은 사용하지 않도록 수정해야 합니다.  
  
### <a name="migration-scenarios"></a>마이그레이션 시나리오  
 이제 WCF에서 다음과 같은 일반적인 Remoting 시나리오를 수행하는 방법을 살펴보겠습니다.  
  
1.  서버에서 값 방식으로 클라이언트에 개체를 반환합니다.  
  
2.  서버에서 참조 방식으로 클라이언트에 개체를 반환합니다.  
  
3.  클라이언트에서 값 방식으로 서버에 개체를 전송합니다.  
  
> [!NOTE]
>  WCF에서는 클라이언트에서 참조 방식으로 서버에 개체를 전송할 수 없습니다.  
  
 이러한 시나리오에서는 .NET Remoting의 기준 인터페이스가 다음 예제와 같다고 가정합니다. 여기서는 WCF를 사용하여 해당 기능을 구현하는 방법만 설명하려 하므로, .NET Remoting 구현은 중요하지 않습니다.  
  
```csharp
public class RemotingServer : MarshalByRefObject  
{  
    // Demonstrates server returning object by-value  
    public Customer GetCustomer(int customerId) {…}  
  
    // Demonstrates server returning object by-reference  
    public CustomerReference GetCustomerReference(int customerId) {…}  
  
    // Demonstrates client passing object to server by-value  
    public bool UpdateCustomer(Customer customer) {…}  
}  
```  
  
#### <a name="scenario-1-service-returns-an-object-by-value"></a>시나리오 1: 서비스에서 값 방식으로 개체 반환  
 이 시나리오에서는 값 방식으로 클라이언트에 개체를 반환하는 서버를 설명합니다. WCF에서는 항상 값 방식으로 서버에서 개체를 반환하므로, 다음 단계는 단순히 일반적인 WCF 서비스를 빌드하는 방법만 설명합니다.  
  
1.  WCF 서비스의 공용 인터페이스를 정의하여 시작한 다음 [ServiceContract] 특성으로 표시합니다. 여기서는 [OperationContract]를 사용하여 클라이언트에서 호출할 서버 측 메서드를 식별합니다.  
  
   ```csharp
   [ServiceContract]  
   public interface ICustomerService  
   {  
       [OperationContract]  
       Customer GetCustomer(int customerId);  
  
       [OperationContract]  
       bool UpdateCustomer(Customer customer);  
   }  
   ```  
  
2.  다음 단계에서는 이 서비스의 데이터 계약을 만듭니다. [DataContract] 특성으로 표시된 클래스(인터페이스가 아님)를 만들어 이 작업을 수행합니다. 클라이언트와 서버 둘 다에 표시할 개별 속성 또는 필드는 [DataMember]로 표시됩니다. 파생 형식을 허용하려면 [KnownType] 특성을 사용하여 식별해야 합니다. WCF에서 이 서비스용으로 직렬화하거나 역직렬화하도록 허용될 유일한 형식은 서비스 인터페이스에 있는 형식, 즉 "known types"입니다. 이 목록에 없는 다른 형식을 교환하려고 하면 거부됩니다.  
  
   ```csharp
   [DataContract]  
   [KnownType(typeof(PremiumCustomer))]  
   public class Customer  
   {  
       [DataMember]  
       public string FirstName { get; set; }  
  
       [DataMember]  
       public string LastName { get; set; }  
  
       [DataMember]  
       public int CustomerId { get; set; }  
   }  
  
   [DataContract]  
   public class PremiumCustomer : Customer   
   {  
       [DataMember]  
       public int AccountId { get; set; }  
   }  
   ```  
  
3.  다음으로 서비스 인터페이스의 구현을 제공합니다.  
  
   ```csharp  
   public class CustomerService : ICustomerService  
   {  
       public Customer GetCustomer(int customerId)  
       {  
           // read from database  
       }  
  
       public bool UpdateCustomer(Customer customer)  
       {  
           // write to database  
       }  
   }  
   ```  
  
4.  WCF 서비스를 실행하려면 특정 WCF 바인딩을 사용하여 특정 URL에 해당 서비스 인터페이스를 노출하는 끝점을 선언해야 합니다. 일반적으로 서버 프로젝트의 web.config 파일에 다음 섹션을 추가하여 수행합니다.  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service name="Server.CustomerService">  
            <endpoint address="http://localhost:8083/CustomerService"  
                      binding="basicHttpBinding"  
                      contract="Shared.ICustomerService" />  
          </service>  
        </services>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
5.  그러면 다음 코드를 사용하여 WCF 서비스를 시작할 수 있습니다.  
  
   ```csharp
   ServiceHost customerServiceHost = new ServiceHost(typeof(CustomerService));  
       customerServiceHost.Open();  
   ```  
  
     이 ServiceHost가 시작되고 나면 web.config 파일을 사용하여 적절한 계약, 바인딩 및 엔드포인트를 설정합니다. 구성 파일에 대 한 자세한 내용은 참조 하세요. [구성 파일을 사용 하 여 서비스 구성](./configuring-services-using-configuration-files.md)합니다. 이와 같은 서버 시작 스타일을 자체 호스트라고 합니다. WCF 서비스 호스팅에 대 한 다른 옵션에 대 한 자세한 내용은 참조 하세요 [호스팅 서비스](./hosting-services.md)합니다.  
  
6.  클라이언트 프로젝트의 app.config에서 서비스 엔드포인트에 일치하는 바인딩 정보를 선언해야 합니다. Visual Studio에서이 작업을 수행 하는 가장 쉬운 방법은 사용 하는 것 **서비스 참조 추가**, app.config 파일을 자동으로 업데이트 됩니다입니다. 또는 수동으로 동일한 변경 내용을 추가할 수 있습니다.  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <client>  
          <endpoint name="customerservice"  
                    address="http://localhost:8083/CustomerService"  
                    binding="basicHttpBinding"  
                    contract="Shared.ICustomerService"/>  
        </client>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     사용에 대 한 자세한 내용은 **서비스 참조 추가**를 참조 하십시오 [방법: 추가, 업데이트 또는 서비스 참조를 제거](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference)합니다.  
  
7.  이제 클라이언트에서 WCF 서비스를 호출할 수 있습니다. 해당 서비스의 채널 팩터리를 만들고, 채널을 요청한 다음, 해당 채널에서 원하는 메서드를 직접 호출하여 수행할 수 있습니다. 채널에서 서비스의 인터페이스를 구현하고 기본 요청/응답 논리를 처리하므로 가능합니다. 이 메서드 호출의 반환 값은 역직렬화된 서버 응답 복사본입니다.  
  
   ```csharp
   ChannelFactory<ICustomerService> factory =  
       new ChannelFactory<ICustomerService>("customerservice");  
   ICustomerService service = factory.CreateChannel();  
   Customer customer = service.GetCustomer(42);  
   Console.WriteLine(String.Format("  Customer {0} {1} received.",  
           customer.FirstName, customer.LastName));  
   ```  
  
 WCF를 통해 서버에서 클라이언트에 반환하는 개체는 항상 값 방식을 사용합니다. 개체는 서버에서 보낸 데이터의 역직렬화된 복사본입니다. 클라이언트에서 콜백을 통해 서버 코드를 호출하는 위험 없이 이러한 로컬 복사본에서 메서드를 호출할 수 있습니다.  
  
#### <a name="scenario-2-server-returns-an-object-by-reference"></a>시나리오 2: 서버에서 참조 방식으로 개체 반환  
 이 시나리오에서는 참조 방식으로 클라이언트에 개체를 제공하는 서버를 설명합니다. .NET Remoting에서는 참조 방식으로 직렬화되는 MarshalByRefObject에서 파생된 모든 형식에 대해 자동으로 처리됩니다. 이 시나리오의 예제에서는 여러 클라이언트에 개별 세션 서버 측 개체가 있을 수 있습니다. 앞서 설명한 것처럼, WCF 서비스에서 반환된 개체는 언제나 값 방식을 사용하므로 직접적으로 대응되는 참조 방식 개체가 없지만 <xref:System.ServiceModel.EndpointAddress10> 개체를 사용하여 참조 방식 의미 체계와 비슷한 작업을 수행할 수 있습니다. 이는 서버에서 세션 참조 방식 개체를 가져오기 위해 클라이언트에서 사용할 수 있는 직렬화 가능 값 방식 개체입니다. 따라서 개별 세션 서버 측 개체가 있는 클라이언트가 여러 개인 시나리오가 가능하게 됩니다.  
  
1.  먼저 세션 개체 자체에 해당하는 WCF 서비스 계약을 정의해야 합니다.  
  
   ```csharp
   [ServiceContract(SessionMode = SessionMode.Allowed)]  
       public interface ISessionBoundObject  
       {  
           [OperationContract]  
           string GetCurrentValue();  
  
           [OperationContract]  
           void SetCurrentValue(string value);  
       }  
   ```  
  
    > [!TIP]
    >  세션 개체는 [ServiceContract]로 표시되어 일반 WCF 서비스 인터페이스가 됩니다. SessionMode 속성을 설정하면 세션 서비스가 됩니다. WCF에서 세션은 두 엔드포인트 간에 전송된 여러 메시지를 서로 관련시키는 방법입니다. 즉, 클라이언트가 이 서비스에 대한 연결을 확보하고 나면 클라이언트와 서버 간에 세션이 설정됩니다. 클라이언트는 이 단일 세션 내에서 수행되는 모든 상호 작용을 수행하는 데 하나의 고유한 서버 측 개체 인스턴스를 사용합니다.  
  
2.  다음으로 이 서비스 인터페이스의 구현을 제공해야 합니다. [ServiceBehavior]로 표시하고 InstanceContextMode를 설정하여 WCF에 각 세션에서 이 형식의 고유한 인스턴스를 사용하려 함을 표시합니다.  
  
   ```csharp
   [ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]  
       public class MySessionBoundObject : ISessionBoundObject  
       {  
           private string _value;  
  
           public string GetCurrentValue()  
           {  
               return _value;  
           }  
  
           public void SetCurrentValue(string val)  
           {  
               _value = val;  
           }  
  
       }  
   ```  
  
3.  이제 이 세션 개체의 인스턴스를 가져올 방법이 필요합니다. 여기서는 EndpointAddress10 개체를 반환하는 또 다른 WCF 서비스 인터페이스를 만들어 가져옵니다. 이 인터페이스는 클라이언트에서 세션 개체를 만드는 데 사용할 수 있는 직렬화 가능한 형식의 엔드포인트입니다.  
  
   ```csharp
   [ServiceContract]  
       public interface ISessionBoundFactory  
       {  
           [OperationContract]  
           EndpointAddress10 GetInstanceAddress();  
       }  
   ```  
  
     다음과 같이 이 WCF 서비스를 구현합니다.  
  
   ```csharp
   public class SessionBoundFactory : ISessionBoundFactory  
       {  
           public static ChannelFactory<ISessionBoundObject> _factory =   
               new ChannelFactory<ISessionBoundObject>("sessionbound");  
 
           public SessionBoundFactory()  
           {  
           }  
  
           public EndpointAddress10 GetInstanceAddress()  
           {  
               IClientChannel channel = (IClientChannel)_factory.CreateChannel();  
               return EndpointAddress10.FromEndpointAddress(channel.RemoteAddress);  
           }  
       }  
   ```  
  
     이 구현에서는 세션 개체를 만들기 위해 단일 채널 팩터리를 유지 관리합니다. GetInstanceAddress()를 호출하면 채널을 만들고 이 채널과 연결된 원격 주소를 효과적으로 가리키는 EndpointAddress10 개체를 만듭니다. EndpointAddress10은 값 방식으로 클라이언트에 반환될 수 있는 데이터 형식일 뿐입니다.  
  
4.  다음 예제와 같이 다음 두 작업을 수행하여 서버의 구성 파일을 수정해야 합니다.  
  
    1.  선언 된 \<클라이언트 > 세션 개체에 대 한 끝점을 설명 하는 섹션입니다. 이 경우 서버는 클라이언트 역할도 수행하므로 이와 같은 선언이 필요합니다.  
  
    2.  팩터리와 세션 개체의 엔드포인트를 선언합니다. 클라이언트에서 서비스 엔드포인트와 통신하여 EndpointAddress10을 획득하고 세션 채널을 만들 수 있어야 하므로 필요합니다.  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
         <client>  
          <endpoint name="sessionbound"  
                    address="net.tcp://localhost:8081/SessionBoundObject"  
                    binding="netTcpBinding"  
                    contract="Shared.ISessionBoundObject"/>  
        </client>  
        <services>  
          <service name="Server.CustomerService">  
            <endpoint address="http://localhost:8083/CustomerService"  
                      binding="basicHttpBinding"  
                      contract="Shared.ICustomerService" />  
          </service>  
          <service name="Server.MySessionBoundObject">  
            <endpoint address="net.tcp://localhost:8081/SessionBoundObject"  
                      binding="netTcpBinding"  
                      contract="Shared.ISessionBoundObject" />  
          </service>  
          <service name="Server.SessionBoundFactory">  
            <endpoint address="net.tcp://localhost:8081/SessionBoundFactory"  
                      binding="netTcpBinding"  
                      contract="Shared.ISessionBoundFactory" />  
          </service>  
        </services>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     그러면 다음과 같은 서비스를 시작할 수 있습니다.  
  
   ```csharp
   ServiceHost factoryHost = new ServiceHost(typeof(SessionBoundFactory));  
   factoryHost.Open();  
  
   ServiceHost sessionHost = new ServiceHost(typeof(MySessionBoundObject));  
   sessionHost.Open();  
   ```  
  
5.  프로젝트의 app.config 파일에서 이와 같이 동일한 엔드포인트를 선언하여 클라이언트를 구성합니다.  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <client>  
          <endpoint name="customerservice"  
                    address="http://localhost:8083/CustomerService"  
                    binding="basicHttpBinding"  
                    contract="Shared.ICustomerService"/>  
          <endpoint name="sessionbound"  
                    address="net.tcp://localhost:8081/SessionBoundObject"  
                    binding="netTcpBinding"  
                    contract="Shared.ISessionBoundObject"/>  
          <endpoint name="factory"  
                    address="net.tcp://localhost:8081/SessionBoundFactory"  
                    binding="netTcpBinding"  
                    contract="Shared.ISessionBoundFactory"/>  
        </client>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
6.  이 세션 개체를 만들고 사용하려면 클라이언트에서 다음 단계를 수행해야 합니다.  
  
    1.  ISessionBoundFactory 서비스에 대한 채널을 만듭니다.  
  
    2.  이 채널을 통해 해당 서비스를 호출하여 EndpointAddress10을 가져옵니다.  
  
    3.  EndpointAddress10을 사용하여 세션 개체를 가져올 채널을 만듭니다.  
  
    4.  여러 호출에서 동일한 인스턴스로 남아 있음을 보여주기 위해 세션 개체와 상호 작용합니다.  
  
   ```csharp
   ChannelFactory<ISessionBoundFactory> channelFactory =   
       new ChannelFactory<ISessionBoundFactory>("factory");  
   ISessionBoundFactory sessionFactory = channelFactory.CreateChannel();  
  
   EndpointAddress10 address1 = sessionFactory.GetInstanceAddress();  
   EndpointAddress10 address2 = sessionFactory.GetInstanceAddress();  
  
   ChannelFactory<ISessionBoundObject> sessionObjectFactory1 =   
       new ChannelFactory<ISessionBoundObject>(new NetTcpBinding(),   
                                               address1.ToEndpointAddress());  
   ChannelFactory<ISessionBoundObject> sessionObjectFactory2 =   
       new ChannelFactory<ISessionBoundObject>(new NetTcpBinding(),   
                                               address2.ToEndpointAddress());  
  
   ISessionBoundObject sessionInstance1 = sessionObjectFactory1.CreateChannel();  
   ISessionBoundObject sessionInstance2 = sessionObjectFactory2.CreateChannel();  
  
   sessionInstance1.SetCurrentValue("Hello");  
   sessionInstance2.SetCurrentValue("World");  
  
   if (sessionInstance1.GetCurrentValue() == "Hello" &&  
       sessionInstance2.GetCurrentValue() == "World")  
   {  
       Console.WriteLine("sessionful server object works as expected");  
   }  
   ```  
  
 WCF에서는 언제나 값 방식으로 개체를 반환하지만, EndpointAddress10을 사용하여 상응하는 참조 방식 의미 체계를 지원할 수 있습니다. 그러면 클라이언트에서 세션 WCF 서비스 인스턴스를 요청할 수 있으므로 다른 WCF 서비스와 마찬가지로 상호 작용할 수 있습니다.  
  
#### <a name="scenario-3-client-sends-server-a-by-value-instance"></a>시나리오 3: 클라이언트에서 서버에 값 방식 인스턴스 전송  
 이 시나리오에서는 기본 형식이 아닌 개체 인스턴스를 값 방식으로 서버에 보내는 클라이언트를 설명합니다.  WCF에서는 값 방식으로만 개체를 전송하므로 이 시나리오에서는 일반 WCF 사용을 설명합니다.  
  
1.  시나리오 1과 동일한 WCF 서비스를 사용합니다.  
  
2.  클라이언트를 사용하여 새로운 값 방식 개체(Customer)를 만들고 ICustomerService 서비스와 통신하는 채널을 만든 다음 개체를 보냅니다.  
  
   ```csharp
   ChannelFactory<ICustomerService> factory =  
       new ChannelFactory<ICustomerService>("customerservice");  
   ICustomerService service = factory.CreateChannel();  
   PremiumCustomer customer = new PremiumCustomer {   
   FirstName = "Bob",   
   LastName = "Jones",   
   CustomerId = 43,   
   AccountId = 99};  
   bool success = service.UpdateCustomer(customer);  
   Console.WriteLine(String.Format("  Server returned {0}.", success));  
   ```  
  
     Customer 개체가 직렬화되어 서버에 전송되면 이 서버에서 해당 개체의 새 복사본으로 역직렬화됩니다.  
  
    > [!NOTE]
    >  이 코드는 파생 형식(PremiumCustomer) 전송도 보여 줍니다. 서비스 인터페이스에서는 Customer 개체를 기대하지만, Customer 클래스에 표시된 PremiumCustomer의 [KnownType] 특성도 허용됩니다. WCF에서 이 서비스 인터페이스를 통해 다른 형식을 직렬화하거나 역직렬화하려고 하면 모두 실패합니다.  
  
 데이터의 표준 WCF 교환은 값 방식입니다. 이 경우 이러한 데이터 개체 중 하나에서 메서드를 호출하면 로컬에서만 실행되며, 다른 계층에서는 코드를 호출하지 않습니다. 반환 되는 참조 개체와 같은 목표를 달성할 수 중일 *에서* 서버 수 없는 참조에의 한 개체를 전달 하는 클라이언트에 대 한 *에* 서버. 클라이언트와 서버 간에 서로 대화하는 데 필요한 시나리오는 WCF에서 이중 서비스를 사용하여 수행할 수 있습니다. 자세한 내용은 [이중 서비스](./feature-details/duplex-services.md)합니다.  
  
## <a name="summary"></a>요약  
 .NET Remoting은 완전히 신뢰할 수 있는 환경에서만 사용하도록 고안된 통신 프레임워크입니다. 이는 레거시 제품이며 이전 버전과의 호환성을 위해서만 지원됩니다. 새 응용 프로그램을 빌드하는 데 사용할 수 없습니다. 반대로, WCF는 보안을 염두에 두고 설계되었으며, 신규 및 기존 응용 프로그램에 사용하는 것이 좋습니다. Microsoft에서는 기존 Remoting 응용 프로그램을 마이그레이션하여 WCF나 ASP.NET Web API를 대신 사용하도록 권장합니다.