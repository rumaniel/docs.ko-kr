---
title: 시간 기반 캐시 정책
ms.date: 03/30/2017
helpviewer_keywords:
- time-based cache policies
- cache synchronization date policy
- cache [.NET Framework], time-based policies
- freshness of cached resources
- time, cached resources
- maximum age policy
- synchronization, cache
- staleness of cached resources
- default time-based cache policy
- maximum staleness policy
- content cache policies
- expired content
- minimum freshness policy
- age of cached resources
ms.assetid: 74f0bcaf-5c95-40c1-9967-f3bbf1d2360a
ms.openlocfilehash: 0edde8e716d5ce3b1444e994234def5835341475
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71047121"
---
# <a name="time-based-cache-policies"></a>시간 기반 캐시 정책
시간 기반 캐시 정책은 리소스가 검색된 시간, 리소스와 함께 반환된 헤더, 현재 시간을 사용하여 캐시된 항목의 새로 고침을 정의합니다. 시간 기반 캐시 정책을 설정하는 경우 <xref:System.Net.Cache.HttpRequestCacheLevel.Default> 시간 기반 정책을 사용하거나 사용자 지정 시간 기반 정책을 만들 수 있습니다. HTTP(Hypertext Transfer Protocol)를 사용하여 얻은 리소스에 대한 기본 시간 기반 정책을 사용하는 경우 정확한 캐시 동작은 [IETF(Internet Engineering Task Force)](https://www.ietf.org/) 웹 사이트에 있는 RFC 2616의 섹션 13 및 14에 지정된 동작 및 캐시된 응답에 포함된 헤더에 의해 결정됩니다. HTTP 리소스에 대한 기본 시간 기반 정책을 설정하는 방법을 보여 주는 코드 예제는 [방법: 애플리케이션의 기본 시간 기반 캐시 정책 설정](how-to-set-the-default-time-based-cache-policy-for-an-application.md)을 참조하세요. 캐시 정책을 만들고 사용하는 방법을 보여 주는 코드 예제는 [네트워크 애플리케이션에서 캐싱 구성](configuring-caching-in-network-applications.md)을 참조하세요.  
  
## <a name="criteria-to-determine-freshness-of-cached-entries"></a>캐시된 항목의 새로 고침을 결정하는 조건  
 시간 기반 캐시 정책을 사용자 지정하려면 다음 조건 중 하나 이상을 사용하여 캐시된 항목의 새로 고침을 결정하도록 지정할 수 있습니다.  
  
- 최대 보존 기간  
  
- 최대 부실  
  
- 최소 새로 고침  
  
- 캐시 동기화 날짜  
  
> [!NOTE]
> 기본 시간 기반 캐시 정책 사용과 애플리케이션에 대한 기본 캐시 정책 설정을 혼동하면 안 됩니다. 기본 시간 기반 정책은 요청 또는 애플리케이션 수준에서 사용할 수 있는 특정 정책입니다. 애플리케이션에 대한 기본 캐시 정책은 요청에 설정된 정책이 없는 경우 적용되는 정책(위치 기반 또는 시간 기반)입니다. 애플리케이션에 대한 기본 캐시 정책을 설정하는 방법에 대한 자세한 내용은 <xref:System.Net.WebRequest.DefaultCachePolicy%2A>를 참조하세요.  
  
### <a name="maximum-age"></a>최대 보존 기간  
 최대 보존 기간 정책 조건은 리소스의 캐시된 복사본을 사용할 수 있는 시간을 지정합니다. 리소스의 캐시된 복사본이 지정된 시간보다 오래된 경우 서버 콘텐츠와 비교해서 확인하여 리소스의 유효성을 재검사해야 합니다. 최대 보존 기간이 만료된 리소스를 사용할 수 있도록 허용하는 경우 최대 부실 값도 지정하지 않으면 이 조건은 적용되지 않습니다.  
  
### <a name="maximum-staleness"></a>최대 부실  
 최대 부실 정책 조건은 리소스의 캐시된 복사본을 사용할 수 있는 콘텐츠 만료 후의 기간을 지정합니다. 만료된 리소스를 사용할 수 있도록 허용하는 유일한 캐시 정책 조건입니다.  
  
### <a name="minimum-freshness"></a>최소 새로 고침  
 최소 새로 고침 정책 조건은 리소스의 캐시된 복사본을 사용할 수 있는 콘텐츠 만료 전의 기간을 지정합니다. 이 정책은 캐시 항목이 만료 날짜 전에 만료되도록 하므로 최소 새로 고침 및 최대 부실 설정은 함께 사용할 수 없습니다.  
  
## <a name="cache-synchronization-date"></a>캐시 동기화 날짜  
 캐시 동기화 날짜 정책 조건은 서버 콘텐츠와 비교해서 확인하여 리소스의 캐시된 복사본 유효성을 재검사해야 하는 시기를 결정합니다. 항목이 캐시된 이후 콘텐츠가 변경된 경우 서버에서 검색되어 캐시에 저장된 다음 애플리케이션에 반환됩니다. 콘텐츠가 변경되지 않은 경우 해당 타임스탬프가 업데이트되고 애플리케이션이 캐시된 콘텐츠를 가져옵니다.  
  
 캐시 동기화 날짜를 사용하면 캐시된 콘텐츠의 유효성을 검사해야 하는 절대 날짜를 지정할 수 있습니다. 캐시 동기화 날짜 전에 새 캐시 항목의 유효성을 마지막으로 검사한 경우에도 서버와 유효성 검사가 다시 수행됩니다. 캐시 동기화 날짜 이후에 캐시 항목의 유효성이 재검사되었으며 캐시된 항목을 무효화하는 추가 새로 고침 또는 서버 유효성 재검사 요구 사항이 없는 경우 캐시의 항목이 사용됩니다. 캐시 동기화 날짜가 미래의 특정 날짜로 설정된 경우 캐시 동기화 날짜가 지날 때까지 요청될 때마다 항목의 유효성이 재검사됩니다.  
  
 다음 항목에서는 시간 기반 캐시 정책 조건을 결합한 결과에 대한 정보를 제공합니다.  
  
- [캐시 정책 조작 -최대 사용 기간 및 최대 부실](cache-policy-interaction-maximum-age-and-maximum-staleness.md)  
  
- [캐시 정책 상호 작용 - 최대 보존 기간 및 최소 새로 고침](cache-policy-interaction-maximum-age-and-minimum-freshness.md)  
  
## <a name="see-also"></a>참고 항목

- [네트워크 애플리케이션에 대한 캐시 관리](cache-management-for-network-applications.md)
- [캐시 정책](cache-policy.md)
- [위치 기반 캐시 정책](location-based-cache-policies.md)
- [네트워크 애플리케이션에서 캐싱 구성](configuring-caching-in-network-applications.md)
- [\<requestCaching> 요소(네트워크 설정)](../configure-apps/file-schema/network/requestcaching-element-network-settings.md)
