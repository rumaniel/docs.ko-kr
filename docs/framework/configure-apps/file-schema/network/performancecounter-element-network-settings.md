---
title: <performanceCounter> 요소(네트워크 설정)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/performanceCounters
- http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters
helpviewer_keywords:
- performanceCounter element
- <performanceCounter> element
ms.assetid: 3afa1586-e1b8-473d-8985-c3fc90cf561b
ms.openlocfilehash: 3fe6b19d0055aafad859b55960800d9786d7fa08
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697995"
---
# <a name="performancecounter-element-network-settings"></a>\<performanceCounter > 요소 (네트워크 설정)
네트워킹 성능 카운터를 사용 하거나 사용 하지 않도록 설정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4c.net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<settings >** ](settings-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 **\<performanceCounters >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<performanceCounters  
  enabled="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|네트워킹 성능 카운터의 사용 여부를 지정 합니다. 기본값은 `false`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[settings](settings-element-network-settings.md)|<xref:System.Net> 네임스페이스에 대한 기본 네트워크 옵션을 구성합니다.|  
  
## <a name="remarks"></a>설명  
 이 요소는 애플리케이션 구성 파일 또는 컴퓨터 구성 파일(Machine.config)에서 사용할 수 있습니다.  
  
 네트워킹 성능 카운터를 사용하려면 구성 파일에서 사용하도록 설정해야 합니다. 구성 파일의 단일 설정을 통해 모든 네트워킹 성능 카운터를 사용하거나 사용하지 않도록 설정합니다. 개별 네트워킹 성능 카운터를 사용하거나 사용하지 않도록 설정할 수는 없습니다. 특정 네트워킹 성능 카운터에 대 한 자세한 내용은 [네트워킹 성능 카운터](../../../debug-trace-profile/performance-counters.md#networking)를 참조 하세요.  
  
 기본값은 네트워킹 성능 카운터를 사용 하지 않도록 설정 하는 것입니다.  
  
 @No__t-0 속성은 적용 가능한 구성 파일에서 **사용 가능한** 특성의 현재 값을 가져오는 데 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 네트워킹 성능 카운터를 사용 하도록 <xref:System.Net> 및 관련 네임 스페이스를 구성 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <performanceCounters  
        enabled="true"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Net.Configuration.PerformanceCountersElement?displayProperty=nameWithType>
- <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType>
- [네트워크 설정 스키마](index.md)
- [네트워킹 성능 카운터](../../../debug-trace-profile/performance-counters.md#networking)
