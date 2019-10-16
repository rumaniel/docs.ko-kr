---
title: <issuerTokenResolver>
ms.date: 03/30/2017
ms.assetid: f74392f6-3f5b-4880-bd8a-3a9130d31e65
author: BrucePerlerMS
ms.openlocfilehash: 8775e3044e58886cfa53a9fd9fc8b4b8ed2105b5
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251947"
---
# <a name="issuertokenresolver"></a>\<issuerTokenResolver>
토큰 처리기 컬렉션의 처리기에서 사용 하는 발급자 토큰 확인자를 등록 합니다. 발급자 토큰 확인자는 들어오는 토큰과 메시지의 서명 토큰을 확인 하는 데 사용 됩니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlers >** ](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlerConfiguration >** ](securitytokenhandlerconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<issuerTokenResolver >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerTokenResolver type=xs:string>  
        </issuerTokenResolver>  
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
|type|발급자 토큰 확인자 유형을 지정 합니다. 클래스 또는 <xref:System.IdentityModel.Tokens.IssuerTokenResolver> 클래스에서 파생 되는 형식 이어야 합니다. <xref:System.IdentityModel.Tokens.IssuerTokenResolver> 필수 요소.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|보안 토큰 처리기의 컬렉션에 대 한 구성을 제공 합니다.|  
  
## <a name="remarks"></a>설명  
 발급자 토큰 확인자는 들어오는 토큰과 메시지의 서명 토큰을 확인 하는 데 사용 됩니다. 서명을 확인 하는 데 사용 되는 암호화 자료를 검색 하는 데 사용 됩니다. 특성을 `type` 지정 해야 합니다. 지정 된 형식은 <xref:System.IdentityModel.Tokens.IssuerTokenResolver> 이거나 <xref:System.IdentityModel.Tokens.IssuerTokenResolver> 클래스에서 파생 되는 사용자 지정 형식일 수 있습니다.  
  
 일부 토큰 처리기를 사용 하면 구성에서 발급자 토큰 확인자 설정을 지정할 수 있습니다. 개별 토큰 처리기의 설정은 보안 토큰 처리기 컬렉션에 지정 된 설정을 재정의 합니다.  
  
> [!NOTE]
> IdentityConfiguration > 요소의 자식 요소로 `<issuerTokenResolver>` [요소를 지정 하는 것은 더 이상 사용 되지 않지만 이전 버전과의 호환성을 위해 \<](identityconfiguration.md) 계속 지원 됩니다. 요소의 설정은 `<identityConfiguration>` 요소의 설정을 재정의 합니다. `<securityTokenHandlerConfiguration>`  
  
## <a name="example"></a>예제  
 다음 XML에서는에서 <xref:System.IdentityModel.Tokens.IssuerTokenResolver>파생 되는 사용자 지정 클래스를 기반으로 하는 발급자 토큰 확인자에 대 한 구성을 보여 줍니다. 토큰 확인자는 클래스에 대해 정의 된 사용자 지정 구성 요소 (`<AddAudienceKeyPair>`)에서 초기화 되는 대상 키 쌍의 사전을 유지 관리 합니다. 클래스는 <xref:System.IdentityModel.Selectors.SecurityTokenResolver.LoadCustomConfiguration%2A> 메서드를 재정의 하 여이 요소를 처리 합니다. 재정의는 다음 예제에 나와 있습니다. 그러나 호출 하는 메서드는 간결 하 게 표시 되지 않습니다. 전체 예제는 `CustomToken` 샘플을 참조 하세요.  
  
```xml  
<issuerTokenResolver type="SimpleWebToken.CustomIssuerTokenResolver, SimpleWebToken">  
  <AddAudienceKeyPair  symmetricKey="wAVkldQiFypTQ+kdNdGWCYCHRcee8XmXxOvgmak8vSY=" audience="http://localhost:19851/" />  
</issuerTokenResolver>  
```  
  
## <a name="example"></a>예제  
  
```  
public override void LoadCustomConfiguration(System.Xml.XmlNodeList nodelist)  
{  
    foreach (XmlNode node in nodelist)  
    {  
        XmlDictionaryReader rdr = XmlDictionaryReader.CreateDictionaryReader(new XmlTextReader(new StringReader(node.OuterXml)));  
        rdr.MoveToContent();  
  
        string symmetricKey = rdr.GetAttribute("symmetricKey");  
        string audience = rdr.GetAttribute("audience");  
  
        this.AddAudienceKeyPair(audience, symmetricKey);  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Tokens.IssuerTokenResolver>
