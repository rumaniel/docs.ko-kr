---
title: <namedCaches>에 대한 <clear> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- <clear> element for <namedCaches>
- clear element for <namedCaches>
ms.assetid: ea01a858-65da-4348-800f-5e3df59d4d79
ms.openlocfilehash: bcc0e23f0c47ad3a98430e36da31d39612caa3c9
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252755"
---
# <a name="clear-element-for-namedcaches"></a>\<namedcaches의 > \<요소를 지웁니다 >
메모리 캐시 `namedCache` 의 `namedCaches` 컬렉션에서 모든 항목을 지웁니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<>의 런타임 캐싱**](system-runtime-caching-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<memoryCache >** ](memorycache-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<namedCaches >** ](namedcaches-element-cache-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> 지우기**  
  
## <a name="syntax"></a>구문  
  
```xml  
<namedCaches>  
    <clear name="Default" />  
    <!-- child elements -->  
 </namedCaches>  
```  
  
## <a name="type"></a>형식  
 `Type`  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 `None`  
  
### <a name="child-elements"></a>자식 요소  
 `None`  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<namedCaches>](namedcaches-element-cache-settings.md)|명명 <xref:System.Runtime.Caching.MemoryCache> 된 인스턴스에 대 한 구성 설정의 컬렉션을 포함 합니다.|  
  
## <a name="remarks"></a>설명  
 요소 `clear` 는 메모리 캐시 `namedCache` 에 대해 명명 된 캐시 컬렉션에서 모든 항목을 지웁니다. 요소를 사용 하 `clear` 여 새 명명 된 캐시 `add` 엔트리를 추가 하기 전에 요소를 사용 하 여 컬렉션에 명명 된 다른 캐시가 없는지 확인할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [\<namedCaches > 요소 (캐시 설정)](namedcaches-element-cache-settings.md)
