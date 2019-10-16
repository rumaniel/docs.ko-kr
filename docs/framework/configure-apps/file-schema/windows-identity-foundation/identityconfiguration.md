---
title: <identityConfiguration>
ms.date: 03/30/2017
ms.assetid: 1db76253-07da-447b-9e7a-3705c7228cf4
author: BrucePerlerMS
ms.openlocfilehash: 0fa8c574fd5663606cf081f1000a24884306edfe
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251991"
---
# <a name="identityconfiguration"></a>\<identityConfiguration>

서비스 수준 id 설정을 지정 합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<identityConfiguration >**  

## <a name="syntax"></a>구문

```xml
<system.identityModel>
  <identityConfiguration
      name=xs:string
      saveBootstrapContext=xs:boolean>
      maximumClockSkew=TimeSpan >
  </identityConfiguration>
</system.identityModel>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|Description|
|---------------|-----------------|
|name|Id 구성 섹션의 이름입니다. 이 이름을 사용 하 여 특정 구성 섹션을 참조할 수 있습니다. 특성을 `name` 지정 하지 않으면 섹션에서 기본 구성을 정의 합니다. 기본 구성은 항상 수동 페더레이션 시나리오에 사용 됩니다. 자세한 내용은 [ \<federationConfiguration >](federationconfiguration.md) 요소를 참조 하세요.|
|saveBootstrapContext|부트스트랩 토큰이 세션 토큰에 포함 되어야 하는지 여부를 지정 합니다. `saveBootstrapContext` [SecurityTokenHandlerConfiguration > 요소에 대 한 특성을 설정 하 여 토큰 처리기 컬렉션에서 값을 설정할 수도 있습니다. \<](securitytokenhandlerconfiguration.md) 토큰 처리기 컬렉션에 설정 된 값은 서비스에 설정 된 값을 재정의 합니다.|
|maximumClockSkew|허용 되는 최대 클록 오차를 지정 하는입니다.<xref:System.TimeSpan> 로그인 세션이 만료 시간 유효성 검사와 같은 시간에 민감한 작업을 수행할 때 허용 되는 최대 클럭 오차를 제어 합니다. 기본값은 5 분 "00:05:00"입니다. 값을 지정 <xref:System.TimeSpan> 하는 방법에 대 한 자세한 내용은 [Timespan 값](../windows-workflow-foundation/index.md)을 참조 하세요. `maximumClockSkew` [SecurityTokenHandlerConfiguration > 요소에 대 한 특성을 설정 하 여 토큰 처리기 컬렉션에서 최대 클록 오차를 설정할 수도 있습니다. \<](securitytokenhandlerconfiguration.md) 토큰 처리기 컬렉션에 설정 된 값은 서비스에 설정 된 값을 재정의 합니다.|

### <a name="child-elements"></a>자식 요소

|요소|Description|
|-------------|-----------------|
|[\<caches>](caches.md)|세션 토큰 및 토큰 재생 검색에 사용 되는 캐시를 등록 합니다. 는 서비스 수준 또는 보안 토큰 처리기 컬렉션에서 지정할 수 있습니다. 선택 사항입니다.|
|[\<certificateValidation>](certificatevalidation.md)|토큰 처리기에서 인증서의 유효성을 검사 하는 데 사용 하는 설정을 제어 합니다. 는 서비스 수준 또는 보안 토큰 처리기 컬렉션에서 지정할 수 있습니다. 선택 사항입니다.|
|[\<claimsAuthenticationManager>](claimsauthenticationmanager.md)|들어오는 클레임에 대 한 클레임 인증 관리자를 등록 합니다. 선택 사항입니다.|
|[\<claimsAuthorizationManager>](claimsauthorizationmanager.md)|들어오는 클레임에 대 한 클레임 권한 부여 관리자를 등록 합니다. 선택 사항입니다.|
|[\<claimTypeRequired>](claimtyperequired.md)|들어오는 보안 토큰에 대 한 필수 클레임 집합을 지정 합니다. 선택 사항입니다.|
|[\<securityTokenHandlers>](securitytokenhandlers.md)|보안 토큰 처리기의 컬렉션을 지정 합니다. 0 개 이상의 보안 토큰 처리기 컬렉션을 지정할 수 있습니다. 선택 사항입니다.|
|[\<tokenReplayDetection>](tokenreplaydetection.md)|토큰 재생 검색을 사용 하도록 설정 하 고 토큰의 만료 시간을 지정 합니다. 는 서비스 수준 또는 보안 토큰 처리기 컬렉션에서 지정할 수 있습니다. 선택 사항입니다.|

### <a name="parent-elements"></a>부모 요소

|요소|Description|
|-------------|-----------------|
|[\<system.identityModel>](system-identitymodel.md)|응용 프로그램에서 WIF (Windows Identity Foundation) 옵션을 사용 하도록 구성 하는 구성을 제공 합니다.|

## <a name="remarks"></a>설명

각각 고유한 이름을 가진 여러 id 구성이 정의 될 수 있습니다. 동작은 다음과 같습니다.

1. 요소가 지정 `<identityConfiguration>` 되지 않은 경우입니다. 기본 id 구성은 런타임에 만들어지며 기본값으로 채워집니다.

2. 단일 `<identityConfiguration>` 요소가 지정 된 경우 기본 id 구성입니다. 이름이 지정 되거나 이름이 지정 되지 않은 경우에는 중요 하지 않습니다.

3. 여러 `<identityConfiguration>` 요소가 지정 된 경우입니다. 명명 되지 않은 요소는 기본 id 구성을 지정 합니다. 여러 `<identityConfiguration>` 요소를 지정 하는 경우 둘 중 하나를 명명 되지 않은 상태로 지정 하는 것이 좋습니다.

> [!WARNING]
> 여러 `<identityConfiguration>` 요소를 지정 하는 경우 그 중 하나에 이름이 지정 되지 않아야 합니다. 명명 되지 않은 요소는 기본 id 구성입니다.

 `<identityConfiguration>` 요소에 지정 된 설정 중 일부는 보안 토큰 처리기 컬렉션의 설정 또는 개별 보안 토큰 처리기의 설정에 의해 재정의 될 수 있습니다.

> [!IMPORTANT]
> 또는 클래스를 사용 하 여 `<federationConfiguration>` 코드에서 클레임 기반 액세스 제어를 제공 하는 경우 요소에서 참조 하는 id 구성은 클레임 권한 부여 관리자 및 다음을 수행 하는 데 사용 되는 정책을 구성 합니다. <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> 권한 부여 결정. 이는 Windows Communication Foundation (WCF) 응용 프로그램 또는 웹 기반이 아닌 응용 프로그램 등 수동 웹 시나리오가 아닌 시나리오 에서도 마찬가지입니다. 응용 프로그램이 수동 웹 응용 프로그램이 [ \<](claimsauthorizationmanager.md) 아닌 경우 참조 되는 id 구성의 claimsAuthorizationManager > 요소와 자식 정책 요소 (있는 경우)만 적용 됩니다. 다른 모든 설정은 무시 됩니다. 자세한 내용은 [ \<federationConfiguration >](federationconfiguration.md) 요소를 참조 하세요.

합니다 `<identityConfiguration>` 에서 요소가 표시 되는 <xref:System.IdentityModel.Configuration.IdentityConfigurationElement> 클래스입니다. Id 구성 섹션은 <xref:System.IdentityModel.Configuration.IdentityConfiguration> 클래스로 표현 됩니다.

> [!IMPORTANT]
> 다음 요소를 `<identityConfiguration>` 요소의 자식 요소로 지정 하는 기능은 이전 버전과의 호환성을 위해 계속 지원 되지만 더 이상 사용 되지 않습니다. 대신 이러한 요소는 [ \<securityTokenHandlerConfiguration >](securitytokenhandlerconfiguration.md) 요소 아래에 지정 해야 합니다.
>
> - [\<audienceUris>](audienceuris.md)
> - [\<issuerNameRegistry>](issuernameregistry.md)
> - [\<issuerTokenResolver>](issuertokenresolver.md)
> - [\<serviceTokenResolver>](servicetokenresolver.md)

## <a name="example"></a>예제

다음 예에서는 "alternateConfiguration" 라는 id 구성을 만듭니다. Id 구성에서는 기본 설정을 지정 합니다.

```xml
<system.identityModel>
    <identityConfiguration name="alternateConfiguration"/>
</system.identityModel>
```

## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Configuration.IdentityConfiguration>
- <xref:System.IdentityModel.Configuration.IdentityConfigurationElement>
