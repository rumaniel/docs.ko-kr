---
title: 서비스 거부
ms.date: 03/30/2017
helpviewer_keywords:
- denial of service [WCF]
ms.assetid: dfb150f3-d598-4697-a5e6-6779e4f9b600
ms.openlocfilehash: f67a8b2977e84e24654b4b65c0cdd03bcbcb1b20
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968831"
---
# <a name="denial-of-service"></a>서비스 거부
서비스 거부는 시스템을 가득 채워 메시지를 처리할 수 없거나 메시지가 매우 느리게 처리되는 경우에 발생합니다.  
  
## <a name="excess-memory-consumption"></a>과도한 메모리 사용  
 고유 로컬 이름, 네임스페이스 또는 접두사를 많이 포함하는 XML 문서를 읽을 때 문제가 발생할 수 있습니다. <xref:System.Xml.XmlReader>에서 파생되는 클래스를 사용할 경우 각 항목에 대해 <xref:System.Xml.XmlReader.LocalName%2A>, <xref:System.Xml.XmlReader.Prefix%2A> 또는 <xref:System.Xml.XmlReader.NamespaceURI%2A> 속성을 호출하면 반환된 문자열이 <xref:System.Xml.NameTable>에 추가됩니다. <xref:System.Xml.NameTable>에 포함된 컬렉션은 크기가 줄지 않아 문자열 핸들의 가상 "메모리 누수"를 일으킵니다.  
  
 완화 방안은 다음과 같습니다.  
  
- <xref:System.Xml.NameTable> 클래스에서 파생되고 최대 크기 할당량을 적용합니다. 가득 찼을 때 <xref:System.Xml.NameTable> 사용을 금지하거나 <xref:System.Xml.NameTable>을 전환할 수 없습니다.  
  
- 가능한 경우 위에서 설명한 속성 대신 <xref:System.Xml.XmlReader.MoveToAttribute%2A> 메서드와 함께 <xref:System.Xml.XmlReader.IsStartElement%2A> 메서드를 사용합니다. 이러한 메서드는 문자열을 반환하지 않으므로 <xref:System.Xml.NameTable> 컬렉션이 과도하게 채워지지 않습니다.  
  
## <a name="malicious-client-sends-excessive-license-requests-to-service"></a>악의적인 클라이언트가 과도한 라이선스 요청을 서비스로 전송  
 악의적인 클라이언트가 과도한 라이선스 요청으로 서비스를 채우면 서버가 메모리를 지나치게 많이 사용할 수 있습니다.  
  
 완화: <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> 클래스의 다음 속성을 사용 합니다.  
  
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxCachedCookies%2A>: `SecurityContextToken` 또는 `SPNego` 협상 후에 서버에서 캐시하는 시간이 제한된 `SSL`의 최대 개수를 제어합니다.  
  
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.IssuedCookieLifetime%2A>: `SecurityContextTokens` 또는 `SPNego` 협상 후에 서버에서 발급하는 `SSL`의 수명을 제어합니다. 서버는 이 기간 동안 `SecurityContextToken`을 캐시합니다.  
  
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxPendingSessions%2A>: 서버에서 설정되었지만 애플리케이션 메시지가 처리되지 않은 보안 대화의 최대 개수를 제어합니다. 이 할당량은 클라이언트가 서비스에서 보안 대화를 설정할 수 없도록 하여 서비스가 클라이언트별 상태를 유지 관리하게 하지만 사용하지는 않습니다.  
  
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.InactivityTimeout%2A>: 서비스가 대화를 위해 클라이언트로부터 애플리케이션 메시지를 받지 않고 보안 대화를 활성 상태로 유지하는 최대 시간을 제어합니다. 이 할당량은 클라이언트가 서비스에서 보안 대화를 설정할 수 없도록 하여 서비스가 클라이언트별 상태를 유지 관리하게 하지만 사용하지는 않습니다.  
  
## <a name="wsdualhttpbinding-or-dual-custom-bindings-require-client-authentication"></a>WSDualHttpBinding 또는 이중 사용자 지정 바인딩에 클라이언트 인증이 필요함  
 기본적으로 <xref:System.ServiceModel.WSDualHttpBinding>은 보안을 사용합니다. 그러나 <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> 속성을 <xref:System.ServiceModel.MessageCredentialType.None>으로 설정하여 클라이언트 인증을 비활성화한 경우 악의적인 사용자가 제 3의 서비스에 대해 서비스 거부 공격을 발생시킬 수 있습니다. 이는 악의적인 클라이언트가 메시지 스트림을 제 3의 서비스로 보내도록 서비스에 지시할 수 있기 때문입니다.  
  
 이 문제를 완화하려면 속성을 `None`으로 설정하지 마세요. 또한 이중 메시지 패턴이 있는 사용자 지정 바인딩을 만들 때 이러한 가능성에 주의합니다.  
  
## <a name="auditing-event-log-can-be-filled"></a>감사 이벤트 로그가 채워질 수 있음  
 악의적인 사용자가 감사가 설정된 사실을 알고 있다면 잘못된 메시지를 보내 감사 항목이 기록되게 할 수 있습니다. 이런 식으로 감사 로그가 채워지면 감사 시스템이 실패합니다.  
  
 이 문제를 완화하려면 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> 속성을 `true`로 설정하고 이벤트 뷰어의 속성을 사용하여 감사 동작을 제어합니다. 이벤트 뷰어를 사용 하 여 이벤트 로그를 보고 관리 하는 방법에 대 한 자세한 내용은 [이벤트 뷰어](https://go.microsoft.com/fwlink/?LinkId=186123)을 참조 하십시오. 자세한 내용은 [감사](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)합니다.  
  
## <a name="invalid-implementations-of-iauthorizationpolicy-can-cause-service-to-become-unresponsive"></a>IAuthorizationPolicy의 구현이 잘못 된 경우 서비스가 응답 하지 않을 수 있습니다.  
 인터페이스의 잘못 된 구현에서 메서드를 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> 호출 하면 서비스가 응답 하지 않을 수 있습니다. <xref:System.IdentityModel.Policy.IAuthorizationPolicy>  
  
 완화: 신뢰할 수 있는 코드만 사용 합니다. 즉, 직접 작성하고 테스트한 코드나 신뢰할 수 있는 공급자가 제공한 코드만 사용합니다. 신뢰할 수 없는 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 확장이 적절한 고려 없이 코드에 연결할 수 없도록 합니다. 이 내용은 서비스 구현에 사용되는 모든 확장에 적용됩니다. WCF는 확장성 위치를 사용 하 여 연결 된 응용 프로그램 코드와 외부 코드를 구분 하지 않습니다.  
  
## <a name="kerberos-maximum-token-size-may-need-resizing"></a>Kerberos 최대 토큰 크기를 조정해야 할 수 있음  
 클라이언트는 다수의 그룹(실제 개수는 그룹에 따라 다를 수 있지만 대략 900개)에 속해 있지만 메시지 헤더의 블록이 64KB를 초과할 때 문제가 발생할 수 있습니다. 이 경우 Microsoft 지원 문서 "[IIS에 연결 하는 버퍼가 부족 하 여 Internet Explorer Kerberos 인증이 작동 하지](https://go.microsoft.com/fwlink/?LinkId=89176)않습니다." 문서에 설명 된 대로 최대 Kerberos 토큰 크기를 늘릴 수 있습니다. 큰 Kerberos 토큰을 수용 하기 위해 최대 WCF 메시지 크기를 늘려야 할 수도 있습니다.  
  
## <a name="autoenrollment-results-in-multiple-certificates-with-same-subject-name-for-machine"></a>자동 등록으로 인해 한 컴퓨터에 대해 동일한 주체 이름을 가진 여러 인증서가 발생함  
 자동 *등록* 은 인증서에 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 대 한 사용자 및 컴퓨터를 자동으로 등록 하는 기능입니다. 이 기능을 사용하는 도메인에 컴퓨터가 있으면 새 컴퓨터가 네트워크에 참가할 때마다 용도가 클라이언트 인증인 X.509 인증서가 자동으로 만들어지고 로컬 컴퓨터의 개인 인증서 저장소에 삽입됩니다. 그러나 자동 등록은 캐시에 만드는 모든 인증서에 대해 동일한 주체 이름을 사용합니다.  
  
 이 경우 WCF 서비스는 자동 등록을 사용 하 여 도메인에서 열지 못할 수 있습니다. 이 문제는 컴퓨터의 정규화된 DNS(Domain Name System) 이름을 포함하는 여러 인증서가 있어서 기본 서비스 X.509 자격 증명 검색 조건이 모호할 수 있기 때문에 발생합니다. 한 인증서는 자동 등록에서 시작되고 다른 인증서는 자체 서명된 인증서일 수 있습니다.  
  
 이를 완화 하려면 [ \<serviceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)에 대 한 보다 정확한 검색 조건을 사용 하 여 사용할 정확한 인증서를 참조 합니다. 예를 들어 <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint> 옵션을 사용하고 고유한 지문(해시)으로 인증서를 지정합니다.  
  
 자동 등록 기능에 대 한 자세한 내용은 [Windows Server 2003의 인증서 자동 등록](https://go.microsoft.com/fwlink/?LinkId=95166)을 참조 하세요.  
  
## <a name="last-of-multiple-alternative-subject-names-used-for-authorization"></a>권한 부여에 사용되는 여러 개의 대체 주체 이름 중 마지막  
 드물지만 X.509 인증서에 여러 개의 대체 주체 이름이 포함된 경우 대체 주체 이름을 사용하여 권한을 부여하면 권한 부여가 실패할 수도 있습니다.  
  
## <a name="protect-configuration-files-with-acls"></a>ACL을 사용하여 구성 파일 보호  
 코드 및 CardSpace 발급 된 토큰에 대 한 구성 파일에서 필수 및 선택적 클레임을 지정할 수 있습니다. 이로 인해 보안 토큰 서비스로 전송되는 `RequestSecurityToken` 메시지에 해당 요소가 내보내집니다. 공격자는 코드나 구성을 수정하여 필수 또는 선택적 클레임을 제거하고 보안 토큰 서비스가 대상 서비스에 대한 액세스를 허용하지 않는 토큰을 발급하게 할 수 있습니다.  
  
 완화: 구성 파일을 수정 하려면 컴퓨터에 액세스 해야 합니다. 파일 ACL(액세스 제어 목록)을 사용하여 구성 파일에 보안을 설정합니다. WCF를 사용 하려면 코드가 응용 프로그램 디렉터리 또는 전역 어셈블리 캐시에 있어야 해당 코드를 구성에서 로드할 수 있습니다. 디렉터리 ACL을 사용하여 디렉터리에 보안을 설정합니다.  
  
## <a name="maximum-number-of-secure-sessions-for-a-service-is-reached"></a>서비스에 허용되는 보안 세션의 최대 개수  
 서비스에서 성공적으로 클라이언트를 인증하고 서비스와의 보안 세션이 설정된 경우 서비스는 클라이언트가 세션을 취소하거나 세션이 만료될 때까지 세션을 추적합니다. 설정된 각 세션은 서비스에 대해 허용되는 동시 활성 세션의 최대 개수 제한에 계산됩니다. 이 제한에 도달하면 하나 이상의 활성 세션이 만료되거나 클라이언트에 의해 취소될 때까지 해당 서비스와 새 세션을 만들려고 시도하는 클라이언트가 거부됩니다. 클라이언트는 서비스와 여러 세션을 만들 수 있으며, 이러한 세션의 각각이 제한에 계산됩니다.  
  
> [!NOTE]
> 상태 저장 세션을 사용하는 경우 이전 단락의 내용이 적용되지 않습니다. 상태 저장 세션 [에 대 한 자세한 내용은 방법: 보안 세션](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)에 대 한 보안 컨텍스트 토큰을 만듭니다.  
  
 이 문제를 완화하려면 <xref:System.ServiceModel.Channels.SecurityBindingElement> 클래스의 <xref:System.ServiceModel.Channels.SecurityBindingElement> 속성을 설정하여 활성 세션의 최대 개수와 세션의 최대 수명에 대해 제한을 설정합니다.  
  
## <a name="see-also"></a>참고자료

- [보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)
- [정보 공개](../../../../docs/framework/wcf/feature-details/information-disclosure.md)
- [권한 상승](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)
- [서비스 거부](../../../../docs/framework/wcf/feature-details/denial-of-service.md)
- [재생 공격](../../../../docs/framework/wcf/feature-details/replay-attacks.md)
- [변조](../../../../docs/framework/wcf/feature-details/tampering.md)
- [지원되지 않는 시나리오](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)
