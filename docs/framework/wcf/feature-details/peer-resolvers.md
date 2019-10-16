---
title: 피어 확인자
ms.date: 03/30/2017
ms.assetid: d86d12a1-7358-450f-9727-b6afb95adb9c
ms.openlocfilehash: 0547bb37b03235c61f43cec365551438f7931ad1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69909922"
---
# <a name="peer-resolvers"></a>피어 확인자
메시에 연결하려면 피어 노드에 다른 노드의 IP 주소가 필요합니다. IP 주소를 가져오려면 메시 ID를 사용하고 해당 메시 ID로 등록된 노드에 해당하는 주소 목록을 반환하는 확인자 서비스에 연결합니다. 확인자는 메시의 각 노드가 서비스에 등록되게 하여 만드는 등록된 주소 목록을 유지합니다.  
  
 `Resolver`의 <xref:System.ServiceModel.NetPeerTcpBinding> 속성을 통해 사용할 PeerResolver 서비스를 지정할 수 있습니다.  
  
## <a name="supported-peer-resolvers"></a>지원되는 피어 확인자  
 피어 채널은 두 가지 유형의 해결 프로그램을 지원 합니다. PNRP (피어 이름 확인 프로토콜) 및 사용자 지정 해결 프로그램 서비스입니다.  
  
 기본적으로 피어 채널은 PNRP 피어 확인자 서비스를 사용하여 메시의 피어 및 인접한 환경을 검색합니다. PNRP를 사용할 수 없거나 적절 하지 않은 상황/플랫폼의 경우 WCF (Windows Communication Foundation)는 서버 기반 검색 서비스인를 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>제공 합니다. <xref:System.ServiceModel.PeerResolvers.IPeerResolverContract> 인터페이스를 구현하는 클래스를 작성하여 사용자 지정 확인자 서비스를 명시적으로 정의할 수도 있습니다.  
  
### <a name="peer-name-resolution-protocol-pnrp"></a>PNRP(피어 이름 확인 프로토콜)  
 [!INCLUDE[wv](../../../../includes/wv-md.md)]의 기본 확인자인 PNRP는 서버가 없는 분산 이름 확인자 서비스입니다. 고급 네트워킹 팩을 설치하여 [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)]에서 PNRP를 사용할 수도 있습니다. 동일한 버전의 PNRP를 실행하는 두 개의 클라이언트는 개입하는 회사 방화벽 없음 등 특정 조건을 만족할 경우 이 프로토콜을 사용하여 서로를 찾을 수 있습니다. [!INCLUDE[wv](../../../../includes/wv-md.md)]에 포함된 PNRP 버전이 고급 네트워킹 팩에 포함된 버전보다 최신 버전입니다. Microsoft 다운로드 센터에서 [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)]용 PNRP 업데이트를 확인하세요.  
  
### <a name="custom-resolver-services"></a>사용자 지정 확인자 서비스  
 PNRP 서비스를 사용할 수 없거나 메시 형성을 완벽하게 제어하려면 서버 기반의 사용자 지정 확인자 서비스를 사용합니다. 이 서비스는 <xref:System.ServiceModel.PeerResolvers.IPeerResolverContract> 인터페이스를 구현하는 확인자 클래스를 작성하거나 Windows 제공 기본 구현인 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>를 사용하여 명시적으로 정의할 수 있습니다.  
  
 서비스의 기본 구현에서 클라이언트가 명시적으로 등록을 새로 고치지 않을 경우 클라이언트 등록은 특정 시간 후에 만료됩니다. 확인자 서비스를 사용하는 클라이언트가 시간 내에 등록을 새로 고치려면 클라이언트 서버 대기 시간의 상한을 고려해야 합니다. 이 경우 확인자 서비스에서 적절한 새로 고침 시간 제한(`RefreshInterval`)을 선택해야 합니다. 자세한 내용은 CustomPeerResolverService 내에서을 [참조 하세요. 클라이언트 등록](../../../../docs/framework/wcf/feature-details/inside-the-custompeerresolverservice-client-registrations.md))  
  
 애플리케이션 작성기에서 클라이언트와 사용자 지정 확인자 서비스 간의 연결에 보안을 설정해야 합니다. 이렇게 하려면 클라이언트가 확인자 서비스에 연결하는 데 사용하는 <xref:System.ServiceModel.NetTcpBinding>의 보안 설정을 사용합니다. 피어 채널을 만드는 데 사용되는 `ChannelFactory`에 자격 증명(사용하는 경우)을 지정해야 합니다. 이러한 자격 증명은 사용자 지정 확인자에 대한 채널을 만드는 데 사용되는 `ChannelFactory`에 전달됩니다.  
  
> [!NOTE]
> 로컬 및 임시 네트워크에 사용자 지정 확인자를 사용하는 경우 링크-로컬 또는 임시 네트워크를 사용하거나 지원하는 애플리케이션이 연결 시 사용할 단일 링크-로컬 주소를 선택하는 논리를 포함하는 것이 좋습니다. 이렇게 하면 여러 개의 링크-로컬 주소가 있는 컴퓨터로 인해 발생하는 혼동을 방지할 수 있습니다. 이에 따라 피어 채널은 한 번에 하나의 링크-로컬 주소 사용만 지원합니다. `ListenIpAddress`의 <xref:System.ServiceModel.NetPeerTcpBinding> 속성을 사용하여 이 주소를 지정할 수 있습니다.  
  
 사용자 지정 해결 프로그램을 구현 하는 방법에 대 한 데모는 [피어 채널 사용자 지정 피어 확인자](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751466(v=vs.90))를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [CustomPeerResolverService 내에서: 클라이언트 등록](../../../../docs/framework/wcf/feature-details/inside-the-custompeerresolverservice-client-registrations.md)  
  
## <a name="see-also"></a>참고자료

- [피어 채널 개념](../../../../docs/framework/wcf/feature-details/peer-channel-concepts.md)
- [피어 채널 보안](../../../../docs/framework/wcf/feature-details/peer-channel-security.md)
- [피어 채널 응용 프로그램 빌드](../../../../docs/framework/wcf/feature-details/building-a-peer-channel-application.md)
