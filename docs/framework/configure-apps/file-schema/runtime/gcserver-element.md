---
title: <gcServer> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/gcServer
- http://schemas.microsoft.com/.NetConfiguration/v2.0#gcServer
helpviewer_keywords:
- gcServer element
- <gcServer> element
ms.assetid: 8d25b80e-2581-4803-bd87-a59528e3cb03
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: aa03179df1cd2595b4be428106dd3ec10b309317
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252546"
---
# <a name="gcserver-element"></a>\<gcServer > 요소
공용 언어 런타임이 서버 가비지 컬렉션을 실행하는지 여부를 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<gcServer>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<gcServer    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|필수 특성입니다.<br /><br /> 런타임이 서버 가비지 수집을 실행하는지 여부를 지정합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|서버 가비지 컬렉션을 실행하지 않습니다. 이 값이 기본값입니다.|  
|`true`|서버 가비지 컬렉션을 실행합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 CLR(공용 언어 런타임)에서는 두 가지 유형의 가비지 컬렉션을 지원합니다. 워크스테이션 가비지 컬렉션은 모든 시스템에서 사용할 수 있고, 서버 가비지 컬렉션은 다중 프로세서 시스템에서 사용할 수 있습니다. `<gcServer>` 요소를 사용하여 CLR에서 수행하는 가비지 수집 유형을 제어합니다. <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=nameWithType> 속성을 사용하여 서버 가비지 수집이 사용하도록 설정되었는지 확인합니다.  
  
 단일 프로세서 컴퓨터의 경우 기본 워크스테이션 가비지 수집이 가장 빠른 옵션입니다. 두 개의 프로세서가 있는 컴퓨터에는 워크스테이션 또는 서버를 사용할 수 있습니다. 세 개 이상 프로세서의 경우 서버 가비지 수집이 가장 빠른 옵션입니다.  
  
 이 요소는 응용 프로그램 구성 파일에만 사용할 수 있습니다. 컴퓨터 구성 파일에 있는 경우 무시됩니다.  
  
> [!NOTE]
> .NET Framework 4 및 이전 버전에서, 서버 가비지 수집이 사용되는 경우에는 동시 가비지 수집을 사용할 수 없습니다. .NET Framework 4.5부터 서버 가비지 수집이 동시에 이루어 집니다. 비 동시 서버 가비지 `<gcServer>` 수집을 사용 하려면 요소를로 `true` 설정 하 고 [ \<gcConcurrent > 요소](gcconcurrent-element.md) 를로 `false`설정 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 서버 가비지 컬렉션을 사용하도록 설정합니다.  
  
```xml  
<configuration>  
   <runtime>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=nameWithType>
- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [동시 가비지 수집을 사용 하지 않도록 설정 하려면](gcconcurrent-element.md#to-disable-background-garbage-collection)
