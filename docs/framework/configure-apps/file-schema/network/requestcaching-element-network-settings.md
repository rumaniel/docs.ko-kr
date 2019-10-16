---
title: <requestCaching> 요소(네트워크 설정)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#requestCaching
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching
helpviewer_keywords:
- requestCaching element
- <requestCaching> element
ms.assetid: 9962a2fe-cbda-41a6-9377-571811eaea84
ms.openlocfilehash: f0979d2e0caeb0b22b90572aef0ad53235020f1d
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697834"
---
# <a name="requestcaching-element-network-settings"></a>\<requestCaching> 요소(네트워크 설정)
네트워크 요청에 대 한 캐싱 메커니즘을 제어 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4c.net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t **\<requestCaching >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<requestCaching  
  isPrivateCache ="true|false"  
  disableAllCaching="true|false"  
  defaultPolicyLevel="BypassCache|Default|CacheOnly|CacheIfAvailable|Revalidate|Reload|NoCacheNoStore|Revalidate"  
  unspecifiedMaximumAge= "d.hh.mm.ss">  
    <defaultHttpCachePolicy>...</defaultHttpCachePolicy>  
    <defaultFtpCachePolicy>...</defaultFtpCachePolicy>  
</requestCaching>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`isPrivateCache`|캐시에서 다른 사용자의 정보를 격리 하는지 여부를 지정 합니다. 기본값은 `true`입니다. 중간 계층 응용 프로그램의 경우이 값은 0 @no__t 이어야 합니다.|  
|`disableAllCaching`|모든 웹 응답에 대해 캐싱이 사용 되지 않도록 지정 하 고 프로그래밍 방식으로 재정의할 수 없도록 지정 합니다.|  
|`defaultPolicyLevel`|<xref:System.Net.Cache.RequestCacheLevel> 열거형에 값 중 하나입니다. 기본값은 `BypassCache`입니다.|  
|`unspecifiedMaximumAge`|콘텐츠가 만료 된 것으로 표시 되는 기본 시간을 지정 합니다.|  
  
## <a name="policylevel-attribute"></a>policyLevel 특성  
  
|값|설명|  
|-----------|-----------------|  
|`Default`|리소스 새로 고침, 콘텐츠 길이 정확 하 고, 이며 만료, 수정 및 콘텐츠 길이 특성이 있는 경우 캐시 된 리소스를 반환 합니다.|  
|`BypassCache`|서버에서 리소스를 반환합니다.|  
|`CacheOnly`|콘텐츠 길이가 있고 항목 크기와 일치 하는 경우 캐시 된 리소스를 반환 합니다.|  
|`CacheIfAvailable`|콘텐츠 길이 제공 하는 크기와 일치 항목; 경우 캐시 된 리소스를 반환 합니다. 그렇지 않은 경우 리소스 서버에서 다운로드 되 고 호출자에 게 반환 됩니다.|  
|`Revalidate`|캐시 된 리소스의 타임 스탬프가 서버에 있는 리소스의 타임 스탬프와 동일한 경우 캐시 된 리소스를 반환 합니다. 그렇지 않으면 리소스가 서버에서 다운로드 되어 캐시에 저장 되며 호출자에 게 반환 됩니다.|  
|`Reload`|서버에서 리소스를 다운로드, 캐시에 저장 하 고 호출자에 게 리소스를 반환 합니다.|  
|`NoCacheNoStore`|캐시 된 리소스가 있는 경우 삭제 됩니다. 리소스는 서버에서 다운로드 되 고 호출자에 게 반환 됩니다.|  
|`Revalidate`|타임 스탬프가 서버의 리소스 타임 스탬프와 동일한 경우 캐시 된 리소스 복사본을 사용 하 여 요청을 만족 시킵니다. 그렇지 않으면 리소스가 서버에서 다운로드 되 고 호출자에 게 표시 되며 캐시에 저장 됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[defaultHttpCachePolicy](defaulthttpcachepolicy-element-network-settings.md)|선택적 요소입니다.<br /><br /> HTTP 캐싱이 활성 상태 인지 여부를 설명 하 고 기본 캐싱 정책을 설명 합니다.|  
|[\<defaultFtpCachePolicy > 요소 (네트워크 설정)](defaultftpcachepolicy-element-network-settings.md)|선택적 요소입니다.<br /><br /> FTP 캐싱이 활성 상태 인지 여부를 설명 하 고 기본 캐싱 정책을 설명 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[system.net](system-net-element-network-settings.md)|.NET Framework의 네트워크 연결 방법을 지정하는 설정을 포함합니다.|  
  
## <a name="example"></a>예제  
 다음 예에서는 모든 캐싱을 사용 하지 않도록 설정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.net>  
    <requestCaching  
      disableAllCaching="true"  
    />  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Net.Cache?displayProperty=nameWithType>
- [네트워크 설정 스키마](index.md)
