---
title: IPv6 자동 구성
ms.date: 03/30/2017
ms.assetid: 581c1d21-1013-43a3-bf3e-2d9ead62b79c
ms.openlocfilehash: 31aaebaefa0d2682ee20ae93496aff42ae1633d8
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199138"
---
# <a name="ipv6-auto-configuration"></a>IPv6 자동 구성
IPv6의 중요한 목표 중 하나는 노드 플러그 앤 플레이를 지원하는 것입니다. 즉, 노드를 IPv6 네트워크에 플러그하여 사용자가 개입하지 않고 자동으로 구성되도록 해야 합니다.  
  
## <a name="type-of-auto-configuration"></a>자동 구성 형식  
 IPv6에서는 다음과 같은 형식의 자동 구성을 지원합니다.  
  
-   **상태 저장 자동 구성**. 노드 설치 및 관리를 위해 DHCPv6(Dynamic Host Configuration Protocol for IPv6) 서버가 필요하므로 이러한 형식의 구성에는 일정 수준의 사용자 개입이 필요합니다. DHCPv6 서버에서는 구성 정보를 제공하는 노드 목록을 유지합니다. 또한 각 주소를 사용하는 기간 및 재할당이 가능한 시기를 서버에서 알 수 있도록 상태 정보도 유지합니다.  
  
-   **상태 비저장 자동 구성**. 이 구성 형식은 소규모 조직 및 개인이 사용하기에 적합합니다. 이 경우 각 호스트에서는 수신된 라우터 알림의 콘텐츠를 통해 해당 주소를 판별합니다. IEEE EUI-64 표준을 사용하여 주소의 네트워크 ID 부분을 정의하면 링크에서 호스트 주소가 고유하다고 가정할 수 있습니다.  
  
 주소를 결정하는 방법에 관계없이 노드에서 잠재적인 주소가 로컬 링크에 고유한지 확인해야 합니다. 이 작업은 잠재적 주소에 네트워크 환경 요청 메시지를 전송하여 수행합니다. 노드에서 응답을 받으면 주소가 이미 사용 중이므로 다른 주소를 판별해야 합니다.  
  
## <a name="ipv6-mobility"></a>IPv6 이동성  
 모바일 장치가 확산됨에 따라 새로운 요구 사항이 제기되었습니다. 장치에서 IPv6 인터넷의 위치를 임의로 변경하고 기존 연결은 여전히 유지할 수 있어야 합니다. 이 기능을 제공하기 위해 모바일 노드에 언제나 도달할 수 있는 홈 주소가 할당됩니다. 모바일 노드가 홈에 있으면 홈 링크에 연결하고 홈 주소를 사용합니다. 모바일 노드가 항상 홈 외부에 있으면 일반적으로 라우터인 홈 에이전트에서 모바일 노드 및 이 노드와 통신하는 노드 간에 메시지를 릴레이합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터넷 프로토콜 버전 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)  
 [소켓](../../../docs/framework/network-programming/sockets.md)
