---
title: 응용 프로그램 개발의 PNRP
ms.date: 03/30/2017
ms.assetid: 265615d6-4423-4b5d-8626-752e456f4f4e
ms.openlocfilehash: b19138c43185f4d31bef4fe67af48f89dc03eba4
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50180435"
---
# <a name="pnrp-in-application-development"></a>응용 프로그램 개발의 PNRP
Windows Vista에서 네트워킹 응용 프로그램은 단순화된 PNRP API(응용 프로그래밍 인터페이스)를 통해 PNRP 이름 게시 및 확인 기능에 액세스할 수 있습니다.  
  
## <a name="implementing-the-peer-name-resolution-protocol"></a>피어 이름 확인 프로토콜의 구현  
 간소화된 PNRP API를 사용하면 이름과 주소를 등록하도록 클라우드가 명시적으로 지정되지 않습니다. PNRP 구성 요소를 통해 조인하는 데 적절한 클라우드와 클라우드에서 게시할 주소를 자동으로 결정합니다.  
  
 Windows Vista에서 상당히 단순화된 형태의 PNRP 이름 확인 기능의 경우 PNRP 이름이 getaddrinfo() Windows 소켓 함수에 통합되었습니다. 따라서 응용 프로그램이 PNRP를 이용하여 IPv6 주소에 해당하는 이름을 확인할 때 getaddrinfo() 함수를 사용하여 FQDN(정규화된 도메인 이름) name.prnp.net(여기서 name은 확인할 피어 이름)을 확인할 수 있습니다. pnrp.net 도메인은 Windows Vista에서 PNRP 이름 확인에 사용하도록 예약된 도메인입니다.  
  
 PeerToPeer 응용 프로그램 간에 전달되는 메시지는 여전히 PeerChannel 및 WCF [대형 데이터 및 스트리밍](https://go.microsoft.com/fwlink/?LinkID=179652) 등의 기본 아키텍처에서 처리합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.PeerToPeer>
