---
title: 자격 증명 형식 선택
ms.date: 03/30/2017
ms.assetid: bf707063-3f30-4304-ab53-0e63413728a8
ms.openlocfilehash: b5dd757328fc04ccbbce7eaed2bd1a28b3e1282e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69949220"
---
# <a name="selecting-a-credential-type"></a>자격 증명 형식 선택
*자격 증명* 은 요청 된 id 또는 기능을 설정 하는 데 사용 하는 WCF (데이터 Windows Communication Foundation)입니다. 예를 들어 여권은 정부에서 국가나 지역의 시민권을 입증하기 위해 발급하는 자격 증명입니다. WCF에서 자격 증명은 사용자 이름 토큰 및 x.509 인증서와 같은 많은 형식을 사용할 수 있습니다. 이 항목에서는 자격 증명, WCF에서 자격 증명을 사용 하는 방법 및 응용 프로그램에 적합 한 자격 증명을 선택 하는 방법에 대해 설명 합니다.  
  
 많은 국가와 지역에서 운전 면허는 자격 증명의 예입니다. 라이선스에는 사용자의 신분과 능력을 나타내는 데이터가 들어 있습니다. 또한 소유자의 사진 형태로 소유 증명이 포함되어 있습니다. 라이선스는 신뢰할 수 있는 기관(일반적으로 정부 라이선스 부서)에서 발급됩니다. 라이선스에는 날인이 찍히며, 변조 또는 위조되지 않았음을 증명하는 홀로그램이 삽입되어 있을 수 있습니다.  
  
 자격 증명을 제공할 때는 데이터와 데이터 소유 증명을 모두 제공해야 합니다. WCF는 전송 및 메시지 보안 수준에서 다양 한 자격 증명 형식을 지원 합니다. 예를 들어 WCF: 사용자 이름 및 (x.509) 인증서 자격 증명에서 지원 되는 두 가지 형식의 자격 증명을 고려 합니다.  
  
 사용자 이름 자격 증명에서 사용자 이름은 요구된 ID를 나타내고 암호는 소유 증명을 제공합니다. 이 경우 신뢰할 수 있는 기관은 사용자 이름과 암호의 유효성을 검사하는 시스템입니다.  
  
 X.509 인증서 자격 증명을 사용 하 여 주체 이름, 주체 대체 이름 또는 인증서 내의 특정 필드를 id 클레임으로 사용할 수 있는 반면, `Valid From` 및 `Valid To` 필드와 같은 다른 필드는의 유효성을 지정 합니다. 인증서.  
  
## <a name="transport-credential-types"></a>전송 자격 증명 형식  
 다음 표에서는 전송 보안 모드의 바인딩에서 사용할 수 있는 클라이언트 자격 증명 형식을 보여 줍니다. 서비스를 만드는 경우 `ClientCredentialType` 속성을 이러한 값 중 하나로 설정하여 클라이언트가 서비스와 통신하기 위해 제공해야 하는 자격 증명 형식을 지정합니다. 코드 또는 구성 파일에서 형식을 설정할 수 있습니다.  
  
|설정|Description|  
|-------------|-----------------|  
|없음|클라이언트가 자격 증명을 제공할 필요가 없음을 지정합니다. 익명 클라이언트로 변환됩니다.|  
|Basic|클라이언트에 대한 기본 인증을 지정합니다. 자세한 내용은 RFC2617-[HTTP Authentication을 참조 하세요. 기본 인증 및 다이제스트 인증](https://go.microsoft.com/fwlink/?LinkID=88313)을 참조하세요.|  
|Digest|클라이언트에 대한 다이제스트 인증을 지정합니다. 자세한 내용은 RFC2617-[HTTP Authentication을 참조 하세요. 기본 인증 및 다이제스트 인증](https://go.microsoft.com/fwlink/?LinkID=88313)을 참조하세요.|  
|Ntlm|NTLM(NT LAN Manager) 인증을 지정합니다. 이 인증은 어떤 이유로 Kerberos 인증을 사용할 수 없는 경우에 사용됩니다. <xref:System.ServiceModel.Security.WindowsClientCredential.AllowNtlm%2A> 속성을로 `false`설정 하 여이를 대체 방법으로 사용 하지 않도록 설정할 수도 있습니다. 이렇게 하면 NTLM이 사용 되는 경우 WCF에서 예외를 throw 하는 데 가장 적합 합니다. 이 속성을 `false`로 설정하면 유선을 통해 NTLM 자격 증명을 보낼 수 있습니다.|  
|Windows|Windows 인증을 지정합니다. Windows 도메인에서 Kerberos 프로토콜만 지정하려면 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowNtlm%2A> 속성을 `false`로 설정합니다. 기본값은 `true`입니다.|  
|Certificate|X.509 인증서를 사용하여 클라이언트 인증을 수행합니다.|  
|암호|사용자가 사용자 이름과 암호를 제공해야 합니다. Windows 인증 또는 다른 사용자 지정 솔루션을 사용하여 사용자 이름/암호 쌍의 유효성을 검사합니다.|  
  
### <a name="message-client-credential-types"></a>메시지 클라이언트 자격 증명 형식  
 다음 표에서는 메시지 보안을 사용하는 애플리케이션을 만들 때 사용할 수 있는 자격 증명 형식을 보여 줍니다. 코드 또는 구성 파일에서 이러한 값을 사용할 수 있습니다.  
  
|설정|설명|  
|-------------|-----------------|  
|없음|클라이언트가 자격 증명을 제공할 필요가 없음을 지정합니다. 익명 클라이언트로 변환됩니다.|  
|Windows|Windows 자격 증명으로 설정된 보안 컨텍스트에서 SOAP 메시지 교환을 수행할 수 있습니다.|  
|Username|서비스에서 사용자 이름 자격 증명을 사용하여 클라이언트를 인증하도록 요구할 수 있습니다. WCF에서는 서명 생성 또는 데이터 암호화와 같은 사용자 이름을 가진 암호화 작업을 허용 하지 않습니다. WCF는 사용자 이름 자격 증명을 사용할 때 전송 보안이 유지 되도록 합니다.|  
|Certificate|서비스에서 X.509 인증서를 사용하여 클라이언트를 인증하도록 요구할 수 있습니다.|  
|Issued Token|보안 정책에 따라 구성된 사용자 지정 토큰 형식입니다. 기본 토큰 형식은 SAML(Security Assertions Markup Language)입니다. 토큰은 보안 토큰 서비스에 의해 발급됩니다. 자세한 내용은 [페더레이션 및 발급 된 토큰](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)을 참조 하세요.|  
  
### <a name="negotiation-model-of-service-credentials"></a>서비스 자격 증명의 협상 모델  
 *협상* 은 자격 증명을 교환 하 여 클라이언트와 서비스 간에 트러스트를 설정 하는 프로세스입니다. 이 프로세스는 협상 프로세스의 다음 단계에 필요한 정보만 공개하도록 클라이언트와 서비스 간에 반복적으로 수행됩니다. 실제로 최종 결과는 후속 작업에 사용할 서비스의 자격 증명이 클라이언트에 전달됩니다.  
  
 한 가지 예외를 제외 하 고 기본적으로 WCF의 시스템 제공 바인딩은 메시지 수준 보안을 사용 하는 경우 서비스 자격 증명을 자동으로 협상 합니다. 예외는 기본적으로 보안을 사용하지 않는 <xref:System.ServiceModel.BasicHttpBinding>입니다. 이 동작을 사용하지 않도록 설정하려면 <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> 및 <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.NegotiateServiceCredential%2A> 속성을 참조하세요.  
  
> [!NOTE]
> .NET Framework 3.5 이상에서 SSL 보안을 사용 하는 경우 WCF 클라이언트는 인증서 저장소의 중간 인증서와 SSL 협상 중에 받은 중간 인증서를 모두 사용 하 여 서비스에서 인증서 체인 유효성 검사를 수행 합니다. 인증서. .NET Framework 3.0은 로컬 인증서 저장소에 설치된 중간 인증서만 사용합니다.  
  
#### <a name="out-of-band-negotiation"></a>Out-of-Band 협상  
 자동 협상을 사용하지 않는 경우 메시지를 서비스로 보내기 전에 클라이언트에서 서비스 자격 증명을 구축해야 합니다. 이를 *대역 외* 프로 비전이 라고도 합니다. 예를 들어 지정한 자격 증명 형식이 인증서이고 자동 협상을 사용할 수 없는 경우 클라이언트는 서비스 소유자에 연결하여 인증서를 받고 클라이언트 애플리케이션을 실행하는 컴퓨터에 설치해야 합니다. 이 작업은 예를 들어 B2B 시나리오에서 서비스에 액세스할 수 있는 클라이언트를 엄격하게 제어하려는 경우에 수행할 수 있습니다. 이러한 대역 외 협상은 전자 메일에서 수행할 수 있으며, x.509 인증서는 Microsoft Management Console (MMC) 인증서 스냅인과 같은 도구를 사용 하 여 Windows 인증서 저장소에 저장 됩니다.  
  
> [!NOTE]
> <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 속성은 out-of-band 협상을 통해 얻은 인증서를 서비스에 제공하는 데 사용됩니다. 이 속성은 바인딩에서 자동 협상을 허용하지 않으므로 <xref:System.ServiceModel.BasicHttpBinding> 클래스를 사용할 때 필요합니다. 이 속성은 상관 관계가 없는 이중 시나리오에서도 사용됩니다. 이 시나리오에서는 클라이언트가 먼저 서버로 요청을 보내지 않고도 서버가 클라이언트에게 메시지를 보냅니다. 서버는 클라이언트로부터 받은 요청이 없으므로 클라이언트 인증서를 사용하여 클라이언트에 대한 메시지를 암호화해야 합니다.  
  
## <a name="setting-credential-values"></a>자격 증명 값 설정  
 보안 모드를 선택한 후에는 실제 자격 증명을 지정해야 합니다. 예를 들어 자격 증명 형식이 "인증서"로 설정된 경우 특정 X.509 인증서 같은 특정 자격 증명을 서비스 또는 클라이언트와 연결해야 합니다.  
  
 서비스 또는 클라이언트를 프로그래밍할지에 따라 자격 증명 값을 설정하는 방법이 약간씩 다릅니다.  
  
### <a name="setting-service-credentials"></a>서비스 자격 증명 설정  
 전송 모드를 사용하고 HTTP를 전송으로 사용하는 경우에는 IIS(인터넷 정보 서비스)를 사용하거나 인증서로 포트를 구성해야 합니다. 자세한 내용은 [전송 보안 개요](../../../../docs/framework/wcf/feature-details/transport-security-overview.md) 및 [HTTP 전송 보안](../../../../docs/framework/wcf/feature-details/http-transport-security.md)을 참조 하세요.  
  
 코드에서 자격 증명으로 서비스를 구축하려면 <xref:System.ServiceModel.ServiceHost> 클래스의 인스턴스를 만들고 <xref:System.ServiceModel.Description.ServiceCredentials> 속성을 통해 액세스하는 <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> 클래스를 사용하여 적절한 자격 증명을 지정합니다.  
  
#### <a name="setting-a-certificate"></a>인증서 설정  
 서비스를 클라이언트에 인증하는 데 사용할 X.509 인증서로 서비스를 구축하려면 <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.SetCertificate%2A> 클래스의 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> 메서드를 사용합니다.  
  
 클라이언트 인증서로 서비스를 구축하려면 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> 클래스의 <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential> 메서드를 사용합니다.  
  
#### <a name="setting-windows-credentials"></a>Windows 자격 증명 설정  
 클라이언트가 올바른 사용자 이름과 암호를 지정하면 해당 자격 증명이 클라이언트 인증에 사용됩니다. 그렇지 않으면 현재 로그온한 사용자의 자격 증명이 사용됩니다.  
  
### <a name="setting-client-credentials"></a>클라이언트 자격 증명 설정  
 WCF에서 클라이언트 응용 프로그램은 WCF 클라이언트를 사용 하 여 서비스에 연결 합니다. 모든 클라이언트는 <xref:System.ServiceModel.ClientBase%601> 클래스에서 파생되고, 클라이언트의 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 속성은 클라이언트 자격 증명의 다양한 값을 지정하는 데 사용됩니다.  
  
#### <a name="setting-a-certificate"></a>인증서 설정  
 클라이언트를 서비스에 인증하는 데 사용되는 X.509 인증서로 서비스를 구축하려면 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> 클래스의 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential> 메서드를 사용합니다.  
  
## <a name="how-client-credentials-are-used-to-authenticate-a-client-to-the-service"></a>클라이언트 자격 증명을 사용하여 클라이언트를 서비스에 인증하는 방법  
 서비스와 통신하는 데 필요한 클라이언트 자격 증명 정보는 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 속성이나 <xref:System.ServiceModel.ChannelFactory.Credentials%2A> 속성을 사용하여 제공됩니다. 보안 채널은 이 정보를 사용하여 클라이언트를 서비스에 인증합니다. 인증은 다음 두 가지 모드 중 하나를 통해 수행됩니다.  
  
- 클라이언트 자격 증명은 WCF 클라이언트 인스턴스를 사용 하 여 보안 컨텍스트를 설정 하는 첫 번째 메시지를 전송 하기 전에 한 번 사용 됩니다. 그런 다음 모든 애플리케이션 메시지는 보안 컨텍스트를 통해 보안이 유지됩니다.  
  
- 서비스로 전송되는 모든 애플리케이션 메시지를 인증하는 데 클라이언트 자격 증명이 사용됩니다. 이 경우에는 클라이언트와 서비스 간에 컨텍스트가 설정되지 않습니다.  
  
### <a name="established-identities-cannot-be-changed"></a>설정된 ID를 변경할 수 없음  
 첫 번째 방법을 사용하면 설정된 컨텍스트가 영구적으로 클라이언트 ID와 연결됩니다. 즉, 보안 컨텍스트가 설정되고 나면 클라이언트와 연결된 ID를 변경할 수 없습니다.  
  
> [!IMPORTANT]
> ID를 전환할 수 없을 때(보안 컨텍스트 설정이 켜진 경우의 기본 동작) 주의해야 할 경우가 있습니다. 두 번째 서비스와 통신 하는 서비스를 만드는 경우 WCF 클라이언트를 두 번째 서비스에 여는 데 사용 된 id를 변경할 수 없습니다. 여러 클라이언트가 첫 번째 서비스를 사용할 수 있고 두 번째 서비스에 액세스할 때 서비스가 클라이언트를 가장하는 경우 이것이 문제가 됩니다. 서비스가 모든 호출자에 대해 동일한 클라이언트를 다시 사용하는 경우 두 번째 서비스에 대한 모든 호출은 클라이언트를 두 번째 서비스에 여는 데 사용된 첫 번째 호출자의 ID로 수행됩니다. 즉, 서비스는 모든 클라이언트에 대해 첫 번째 클라이언트의 ID를 사용하여 두 번째 서비스와 통신합니다. 이 경우 권한 상승이 발생할 수 있습니다. 원하는 서비스 동작이 아닌 경우 각 호출자를 추적하여 각 호출자와 관련해서 두 번째 서비스에 대해 새 클라이언트를 만들고 서비스가 올바른 호출자에 대해 올바른 클라이언트만 사용하여 두 번째 서비스와 통신하도록 해야 합니다.  
  
 자격 증명 및 보안 세션에 대 한 자세한 내용은 보안 [세션의 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-secure-sessions.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpMessageSecurity.ClientCredentialType%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityOverMsmq.ClientCredentialType%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityOverTcp.ClientCredentialType%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.TcpTransportSecurity.ClientCredentialType%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.SetCertificate%2A?displayProperty=nameWithType>
- [보안 개념](../../../../docs/framework/wcf/feature-details/security-concepts.md)
- [서비스 및 클라이언트에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
- [WCF 보안 프로그래밍](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)
- [HTTP 전송 보안](../../../../docs/framework/wcf/feature-details/http-transport-security.md)
