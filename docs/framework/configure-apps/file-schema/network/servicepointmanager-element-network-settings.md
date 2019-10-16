---
title: <servicePointManager> 요소(네트워크 설정)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#servicePointManager
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/servicePointManager
helpviewer_keywords:
- servicePointManager element
- <servicePointManager> element
ms.assetid: 6e5def51-3646-4ef6-a7bd-c69151321bec
ms.openlocfilehash: 95ad1880cbb832a17311e7e63e9203f53257f65f
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697710"
---
# <a name="servicepointmanager-element-network-settings"></a>\<servicePointManager > 요소 (네트워크 설정)
네트워크 리소스에 대 한 연결을 구성 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4c.net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<settings >** ](settings-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 **\<servicePointManager >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<servicePointManager  
  checkCertificateName="true|false"  
  checkCertificateRevocationList="true|false"  
  encryptionPolicy="AllowNoEncryption|NoEncryption|RequireEncryption"  
  expect100Continue="true|false"  
  useNagleAlgorithm="true|false"  
  enableDnsRoundRobin="true|false"  
  dnsRefreshTimeout="time"  
/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|**특성**|**설명**|  
|-------------------|---------------------|  
|`checkCertificateName`|인증서를 사용 하기 전에 시스템에서 인증서의 이름이 서버 호스트 이름과 일치 하는지 확인 해야 하는지 여부를 지정 합니다. 기본값은 `true`입니다.|  
|`checkCertificateRevocationList`|인증서를 사용 하기 전에 시스템에서 인증서가 해지 되었는지 여부를 확인 해야 하는지 여부를 지정 합니다. 기본값은 `false`입니다.|  
|`dnsRefreshTimeout`|Dns 라운드 로빈 옵션과 함께 DNS (Domain Name Service) 확인이 캐시 되는 시간 (밀리초)을 지정 합니다. 기본값은 120,000밀리초(2분)입니다.|  
|`enableDnsRoundRobin`|IP (인터넷 프로토콜) 주소가 여러 개인 호스트 이름에 대 한 DNS 확인이 모든 주소를 반환할지 아니면 첫 번째 주소를 반환할지를 지정 합니다. 기본값은 `false`입니다.|  
|`encryptionPolicy`|@No__t-0 인스턴스의 SSL/TLS 세션에 적용 되는 암호화 정책을 지정 합니다. 가능한 값은 <xref:System.Net.Security.EncryptionPolicy> 열거형의 값과 같습니다. 암호화 정책이 `NoEncryption`로 설정 된 경우에는 <xref:System.Security.Authentication.CipherAlgorithmType.Null>을 사용 해야 합니다. 기본값은 `RequireEncryption`입니다.|  
|`expect100Continue`|POST 메서드가 서버에서 `100-continue` 응답을 받을 것으로 간주 하는지 여부를 지정 합니다. 기본값은 `true`입니다.|  
|`useNagleAlgorithm`|서비스 지점 관리자에서 제어 하는 연결에 Nagle 알고리즘을 사용할지 여부를 지정 합니다. 기본값은 `true`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|**요소**|**설명**|  
|-----------------|---------------------|  
|[설정](settings-element-network-settings.md)|<xref:System.Net> 네임스페이스에 대한 기본 네트워크 옵션을 구성합니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="configuration-files"></a>구성 파일  
 이 요소는 애플리케이션 구성 파일 또는 컴퓨터 구성 파일(Machine.config)에서 사용할 수 있습니다.  
  
## <a name="see-also"></a>참조

- <xref:System.Net.ServicePointManager>
- <xref:System.Net.Security.EncryptionPolicy>
- [네트워크 설정 스키마](index.md)
