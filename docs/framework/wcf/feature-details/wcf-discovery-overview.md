---
title: WCF Discovery 개요
ms.date: 03/30/2017
ms.assetid: 84fad0e4-23b1-45b5-a2d4-c9cdf90bbb22
ms.openlocfilehash: fce16038b4c9ab65047125be1881be4b86976aee
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931851"
---
# <a name="wcf-discovery-overview"></a>WCF Discovery 개요
Discovery API는 WS-Discovery 프로토콜을 사용한 웹 서비스의 동적 게시 및 검색을 위한 통합 프로그래밍 모델을 제공합니다. 이러한 API를 통해 서비스는 스스로를 게시할 수 있고 클라이언트는 게시된 서비스를 찾을 수 있습니다. 서비스가 검색 가능하게 되면 해당 서비스는 검색 요청을 수신하고 이에 대해 응답하는 것 외에 알림 메시지를 보낼 수도 있습니다. 검색 가능한 서비스는 Hello 메시지를 보내 네트워크에서 서비스의 도착을 알리며, Bye 메시지를 보내 네트워크에서 서비스의 출발을 알립니다. 클라이언트는 서비스를 찾기 위해 서비스 계약 형식, 키워드 및 네트워크 범위와 같은 특정 조건이 포함된 `Probe` 요청을 보냅니다. 서비스는 `Probe` 요청을 받고 자신이 이 조건에 일치하는지 여부를 확인합니다. 일치할 경우 서비스는 서비스에 연결하는 데 필요한 정보와 함께 `ProbeMatch` 메시지를 클라이언트로 돌려보내 응답합니다. 또한 클라이언트는 엔드포인트 주소가 변경된 경우에도 서비스를 찾을 수 있는 `Resolve` 요청을 보낼 수도 있습니다. 일치하는 서비스는 `Resolve` 메시지를 클라이언트로 돌려보내 `ResolveMatch` 요청에 응답합니다.  
  
## <a name="ad-hoc-and-managed-modes"></a>애드혹 및 관리 모드  
 검색 API는 다음과 같은 두 가지 모드를 지원 합니다. 관리 및 임시. 관리 모드에는 사용 가능한 서비스에 대한 정보를 유지 관리하는 검색 프록시라는 중앙 서버가 있습니다. 검색 프록시는 다양한 방법을 통해 서비스에 대한 정보로 채워집니다. 예를 들어 서비스가 시작 시에 검색 프록시로 알림 메시지를 보낼 수도 있고, 프록시가 데이터베이스 또는 구성 파일에서 데이터를 읽어 사용 가능한 서비스를 확인할 수도 있습니다. 검색 프록시를 채우는 방법은 전적으로 개발자의 재량에 따라 결정됩니다. 클라이언트는 검색 프록시를 통해 사용 가능한 서비스에 대한 정보를 검색합니다. 클라이언트는 서비스를 검색할 때 검색 프록시로 `Probe` 메시지를 보내며, 프록시는 자신이 아는 서비스 중에 클라이언트가 검색하는 서비스와 일치하는 서비스가 있는지 여부를 확인합니다. 일치하는 서비스가 있으면 검색 프록시는 클라이언트로 `ProbeMatch` 응답을 돌려보냅니다. 그러면 클라이언트는 프록시에서 반환된 서비스 정보를 사용하여 서비스에 직접 연결합니다. 관리 모드의 기반이 되는 핵심 원칙은 검색 요청이 하나의 기관, 즉 검색 프록시로 유니캐스트 방식으로 전송된다는 것입니다. .NET Framework에는 사용자가 직접 프록시를 빌드할 수 있도록 하는 주요 구성 요소가 포함되어 있습니다. 클라이언트와 서비스는 다음과 같은 여러 방법으로 프록시를 찾을 수 있습니다.  
  
- 프록시는 애드혹 메시지에 응답할 수 있습니다.  
  
- 프록시는 시작 시 알림 메시지를 보낼 수 있습니다.  
  
- 잘 알려진 특정 엔드포인트를 찾도록 클라이언트 및 서비스를 작성할 수 있습니다.  
  
 애드혹 모드에는 중앙 서버가 없습니다. 서비스 알림 및 클라이언트 요청과 같은 모든 검색 메시지는 멀티캐스트 방식으로 전송됩니다. 기본적으로 .NET Framework에는 UDP 프로토콜을 통한 애드혹 검색 지원이 포함되어 있습니다. 예를 들어 서비스가 시작 시 Hello 알림을 보내도록 구성된 경우 이 서비스는 UDP 프로토콜을 사용하여 잘 알려진 멀티캐스트 주소를 통해 알림을 보냅니다. 클라이언트는 적극적으로 이러한 알림을 수신하고 적절히 처리해야 합니다. 클라이언트는 서비스에 대한 `Probe` 메시지를 보낼 때 멀티캐스트 프로토콜을 사용하여 네트워크를 통해 이 메시지를 보냅니다. 요청을 받는 각 서비스는 `Probe` 메시지에 포함된 조건과 자신이 일치하는지 여부를 확인하고, `ProbeMatch` 메시지에 지정된 조건과 일치하는 경우 `Probe` 메시지로 클라이언트에 직접 응답합니다.  
  
## <a name="benefits-of-using-wcf-discovery"></a>WCF Discovery를 사용할 경우의 장점  
 WCF Discovery는 WS-Discovery 프로토콜을 사용하여 구현되므로 WS-Discovery를 구현하는 다른 클라이언트, 서비스 및 프록시와 상호 운용이 가능합니다. WCF Discovery는 기존 WCF API를 기반으로 구축되므로 기존 서비스 및 클라이언트에 검색 기능을 손쉽게 추가할 수 있습니다. 서비스 검색 기능은 애플리케이션 구성 설정을 통해 쉽게 추가할 수 있습니다. 또한 WCF Discovery는 피어 넷, 명명 오버레이 및 HTTP와 같은 다른 전송에서의 검색 프로토콜 사용도 지원합니다. WCF Discovery는 검색 프록시가 사용되는 작업의 관리 모드를 지원합니다. 이로써 전체 네트워크로 멀티캐스트 메시지를 보내는 대신 검색 프록시로 메시지를 직접 보내게 되므로 네트워크 트래픽이 감소합니다. WCF Discovery는 웹 서비스와 함께 사용할 때 유연성도 더욱 높여 줍니다. 예를 들어 클라이언트나 서비스를 다시 구성할 필요 없이 서비스 주소를 변경할 수 있습니다. 클라이언트는 서비스에 액세스해야 하는 경우 `Probe` 요청을 통해 `Find` 메시지를 발송하고 서비스가 현재 주소를 사용하여 응답하기를 기다립니다. WCF Discovery를 통해 클라이언트는 계약 형식, 바인딩 요소, 네임스페이스, 범위 및 키워드 또는 버전 번호와 같은 다양한 조건에 따라 서비스를 검색할 수 있습니다. WCF Discovery를 사용하면 런타임 및 디자인 타임 검색이 가능합니다. 내결함성 및 자동 구성과 같은 다른 시나리오를 지원하기 위해 애플리케이션에 검색 기능을 추가할 수 있습니다.  
  
## <a name="service-publication"></a>서비스 게시  
 서비스 검색을 가능하게 하려면 서비스 호스트에 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>를 추가하고 검색 엔드포인트를 추가하여 검색 메시지를 수신할 위치를 지정해야 합니다. 다음 코드 예제에서는 자체 호스팅 서비스를 검색 가능하도록 수정하는 방법을 보여 줍니다.  
  
```csharp  
Uri baseAddress = new Uri(string.Format("http://{0}:8000/discovery/scenarios/calculatorservice/{1}/",  
        System.Net.Dns.GetHostName(), Guid.NewGuid().ToString()));

// Create a ServiceHost for the CalculatorService type.
using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))
{
    // Add calculator endpoint
    serviceHost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(), string.Empty);

    // ** DISCOVERY ** //
    // Make the service discoverable by adding the discovery behavior
    serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());

    // ** DISCOVERY ** //
    // Add the discovery endpoint that specifies where to publish the services
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());

    // Open the ServiceHost to create listeners and start listening for messages.
    serviceHost.Open();

    // The service can now be accessed.
    Console.WriteLine("Press <ENTER> to terminate service.");
    Console.ReadLine();
}
```  
  
 서비스를 검색 가능하게 하려면 서비스 설명에 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> 인스턴스를 추가해야 합니다. 서비스에 검색 요청을 수신할 위치를 알리려면 서비스 호스트에 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> 인스턴스를 추가해야 합니다. 이 예제에서는 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>(<xref:System.ServiceModel.Discovery.DiscoveryEndpoint>에서 파생됨)를 추가하여 서비스가 UDP 멀티캐스트 전송을 통해 검색 요청을 수신하도록 지정합니다. 모든 메시지가 멀티캐스트 방식으로 전송되므로 애드혹 검색을 위해 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>가 사용됩니다.  
  
## <a name="announcement"></a>알림  
 기본적으로 서비스 게시는 알림 메시지를 보내지 않습니다. 알림 메시지를 보내도록 서비스를 구성해야 합니다. 이렇게 하면 서비스 작성기가 검색 메시지 수신과는 별도로 서비스를 알릴 수 있으므로 유연성이 높아집니다. 서비스 알림은 검색 프록시 및 기타 서비스 레지스트리에 서비스를 등록하기 위한 메커니즘으로도 사용할 수 있습니다. 다음 코드는 UDP 바인딩을 통해 알림 메시지를 보내도록 서비스를 구성하는 방법을 보여 줍니다.  
  
```csharp  
Uri baseAddress = new Uri(string.Format("http://{0}:8000/discovery/scenarios/calculatorservice/{1}/",
        System.Net.Dns.GetHostName(), Guid.NewGuid().ToString()));

// Create a ServiceHost for the CalculatorService type.
using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))
{
    // Add calculator endpoint
    serviceHost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(), string.Empty);

    // ** DISCOVERY ** //
    // Make the service discoverable by adding the discovery behavior
    ServiceDiscoveryBehavior discoveryBehavior = new ServiceDiscoveryBehavior();
    serviceHost.Description.Behaviors.Add(discoveryBehavior);

    // Send announcements on UDP multicast transport
    discoveryBehavior.AnnouncementEndpoints.Add(
      new UdpAnnouncementEndpoint());

    // ** DISCOVERY ** //
    // Add the discovery endpoint that specifies where to publish the services
    serviceHost.Description.Endpoints.Add(new UdpDiscoveryEndpoint());

    // Open the ServiceHost to create listeners and start listening for messages.
    serviceHost.Open();

    // The service can now be accessed.
    Console.WriteLine("Press <ENTER> to terminate service.");
    Console.ReadLine();
}
```  
  
## <a name="service-discovery"></a>서비스 검색  
 클라이언트 애플리케이션은 <xref:System.ServiceModel.Discovery.DiscoveryClient> 클래스를 사용하여 서비스를 찾을 수 있습니다. 개발자는 <xref:System.ServiceModel.Discovery.DiscoveryClient> 또는 `Probe` 메시지를 보낼 위치를 지정하는 검색 엔드포인트를 전달하는 `Resolve` 클래스의 인스턴스를 만듭니다. 그러면 클라이언트가 <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> 인스턴스 내에서 검색 조건을 지정하는 <xref:System.ServiceModel.Discovery.FindCriteria>를 호출합니다. 일치하는 서비스가 발견되면 <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A>는 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> 컬렉션을 반환합니다. 다음 코드는 `Find` 메서드를 호출한 다음 검색된 서비스에 연결하는 방법을 보여 줍니다.  
  
```csharp  
class Client
{
    static EndpointAddress serviceAddress;
  
    static void Main()
    {  
        if (FindService()) 
        {
            InvokeService();
        }
    }  
  
    // ** DISCOVERY ** //  
    static bool FindService()  
    {  
        Console.WriteLine("\nFinding Calculator Service ..");  
        DiscoveryClient discoveryClient =   
            new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
        Collection<EndpointDiscoveryMetadata> calculatorServices =   
            (Collection<EndpointDiscoveryMetadata>)discoveryClient.Find(new FindCriteria(typeof(ICalculator))).Endpoints;  
  
        discoveryClient.Close();  
  
        if (calculatorServices.Count == 0)  
        {  
            Console.WriteLine("\nNo services are found.");  
            return false;  
        }  
        else  
        {  
            serviceAddress = calculatorServices[0].Address;  
            return true;  
        }  
    }  
  
    static void InvokeService()  
    {  
        Console.WriteLine("\nInvoking Calculator Service at {0}\n", serviceAddress);  
  
        // Create a client  
        CalculatorClient client = new CalculatorClient();  
        client.Endpoint.Address = serviceAddress;  
        client.Add(10,3);  
    }
}  
```  
  
## <a name="discovery-and-message-level-security"></a>검색 및 메시지 수준 보안  
 메시지 수준 보안을 사용하는 경우 서비스 검색 엔드포인트에 <xref:System.ServiceModel.EndpointIdentity>를, 클라이언트 검색 엔드포인트에 일치하는 <xref:System.ServiceModel.EndpointIdentity>를 지정해야 합니다. 메시지 수준 보안에 대 한 자세한 내용은 [메시지 보안](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)을 참조 하세요.  
  
## <a name="discovery-and-web-hosted-services"></a>검색 및 웹 호스팅 서비스  
 WCF 서비스가 검색 가능하려면 실행되고 있어야 합니다. IIS 또는 WAS에서 호스팅되는 WCF 서비스는 IIS/WAS가 서비스에 바인딩된 메시지를 받을 때까지 실행되지 않으므로 기본적으로 검색 가능하지 않습니다.  웹 호스팅 서비스를 검색 가능하게 만드는 방법은 다음 두 가지입니다.  
  
1. Windows Server AppFabric 자동 시작 기능 사용  
  
2. 서비스 대신 통신할 검색 프록시 사용  
  
 Windows Server AppFabric에는 메시지를 받기 전에 서비스가 시작될 수 있도록 하는 자동 시작 기능이 있습니다. 이 자동 시작 집합을 사용하여 IIS/WAS에서 호스팅된 서비스가 검색 가능하도록 구성할 수 있습니다. 자동 시작 기능에 대 한 자세한 내용은 [Windows Server AppFabric 자동 시작 기능](https://go.microsoft.com/fwlink/?LinkId=205545)을 참조 하세요. 자동 시작 기능을 설정하는 것과 함께 검색에 대해 서비스를 구성해야 합니다. 자세한 내용은 [방법: 프로그래밍 방식으로 WCF 서비스 및 클라이언트](../../../../docs/framework/wcf/feature-details/how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)에 검색 기능을 추가 하 여[구성 파일에서 검색을 구성](../../../../docs/framework/wcf/feature-details/configuring-discovery-in-a-configuration-file.md)합니다.  
  
 WCF 서비스가 실행되지 않을 때 검색 프록시를 사용하여 WCF 서비스 대신 통신할 수 있습니다. 프록시는 프로브 또는 확인 메시지를 수신하고 클라이언트에 응답할 수 있습니다. 그러면 클랑이언트에서 서비스에 직접 메시지를 보낼 수 있습니다. 클라이언트에서 서비스에 메시지를 보낼 때 서비스가 메시지에 응답하기 위해 인스턴스화됩니다. 검색 프록시를 구현 하는 방법에 대 한 자세한 내용은 [검색 프록시 구현](../../../../docs/framework/wcf/feature-details/implementing-a-discovery-proxy.md)을 참조 하세요.  
  
> [!NOTE]
> WCF 검색이 제대로 작동 하려면 모든 Nic (네트워크 인터페이스 컨트롤러)에 IP 주소가 1 개만 있어야 합니다.
