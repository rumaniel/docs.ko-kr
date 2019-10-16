---
title: <publisherPolicy> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/publisherPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/publisherPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#publisherPolicy
helpviewer_keywords:
- publisherPolicy element
- container tags, <publisherPolicy> element
- <publisherPolicy> element
ms.assetid: 4613407e-d0a8-4ef2-9f81-a6acb9fdc7d4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cc206e584440778858e61fc0bab51fc8ffa2009a
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252375"
---
# <a name="publisherpolicy-element"></a>\<Y apply > 요소
런타임이 게시자 정책을 적용할지를 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<assemblyBinding >** ](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<dependentAssembly >** ](dependentassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<Y apply >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<publisherPolicy apply="yes|no"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`apply`|게시자 정책을 적용할지 여부를 지정 합니다.|  
  
## <a name="apply-attribute"></a>특성 적용  
  
|값|설명|  
|-----------|-----------------|  
|`yes`|게시자 정책을 적용 합니다. 이것이 기본 설정입니다.|  
|`no`|게시자 정책을 적용 하지 않습니다.|  
  
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
 구성 요소 공급 업체에서 새 버전의 어셈블리를 출시 하는 경우 이전 버전을 사용 하는 응용 프로그램이 이제 새 버전을 사용 하도록 공급 업체에 게시자 정책을 포함할 수 있습니다. 특정 어셈블리에 대해 게시자 정책을 적용할지 여부를 지정 하려면  **\<y apply >** 요소를  **\<dependentAssembly >** 요소에 배치 합니다.  
  
 **Apply** 특성의 기본 설정은 **예**입니다. **Apply** 특성을 **no** 로 설정 하면 어셈블리의 모든 이전 **예** 설정이 무시 됩니다.  
  
 응용 프로그램에서 응용 프로그램 구성 파일의 [ \<y apply apply = "no"/>](publisherpolicy-element.md) 요소를 사용 하 여 게시자 정책을 명시적으로 무시 하려면 응용 프로그램에 대 한 권한이 필요 합니다. 에 플래그를 <xref:System.Security.Permissions.SecurityPermissionFlag> 설정 하 여 사용 권한을 부여 합니다. <xref:System.Security.Permissions.SecurityPermission> 자세한 내용은 [어셈블리 바인딩 리디렉션 보안 권한](../../assembly-binding-redirection-security-permission.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 어셈블리 `myAssembly`에 대 한 게시자 정책을 해제 합니다.  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                                    publicKeyToken="32ab4ba45e0a69a1"  
                                    culture="neutral" />  
            <publisherPolicy apply="no"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [런타임에서 어셈블리를 찾는 방법](../../../deployment/how-the-runtime-locates-assemblies.md)
- [어셈블리 버전 리디렉션](../../redirect-assembly-versions.md)
