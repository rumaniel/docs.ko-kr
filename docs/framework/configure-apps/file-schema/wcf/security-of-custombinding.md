---
title: <customBinding>의 <security>
ms.date: 03/30/2017
ms.assetid: 243a5148-bbd1-447f-a8a5-6e7792c0a3f1
ms.openlocfilehash: 165d1f2b9b770fd7c3f05143c1d85955c6008463
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399871"
---
# <a name="security-of-custombinding"></a>\<customBinding >의 \<보안 >
사용자 지정 바인딩에 대한 보안 옵션을 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<보안 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<security allowSerializedSigningTokenOnReply="Boolean"
          authenticationMode="AuthenticationMode"
          defaultAlgorithmSuite="SecurityAlgorithmSuite"
          includeTimestamp="Boolean"
          requireDerivedKeys="Boolean"
          keyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"
          messageProtectionOrder="SignBeforeEncrypt/SignBeforeEncryptAndEncryptSignature/EncryptBeforeSign"
          messageSecurityVersion="WSSecurityJan2004/WSSecurityXXX2005"
          requireDerivedKeys="Boolean"
          requireSecurityContextCancellation="Boolean"
          requireSignatureConfirmation="Boolean"
          securityHeaderLayout="Strict/Lax/LaxTimestampFirst/LaxTimestampLast">
   <issuedTokenParameters />
   <localClientSettings />
   <localServiceSettings />
   <secureConversationBootstrap />
</security>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|allowSerializedSigningTokenOnReply|선택 사항입니다. serialize(직렬화)된 토큰을 회신에 사용할 수 있는지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다. 이중 바인딩을 사용하는 경우 설정은 기본적으로 `true`로 지정되며 변경된 설정이 모두 무시됩니다.|  
|authenticationMode|선택 사항입니다. 게시자와 응답자 간에 인증 모드가 사용되도록 지정합니다. 아래의 모든 값을 참조하세요.<br /><br /> 기본값은 `sspiNegotiated`입니다.|  
|defaultAlgorithmSuite|선택 사항입니다. 메시지 암호화 및 키 래핑 알고리즘을 설정합니다. 알고리즘과 키 크기는 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 클래스로 결정됩니다. 이러한 알고리즘은 보안 정책 언어(WS-SecurityPolicy) 사양에 지정된 알고리즘에 매핑됩니다.<br /><br /> 가능한 값이 아래에 나와 있습니다. 기본값은 `Basic256`입니다.<br /><br /> 이 특성은 기본값과 다른 알고리즘 집합에 적합한 다른 플랫폼에서 작업할 때 사용됩니다. 이 설정을 수정하는 경우 관련 알고리즘의 장점과 단점을 파악해야 합니다. 이 특성은 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 형식입니다.|  
|includeTimestamp|각 메시지에 타임스탬프가 포함되는지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.|  
|keyEntropyMode|메시지 보안 설정을 위한 키의 계산 방식을 지정합니다. 키는 클라이언트 키 자료만을 기반으로 하거나 서비스 키 자료만을 기반으로 하거나 두 가지의 조합을 기반으로 할 수 있습니다. 유효한 값은 다음과 같습니다.<br /><br /> -   `ClientEntropy`: 세션 키는 클라이언트에서 제공 하는 키 데이터를 기반으로 합니다.<br />-   `ServerEntropy`: 세션 키는 서버에서 제공 하는 키 데이터를 기반으로 합니다.<br />-   `CombinedEntropy`: 세션 키는 클라이언트 및 서비스에서 제공 하는 키 데이터를 기반으로 합니다.<br /><br /> 기본값은 `CombinedEntropy`입니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.Security.SecurityKeyEntropyMode> 형식입니다.|  
|MessageProtectionOrder|메시지 수준 보안 알고리즘이 메시지에 적용되는 순서를 설정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -   `SignBeforeEncrypt`: 먼저 서명 하 고 암호화 합니다.<br />-   `SignBeforeEncryptAndEncryptSignature`: 먼저 서명 하 고 암호화 한 다음 서명을 암호화 합니다.<br />-   `EncryptBeforeSign`: 먼저 암호화 한 다음 서명 합니다.<br /><br /> 기본값은 사용되는 WS-Security 버전에 따라 달라집니다. WS-Security 1.1을 사용하는 경우 기본값은 `SignBeforeEncryptAndEncryptSignature`입니다. WS-Security 1.0을 사용하는 경우 기본값은 `SignBeforeEncrypt`입니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.Security.MessageProtectionOrder> 형식입니다.|  
|messageSecurityVersion|선택 사항입니다. 사용되는 WS-Security 버전을 설정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -   WSSecurity11WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11<br />-   WSSecurity10WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10<br />-   WSSecurity11WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10<br /><br /> 기본값은 WSSecurity11WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11이며 간단하게 `Default`와 같이 XML로 나타낼 수 있습니다. 이 특성은 <xref:System.ServiceModel.MessageSecurityVersion> 형식입니다.|  
|requireDerivedKeys|키를 원본 증명 키에서 파생할 수 있는지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.|  
|requireSecurityContextCancellation|선택 사항입니다. 더 이상 필요하지 않은 보안 컨텍스트를 취소 및 종료할지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.|  
|requireSignatureConfirmation|선택 사항입니다. WS-Security 시그니처 확인을 사용할 수 있는지 여부를 지정하는 부울 값입니다. `true`로 설정되면 응답자는 메시지 시그니처를 확인합니다.  사용자 지정 바인딩이 상호 인증서에 대해 구성되었거나 발급된 토큰(WSS 1.1 바인딩)을 사용하도록 구성된 경우 이 특성은 기본적으로 `true`로 설정됩니다. 그렇지 않으면 기본값은 `false`입니다.<br /><br /> 서비스가 요청을 완전히 인식하고 응답하는지 확인하기 위해 시그니처 확인이 사용됩니다.|  
|securityHeaderLayout|선택 사항입니다. 보안 헤더의 요소 순서를 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -   `Strict`: 일반적인 “사용 전 선언” 원칙에 따라 항목이 보안 헤더에 추가됩니다.<br />-   `Lax`: WSS: SOAP 메시지 보안을 확인하는 순서로 항목이 보안 헤더에 추가됩니다. 추가됩니다.<br />-   `LaxWithTimestampFirst`: WSS: SOAP 메시지 보안을 확인하는 순서로 항목이 보안 헤더에 추가됩니다. 단, 보안 헤더의 첫 번째 요소는 wsse:Timestamp 요소여야 합니다.<br />-   `LaxWithTimestampLast`: WSS: SOAP 메시지 보안을 확인하는 순서로 항목이 보안 헤더에 추가됩니다. 단, 보안 헤더의 마지막 요소는 wsse:Timestamp 요소여야 합니다.<br /><br /> 기본값은 `Strict`입니다.<br /><br /> 이 요소는 <xref:System.ServiceModel.Channels.SecurityHeaderLayout> 형식입니다.|  
  
## <a name="authenticationmode-attribute"></a>authenticationMode 특성  
  
|값|설명|  
|-----------|-----------------|  
|String|`AnonymousForCertificate`<br /><br /> `AnonymousForSslNegotiated`<br /><br /> `CertificateOverTransport`<br /><br /> `IssuedToken`<br /><br /> `IssuedTokenForCertificate`<br /><br /> `IssuedTokenForSslNegotiated`<br /><br /> `IssuedTokenOverTransport`<br /><br /> `Kerberos`<br /><br /> `KerberosOverTransport`<br /><br /> `MutualCertificate`<br /><br /> `MutualCertificateDuplex`<br /><br /> `MutualSslNegotiated`<br /><br /> `SecureConversation`<br /><br /> `SspiNegotiated`<br /><br /> `UserNameForCertificate`<br /><br /> `UserNameForSslNegotiated`<br /><br /> `UserNameOverTransport`<br /><br /> `SspiNegotiatedOverTransport`|  
  
## <a name="defaultalgorithm-attribute"></a>defaultAlgorithm 특성  
  
|값|설명|  
|-----------|-----------------|  
|Basic128|Aes128 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic192|Aes192 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic256|Aes256 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic256Rsa15|메시지 암호화의 경우 Aes256, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa15를 사용합니다.|  
|Basic192Rsa15|메시지 암호화의 경우 Aes192, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa15를 사용합니다.|  
|TripleDes|TripleDes 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic128Rsa15|메시지 암호화의 경우 Aes128, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa15를 사용합니다.|  
|TripleDesRsa15|TripleDes 암호화, 메시지 다이제스트의 경우 Sha1, 키 래핑의 경우 Rsa15를 사용합니다.|  
|Basic128Sha256|메시지 암호화의 경우 Aes256, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic192Sha256|메시지 암호화의 경우 Aes192, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic256Sha256|메시지 암호화의 경우 Aes256, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|TripleDesSha256|메시지 암호화의 경우 TripleDes, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa-oaep-mgf1p를 사용합니다.|  
|Basic128Sha256Rsa15|메시지 암호화의 경우 Aes128, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa15를 사용합니다.|  
|Basic192Sha256Rsa15|메시지 암호화의 경우 Aes192, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa15를 사용합니다.|  
|Basic256Sha256Rsa15|메시지 암호화의 경우 Aes256, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa15를 사용합니다.|  
|TripleDesSha256Rsa15|메시지 암호화의 경우 TripleDes, 메시지 다이제스트의 경우 Sha256, 키 래핑의 경우 Rsa15를 사용합니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<issuedTokenParameters>](issuedtokenparameters.md)|현재 발급된 토큰을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement> 형식입니다.|  
|[\<localClientSettings>](localclientsettings-element.md)|이 바인딩에 대한 로컬 클라이언트의 보안 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.LocalClientSecuritySettingsElement> 형식입니다.|  
|[\<localServiceSettings>](localservicesettings-element.md)|이 바인딩에 대한 로컬 서비스의 보안 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.LocalServiceSecuritySettingsElement> 형식입니다.|  
|[\<secureConversationBootstrap>](secureconversationbootstrap.md)|보안 대화 서비스 개시에 사용되는 기본값을 지정합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|사용자 지정 바인딩의 모든 바인딩 기능을 정의합니다.|  
  
## <a name="remarks"></a>설명  
 이 요소를 사용 하는 방법에 대 한 자세한 내용은 [SecurityBindingElement 인증 모드](../../../wcf/feature-details/securitybindingelement-authentication-modes.md) 및 [방법: SecurityBindingElement](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)를 사용 하 여 사용자 지정 바인딩을 만듭니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 사용자 지정 바인딩을 사용하여 보안을 구성하는 방법을 보여 줍니다. 여기서는 사용자 지정 바인딩을 사용하여 메시지를 안전하게 전송하고 메시지 수준 보안을 가능하게 하는 방법을 보여 줍니다. 이러한 방법은 클라이언트와 서비스 간에 메시지를 전송하는 데 보안 전송이 요구되면서 동시에 메시지가 메시지 수준에서 보호되어야 하는 경우에 유용합니다. 이 구성은 시스템 제공 바인딩에서는 지원되지 않습니다.  
  
 서비스 구성은 TLS/SSL 프로토콜을 사용하여 보호되는 TCP 통신 및 Windows 메시지 보안을 지원하는 사용자 지정 바인딩을 정의합니다. 사용자 지정 바인딩은 서비스 인증서를 사용하여 전송 수준에서 서비스를 인증하고 클라이언트와 서비스 간 전송 시 메시지를 보호합니다. 이는 [ \<sslstreamsecurity >](sslstreamsecurity.md) binding 요소에 의해 수행 됩니다. 서비스 인증서는 서비스 동작을 사용하여 구성됩니다.  
  
 또한 사용자 지정 바인딩은 기본 자격 증명 형식인 Windows 자격 증명 형식의 메시지 보안을 사용합니다. 이는 [보안](security-of-custombinding.md) 바인딩 요소에 의해 수행 됩니다. Kerberos 인증 메커니즘이 사용 가능한 경우 클라이언트 및 서비스는 모두 메시지 수준 보안을 사용하여 인증됩니다. Kerberos 인증 메커니즘을 사용할 수 없는 경우에는 NTLM 인증이 사용됩니다. NTLM은 서비스에 대해 클라이언트를 인증하지만 클라이언트에 대해 서비스를 인증하지는 않습니다. [보안](security-of-custombinding.md) 바인딩 요소는 authenticationType을 사용 `SecureConversation` 하도록 구성 되며이로 인해 클라이언트와 서비스 모두에 보안 세션이 생성 됩니다. 이러한 구성은 서비스의 이중 계약을 사용할 때 필요합니다. 이 예제를 실행 하는 방법에 대 한 자세한 내용은 [사용자 지정 바인딩 보안](../../../wcf/samples/custom-binding-security.md)을 참조 하세요.  
  
```xml  
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">
        <host>
          <baseAddresses>
            <!-- use following base address -->
            <add baseAddress="net.tcp://localhost:8000/ServiceModelSamples/Service"/>
          </baseAddresses>
        </host>
        <endpoint address=""
                  binding="customBinding"
                  bindingConfiguration="Binding1"
                  contract="Microsoft.ServiceModel.Samples.ICalculatorDuplex" />
        <!-- the mex endpoint is exposed at net.tcp://localhost:8000/ServiceModelSamples/service/mex -->
        <endpoint address="mex"
                  binding="mexTcpBinding"
                  contract="IMetadataExchange" />
      </service>
    </services>
    <bindings>
      <!-- configure a custom binding -->
      <customBinding>
        <binding name="Binding1">
          <security authenticationMode="SecureConversation"
                    requireSecurityContextCancellation="true">
          </security>
          <textMessageEncoding messageVersion="Soap12WSAddressing10"
                               writeEncoding="utf-8" />
          <sslStreamSecurity requireClientCertificate="false" />
          <tcpTransport />
        </binding>
      </customBinding>
    </bindings>
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceMetadata />
          <serviceDebug includeExceptionDetailInFaults="False" />
          <serviceCredentials>
            <serviceCertificate findValue="localhost"
                                storeLocation="LocalMachine"
                                storeName="My"
                                x509FindType="FindBySubjectName" />
          </serviceCredentials>
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
</configuration>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.SecurityElement>
- <xref:System.ServiceModel.Channels.SecurityBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [바인딩](../../../wcf/bindings.md)
- [바인딩 확장](../../../wcf/extending/extending-bindings.md)
- [사용자 지정 바인딩](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [방법: SecurityBindingElement를 사용 하 여 사용자 지정 바인딩 만들기](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [사용자 지정 바인딩 보안](../../../wcf/samples/custom-binding-security.md)
