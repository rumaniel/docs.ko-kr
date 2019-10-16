---
title: <alwaysFlowImpersonationPolicy> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/alwaysFlowImpersonationPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#alwaysFlowImpersonationPolicy
helpviewer_keywords:
- alwaysFlowImpersonationPolicy element
- <alwaysFlowImpersonationPolicy> element
ms.assetid: ee622801-9e46-470b-85ab-88c4b1dd2ee1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 164492eb1abc7329481f158963118b47d2c4aebc
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252858"
---
# <a name="alwaysflowimpersonationpolicy-element"></a>\<alwaysFlowImpersonationPolicy > 요소
가장을 수행하는 방법과 관계없이 Windows ID가 항상 비동기 지점 간을 흐르도록 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<alwaysFlowImpersonationPolicy>** \  
  
## <a name="syntax"></a>구문  
  
```xml  
<alwaysFlowImpersonationPolicy    
  enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|필수 특성입니다.<br /><br /> Windows id가 비동기 요소를 통과 하는지 여부를 나타냅니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|와 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A>같은 관리 되는 메서드를 통해 가장을 수행 하지 않는 한, Windows id는 비동기 요소를 통해 전달 되지 않습니다. 이 값이 기본값입니다.|  
|`true`|Windows id는 가장이 수행 된 방법에 관계 없이 항상 비동기 요소를 통해 흐릅니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework 버전 1.0 및 1.1에서는 Windows id가 비동기 시점 간에 이동 하지 않습니다. .NET Framework 버전 2.0 <xref:System.Threading.ExecutionContext> 에는 현재 실행 중인 스레드에 대 한 정보를 포함 하는 개체가 있으며,이 개체는 응용 프로그램 도메인 내의 비동기 요소를 통해 흐릅니다. 는 <xref:System.Security.Principal.WindowsIdentity> 비동기 요소를 통해 전달 되는 정보의 일부로도 전달 됩니다 .이 경우에는 및와 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A> 같은 관리 되는 메서드를 사용 하 여, 네이티브 메서드에 대 한 플랫폼 호출과 같은 다른 방법을 사용 하지 않는 것이 좋습니다. 이 요소는 가장이 달성 된 방법에 관계 없이 Windows id가 비동기 시점 간에 이동 하도록 지정 하는 데 사용 됩니다.  
  
 다른 두 가지 방법으로이 기본 동작을 변경할 수 있습니다.  
  
1. 스레드 단위로 관리 코드에서  
  
     <xref:System.Threading.ExecutionContext> <xref:System.Security.SecurityContext> , 또는<xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=nameWithType>메서드 를 사용 하 여 및 설정을 수정 하 여 스레드 단위로 흐름을 억제할 수 있습니다. <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=nameWithType> <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=nameWithType>  
  
2. 관리 되지 않는 호스팅 인터페이스를 호출 하 여 CLR (공용 언어 런타임)을 로드 합니다.  
  
     단순한 관리 되는 실행 파일 대신 관리 되지 않는 호스팅 인터페이스를 사용 하 여 CLR을 로드 하는 경우 [CorBindToRuntimeEx 함수](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md) 함수 호출에서 특수 플래그를 지정할 수 있습니다. 전체 프로세스에 대 한 호환성 모드를 사용 하도록 설정 하려면 `flags` [CorBindToRuntimeEx 함수](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md) 에 대 한 `STARTUP_ALWAYSFLOW_IMPERSONATION`매개 변수를로 설정 합니다.  
  
## <a name="configuration-file"></a>구성 파일  
 .NET Framework 응용 프로그램에서이 요소는 응용 프로그램 구성 파일에만 사용할 수 있습니다.  
  
 ASP.NET 응용 프로그램의 경우 \<Windows 폴더 > \Microsoft.NET\Framework\vx.x.xxxx 디렉터리에 있는 aspnet .config 파일에서 가장 흐름을 구성할 수 있습니다.  
  
 ASP.NET는 기본적으로 다음 구성 설정을 사용 하 여 aspnet 파일에서 가장 흐름을 사용 하지 않도록 설정 합니다.  
  
```xml
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
      <alwaysFlowImpersonationPolicy enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
 ASP.NET에서 대신 가장의 흐름을 허용 하려면 다음 구성 설정을 명시적으로 사용 해야 합니다.  
  
```xml  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="false"/>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 관리 되는 메서드가 아닌를 통해 가장을 사용 하는 경우에도 Windows id가 비동기 시점에서 흐르도록 지정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <runtime>  
    <alwaysFlowImpersonationPolicy enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [\<legacyImpersonationPolicy > 요소](legacyimpersonationpolicy-element.md)
