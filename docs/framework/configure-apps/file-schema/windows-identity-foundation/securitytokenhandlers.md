---
title: <securityTokenHandlers>
ms.date: 03/30/2017
ms.assetid: f11a631d-4094-4e11-bb03-4ede74b30281
author: BrucePerlerMS
ms.openlocfilehash: 017309436660991c69da569e9cc4219e842ecaa3
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251869"
---
# <a name="securitytokenhandlers"></a>\<securityTokenHandlers>
끝점에 등록 된 보안 토큰 처리기의 컬렉션을 지정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<securityTokenHandlers >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|name|토큰 처리기 컬렉션의 이름을 지정 합니다. 프레임 워크에서 인식 되는 값은 "ActAs" 및 "OnBehalfOf" 뿐입니다. 이러한 이름 중 하나를 사용 하 여 토큰 처리기 컬렉션을 지정 하면 ActAs 또는 OnBehalfOf 토큰을 각각 처리할 때 컬렉션이 사용 됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<add>](add.md)|토큰 처리기 컬렉션에 보안 토큰 처리기를 추가 합니다.|  
|[\<clear>](clear.md)|토큰 처리기 컬렉션에서 모든 보안 토큰 처리기를 지웁니다.|  
|[\<remove>](remove.md)|토큰 처리기 컬렉션에서 보안 토큰 처리기를 제거 합니다.|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|토큰 처리기의 컬렉션에 대 한 구성을 제공 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<identityConfiguration>](identityconfiguration.md)|서비스 수준 id 설정을 지정 합니다.|  
  
## <a name="remarks"></a>설명  
 서비스 구성에서 보안 토큰 처리기의 명명 된 컬렉션을 하나 이상 지정할 수 있습니다. 특성을 `name` 사용 하 여 컬렉션의 이름을 지정할 수 있습니다. 프레임 워크를 처리 하는 유일한 이름에는 "ActAs" 및 "OnBehalfOf"입니다. 이러한 컬렉션에 처리기가 있는 경우 및 토큰을 처리 `ActAs` 하 `OnBehalfOf` 는 경우 기본 처리기 대신 STS (보안 토큰 서비스)에서 사용 됩니다.  
  
 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>기본적으로 컬렉션은 <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> ,<xref:System.IdentityModel.Tokens.EncryptedSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.KerberosSecurityTokenHandler>, <xref:System.IdentityModel.Tokens.WindowsUserNameSecurityTokenHandler> ,,<xref:System.IdentityModel.Tokens.RsaSecurityTokenHandler>및 처리기 형식으로 채워집니다. <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler> `<add>` ,`<remove>`및 요소`<clear>` 를 사용 하 여 컬렉션을 수정할 수 있습니다. 컬렉션에 특정 형식의 처리기가 하나만 있는지 확인 해야 합니다. 예를 들어 <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> 클래스에서 처리기를 파생 하는 경우 처리기 또는는 단일 컬렉션에서 <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> 구성 될 수 있지만 둘 다로 구성 될 수는 없습니다.  
  
 `<securityTokenHandlerConfiguration>` 요소를 사용 하 여 컬렉션의 처리기에 대 한 구성 설정을 지정 합니다. 이 요소를 통해 지정 된 설정은 [ \<identityConfiguration >](identityconfiguration.md) 요소를 통해 서비스에 지정 된 설정을 재정의 합니다. 일부 처리기 (몇 가지 기본 제공 처리기 형식 포함)는 `<add>` 요소의 자식 요소를 통해 추가 구성을 지원할 수 있습니다. 처리기에 지정 된 설정이 컬렉션 또는 서비스에 지정 된 것과 동일한 설정을 재정의 합니다.
