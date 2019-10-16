---
title: 사용자 지정 바인딩을 사용하는 보안 기능
ms.date: 03/30/2017
ms.assetid: a2425679-484a-4e6c-9c98-7da7304f1516
ms.openlocfilehash: 25d203fa706eeb0d0ccf1eaf4367ffa5bd7b83aa
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61990927"
---
# <a name="security-capabilities-with-custom-bindings"></a>사용자 지정 바인딩을 사용하는 보안 기능
시스템에서 제공되는 바인딩 중 하나를 사용하여 일반적으로 사용되는 보안 작업을 수행할 수 있습니다. 하지만 좀더 제어가 필요한 경우에는 이 항목의 설명에 따라 <xref:System.ServiceModel.Channels.SecurityBindingElement>를 사용하여 사용자 지정 바인딩을 만들 수도 있습니다. 사용자 지정 바인딩에 대 한 자세한 내용은 참조 하세요. [사용자 지정 바인딩을](../../../../docs/framework/wcf/extending/custom-bindings.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SecurityBindingElement 인증 모드](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)  
 사용자 지정 바인딩에서 가능한 인증 모드에 대해 설명합니다.  
  
 [방법: SecurityBindingElement를 사용 하 여 사용자 지정 바인딩 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 보안 요소로 사용자 지정 바인딩을 만드는 기본 단계에 대해 설명합니다.  
  
 [방법: 지정된 된 인증 모드에 대 한 SecurityBindingElement 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)  
 지정된 인증 모드의 보안 요소를 만드는 방법에 대해 설명합니다.  
  
 [방법: WSFederationHttpBinding에서 보안 세션을 사용 하지 않도록 설정](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 페더레이션 서비스를 만드는 경우 보안 세션을 비활성화하는 방법에 대해 설명합니다.  
  
 [방법: 메시지 재생 검색 사용](../../../../docs/framework/wcf/feature-details/how-to-enable-message-replay-detection.md)  
 재생 공격이 발생한 경우를 확인하는 방법에 대해 설명합니다.  
  
 [방법: 지원 자격 증명 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-supporting-credential.md)  
 필요한 경우 서비스에 지원하는 자격 증명을 제공하는 방법에 대해 설명합니다.  
  
 [방법: 서명 확인 설정](../../../../docs/framework/wcf/feature-details/how-to-set-up-a-signature-confirmation.md)  
 메시지에 디지털 서명을 할 때 서명을 확인하는 단계에 대해 설명합니다.  
  
 [방법: 최대 클럭 오차 설정](../../../../docs/framework/wcf/feature-details/how-to-set-a-max-clock-skew.md)  
 서비스와 클라이언트 사이에서 최대로 허용되는 시간 차이를 설정하는 방법에 대해 설명합니다.  
  
 [방법: 디지털 서명의 암호화를 사용 하지 않도록 설정](../../../../docs/framework/wcf/feature-details/how-to-disable-encryption-of-digital-signatures.md)  
 디지털 서명의 암호화를 비활성화할 경우 얻을 수 있는 성능 상의 이점에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>  
  
 [\<security>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)  
  
## <a name="related-sections"></a>관련 단원  
 [보호 수준 이해](../../../../docs/framework/wcf/understanding-protection-level.md)  
  
 [서비스 및 클라이언트에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)  
  
## <a name="see-also"></a>참고자료

- [바인딩 및 보안](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)
- [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [시스템 제공 바인딩](../../../../docs/framework/wcf/system-provided-bindings.md)
