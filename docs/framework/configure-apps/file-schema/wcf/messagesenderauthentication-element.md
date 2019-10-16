---
title: <messageSenderAuthentication> 요소
ms.date: 03/30/2017
ms.assetid: 8d979dfc-a6f9-42ec-96d5-7fbc13a48118
ms.openlocfilehash: bab0e50d7feba3ea55d505be07cfa41427a5cbbc
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70397784"
---
# <a name="messagesenderauthentication-element"></a>\<h > 요소
피어 투 피어 메시지 발신자에 대한 인증 옵션을 지정합니다.  
  
 피어 투 피어 프로그래밍에 대 한 자세한 내용은 [피어 투 피어 네트워킹](../../../wcf/feature-details/peer-to-peer-networking.md)을 참조 하세요.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<endpointBehaviors >** ](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<clientCredentials >** ](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<피어 >** ](peer-of-clientcredentials-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<h >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<messageSenderAuthentication customCertificateValidatorType= "namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"
                             certificateValidationMode = "ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"
                             revocationMode="NoCheck/Online/Offline"
                             trustedStoreLocation="CurrentUser/LocalMachine" />
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`customCertificateValidatorType`|사용자 지정 형식의 유효성을 검사하는 데 사용되는 형식 및 어셈블리입니다. 이 특성은 `certificateValidationMode`가 `Custom`으로 설정되어 있을 때 설정해야 합니다.|  
|`certificateValidationMode`|자격 증명의 유효성을 검사하는 데 사용되는 세 가지 모드 중 하나를 지정합니다. `Custom`으로 설정되면 `customCertificateValidator`도 지정해야 합니다.|  
|`revocationMode`|CRL(해지된 인증서 목록)을 검사하는 데 사용되는 모드 중 하나입니다.|  
|`trustedStoreLocation`|시스템 저장소 위치 `LocalMachine` 또는 `CurrentUser` 중 하나입니다. 서비스 인증서가 클라이언트와 협상될 때 이 값이 사용됩니다. 지정 된 저장소 위치에 있는 **신뢰할 수 있는 사용자** 저장소에 대해 유효성 검사가 수행 됩니다.|  
  
## <a name="customcertificatevalidatortype-attribute"></a>customCertificateValidatorType 특성  
  
|값|Description|  
|-----------|-----------------|  
|문자열|선택 사항입니다. 형식 이름 및 어셈블리와 형식을 찾는 데 사용되는 기타 데이터를 지정합니다. 적어도 네임스페이스 및 형식 이름이 필요합니다. 선택적 정보로는 어셈블리 이름, 버전 번호, 문화권 및 공개 키 토큰이 있습니다.|  
  
## <a name="certificatevalidationmode-attribute"></a>certificateValidationMode 특성  
  
|값|Description|  
|-----------|-----------------|  
|열거형|선택 사항입니다. `None`, `PeerTrust`, `ChainTrust`, `PeerOrChainTrust`, `Custom` 값 중 하나입니다. 기본값은 `ChainTrust`입니다. 기본값은 `ChainTrust`입니다.<br /><br /> 자세한 내용은 [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md)합니다.|  
  
## <a name="revocationmode-attribute"></a>revocationMode 특성  
  
|값|Description|  
|-----------|-----------------|  
|열거형|`NoCheck`, `Online`, `Offline` 값 중 하나입니다. 기본값은 `Online`입니다.<br /><br /> 자세한 내용은 [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md)합니다.|  
  
## <a name="trustedstorelocation-attribute"></a>trustedStoreLocation 특성  
  
|값|Description|  
|-----------|-----------------|  
|열거형|`LocalMachine` 또는 `CurrentUser` 값 중 하나입니다. 기본값은 `CurrentUser`입니다. 시스템 계정으로 클라이언트 애플리케이션을 실행하는 경우 인증서는 대개 `LocalMachine`에 있습니다. 사용자 계정으로 클라이언트 애플리케이션을 실행하는 경우 인증서는 대개 `CurrentUser`에 있습니다. 기본값은 `CurrentUser`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<peer>](peer-of-clientcredentials-element.md)|피어 서비스에 대해 클라이언트를 인증하는 데 사용되는 자격 증명을 지정합니다.|  
  
## <a name="remarks"></a>설명  
 메시지 인증을 선택하면 이 요소를 구성해야 합니다. 출력 채널의 경우 각 메시지는 [ \<인증서 >](certificate-element.md)에서 제공 하는 인증서를 사용 하 여 서명 됩니다. 모든 메시지는 애플리케이션에 배달되기 전에 이 요소의 `customCertificateValidatorType` 특성에 지정된 유효성 검사기를 사용하여 메시지 자격 증명과 비교하여 검사됩니다. 유효성 검사기는 자격 증명을 수락하거나 거부할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 메시지 발신자 유효성 검사 모드를 `PeerOrChainTrust`로 설정합니다.  
  
```xml  
<behaviors>
  <endpointBehaviors>
    <behavior name="MyEndpointBehavior">
      <clientCredentials>
        <peer>
          <certificate findValue="www.contoso.com"
                       storeLocation="LocalMachine"
                       x509FindType="FindByIssuerName" />
          <messageSenderAuthentication certificateValidationMode="PeerOrChainTrust" />
          <messageSenderAuthentication certificateValidationMode="None" />
        </peer>
      </clientCredentials>
    </behavior>
  </endpointBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>
- <xref:System.ServiceModel.Security.PeerCredential.MessageSenderAuthentication%2A>
- <xref:System.ServiceModel.Configuration.PeerCredentialElement.MessageSenderAuthentication%2A>
- <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>
- [인증서 작업](../../../wcf/feature-details/working-with-certificates.md)
- [피어 투 피어 네트워킹](../../../wcf/feature-details/peer-to-peer-networking.md)
- [피어 채널 메시지 인증](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/aa967730(v=vs.90))
- [피어 채널 사용자 지정 인증](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751447(v=vs.90))
- [피어 채널 애플리케이션 보안](../../../wcf/feature-details/securing-peer-channel-applications.md)
