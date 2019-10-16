---
title: <runtime>에 대한 <assemblyBinding> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding
helpviewer_keywords:
- <assemblyBinding> element
- assemblyBinding element
- container tags, <assemblyBinding> element
ms.assetid: 964cbb35-ab49-4498-8471-209689e5dada
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 515261fe39676292ce50858f71b7da92287945d1
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252809"
---
# <a name="assemblybinding-element-for-runtime"></a>\<런타임 >에 대 한 \<assemblybinding > 요소
어셈블리 버전 리디렉션 및 어셈블리 위치에 대한 정보를 포함합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<assemblyBinding>**  
  
## <a name="syntax"></a>구문  
  
```xml  
      <assemblyBinding    
   xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
</assemblyBinding>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|**xmlns**|필수 특성입니다.<br /><br /> 어셈블리 바인딩에 필요한 XML 네임스페이스를 지정합니다. 문자열 string "urn:schemas-microsoft-com:asm.v1"을 값으로 사용합니다.|  
|**appliesTo**|.NET Framework 어셈블리 리디렉션이 적용되는 런타임 버전을 지정합니다. 이 선택적 특성은 .NET Framework 버전 번호를 사용하여 특성이 적용되는 버전을 지정합니다. **appliesTo** 특성이 지정되지 않으면 **\<assemblyBinding>** 요소는 .NET Framework의 모든 버전에 적용됩니다. **AppliesTo** 특성은 .NET Framework 버전 1.1에서 도입 되었습니다. .NET Framework 버전 1.0에서 무시 됩니다. 즉, .NET Framework 버전 1.0을 사용할 때는 **appliesTo** 특성을 지정해도 모든 **\<assemblyBinding>** 요소가 적용됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<dependentAssembly>](dependentassembly-element.md)|어셈블리에 대한 바인딩 정책 및 어셈블리 위치를 캡슐화합니다. 각 어셈블리에 대해 하나의  **\<dependentAssembly >** 태그를 사용 합니다.|  
|[\<probing>](probing-element.md)|어셈블리를 로드할 때 공용 언어 런타임이 검색하는 하위 디렉터리를 지정합니다.|  
|[\<publisherPolicy>](publisherpolicy-element.md)|런타임이 게시자 정책을 적용할지를 지정합니다.|  
|[\<qualifyAssembly>](qualifyassembly-element.md)|부분 이름이 사용될 때 동적으로 로드되어야 하는 어셈블리의 전체 이름을 지정합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="example"></a>예제  
 다음 예제에서는 어셈블리 버전을 다른 버전으로 리디렉션하는 방법을 보여 주고 Codebase를 제공합니다.  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
            <codeBase version="2.0.0.0"  
                      href="http://www.litwareinc.com/myAssembly.dll"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 다음 예제에서는 **appliesTo** 특성을 사용 하 여 .NET Framework 어셈블리의 바인딩을 리디렉션하는 방법을 보여 줍니다.  
  
```xml  
<runtime>  
   <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
      <dependentAssembly>   
         <assemblyIdentity name="mscorcfg" publicKeyToken="b03f5f7f11d50a3a" culture=""/>  
         <bindingRedirect oldVersion="0.0.0.0-65535.65535.65535.65535" newVersion="1.0.3300.0"/>  
      </dependentAssembly>  
   </assemblyBinding>  
</runtime>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [어셈블리 버전 리디렉션](../../redirect-assembly-versions.md)
