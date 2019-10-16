---
title: <runtime>에 대한 <assemblyIdentity> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/assemblyIdentity
- http://schemas.microsoft.com/.NetConfiguration/v2.0#assemblyIdentity
helpviewer_keywords:
- <assemblyIdentity> element
- container tags, <assemblyIdentity> element
- assemblyIdentity element
ms.assetid: cea4d187-6398-4da4-af09-c1abc6a349c1
ms.openlocfilehash: 7cce12f6fb4b957d740cd590bd84851fa16a117d
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252793"
---
# <a name="assemblyidentity-element-for-runtime"></a>\<런타임 >에 대 \<한 assemblyIdentity > 요소
어셈블리에 대 한 식별 정보를 포함 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<assemblyBinding >** ](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<dependentAssembly >** ](dependentassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<assemblyIdentity>**  
  
## <a name="syntax"></a>구문  
  
```xml  
   <assemblyIdentity    
name="assembly name"  
publicKeyToken="public key token"  
culture="assembly culture"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`name`|필수 특성입니다.<br /><br /> 어셈블리의 이름입니다.|  
|`culture`|선택적 특성입니다.<br /><br /> 어셈블리의 언어 및 국가/지역을 지정 하는 문자열입니다.|  
|`publicKeyToken`|선택적 특성입니다.<br /><br /> 어셈블리의 강력한 이름을 지정 하는 16 진수 값입니다.|  
|`processorArchitecture`|선택적 특성입니다.<br /><br /> 프로세서 특정 코드를 포함 하는 어셈블리의 프로세서 아키텍처를 지정 하는 "x86", "amd64", "msil" 또는 "ia64" 값 중 하나입니다. 값은 대/소문자를 구분 하지 않습니다. 특성에 다른 값이 할당 된 경우에는 전체 `<assemblyIdentity>` 요소가 무시 됩니다. <xref:System.Reflection.ProcessorArchitecture>을 참조하세요.|  
  
## <a name="processorarchitecture-attribute"></a>processorArchitecture 특성  
  
|값|설명|  
|-----------|-----------------|  
|`amd64`|AMD x86-64 아키텍처 전용.|  
|`ia64`|Intel Itanium 아키텍처에만 해당 합니다.|  
|`msil`|프로세서 및 워드 당 비트에 대해 중립적입니다.|  
|`x86`|64 비트 플랫폼의 기본 또는 WOW (Windows on Windows) 환경에 있는 32 비트 x86 프로세서|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`assemblyBinding`|어셈블리 버전 리디렉션 및 어셈블리 위치에 대한 정보를 포함합니다.|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`dependentAssembly`|각 어셈블리에 대한 바인딩 정책 및 어셈블리 위치를 캡슐화합니다. 각 어셈블리 `<dependentAssembly>` 에 대해 하나의 요소를 사용 합니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 **모든\<dependentAssembly >** 요소에는 하나의  **\<assemblyIdentity >** 자식 요소가 있어야 합니다.  
  
 특성이 있는 경우 요소는 `<assemblyIdentity>` 해당 프로세서 아키텍처를 사용 하는 어셈블리에만 적용 됩니다. `processorArchitecture` 특성이 없는 경우 요소는 `<assemblyIdentity>` 모든 프로세서 아키텍처를 사용 하 여 어셈블리에 적용할 수 있습니다. `processorArchitecture`  
  
 다음 예제에서는 두 개의 서로 다른 프로세서 아키텍처를 대상으로 하는 동일한 이름의 두 어셈블리에 대 한 구성 파일 및 해당 버전이 동기화에서 유지 관리 되지 않는 경우를 보여 줍니다. 응용 프로그램이 x86 플랫폼에서 실행 되는 경우 첫 `<assemblyIdentity>` 번째 요소가 적용 되 고 나머지 요소는 무시 됩니다. 응용 프로그램이 x86 또는 ia64 이외의 플랫폼에서 실행 되는 경우 둘 다 무시 됩니다.  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"  
                  processorArchitecture="x86" />  
            <bindingRedirect oldVersion= "1.0.0.0"   
                  newVersion="1.1.0.0" />  
         </dependentAssembly>  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"   
                  processorArchitecture="ia64" />  
            <bindingRedirect oldVersion="1.0.0.0"   
                  newVersion="2.0.0.0" />  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 구성 파일에 특성이 없고 `<assemblyIdentity>` `processorArchitecture` 플랫폼과 일치 하는 요소가 포함 되지 않은 요소가 포함 된 경우 `processorArchitecture` 특성이 없는 요소가 사용 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 어셈블리에 대 한 정보를 제공 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <!--Redirection and codeBase policy for myAssembly.-->  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [어셈블리 버전 리디렉션](../../redirect-assembly-versions.md)
