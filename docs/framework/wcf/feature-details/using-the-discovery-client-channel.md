---
title: Discovery 클라이언트 채널 사용
ms.date: 03/30/2017
ms.assetid: 1494242a-1d64-4035-8ecd-eb4f06c8d2ba
ms.openlocfilehash: 3b6bb38298b47b822a15fee92038a1d6beb15df3
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045244"
---
# <a name="using-the-discovery-client-channel"></a>Discovery 클라이언트 채널 사용
WCF 클라이언트 애플리케이션을 작성하는 경우 호출할 서비스의 엔드포인트 주소를 알아야 합니다. 대부분의 경우 서비스의 엔드포인트 주소를 미리 알 수 없거나 시간 경과에 따라 서비스의 주소가 변경됩니다. Discovery 클라이언트 채널을 사용하면 WCF 클라이언트 애플리케이션을 작성하고 호출할 서비스를 설명할 수 있습니다. 그러면 클라이언트 채널이 자동으로 프로브 요청을 보냅니다. 서비스가 응답하면 Discovery 클라이언트 채널은 프로브 응답에서 서비스의 엔드포인트 주소를 검색하고 이를 사용하여 서비스를 호출합니다.  
  
## <a name="using-the-discovery-client-channel"></a>Discovery 클라이언트 채널 사용  
 Discovery 클라이언트 채널을 사용하려면 클라이언트 채널 스택에 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>의 인스턴스를 추가합니다. 또는 <xref:System.ServiceModel.Discovery.DynamicEndpoint>을 사용할 수도 있습니다. 그러면 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>가 아직 없는 경우 바인딩에 자동으로 추가됩니다.  
  
> [!CAUTION]
> <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>를 클라이언트 채널 스택의 맨 위에 추가하는 것이 좋습니다. <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>의 맨 위에 추가되는 바인딩 요소는 자신이 만드는 <xref:System.ServiceModel.ChannelFactory> 또는 채널이 엔드포인트 주소나 `Via` 주소(`CreateChannel` 메서드에 전달됨)를 사용하지 않는지 확인해야 합니다. 이는 이러한 주소에 올바른 주소가 포함되지 않을 수 있기 때문입니다.  
  
 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 클래스에는 다음 두 개의 공용 속성이 들어 있습니다.  
  
1. 호출할 서비스를 설명하는 데 사용되는 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.FindCriteria%2A>  
  
2. <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.DiscoveryEndpointProvider%2A>검색 메시지를 보낼 검색 끝점을 지정 하는입니다.  
  
 <xref:System.ServiceModel.Discovery.FindCriteria.%23ctor%2A> 속성을 사용하면 검색할 서비스 계약, 필요한 모든 범위 URI 및 채널 열기를 시도하는 최대 횟수를 지정할 수 있습니다. 계약 형식은 생성자 <xref:System.ServiceModel.Discovery.FindCriteria>를 호출 하 여 지정 합니다. 범위 URI는 <xref:System.ServiceModel.Discovery.FindCriteria.Scopes%2A> 속성에 추가할 수 있습니다. <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 속성을 사용하면 클라이언트가 연결을 시도하는 최대 결과 수를 지정할 수 있습니다. 프로브 응답을 받으면 클라이언트는 프로브 응답의 엔드포인트 주소를 사용하여 채널을 열려고 시도합니다. 예외가 발생하면 클라이언트는 다음 프로브 응답으로 이동하고 필요한 경우 더 많은 응답이 수신될 때까지 기다립니다. 클라이언트는 채널이 성공적으로 열리거나 최대 결과 수에 도달할 때까지 이 작업을 계속 수행합니다. 이러한 설정에 대 한 자세한 내용은을 <xref:System.ServiceModel.Discovery.FindCriteria>참조 하십시오.  
  
 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.DiscoveryEndpointProvider%2A> 속성을 사용하면 사용할 검색 엔드포인트를 지정할 수 있습니다. 일반적으로 이 엔드포인트는 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>이지만 유효한 모든 엔드포인트일 수 있습니다.  
  
 서비스와 통신하기 위해 사용할 바인딩을 만들 때는 해당 서비스와 똑같은 바인딩을 사용해야 합니다. 유일한 차이점은 클라이언트 바인딩에는 스택의 최상위 요소인 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>가 있다는 것입니다. 서비스에서 시스템 제공 바인딩을 사용하는 경우 새 <xref:System.ServiceModel.Channels.CustomBinding>을 만들고 시스템 제공 바인딩을 <xref:System.ServiceModel.Channels.CustomBinding.%23ctor%2A> 생성자에 전달합니다. 그러면 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 속성에 대해 `Insert`를 호출하여 <xref:System.ServiceModel.Channels.CustomBinding.Elements%2A>를 추가할 수 있습니다.  
  
 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>를 바인딩에 추가하고 구성한 후에는 WCF 클라이언트 클래스의 인스턴스를 만들어서 연 다음 해당 메서드를 호출할 수 있습니다. 다음 예제에서는 Discovery 클라이언트 채널을 사용하여 `ICalculator` 클래스(WCF 시작 자습서에 사용됨)를 구현하고 해당 `Add` 메서드를 호출하는 WCF 서비스를 검색합니다.  
  
```  
// Create the DiscoveryClientBindingElement  
DiscoveryClientBindingElement bindingElement = new DiscoveryClientBindingElement();  
// Search for a service that implements the ICalculator interface, attempting to open  
// the channel a maximum of 2 times  
bindingElement.FindCriteria = new FindCriteria(typeof(ICalculator)) { MaxResults = 2 };  
// Use the UdpDiscoveryEndpoint  
bindingElement.DiscoveryEndpoint = new UdpDiscoveryEndpoint();  
  
// The service uses the BasicHttpBinding, so use that and insert the DiscoveryClientBindingElement at the   
// top of the stack  
CustomBinding binding = new CustomBinding(new BasicHttpBinding());  
binding.Elements.Insert(0,bindingElement);  
  
try  
{  
    // Create the WCF client and call a method  
    CalculatorClient client = new CalculatorClient(binding, new EndpointAddress("http://schemas.microsoft.com/dynamic"));  
    client.Open();  
    client.Add(1, 1);  
}  
catch (EndpointNotFoundException ex)  
{  
    Console.WriteLine("An exception occurred: " + ex.Message);  
}  
```  
  
## <a name="security-and-the-discovery-client-channel"></a>보안 및 Discovery 클라이언트 채널  
 Discovery 클라이언트 채널을 사용하는 경우 두 개의 엔드포인트가 지정됩니다. 하나는 대개 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>인 검색 메시지에 사용되고, 다른 하나는 애플리케이션 엔드포인트입니다. 보안 서비스를 구현할 때는 이러한 두 엔드포인트에 보안을 설정해야 합니다. 보안에 대 한 자세한 내용은 [서비스 및 클라이언트 보안](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)설정을 참조 하세요.
