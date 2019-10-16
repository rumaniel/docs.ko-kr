---
title: <ws2007HttpBinding>의 <transport>
ms.date: 03/30/2017
ms.assetid: 692befa3-8b0b-4ec5-b601-755874e98eb0
ms.openlocfilehash: 4ea60ccaba58bc0b3fa8f2263295bf1413d25e89
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399263"
---
# <a name="transport-of-ws2007httpbinding"></a>\<ws2007HttpBinding >의 \<전송 >
HTTP 전송의 인증 설정을 정의합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<ws2007HttpBinding >** ](ws2007httpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<보안 >** ](security-of-ws2007httpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<전송 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<transport clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"
           proxyCredentialType="Basic/Digest/None/Ntlm/Windows"
           realm="string" />
```  
  
## <a name="type"></a>형식  
 <xref:System.ServiceModel.HttpTransportSecurity>  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`clientCredentialType`|클라이언트를 서비스에 인증할 때 사용되는 자격 증명을 지정합니다. 이 특성은 <xref:System.ServiceModel.HttpClientCredentialType> 형식입니다.|  
|`proxyCredentialType`|클라이언트를 도메인 프록시에 인증할 때 사용되는 자격 증명을 지정합니다. 이 특성은 <xref:System.ServiceModel.HttpProxyCredentialType> 형식입니다.|  
|`realm`|다이제스트 또는 기본 인증을 위한 인증 영역입니다. 기본값은 빈 문자열입니다.<br /><br /> 인증 영역은 최소한, 인증을 수행하는 호스트의 이름을 지정하며, 액세스 권한을 가진 사용자 컬렉션을 지정할 수도 있습니다. 사용자는 여러 개의 사용자 이름 및 암호 중에서 사용할 수 있는 하나를 알아내기 위해 인증 영역을 쿼리할 수 있습니다.|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 특성  
  
|값|설명|  
|-----------|-----------------|  
|없음|보안이 해제되어 있습니다.|  
|Basic|기본 인증을 사용합니다.|  
|Digest|다이제스트 인증을 사용합니다.|  
|Ntlm|Windows 도메인에 대한 대체(fallback)로 NTLM 인증을 사용합니다.|  
|Windows|Windows 통합 인증을 사용합니다.|  
|Certificate|X.509 인증서를 사용하여 클라이언트를 인증합니다.|  
  
## <a name="proxycredentialtype-attribute"></a>proxyCredentialType 특성  
  
|값|설명|  
|-----------|-----------------|  
|없음|보안이 해제되어 있습니다.|  
|Basic|기본 인증을 사용합니다.|  
|Digest|다이제스트 인증을 사용합니다.|  
|Ntlm|Windows 도메인에 대한 대체(fallback)로 NTLM을 사용합니다.|  
|Windows|Windows 통합 인증을 사용합니다.|  
|Certificate|X.509 인증서를 사용하여 클라이언트를 인증합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<security>](security-of-ws2007httpbinding.md)|Ws2007HttpBinding > 요소의 보안 기능 [ \<](ws2007httpbinding.md) 을 나타냅니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.HttpTransportSecurity>
- <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement.Transport%2A>
- <xref:System.ServiceModel.WSHttpSecurity.Transport%2A>
- <xref:System.ServiceModel.Configuration.WSHttpTransportSecurityElement>
- [서비스 및 클라이언트에 보안 설정](../../../wcf/feature-details/securing-services-and-clients.md)
- [바인딩](../../../wcf/bindings.md)
- [시스템 제공 바인딩 구성](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
