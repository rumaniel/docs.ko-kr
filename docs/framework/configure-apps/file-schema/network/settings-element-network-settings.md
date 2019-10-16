---
title: <settings> 요소(네트워크 설정)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#settings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings
helpviewer_keywords:
- settings element
- <settings> element
ms.assetid: 189ce989-c39b-427d-b004-6b82a668b931
ms.openlocfilehash: ba08f630dc602c950da309bf29482d85b41af7ef
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697688"
---
# <a name="settings-element-network-settings"></a>\<settings > 요소 (네트워크 설정)
<xref:System.Net?displayProperty=nameWithType> 네임스페이스에 대한 기본 네트워크 옵션을 구성합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4c.net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t **\<settings >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<settings>  
  <httpListener>...</httpListener>  
  <httpWebRequest>...</httpWebRequest>  
  <ipv6>...</ipv6>  
  <performanceCounters>...</performanceCounters>  
  <servicePointManager>...</servicePointManager>  
  <socket>...</socket>  
  <webProxyScript>...</webProxyScript>  
</settings>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[httpListener](httplistener-element-network-settings.md)|@No__t-0 클래스에서 사용 하는 매개 변수를 사용자 지정 합니다.|  
|[httpWebRequest](httpwebrequest-element-network-settings.md)|웹 요청 매개 변수를 사용자 지정 합니다.|  
|[ipv6](ipv6-element-network-settings.md)|IPv6 (인터넷 프로토콜 버전 6) 지원을 사용 하도록 설정 합니다.|  
|[\<performanceCounter > 요소 (네트워크 설정)](performancecounter-element-network-settings.md)|네트워크 성능 카운터를 사용 하도록 설정 합니다.|  
|[servicePointManager](servicepointmanager-element-network-settings.md)|네트워크 리소스에 대 한 연결을 구성 합니다.|  
|[socket](socket-element-network-settings.md)|소켓 작업에서 완료 포트를 사용 하는지 여부를 지정 합니다.|  
|[\<webProxyScript > 요소 (네트워크 설정)](webproxyscript-element-network-settings.md)|웹 프록시를 검색 하는 데 사용 되는 스크립트의 특징을 구성 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[system.net](system-net-element-network-settings.md)|.NET Framework의 네트워크 연결 방법을 지정하는 설정을 포함합니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="configuration-files"></a>구성 파일  
 이 요소는 애플리케이션 구성 파일 또는 컴퓨터 구성 파일(Machine.config)에서 사용할 수 있습니다.  
  
## <a name="see-also"></a>참조

- <xref:System.Net?displayProperty=nameWithType>
- [네트워크 설정 스키마](index.md)
