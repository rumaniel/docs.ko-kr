---
title: <certificateReference>
ms.date: 03/30/2017
ms.assetid: 2ac8bc14-e9f1-48fb-b662-f5991558fbe4
author: BrucePerlerMS
ms.openlocfilehash: 782ca3344774b8412a18e3cf13bff5f969751ea3
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252150"
---
# <a name="certificatereference"></a>\<certificateReference>
인증서 저장소에서 x.509 인증서를 찾고 유효성을 검사 하는 데 사용 되는 설정을 지정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.identitymodel >** ](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<federationConfiguration >** ](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceCertificate >** ](servicecertificate.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<certificateReference >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <serviceCertificate>  
      <certificateReference   
        storeName="AddressBook||AuthRoot||CertificateAuthority||Disallowed||My||Root||TrustedPeople||TrustedPublisher"  
        storeLocation="CurrentUser||LocalMachine"  
        x509FindType="FindByThumbprint||FindBySubjectName||FindBySubjectDistinguishedName||FindByIssuerName||FindByIssuerDistinguishedName||FindBySerialNumber||FindByTimeValid||FindByTimeNotYetValid||FindByTimeExpired||FindByTemplateName||FindByApplicationPolicy||FindByCertificatePolicy||FindByExtension||FindByKeyUsage||FindBySubjectKeyIdentifier"  
        findValue=xs:String  
        isChainIncluded=xs:Boolean >  
      </certificateReference>  
    </serviceCertificate>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|storeName|X.509 인증서 저장소의 이름입니다. 기본값은 "My"입니다. 선택 사항입니다.|  
|storeLocation|X.509 인증서 저장소의 위치를 지정 하는 값입니다.<xref:System.Security.Cryptography.X509Certificates.StoreLocation> 기본값은 "LocalMachine"입니다. 선택 사항입니다.|  
|x509FindType|실행할 검색 유형을 지정 하는 값입니다.<xref:System.Security.Cryptography.X509Certificates.X509FindType> 기본값은 "FindBySubjectDistinguishedName"입니다. 선택 사항입니다.|  
|findValue|X.509 인증서 저장소에서 검색할 값입니다. 선택 사항입니다.|  
|isChainIncluded|인증서 체인을 사용 하 여 유효성 검사를 수행할지 여부를 지정 합니다. 기본값은 "true"입니다. 유효성 검사는 인증서 체인을 사용 하 여 수행 됩니다. 선택 사항입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<serviceCertificate>](servicecertificate.md)|토큰을 암호화 하 고 해독 하는 데 사용 되는 인증서를 구성 합니다.|  
  
## <a name="remarks"></a>설명  
 요소 `<certificateReference>` 는 인증서 저장소에서 x.509 인증서를 찾고 유효성을 검사 하는 데 사용 되는 설정을 지정 합니다. `<serviceCertificate>` 요소를 요소의 자식 요소로 지정 하면 토큰을 암호화 하 고 해독 하는 데 사용 되는 x.509 인증서의 위치 및 확인 설정을 지정 합니다. 합니다 `<certificateReference>` 에서 요소가 표시 되는 <xref:System.ServiceModel.Configuration.CertificateReferenceElement> 클래스입니다.
