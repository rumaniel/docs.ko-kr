---
title: 권한 높이기
ms.date: 03/30/2017
helpviewer_keywords:
- elevation of privilege [WCF]
- security [WCF], elevation of privilege
ms.assetid: 146e1c66-2a76-4ed3-98a5-fd77851a06d9
ms.openlocfilehash: eae3c2a72e686774ee510dfc3ec9db04df7db630
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966178"
---
# <a name="elevation-of-privilege"></a>권한 높이기
*권한 상승을* 통해 처음에 부여 된 권한 이상의 권한을 공격자에 게 제공 합니다. 예를 들어 "읽기 전용" 권한의 권한 집합을 갖는 공격자는 권한 집합이 "읽기 및 쓰기"를 포함하도록 권한을 상승시킵니다.  
  
## <a name="trusted-sts-should-sign-saml-token-claims"></a>신뢰할 수 있는 STS가 SAML 토큰 클레임에 서명해야 함  
 SAML(Security Assertions Markup Language) 토큰은 발급된 토큰의 기본 형식인 제네릭 XML 토큰입니다. SAML 토큰은 최종 웹 서비스가 일반 교환에서 신뢰하는 STS(보안 토큰 서비스)에 의해 생성될 수 있습니다. SAML 토큰에는 문에 클레임이 있습니다. 공격자는 유효한 토큰에서 클레임을 복사하여 새 SAML 토큰을 만들고 이 토큰에 다른 발급자로 서명할 수 있습니다. 그 목적은 서버가 발급자의 유효성을 검사하는지 확인하고, 검사하지 않을 경우 그러한 취약점을 이용하여 신뢰할 수 있는 STS에서 의도한 수준 이상의 권한을 허용하는 SAML 토큰을 생성하기 위한 것입니다.  
  
 <xref:System.IdentityModel.Tokens.SamlAssertion> 클래스는 SAML 토큰 내에 포함된 디지털 서명을 확인하므로 기본 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>를 사용하려면 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> 클래스의 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>가 <xref:System.ServiceModel.Security.X509CertificateValidationMode.ChainTrust>로 설정된 경우 유효한 X.509 인증서에서 서명한 SAML 토큰이 있어야 합니다. SAML 토큰 발급자를 신뢰할 것인지 여부를 판단하는 데 `ChainTrust` 모드만으로는 부족합니다. 보다 세부적인 신뢰 모델이 필요한 서비스에서 인증 및 적용 정책을 사용하여 발급된 토큰 인증에서 생성된 클레임 집합 발급자를 확인하거나 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>에 대한 X.509 유효성 검사 설정을 사용하여 허용된 서명 인증서 집합을 제한할 수 있습니다. 자세한 내용은 Id 모델 및 [페더레이션 및 발급 된 토큰](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md) [을 사용 하 여 클레임 및 권한 부여 관리](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md) 를 참조 하세요.  
  
## <a name="switching-identity-without-a-security-context"></a>보안 컨텍스트 없이 ID 전환  
 다음은 WinFX에만 적용 됩니다.  
  
 클라이언트와 서버 간에 연결이 설정 되 면 다음 조건에 모두 해당 하는 경우를 제외 하 고 클라이언트의 id는 변경 되지 않습니다. 단, WCF 클라이언트를 연 후에는  
  
- 보안 컨텍스트를 설정 하는 절차 (전송 보안 세션 또는 메시지 보안 세션을 사용 하 여)가 꺼져<xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> 있습니다 (메시지 보안 `false` 또는 전송에서 보안을 설정할 수 없는 경우 속성이로 설정 됨). 세션은 전송 보안 사례에서 사용 됩니다. HTTPS는 그러한 전송의 한 예제입니다.  
  
- Windows 인증을 사용합니다.  
  
- 자격 증명을 명시적으로 설정하지 않습니다.  
  
- 가장된 보안 컨텍스트에서 서비스를 호출합니다.  
  
 이러한 조건이 충족 되는 경우 WCF 클라이언트를 연 후 서비스에 대 한 클라이언트를 인증 하는 데 사용 되는 id가 변경 될 수 있습니다 (대신 가장 된 id가 아니라 프로세스 id가 될 수 있음). 이러한 동작은 클라이언트를 서비스에 인증하는 데 사용된 Windows 자격 증명이 모든 메시지와 함께 전송되고 인증에 사용된 자격 증명을 현재 스레드의 Windows ID에서 가져오기 때문에 발생합니다. 현재 스레드의 Windows ID가 변경되면(예: 다른 호출자 가장으로 인해 변경됨) 메시지에 첨부되고 클라이언트를 서비스로 인증하는 데 사용된 자격 증명도 변경될 수 있습니다.  
  
 가장과 함께 Windows 인증을 사용할 때 동작이 명확하도록 하려면 Windows 자격 증명을 명시적으로 설정하거나 서비스로 보안 컨텍스트를 설정해야 합니다. 이 작업을 수행하려면 메시지 보안 세션 또는 전송 보안 세션을 사용합니다. 예를 들어 net.tcp 전송은 전송 보안 세션을 제공할 수 있습니다. 또한 서비스를 호출할 때 클라이언트 작업의 비동기 버전만 사용해야 합니다. 메시지 보안 컨텍스트를 설정하는 경우 ID가 세션 갱신 프로세스 중에 변경될 수도 있으므로 구성된 세션 갱신 기간 이상으로 서비스에 대한 연결을 유지하면 안 됩니다.  
  
### <a name="credentials-capture"></a>자격 증명 캡처  
 다음 내용은 [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] 및 이후 버전에 적용됩니다.  
  
 클라이언트 또는 서비스에 사용되는 자격 증명은 현재 컨텍스트 스레드를 기반으로 합니다. 자격 증명은 클라이언트 또는 서비스의 `Open` 메서드(비동기 호출의 경우에는 `BeginOpen`)가 호출될 때 가져옵니다. <xref:System.ServiceModel.ServiceHost> 및 <xref:System.ServiceModel.ClientBase%601> 클래스의 경우 `Open` 및 `BeginOpen` 메서드는 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 클래스의 <xref:System.ServiceModel.Channels.CommunicationObject.BeginOpen%2A> 및 <xref:System.ServiceModel.Channels.CommunicationObject> 메서드에서 상속됩니다.  
  
> [!NOTE]
> `BeginOpen` 메서드를 사용할 때 캡처한 자격 증명은 메서드를 호출하는 프로세스의 자격 증명이 아닐 수도 있습니다.  
  
## <a name="token-caches-allow-replay-using-obsolete-data"></a>토큰 캐시를 통해 사용되지 않는 데이터를 사용하여 재생  
 WCF는 LSA (로컬 보안 기관) `LogonUser` 함수를 사용 하 여 사용자 이름 및 암호를 통해 사용자를 인증 합니다. Logon 함수는 비용이 많이 드는 작업 이므로 WCF를 사용 하면 인증 된 사용자를 나타내는 토큰을 캐시 하 여 성능을 향상 시킬 수 있습니다. 캐싱 메커니즘은 다음 사용자를 위해 `LogonUser`의 결과를 저장합니다. 이 메커니즘은 기본적으로 사용 되지 않습니다. 이 <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.CacheLogonTokens%2A> 기능을 사용 하려면 속성을로 `true`설정 하거나 [ \<userNameAuthentication >](../../../../docs/framework/configure-apps/file-schema/wcf/usernameauthentication.md)의 `cacheLogonTokens` 특성을 사용 합니다.  
  
 <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.CachedLogonTokenLifetime%2A> 속성을 <xref:System.TimeSpan>으로 설정하여 캐시된 토큰에 대한 TTL(Time to Live)을 설정하거나 `cachedLogonTokenLifetime` 요소의 `userNameAuthentication` 특성을 사용할 수 있습니다. 기본값은 15분입니다. 토큰이 캐시되면 사용자 계정이 Windows에서 삭제되거나 해당 암호가 변경되어도 동일한 사용자 이름과 암호를 나타내는 모든 클라이언트가 이 토큰을 사용할 수 있습니다. TTL이 만료 되 고 토큰이 캐시에서 제거 될 때까지 WCF는 악의적인 사용자가 인증할 수 있도록 허용 합니다.  
  
 이를 완화 하려면: 사용자가 필요로 하는 최단 시간 `cachedLogonTokenLifetime` 범위로 값을 설정 하 여 공격 기간을 줄입니다.  
  
## <a name="issued-token-authorization-expiration-reset-to-large-value"></a>발급 된 토큰 권한 부여: 대량 값으로 만료 다시 설정  
 경우에 따라 <xref:System.IdentityModel.Policy.AuthorizationContext.ExpirationTime%2A>의 <xref:System.IdentityModel.Policy.AuthorizationContext> 속성이 예상치 못한 큰 값(<xref:System.DateTime.MaxValue> 필드 값에서 1일을 뺀 값 또는 9999년 12월 20일)으로 설정되는 경우가 있습니다.  
  
 이러한 설정은 <xref:System.ServiceModel.WSFederationHttpBinding> 및 클라이언트 자격 증명 형식으로 발급된 토큰이 있는 시스템 제공 바인딩을 사용할 때 발생합니다.  
  
 또한 다음 메서드 중 하나를 사용하여 사용자 지정 바인딩을 만들 때 발생합니다.  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenBindingElement%2A>  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement%2A>  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForSslBindingElement%2A>  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenOverTransportBindingElement%2A>  
  
 이러한 문제가 발생할 가능성을 줄이려면 권한 부여 정책이 각 권한 부여 정책의 작업 및 만료 시간을 확인해야 합니다.  
  
## <a name="the-service-uses-a-different-certificate-than-the-client-intended"></a>서비스에서 클라이언트가 의도한 것과 다른 인증서 사용  
 경우에 따라 클라이언트가 X.509 인증서를 사용하여 메시지에 디지털 서명을 하고 서비스에서 의도한 인증서와 다른 인증서를 검색하도록 할 수 있습니다.  
  
 이러한 상황은 다음과 같은 경우에 발생할 수 있습니다.  
  
- 클라이언트가 X.509 인증서를 사용하여 메시지에 디지털 서명을 하고 X.509 인증서를 메시지에 첨부하지 않으며 해당 주체 키 식별자를 사용하여 인증서를 참조합니다.  
  
- 서비스의 컴퓨터에는 공개 키가 같지만 다른 정보가 들어 있는 인증서가 두 개 이상 있습니다.  
  
- 서비스에서는 주체 키 식별자와 일치하는 인증서를 검색하지만 클라이언트가 사용하려고 했던 인증서는 아닙니다. WCF는 메시지를 수신 하 고 서명을 확인할 때 원치 않는 x.509 인증서의 정보를 클라이언트에서 예상한 것과 다른 잠재적으로 상승 된 클레임 집합에 매핑합니다.  
  
 이 가능성을 줄이려면 <xref:System.ServiceModel.Security.Tokens.X509KeyIdentifierClauseType.IssuerSerial> 사용 등의 방식으로 X.509 인증서를 참조합니다.  
  
## <a name="see-also"></a>참고자료

- [보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)
- [정보 공개](../../../../docs/framework/wcf/feature-details/information-disclosure.md)
- [서비스 거부](../../../../docs/framework/wcf/feature-details/denial-of-service.md)
- [재생 공격](../../../../docs/framework/wcf/feature-details/replay-attacks.md)
- [변조](../../../../docs/framework/wcf/feature-details/tampering.md)
- [지원되지 않는 시나리오](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)
