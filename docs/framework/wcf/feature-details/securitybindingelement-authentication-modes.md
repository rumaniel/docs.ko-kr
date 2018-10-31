---
title: SecurityBindingElement 인증 모드
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 12300bf4-c730-4405-9f65-d286f68b5a43
ms.openlocfilehash: 2b1601bd84e92b5a39c5c4c91fdfe67537720430
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198397"
---
# <a name="securitybindingelement-authentication-modes"></a>SecurityBindingElement 인증 모드
Windows Communication Foundation (WCF)는 클라이언트 및 서비스 인증 서로 몇 가지 모드를 제공 합니다. <xref:System.ServiceModel.Channels.SecurityBindingElement> 클래스에 정적 메서드를 사용하거나 구성을 통해 이러한 인증 모드의 보안 바인딩 요소를 만들 수 있습니다. 이 항목에서는 18가지의 인증 모드에 대해 간단히 설명합니다.  
  
 요소를 사용 하 여 인증 모드 중 하나에 대 한 예제를 보려면 [방법: 지정 된 인증 모드에 대 한 SecurityBindingElement 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)합니다.  
  
## <a name="basic-configuration-programming"></a>기본 구성 프로그래밍  
 다음 절차에서는 구성 파일에 인증 모드를 설정하는 방법을 설명합니다.  
  
#### <a name="to-set-the-authentication-mode-in-configuration"></a>구성 파일에 인증 모드를 설정하려면  
  
1.  에 [ \<바인딩 >](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 요소에 추가 [ \<customBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)합니다.  
  
2.  자식 요소를 추가 하는 [ \<바인딩 >](../../../../docs/framework/misc/binding.md) 요소를 `<customBinding>` 요소.  
  
3.  `<security>` 요소를 `<binding>` 요소에 추가합니다.  
  
4.  `authenticationMode` 특성을 아래 설명된 값 중 하나로 설정합니다. 예를 들어 다음 코드에서는 모드를 `AnonymousForCertificate`로 설정합니다.  
  
    ```xml  
    <bindings>  
      <customBinding>  
        <binding name="SecureCustomBinding">  
         <security authenticationMode ="AnonymousForCertificate" />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
#### <a name="to-set-the-mode-programmatically"></a>프로그래밍 방식으로 모드를 설정하려면  
  
1.  반환 형식을<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>, <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>, <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 또는 <xref:System.ServiceModel.Channels.SecurityBindingElement> 중에서 선택합니다.  
  
2.  <xref:System.ServiceModel.Channels.SecurityBindingElement> 클래스의 적절한 정적 메서드를 호출합니다. 예를 들어 다음 코드에서는 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateAnonymousForCertificateBindingElement%2A> 메서드를 호출합니다.  
  
     [!code-csharp[c_CustomBindingsAuthMode#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombindingsauthmode/cs/source.cs#3)]
     [!code-vb[c_CustomBindingsAuthMode#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_custombindingsauthmode/vb/source.vb#3)]  
  
3.  바인딩 요소를 사용하여 사용자 지정 바인딩을 만듭니다. 자세한 내용은 [사용자 지정 바인딩](../../../../docs/framework/wcf/extending/custom-bindings.md)합니다.  
  
## <a name="mode-descriptions"></a>모드 설명  
  
### <a name="anonymousforcertificate"></a>AnonymousForCertificate  
 이 인증 모드에서 클라이언트는 비대칭이고 서비스는 X.509 인증서를 사용하여 인증됩니다. 보안 바인딩 요소는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateAnonymousForCertificateBindingElement%2A>입니다. 또는 설정 합니다 `authenticationMode` 특성을 <`security`> 요소를 `AnonymousForCertificate`.  
  
### <a name="anonymousforsslnegotiated"></a>AnonymousForSslNegotiated  
 이 인증 모드에서 클라이언트는 비대칭이고 서비스는 런타임에 협상되는 X.509 인증서를 사용하여 인증됩니다. 보안 바인딩 요소는 첫 번째 매개 변수에 대해 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 값이 전달될 때 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSslNegotiationBindingElement%2A> 메서드에 의해 반환된 `false`입니다. 또는 `authenticationMode` 특성을 `AnonymousForSslNegotiated`로 설정합니다.  
  
### <a name="certificateovertransport"></a>CertificateOverTransport  
 이 인증 모드에서 클라이언트는 메시지 서명에 서명한 토큰인 보증 지원 토큰으로 SOAP 계층에 표시되는 X.509 인증서를 사용하여 인증합니다. 서비스는 전송 계층에서 X.509 인증서를 사용하여 인증됩니다. 보안 바인딩 요소는 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement> 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateCertificateOverTransportBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `CertificateOverTransport`로 설정합니다.  
  
### <a name="issuedtoken"></a>IssuedToken  
 이 인증 모드에서는 클라이언트가 서비스를 인증하지 않으므로 대신 클라이언트가 보안 토큰 서비스를 인증하고 SAML 토큰을 수신한 다음 서버에 제공하여 공유 키에 대해 알고 있음을 증명합니다. 서비스가 클라이언트에 인증되지 않습니다. 대신 보안 토큰 서비스에서 공유 키를 발급된 토큰의 일부로 암호화하여 서비스에서만 키를 해독할 수 있게 합니다. 보안 바인딩 요소는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `IssuedToken`로 설정합니다.  
  
### <a name="issuedtokenforcertificate"></a>IssuedTokenForCertificate  
 이 인증 모드에서는 클라이언트가 서비스를 인증하지 않으므로 대신 클라이언트가 보안 토큰 서비스를 인증하고 SAML 토큰을 수신한 다음 서버에 제공하여 공유 키에 대해 알고 있음을 증명합니다. 발급된 토큰은 메시지 서명에 서명한 토큰인 보증 지원 토큰 또는 bearer 토큰으로 SOAP 계층에 표시됩니다. 서비스는 X.509 인증서를 사용하여 클라이언트를 인증합니다. 보안 바인딩 요소는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `IssuedTokenForCertificate`로 설정합니다.  
  
### <a name="issuedtokenforsslnegotiated"></a>IssuedTokenForSslNegotiated  
 이 인증 모드에서는 클라이언트가 서비스를 인증하지 않으므로 대신 클라이언트가 보안 토큰 서비스를 인증하고 SAML 토큰을 수신한 다음 서버에 제공하여 공유 키에 대해 알고 있음을 증명합니다. 발급된 토큰은 메시지 서명에 서명한 토큰인 보증 지원 토큰 또는 bearer 토큰으로 SOAP 계층에 표시됩니다. 서비스는 X.509 인증서를 사용하여 인증됩니다. 보안 바인딩 요소는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForSslBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `IssuedTokenForSslnegotiated`로 설정합니다.  
  
### <a name="issuedtokenovertransport"></a>IssuedTokenOverTransport  
 이 인증 모드에서는 클라이언트가 서비스를 인증하지 않으므로 대신 클라이언트가 보안 토큰 서비스를 인증하고 SAML 토큰을 수신한 다음 서버에 제공하여 공유 키에 대해 알고 있음을 증명합니다. 발급된 토큰은 메시지 서명에 서명한 토큰인 보증 지원 토큰 또는 bearer 토큰으로 SOAP 계층에 표시됩니다. 서비스는 전송 계층에서 X.509 인증서를 사용하여 인증됩니다. 보안 바인딩 요소는 `TransportSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenOverTransportBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `IssuedTokenOverTransport`로 설정합니다.  
  
### <a name="kerberos"></a>Kerberos  
 이 인증 모드에서는 클라이언트가 Kerberos 티켓을 사용하여 서비스를 인증합니다. 동일한 티켓에서 서버 인증을 제공합니다. 보안 바인딩 요소는 `SymmetricSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `Kerberos`로 설정합니다.  
  
> [!NOTE]
>  이 인증 모드를 사용하려면 서비스 계정이 SPN(서비스 사용자 이름)과 연결되어야 합니다. 이 작업을 수행하려면 NETWORK SERVICE 계정이나 LOCAL SYSTEM 계정에서 서비스를 실행합니다. 또는 SetSpn.exe 도구를 사용하여 서비스 계정의 SPN을 만듭니다. 두 경우 모두 클라이언트에는 정확한 SPN을 사용 해야 합니다는 [ \<servicePrincipalName >](../../../../docs/framework/configure-apps/file-schema/wcf/serviceprincipalname.md) 요소를 또는 사용 하 여는 <xref:System.ServiceModel.EndpointAddress> 생성자입니다. 자세한 내용은 [서비스 Id 및 인증](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)합니다.  
  
> [!NOTE]
>  `Kerberos` 인증 모드를 사용하면 <xref:System.Security.Principal.TokenImpersonationLevel.Anonymous> 및 <xref:System.Security.Principal.TokenImpersonationLevel.Delegation> 가장 수준이 지원되지 않습니다.  
  
### <a name="kerberosovertransport"></a>KerberosOverTransport  
 이 인증 모드에서는 클라이언트가 Kerberos 티켓을 사용하여 서비스를 인증합니다. Kerberos 토큰은 메시지 서명에 서명한 토큰인 보증 지원 토큰으로 SOAP 계층에 표시됩니다. 서비스는 전송 계층에서 X.509 인증서를 사용하여 인증됩니다. 보안 바인딩 요소는 `TransportSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosOverTransportBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `KerberosOverTransport`로 설정합니다.  
  
> [!NOTE]
>  이 인증 모드를 사용하려면 서비스 계정이 SPN과 연결되어야 합니다. 이 작업을 수행하려면 NETWORK SERVICE 계정이나 LOCAL SYSTEM 계정에서 서비스를 실행합니다. 또는 SetSpn.exe 도구를 사용하여 서비스 계정의 SPN을 만듭니다. 두 경우 모두 클라이언트에는 정확한 SPN을 사용 해야 합니다는 [ \<servicePrincipalName >](../../../../docs/framework/configure-apps/file-schema/wcf/serviceprincipalname.md) 요소를 또는 사용 하 여는 <xref:System.ServiceModel.EndpointAddress> 생성자입니다. 자세한 내용은 [서비스 Id 및 인증](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)합니다.  
  
### <a name="mutualcertificate"></a>MutualCertificate  
 이 인증 모드에서 클라이언트는 메시지 서명에 서명한 토큰인 보증 지원 토큰으로 SOAP 계층에 표시되는 X.509 인증서를 사용하여 인증합니다. 서비스도 X.509 인증서를 사용하여 인증됩니다. 보안 바인딩 요소는 `SymmetricSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `MutualCertificate`로 설정합니다.  
  
### <a name="mutualcertificateduplex"></a>MutualCertificateDuplex  
 이 인증 모드에서 클라이언트는 메시지 서명에 서명한 토큰인 보증 지원 토큰으로 SOAP 계층에 표시되는 X.509 인증서를 사용하여 인증합니다. 서비스도 X.509 인증서를 사용하여 인증됩니다. 바인딩은 `AsymmetricSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateDuplexBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `MutualCertificateDuplex`로 설정합니다.  
  
### <a name="mutualsslnegotiated"></a>MutualSslNegotiated  
 이 인증 모드에서 클라이언트 및 서비스는 X.509 인증서를 사용하여 인증합니다. 보안 바인딩 요소는 첫 번째 매개 변수에 대해 `SymmetricSecurityBindingElement` 값이 전달될 때 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSslNegotiationBindingElement%2A> 메서드에 의해 반환된 `true`입니다. 또는 `authenticationMode` 특성을 `MutualSslNegotiated`로 설정합니다.  
  
### <a name="secureconversation"></a>SecureConversation  
 보안 바인딩 요소는 `SymmetricSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSecureConversationBindingElement%2A>입니다. 이 메서드는 <xref:System.ServiceModel.Channels.SecurityBindingElement>를 초기화 중에 보안 세션 설정에 사용할 매개 변수로 사용합니다. 또는 `authenticationMode` 특성을 `SecureConversation`로 설정합니다.  
  
 부트스트랩 바인딩이 지정되지 않은 경우에는 `SspiNegotiated` 인증 모드가 부트스트랩에 사용됩니다.  
  
### <a name="sspinegotiation"></a>SspiNegotiation  
 이 인증 모드에서는 협상 프로토콜을 사용하여 클라이언트 및 서버 인증을 수행합니다. 가능한 경우에는 Kerberos가 사용되며 그 이외에는 NTLM(NT LanMan)이 사용됩니다. 보안 바인딩 요소는 `SymmetricSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `SspiNegotiated`로 설정합니다.  
  
### <a name="sspinegotiatedovertransport"></a>SspiNegotiatedOverTransport  
 이 인증 모드에서는 협상 프로토콜을 사용하여 클라이언트 및 서버 인증을 수행합니다. 가능하면 Kerberos 프로토콜이 사용되고, 그렇지 않으면 NTLM이 사용됩니다. 결과 토큰은 메시지 서명에 서명한 토큰인 보증 지원 토큰으로 SOAP 계층에 표시됩니다. 서비스는 전송 계층에서 X.509 인증서를 사용하여 추가 인증됩니다. 보안 바인딩 요소는 `TransportSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationOverTransportBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `SspiNegotiatedOverTransport`로 설정합니다.  
  
### <a name="usernameforcertificate"></a>UserNameForCertificate  
 이 인증 모드에서 클라이언트는 메시지 서명에 의해 서명된 토큰인 서명된 지원 토큰으로 SOAP 계층에 표시되는 사용자 이름 토큰을 사용하여 서비스를 인증합니다. 서비스는 X.509 인증서를 사용하여 클라이언트를 인증합니다. 보안 바인딩 요소는 `SymmetricSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateUserNameForCertificateBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `UserNameForCertificate`로 설정합니다.  
  
 `UserNameForCertificate` 인증 모드의 경우 클라이언트와 서비스 모두 WS-Security 1.1을 사용해야 합니다.  
  
### <a name="usernameforsslnegotiated"></a>UserNameForSslNegotiated  
 이 인증 모드에서 클라이언트는 메시지 서명에 의해 서명된 토큰인 서명된 지원 토큰으로 SOAP 계층에 표시되는 사용자 이름 토큰을 사용하여 인증합니다. 서비스는 X.509 인증서를 사용하여 인증됩니다. 보안 바인딩 요소는 `SymmetricSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateUserNameForSslBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `UserNameForSslNegotiated`로 설정합니다.  
  
### <a name="usernameovertransport"></a>UserNameOverTransport  
 이 인증 모드에서 클라이언트는 메시지 서명에 의해 서명된 토큰인 서명된 지원 토큰으로 SOAP 계층에 표시되는 사용자 이름 토큰을 사용하여 인증합니다. 서비스는 전송 계층에서 X.509 인증서를 사용하여 인증됩니다. 보안 바인딩 요소는 `TransportSecurityBindingElement` 메서드에서 반환된 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateUserNameOverTransportBindingElement%2A>입니다. 또는 `authenticationMode` 특성을 `UserNameOverTransport`로 설정합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>  
 [방법: 지정된 인증 모드에 대한 SecurityBindingElement 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)
