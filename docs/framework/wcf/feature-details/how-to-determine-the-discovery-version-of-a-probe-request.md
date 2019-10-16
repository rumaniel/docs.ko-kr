---
title: '방법: 프로브 요청의 검색 버전 확인'
ms.date: 03/30/2017
ms.assetid: b3c4e2e2-2957-4074-ae6a-776a5ca84278
ms.openlocfilehash: 8fbc3936278a5c6f403f48b59390c69c64378004
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425263"
---
# <a name="how-todetermine-the-discovery-version-of-a-probe-request"></a>방법: 프로브 요청의 검색 버전 확인

검색 프록시는 여러 검색 버전을 사용하여 검색 엔드포인트를 노출할 수 있습니다. Udp 멀티 캐스트 프로브 요청이 프록시에 도착, 프록시는 멀티 캐스트 비 표시 오류 메시지를 사용 하 여 응답 해야 합니다. 이 작업을 수행 하기 위해 했을 때 요청의 검색 버전을 알아야 합니다.

## <a name="to-determine-the-discovery-version-of-a-probe-request"></a>프로브 요청의 검색 버전을 확인하려면

프로브 요청에 응답 하는 방법에 (예를 들어 <xref:System.ServiceModel.Discovery.DiscoveryProxy.OnBeginFind%2A?displayProperty=nameWithType>) 정적을 사용 하 여 <xref:System.ServiceModel.OperationContext.Current%2A?displayProperty=nameWithType> 검색할 속성을 <xref:System.ServiceModel.Discovery.DiscoveryOperationContextExtension>다음 코드에 표시 된 것 처럼 합니다.

```csharp
DiscoveryOperationContextExtension doce = OperationContext.Current.Extensions.Find<DiscoveryOperationContextExtension>();
// Access the discovery version from the DiscoveryOperationContextExtension
doce.DiscoveryVersion;
```

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Discovery.Configuration.AnnouncementEndpointElement.DiscoveryVersion%2A>
- [검색 프록시 구현](../../../../docs/framework/wcf/feature-details/implementing-a-discovery-proxy.md)
