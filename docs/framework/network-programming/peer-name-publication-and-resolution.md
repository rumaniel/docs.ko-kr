---
title: 피어 이름 게시 및 확인
ms.date: 03/30/2017
ms.assetid: f0370e08-9fa6-4ee5-ab78-9a58a20a7da2
ms.openlocfilehash: 4a0787972a61f5700d1e8728be96db8ef9ee749e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623197"
---
# <a name="peer-name-publication-and-resolution"></a>피어 이름 게시 및 확인

## <a name="publishing-a-peer-name"></a>피어 이름 게시  

 새 PNRP ID를 게시하기 위해 피어에서 다음을 수행합니다.  
  
- 캐시 내에서 인접해 있는 피어(캐시의 최하위 수준에 PNRP ID가 등록된 피어)에 PNRP 게시 메시지를 보내 자신의 캐시를 시드합니다.  
  
- 클라우드에서 인접해 있지 않은 임의 노드를 선택하고 PNRP 이름 확인 요청을 보내 해당 노드의 P2P ID를 확인합니다. 그 결과 수행되는 엔드포인트 확인 프로세스에서 클라우드에서 게시하는 피어의 PNRP ID를 가진 임의 노드의 캐시를 시드합니다.  
  
PNRP 버전 2 노드에서는 다른 P2P ID만 확인하는 경우 PNRP ID를 게시하지 않습니다. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\PeerNet\PNRP\IPV6-Global\SearchOnly=1 레지스트리 값(REG_DWORD 종류)은 피어에서 PNRP를 이름 확인에만 사용하고 이름 게시에는 사용하지 않도록 지정합니다. 이 레지스트리 값은 그룹 정책을 통해 구성할 수도 있습니다.  
  
## <a name="resolving-a-peer-name"></a>피어 이름 확인

 PNRP 네트워크 또는 클라우드에서 다른 피어를 찾는 것은 다음 두 단계로 구성된 프로세스입니다.  
  
1. 엔드포인트 확인  
  
2. PNRP ID 확인  
  
 엔드포인트 확인 단계에서 다른 컴퓨터에 있는 서비스의 PNRP ID를 확인하려는 피어가 해당 원격 피어의 IPv6 주소를 판별합니다.  원격 피어는 게시된 피어이거나 서비스 또는 컴퓨터의 PNRP ID와 연결됩니다.  
  
 원격 엔드포인트가 PNRP 클라우드에 등록되었음을 확인한 다음 PNRP ID 확인 단계의 요청 피어에서 원하는 서비스의 PNRP ID를 위해 해당 피어 엔드포인트에 요청을 보냅니다. 엔드포인트에서는 요청하는 피어에서 나중에 통신하는 데 사용할 수 있도록 서비스의 PNRP ID뿐만 아니라 설명 및 최대 4킬로바이트의 추가 정보가 포함된 응답을 보냅니다. 예를 들어 원하는 엔드포인트가 게임 서버인 경우 이러한 추가 피어 이름 레코드 데이터에는 게임, 플레이 레벨, 현재 플레이어 수 등의 정보가 포함될 수 있습니다.  
  
 엔드포인트를 확인하는 단계에서 PNRP는 반복 프로세스를 사용하여 PNRP ID를 게시한 노드를 찾습니다. 이 프로세스에서 확인 작업을 수행하는 노드는 대상 PNRP ID에 인접한 여러 노드를 연결하는 역할을 합니다.  
  
 PNRP에서 이름 확인 작업을 수행하려면 피어가 자체 캐시를 조사하여 대상 PNRP ID와 일치하는 항목을 찾아야 합니다. 이러한 항목이 발견되면 피어는 해당 피어에 PNRP 요청 메시지를 보내고 응답을 기다립니다. 해당 PNRP ID와 일치하는 항목이 없으면 피어는 PNRP ID가 대상 PNRP ID에 가장 근접한 항목에 해당하는 피어에 PNRP 요청 메시지를 보냅니다. PNRP 요청 메시지를 받은 노드는 자체 캐시를 조사하고 다음을 수행합니다.  
  
- PNRP ID가 있으면 요청받은 엔드포인트 피어가 요청한 피어에 직접 응답합니다.  
  
- 해당 PNRP ID가 없고 캐시에 대상 PNRP ID에 근접한 PNRP ID가 있으면 요청받은 피어가 요청한 피어에 대상 PNRP ID에 더 근접한 PNRP ID를 가진 항목에 해당하는 피어의 IPv6 주소가 포함된 응답을 보냅니다. 응답에서 IP 주소를 사용하면 요청 노드가 다른 PNRP 요청 메시지를 IPv6 주소에 전송하여 캐시를 검사하거나 응답합니다.  
  
- 해당 PNRP ID가 없고 캐시에 대상 PNRP ID에 근접한 PNRP ID도 없으면 요청받은 피어가 요청한 피어에 이러한 상황을 알리는 응답을 보냅니다. 그러면 요청한 피어는 다음으로 가장 근접한 PNRP ID를 선택합니다.  
  
요청한 피어는 이 프로세스를 연속적으로 반복하여 PNRP ID를 등록한 노드를 찾습니다.  
  
 <xref:System.Net.PeerToPeer> 네임스페이스에서 엔드포인트를 포함하는 <xref:System.Net.PeerToPeer.PeerName> 레코드 및 이와 통신하는 PNRP 클라우드 또는 메시 간에는 다대다 관계가 있습니다. 중복 항목 또는 오래된 항목이 있거나 피어 이름이 같은 노드가 여러 개인 경우 PNRP 노드에서는 <xref:System.Net.PeerToPeer.PeerNameResolver> 클래스를 사용하여 최신 정보를 가져올 수 있습니다. <xref:System.Net.PeerToPeer.PeerNameResolver> 메서드에서는 단일 피어 이름을 사용하여 큐브 뷰를 하나의 피어 대 여러 피어 이름 레코드 및 마찬가지로 한 피어 대 여러 클라우드로 간소화합니다. 관계형 테이블 조인을 사용한 쿼리와 비슷합니다. 성공적으로 완료되면 확인자 개체에서 지정된 피어 이름에 대해 <xref:System.Net.PeerToPeer.PeerNameRecordCollection>을 반환합니다.  예를 들어 피어 이름은 컬렉션의 모든 피어 이름 레코드에 표시되며 클라우드별로 순서가 지정됩니다. PNRP 기반 애플리케이션에서 요청할 수 있는 지원 데이터가 있는 피어 이름의 인스턴스입니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Net.PeerToPeer>
