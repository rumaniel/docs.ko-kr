---
title: PNRP 클라우드
ms.date: 03/30/2017
ms.assetid: a82e2bf1-62ab-4c2d-83f3-3217a6aead2e
ms.openlocfilehash: 22401459a183d8d21e37211d942b24dbc76a6f94
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50195361"
---
# <a name="pnrp-clouds"></a>PNRP 클라우드
PNRP “클라우드”는 네트워크를 통해 서로 통신할 수 있는 노드 집합을 나타냅니다. “클라우드”라는 용어는 “피어 메시” 및 “피어 투 피어 그래프”와 동의어입니다.  
  
 노드 간 통신은 한 클라우드에서 다른 클라우드로 전달되지 않습니다. <xref:System.Net.PeerToPeer.Cloud> 인스턴스는 대소문자를 구분하는 이름으로 고유하게 식별됩니다. 단일 피어 또는 노드는 두 개 이상의 클라우드에 연결될 수 있습니다.  
  
 클라우드는 네트워크 인터페이스와 매우 밀접하게 연결됩니다.  두 개의 네트워크 카드가 여러 다른 서브넷에 연결되어 있는 다중 홈 컴퓨터에서는 세 개의 클라우드가 반환됩니다. 즉, 인터페이스별 링크 로컬 주소당 하나씩 반환되고 단일 글로벌 범위 클라우드용으로 하나가 반환됩니다.  
  
 PNRP에서는 3개의 클라우드 “범위”를 사용합니다. 여기서 범위는 서로 찾을 수 있는 컴퓨터 그룹입니다.  
  
-   글로벌 클라우드는 글로벌 IPv6 주소 범위 및 글로벌 주소에 해당하며 전체 IPv6 인터넷상의 모든 컴퓨터를 나타냅니다. 글로벌 클라우드는 하나만 존재합니다.  
  
-   링크-로컬 클라우드는 링크 로컬 IPv6 주소 범위 및 링크-로컬 주소에 해당합니다. 링크-로컬 클라우드는 특정 링크에 사용되는데 일반적으로 이러한 링크는 로컬로 연결된 서브넷과 같습니다. 링크 로컬 클라우드의 경우 여러 개가 존재할 수 있습니다.  
  
 세 번째로 사이트별 클라우드가 있는데 이는 사이트 IPv6 주소 범위 및 사이트 로컬 주소에 해당합니다. 이 클라우드는 더 이상 사용되지 않지만 PNRP에서는 아직 지원됩니다.  
  
## <a name="clouds"></a>클라우드  
 PNRP 클라우드는 <xref:System.Net.PeerToPeer.Cloud> 클래스의 인스턴스로 표시됩니다. 피어를 사용하는 클라우드 그룹은 열거형 <xref:System.Net.PeerToPeer.CloudCollection> 클래스의 인스턴스로 표시됩니다. 현재 피어에 알려진 PNRP 클라우드 컬렉션은 정적 <xref:System.Net.PeerToPeer.Cloud.GetAvailableClouds%2A> 메서드를 호출하여 얻을 수 있습니다.  
  
 개별 클라우드에는 고유한 이름이 있으며 256자 유니코드 문자열로 표시됩니다. 이러한 이름을 위에 언급된 범위와 함께 사용하여 클라우드 클래스의 고유한 인스턴스를 구성합니다. 이러한 인스턴스는 직렬화할 수 있으며 영구적으로 사용하기 위해 재구성할 수 있습니다.  
  
 클라우드 인스턴스를 만들거나 가져오고 나면 피어 이름을 등록하여 알려진 피어의 메시를 만들 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.PeerToPeer.Cloud>  
 [피어 이름 확인 프로토콜](../../../docs/framework/network-programming/peer-name-resolution-protocol.md)
