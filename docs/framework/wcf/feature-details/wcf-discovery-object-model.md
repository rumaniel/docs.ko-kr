---
title: WCF Discovery 개체 모델
ms.date: 03/30/2017
ms.assetid: 8365a152-eacd-4779-9130-bbc48fa5c5d9
ms.openlocfilehash: d305528c379bd4ded339854ee1f9fa55c76b40c0
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614791"
---
# <a name="wcf-discovery-object-model"></a>WCF Discovery 개체 모델
WCF Discovery는 런타임에 검색 가능한 서비스와 이러한 서비스를 찾아서 사용하는 클라이언트를 작성할 수 있는 통합된 프로그래밍 모델을 제공하는 일련의 형식으로 구성되어 있습니다.  
  
## <a name="making-a-service-discoverable-and-finding-services"></a>서비스를 검색 가능하게 만들고 서비스 찾기  
 WCF 서비스를 검색 가능하게 만들려면 서비스 호스트의 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>에 <xref:System.ServiceModel.Description.ServiceDescription>를 추가하고 검색 엔드포인트를 추가합니다. <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>를 추가하여 알림 메시지를 보내도록 서비스를 구성한 경우 서비스 호스트가 열리고 닫힐 때 알림이 보내집니다.  
  
 서비스 알림 메시지를 수신 대기할 클라이언트는 알림 서비스를 호스팅하고 하나 이상의 알림 엔드포인트를 추가합니다. 알림 서비스는 알림 메시지를 받고 알림 이벤트를 발생시킵니다.  
  
 클라이언트는 <xref:System.ServiceModel.Discovery.DiscoveryClient> 클래스를 사용하여 사용 가능한 서비스를 검색합니다. 클라이언트 애플리케이션은 <xref:System.ServiceModel.Discovery.DiscoveryClient> 클래스를 인스턴스화하여 검색 메시지를 보낼 위치를 지정하는 검색 엔드포인트를 제공합니다. 클라이언트가 <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> 메서드를 호출하여 `Probe` 요청을 보내면 검색 메시지를 수신 대기하는 서비스가 이 `Probe` 요청을 받습니다. 이 서비스는 `Probe`에 지정된 조건과 일치할 경우 클라이언트에 `ProbeMatch` 메시지를 다시 보냅니다.  
  
## <a name="object-model"></a>개체 모델  
 WCF Discovery API는 다음과 같은 클래스를 정의합니다.  
  
- <xref:System.ServiceModel.Discovery.AnnouncementClient>  
  
- <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
  
- <xref:System.ServiceModel.Discovery.AnnouncementService>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryClient>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryMessageSequenceGenerator>  
  
- <xref:System.ServiceModel.Discovery.ServiceDiscoveryMode>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryProxy>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryService>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryVersion>  
  
- <xref:System.ServiceModel.Discovery.DynamicEndpoint>  
  
- <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior>  
  
- <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>  
  
- <xref:System.ServiceModel.Discovery.FindCriteria>  
  
- <xref:System.ServiceModel.Discovery.FindRequestContext>  
  
- <xref:System.ServiceModel.Discovery.FindResponse>  
  
- <xref:System.ServiceModel.Discovery.ResolveCriteria>  
  
- <xref:System.ServiceModel.Discovery.ResolveResponse>  
  
- <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>  
 
- <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
  
- <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
  
## <a name="announcementclient"></a>AnnouncementClient  
 <xref:System.ServiceModel.Discovery.AnnouncementClient> 클래스는 알림 메시지를 보내기 위한 동기 및 비동기 메서드를 제공합니다. 알림 메시지에는 Hello와 Bye라는 두 가지 유형이 있습니다. Hello 메시지는 서비스가 사용 가능하게 되었음을 알리는 데 사용되고 Bye 메시지는 기존 서비스가 사용 가능하지 않게 되었음을 알리는 데 사용됩니다. 개발자는 <xref:System.ServiceModel.Discovery.AnnouncementClient> 인스턴스를 만들어 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>의 인스턴스를 생성자 매개 변수로 제공합니다.  
  
## <a name="announcementendpoint"></a>AnnouncementEndpoint  
 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>는 고정 알림 계약이 있는 표준 엔드포인트를 나타냅니다. 이 표준 끝점은 서비스나 클라이언트에서 알림 메시지를 보내고 받는 데 사용됩니다. 기본적으로 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> 클래스는 WS_Discovery 11 프로토콜 버전을 사용하도록 설정됩니다.  
  
## <a name="announcementservice"></a>AnnouncementService  
 <xref:System.ServiceModel.Discovery.AnnouncementService>는 알림 메시지를 받고 처리하는 알림 서비스의 시스템 제공 구현입니다. Hello 또는 Bye 메시지가 수신되면 <xref:System.ServiceModel.Discovery.AnnouncementService> 인스턴스는 해당 가상 메서드인 <xref:System.ServiceModel.Discovery.AnnouncementService.OnBeginOnlineAnnouncement%2A> 또는 <xref:System.ServiceModel.Discovery.AnnouncementService.OnBeginOfflineAnnouncement%2A>를 호출하여 알림 이벤트를 발생시킵니다.  
  
## <a name="discoveryclient"></a>DiscoveryClient  
 <xref:System.ServiceModel.Discovery.DiscoveryClient> 클래스는 클라이언트 애플리케이션에서 사용 가능한 서비스를 찾고 확인하는 데 사용됩니다. 이 클래스는 지정된 <xref:System.ServiceModel.Discovery.FindCriteria> 및 <xref:System.ServiceModel.Discovery.ResolveCriteria>를 각각 기반으로 하여 서비스를 찾고 확인하기 위한 동기 및 비동기 메서드를 제공합니다. 개발자는 <xref:System.ServiceModel.Discovery.DiscoveryClient> 인스턴스를 만들어 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>의 인스턴스를 생성자 매개 변수로 제공합니다.  
  
 개발자는 사용할 검색 조건이 들어 있는 `Find` 인스턴스를 제공하는 동기 또는 비동기 <xref:System.ServiceModel.Discovery.FindCriteria> 메서드를 호출하여 서비스를 찾습니다. <xref:System.ServiceModel.Discovery.DiscoveryClient>는 해당 헤더가 포함된 `Probe` 메시지를 만들고 찾기 요청을 보냅니다. 처리되지 않은 `Find` 요청은 언제든지 둘 이상 있을 수 있으므로 클라이언트는 수신된 응답을 상호 연결하고 이러한 응답의 유효성을 검사한 다음 `Find`를 사용하여 <xref:System.ServiceModel.Discovery.FindResponse> 작업의 호출자에게 결과를 전달합니다.  
  
 개발자는 알려진 서비스의 `Resolve`가 들어 있는 <xref:System.ServiceModel.Discovery.ResolveCriteria>의 인스턴스를 제공하는 동기 또는 비동기 <xref:System.ServiceModel.EndpointAddress> 메서드를 호출하여 알려진 서비스를 확인합니다. <xref:System.ServiceModel.Discovery.DiscoveryClient>는 해당 헤더가 포함된 `Resolve` 메시지를 만들고 확인 요청을 보냅니다. 그러면 수신된 응답이 처리되지 않은 확인 요청과 상호 연결되고 `Resolve`를 사용하여 결과가 <xref:System.ServiceModel.Discovery.ResolveResponse> 작업의 호출자에게 전달됩니다.  
  
 검색 프록시가 네트워크에 있는 경우 <xref:System.ServiceModel.Discovery.DiscoveryClient>가 검색 요청을 멀티캐스트 방식으로 보내면 검색 프록시가 멀티캐스트 비표시 오류(Suppression) Hello 메시지로 응답할 수 있습니다. <xref:System.ServiceModel.Discovery.DiscoveryClient>는 처리되지 않은 `ProxyAvailable` 또는 `Find` 요청에 대한 응답으로 Hello 메시지를 받으면 `Resolve` 이벤트를 발생시킵니다. `ProxyAvailable` 이벤트에는 검색 프록시에 대한 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>가 포함되어 있습니다. 이 정보를 사용하여 애드혹 모드에서 관리 모드로 전환하는 것은 개발자에게 달려 있습니다.  
  
## <a name="discoveryendpoint"></a>DiscoveryEndpoint  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>는 고정 검색 계약이 있는 표준 엔드포인트를 나타냅니다. 이 표준 끝점은 서비스나 클라이언트에서 검색 메시지를 보내거나 받는 데 사용됩니다. 기본적으로 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>는 <xref:System.ServiceModel.Discovery.ServiceDiscoveryMode.Managed?displayProperty=nameWithType> 모드와 WSDiscovery11 WS-Discovery 버전을 사용하도록 설정됩니다.  
  
## <a name="discoverymessagesequencegenerator"></a>DiscoveryMessageSequenceGenerator  
 <xref:System.ServiceModel.Discovery.DiscoveryMessageSequenceGenerator>는 서비스에서 검색 또는 알림 메시지를 보낼 때 <xref:System.ServiceModel.Discovery.DiscoveryMessageSequence>를 생성하는 데 사용됩니다.  
  
## <a name="discoveryservice"></a>DiscoveryService  
 <xref:System.ServiceModel.Discovery.DiscoveryService> 추상 클래스는 `Probe` 및 `Resolve` 메시지를 받고 처리하기 위한 프레임워크를 제공합니다. `Probe` 메시지가 수신되면 <xref:System.ServiceModel.Discovery.DiscoveryService>는 들어오는 메시지를 기반으로 <xref:System.ServiceModel.Discovery.FindRequestContext>의 인스턴스를 만들고 <xref:System.ServiceModel.Discovery.DiscoveryService.OnBeginFind%2A> 가상 메서드를 호출합니다. `Resolve` 메서드가 수신되면 <xref:System.ServiceModel.Discovery.DiscoveryService>는 <xref:System.ServiceModel.Discovery.DiscoveryService.OnBeginResolve%2A> 가상 메서드를 호출합니다. 사용자 지정 검색 서비스 구현을 제공하려면 이 클래스에서 상속할 수 있습니다.  
  
## <a name="discoveryproxy"></a>DiscoveryProxy  
 <xref:System.ServiceModel.Discovery.DiscoveryProxy> 추상 클래스는 검색 및 알림 메시지를 받고 처리하기 위한 프레임워크를 제공합니다. 사용자 지정 검색 프록시를 구현하는 경우 이 클래스에서 상속합니다. `Probe` 메시지가 멀티캐스트를 통해 수신되면 <xref:System.ServiceModel.Discovery.DiscoveryProxy> 클래스는 `BeginShouldRedirectFind` 가상 메서드를 호출하여 멀티캐스트 비표시 오류(Suppression) 메시지를 보내야 하는지 여부를 결정합니다. 개발자가 멀티캐스트 비표시 오류(Suppression) 메시지를 보내지 않도록 결정하거나 `Probe` 메시지가 유니캐스트를 통해 수신되는 경우 이 클래스는 들어오는 메시지를 기반으로 <xref:System.ServiceModel.Discovery.FindRequestContext> 클래스의 인스턴스를 만들고 `OnBeginFind` 가상 메서드를 호출합니다. `Resolve` 메시지가 멀티캐스트를 통해 수신되면 <xref:System.ServiceModel.Discovery.DiscoveryProxy> 클래스는 `ShouldRedirectResolve` 가상 메서드를 호출하여 멀티캐스트 비표시 오류(Suppression) 메시지를 보내야 하는지 여부를 결정합니다. 개발자가 멀티캐스트 비표시 오류(Suppression) 메시지를 보내지 않도록 결정하거나 `Resolve` 메시지가 유니캐스트를 통해 수신되는 경우 이 클래스는 들어오는 메시지를 기반으로 <xref:System.ServiceModel.Discovery.ResolveCriteria> 클래스의 인스턴스를 만들고 `OnBeginResolve` 가상 메서드를 호출합니다. Hello 또는 Bye 메시지가 수신되면 <xref:System.ServiceModel.Discovery.DiscoveryProxy>는 알림 이벤트를 발생시키는 해당 가상 메서드(`OnBeginOnlineAnnouncement` 또는 `OnBeingOfflineAnnouncement`)를 호출합니다.  
  
## <a name="discoveryversion"></a>DiscoveryVersion  
 <xref:System.ServiceModel.Discovery.DiscoveryVersion> 클래스는 사용할 검색 프로토콜 버전을 나타냅니다.  
  
## <a name="endpointdiscoverybehavior"></a>EndpointDiscoveryBehavior  
 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> 클래스는 엔드포인트의 검색 기능을 제어하고 확장명, 추가 계약 형식 이름 및 해당 엔드포인트와 연결된 범위를 지정하는 데 사용됩니다. 이 동작은 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>를 구성하기 위해 애플리케이션 엔드포인트에 추가됩니다. <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>가 서비스 호스트에 추가되면 서비스 호스트에 의해 기본적으로 호스팅되는 모든 애플리케이션 엔드포인트가 검색 가능하게 됩니다. 개발자는 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior.Enabled%2A> 속성을 `false`로 설정하여 특정 엔드포인트에 대한 검색을 해제할 수 있습니다.  
  
## <a name="endpointdiscoverymetadata"></a>EndpointDiscoveryMetadata  
 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> 클래스는 서비스가 게시한 엔드포인트를 버전에 관계없이 나타냅니다. 이 클래스에는 서비스 개발자가 지정한 엔드포인트 주소, 수신 대기 URI, 계약 형식 이름, 범위, 메타데이터 버전 및 확장이 포함되어 있습니다. <xref:System.ServiceModel.Discovery.FindCriteria> 작업 중에 클라이언트가 보낸 `Probe`는 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>와 일치하는지 비교됩니다. 조건이 일치하면 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>가 클라이언트에 반환됩니다. <xref:System.ServiceModel.Discovery.ResolveCriteria>의 엔드포인트 주소는 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>의 엔드포인트 주소와 일치하는지 비교됩니다. 조건이 일치하면 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>가 클라이언트에 반환됩니다.  
  
## <a name="findcriteria"></a>FindCriteria  
 <xref:System.ServiceModel.Discovery.FindCriteria> 클래스는 서비스를 찾을 때 사용되는 조건을 지정하는 데 사용되는 버전에 관계없는 클래스로, 일치하는 서비스에 대한 WS-Discovery 정의 조건을 완전히 지원하며 개발자가 일치 작업 중에 사용할 수 있는 사용자 지정 값을 지정하기 위해 사용할 수 있는 확장도 포함하고 있습니다. 개발자는 `Find`를 지정하여 <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 작업에 대한 종료 조건을 제공할 수 있습니다. 이 클래스는 개발자가 검색할 최대 서비스 수를 지정하거나 클라이언트가 응답을 기다리는 기간을 지정하는 값인 <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A>을 지정합니다.  
  
## <a name="findrequestcontext"></a>FindRequestContext  
 <xref:System.ServiceModel.Discovery.FindRequestContext> 클래스는 클라이언트가 `Probe` 작업을 시작할 때 수신되는 `Find` 메시지를 기반으로 검색 서비스에 의해 인스턴스화됩니다. 이 클래스에는 클라이언트가 지정한 <xref:System.ServiceModel.Discovery.FindCriteria>의 인스턴스가 포함되어 있습니다.  
  
## <a name="findresponse"></a>FindResponse  
 <xref:System.ServiceModel.Discovery.FindResponse> 클래스는 <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> 작업의 응답과 함께 `Find`의 호출자에게 반환됩니다. 이 클래스는 <xref:System.ServiceModel.Discovery.FindCompletedEventArgs>에도 제공됩니다. 이 클래스에는 검색된 엔드포인트와 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> 및 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> 사전의 컬렉션인 <xref:System.ServiceModel.Discovery.DiscoveryMessageSequence>의 컬렉션이 포함되어 있습니다.  
  
## <a name="resolvecriteria"></a>ResolveCriteria  
 <xref:System.ServiceModel.Discovery.ResolveCriteria> 클래스는 이미 알려진 서비스를 확인할 때 사용되는 조건을 지정하는 데 사용되는 버전에 관계없는 클래스입니다. 이 클래스에는 알려진 서비스의 엔드포인트 주소가 포함되어 있습니다. 개발자는 <xref:System.ServiceModel.Discovery.ResolveCriteria.Duration%2A>을 지정하여 확인 작업에 대한 종료 조건을 제공할 수 있습니다. 이 클래스는 클라이언트가 응답을 기다리는 기간을 지정합니다.  
  
## <a name="resolveresponse"></a>ResolveResponse  
 <xref:System.ServiceModel.Discovery.ResolveResponse>는 <xref:System.ServiceModel.Discovery.DiscoveryClient.Resolve%2A> 작업의 응답과 함께 `Resolve` 메서드의 호출자에게 반환됩니다. 이 클래스는 <xref:System.ServiceModel.Discovery.ResolveCompletedEventArgs>에도 제공됩니다. 이 클래스에는 검색된 엔드포인트인 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>의 인스턴스와 <xref:System.ServiceModel.Discovery.DiscoveryMessageSequence>의 인스턴스가 포함되어 있습니다.  
  
## <a name="servicediscoverybehavior"></a>ServiceDiscoveryBehavior  
 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> 클래스는 개발자가 검색 기능을 서비스에 추가하는 데 사용됩니다. 이 동작은 <xref:System.ServiceModel.ServiceHost>에 추가됩니다. ph x=&quot;1&quot; /&amp;gt; 클래스는 서비스 호스트에 추가된 애플리케이션 엔드포인트에 대해 반복되고 검색 가능한 엔드포인트에서 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>의 컬렉션을 만듭니다. 모든 엔드포인트는 기본적으로 검색 가능합니다. 원하는 엔드포인트에 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior>를 추가하면 해당 엔드포인트의 검색 기능을 제어할 수 있습니다. <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>에 알림 엔드포인트를 추가하면 서비스 호스트가 열리거나 닫힐 때 검색 가능한 모든 엔드포인트의 알림이 각 알림 엔드포인트를 통해 보내집니다.  
  
## <a name="udpannouncementendpoint"></a>UdpAnnouncementEndpoint  
 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> 클래스는 UDP 멀티캐스트 바인딩을 통한 알림에 대해 미리 구성된 표준 알림 엔드포인트입니다. 기본적으로 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>는 WSApril2005 WS_Discovery 버전을 사용하도록 설정됩니다.  
  
## <a name="udpdiscoveryendpoint"></a>UdpDiscoveryEndpoint  
 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 클래스는 UDP 멀티캐스트 바인딩을 통한 검색에 대해 미리 구성된 표준 검색 엔드포인트입니다. 기본적으로 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>는 WSDiscovery11 WS-Discovery 버전과 <xref:System.ServiceModel.Discovery.ServiceDiscoveryMode.Adhoc?displayProperty=nameWithType> 모드를 사용하도록 설정됩니다.
