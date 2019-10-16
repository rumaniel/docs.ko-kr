---
title: <claimsAuthorizationManager>
ms.date: 03/30/2017
ms.assetid: 9354eee3-f692-4ad6-8427-3169686b8bcc
author: BrucePerlerMS
ms.openlocfilehash: ddbe8a862940272e4192a3f4c0abdc1f9e8b5d48
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252081"
---
# <a name="claimsauthorizationmanager"></a>\<claimsAuthorizationManager>
들어오는 클레임에 대 한 클레임 권한 부여 관리자를 등록 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<claimsAuthorizationManager >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthorizationManager type = xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthorizationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|type|<xref:System.Security.Claims.ClaimsAuthorizationManager> 클래스에서 파생 되는 사용자 지정 형식입니다. `type` 특성을 지정 하는 방법에 대 한 자세한 내용은 [사용자 지정 형식 참조](../windows-workflow-foundation/index.md)를 참조 하세요.|  
  
### <a name="child-elements"></a>자식 요소  
 <xref:System.Security.Claims.ClaimsAuthenticationManager> `<claimsAuthorizationManager>` 특성이 없거나 특성이 클래스를 참조 하는 경우 요소는 자식 요소를 사용 하지 않습니다. 그러나에서 <xref:System.Security.Claims.ClaimsAuthorizationManager> 파생 된 클래스는 자식 구성 요소를 정의할 수 있습니다. `type` `type`  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<identityConfiguration>](identityconfiguration.md)|서비스 수준 id 설정을 지정 합니다.|  
  
## <a name="remarks"></a>설명  
 클래스를 <xref:System.Security.Claims.ClaimsAuthorizationManager> 통해 제공 되는 기본 동작은 항상 들어오는 클레임을 승인 합니다. 특성을 `type` 지정 하지 않거나 특성에서 `type` <xref:System.Security.Claims.ClaimsAuthorizationManager> 클래스를 지정 하는 경우 요소 `<claimsAuthorizationManager>` 는 자식 요소를 사용 하지 않습니다. 특성을 지정 하 `type` 여 <xref:System.Security.Claims.ClaimsAuthorizationManager> 클래스에서 파생 된 형식을 등록 하 고 사용자 지정 동작을 구현할 수 있습니다. 파생 클래스는 이러한 요소를 처리 하도록 메서드를 `<claimsAuthorizationManager>` <xref:System.Security.Claims.ClaimsAuthorizationManager.LoadCustomConfiguration%2A> 재정의 하 여 요소의 자식 요소를 통해 구성을 지원할 수 있습니다. 자식 요소에 대해 정의 된 스키마는 클래스의 디자이너입니다.  
  
> [!IMPORTANT]
> 또는 클래스를 사용 하 여 `<federationConfiguration>` 코드에서 클레임 기반 액세스 제어를 제공 하는 경우 요소에서 참조 하는 id 구성은 클레임 권한 부여 관리자 및 다음을 수행 하는 데 사용 되는 정책을 구성 합니다. <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> 권한 부여 결정. 이는 Windows Communication Foundation (WCF) 응용 프로그램 또는 웹 기반이 아닌 응용 프로그램 등 수동 웹 시나리오가 아닌 시나리오 에서도 마찬가지입니다. 응용 프로그램이 수동 웹 응용 프로그램이 `<claimsAuthorizationManager>` 아닌 경우 참조 되는 id 구성의 요소 및 자식 정책 요소 (있는 경우)만 적용 됩니다. 다른 모든 설정은 무시 됩니다. 자세한 내용은 [ \<federationConfiguration >](federationconfiguration.md) 요소를 참조 하세요.  
  
 이 요소는 속성 <xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthorizationManager%2A?displayProperty=nameWithType> 을 설정 합니다.  
  
## <a name="example"></a>예제  
 다음 XML은 리소스 작업 쌍으로 구성 된 정책을 구현 하는 클레임 권한 부여 관리자에 대 한 구성을 보여 줍니다. 각각은 요청자에 게 리소스에 대 한 작업을 수행 하기 위해 소유 해야 하는 클레임의 부울 조합을 지정 합니다. 이 정책을 사용할 수 있는 클레임 권한 부여 관리자를 구현 하는 코드는 `ClaimsBasedAuthorization` 샘플에서 찾을 수 있습니다.  
  
```xml  
<system.identityModel>  
    <identityConfiguration>  
      <claimsAuthorizationManager type="ClaimsAuthorizationLibrary.MyClaimsAuthorizationManager, ClaimsAuthorizationLibrary">  
        <policy resource="http://localhost:28491/Developers.aspx" action="GET">  
          <or>  
            <claim claimType="http://schemas.microsoft.com/ws/2008/06/identity/claims/role" claimValue="developer" />  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
          </or>  
        </policy>  
        <policy resource="http://localhost:28491/Administrators.aspx" action="GET">  
          <and>  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
            <claim claimType="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country" claimValue="USA" />  
          </and>  
        </policy>  
        <policy resource="http://localhost:28491/Default.aspx" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/Claims.aspx" action="GET">  
        </policy>  
      </claimsAuthorizationManager>  
    <identityConfiguration>  
<system.identityModel>  
```
