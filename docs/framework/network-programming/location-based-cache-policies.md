---
title: 위치 기반 캐시 정책
ms.date: 03/30/2017
helpviewer_keywords:
- Cache If Available policy
- reload policy
- location-based cache policies
- Cache Only policy
- local cache
- intermediate cache
- No Cache No Store policy
- cache [.NET Framework], location-based policies
- Revalidate policy
- freshness of cached resources
- Cache Or Next Cache Only policy
- Refresh policy
ms.assetid: e41d7f1a-0a6a-4dee-97d1-c6a8b6a07fc2
ms.openlocfilehash: 1bbaf4fc85fe4d7e3d3737cf62cb63d8e09927cd
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50194412"
---
# <a name="location-based-cache-policies"></a>위치 기반 캐시 정책
위치 기반 캐시 정책은 요청한 리소스를 가져올 수 있는 위치를 기반으로 캐시된 유효한 항목의 새로 고침을 정의합니다. 캐시된 리소스를 사용해도 서버 지정 유효성 재검사 요구 사항을 위반하지 않으면 해당 리소스는 유효합니다. 위치 기반 캐시 정책은 <xref:System.Net.Cache.RequestCachePolicy> 또는 <xref:System.Net.Cache.HttpRequestCachePolicy> 클래스 생성자를 사용하여 프로그래밍 방식으로 만듭니다. 위치 기반 정책 형식은 <xref:System.Net.Cache.RequestCacheLevel> 또는 <xref:System.Net.Cache.HttpRequestCacheLevel> 열거형 값을 사용하여 생성자에 전달됩니다. 위치 기반 캐시 정책을 만드는 코드 예제는 [방법: 응용 프로그램에 대한 위치 기반 캐시 정책 설정](../../../docs/framework/network-programming/how-to-set-a-location-based-cache-policy-for-an-application.md)을 참조하세요. 다음 섹션에서는 Hypertext Transfer Protocol(http 및 https) 리소스를 위한 각각의 위치 기반 캐시 정책 형식을 설명합니다.  
  
## <a name="cache-if-available-policy"></a>사용 가능한 경우 캐시 정책  
 로컬 캐시에 요청된 유효한 리소스가 있으면 캐시된 리소스가 사용되고, 그러지 않으면 리소스 요청이 서버에 전송됩니다. 클라이언트와 서버 사이의 모든 캐시에서 요청된 리소스를 사용할 수 있으면 중간 캐시에서 요청을 만족시킬 수 있습니다.  
  
## <a name="cache-only-policy"></a>캐시 전용 정책  
 로컬 캐시에 요청된 유효한 리소스가 있으면 캐시된 리소스가 사용됩니다. 이 캐시 정책 수준이 지정된 경우 항목이 로컬 캐시에 없으면 <xref:System.Net.WebException> 예외가 throw됩니다.  
  
## <a name="cache-or-next-cache-only-policy"></a>캐시 또는 다음 캐시 전용 정책  
 요청된 유효한 리소스가 로컬 캐시나 Local Area Network의 중간 캐시에 있으면 캐시된 리소스가 사용됩니다. <xref:System.Net.WebException> 예외가 throw됩니다. HTTP 캐싱 프로토콜에서 이 작업은 캐시 전용(only-if-cached) 캐시 제어 지시문을 사용하여 수행합니다.  
  
## <a name="no-cache-no-store-policy"></a>캐시 없이 저장 안 함 정책  
 요청된 리소스는 임의 캐시에서 사용되지 않으며 임의 캐시에 두지 않습니다. 요청된 리소스가 로컬 캐시에 있으면 제거됩니다. 이 정책 수준은 중간 캐시에서도 리소스를 제거해야 함을 나타냅니다. HTTP 캐싱 프로토콜에서 이 작업은 저장 안 함(no-store) 캐시 제어 지시문을 사용하여 수행합니다.  
  
## <a name="refresh-policy"></a>새로 고침 정책  
 요청된 리소스를 서버에서 얻거나 로컬 캐시 이외의 캐시에서 찾은 경우 사용할 수 있습니다. 중간 캐시에서 요청을 만족시키려면 캐시에서 서버를 사용하여 해당 캐시 항목의 유효성을 다시 검증해야 합니다. HTTP 캐싱 프로토콜에서 이 작업은 max-age = 0 캐시 제어 지시문과 캐시 없음(no-cache) Pragma 헤더를 사용하여 수행합니다.  
  
## <a name="reload-policy"></a>다시 로드 정책  
 요청된 리소스는 서버에서 가져와야 합니다. 응답은 로컬 캐시에 저장될 수 있습니다. HTTP 캐싱 프로토콜에서 이 작업은 캐시 없음(no-cache) 캐시 제어 지시문과 캐시 없음(no-cache) Pragma 헤더를 사용하여 수행합니다.  
  
## <a name="revalidate-policy"></a>유효성 다시 검사 정책  
 서버의 복사본과 캐시에 있는 리소스의 복사본을 비교합니다. 서버의 복사본이 최신이면 요청을 처리하는 데 사용하고 캐시의 복사본을 대체합니다. 캐시의 복사본이 서버의 복사본과 동일하면 캐시된 복사본을 사용합니다. HTTP 캐싱 프로토콜에서는 조건부 요청을 사용하여 이 작업을 수행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 응용 프로그램에 대한 캐시 관리](../../../docs/framework/network-programming/cache-management-for-network-applications.md)  
 [캐시 정책](../../../docs/framework/network-programming/cache-policy.md)  
 [시간 기반 캐시 정책](../../../docs/framework/network-programming/time-based-cache-policies.md)  
 [네트워크 응용 프로그램에서 캐싱 구성](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)  
 [\<requestCaching> 요소(네트워크 설정)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)
