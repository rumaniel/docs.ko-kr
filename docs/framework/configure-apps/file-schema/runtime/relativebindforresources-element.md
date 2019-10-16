---
title: <relativeBindForResources> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- RelativeBindForResources element
- <relativeBindForResources> element
ms.assetid: 846ffa47-7257-4ce3-8cac-7ff627e0e34f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b1ac2900707ddb39c62b34b0ebfbc4547cdd2653
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252356"
---
# <a name="relativebindforresources-element"></a>\<런타임은 relativebindforresources> 요소가 > 요소
위성 어셈블리에 대한 프로브를 최적화합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<relativeBindForResources>**  
  
## <a name="syntax"></a>구문  
  
```xml
<relativeBindForResources    
   enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|필수 특성입니다.<br /><br /> 공용 언어 런타임에서 위성 어셈블리에 대 한 프로브를 최적화할지 여부를 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|런타임은 위성 어셈블리에 대 한 프로브를 최적화 하지 않습니다. 기본값입니다.|  
|`true`|런타임은 위성 어셈블리에 대 한 프로브를 최적화 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|런타임 초기화 옵션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 일반적으로 [리소스 패키징 및 배포](../../../resources/packaging-and-deploying-resources-in-desktop-apps.md) 항목에 설명 된 대로 리소스에 대 한 프로브를 리소스 관리자 합니다. 즉, 지역화 된 특정 버전의 리소스를 리소스 관리자 검색할 때 전역 어셈블리 캐시에서 응용 프로그램의 코드 베이스에 있는 문화권별 폴더를 찾고 위성 어셈블리에 대 한 Windows Installer을 쿼리 한 다음이를 발생 시킬 수 있습니다. <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 이벤트. 요소 `<relativeBindForResources>` 는 위성 어셈블리를 리소스 관리자 프로브 하는 방법을 최적화 합니다. 다음 조건에서 리소스를 검색할 때 성능을 향상 시킬 수 있습니다.  
  
- 위성 어셈블리가 코드 어셈블리와 동일한 위치에 배포 되는 경우 즉, 코드 어셈블리가 전역 어셈블리 캐시에 설치 된 경우 위성 어셈블리도 여기에 설치 되어야 합니다. 코드 어셈블리가 응용 프로그램의 코드 베이스에 설치 된 경우에는 코드 베이스의 문화권별 폴더에도 위성 어셈블리를 설치 해야 합니다.  
  
- Windows Installer 사용 되지 않거나 위성 어셈블리의 요청 시 설치에 드물게 사용 됩니다.  
  
- 응용 프로그램 코드가 이벤트를 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 처리 하지 않는 경우  
  
 요소의 특성을 설정 하 여 다음과 같이 위성 어셈블리에 대 한 리소스 관리자 프로브를 최적화 합니다 `true`. `enabled` `<relativeBindForResources>`  
  
- 부모 코드 어셈블리의 위치를 사용 하 여 위성 어셈블리를 검색 합니다.  
  
- 위성 어셈블리에 대 한 Windows Installer를 쿼리하지 않습니다.  
  
- 이벤트를 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 발생 시 키 지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [리소스 패키징 및 배포](../../../resources/packaging-and-deploying-resources-in-desktop-apps.md)
- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
