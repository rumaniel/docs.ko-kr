---
title: HTTP 인증 이해
ms.date: 03/30/2017
ms.assetid: 9376309a-39e3-4819-b47b-a73982b57620
ms.openlocfilehash: ebfb5920fcd5c1a8faac8780dc1c32c92f9f6255
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614810"
---
# <a name="understanding-http-authentication"></a>HTTP 인증 이해
인증은 클라이언트가 리소스에 액세스할 자격이 있는지 여부를 식별하는 프로세스입니다. HTTP 프로토콜에서는 보안 리소스에 대한 액세스를 협상하기 위해 인증을 지원합니다.  
  
 일반적으로 클라이언트의 초기 요청은 익명 요청으로 인증 정보가 포함되어 있지 않습니다. HTTP 서버 애플리케이션은 인증이 필요함을 나타내는 동안 익명 요청을 거부할 수 있습니다. 서버 애플리케이션에서는 지원되는 인증 스키마를 나타내기 위해 WWW-Authentication 헤더를 보냅니다. 이 문서는 HTTP에 대 한 여러 인증 체계를 설명 하 고 지원을 Windows Communication Foundation (WCF)에서 설명 합니다.  
  
## <a name="http-authentication-schemes"></a>HTTP 인증 스키마  
 서버는 클라이언트에서 선택할 여러 인증 체계를 지정할 수 있습니다. 다음 표에서 Windows 응용 프로그램에서 흔히 발견 되는 인증 체계를 설명 합니다.  
  
|인증 스키마|설명|  
|---------------------------|-----------------|  
|Anonymous|익명 요청에는 인증 정보가 포함되어 있지 않습니다. 이는 모든 사용자에게 리소스에 대한 액세스 권한을 것과 같습니다.|  
|Basic|Basic 인증에서는 클라이언트의 사용자 이름 및 암호를 포함하는 Base64로 인코딩된 문자열을 보냅니다. Base64는 암호화 형식이 아니므로 사용자 이름 및 암호를 일반 텍스트로 보내는 것과 동일하다고 간주해야 합니다. 리소스를 보호해야 하는 경우 Basic 인증이 아닌 인증 스키마를 사용하는 것이 좋습니다.|  
|Digest|다이제스트 인증은 Basic 인증을 대체하기 위한 시도/응답 스키마입니다. 서버 라고 하는 임의 데이터의 문자열을 보냅니다를 *nonce* 을 시도로 클라이언트를 합니다. 클라이언트에서는 추가 정보 중에서 사용자 이름, 암호 및 nonce를 포함하는 해시를 사용하여 응답합니다. 이러한 교환 과정에서 발생하는 복잡성 및 데이터 해시 때문에 Digest 인증 스키마를 사용하는 사용자의 자격 증명을 도용하거나 재사용하기는 다른 경우보다 어렵습니다.<br /><br /> 다이제스트 인증의 경우 Windows 도메인 계정을 사용해야 합니다. 다이제스트 *영역* Windows 도메인 이름입니다. 따라서 Windows 도메인, Windows XP Home Edition과 같이 다이제스트 인증을 지원 하지 않는 운영 체제에서 실행 하는 서버를 사용할 수 없습니다. 반대로 Windows 도메인을 지원하지 않는 운영 체제에서 클라이언트를 실행하는 경우 인증하는 동안 도메인 계정을 명시적으로 지정해야 합니다.|  
|NTLM|NTLM(NT LAN Manager) 인증은 다이제스트 인증의 보다 안전한 변형인 시도/응답 스키마입니다. NTLM에서는 Windows 자격 증명을 사용하여 인코딩되지 않은 사용자 이름 및 암호 대신 시도 데이터를 변형합니다. NTLM 인증의 경우 클라이언트와 서버 간 다중 교환이 필요합니다. 서버 및 개입된 모든 프록시에서는 인증을 성공적으로 완료하기 위해 영구 연결을 지원해야 합니다.|  
|Negotiate|Negotiate 인증의 경우 사용 가능 여부에 따라 Kerberos 프로토콜 및 NTLM 인증 중 하나를 자동으로 선택합니다. Kerberos 프로토콜이 사용 가능하면 먼저 사용되고, 그렇지 않으면 NTLM이 사용됩니다. Kerberos 인증은 NTLM에 비해 크게 향상되었습니다. Kerberos 인증은 NTLM보다 빠르고, 상호 인증을 사용할 수 있으며 원격 시스템에 자격 증명을 위임할 수 있습니다.|  
|Windows Live ID|내부 Windows HTTP 서비스에는 페더레이션 프로토콜을 사용하는 인증이 포함되어 있습니다. 그러나 WCF에는 표준 HTTP 전송의 Microsoft Windows Live ID와 같은 페더레이션된 인증 스키마를 사용 하 여 지원 하지 않습니다. 현재 메시지 보안을 통해 이 기능을 사용할 수 있습니다. 자세한 내용은 [페더레이션 및 발급 된 토큰](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)합니다.|  
  
## <a name="choosing-an-authentication-scheme"></a>인증 스키마 선택  
 HTTP 서버의 잠재적 인증 스키마를 선택할 때 고려할 몇 가지 항목은 다음과 같습니다.  
  
- 리소스 보호가 필요한지 여부를 고려합니다. HTTP 인증을 사용하면 더 많은 데이터 전송이 필요하며 클라이언트와의 상호 운용성이 제한될 수 있습니다. 보호할 필요가 없는 리소스에 익명 액세스를 허용합니다.  
  
- 리소스 보호가 필요한 경우 필요한 보안 수준을 제공하는 인증 스키마를 고려합니다. 여기에서 설명한 가장 약한 표준 인증 스키마는 기본 인증입니다. 기본 인증에서는 사용자의 자격 증명이 보호되지 않습니다. 가장 강력한 표준 인증 스키마는 Negotiate 인증으로 Kerberos 프로토콜을 사용합니다.  
  
- 서버는 WWW-Authentication 헤더에 수락할 준비가 되지 않았거나 보호된 리소스를 제대로 보호하지 않는 스키마를 제공하면 안 됩니다. 클라이언트는 서버에서 제공하는 인증 스키마 중에서 자유롭게 선택할 수 있습니다. 일부 클라이언트는 기본적으로 약한 인증 스키마나 서버 목록의 첫 번째 인증 스키마를 사용합니다.  
  
## <a name="see-also"></a>참고자료

- [전송 보안 개요](../../../../docs/framework/wcf/feature-details/transport-security-overview.md)
- [전송 보안을 통해 가장 사용](../../../../docs/framework/wcf/feature-details/using-impersonation-with-transport-security.md)
- [위임 및 가장](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)
