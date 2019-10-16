---
title: 변조
ms.date: 03/30/2017
ms.assetid: 3bad93be-60bb-4f89-96ab-a1c3dc7c0fad
ms.openlocfilehash: 7a4265c30a6713f9557de2b3d1e99c87b7dd3e58
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61703389"
---
# <a name="tampering"></a>변조
*변조* 의도 된 것 이외의 목적을 위해 변경된 된 메시지를 사용 하 여 메시지 또는 메시지 배달 변경 하는 동작입니다.  
  
## <a name="do-not-disable-ws-addressing"></a>WS-Addressing 활성화  
 WS-Addressing 사양은 각 메시지에 대한 주소 헤더를 제공하여 메시지 받는 사람이 메시지를 보낸 사람을 확인할 수 있습니다. <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> 속성을 <xref:System.ServiceModel.Channels.AddressingVersion.None%2A>으로 설정하여 이 기능을 비활성화할 수 있습니다.  
  
 보안 모드를 메시지로 설정하는 경우 WS-Addressing을 사용하지 않도록 설정하면 공격자가 클라이언트에서 요청을 가져와 다른 서비스에 보낼 수 있으며 두 번째 서비스는 메시지가 원래 클라이언트에서 전송되었는지를 검색할 수 없습니다. 실제로 첫 번째 서비스는 두 번째 서비스와 통신할 때 클라이언트인 것처럼 가장할 수 있습니다.  
  
 이러한 문제를 줄이려면 <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> 속성을 <xref:System.ServiceModel.Channels.AddressingVersion.None%2A>으로 설정하지 않고 <xref:System.ServiceModel.Channels.MessageVersion> 속성을 <xref:System.ServiceModel.Channels.MessageVersion.Soap12%2A>로 설정하는 정적 <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> 속성과 같이 <xref:System.ServiceModel.Channels.AddressingVersion.None%2A>을 사용하지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)
- [정보 공개](../../../../docs/framework/wcf/feature-details/information-disclosure.md)
- [권한 상승](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)
- [서비스 거부](../../../../docs/framework/wcf/feature-details/denial-of-service.md)
- [지원되지 않는 시나리오](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)
- [재생 공격](../../../../docs/framework/wcf/feature-details/replay-attacks.md)
