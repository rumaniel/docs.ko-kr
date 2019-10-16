---
title: <endpointExtensions>
ms.date: 03/30/2017
ms.assetid: 33396e0a-1fae-4616-b822-923584eebfd1
ms.openlocfilehash: fe57cb84cfa70b1f6b92abf1dbac89ddad9d4dc8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925704"
---
# <a name="endpointextensions"></a>\<endpointExtensions>
이 섹션에서는 새 표준 엔드포인트를 컴퓨터 또는 애플리케이션 구성 파일의 extensions 섹션에 등록합니다. `add` 키워드를 사용하고 요소의 `type` 특성을 해당 엔드포인트 형식으로 설정하고, `name` 특성을 표준 엔드포인트의 이름으로 설정하여 표준 엔드포인트를 이 컬렉션에 추가할 수 있습니다.  
  
 다음 예제에서는 `add` 요소와 `name` 특성을 사용하여 구성 파일의 `<endpointExtensions>` 섹션에 표준 엔드포인트를 추가합니다.  
  
```xml  
<system.serviceModel>
  <extensions>
    <endpointExtensions>
      <add name="udpDiscoveryEndpoint"
           type="System.Discovery.UdpEndpointCollectionElement, System.Discovery.dll, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ffffffffffffffff"/>
    </endpointExtensions>
  </extensions>
</system.serviceModel>
```  
  
 표준 엔드포인트를 등록한 다음 이를 다음 예제와 같이 사용할 수 있습니다. 끝점 > 요소에서 특성은 `kind` `<endpointExtensions>` 섹션에 등록 된 표준 끝점 형식을 지정 합니다. [ \<](endpoint-element.md) 특성 `endpointConfiguration` 은 섹션의`<standardEndpoints>` 표준 끝점에 `name` 대 한 구성 요소의 특성과 동일 합니다.  
  
```xml  
<system.serviceModel>
  <services>
    <service name="Service1">
      <endpoint kind="udpDiscoveryEndpoint"
                endpointConfiguration="udpConfig" />
    </service>
  </services>
  <standardEndpoints>
    <udpDiscoveryEndpoint>
      <standardEndpoint name="udpConfig"
                        multicastAddress="soap.udp://239.255.255.250:3703"
                        ... />
    </udpDiscoveryEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
