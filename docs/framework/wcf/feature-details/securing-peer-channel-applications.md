---
title: 피어 채널 애플리케이션 보안
ms.date: 03/30/2017
ms.assetid: d4a0311d-3f78-4525-9c4b-5c93c4492f28
ms.openlocfilehash: 4b52e0476ce6ac54a2e4a3a8cfceb112d662186b
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959879"
---
# <a name="securing-peer-channel-applications"></a>피어 채널 애플리케이션 보안
WinFX, 다른 바인딩과 마찬가지로 `NetPeerTcpBinding` 보안이 기본적으로 활성화 되어 있고 모두 전송 및 메시지 기반 보안 (또는 둘 다)를 제공 합니다. 이 항목에서는 이러한 두 가지 보안 형식에 대해 설명합니다. 보안 형식은 바인딩 사양의 보안 모드 태그(<xref:System.ServiceModel.NetPeerTcpBinding.Security%2A>`Mode`)로 지정됩니다.  
  
## <a name="transport-based-security"></a>전송 기반 보안  
 피어 채널은 전송 보안을 위한 두 가지 형식의 인증 자격 증명을 지원하며, 두 형식에서 모두 연결된 `ClientCredentialSettings.Peer`의 `ChannelFactory` 속성을 설정해야 합니다.  
  
- 암호입니다. 클라이언트는 암호를 사용하여 연결을 인증합니다. 이 자격 증명 형식을 사용하는 경우 `ClientCredentialSettings.Peer.MeshPassword`에 올바른 암호와 선택적으로 `X509Certificate2` 인스턴스가 있어야 합니다.  
  
- 인증서. 특정 애플리케이션 인증이 사용됩니다. 이 자격 증명 형식을 사용하는 경우 <xref:System.IdentityModel.Selectors.X509CertificateValidator>에서 `ClientCredentialSettings.Peer.PeerAuthentication`의 구체적 구현을 사용해야 합니다.  
  
## <a name="message-based-security"></a>메시지 기반 보안  
 애플리케이션은 메시지 보안을 사용하여 보내는 메시지에 서명할 수 있습니다. 이 경우 모든 수신 당사자는 메시지가 신뢰할 수 있는 당사자에 의해 전송되었으며 메시지가 변조되지 않았음을 확인할 수 있습니다. 현재 피어 채널은 X.509 자격 증명 메시지 서명만 지원합니다.  
  
## <a name="best-practices"></a>모범 사례  
  
- 이 단원에서는 피어 채널 애플리케이션에 보안을 설정하는 최선의 방법에 대해 설명합니다.  
  
### <a name="enable-security-with-peer-channel-applications"></a>피어 채널 애플리케이션을 사용하여 보안 설정  
 피어 채널 프로토콜의 분산 특성 때문에 보안되지 않은 메시에서는 메시 멤버 자격, 기밀성 및 개인 정보를 적용하기 어렵습니다. 또한 클라이언트와 확인자 서비스 간에 통신 보안을 설정하는 것이 중요합니다. PNRP(Peer Name Resolution Protocol)에서 보안 이름을 사용하여 스푸핑 및 다른 일반적인 공격을 방지합니다. 메시지 및 전송 기반 보안을 비롯하여 클라이언트가 확인자 서비스에 연결하는 데 사용하는 연결에 보안을 설정하여 사용자 지정 확인자 서비스에 보안을 설정합니다.  
  
### <a name="use-the-strongest-possible-security-model"></a>가장 강력한 보안 모델 사용  
 예를 들어 메시의 각 멤버를 개별적으로 식별해야 하는 경우 인증서 기반 인증 모델을 사용합니다. 사용할 수 없는 경우 현재 권장 사항에 따라 암호 기반 인증을 사용하여 보안을 유지합니다. 여기에는 신뢰할 수 있는 당사자하고만 암호 공유, 보안 매체를 사용하여 암호 전송, 자주 암호 변경, 강력한 암호(8자 이상으로 대/소문자의 한 문자 이상, 숫자 및 특수 문자 포함) 사용이 포함됩니다.  
  
### <a name="never-accept-self-signed-certificates"></a>자체 서명된 인증서 허용 안 함  
 주체 이름을 기반으로 인증서 자격 증명을 허용하지 마세요. 누구든지 인증서를 만들 수 있으며 누구든지 유효성이 확인되는 이름을 선택할 수 있습니다. 스푸핑을 방지하려면 발급 기관 자격 증명(신뢰할 수 있는 발급자 또는 루트 인증 기관)을 기반으로 인증서의 유효성을 검사합니다.  
  
### <a name="use-message-authentication"></a>메시지 인증 사용  
 메시지 인증을 사용하여 신뢰할 수 있는 소스에서 메시지가 시작되었으며 전송 중에 메시지를 변조한 사람이 없음을 확인할 수 있습니다. 메시지 인증을 사용하지 않으면 악성 클라이언트가 메시의 메시지를 쉽게 스푸핑하거나 변조할 수 있습니다.  
  
## <a name="peer-channel-code-examples"></a>피어 채널 코드 예제  
 [피어 채널 시나리오](../../../../docs/framework/wcf/feature-details/peer-channel-scenarios.md)  
  
## <a name="see-also"></a>참고자료

- [피어 채널 보안](../../../../docs/framework/wcf/feature-details/peer-channel-security.md)
- [피어 채널 응용 프로그램 빌드](../../../../docs/framework/wcf/feature-details/building-a-peer-channel-application.md)
