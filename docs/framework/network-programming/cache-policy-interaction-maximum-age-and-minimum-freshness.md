---
title: 캐시 정책 상호 작용 - 최대 보존 기간 및 최소 새로 고침
ms.date: 03/30/2017
helpviewer_keywords:
- time-based cache policies
- Revalidate policy
- cache [.NET Framework], time-based policies
- freshness of cached resources
- maximum age policy
- minimum freshness policy
- age of cached resources
ms.assetid: 6567d451-ecec-496c-95a3-a415b99ba52a
ms.openlocfilehash: eab50c308441ce73e994313d009588559302671e
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199320"
---
# <a name="cache-policy-interactionmaximum-age-and-minimum-freshness"></a>캐시 정책 상호 작용 - 최대 보존 기간 및 최소 새로 고침
최신 콘텐츠가 클라이언트 응용 프로그램에 반환되도록 돕기 위해 클라이언트 캐시 정책 및 서버 유효성 재검사 요구 사항의 상호 작용 결과로 항상 가장 보수적인 캐시 정책이 생성됩니다. 이 항목의 모든 예제에서는 1월 1일에 캐시되었으며 1월 4일에 만료되는 리소스에 대한 캐시 정책을 보여 줍니다.  
  
 다음 예제에서는 최대 사용 기간(`maxAge`) 및 최소 새로 고침(`minFresh`) 값의 상호 작용 결과로 생성되는 캐시 정책을 설명합니다.  
  
-   캐시 정책이 `maxAge` = 2일을 설정하고 `minFresh`를 지정하지 않을 경우 1월 3일에 콘텐츠 유효성이 재검사됩니다.  
  
-   캐시 정책이 `maxAge` = 2일, `minFresh` = 1일을 설정하는 경우 `maxAge`에 따라 1월 3일까지 콘텐츠가 최신 상태입니다. `minFresh`에 따라 콘텐츠가 1월 3일까지 최신 상태입니다. 따라서 1월 3일에 콘텐츠 유효성을 재검사해야 합니다.  
  
-   캐시 정책이 `maxAge` = 2일, `minFresh` = 2일을 설정하는 경우 `maxAge`에 따라 1월 3일까지 콘텐츠가 최신 상태입니다. `minFresh`에 따라 콘텐츠가 1월 2일까지 최신 상태입니다. 따라서 1월 2일에 콘텐츠 유효성을 재검사해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 응용 프로그램에 대한 캐시 관리](../../../docs/framework/network-programming/cache-management-for-network-applications.md)  
 [캐시 정책](../../../docs/framework/network-programming/cache-policy.md)  
 [위치 기반 캐시 정책](../../../docs/framework/network-programming/location-based-cache-policies.md)  
 [시간 기반 캐시 정책](../../../docs/framework/network-programming/time-based-cache-policies.md)  
 [네트워크 응용 프로그램에서 캐싱 구성](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)  
 [캐시 정책 조작 -최대 사용 기간 및 최대 부실](../../../docs/framework/network-programming/cache-policy-interaction-maximum-age-and-maximum-staleness.md)
