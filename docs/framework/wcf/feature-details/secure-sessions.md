---
title: 보안 세션
ms.date: 03/30/2017
ms.assetid: 7b50602f-d7b5-42e9-8e92-1f0413df0d8b
ms.openlocfilehash: d511a45d990e441c5dcfd8405794ec937c0278d1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966064"
---
# <a name="secure-sessions"></a>보안 세션
WCF (Windows Communication Foundation) 기능은 메시지가 전송 된 순서 대로 수신 되도록 보장 하는 신뢰할 수 있는 세션입니다. 이 단원의 항목에서는 신뢰할 수 있는 세션을 만들 때 고려해야 할 보안 관련 문제에 대해 설명합니다. 신뢰할 수 있는 세션에 대 한 자세한 내용은 [세션 사용](../../../../docs/framework/wcf/using-sessions.md)을 참조 하세요.  
  
> [!NOTE]
> Windows XP에서 가장이 필요한 경우 상태 저장 SCT(보안 컨텍스트 토큰) 없이 보안 세션을 사용합니다. 상태 저장 SCT가 가장과 함께 사용되는 경우 <xref:System.InvalidOperationException>이 throw됩니다. 자세한 내용은 [지원 되지 않는 시나리오](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|||  
|-|-|  
|[보안 대화 및 보안 세션](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md)|보안 대화 및 보안 세션은 동의어입니다. 이 항목에서는 보안 대화가 작동하는 방식과 패턴을 사용하는 시기와 이유에 대해 설명합니다.|  
|[방법: 보안 세션 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-secure-session.md)|기본적인 보안 세션 만들기에 대해 설명합니다.|  
|[방법: 보안 세션에 대 한 보안 컨텍스트 토큰 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)|클라이언트로 상태 및 세션을 관리할 웹 팜을 만드는 단계에 대해 설명합니다.|  
|[보안 세션에 대한 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-secure-sessions.md)|보안 세션에 대해 고려할 사항에 대해 설명합니다.|  
  
## <a name="reference"></a>참조  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
## <a name="related-sections"></a>관련 단원  
 [세션, 인스턴스 및 동시성](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)  
  
 [서비스 디자인 및 구현](../../../../docs/framework/wcf/designing-and-implementing-services.md)  
  
## <a name="see-also"></a>참고자료

- [방법: 메시지 재생 검색 사용](../../../../docs/framework/wcf/feature-details/how-to-enable-message-replay-detection.md)
- [재생 공격](../../../../docs/framework/wcf/feature-details/replay-attacks.md)
- [방법: 세션이 필요한 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)
