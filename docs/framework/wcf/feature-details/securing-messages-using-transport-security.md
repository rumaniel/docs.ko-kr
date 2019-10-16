---
title: 전송 보안을 사용하여 메시지에 보안 설정
ms.date: 03/30/2017
ms.assetid: 9029771a-097e-448a-a13a-55d2878330b8
ms.openlocfilehash: b0507590914e2e8cda7e5e599914a9e3d7b0acd0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69911714"
---
# <a name="securing-messages-using-transport-security"></a>전송 보안을 사용하여 메시지에 보안 설정
이 단원에서는 큐에 보내는 메시지를 보안 설정하는 데 사용할 수 있는 메시지 큐(MSMQ) 전송 보안에 대해 설명합니다.  
  
> [!NOTE]
> 이 항목을 읽기 전에 [보안 개념](../../../../docs/framework/wcf/feature-details/security-concepts.md)을 확인 하는 것이 좋습니다.  
  
 다음 그림에서는 Windows Communication Foundation (WCF)를 사용 하는 대기 중인 통신의 개념적 모델을 제공 합니다. 이 그림과 용어는 전송 보안 개념을 설명하는 데 사용됩니다.  
  
 ![대기 중인 응용 프로그램 다이어그램](../../../../docs/framework/wcf/feature-details/media/distributed-queue-figure.jpg "분산 큐-그림")  
  
 를 사용 하 여 wcf <xref:System.ServiceModel.NetMsmqBinding>를 사용 하 여 대기 중인 메시지를 보내는 경우 wcf 메시지는 MSMQ 메시지의 본문으로 연결 됩니다. 전송 보안은 MSMQ 메시지 전체(MSMQ 메시지 헤더 또는 속성 및 메시지 본문)에 대한 보안을 설정합니다. MSMQ 메시지의 본문 이기 때문에 전송 보안을 사용 하면 WCF 메시지도 보호 됩니다.  
  
 전송 보안의 주요 개념은 클라이언트가 대상 큐로 메시지를 가져오는 데 필요한 보안 요구 사항을 만족해야 한다는 것입니다. 이 개념은 메시지를 받는 애플리케이션에서 메시지가 보안되는 메시지 보안과는 다릅니다.  
  
 <xref:System.ServiceModel.NetMsmqBinding> 및 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>을 사용하는 전송 보안은 전송 큐 및 대상 큐 간의 전송 시 MSMQ 메시지가 보안되는 방법에 영향을 주며, 메시지 보안은 다음을 의미합니다.  
  
- 메시지가 훼손되지 않도록 메시지에 서명합니다.  
  
- 메시지가 보이지 않거나 훼손되지 않도록 메시지를 암호화합니다. 암호화하는 것이 좋지만 반드시 암호화할 필요는 없습니다.  
  
- 거부 방지를 위해 메시지를 보낸 사람을 식별하는 대상 큐 관리자입니다.  
  
 MSMQ에서 인증 여부와 관계없이 대상 큐에는 ACL(액세스 제어 목록)이 있어 클라이언트가 메시지를 대상 큐에 보낼 수 있는 권한이 있는지 여부를 확인합니다. 또한 대상 큐에서 메시지를 받을 수 있는 권한이 있는지 수신 애플리케이션을 확인합니다.  
  
## <a name="wcf-msmq-transport-security-properties"></a>WCF MSMQ 전송 보안 속성  
 MSMQ는 인증을 위해 Windows 보안을 사용합니다. Windows SID(보안 식별자)를 사용하여 클라이언트를 식별하고 클라이언트 인증 시 Active Directory 디렉터리 서비스를 인증 기관으로 사용합니다 이를 위해 MSMQ를 Active Directory 통합과 함께 설치해야 합니다. Windows 도메인 SID는 클라이언트를 식별하는 데 사용되므로 이 보안 옵션은 클라이언트와 서비스 모두 동일한 Windows 도메인의 일부인 경우에만 의미가 있습니다.  
  
 또한 MSMQ에서는 Active Directory에 등록되어 있지 않은 메시지와 함께 인증서를 첨부하는 기능을 제공합니다. 이 경우 첨부된 인증서를 사용하여 메시지가 서명되었는지 확인합니다.  
  
 WCF는 이러한 옵션을 MSMQ 전송 보안의 일부로 제공 하며 전송 보안에 대 한 키 피벗입니다.  
  
 기본적으로 전송 보안은 켜져 있습니다.  
  
 이를 바탕으로 다음 단원에서는 <xref:System.ServiceModel.NetMsmqBinding> 및 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>과 함께 제공되는 전송 보안 속성에 대해 설명합니다.  
  
#### <a name="msmq-authentication-mode"></a>MSMQ 인증 모드  
 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>는 메시지 보안을 위해 Windows 도메인 보안을 사용할지 또는 외부 인증서 기반 보안을 사용할지 명시적으로 지정합니다. 두 인증 모드에서 모두 WCF 대기 중인 전송 채널은 서비스 `CertificateValidationMode` 구성에 지정 된를 사용 합니다. 인증서 유효성 검사 모드에서는 인증서의 유효성을 확인하는 데 사용하는 메커니즘을 지정합니다.  
  
 전송 보안이 켜져 있는 경우 기본 설정은 <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain>입니다.  
  
#### <a name="windows-domain-authentication-mode"></a>Windows 도메인 인증 모드  
 Windows 보안을 사용하려면 Active Directory 통합이 필요합니다. <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain>은 기본 전송 보안 모드입니다. 이를 설정 하면 WCF 채널은 Windows SID를 MSMQ 메시지에 연결 하 고 Active Directory에서 가져온 내부 인증서를 사용 합니다. MSMQ에서는 메시지 보안을 위해 내부 인증서를 사용합니다. 수신 큐 관리자는 Active Directory를 사용하여 클라이언트를 인증하기 위해 일치하는 인증서를 검색하고, SID가 클라이언트의 인증서와 일치하는지도 확인합니다. `WindowsDomain` 인증 모드의 경우 내부에서 생성된 인증서, `Certificate` 인증 모드의 경우 외부에서 생성된 인증서가 메시지에 첨부되면 대상 큐가 필수 인증으로 표시되어 있지 않더라도 이 인증 단계가 실행됩니다.  
  
> [!NOTE]
> 큐를 만들 때 큐에 메시지를 보내는 클라이언트의 인증이 필요함을 나타내려면 큐를 인증된 큐로 표시할 수 있습니다. 이렇게 하면 인증되지 않은 메시지는 큐에서 수락하지 않습니다.  
  
 또한 메시지와 함께 첨부된 SID는 클라이언트가 큐에 메시지를 전송할 권한이 있는지 확인하기 위해 대상 큐의 ACL을 확인하는 데 사용됩니다.  
  
#### <a name="certificate-authentication-mode"></a>인증서 인증 모드  
 인증서 인증 모드를 사용하려면 Active Directory 통합이 필요하지 않습니다. 실제로 Active Directory 통합을 사용하지 않고 MSMQ를 작업 그룹 모드에 설치한 경우 또는 SRMP(SOAP Reliable Messaging Protocol) 전송 프로토콜을 사용하여 큐에 메시지를 전송하는 경우 <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate>만 작동합니다.  
  
 를 사용 <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate>하 여 wcf 메시지를 보낼 때 wcf 채널은 Windows SID를 MSMQ 메시지에 연결 하지 않습니다. 이런 경우 대상 큐 ACL에서는 큐에 메시지를 보낼 수 있도록 `Anonymous` 사용자 액세스 권한을 허용해야 합니다. 수신 큐 관리자는 인증서를 사용하여 MSMQ 메시지가 서명되었는지 여부를 확인하지만 인증을 수행하지는 않습니다.  
  
 클레임 및 id 정보를 포함 하는 인증서는 WCF의 <xref:System.ServiceModel.ServiceSecurityContext> 대기 중인 전송 채널을 통해에 채워집니다. 서비스는 이 정보를 사용하여 보낸 사람에 대한 고유한 인증을 수행합니다.  
  
### <a name="msmq-protection-level"></a>MSMQ 보호 수준  
 보호 수준은 MSMQ 메시지가 훼손되지 않도록 보호하는 방법을 명시적으로 지정합니다. 이 수준은 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> 속성에 지정되어 있습니다. 기본값은 <xref:System.Net.Security.ProtectionLevel.Sign>입니다.  
  
#### <a name="sign-protection-level"></a>서명 보호 수준  
 MSMQ 메시지는 `WindowsDomain` 인증 모드를 사용하는 경우 내부에서 생성된 인증서, `Certificate` 인증 모드를 사용하는 경우 외부에서 생성된 인증서를 사용하여 서명됩니다.  
  
#### <a name="sign-and-encrypt-protection-level"></a>서명 및 암호화 보호 수준  
 MSMQ 메시지는 `WindowsDomain` 인증 모드를 사용하는 경우 내부에서 생성된 인증서, `Certificate` 인증 모드를 사용하는 경우 외부에서 생성된 인증서를 사용하여 서명됩니다.  
  
 메시지 서명 외에 MSMQ 메시지는 인증서의 공개 키를 사용하여 암호화됩니다. 이 인증서는 대상 큐를 호스팅하는 수신 큐 관리자에 속한 Active Directory에서 가져옵니다. 전송 큐 관리자는 MSMQ 메시지가 전송 시 암호화되어 있는지 확인합니다. 수신 큐 관리자는 내부 인증서의 프라이빗 키를 사용하여 MSMQ 메시지를 해독하고, 인증되고 권한이 부여된 경우 일반 텍스트로 메시지를 큐에 저장합니다.  
  
> [!NOTE]
> 메시지를 암호화하려면 Active Directory 액세스가 필요하며(`UseActiveDirectory`의 <xref:System.ServiceModel.NetMsmqBinding> 속성이 `true`로 설정되어야 함), <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> 및 <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain>과 함께 사용할 수 있습니다.  
  
#### <a name="none-protection-level"></a>None 보호 수준  
 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>이 <xref:System.Net.Security.ProtectionLevel.None>으로 설정된 경우 이 수준으로 간주됩니다. 이 수준은 다른 인증 모드에서 유효한 값이 될 수 없습니다.  
  
> [!NOTE]
> MSMQ 메시지가 서명된 경우 MSMQ에서는 큐의 상태와 관계없이 즉, 인증된 큐인지 아닌지에 관계없이 메시지가 첨부된 내부 또는 외부 인증서를 사용하여 서명되었는지 여부를 확인합니다.  
  
### <a name="msmq-encryption-algorithm"></a>MSMQ 암호화 알고리즘  
 암호화 알고리즘은 통신 중에 MSMQ 메시지를 암호화하는 데 사용하는 알고리즘을 지정합니다. 이 속성은 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>이 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>로 설정되어 있을 경우에만 사용합니다.  
  
 지원되는 알고리즘은 `RC4Stream` 및 `AES`이며, 기본값은 `RC4Stream`입니다.  
  
 보낸 사람이 MSMQ 4.0을 설치한 경우에만 `AES` 알고리즘을 사용할 수 있습니다. 또한 대상 큐가 MSMQ 4.0에서 호스팅되어야 합니다.  
  
### <a name="msmq-hash-algorithm"></a>MSMQ 해시 알고리즘  
 해시 알고리즘은 MSMQ 메시지의 디지털 서명을 만드는 데 사용하는 알고리즘을 지정합니다. 수신 큐 관리자는 동일한 이 알고리즘을 사용하여 MSMQ 메시지를 인증합니다. <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>이 <xref:System.Net.Security.ProtectionLevel.Sign> 또는 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>으로 설정되어 있을 경우에만 이 속성을 사용합니다.  
  
 지원되는 알고리즘은 `MD5`, `SHA1`, `SHA256` 및 `SHA512`입니다. 기본값은 `SHA1`입니다.

 MD5/SHA1의 충돌 문제로 인해 s h a 1 이상을 권장 합니다.
  
## <a name="see-also"></a>참고자료

- [큐 개요](queues-overview.md)
- [보안 개념](../../../../docs/framework/wcf/feature-details/security-concepts.md)
- [서비스 및 클라이언트에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
