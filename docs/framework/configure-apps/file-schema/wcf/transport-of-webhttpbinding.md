---
title: <webHttpBinding>의 <transport>
ms.date: 03/30/2017
ms.assetid: f150fb19-7de1-44af-81f4-86cad881cd05
ms.openlocfilehash: 98cdaa86441f91552c7133d8e5694f88019a6dbf
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399276"
---
# <a name="transport-of-webhttpbinding"></a>\<webHttpBinding >의 \<전송 >
HTTP 요청을 수신하도록 구성된 서비스 엔드포인트의 전송 수준 보안 설정을 정의합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<webHttpBinding >** ](webhttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<보안 >** ](security-of-webhttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<전송 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<webHttpBinding>
  <binding>
    <security mode="None|Transport|Message|TransportWithMessageCredential|TransportCredentialOnly">
      <transport clientCredentialType="None|Basic|Digest|Ntlm|Windows"
                 proxyCredentialType="None|Basic|Digest|Ntlm|Windows"
                 realm="string">
        <extendedProtectionPolicy policyEnforcement="Never|WhenSupported|Always"
                                  protectionScenario="TransportSelected|TrustedProxy">
          <customServiceNames>
          </customServiceNames>
        </extendedProtectionPolicy>
      </transport>
    </security>
  </binding>
</webHttpBinding>
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
|`realm`|다이제스트 또는 기본 인증을 위한 인증 영역을 지정하는 문자열입니다. 기본값은 빈 문자열입니다.<br /><br /> 인증 영역은 최소한, 인증을 수행하는 호스트의 이름을 지정하며, 액세스 권한을 가진 사용자 컬렉션을 지정할 수도 있습니다. 사용자는 여러 개의 사용자 이름 및 암호 중에서 사용할 수 있는 하나를 알아내기 위해 인증 영역을 쿼리할 수 있습니다.|  
|`policyEnforcement`|이 열거형은 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy>가 적용되는 경우를 지정합니다.<br /><br /> 1.  Never - 정책이 적용되지 않습니다(확장 보호가 사용되지 않음).<br />2.  WhenSupported – 클라이언트에서 확장 보호를 지원하는 경우에만 정책이 적용됩니다.<br />3.  Always – 정책이 항상 적용됩니다. 확장 보호를 지원하지 않는 클라이언트는 인증되지 않습니다.|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 특성  
  
|값|Description|  
|-----------|-----------------|  
|`None`|보안이 해제되어 있습니다.|  
|`Basic`|기본 인증을 사용합니다.|  
|`Certificate`|X.509 인증서를 사용하여 클라이언트를 인증합니다.|  
|`Digest`|다이제스트 인증을 사용합니다.|  
|`Ntlm`|Windows 도메인에 대한 대체(fallback)로 NTLM 인증을 사용합니다.|  
|`Windows`|Windows 통합 인증을 사용합니다.|  
  
## <a name="proxycredentialtype-attribute"></a>proxyCredentialType 특성  
  
|값|Description|  
|-----------|-----------------|  
|`None`|보안이 해제되어 있습니다.|  
|`Basic`|기본 인증을 사용합니다.|  
|`Digest`|다이제스트 인증을 사용합니다.|  
|`Ntlm`|Windows 도메인에 대한 대체(fallback)로 NTLM을 사용합니다.|  
|`Windows`|Windows 통합 인증을 사용합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<security>](security-of-webhttpbinding.md)|WsHttpBinding > 요소의 보안 기능 [ \<](wshttpbinding.md) 을 나타냅니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.HttpTransportSecurity>
- <xref:System.ServiceModel.Configuration.WebHttpSecurityElement.Transport%2A>
- <xref:System.ServiceModel.WebHttpSecurity.Transport%2A>
- <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>
- [서비스 및 클라이언트에 보안 설정](../../../wcf/feature-details/securing-services-and-clients.md)
- [바인딩](../../../wcf/bindings.md)
- [시스템 제공 바인딩 구성](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
- [WCF 웹 HTTP 프로그래밍 모델](../../../wcf/feature-details/wcf-web-http-programming-model.md)
