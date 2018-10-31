---
title: 네트워크 응용 프로그램에 대한 캐시 관리
ms.date: 03/30/2017
helpviewer_keywords:
- cache [.NET Framework], network applications
- network resources, caching
- Internet, caching
ms.assetid: fc258a40-f370-434f-ae09-4a8cb11ddaeb
ms.openlocfilehash: 265b4e451ebb76dbabe0d3e0df065504a3891f32
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199593"
---
# <a name="cache-management-for-network-applications"></a>네트워크 응용 프로그램에 대한 캐시 관리
이 항목 및 관련 하위 항목에서는 <xref:System.Net.WebClient>, <xref:System.Net.WebRequest>, <xref:System.Net.HttpWebRequest> 및 <xref:System.Net.FtpWebRequest> 클래스를 사용하여 얻은 리소스에 대한 캐싱을 설명합니다.  
  
 캐시는 응용 프로그램에서 요청된 리소스의 임시 저장소를 제공합니다. 응용 프로그램이 동일한 리소스를 두 번 이상 요청하는 경우 캐시에서 리소스를 반환하여 서버에서 다시 요청하는 오버헤드를 방지할 수 있습니다. 캐싱은 요청된 리소스를 가져오는 데 필요한 시간을 줄여 응용 프로그램 성능을 향상시킬 수 있습니다. 또한 캐싱은 서버로의 트립 수를 줄여 네트워크 트래픽을 줄일 수 있습니다. 캐싱은 성능을 개선하지만 응용 프로그램에 반환되는 리소스가 부실할 위험, 즉 캐싱을 사용하지 않을 경우 서버에서 전송될 리소스와 동일하지 않을 위험이 증가합니다.  
  
 캐싱으로 인해 권한 없는 사용자 또는 프로세스가 중요한 데이터를 읽을 수도 있습니다. 캐시된 인증된 응답을 추가 인증 없이 캐시에서 검색할 수 있습니다. 캐싱을 사용하는 경우 <xref:System.Net.WebRequest.CachePolicy%2A>를 <xref:System.Net.Cache.RequestCacheLevel.BypassCache> 또는 <xref:System.Net.Cache.RequestCacheLevel.NoCacheNoStore>로 변경하여 이 요청에 대해 캐싱을 사용하지 않도록 설정합니다.  
  
 보안 문제로 인해 중간 계층 시나리오에는 캐싱이 권장되지 **않습니다**.  
  
## <a name="in-this-section"></a>섹션 내용  
 [캐시 정책](../../../docs/framework/network-programming/cache-policy.md)  
 캐시 정책이란 무엇이고 어떻게 정의하는지를 설명합니다.  
  
 [위치 기반 캐시 정책](../../../docs/framework/network-programming/location-based-cache-policies.md)  
 Hypertext Transfer Protocol(http 및 https) 리소스에 사용 가능한 각 위치 기반 캐시 정책 형식을 정의합니다.  
  
 [시간 기반 캐시 정책](../../../docs/framework/network-programming/time-based-cache-policies.md)  
 시간 기반 캐시 정책을 사용자 지정하는 데 사용할 수 있는 조건을 설명합니다.  
  
 [네트워크 응용 프로그램에서 캐싱 구성](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)  
 프로그래밍 방식으로 캐시 정책 및 캐싱을 사용하는 요청을 만드는 방법을 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Net.Cache>  
 <xref:System.Net.WebRequest>, <xref:System.Net.HttpWebRequest> 및 <xref:System.Net.FtpWebRequest> 클래스를 사용하여 얻은 리소스에 대한 캐시 정책을 정의하는 데 사용되는 형식과 열거형을 정의합니다.
