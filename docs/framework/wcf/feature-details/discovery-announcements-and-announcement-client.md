---
title: 검색 알림 및 알림 클라이언트
ms.date: 03/30/2017
ms.assetid: 426c6437-f8d2-4968-b23a-18afd671aa4b
ms.openlocfilehash: 4ad0b3ea5c257fa3117c426391bd59ad7b560d4f
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040175"
---
# <a name="discovery-announcements-and-announcement-client"></a>검색 알림 및 알림 클라이언트

WCF 검색 기능을 사용 하면 구성 요소에서 해당 가용성을 알릴 수 있습니다. 이렇게 구성된 경우 서비스는 Hello 및 Bye 알림을 보냅니다. 클라이언트 또는 기타 구성 요소는 이러한 알림 메시지를 수신 대기하고 이에 대해 동작을 수행할 수 있습니다. 이 기능은 클라이언트가 서비스를 인식하는 또 다른 방법을 제공합니다. 알림 기능은 여러 가지 용도로 사용됩니다. 예를 들어 서비스가 빈번하게 네트워크에 들어왔다가 나가는 경우 알림을 사용하는 것이 서비스를 검색하는 것보다 더 효율적일 수 있습니다. 이 방법을 사용하면 네트워크 트래픽이 줄어들고 클라이언트가 알림을 받는 즉시 해당 서비스가 있는지 여부를 알 수 있습니다.

## <a name="discovery-announcements"></a>검색 알림

알림을 받도록 구성된 서비스는 네트워크에 연결되어 검색 가능한 상태가 되면 수신 대기 중인 클라이언트에 자신의 가용성을 알리는 Hello 메시지를 보냅니다. 이 메시지에는 계약, 엔드포인트 주소, 연결된 범위 등 서비스에 대한 검색 관련 정보가 포함됩니다. <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> 클래스를 사용하면 알림 메시지를 보낼 위치를 지정할 수 있습니다. 알림 엔드포인트가 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>이면 Hello 및 Bye가 적절히 멀티캐스트됩니다. 그러나 알림 엔드포인트가 유니캐스트이면 메시지가 지정된 엔드포인트에 직접 보내집니다.

> [!NOTE]
> 알림은 서비스 호스트가 열리고 닫힐 때 보내집니다. 이러한 호출이 올바로 완료되지 않으면 알림 메시지가 보내지지 않을 수 있습니다. 예를 들어 서비스에서 오류가 발생해도 Bye 알림 메시지가 보내지지 않습니다.

> [!TIP]
> 선택할 때마다 알림을 보낼 수 있도록 알림 기능을 사용자 지정할 수 있습니다.

[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]에서는 서비스와 클라이언트에서 손쉽게 Hello 및 Bye 알림을 보낼 수 있도록 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> 및 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>를 표준 엔드포인트로 정의합니다.

### <a name="announcements-on-the-service"></a>서비스에서의 알림

알림을 보내도록 서비스를 구성하려면 알림 엔드포인트를 사용하여 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>를 추가합니다. 다음 예제에서는 프로그래밍 방식으로 이 동작을 서비스 호스트에 추가하는 방법을 보여 줍니다. 이 예제에서는 `UdpAnnouncementEndpoint`를 사용하여 알림이 해당 표준 엔드포인트에 의해 지정된 위치에 멀티캐스트되도록 합니다.

```csharp
ServiceDiscoveryBehavior serviceDiscoveryBehavior = new ServiceDiscoveryBehavior();
serviceDiscoveryBehavior.AnnouncementEndpoints.Add(new UdpAnnouncementEndpoint());
serviceHost.Description.Behaviors.Add(serviceDiscoveryBehavior);
```

다음 예제와 같이 구성 파일에서 동작을 구성할 수도 있습니다.

```xml
<services>
  <service behaviorConfiguration="CalculatorBehavior" name="Microsoft.Samples.Discovery.CalculatorService">
    <!--Add Discovery Endpoint-->
    <endpoint name="udpDiscoveryEpt" kind="udpDiscoveryEndpoint" />
  </service>
</services>
<behaviors>
  <serviceBehaviors>
    <behavior name="CalculatorBehavior">
      <!--Add Discovery behavior-->
      <serviceDiscovery>
        <announcementEndpoints>
          <endpoint kind="udpAnnouncementEndpoint" />
        </announcementEndpoints>
      </serviceDiscovery>
    </behavior>
  </serviceBehaviors>
</behaviors>
```

위의 예제에서는 자동으로 알림 메시지를 보내도록 서비스를 구성했지만 <xref:System.ServiceModel.Discovery.AnnouncementClient> 클래스를 사용하여 알림 메시지를 명시적으로 보낼 수도 있습니다.

### <a name="announcements-on-the-client"></a>클라이언트에서의 알림

클라이언트 애플리케이션에서는 Hello 및 Bye 메시지에 응답하고 <xref:System.ServiceModel.Discovery.AnnouncementService.OnlineAnnouncementReceived> 및 <xref:System.ServiceModel.Discovery.AnnouncementService.OfflineAnnouncementReceived> 이벤트를 구독할 수 있도록 알림 서비스를 호스팅해야 합니다. 다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.

```csharp
// Create an AnnouncementService instance
AnnouncementService announcementService = new AnnouncementService();

// Subscribe the announcement events
announcementService.OnlineAnnouncementReceived += OnOnlineEvent;
announcementService.OfflineAnnouncementReceived += OnOfflineEvent;

// Create ServiceHost for the AnnouncementService
using (ServiceHost announcementServiceHost = new ServiceHost(announcementService))
{
    // Listen for the announcements sent over UDP multicast
    announcementServiceHost.AddServiceEndpoint(new UdpAnnouncementEndpoint());
    announcementServiceHost.Open();

    Console.WriteLine("Press <ENTER> to terminate.");
    Console.ReadLine();
}
```

Hello 또는 Bye 메시지를 받으면 다음 예제와 같이 <xref:System.ServiceModel.Discovery.AnnouncementEventArgs>를 통해 엔드포인트 검색 메타데이터에 액세스할 수 있습니다.

```csharp
static void OnOnlineEvent(object sender, AnnouncementEventArgs e)
{
    Console.WriteLine("Received an online announcement from {0}",
e.EndpointDiscoveryMetadata.Address);
}

static void OnOfflineEvent(object sender, AnnouncementEventArgs e)
{
    Console.WriteLine("Received an offline announcement from {0}",
e.EndpointDiscoveryMetadata.Address);
}
```
