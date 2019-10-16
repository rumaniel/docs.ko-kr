---
title: <trustedIssuers>
ms.date: 03/30/2017
ms.assetid: d818c917-07b4-40db-9801-8676561859fd
author: BrucePerlerMS
ms.openlocfilehash: 50fc7194823fb0c5c426fb54ffd50b17c3714ed9
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251752"
---
# <a name="trustedissuers"></a>\<trustedIssuers>
구성 기반 발급자 이름 레지스트리 (<xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>)에서 사용 하는 신뢰할 수 있는 발급자 인증서 목록을 구성 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlers >** ](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlerConfiguration >** ](securitytokenhandlerconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<issuerNameRegistry >** ](issuernameregistry.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<s >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerNameRegistry>  
          <trustedIssuers>  
            <add thumbprint=xs:string name=xs:string>  
            <clear>  
            <remove thumbprint=xs:string>  
          </trustedIssuers>  
        </issuerNameRegistry>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`<add thumbprint=xs:string name=xs:string>`|신뢰할 수 있는 발급자 컬렉션에 인증서를 추가 합니다. 인증서는 `thumbprint` 특성을 사용 하 여 지정 됩니다. 이 특성은 필수 이며, asn.1.1로 인코딩된 인증서 지문 형식을 포함 해야 합니다. 특성 `name` 은 선택 사항이 며 인증서의 이름을 지정 하는 데 사용할 수 있습니다.|  
|`<clear>`|신뢰할 수 있는 발급자 컬렉션에서 모든 인증서를 지웁니다.|  
|`<remove thumbprint=xs:string>`|신뢰할 수 있는 발급자 컬렉션에서 인증서를 제거 합니다. 인증서는 `thumbprint` 특성을 사용 하 여 지정 됩니다. 필수 특성입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<issuerNameRegistry>](issuernameregistry.md)|발급자 이름 레지스트리를 구성 합니다. **중요:**  요소의 `type` 특성 `<issuerNameRegistry>` 은 `<trustedIssuers>` 요소에 대 한 클래스 <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> 를 참조 해야 유효 합니다.|  
  
## <a name="remarks"></a>설명  
 WIF (Windows Identity Foundation)는 클래스의 단일 구현을 <xref:System.IdentityModel.Tokens.IssuerNameRegistry> <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> 제공 합니다. 클래스는 클래스입니다. 구성 발급자 이름 레지스트리는 구성에서 로드 되는 신뢰할 수 있는 발급자의 목록을 유지 관리 합니다. 목록은 각 발급자 이름을 발급자가 생성 한 토큰의 서명을 확인 하는 데 필요한 x.509 인증서와 연결 합니다. 신뢰할 수 있는 발급자 인증서의 목록은 `<trustedIssuers>` 요소 아래에 지정 되어 있습니다. 목록의 각 요소는 니모닉 발급자 이름과 해당 발급자가 생성 한 토큰의 서명을 확인 하는 데 필요한 x.509 인증서를 연결 합니다. 신뢰할 수 있는 인증서는 asn.1로 인코딩된 인증서 지문 형태를 사용 하 여 지정 되 고 요소를 사용 `<add>` 하 여 컬렉션에 추가 됩니다. `<clear>` 및`<remove>` 요소를 사용 하 여 목록에서 발급자 (인증서)를 지우거 나 제거할 수 있습니다.  
  
 요소의 `type` 특성 `<issuerNameRegistry>` 은 `<trustedIssuers>` 요소에 대 한 클래스 <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> 를 참조 해야 유효 합니다.  
  
## <a name="example"></a>예제  
 다음 XML에서는 구성 기반 발급자 이름 레지스트리를 지정 하는 방법을 보여 줍니다.  
  
```xml  
<issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
  <trustedIssuers>  
    <add thumbprint="9B74CB2F32 … B1DC01EF40D0" name="LocalSTS" />  
  </trustedIssuers>  
</issuerNameRegistry>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>
- <xref:System.IdentityModel.Tokens.IssuerNameRegistry>
