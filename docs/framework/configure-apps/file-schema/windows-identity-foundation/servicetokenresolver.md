---
title: <serviceTokenResolver>
ms.date: 03/30/2017
ms.assetid: 6e9001e1-e064-4f47-84b2-46225c177746
author: BrucePerlerMS
ms.openlocfilehash: 30a53c11b551623311f7ca3f957143fc702568a1
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251845"
---
# <a name="servicetokenresolver"></a>\<serviceTokenResolver>
토큰 처리기 컬렉션의 처리기에서 사용 하는 서비스 토큰 확인자를 등록 합니다. 서비스 토큰 확인자는 들어오는 토큰과 메시지의 암호화 토큰을 확인 하는 데 사용 됩니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlers >** ](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlerConfiguration >** ](securitytokenhandlerconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<serviceTokenResolver >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <serviceTokenResolver type=xs:string>  
        </serviceTokenResolver>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|type|서비스 토큰 확인자 유형을 지정 합니다. 형식 또는 <xref:System.IdentityModel.Selectors.SecurityTokenResolver> 클래스에서 파생 되는 형식입니다. <xref:System.IdentityModel.Selectors.SecurityTokenResolver> `type` 특성을 지정 하는 방법에 대 한 자세한 내용은 [사용자 지정 형식 참조]를 참조 하세요. 필수 요소.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|보안 토큰 처리기의 컬렉션에 대 한 구성을 제공 합니다.|  
  
## <a name="remarks"></a>설명  
 서비스 토큰 확인자를 사용 하 여 들어오는 토큰과 메시지의 암호화 토큰을 확인할 수 있습니다. 들어오는 토큰의 암호를 해독 하는 데 사용 되는 키를 검색 하는 데 사용 됩니다. 특성을 `type` 지정 해야 합니다. 지정 된 형식은 <xref:System.IdentityModel.Selectors.SecurityTokenResolver> 이거나 <xref:System.IdentityModel.Selectors.SecurityTokenResolver> 클래스에서 파생 되는 사용자 지정 형식일 수 있습니다.  
  
 일부 토큰 처리기를 사용 하면 구성에서 서비스 토큰 확인자 설정을 지정할 수 있습니다. 개별 토큰 처리기의 설정은 보안 토큰 처리기 컬렉션에 지정 된 설정을 재정의 합니다.  
  
> [!NOTE]
> IdentityConfiguration > 요소의 자식 요소로 `<serviceTokenResolver>` [요소를 지정 하는 것은 더 이상 사용 되지 않지만 이전 버전과의 호환성을 위해 \<](identityconfiguration.md) 계속 지원 됩니다. 요소의 설정은 `<identityConfiguration>` 요소의 설정을 재정의 합니다. `<securityTokenHandlerConfiguration>`  
  
## <a name="example"></a>예제  
  
```xml  
<serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
```
 