---
title: <serviceAuthorization> 요소
ms.date: 03/30/2017
ms.assetid: 18cddad5-ddcb-4839-a0ac-1d6f6ab783ca
ms.openlocfilehash: f476f754a340f52859be2986e42754cba0ef3771
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834018"
---
# <a name="serviceauthorization-element"></a>\<serviceAuthorization > 요소

서비스 작업에 대한 액세스 권한을 부여하는 설정을 지정합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp; @ no__t-1 @ no__t-2[ **&nbsp;-6behaviors >** ](behaviors.md)\
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5[ **\<serviceBehaviors >** ](servicebehaviors.md)\
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7[ **&nbsp;0 behavior >** ](behavior-of-servicebehaviors.md)1
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7 @ no__t-8 @ no__t-9 **&nbsp;1serviceAuthorization >**  

## <a name="syntax"></a>구문

```xml
<serviceAuthorization impersonateCallerForAllOperations="Boolean"
                      principalPermissionMode="None/UseWindowsGroups/UseAspNetRoles/Custom"
                      roleProviderName="String"
                      serviceAuthorizationManagerType="String">
  <authorizationPolicies>
    <add policyType="String" />
  </authorizationPolicies>
</serviceAuthorization>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명 합니다.

### <a name="attributes"></a>특성

|특성|설명|  
|---------------|-----------------|  
|impersonateCallerForAllOperations|서비스의 모든 작업이 호출자를 가장하는지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 특정 서비스 작업이 호출자를 가장하면 지정된 서비스를 실행하기 전에 스레드 컨텍스트가 호출자 컨텍스트로 전환됩니다.|  
|principalPermissionMode|서버에서 작업을 수행할 때 사용되는 사용자를 설정합니다. 여기에는 다음 값이 포함됩니다.<br /><br /> -None<br />-   UseWindowsGroups<br />-   UseAspNetRoles<br />-Custom<br /><br /> 기본값은 UseWindowsGroups입니다. 값은 <xref:System.ServiceModel.Description.PrincipalPermissionMode> 형식입니다. 이 특성을 사용 하는 방법에 대 한 자세한 내용은 [How to: PrincipalPermissionAttribute 클래스 @ no__t-0을 사용 하 여 액세스를 제한 합니다.|  
|roleProviderName|역할 공급자의 이름을 지정하는 문자열로, WCF(Windows Communication Foundation) 애플리케이션에 대한 역할 정보를 제공합니다. 기본값은 빈 문자열입니다.|  
|ServiceAuthorizationManagerType|서비스 인증 관리자의 형식을 포함하는 문자열입니다. 자세한 내용은 <xref:System.ServiceModel.ServiceAuthorizationManager>을 참조하세요.|  

### <a name="child-elements"></a>자식 요소

|요소|설명|  
|-------------|-----------------|  
|authorizationPolicies|`add` 키워드를 사용하여 추가할 수 있는 인증 정책 형식 컬렉션이 포함되어 있습니다. 각 인증 정책에는 문자열에 해당하는 단일 필수 `policyType` 특성이 포함되어 있습니다. 이 특성은 한 입력 클레임 집합을 다른 클레임 집합으로 변환할 수 있도록 하는 인증 정책을 지정합니다. 그에 따라 액세스 제어가 부여되거나 거부됩니다. 자세한 내용은 <xref:System.ServiceModel.Configuration.AuthorizationPolicyTypeElement>을 참조하세요.|  

### <a name="parent-elements"></a>부모 요소

|요소|설명|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|서비스의 동작에 대한 설정 컬렉션을 포함합니다.|  

## <a name="remarks"></a>설명

이 섹션에는 권한 부여, 사용자 지정 역할 공급자 및 가장에 영향을 주는 요소가 포함되어 있습니다.  
  
`principalPermissionMode` 특성은 보호된 메서드의 사용 권한을 부여할 때 사용할 사용자 그룹을 지정합니다. 기본값은 `UseWindowsGroups`이며 리소스에 액세스하려는 ID에 대해 "Administrators" 또는 "Users"와 같은 Windows 그룹을 검색하도록 지정합니다. 다음 코드와 같이 @no__t -1system > 요소 아래에 구성 된 사용자 지정 역할 공급자를 사용 하려면 @no__t를 지정할 수도 있습니다.

```xml
<system.web>
  <membership defaultProvider="SqlProvider"
              userIsOnlineTimeWindow="15">
    <providers>
      <clear />
      <add name="SqlProvider"
           type="System.Web.Security.SqlMembershipProvider"
           connectionStringName="SqlConn"
           applicationName="MembershipProvider"
           enablePasswordRetrieval="false"
           enablePasswordReset="false"
           requiresQuestionAndAnswer="false"
           requiresUniqueEmail="true"
           passwordFormat="Hashed" />
    </providers>
  </membership>
  <!-- Other configuration code not shown. -->
</system.web>
```
  
다음 코드에서는 `principalPermissionMode` 특성과 함께 사용 되는 @no__t를 보여 줍니다.
  
```xml
<behaviors>
  <behavior name="ServiceBehaviour">
    <serviceAuthorization principalPermissionMode ="UseAspNetRoles"
                          roleProviderName ="SqlProvider" />
  </behavior>
  <!-- Other configuration code not shown. -->
</behaviors>
```

이 구성 요소 사용에 대 한 자세한 예제는 서비스 작업 및 [권한 부여 정책](../../../wcf/samples/authorization-policy.md)에 대 한 [액세스 권한 부여](../../../wcf/samples/authorizing-access-to-service-operations.md) 를 참조 하세요.
  
## <a name="see-also"></a>참조

- <xref:System.ServiceModel.Configuration.ServiceAuthorizationElement>
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>
- [보안 동작](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [서비스 작업에 대한 액세스 승인](../../../wcf/samples/authorizing-access-to-service-operations.md)
- [방법: 서비스에 대 한 사용자 지정 권한 부여 관리자 만들기 @ no__t-0
- [방법: PrincipalPermissionAttribute 클래스를 사용 하 여 액세스 제한 @ no__t-0
- [권한 부여 정책](../../../wcf/samples/authorization-policy.md)
