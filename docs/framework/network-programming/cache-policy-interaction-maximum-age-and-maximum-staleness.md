---
title: 캐시 정책 조작 -최대 사용 기간 및 최대 부실
ms.date: 03/30/2017
helpviewer_keywords:
- maximum staleness
- freshness of cached resources
- time, cached resources
- maximum age policy
- staleness of cached resources
- age of cached resources
ms.assetid: 7f775925-89a1-4956-ba90-c869c1749a94
ms.openlocfilehash: 7a066f403e526c50054b58a099bb7978ef57e74d
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50181149"
---
# <a name="cache-policy-interactionmaximum-age-and-maximum-staleness"></a>캐시 정책 조작 -최대 사용 기간 및 최대 부실
최신 콘텐츠가 클라이언트 응용 프로그램에 반환되도록 돕기 위해 클라이언트 캐시 정책 및 서버 유효성 재검사 요구 사항의 상호 작용 결과로 항상 가장 보수적인 캐시 정책이 생성됩니다. 이 항목의 모든 예제에서는 1월 1일에 캐시되었으며 1월 4일에 만료되는 리소스에 대한 캐시 정책을 보여 줍니다.  
  
 다음 예제에서는 최대 부실 값(`maxStale`)이 최대 사용 기간(`maxAge`)과 함께 사용됩니다.  
  
-   캐시 정책이 `maxAge` = 5일을 설정하고 `maxStale` 값을 지정하지 않을 경우 `maxAge` 값에 따라 1월 6일까지 콘텐츠를 사용할 수 있습니다. 그러나 서버의 유효성 재검사 요구 사항에 따라 콘텐츠가 1월 4일에 만료됩니다. 콘텐츠 만료 날짜가 더 보수적이기(더 빠르기) 때문에 `maxAge` 정책보다 우선 적용됩니다. 따라서 콘텐츠는 1월 4일에 만료되고 최대 사용 기간에 도달하지 않았지만 유효성을 재검사해야 합니다.  
  
-   캐시 정책이 `maxAge` = 5일, `maxStale` = 3일을 설정하는 경우 `maxAge` 값에 따라 1월 6일까지 콘텐츠를 사용할 수 있습니다. `maxStale` 값에 따라 콘텐츠를 1월 7일까지 사용할 수 있습니다. 따라서 콘텐츠는 1월 6일에 유효성이 재검사됩니다.  
  
-   캐시 정책이 `maxAge` = 5일, `maxStale` = 1일을 설정하는 경우 `maxAge` 값에 따라 1월 6일까지 콘텐츠를 사용할 수 있습니다. `maxStale` 값에 따라 콘텐츠를 1월 5일까지 사용할 수 있습니다. 따라서 1월 5일에 콘텐츠 유효성이 재검사됩니다.  
  
 최대 사용 기간이 콘텐츠 만료 날짜보다 이전이면 보다 보수적인 캐싱 동작이 항상 우선 적용되고 최대 부실 값은 영향을 주지 않습니다. 다음 예제에서는 콘텐츠가 만료되기 전에 최대 사용 기간(`maxAge`)에 도달할 경우 최대 부실(`maxStale`) 값을 설정할 경우의 영향을 보여 줍니다.  
  
-   캐시 정책이 `maxAge` = 1일을 설정하고 `maxStale` 값을 지정하지 않을 경우 콘텐츠가 만료되지 않았어도 1월 2일에 유효성이 재검사됩니다.  
  
-   캐시 정책이 `maxAge` = 1일, `maxStale` = 3일을 설정하는 경우 보다 보수적인 정책 설정을 적용하기 위해 1월 2일에 콘텐츠 유효성이 재검사됩니다.  
  
-   캐시 정책이 `maxAge` = 1일, `maxStale` = 1일을 설정하는 경우 1월 2일에 콘텐츠 유효성이 재검사됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 응용 프로그램에 대한 캐시 관리](../../../docs/framework/network-programming/cache-management-for-network-applications.md)  
 [캐시 정책](../../../docs/framework/network-programming/cache-policy.md)  
 [위치 기반 캐시 정책](../../../docs/framework/network-programming/location-based-cache-policies.md)  
 [시간 기반 캐시 정책](../../../docs/framework/network-programming/time-based-cache-policies.md)  
 [네트워크 응용 프로그램에서 캐싱 구성](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)  
 [캐시 정책 상호 작용 - 최대 보존 기간 및 최소 새로 고침](../../../docs/framework/network-programming/cache-policy-interaction-maximum-age-and-minimum-freshness.md)
