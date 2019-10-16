---
title: <namedCaches> 요소(캐시 설정)
ms.date: 03/30/2017
helpviewer_keywords:
- namedCaches element
- caching [.NET Framework], configuration
- <namedCaches> element
ms.assetid: 6bd4fbc5-55a6-4dc4-998b-cdcc7e023330
ms.openlocfilehash: 4587234ad91fa3b1abbb376bd7ae517d5abea6c3
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252456"
---
# <a name="namedcaches-element-cache-settings"></a>\<namedCaches > 요소 (캐시 설정)
명명 <xref:System.Runtime.Caching.MemoryCache> 된 인스턴스에 대 한 구성 설정의 컬렉션을 지정 합니다. 합니다 <xref:System.Runtime.Caching.Configuration.MemoryCacheSection.NamedCaches%2A> 하나 이상의 구성 설정의 컬렉션을 참조 하는 속성 `namedCaches` 구성 파일의 요소입니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<>의 런타임 캐싱**](system-runtime-caching-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<memoryCache >** ](memorycache-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<namedCaches >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<namedCaches>  
  <add name="default"/>   
</namedCaches>  
```  
  
## <a name="type"></a>형식  
 `None`  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|`cacheMemoryLimitMegabytes`|인스턴스를 확장할 <xref:System.Runtime.Caching.MemoryCache> 수 있는 최대 허용 크기 (mb)를 지정 하는 정수 값입니다. 기본값은 0입니다. 즉, <xref:System.Runtime.Caching.MemoryCache> 클래스의 자동 크기 조정 추론은 기본적으로 사용 됩니다.|  
|`name`|캐시의 이름입니다.|  
|`physicalMemoryLimitPercentage`|캐시에서 사용할 수 있는 물리적으로 설치 된 컴퓨터 메모리의 최대 백분율을 지정 하는 0에서 100 사이의 정수 값입니다. 기본값은 0입니다. 즉, <xref:System.Runtime.Caching.MemoryCache> 클래스의 자동 크기 조정 추론은 기본적으로 사용 됩니다.|  
|`pollingInterval`|캐시 구현이 현재 메모리 로드를 캐시 인스턴스에 대해 설정된 절대 및 백분율 기반 메모리 제한과 비교하기까지의 시간 간격을 나타내는 값입니다. 이 값은 "HH: MM: SS" 형식으로 입력 됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<add>](add-element-for-namedcaches.md)|메모리 캐시용으로 명명된 캐시를 `namedCaches` 컬렉션에 추가합니다.|  
|[\<clear>](clear-element-for-namedcaches.md)|메모리 캐시에 대해 `namedCaches` 컬렉션을 지웁니다.|  
|[\<remove>](remove-element-for-namedcaches.md)|메모리 캐시용으로 명명된 캐시 항목을 `namedCaches` 컬렉션에서 제거합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<구성>](../configuration-element.md)|공용 언어 런타임 및 .NET Framework 응용 프로그램에서 사용 하는 모든 구성 파일의 루트 요소를 지정 합니다.|  
|[\<memoryCache>](memorycache-element-cache-settings.md)|<xref:System.Runtime.Caching.MemoryCache> 클래스를 기반으로 하는 캐시 구성에 사용되는 요소를 정의합니다.|  
|[\<system.runtime.caching>](system-runtime-caching-element-cache-settings.md)|.NET Framework에 기본 제공 되는 응용 프로그램에서 출력 캐싱을 구현할 수 있는 형식을 포함 합니다.|  
  
## <a name="remarks"></a>설명  
 Web.config 파일의 메모리 캐시 구성 섹션 `add`에는 `namedCaches` 컬렉션에 대 한, `remove`및 `clear` 특성을 포함할 수 있습니다. 각 `namedCaches` 항목은 특성에 `name` 의해 고유 하 게 식별 됩니다.  
  
 응용 프로그램 구성 파일의 정보를 참조 하 여 메모리 캐시 항목의 인스턴스를 검색할 수 있습니다. 기본적으로 기본 캐시 인스턴스만 구성 파일에 항목을 포함 합니다. 기본 캐시 인스턴스는 <xref:System.Runtime.Caching.MemoryCache.Default%2A> 속성에서 반환 되는 인스턴스입니다.  
  
 Name 특성을 "default"로 설정 하는 경우 요소는 기본 메모리 캐시 인스턴스를 사용 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `name` 특성을 "기본값"으로 설정 하 여 캐시 이름을 기본 캐시 항목 이름으로 설정 하는 방법을 보여 줍니다.  
  
 `cacheMemoryLimitMegabytes` 특성 및 `physicalMemoryPercentage` 특성은 0으로 설정됩니다. 이러한 특성을 0으로 설정 하면 <xref:System.Runtime.Caching.MemoryCache> 클래스의 자동 크기 조정 추론을 사용 하는 것입니다. 캐시 구현에서는 현재 메모리 부하가 절대 및 백분율 기반 메모리 제한과 2 분 마다 비교 됩니다.  
  
```xml  
<configuration>  
  
  <system.runtime.caching>  
    <memoryCache>  
      <namedCaches>  
          <add name="default"   
               cacheMemoryLimitMegabytes="0"   
               physicalMemoryLimitPercentage="0"  
               pollingInterval="00:02:00" />  
      </namedCaches>  
    </memoryCache>  
  </system.runtime.caching>  
  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [\<memoryCache > 요소 (캐시 설정)](memorycache-element-cache-settings.md)
