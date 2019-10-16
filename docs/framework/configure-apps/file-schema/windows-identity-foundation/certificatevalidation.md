---
title: <certificateValidation>
ms.date: 03/30/2017
ms.assetid: 6c54c704-b55e-4631-88ff-4d4a5621554c
author: BrucePerlerMS
ms.openlocfilehash: c2d1a5d36cb5616ef06eedc093dd70a68a164a81
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252129"
---
# <a name="certificatevalidation"></a>\<certificateValidation>
토큰 처리기에서 인증서의 유효성을 검사 하는 데 사용 하는 설정을 제어 합니다. 이러한 설정은 고유한 유효성 검사기를 사용 하 여 특정 처리기를 구성 하는 경우 재정의 됩니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<identityConfiguration >** ](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<certificateValidation >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <certificateValidation  
      certificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
      revocationMode="NoCheck||Offline||Online"  
      trustedStoreLocation="CurrentLocation||LocalMachine" >  
    </certificateValidation>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|certificateValidationMode|X.509 인증서에 사용할 유효성 검사 모드를 지정 하는 값입니다.<xref:System.ServiceModel.Security.X509CertificateValidationMode> 기본값은 "PeerOrChainTrust"입니다. 사용자 지정 유효성 검사기를 지정 하려면이 특성을 "custom"으로 설정 하 고 [ \<certificateValidator >](certificatevalidator.md) 요소를 사용 하 여 유효성 검사기를 지정 합니다. 선택 사항입니다.|  
|revocationMode|X.509 인증서에 사용할 해지 모드를 지정 하는 값입니다.<xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 기본값은 "Online"입니다. 선택 사항입니다.|  
|trustedStoreLocation|X.509 인증서 저장소를 지정 하는 값입니다.<xref:System.Security.Cryptography.X509Certificates.StoreLocation> 기본값은 "LocalMachine"입니다. 선택 사항입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<certificateValidator>](certificatevalidator.md)|인증서 유효성 검사에 대 한 사용자 지정 형식을 지정 합니다. 이 형식은 `certificateValidationMode` [ \<certificatevalidation >](certificatevalidation.md) 요소의 특성이 "Custom"으로 설정 된 경우에만 사용 됩니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<identityConfiguration>](identityconfiguration.md)|서비스 수준 id 설정을 지정 합니다.|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|보안 토큰 처리기의 컬렉션에 대 한 구성을 제공 합니다.|  
  
## <a name="remarks"></a>설명  
 요소는 요소 아래의 서비스 수준 `<identityConfiguration>` 또는 요소의 보안 토큰 `<securityTokenHandlerConfiguration>` 처리기 컬렉션 수준에서 지정할 수 있습니다. `<certificateValidation>` 토큰 처리기 컬렉션의 설정은 서비스에 지정 된 설정을 재정의 합니다. 일부 토큰 처리기를 사용 하면 구성에서 인증서 유효성 검사 설정을 지정할 수 있습니다. 개별 토큰 처리기의 설정은 서비스 수준 및 보안 토큰 처리기 컬렉션 둘 다에서 지정 된 설정을 재정의 합니다.  
  
## <a name="example"></a>예제  
  
```xml  
<certificateValidation certificateValidationMode="PeerOrChainTrust"  
                       revocationMode="Online"  
                       trustedStoreLocation="LocalMachine" />  
```
