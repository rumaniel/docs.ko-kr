---
title: <userNameAuthentication>
ms.date: 03/30/2017
ms.assetid: 24d8b398-770f-418f-ba23-c4325419cfa6
ms.openlocfilehash: dc5c00a2204646863ae2570bb97b8d70e22a72d4
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399192"
---
# <a name="usernameauthentication"></a>\<userNameAuthentication>
사용자 이름 및 암호에 따라 서비스의 자격 증명을 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceBehaviors >** ](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceCredentials >** ](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<userNameAuthentication >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<userNameAuthentication cacheLogonTokenLifetime="TimeSpan"
                        cacheLogonTokens="Boolean"
                        customUserNamePasswordValidatorType="String"
                        includeWindowsGroups="Boolean"
                        maxCacheLogonTokens="Integer"
                        membershipProviderName="String"
                        userNamePasswordValidationMode="Windows/MembershipProvider/Custom" />
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`cacheLogonTokenLifetime`|토큰이 캐시되는 최대 시간 길이를 지정하는 <xref:System.TimeSpan>입니다. 기본값은 00:15:00입니다.|  
|`cacheLogonTokens`|로그온 토큰 캐시 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.|  
|`customUserNamePasswordValidatorType`|사용되는 사용자 지정 사용자 이름 암호 유효성 검사기 형식을 지정하는 문자열입니다. 기본값은 빈 문자열입니다.|  
|`includeWindowsGroups`|Windows 그룹이 보안 컨텍스트에 포함되는지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.<br /><br /> 이 특성을 `true`로 설정하면 전체 그룹이 확장되므로 성능에 영향을 줍니다. 사용자가 속한 그룹의 목록을 설정할 필요가 없으면 이 속성을 `false`로 설정합니다.|  
|`maxCacheLogonTokens`|캐시할 로그온 토큰의 최대 수를 지정하는 정수입니다. 이 값은 0보다 커야 합니다. 기본값은 128입니다.|  
|`membershipProviderName`|바인딩의 `clientCredentialType` 특성이 `username`으로 설정되면 사용자 이름이 Windows 계정에 매핑됩니다. 이 특성을 사용하여 이 동작을 재정의할 수 있습니다. 해당 특성은 관련 암호 유효성 검사 메커니즘을 제공하는 <xref:System.Web.Security.MembershipProvider> 값의 이름을 포함하는 문자열입니다.|  
|`userNamePasswordValidationMode`|사용자 이름 암호의 유효성 검사 방식을 지정합니다. 유효한 값은<br /><br /> -   Windows<br />-MembershipProvider<br />-Custom<br /><br /> 기본값은 Windows입니다. 이 특성은 <xref:System.ServiceModel.Security.UserNamePasswordValidationMode> 형식입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<serviceCredentials>](servicecredentials.md)|서비스를 인증하는 데 사용되는 자격 증명 및 클라이언트 자격 증명 확인 관련 설정을 지정합니다.|  
  
## <a name="remarks"></a>설명  
 사용자 이름/암호 기반 인증을 위해 구성된 서비스에서 사용하는 바인딩이 없으면 이 요소의 특성이 무시됩니다. 이것에는 `customUserNamePasswordValidatorType`, `includeWindowsGroups`, `membershipProviderName` 및 `userNamePasswordValidationMode`가 있습니다.  
  
 사용자 이름/암호에 대한 Windows 인증을 사용하기 위해 구성된 서비스에서 사용하는 바인딩이 없으면 로그온 토큰의 캐싱과 관련된 설정이 무시됩니다. 이것에는 `cacheLogonTokenLifetime`, `cacheLogonTokens` 및 `maxCacheLogonTokens`가 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.UserNameServiceElement>
- <xref:System.ServiceModel.Description.ServiceCredentials.UserNameAuthentication%2A>
- <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential>
- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.UserNameAuthentication%2A>
