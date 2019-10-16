---
title: <issuerNameRegistry>
ms.date: 03/30/2017
ms.assetid: 58b39d12-c953-40c4-88af-d7eb3343ca28
author: BrucePerlerMS
ms.openlocfilehash: 209e702da80f2569f2b6c068f50f1af4489157f6
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251961"
---
# <a name="issuernameregistry"></a>\<issuerNameRegistry>
토큰 처리기 컬렉션의 처리기에서 사용 하는 발급자 이름 레지스트리를 구성 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlers >** ](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlerConfiguration >** ](securitytokenhandlerconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<issuerNameRegistry >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerNameRegistry type=xs:string>  
          <optionalCustomConfigurationElements />  
        </issuerNameRegistry>  
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
|type|<xref:System.IdentityModel.Tokens.IssuerNameRegistry> 클래스에서 파생 되는 형식입니다. 사용자 지정 `type`을 지정 하는 방법에 대 한 자세한 내용은 [사용자 지정 형식 참조]를 참조 하세요.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<trustedIssuers>](trustedissuers.md)|특성이 구성 기반 발급자 이름 레지스트리 <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> (클래스)를 [ \<](trustedissuers.md) 지정 하는 경우 s > 요소를 지정 해야 합니다. `type` [ \<S >](trustedissuers.md) 요소는, 또는 `<add>`요소를 `<clear>`자식 요소로사용할수있습니다`<remove>` .|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|보안 토큰 처리기의 컬렉션에 대 한 구성을 제공 합니다.|  
  
## <a name="remarks"></a>설명  
 발급자 이름 레지스트리를 사용 하 여 모든 발급자 토큰의 유효성을 검사 합니다. <xref:System.IdentityModel.Tokens.IssuerNameRegistry> 클래스에서 파생 되는 개체입니다. 발급자 이름 레지스트리는 니모닉 이름을 해당 발급자가 생성 한 토큰의 서명을 확인 하는 데 필요한 암호화 자료에 연결 하는 데 사용 됩니다. 발급자 이름 레지스트리는 RP (신뢰 당사자) 응용 프로그램에서 신뢰할 수 있는 발급자 목록을 유지 관리 합니다. 발급자 이름 레지스트리의 형식은 특성을 `type` 사용 하 여 지정 합니다. 요소 `<issuerNameRegistry>` 는 지정 된 형식에 대 한 구성을 제공 하는 하나 이상의 자식 요소를 포함할 수 있습니다. 메서드를 <xref:System.IdentityModel.Tokens.IssuerNameRegistry.LoadCustomConfiguration%2A> 재정의 하 여 이러한 자식 요소를 처리 하는 논리를 제공 합니다.  
  
 WIF은 기본적으로 <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> 클래스의 단일 발급자 이름 레지스트리 유형을 제공 합니다. 이 클래스는 구성에 지정 된 신뢰할 수 있는 발급자 인증서 집합을 사용 합니다. 여기에는 신뢰할 수 있는 발급자 `<trustedIssuers>`인증서의 컬렉션을 구성 하는 자식 구성 요소가 필요 합니다. 신뢰할 수 있는 인증서는 ASN으로 인코딩된 인증서 지문 형태를 사용 하 여 지정 되며, 또는 `<add>` `<remove>` 요소를 `<clear>`사용 하 여 컬렉션에서 추가 되거나 제거 됩니다.  
  
 합니다 `<issuerNameRegistry>` 에서 요소가 표시 되는 <xref:System.IdentityModel.Configuration.IssuerNameRegistryElement> 클래스입니다.  
  
> [!NOTE]
> IdentityConfiguration > 요소의 자식 요소로 `<issuerNameRegistry>` [요소를 지정 하는 것은 더 이상 사용 되지 않지만 이전 버전과의 호환성을 위해 \<](identityconfiguration.md) 계속 지원 됩니다. 요소의 설정은 `<identityConfiguration>` 요소의 설정을 재정의 합니다. `<securityTokenHandlerConfiguration>`  
  
## <a name="example"></a>예제  
 다음 XML에서는 구성 기반 발급자 이름 레지스트리를 지정 하는 방법을 보여 줍니다.  
  
```xml  
<issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
  <trustedIssuers>  
    <add thumbprint="9B74CB … 1EF40D0" name="LocalSTS" />  
  </trustedIssuers>  
</issuerNameRegistry>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Tokens.IssuerNameRegistry>
- <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>
