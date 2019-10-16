---
title: <disableCachingBindingFailures> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCachingBindingFailures
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCachingBindingFailures
helpviewer_keywords:
- assemblies [.NET Framework],caching binding failures
- caching assembly binding failures
- <disableCachingBindingFailures> element
- disableCachingBindingFailures element
ms.assetid: bf598873-83b7-48de-8955-00b0504fbad0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d5b45ea4b30677d17e72685b16c19f9192c8c144
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252675"
---
# <a name="disablecachingbindingfailures-element"></a>\<disableCachingBindingFailures > 요소
검색을 통해 어셈블리를 찾을 수 없기 때문에 발생 하는 바인딩 실패의 캐싱을 사용 하지 않도록 설정할지 여부를 지정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<disableCachingBindingFailures>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<disableCachingBindingFailures enabled="0|1"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|사용|필수 특성입니다.<br /><br /> 검색을 통해 어셈블리를 찾을 수 없기 때문에 발생 하는 바인딩 실패의 캐싱을 사용 하지 않도록 설정할지 여부를 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|0|검색을 통해 어셈블리를 찾을 수 없기 때문에 발생 하는 바인딩 실패의 캐싱을 사용 하지 않도록 설정 하지 마십시오. 이는 .NET Framework 버전 2.0부터 시작 하는 기본 바인딩 동작입니다.|  
|1|검색을 통해 어셈블리를 찾을 수 없기 때문에 발생 하는 바인딩 실패의 캐싱을 사용 하지 않도록 설정 합니다. 이 설정은 .NET Framework 버전 1.1의 바인딩 동작으로 되돌립니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework 버전 2.0부터 어셈블리를 로드 하는 기본 동작은 모든 바인딩과 로드 오류를 캐시 하는 것입니다. 즉, 어셈블리를 로드 하지 못한 경우 어셈블리를 찾지 않고도 동일한 어셈블리를 로드 하는 후속 요청이 즉시 실패 합니다. 이 요소는 어셈블리를 검색 경로에서 찾을 수 없기 때문에 발생 하는 바인딩 실패에 대 한 기본 동작을 사용 하지 않도록 설정 합니다. 이러한 오류는 <xref:System.IO.FileNotFoundException>throw 됩니다.  
  
 일부 바인딩 및 로드 오류는이 요소의 영향을 받지 않으며 항상 캐시 됩니다. 이러한 오류는 어셈블리를 찾았지만 로드할 수 없기 때문에 발생 합니다. <xref:System.BadImageFormatException> 또는<xref:System.IO.FileLoadException>를 throw 합니다. 다음 목록에 이러한 오류의 몇 가지 예가 포함 되어 있습니다.  
  
- 올바른 어셈블리가 아닌 파일을 로드 하려고 시도 하는 경우 잘못 된 파일이 올바른 어셈블리로 바뀐 경우에도 이후에 어셈블리를 로드 하려는 시도가 실패 합니다.  
  
- 파일 시스템에 의해 잠긴 어셈블리를 로드 하려고 하면 파일 시스템에서 어셈블리를 해제 한 후에도 이후에 어셈블리를 로드 하려는 시도가 실패 합니다.  
  
- 로드 하려는 하나 이상의 어셈블리 버전이 검색 경로에 있지만 요청 하는 특정 버전이 검색 경로에 없는 경우 올바른 버전이 검색 경로로 이동 되더라도 이후 버전의 로드 시도는 실패 하 게 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 어셈블리를 검색 하 여 찾을 수 없기 때문에 발생 하는 어셈블리 바인딩 실패의 캐싱을 사용 하지 않도록 설정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <runtime>  
      <disableCachingBindingFailures enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [런타임에서 어셈블리를 찾는 방법](../../../deployment/how-the-runtime-locates-assemblies.md)
