---
title: <securityTokenHandlerConfiguration>
ms.date: 03/30/2017
ms.assetid: 28724cc6-020c-4a06-9a1f-d7594f315019
author: BrucePerlerMS
ms.openlocfilehash: 330e52bd73a8032e4073fe434c852e5bdf8e1d47
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251881"
---
# <a name="securitytokenhandlerconfiguration"></a>\<securityTokenHandlerConfiguration>
토큰 처리기의 컬렉션에 대 한 구성을 제공 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<securityTokenHandlers >** ](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<securityTokenHandlerConfiguration >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration saveBootstrapContext=xs:boolean  
          maximumClockSkew=TimeSpan>  
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
|saveBootstrapContext|부트스트랩 토큰이 세션 토큰에 포함 되어야 하는지 여부를 지정 합니다. `saveBootstrapContext` [IdentityConfiguration > 요소에 대 한 특성을 설정 하 여 토큰 처리기 컬렉션에서 값을 설정할 수도 있습니다. \<](identityconfiguration.md) 토큰 처리기 컬렉션에 설정 된 값은 서비스에 설정 된 값을 재정의 합니다.|  
|maximumClockSkew|허용 되는 최대 클록 오차를 지정 하는입니다.<xref:System.TimeSpan> 로그인 세션이 만료 시간 유효성 검사와 같은 시간에 민감한 작업을 수행할 때 허용 되는 최대 클럭 오차를 제어 합니다. 기본값은 5 분 "00:05:00"입니다. 값을 지정 <xref:System.TimeSpan> 하는 방법에 대 한 자세한 내용은 [Timespan 값](../windows-workflow-foundation/index.md)을 참조 하세요. IdentityConfiguration > 요소 `maximumClockSkew` 에 특성을 설정 하 여 서비스 수준에서 최대 클럭 오차를 설정할 수도 있습니다. [ \<](identityconfiguration.md) 토큰 처리기 컬렉션에 설정 된 값은 서비스에 설정 된 값을 재정의 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<audienceUris>](audienceuris.md)|이 신뢰 당사자의 허용 되는 식별자에 해당 하는 Uri 집합을 지정 합니다. 선택 사항입니다.|  
|[\<caches>](caches.md)|세션 토큰 및 토큰 재생 검색에 사용 되는 캐시를 등록 합니다. 는 서비스 수준 또는 보안 토큰 처리기 컬렉션에서 지정할 수 있습니다. 선택 사항입니다.|  
|[\<certificateValidation>](certificatevalidation.md)|토큰 처리기에서 인증서의 유효성을 검사 하는 데 사용 하는 설정을 제어 합니다. 는 서비스 수준 또는 보안 토큰 처리기 컬렉션에서 지정할 수 있습니다. 이러한 설정은 고유한 유효성 검사기를 사용 하 여 특정 처리기를 구성 하는 경우 재정의 됩니다. 선택 사항입니다.|  
|[\<issuerNameRegistry>](issuernameregistry.md)|토큰 처리기 컬렉션의 처리기에서 사용 하는 발급자 이름 레지스트리를 구성 합니다. 선택 사항입니다.|  
|[\<issuerTokenResolver>](issuertokenresolver.md)|토큰 처리기 컬렉션의 처리기에서 사용 하는 발급자 토큰 확인자를 등록 합니다. 발급자 토큰 확인자는 들어오는 토큰과 메시지의 서명 토큰을 확인 하는 데 사용 됩니다. 선택 사항입니다.|  
|[\<serviceTokenResolver>](servicetokenresolver.md)|토큰 처리기 컬렉션의 처리기에서 사용 하는 서비스 토큰 확인자를 등록 합니다. 서비스 토큰 확인자는 들어오는 토큰과 메시지의 암호화 토큰을 확인 하는 데 사용 됩니다. 선택 사항입니다.|  
|[\<tokenReplayDetection>](tokenreplaydetection.md)|토큰 재생 검색을 사용 하도록 설정 하 고 토큰의 만료 시간을 지정 합니다. 는 서비스 수준 또는 보안 토큰 처리기 컬렉션에서 지정할 수 있습니다. 선택 사항입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<securityTokenHandlers>](securitytokenhandlers.md)|끝점에 등록 된 보안 토큰 처리기의 컬렉션을 지정 합니다.|  
  
## <a name="remarks"></a>설명  
 이 섹션에서는 <xref:System.IdentityModel.Tokens.SecurityTokenHandlerConfiguration> 개체의 속성 값을 제공 합니다. 이 섹션에서 구성 된 설정은 서비스에 구성 된 설정을 재정의 합니다. 이러한 설정 중 일부는 보안 토큰 처리기 컬렉션에 처리기를 추가할 때 지정 된 설정에 의해 재정의 될 수 있습니다.  
  
## <a name="example"></a>예제  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>   
      <securityTokenHandlerConfiguration>  
  
        <audienceUris>  
          <clear/>  
          <add value="http://www.example.com/myapp/" />  
        </audienceUris>  
  
        <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel">  
          <trustedIssuers>  
            <add thumbprint="97249e1a … 4c9158de" name="contoso.com" />  
          </trustedIssuers>  
        </issuerNameRegistry>  
  
        <issuerTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
  
        <serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```
