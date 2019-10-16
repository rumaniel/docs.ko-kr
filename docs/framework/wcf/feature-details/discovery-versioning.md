---
title: 검색 버전 관리
ms.date: 03/30/2017
ms.assetid: f91c6d0a-3af2-45c5-9a5c-e75390619836
ms.openlocfilehash: 4a1ca07fc6773ce6f883d654abfedab4986341e1
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425250"
---
# <a name="discovery-versioning"></a>검색 버전 관리

이 항목에서는 일부 새 검색 기능의 구현에 대해 간략하게 설명하고 사용할 검색 버전을 선택하는 방법에 대해서도 간략하게 설명합니다.

## <a name="discovery-versioning"></a>검색 버전 관리

검색 기능은 세 가지 버전의 WS_Discovery 프로토콜을 지원합니다. 검색 API를 사용하면 사용할 프로토콜 버전을 선택할 수 있습니다. 이 문서에서는 버전 관리 관련 설정에 대해 간략하게 설명합니다.

다음은 <xref:System.ServiceModel.Discovery.DiscoveryVersion> 속성을 포함하고 있고 해당 생성자에 <xref:System.ServiceModel.Discovery.DiscoveryVersion> 인수를 사용하는 검색 클래스입니다.

- <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>

- <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>

- <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>

- <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>

### <a name="discoveryversionwsdiscoveryapril2005"></a>DiscoveryVersion.WSDiscoveryApril2005

제공 <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryApril2005> 생성자 매개 변수는 Ws-discovery 프로토콜의 April2005 버전을 사용 하 여 구현 합니다. 이 버전은 WS-Discovery 프로토콜 사양의 게시된 버전에 해당합니다. WS-Discovery의 April2005 버전을 사용하는 레거시 애플리케이션과 상호 운용하려면 이 버전을 사용해야 합니다.

### <a name="discoveryversionwsdiscovery11"></a>DiscoveryVersion.WSDiscovery11

기본 검색 Api에서 사용 되는 버전이 <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscovery11>합니다. 이 버전은 WS-Discovery 프로토콜의 현재 표준화된 버전입니다.

## <a name="discoveryversionwsdiscoverycd1"></a>DiscoveryVersion.WSDiscoveryCD1

<xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryCD1>을 생성자 매개 변수로 제공하면 구현 시 WS-Discovery 프로토콜의 committee draft 1 버전이 사용됩니다. WS-Discovery 프로토콜의 CD1 버전을 실행하는 구현과 상호 운용하려면 이 버전의 프로토콜을 사용해야 합니다.

## <a name="supporting-multiple-udp-discovery-endpoints-for-different-discovery-versions-on-a-single-service-host"></a>단일 서비스 호스트에서 다양한 검색 버전에 대해 여러 개의 UDP 검색 엔드포인트 지원

단일 서비스 호스트에서 다양한 검색 버전에 대해 여러 개의 UDP 검색 엔드포인트를 노출할 수 있습니다. 이렇게 하려면 각 UDP 검색 엔드포인트에 고유한 주소를 지정해야 합니다. 다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.

```csharp
UdpDiscoveryEndpoint newVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscovery11);
UdpDiscoveryEndpoint oldVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);

newVersionUdpEndpoint.Address = new EndpointAddress(newVersionUdpEndpoint.Address.Uri.ToString() + "/version11");
oldVersionUdpEndpoint.Address = new EndpointAddress(oldVersionUdpEndpoint.Address.Uri.ToString() + "/versionApril2005");

serviceHost.AddServiceEndpoint(newVersionUdpEndpoint);
serviceHost.AddServiceEndpoint(oldVersionUdpEndpoint);
```
