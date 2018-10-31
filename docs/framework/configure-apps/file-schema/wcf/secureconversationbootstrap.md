---
title: '&lt;secureConversationBootstrap&gt;'
ms.date: 03/30/2017
ms.assetid: 66b46f95-fa2d-4b5b-b6ce-0572ab0cdd50
ms.openlocfilehash: a1b739ac8af87340a693d88bac0a379f0c3a447a
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197771"
---
# <a name="ltsecureconversationbootstrapgt"></a>&lt;secureConversationBootstrap&gt;
보안 대화 서비스 개시에 사용되는 기본값을 지정합니다.  
  
 \<system.serviceModel>  
\<바인딩 >  
\<customBinding>  
\<바인딩 >  
\<security>  
\<secureConversationBootstrap >  
  
## <a name="syntax"></a>구문  
  
```xml  
<secureConversationBootstrap  
   allowSerializedSigningTokenOnReply="Boolean"  
   authenticationMode="AuthenticationMode"  
   defaultAlgorithmSuite="SecurityAlgorithmSuite"  
   includeTimestamp="Boolean"  
   requireDerivedKeys="Boolean"  
   keyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"   
messageProtectionOrder="SignBeforeEncrypt/SignBeforeEncryptAndEncryptSignature/EncryptBeforeSign"  
   messageSecurityVersion="WSSecurityJan2004/WSSecurityXXX2005"  
   requireDerivedKeys="Boolean"  
   requireSecurityContextCancellation="Boolean"  
   requireSignatureConfirmation="Boolean" >  
   securityHeaderLayout="Strict/Lax/LaxTimestampFirst/LaxTimestampLast"  
   includeTimestamp="Boolean" />  
```  
  
## <a name="type"></a>형식  
 `Type`  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`allowSerializedSigningTokenOnReply`|선택 사항입니다. serialize(직렬화)된 토큰을 회신에 사용할 수 있는지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다. 이중 바인딩을 사용하는 경우 설정은 기본적으로 `true`로 지정되며 변경된 설정이 모두 무시됩니다.|  
|`authenticationMode`|게시자와 응답자 간에 SOAP 인증 모드가 사용되도록 지정합니다.<br /><br /> 기본값은 sspiNegotiated입니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.Configuration.AuthenticationMode> 형식입니다.|  
|`defaultAlgorithmSuite`|보안 알고리즘 모음은 정형화, 다이제스트, 키 래핑, 시그니처, 암호화 및 키 파생 알고리즘과 같은 다양한 알고리즘을 정의합니다. 각 보안 알고리즘 모음은 이러한 다양한 매개 변수의 값을 정의합니다. 이러한 알고리즘을 통해 메시지 기반 보안이 구현됩니다.<br /><br /> 이 특성은 기본값과 다른 알고리즘 집합에 적합한 다른 플랫폼에서 작업할 때 사용됩니다. 이 설정을 수정하는 경우 관련 알고리즘의 장점과 단점을 파악해야 합니다. 이 특성은 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 형식입니다. 기본값은 `Basic256`입니다.|  
|`includeTimestamp`|각 메시지에 타임스탬프가 포함되는지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.|  
|`keyEntropyMode`|메시지 보안 설정을 위한 키의 계산 방식을 지정합니다. 키는 클라이언트 키 자료만을 기반으로 하거나 서비스 키 자료만을 기반으로 하거나 두 가지의 조합을 기반으로 할 수 있습니다. 올바른 값은 다음과 같습니다.<br /><br /> -ClientEntropy: 세션 키를 기반으로 클라이언트 키 자료를 제공 합니다.<br />-ServerEntropy: 세션 키를 기반으로 서비스 키 자료를 제공 합니다.<br />-CombinedEntropy: 세션 키를 기반으로 클라이언트 및 서비스 키 자료를 제공 합니다.<br /><br /> 기본값은 CombinedEntropy입니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.Security.SecurityKeyEntropyMode> 형식입니다.|  
|`messageProtectionOrder`|메시지 수준 보안 알고리즘이 메시지에 적용되는 순서를 설정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -SignBeforeEncrypt: 먼저, 로그인 한 다음 암호화 합니다.<br />-SignBeforeEncryptAndEncryptSignature: 서명, 암호화 하 고 서명을 암호화 합니다.<br />-EncryptBeforeSign: 먼저 암호화 한 다음 로그인 합니다.<br /><br /> WS-Security 1.1과 함께 상호 인증서를 사용하는 경우 기본값은 SignBeforeEncryptAndEncryptSignature입니다.  WS-Security 1.0을 사용하는 경우 기본값은 SignBeforeEncrypt입니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.Security.MessageProtectionOrder> 형식입니다.|  
|`messageSecurityVersion`|사용되는 WS-Security 버전을 설정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -WSSecurityJan2004<br />-WSSecurityXXX2005<br /><br /> 기본값은 WSSecurityXXX2005입니다. 이 특성은 <xref:System.ServiceModel.MessageSecurityVersion> 형식입니다.|  
|`requireDerivedKeys`|키를 원본 증명 키에서 파생할 수 있는지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.|  
|`requireSecurityContextCancellation`|더 이상 필요하지 않은 보안 컨텍스트를 취소 및 종료할지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.|  
|`requireSignatureConfirmation`|WS-Security 시그니처 확인을 사용할 수 있는지 여부를 지정하는 부울 값입니다. `true`로 설정되면 응답자는 메시지 시그니처를 확인합니다. 기본값은 `false`입니다.<br /><br /> 서비스가 요청을 완전히 인식하고 응답하는지 확인하기 위해 시그니처 확인이 사용됩니다.|  
|`securityHeaderLayout`|보안 헤더의 요소 순서를 지정합니다. 올바른 값은 다음과 같습니다.<br /><br /> -Strict. 일반적인 “사용 전 선언” 원칙에 따라 항목이 보안 헤더에 추가됩니다.<br />-명확 하지 않습니다. WSS: SOAP 메시지 보안을 확인하는 순서로 항목이 보안 헤더에 추가됩니다.<br />-LaxWithTimestampFirst 합니다. WSS: SOAP 메시지 보안을 확인하는 순서로 항목이 보안 헤더에 추가되며 보안 헤더의 첫 번째 요소는 wsse:Timestamp 요소여야 합니다.<br />-LaxWithTimestampLast 합니다. WSS: SOAP 메시지 보안을 확인하는 순서로 항목이 보안 헤더에 추가되며 보안 헤더의 마지막 요소는 wsse:Timestamp 요소여야 합니다.<br /><br /> 기본값은 Strict입니다.<br /><br /> 이 요소는 <xref:System.ServiceModel.Channels.SecurityHeaderLayout> 형식입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<issuedTokenParameters>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenparameters.md)|현재 발급된 토큰을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement> 형식입니다.|  
|[\<localClientSettings >](../../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md)|이 바인딩에 대한 로컬 클라이언트의 보안 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.LocalClientSecuritySettingsElement> 형식입니다.|  
|[\<localServiceSettings >](../../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md)|이 바인딩에 대한 로컬 서비스의 보안 설정을 지정합니다. 이 요소는 <xref:System.ServiceModel.Configuration.LocalServiceSecuritySettingsElement> 형식입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<security>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)|사용자 지정 바인딩에 대한 보안 옵션을 지정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Configuration.LocalServiceSecuritySettingsElement>  
 <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSettings%2A>  
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>  
 <xref:System.ServiceModel.Channels.CustomBinding>  
 [바인딩](../../../../../docs/framework/wcf/bindings.md)  
 [바인딩 확장](../../../../../docs/framework/wcf/extending/extending-bindings.md)  
 [사용자 지정 바인딩](../../../../../docs/framework/wcf/extending/custom-bindings.md)  
 [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)  
 [방법: SecurityBindingElement를 사용하여 사용자 지정 바인딩 만들기](../../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 [사용자 지정 바인딩 보안](../../../../../docs/framework/wcf/samples/custom-binding-security.md)
