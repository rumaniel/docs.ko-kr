---
title: Windows 인증 오류 디버깅
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, authentication
- WCF, Windows authentication
ms.assetid: 181be4bd-79b1-4a66-aee2-931887a6d7cc
ms.openlocfilehash: 20ca8f049298f75412da4c8a7e58975954f67741
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968854"
---
# <a name="debugging-windows-authentication-errors"></a>Windows 인증 오류 디버깅
Windows 인증을 보안 메커니즘으로 사용하면 SSPI(보안 지원 공급자 인터페이스)에서 보안 프로세스를 처리합니다. SSPI 계층에서 보안 오류가 발생 하면 Windows Communication Foundation (WCF)에 의해 표시 됩니다. 이 항목에서는 오류 진단에 도움이 되는 프레임워크 및 일련의 질문을 제공합니다.  
  
 Kerberos 프로토콜에 대 한 개요는 [Kerberos 설명](https://go.microsoft.com/fwlink/?LinkID=86946)을 참조 하세요. SSPI의 개요는 [sspi](https://go.microsoft.com/fwlink/?LinkId=88941)를 참조 하십시오.  
  
 Windows 인증의 경우 WCF는 일반적으로 클라이언트와 서비스 간에 Kerberos 상호 인증을 수행 하는 *NEGOTIATE* SSP (보안 지원 공급자)를 사용 합니다. Kerberos 프로토콜을 사용할 수 없는 경우 기본적으로 WCF는 NTLM (NT LAN Manager)으로 대체 됩니다. 그러나 Kerberos 프로토콜만 사용 하도록 WCF를 구성 하 고 Kerberos를 사용할 수 없는 경우 예외를 throw 할 수 있습니다. 제한 된 형태의 Kerberos 프로토콜을 사용 하도록 WCF를 구성할 수도 있습니다.  
  
## <a name="debugging-methodology"></a>디버깅 방법  
 기본 방법은 다음과 같습니다.  
  
1. Windows 인증 사용 여부를 결정합니다. 다른 스키마를 사용할 경우 이 항목이 적용되지 않습니다.  
  
2. Windows 인증을 사용 하는 경우 WCF 구성에서 Kerberos 다이렉트를 사용 하는지 아니면 Negotiate를 사용 하는지 결정 합니다.  
  
3. 구성에서 Kerberos 프로토콜을 사용할지 또는 NTLM을 사용할지 결정한 다음에는 올바른 컨텍스트에서 오류 메시지를 이해할 수 있습니다.  
  
### <a name="availability-of-the-kerberos-protocol-and-ntlm"></a>Kerberos 프로토콜 및 NTLM 사용 가능성  
 Kerberos SSP에는 Kerberos KDC(키 배포 센터) 역할을 하는 도메인 컨트롤러가 있어야 합니다. Kerberos 프로토콜은 클라이언트와 서비스 둘 다에서 도메인 ID를 사용하는 경우에만 사용할 수 있습니다. 다음 표에 요약된 것처럼 다른 계정 조합의 경우 NTLM이 사용됩니다.  
  
 표 머리글에는 서버에서 사용할 수 있는 계정 형식이 표시되어 있으며, 왼쪽 열에는 클라이언트에서 사용할 수 있는 계정 형식이 표시되어 있습니다.  
  
||로컬 사용자|로컬 시스템|도메인 사용자|도메인 컴퓨터|  
|-|----------------|------------------|-----------------|--------------------|  
|로컬 사용자|NTLM|NTLM|NTLM|NTLM|  
|로컬 시스템|익명 NTLM|익명 NTLM|익명 NTLM|익명 NTLM|  
|도메인 사용자|NTLM|NTLM|Kerberos|Kerberos|  
|도메인 컴퓨터|NTLM|NTLM|Kerberos|Kerberos|  
  
 특히 네 가지 계정 형식에는 다음이 포함됩니다.  
  
- 로컬 사용자: 컴퓨터 전용 사용자 프로필입니다. 예를 들면 `MachineName\Administrator` 또는 `MachineName\ProfileName` 등입니다.  
  
- 로컬 시스템: 도메인에 가입 되지 않은 컴퓨터의 기본 제공 계정 시스템입니다.  
  
- 도메인 사용자: Windows 도메인의 사용자 계정 예를 들어 `DomainName\ProfileName`을 참조하십시오.  
  
- 도메인 컴퓨터: Windows 도메인에 가입 된 컴퓨터에서 실행 되는 컴퓨터 id를 사용 하는 프로세스입니다. 예를 들어 `MachineName\Network Service`을 참조하십시오.  
  
> [!NOTE]
> 서비스 자격 증명은 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 클래스의 <xref:System.ServiceModel.ServiceHost> 메서드가 호출될 때 캡처됩니다. 클라이언트 자격 증명은 클라이언트가 메시지를 보낼 때마다 읽어 옵니다.  
  
## <a name="common-windows-authentication-problems"></a>일반적인 Windows 인증 문제  
 이 단원에서는 몇 가지 일반적인 Windows 인증 문제와 그 해결 방법에 대해 설명합니다.  
  
### <a name="kerberos-protocol"></a>Kerberos 프로토콜  
  
#### <a name="spnupn-problems-with-the-kerberos-protocol"></a>Kerberos 프로토콜에 대한 SPN/UPN 문제  
 Windows 인증을 사용할 때 Kerberos 프로토콜을 사용하거나 SSPI 협상을 수행하는 경우, 클라이언트 엔드포인트에 사용되는 URL은 서비스 URL 내에 있는 서비스 호스트의 정규화된 도메인 이름을 포함해야 합니다. 이 경우 서비스를 실행 하는 계정에는 컴퓨터를 Active Directory 도메인에 추가할 때 생성 되는 컴퓨터 (기본) SPN (서비스 사용자 이름) 키에 대 한 액세스 권한이 있다고 가정 합니다 .이는 아래에서 서비스를 실행 하 여 가장 일반적으로 수행 됩니다. 네트워크 서비스 계정. 서비스에 시스템 SPN 키에 대한 액세스 권한이 없는 경우 클라이언트의 엔드포인트 ID로 서비스가 실행 중인 계정의 올바른 SPN 또는 UPN(User Principal Name)을 제공해야 합니다. WCF가 SPN 및 UPN과 작동 하는 방법에 대 한 자세한 내용은 [서비스 id 및 인증](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)을 참조 하세요.  
  
 웹 팜 또는 웹 가든과 같은 부하 분산 시나리오에서는 각 애플리케이션에 대해 고유한 계정을 정의하고, 해당 계정에 SPN을 할당하고, 애플리케이션의 모든 서비스가 해당 계정으로 실행되도록 하는 것이 일반적입니다.  
  
 서비스 계정에 대한 SPN을 얻으려면 Active Directory 도메인 관리자여야 합니다. 자세한 내용은 [Windows 용 Kerberos 기술 보충 자료](https://go.microsoft.com/fwlink/?LinkID=88330)를 참조 하십시오.  
  
#### <a name="kerberos-protocol-direct-requires-the-service-to-run-under-a-domain-machine-account"></a>Kerberos 프로토콜을 직접 사용하려면 도메인 컴퓨터 계정으로 서비스 실행이 필요  
 이는 다음 코드처럼 `ClientCredentialType` 속성이 `Windows`로 설정되고, <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> 속성이 `false`로 설정된 경우 발생합니다.  
  
 [!code-csharp[C_DebuggingWindowsAuth#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#1)]
 [!code-vb[C_DebuggingWindowsAuth#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#1)]  
  
 이 문제를 해결하려면 도메인과 연결된 컴퓨터에서 Network Service 등의 도메인 컴퓨터 계정을 사용하여 서비스를 실행합니다.  
  
### <a name="delegation-requires-credential-negotiation"></a>위임에 자격 증명 협상 필요  
 Kerberos 인증 프로토콜을 위임과 함께 사용하려면 자격 증명 협상이 포함된 Kerberos 프로토콜("multi-leg" 또는 "multi-step" Kerberos라고 함)을 구현해야 합니다. 자격 증명 협상이 포함되지 않은 Kerberos 프로토콜("one-shot" 또는 "single-leg" Kerberos라고도 함)을 구현하면 예외가 throw됩니다.  
  
 자격 증명 협상이 포함된 Kerberos 프로토콜을 구현하려면 다음 단계를 수행합니다.  
  
1. <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A>을 <xref:System.Security.Principal.TokenImpersonationLevel.Delegation>으로 설정하여 위임을 구현합니다.  
  
2. SSPI 협상이 필요합니다.  
  
    1. 표준 바인딩을 사용하는 경우 `NegotiateServiceCredential` 속성을 `true`로 설정합니다.  
  
    2. 사용자 지정 바인딩을 사용하는 경우 `AuthenticationMode` 요소의 `Security` 속성을 `SspiNegotiated`로 설정합니다.  
  
3. NTLM 사용을 허용하지 않고 Kerberos를 사용하려면 SSPI 협상이 필요합니다.  
  
    1. `ChannelFactory.Credentials.Windows.AllowNtlm = false` 문과 함께 코드에서 이 작업을 수행합니다.  
  
    2. `allowNtlm` 특성을 `false`로 설정하여 구성 파일에서 이 작업을 수행할 수도 있습니다. 이 특성은 [ \<windows >](../../../../docs/framework/configure-apps/file-schema/wcf/windows-of-clientcredentials-element.md)에 포함 되어 있습니다.  
  
### <a name="ntlm-protocol"></a>NTLM 프로토콜  
  
#### <a name="negotiate-ssp-falls-back-to-ntlm-but-ntlm-is-disabled"></a>협상 SSP가 NTLM으로 대체되어도 NTLM을 사용하지 않도록 설정  
 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowNtlm%2A> 속성이 로`false`설정 되어 있어 NTLM이 사용 되는 경우 WCF (Windows Communication Foundation)에서 예외를 throw 하는 데 가장 적합 합니다. 이 속성을 `false`로 설정하면 유선을 통해 NTLM 자격 증명을 보낼 수 있습니다.  
  
 다음은 NTLM으로 대체되지 않도록 설정하는 방법을 보여 줍니다.  
  
 [!code-csharp[C_DebuggingWindowsAuth#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#4)]
 [!code-vb[C_DebuggingWindowsAuth#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#4)]  
  
#### <a name="ntlm-logon-fails"></a>NTLM 로그온 실패  
 클라이언트 자격 증명이 서비스에 유효하지 않습니다. 사용자 이름과 암호를 올바르게 설정했는지, 서비스를 실행하는 컴퓨터에서 인식하는 계정과 일치하는지 확인합니다. NTLM에서는 서비스의 컴퓨터에 로그온하기 위해 지정된 자격 증명을 사용합니다. 클라이언트를 실행하는 컴퓨터에서 유효한 자격 증명이라도 서비스의 컴퓨터에서 유효하지 않으면 로그온이 실패합니다.  
  
#### <a name="anonymous-ntlm-logon-occurs-but-anonymous-logons-are-disabled-by-default"></a>익명 NTLM 로그온을 수행해도 기본적으로 익명 로그온을 사용하지 않도록 설정  
 클라이언트를 만들 때 다음 예제에서처럼 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> 속성이 <xref:System.Security.Principal.TokenImpersonationLevel.Anonymous>로 설정되지만 기본적으로 서버에서 익명 로그온을 허용하지 않습니다. 이는 <xref:System.ServiceModel.Security.WindowsServiceCredential.AllowAnonymousLogons%2A> 클래스의 <xref:System.ServiceModel.Security.WindowsServiceCredential> 속성의 기본값이 `false`로 설정되기 때문에 발생합니다.  
  
 다음 클라이언트 코드에서는 익명 로그온을 사용하도록 설정합니다. 기본 속성은 `Identification`입니다.  
  
 [!code-csharp[C_DebuggingWindowsAuth#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#5)]
 [!code-vb[C_DebuggingWindowsAuth#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#5)]  
  
 다음 서비스 코드에서는 서버에서 익명 로그온을 사용하도록 기본값을 변경합니다.  
  
 [!code-csharp[C_DebuggingWindowsAuth#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#6)]
 [!code-vb[C_DebuggingWindowsAuth#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#6)]  
  
 가장에 대 한 자세한 내용은 [위임 및 가장](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)을 참조 하세요.  
  
 또는 기본 제공 계정인 SYSTEM을 사용하여 클라이언트를 Windows 서비스로 실행합니다.  
  
### <a name="other-problems"></a>기타 문제  
  
#### <a name="client-credentials-are-not-set-correctly"></a>클라이언트 자격 증명이 올바르게 설정되지 않음  
 Windows 인증에서는 <xref:System.ServiceModel.Security.WindowsClientCredential>을 사용하지 않고, <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 클래스의 <xref:System.ServiceModel.ClientBase%601> 속성에서 반환된 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential> 인스턴스를 사용합니다. 다음은 잘못된 예제입니다.  
  
 [!code-csharp[C_DebuggingWindowsAuth#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#2)]
 [!code-vb[C_DebuggingWindowsAuth#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#2)]  
  
 다음은 올바른 예제입니다.  
  
 [!code-csharp[C_DebuggingWindowsAuth#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#3)]
 [!code-vb[C_DebuggingWindowsAuth#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#3)]  
  
#### <a name="sspi-is-not-available"></a>SSPI를 사용할 수 없음  
 다음 운영 체제는 서버로 사용 되는 경우 Windows 인증을 지원 하지 않습니다. [!INCLUDE[wxp](../../../../includes/wxp-md.md)]Home edition, [!INCLUDE[wxp](../../../../includes/wxp-md.md)] Media Center edition 및 [!INCLUDE[wv](../../../../includes/wv-md.md)]home edition.  
  
#### <a name="developing-and-deploying-with-different-identities"></a>다른 ID로 개발 및 배포  
 애플리케이션을 한 컴퓨터에서 개발하여 다른 컴퓨터에 배포하고 서로 다른 계정 형식을 사용하여 각 컴퓨터에서 인증을 수행하면 동작이 동일하지 않을 수 있습니다. 예를 들어 `SSPI Negotiated` 인증 모드를 사용하여 Windows XP Pro 컴퓨터에서 애플리케이션을 개발할 경우 로컬 사용자 계정을 사용하여 인증하면 NTLM 프로토콜이 사용됩니다. 애플리케이션 개발을 마친 후 도메인 계정으로 실행되는 Windows Server 2003 컴퓨터에 해당 서비스를 배포하면 클라이언트에서는 Kerberos 및 도메인 컨트롤러를 사용할 것이므로 해당 서비스를 인증할 수 없습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Security.WindowsClientCredential>
- <xref:System.ServiceModel.Security.WindowsServiceCredential>
- <xref:System.ServiceModel.Security.WindowsClientCredential>
- <xref:System.ServiceModel.ClientBase%601>
- [위임 및 가장](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)
- [지원되지 않는 시나리오](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)
