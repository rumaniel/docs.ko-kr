---
title: 보안 개요-WCF
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, security
- WCF, security
ms.assetid: f478c80d-792d-4e7a-96bd-a2ff0b6f65f9
ms.openlocfilehash: ae03684449e902c0d05744a19671169f2e0b8be2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69949351"
---
# <a name="windows-communication-foundation-security-overview"></a>Windows Communication Foundation 보안 개요
WCF (Windows Communication Foundation)는 SOAP 메시지 기반의 분산 프로그래밍 플랫폼 이며, 클라이언트와 서비스 간의 메시지 보안은 데이터를 보호 하는 데 필요 합니다. WCF는 기존 보안 인프라와 SOAP 메시지에 대해 인식 되는 보안 표준을 기반으로 보안 메시지를 교환 하기 위한 다양 하 고 상호 운용할 수 있는 플랫폼을 제공 합니다.  
  
> [!NOTE]
> WCF 보안에 대 한 포괄적인 가이드는 [Wcf 보안 지침](https://go.microsoft.com/fwlink/?LinkID=158912)을 참조 하세요.  
  
 WCF는 HTTPS, Windows 통합 보안, 사용자 이름 및 암호와 같은 기존 기술을 사용 하 여 보안 분산 응용 프로그램을 구축 하 여 사용자를 인증 하는 경우 익숙한 개념을 사용 합니다. WCF는 기존 보안 인프라와 통합 될 뿐 아니라 보안 SOAP 메시지를 사용 하 여 Windows 전용 도메인 이상의 분산 보안도 확장 합니다. 기존 프로토콜을 비롯 하 여 SOAP를 프로토콜로 사용 하는 주요 이점을 활용 하 여 기존 보안 메커니즘을 구현 하는 것이 좋습니다. 예를 들어, 사용자 이름과 암호 또는 X.509 인증서와 같이 클라이언트 또는 서비스를 식별하는 자격 증명에는 상호 운용성 있는 XML 기반 SOAP 프로필이 있습니다. 이러한 프로필을 사용하면 XML 디지털 서명 및 XML 암호화와 같은 개방형 규격을 활용하여 메시지가 안전하게 교환됩니다. 사양 목록은 [시스템 제공 상호 운용성 바인딩에서 지 원하는 웹 서비스 프로토콜](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)을 참조 하세요.  
  
 또 다른 예로 보안 분산 애플리케이션을 가능하게 하는 Windows 플랫폼의 COM(구성 요소 개체 모델)을 들 수 있습니다. COM에는 구성 요소 간에 보안 컨텍스트를 이동할 수 있는 포괄적인 보안 메커니즘이 있습니다. 이 메커니즘은 무결성, 기밀성 및 인증을 적용합니다. 그러나 COM은 WCF와 같은 플랫폼 간 보안 메시징을 사용 하도록 설정 하지 않습니다. WCF를 사용 하면 인터넷을 통해 Windows 도메인에서 확장 되는 서비스 및 클라이언트를 빌드할 수 있습니다. WCF의 상호 운용 가능한 메시지는 사용자의 정보 보안을 확실히 파악 하는 데 도움이 되는 동적인 비즈니스 중심 서비스를 구축 하는 데 필수적입니다.  
  
## <a name="windows-communication-foundation-security-benefits"></a>Windows Communication Foundation 보안 이점  
 WCF는 SOAP 메시지를 기반으로 하는 분산 프로그래밍 플랫폼입니다. WCF를 사용 하 여 서비스 및 서비스 클라이언트 역할을 하는 응용 프로그램을 만들 수 있으며, 다른 서비스와 클라이언트를 무제한으로 만들고 처리할 수 있습니다. 이러한 분산 애플리케이션에서는 메시지가 방화벽, 인터넷 및 수많은 SOAP 매개자를 통해 노드 간에 이동할 수 있으므로 다양한 메시지 보안 위협에 노출됩니다. 다음 예에서는 WCF 보안이 엔터티 간에 메시지를 교환할 때 완화 하는 데 도움이 되는 몇 가지 일반적인 위협을 보여 줍니다.  
  
- 네트워크 트래픽을 관찰하여 중요한 정보 입수. 예를 들어, 온라인 뱅킹 시나리오에서 클라이언트가 계좌 간에 자금 이체를 요청합니다. 악의적인 사용자가 이 메시지를 가로채서 계좌 번호와 암호를 입수하고 나중에 보안되지 않는 계좌로부터 자금 이체를 수행합니다.  
  
- 클라이언트가 알아채지 못하게 서비스로 작동하는 악의적인 엔터티. 이 시나리오에서는 악의적인 사용자가 온라인 서비스로 작동하여 클라이언트가 보낸 메시지를 가로채서 중요한 정보를 입수합니다. 그런 다음 이 훔친 데이터를 사용하여 손상된 계좌로부터 자금을 이체합니다. 이 공격은 *피싱 공격*에도 알려져 있습니다.  
  
- 메시지를 변경하여 호출자가 의도한 것과 다른 결과 생성. 예를 들어, 예금이 들어오는 계좌 번호를 변경하여 자금이 악의적인 계좌로 이체되도록 할 수 있습니다.  
  
- 불법 해커가 동일한 구매 주문서를 재생하는 해커 재생. 예를 들어, 온라인 서점에서 수백 건의 주문을 받고 주문하지 않은 고객에게 책을 보냅니다.  
  
- 서비스가 클라이언트를 인증할 수 없음. 이 경우 서비스는 해당 당사자가 거래를 수행했는지 확인할 수 없습니다.  
  
 요약하면 전송 보안은 다음을 보증합니다.  
  
- 서비스 엔드포인트(응답자) 인증  
  
- 클라이언트 주체(개시자) 인증  
  
- 메시지 무결성  
  
- 메시지 기밀성  
  
- 재생 검색  
  
### <a name="integration-with-existing-security-infrastructures"></a>기존 보안 인프라와 통합  
 종종 웹 서비스 배포에서는 SSL(Secure Sockets Layer) 또는 Kerberos 프로토콜과 같은 기존 보안 솔루션을 그대로 사용합니다. Active Directory를 사용하는 Windows 도메인과 같이 이미 배포된 보안 인프라를 활용하는 경우도 있습니다. 이러한 기존 기술과 통합하는 동시에 새로운 기술을 평가하고 채택해야 할 수도 있습니다.  
  
 WCF 보안은 기존 전송 보안 모델과 통합 되며, SOAP 메시지 보안을 기반으로 하는 새로운 전송 보안 모델에 기존 인프라를 활용할 수 있습니다.  
  
### <a name="integration-with-existing-authentication-models"></a>기존 인증 모델과 통합  
 통신 보안 모델의 중요한 부분은 통신 중인 엔터티를 식별하여 인증할 수 있는 기능입니다. 이러한 통신 중인 엔터티는 "디지털 ID" 즉, 자격 증명을 사용하여 통신 상대에게 자신을 인증합니다. 분산 통신 플랫폼이 발전함에 따라 다양한 자격 증명 인증 및 관련 보안 모델이 구현되었습니다. 예를 들어, 인터넷에서는 일반적으로 사용자 이름과 암호를 사용하여 사용자를 식별합니다. 인트라넷에서는 Kerberos 도메인 컨트롤러를 사용하여 사용자 및 서비스 인증을 지원하는 것이 일반적입니다. 두 비즈니스 파트너 사이와 같은 특정 시나리오에서는 인증서를 사용하여 파트너를 상호 인증할 수 있습니다.  
  
 따라서 동일한 서비스가 내부 회사 고객뿐 아니라 외부 파트너 또는 인터넷 고객에게 노출될 수 있는 웹 서비스에서는 인프라가 이러한 기존 보안 인증 모델과의 통합을 제공하는 것이 중요합니다. WCF 보안은 다음과 같은 다양 한 자격 증명 유형 (인증 모델)을 지원 합니다.  
  
- 익명 호출자  
  
- 사용자 이름 클라이언트 자격 증명  
  
- 인증서 클라이언트 자격 증명  
  
- Windows(Kerberos 프로토콜 및 NTLM[NT LanMan])  
  
### <a name="standards-and-interoperability"></a>표준 및 상호 운용성  
 기존의 대규모 배포에서는 동기종 환경을 유지하는 경우가 극히 드뭅니다. 분산 컴퓨팅/통신 플랫폼은 다른 공급업체에서 제공하는 기술과 상호 운용되어야 합니다. 마찬가지로 보안 역시 상호 운용 가능해야 합니다.  
  
 상호 운용 가능한 보안 시스템을 지원하기 위해 웹 서비스 업계 기업들은 다양한 표준을 작성하고 있습니다. 특히 보안과 관련 하 여 몇 가지 주목할 만한 표준을 제안 했습니다. WS-SECURITY: SOAP 메시지 보안 (OASIS 표준 본문 및 이전의 WS-SECURITY로 알려짐), WS-TRUST, Ws-secureconversation 및 WS-Ws-securitypolicy.  
  
 WCF는 다양 한 상호 운용성 시나리오를 지원 합니다. <xref:System.ServiceModel.BasicHttpBinding> 클래스는 BSP(기본 보안 프로필)를 대상으로 하고 <xref:System.ServiceModel.WSHttpBinding> 클래스는 WS-Security 1.1 및 WS-SecureConversation과 같은 최신 보안 표준을 대상으로 합니다. 이러한 표준을 준수 하 여 WCF 보안은 Microsoft Windows 이외의 운영 체제 및 플랫폼에서 호스팅되는 웹 서비스와 상호 운용 하 고 통합할 수 있습니다.  
  
## <a name="wcf-security-functional-areas"></a>WCF 보안 기능 영역  
 WCF 보안은 전송 보안, 액세스 제어 및 감사의 세 가지 기능 영역으로 구분 됩니다. 다음 단원에서는 이러한 영역에 대해 간략하게 설명하고 추가 정보를 위한 링크를 제공합니다.  
  
### <a name="transfer-security"></a>전송 보안  
 전송 보안은 무결성, 기밀성 및 인증의 세 가지 주요 보안 기능을 포함합니다. *무결성* 은 메시지가 변조 되었는지 여부를 검색할 수 있는 기능입니다. *기밀성* 은 의도 된 받는 사람이 아닌 다른 사람이 메시지를 읽을 수 없도록 하는 기능입니다. 이는 암호화를 통해 달성 됩니다. *인증은* 요청 된 id를 확인할 수 있는 기능입니다. 이러한 세 기능을 함께 사용하면 메시지를 지점 간에 안전하게 전달할 수 있습니다.  
  
#### <a name="transport-and-message-security-modes"></a>전송 및 메시지 보안 모드  
 WCF에서 전송 보안을 구현 하는 데는 *전송* 보안 모드와 *메시지* 보안 모드의 두 가지 기본 메커니즘이 사용 됩니다.  
  
- *전송 보안 모드* 에서는 HTTPS와 같은 전송 수준 프로토콜을 사용 하 여 전송 보안을 구현 합니다. 전송 모드는 광범위하게 채택되고, 다양한 플랫폼에서 사용 가능하며, 계산 과정이 복잡하지 않다는 이점이 있는 한편 지점 간 메시지의 보안만 유지할 수 있다는 단점이 있습니다.  
  
- 반면에 *메시지 보안 모드*는 ws-security (및 기타 사양)를 사용 하 여 전송 보안을 구현 합니다. 메시지 보안은 SOAP 메시지에 직접 적용되고 SOAP 봉투에 애플리케이션 데이터와 함께 포함되기 때문에 전송 프로토콜에 독립적이고, 확장성이 뛰어나며, 엔드투엔드 보안(지점 간과 비교)을 보장한다는 이점이 있습니다. 반면 SOAP 메시지의 XML 특성을 처리해야 하기 때문에 전송 보안 모드보다 몇 배 더 느리다는 단점이 있습니다.  
  
 이러한 차이점에 대 한 자세한 내용은 [서비스 및 클라이언트 보안](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)설정을 참조 하세요.  
  
 세 번째 보안 모드는 위 두 가지 모드를 모두 사용하며 두 모드의 이점을 모두 갖추고 있습니다. 이 모드를 `TransportWithMessageCredential`이라고 합니다. 이 모드에서는 클라이언트를 인증하는 데 메시지 보안을 사용하고 서버를 인증하고 메시지 기밀성과 무결성을 제공하는 데 전송 보안을 사용합니다. 이로 인해 `TransportWithMessageCredential` 보안 모드는 전송 보안 모드만큼 빠른 속도를 제공하면서 메시지 보안과 같은 방식으로 클라이언트 인증 확장성을 지원합니다. 반면 메시지 보안 모드와는 달리 완벽한 엔드투엔드 보안은 제공하지 않습니다.  
  
### <a name="access-control"></a>Access Control  
 *액세스 제어* 를 권한 부여 라고도 합니다. *권한 부여* 를 통해 서로 다른 사용자가 데이터를 볼 수 있는 권한을 가질 수 있습니다. 예를 들어, 회사의 인사 관리 파일에는 중요한 직원 데이터가 들어 있기 때문에 관리자만 직원 데이터를 볼 수 있습니다. 또한 관리자는 자신이 관리하는 부하 직원에 대한 데이터만 볼 수 있습니다. 이 경우 액세스 제어는 역할("관리자")뿐 아니라 관리자의 특정 ID에 기반하므로 관리자는 다른 관리자의 직원 레코드를 볼 수 없습니다.  
  
 WCF에서 액세스 제어 기능은 CLR (공용 언어 런타임) <xref:System.Security.Permissions.PrincipalPermissionAttribute> 과의 통합 및 *id 모델*이라는 api 집합을 통해 제공 됩니다. 액세스 제어 및 클레임 기반 권한 부여에 대 한 자세한 내용은 [보안 확장](../../../../docs/framework/wcf/extending/extending-security.md)을 참조 하세요.  
  
### <a name="auditing"></a>감사  
 *감사* 는 Windows 이벤트 로그에 보안 이벤트를 기록 하는 것입니다. 인증 실패 또는 성공과 같은 보안 관련 이벤트를 기록할 수 있습니다. 자세한 내용은 [감사](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)합니다. 프로그래밍에 대 한 자세한 [내용은 방법: 보안 이벤트](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)를 감사 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Security.Permissions.PrincipalPermissionAttribute>
- [서비스에 보안 설정](../../../../docs/framework/wcf/securing-services.md)
- [일반적인 보안 시나리오](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)
- [바인딩 및 보안](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)
- [서비스 및 클라이언트에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
- [인증](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)
- [권한 부여](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)
- [페더레이션 및 발급된 토큰](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)
- [감사](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)
- [보안 지침 및 최선의 방법](../../../../docs/framework/wcf/feature-details/security-guidance-and-best-practices.md)
- [구성 파일을 사용하여 서비스 구성](../../../../docs/framework/wcf/configuring-services-using-configuration-files.md)
- [시스템 제공 바인딩](../../../../docs/framework/wcf/system-provided-bindings.md)
- [엔드포인트 만들기 개요](../../../../docs/framework/wcf/endpoint-creation-overview.md)
- [보안 확장](../../../../docs/framework/wcf/extending/extending-security.md)
- [Windows Server Fabric 용 보안 모델](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
