---
title: WCF에서 이벤트 로깅
ms.date: 03/30/2017
helpviewer_keywords:
- event logging [WCF]
ms.assetid: aac0530d-f44c-45a1-bada-e30e0677b41f
ms.openlocfilehash: 0c74b93be026007a5593372c938cf73e08fafb15
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797803"
---
# <a name="event-logging-in-wcf"></a>WCF에서 이벤트 로깅
WCF (Windows Communication Foundation)는 Windows 이벤트 로그의 내부 이벤트를 추적 합니다.  
  
## <a name="viewing-event-logs"></a>이벤트 로그 보기  
 이벤트 로깅은 기본적으로 활성화되며 비활성화 메커니즘이 없습니다. 이벤트 뷰어를 사용 하 여 WCF에 의해 기록 된 이벤트를 볼 수 있습니다. 이 도구를 시작 하려면 **시작**, **제어판**을 차례로 클릭 하 고 **관리 도구**를 두 번 클릭 한 다음 **이벤트 뷰어**를 두 번 클릭 합니다.  
  
### <a name="application-event-log"></a>응용 프로그램 이벤트 로그  
 **응용 프로그램 이벤트 로그** 에는 WCF에 의해 생성 된 대부분의 이벤트가 포함 됩니다. 대부분의 항목은 애플리케이션에서 특정 기능을 시작하지 못한 것을 나타냅니다. 예를 들어 다음과 같습니다.  
  
- 메시지 로깅/추적: WCF는 추적 및 메시지 로깅이 실패할 때 이벤트 로그에 이벤트를 기록 합니다. 그러나 모든 추적 실패가 이벤트를 트리거하는 것은 아닙니다. 이벤트 로그가 추적 실패로 완전히 채워지지 않도록 WCF는 이러한 이벤트에 대해 10 분의 블랙 아웃 기간을 구현 합니다. 즉, WCF가 이벤트 로그에 추적 실패를 기록 하는 경우 10 분 이상 동안 다시 수행 하지 않습니다.  
  
- 공유 수신기: WCF TCP 포트 공유 서비스는 시작 하지 못할 때 이벤트를 기록 합니다.  
  
- CardSpace 서비스가 시작 되지 않을 때 이벤트를 로깅합니다.  
  
- 시작 실패 또는 크래시 등의 위험 및 오류 이벤트  
  
- 메시지 로깅 설정: 메시지 로깅이 설정 된 경우 이벤트를 로깅합니다. 이는 관리자에게 중요한 애플리케이션 관련 정보가 메시지 헤더 및 본문에 기록될 수 있다는 것을 알리기 위해서입니다.  
  
- `enableLoggingKnownPII` 파일의 `machineSettings` 요소에서 `machine.config` 특성이 설정되면 이벤트가 기록됩니다. 이 특성에서는 시스템에서 실행 중인 애플리케이션 중 알려진 PII(개인적으로 식별할 수 있는 정보)의 로그가 허용되는 것이 있는지 여부를 지정합니다.  
  
- 특정 애플리케이션에 대해 `logKnownPii` 또는 `app.config` 파일에서 `web.config` 특성이 PII 로깅을 켜도록 `true`로 설정되어 있지만 `enableLoggingKnownPII` 파일의 `machineSettings` 요소에 있는 `machine.config` 특성이 `false`로 설정되어 있으면 이벤트가 기록됩니다. 또한 `logKnownPii` 및 `enableLoggingKnownPII`가 모두 `true`로 설정되어 있으면 이벤트가 기록됩니다. 이러한 구성 설정에 대 한 자세한 내용은 [메시지 로깅 구성](../configuring-message-logging.md) 항목의 보안 섹션을 참조 하세요.  
  
### <a name="security-event-log"></a>보안 이벤트 로그  
 **보안 이벤트 로그** 에는 WCF에서 기록 하는 보안 감사 이벤트가 포함 됩니다.  
  
### <a name="system-event-log"></a>시스템 이벤트 로그  
 WCF는 **시스템 이벤트 로그**에 아무것도 기록 하지 않습니다.  
  
### <a name="event-log-entries"></a>이벤트 로그 항목  
 이벤트의 **소스** 는 로그 항목을 생성 하는 어셈블리의 이름입니다.  
  
 이벤트 로그 항목의 형식은 이벤트의 심각도를 나타내는 데 사용됩니다. 각 이벤트는 애플리케이션에서 이벤트를 보고할 때 나타내는 단일 형식이어야 합니다. 이벤트 뷰어는 이 형식을 사용하여 로그의 목록 보기에 표시할 아이콘을 결정합니다. 이벤트 로그 항목의 다른 이벤트 형식은 <xref:System.Diagnostics.EventLogEntryType>을 참조하십시오.  
  
 이벤트 뷰어에서 이벤트를 볼 때 "추가 정보"를 클릭 하면 이벤트 뷰어 인터넷을 통해 정보를 보낼 수 있습니다. 자세한 내용은 이벤트 뷰어 도움말을 참조하십시오.  
  
## <a name="see-also"></a>참고자료

- [관리 및 진단](../index.md)
- [이벤트 일반 참조](events-general-reference.md)
