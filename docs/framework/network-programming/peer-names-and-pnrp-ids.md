---
title: 피어 이름 및 PNRP ID
ms.date: 03/30/2017
ms.assetid: afa538e8-948f-4a98-aa9f-305134004115
ms.openlocfilehash: d842c66de7550c94f4e287449a238ff964093fb2
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50187654"
---
# <a name="peer-names-and-pnrp-ids"></a>피어 이름 및 PNRP ID
피어 이름은 통신의 엔드포인트를 나타내며, 컴퓨터, 사용자, 그룹, 서비스 또는 IPv6 주소로 확인될 수 있는 피어와 연결된 모든 항목이 될 수 있습니다. 피어 이름 확인 프로토콜(PNRP)은 클라우드 멤버를 확인하는 데 사용되는 PNRP ID를 만드는 데 통계적으로 고유한 피어 이름을 사용합니다.  
  
## <a name="peer-names"></a>피어 이름  
 피어 이름은 보안되지 않음 또는 보안됨으로 등록될 수 있습니다. 보안되지 않은 이름은 단순한 텍스트 문자열로, 스푸핑이 가능하기 때문에 누구나 중복된 이름을 등록할 수 있습니다. 보안되지 않은 이름은 개인 네트워크 또는 보호되는 네트워크에 적합합니다. 반면 보안되는 이름은 인증서와 디지털 시그니처로 보호됩니다. 따라서 원래 게시자만 이 이름에 대한 소유권을 증명할 수 있습니다.  
  
 클라우드와 범위를 조합하면 PNRP 활동에 참여하는 피어를 위해 꽤 안전한 환경을 제공합니다. 그러나 보안 피어 이름을 사용해도 네트워킹 응용 프로그램의 전체적인 보안이 보장되지 않습니다. 응용 프로그램의 보안은 구현에 따라 다릅니다.  
  
 보안 피어 이름은 소유자만 등록할 수 있으며 공개 키 암호화를 통해 보호합니다. 보안 피어 이름은 대응하는 개인 키가 있는 피어 엔터티가 소유하는 것으로 간주됩니다. 소유권은 개인 키를 사용하여 서명되는 인증된 피어 주소(CPA)를 통해 입증할 수 있습니다. 악의적인 사용자는 해당 개인 키 없이도 피어 이름의 소유권을 위조할 수 있습니다.  
  
## <a name="pnrp-ids"></a>PNRP ID  
 ![PNRP ID](../../../docs/framework/network-programming/media/fdc9e8a0-4a1c-488d-a019-bc3a1973220c.gif "fdc9e8a0-4a1c-488d-a019-bc3a1973220c")  
  
 PNRP ID는 다음으로 구성됩니다.  
  
-   순위가 높은 128비트는 P2P(피어 투 피어) ID라고 하며 엔드포인트에 할당된 피어 이름의 해시입니다. 피어 이름의 형식은 *Authority.Classifier*입니다. 보안되는 이름의 경우, *Authority*는 16진수 문자 형식의 피어 이름 공개 키의 SHA1(Secure Hash Algorithm 1) 해시입니다. 보안되지 않는 이름의 경우 *Authority*는 단일 문자 “0”입니다. *분류자*는 응용 프로그램을 식별하는 문자열입니다. 피어 이름 분류자는 `null` 종결자를 포함하여 길이지 149자를 초과할 수 없습니다.  
  
-   순위가 낮은 128비트는 특정 클라우드에서 동일한 P2P ID의 여러 인스턴스를 식별하도록 생성된 수로 서비스 위치를 나타내는 데 사용됩니다.  
  
 이렇게 PNRP ID는 P2P ID와 서비스 위치가 조합된 형식이기 때문에 단일 컴퓨터에서 여러 PNRP ID를 등록할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.PeerToPeer.PeerName>  
 <xref:System.Net.PeerToPeer>
