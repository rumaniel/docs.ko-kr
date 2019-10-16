---
title: <claimsAuthenticationManager>
ms.date: 03/30/2017
ms.assetid: 6d30a450-6d13-4671-81a8-77e0204500c5
author: BrucePerlerMS
ms.openlocfilehash: c901daf4d442a206345301795c7a4bdc076329cd
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252099"
---
# <a name="claimsauthenticationmanager"></a>\<claimsAuthenticationManager>
들어오는 클레임에 대 한 클레임 인증 관리자를 등록 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<claimsAuthenticationManager >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthenticationManager type=xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthenticationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|type|<xref:System.Security.Claims.ClaimsAuthenticationManager> 클래스에서 파생 되는 사용자 지정 형식을 지정 합니다. `type` 특성을 지정 하는 방법에 대 한 자세한 내용은 [사용자 지정 형식 참조]를 참조 하세요.|  
  
### <a name="child-elements"></a>자식 요소  
 <xref:System.Security.Claims.ClaimsAuthenticationManager> `<claimsAuthenticationManager>` 특성이 없거나 특성이 클래스를 참조 하는 경우 요소는 자식 요소를 사용 하지 않습니다. 그러나에서 <xref:System.Security.Claims.ClaimsAuthenticationManager> 파생 된 클래스는 자식 구성 요소를 정의할 수 있습니다. `type` `type`  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<identityConfiguration>](identityconfiguration.md)|서비스 수준 id 설정을 지정 합니다.|  
  
## <a name="remarks"></a>설명  
 클래스를 <xref:System.Security.Claims.ClaimsAuthenticationManager> 통해 제공 되는 기본 동작은 들어오는 클레임을 에코 합니다. 특성을 `type` 지정 하지 않거나 특성에서 `type` <xref:System.Security.Claims.ClaimsAuthenticationManager> 클래스를 지정 하는 경우 요소 `<claimsAuthenticationManager>` 는 자식 요소를 사용 하지 않습니다. 특성을 지정 하 `type` 여 <xref:System.Security.Claims.ClaimsAuthenticationManager> 클래스에서 파생 된 형식을 등록 하 고 사용자 지정 동작을 구현할 수 있습니다. 파생 클래스는 이러한 요소를 처리 하도록 메서드를 `<claimsAuthenticationManager>` <xref:System.Security.Claims.ClaimsAuthenticationManager.LoadCustomConfiguration%2A> 재정의 하 여 요소의 자식 요소를 통해 구성을 지원할 수 있습니다. 자식 요소에 대해 정의 된 스키마는 클래스의 디자이너입니다.  
  
 요소 `<claimsAuthenticationManager>` 는 속성을 <xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthenticationManager%2A?displayProperty=nameWithType> 설정 합니다.  
  
## <a name="example"></a>예제  
  
```xml  
<system.identityModel>  
    <identityConfiguration name="MyIdentity">  
      <claimsAuthenticationManager type="MyNamespace.CustomClaimsAuthenticationManager, MyAssembly"/>          
    </identityConfiguration>  
</system.identityModel>  
```
