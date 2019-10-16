---
title: 캐시 정책
ms.date: 03/30/2017
helpviewer_keywords:
- time-based cache policies
- location-based cache policies
- cache [.NET Framework], policies
- request cache policies
- freshness of cached resources
- content cache policies
- expired content
ms.assetid: 1a7e04ec-7872-41c2-96c6-52566dcb412b
ms.openlocfilehash: 2d3d85ebd80f417ebd0fa0e619097e15f2a6a39b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71048768"
---
# <a name="cache-policy"></a>캐시 정책
캐시 정책이 요청된 리소스의 캐시된 복사본을 통해 요청을 충족할 수 있는지 여부를 결정하는 데 사용되는 규칙을 정의합니다. 애플리케이션에서 새로 고침에 대한 클라이언트 캐시 요구 사항을 지정하지만, 유효한 캐시 정책은 클라이언트 캐시 요구 사항, 서버의 콘텐츠 만료 요구 사항 및 서버의 유효성 재검사 요구 사항에 의해 결정됩니다. 최신 콘텐츠가 클라이언트 애플리케이션에 반환되도록 돕기 위해 클라이언트 캐시 정책 및 서버 요구 사항의 상호 작용 결과로 항상 가장 보수적인 캐시 정책이 생성됩니다.  
  
 캐시 정책은 위치 기반 또는 시간 기반입니다. 위치 기반 캐시 정책은 요청한 리소스를 가져올 수 있는 위치를 기준으로 캐시된 항목의 새로 고침을 정의합니다. 시간 기반 캐시 정책은 리소스가 검색된 시간, 리소스와 함께 반환된 헤더, 현재 시간을 사용하여 캐시된 항목의 새로 고침을 정의합니다. 대부분의 애플리케이션은 [IETF(Internet Engineering Task Force)](https://www.ietf.org/) 웹 사이트에 있는 RFC 2616에 지정된 캐싱 정책을 구현하는 기본 시간 기반 캐시 정책을 사용할 수 있습니다.  
  
 다음 표에 설명된 클래스는 캐시 정책을 지정하는 데 사용됩니다.  
  
|클래스 이름|설명|  
|----------------|-----------------|  
|<xref:System.Net.Cache.HttpRequestCachePolicy>|<xref:System.Net.HttpWebRequest> 개체를 사용하여 요청된 리소스에 대한 위치 기반 및 시간 기반 캐시 정책을 나타냅니다.|  
|<xref:System.Net.Cache.RequestCachePolicy>|<xref:System.Net.Cache.RequestCacheLevel.Default> 개체를 사용하여 요청된 리소스에 대한 위치 기반 캐시 정책 또는 <xref:System.Net.WebRequest> 시간 기반 캐시 정책을 나타냅니다.|  
|<xref:System.Net.Cache.HttpCacheAgeControl>|시간 기반 <xref:System.Net.Cache.HttpRequestCachePolicy> 개체를 만드는 데 사용되는 값을 지정합니다.|  
|<xref:System.Net.Cache.HttpRequestCacheLevel>|위치 기반 및 시간 기반 <xref:System.Net.Cache.HttpRequestCachePolicy> 개체를 만드는 데 사용되는 값을 지정합니다.|  
|<xref:System.Net.Cache.RequestCacheLevel>|위치 기반 또는 <xref:System.Net.Cache.RequestCacheLevel.Default> 시간 기반 <xref:System.Net.Cache.RequestCachePolicy> 개체를 만드는 데 사용되는 값을 지정합니다.|  
  
 애플리케이션에서 만든 모든 요청 또는 개별 요청에 대한 캐시 정책을 정의할 수 있습니다. 애플리케이션 수준 캐시 정책과 요청 수준 캐시 정책을 둘 다 지정하는 경우 요청 수준 정책이 사용됩니다. 프로그래밍 방식으로 또는 애플리케이션 또는 컴퓨터 구성 파일을 사용하여 애플리케이션 수준 캐시 정책을 지정할 수 있습니다. 자세한 내용은 [\<requestCaching> 요소(네트워크 설정)](../configure-apps/file-schema/network/requestcaching-element-network-settings.md)를 참조하세요.  
  
 캐시 정책을 만들려면 <xref:System.Net.Cache.RequestCachePolicy> 또는 <xref:System.Net.Cache.HttpRequestCachePolicy> 클래스 인스턴스를 만들어 정책 개체를 만들어야 합니다. 요청에 정책을 지정하려면 요청의 <xref:System.Net.WebRequest.CachePolicy%2A> 속성을 정책 개체로 설정합니다. 프로그래밍 방식으로 애플리케이션 수준 정책을 설정하는 경우 <xref:System.Net.HttpWebRequest.DefaultCachePolicy%2A> 속성을 정책 개체로 설정합니다.  
  
 캐시 정책을 만들고 사용하는 방법을 보여 주는 코드 예제는 [네트워크 애플리케이션에서 캐싱 구성](configuring-caching-in-network-applications.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [네트워크 애플리케이션에 대한 캐시 관리](cache-management-for-network-applications.md)
- [위치 기반 캐시 정책](location-based-cache-policies.md)
- [시간 기반 캐시 정책](time-based-cache-policies.md)
- [네트워크 애플리케이션에서 캐싱 구성](configuring-caching-in-network-applications.md)
