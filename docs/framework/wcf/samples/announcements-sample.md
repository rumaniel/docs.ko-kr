---
title: 알림 샘플
ms.date: 03/30/2017
ms.assetid: 954a75e4-9a97-41d6-94fc-43765d4205a9
ms.openlocfilehash: 1acf51ebe36872424be1e0fdda65a7d18aa737f2
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045790"
---
# <a name="announcements-sample"></a>알림 샘플

이 샘플에서는 검색 기능의 알림 기능을 사용하는 방법을 보여 줍니다. 서비스에서는 알림을 사용하여 서비스에 대한 메타데이터가 들어 있는 알림 메시지를 보낼 수 있습니다. 기본적으로 서비스가 시작될 때는 Hello 알림이 보내지고 서비스가 종료될 때는 Bye 알림이 보내집니다. 이러한 알림은 멀티캐스트하거나 지점 간에 보낼 수 있습니다. 이 샘플은 서비스와 클라이언트에 해당하는 두 개의 프로젝트로 구성되어 있습니다.

## <a name="service"></a>서비스

이 프로젝트에는 자체 호스팅 계산기 서비스가 들어 있습니다. `Main` 메서드에서는 서비스 호스트가 만들어지고 이 서비스 호스트에 서비스 엔드포인트가 추가됩니다. 그런 다음 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>가 만들어집니다. 알림을 사용하도록 설정하려면 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>에 알림 엔드포인트를 추가해야 합니다. 이 경우 UDP 멀티캐스트를 사용하는 표준 엔드포인트가 알림 엔드포인트로 추가됩니다. 이 끝점에서는 잘 알려진 UDP 주소를 통해 알림을 브로드캐스팅합니다.

```csharp
Uri baseAddress = new Uri("http://localhost:8000/" + Guid.NewGuid().ToString());

// Create a ServiceHost for the CalculatorService type.
using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))
{
     serviceHost.AddServiceEndpoint(typeof(ICalculatorService), new WSHttpBinding(), String.Empty);

     ServiceDiscoveryBehavior serviceDiscoveryBehavior = new ServiceDiscoveryBehavior();

     // Announce the availability of the service over UDP multicast
    serviceDiscoveryBehavior.AnnouncementEndpoints.Add(new UdpAnnouncementEndpoint());

    // Make the service discoverable over UDP multicast.
    serviceHost.Description.Behaviors.Add(serviceDiscoveryBehavior);
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());
    serviceHost.Open();
    // ...
}
```

## <a name="client"></a>클라이언트

이 프로젝트에서는 클라이언트가 <xref:System.ServiceModel.Discovery.AnnouncementService>를 호스팅합니다. 또한 두 개의 대리자가 이벤트에 등록됩니다. 이러한 이벤트는 온라인 및 오프라인 알림을 받을 때 클라이언트에서 수행하는 작업을 나타냅니다.

```csharp
// Create an AnnouncementService instance
AnnouncementService announcementService = new AnnouncementService();

// Subscribe the announcement events
announcementService.OnlineAnnouncementReceived += OnOnlineEvent;
announcementService.OfflineAnnouncementReceived += OnOfflineEvent;
```

`OnOnlineEvent` 및 `OnOfflineEvent` 메서드는 각각 Hello 알림과 Bye 알림을 처리합니다.

```csharp
static void OnOnlineEvent(object sender, AnnouncementEventArgs e)
{
    Console.WriteLine();
    Console.WriteLine("Received an online announcement from {0}:", e.AnnouncementMessage.EndpointDiscoveryMetadata.Address);
PrintEndpointDiscoveryMetadata(e.AnnouncementMessage.EndpointDiscoveryMetadata);
}

static void OnOfflineEvent(object sender, AnnouncementEventArgs e)
{
    Console.WriteLine();
    Console.WriteLine("Received an offline announcement from {0}:", e.AnnouncementMessage.EndpointDiscoveryMetadata.Address);
            PrintEndpointDiscoveryMetadata(e.AnnouncementMessage.EndpointDiscoveryMetadata);
}
```

#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1. 이 샘플에서는 HTTP 끝점을 사용 하며이 샘플을 실행 하려면 적절 한 URL Acl을 추가 해야 합니다. 자세한 내용은 [http 및 HTTPS 구성](https://go.microsoft.com/fwlink/?LinkId=70353) 을 참조 하세요. 높은 권한으로 다음 명령을 실행하면 적절한 ACL이 추가됩니다. 명령이 지정한 대로 작동하지 않는 경우 다음 인수의 도메인과 사용자 이름을 대체할 수 있습니다. `netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%`

2. 솔루션을 빌드합니다.

3. client.exe 응용 프로그램을 실행합니다.

4. service.exe 응용 프로그램을 실행합니다. 그러면 클라이언트에서는 온라인 알림을 받습니다.

5. service.exe 응용 프로그램을 닫습니다. 그러면 클라이언트에서는 오프라인 알림을 받습니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\Announcements`
