---
title: CLR ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- CLR ETW events
- ETW, common language runtime
- ETW, CLR events
ms.assetid: ef2b31c3-7426-43e7-9924-92339b96556d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6798a83973f94f07a2a215d5208aa55f0f9ae929
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046742"
---
# <a name="clr-etw-events"></a>CLR ETW 이벤트
이 섹션의 항목은 ETW(Windows용 이벤트 추적) 이벤트를 설명합니다. 각 이벤트에는 연결된 키워드 및 수준이 있으며, [CLR ETW 키워드 및 수준](clr-etw-keywords-and-levels.md) 항목에서 설명합니다. CLR에는 이벤트에 대한 두 개의 공급자가 있습니다.  
  
- 런타임 공급자 - 사용하도록 설정된 키워드(이벤트 범주)에 따라 이벤트를 발생시킵니다. CLR 런타임 공급자 GUID는 e13c0d23-ccbc-4e12-931b-d9cc2eee27e4입니다.  
  
- 런다운 공급자 - 특별한 용도로 사용됩니다. CLR 런다운 공급자 GUID는 a669021c-c450-4609-a035-5af59af4df18입니다.  
  
 공급자에 대한 자세한 내용은 [CLR ETW 공급자](clr-etw-providers.md)를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [런타임 정보 이벤트](runtime-information-etw-events.md)  
 SKU, 버전 번호, 런타임이 활성화된 방법, 시작하는 데 사용된 명령줄 매개 변수, GUID(해당되는 경우) 및 다른 관련 정보를 비롯한 런타임 관련 정보를 캡처합니다.  
  
 [예외가 throw된 V1 이벤트](exception-thrown-v1-etw-event.md)  
 throw된 예외에 대한 정보를 캡처합니다.  
  
 [경합 이벤트](contention-etw-events.md)  
 런타임이 사용하는 모니터 잠금이나 네이티브 잠금의 경합에 대한 정보를 캡처합니다.  
  
 [스레드 풀 이벤트](thread-pool-etw-events.md)  
 작업자 스레드 풀 및 I/O 스레드 풀에 대한 정보를 캡처합니다.  
  
 [로더 이벤트](loader-etw-events.md)  
 애플리케이션 도메인, 어셈블리 및 모듈 로딩 및 언로딩에 대한 정보를 캡처합니다.  
  
 [메서드 이벤트](method-etw-events.md)  
 기호 확인을 위한 CLR 메서드에 대한 정보를 캡처합니다.  
  
 [가비지 수집 이벤트](garbage-collection-etw-events.md)  
 진단 및 디버깅에 도움이 되는 가비지 수집 관련 정보를 캡처합니다.  
  
 [JIT 추적 이벤트](jit-tracing-etw-events.md)  
 JIT(Just-In-Time) 인라인 및 후속 호출에 대한 정보를 캡처합니다.  
  
 [Interop 이벤트](interop-etw-events.md)  
 MSIL(Microsoft intermediate language) 스텁 생성 및 캐싱에 대한 정보를 캡처합니다.  
  
 [ARM 이벤트](application-domain-resource-monitoring-arm-etw-events.md)  
 애플리케이션 도메인의 상태에 대한 세부적인 진단 정보를 캡처합니다.  
  
 [보안 이벤트](security-etw-events.md)  
 강력한 이름 및 Authenticode 확인에 대한 정보를 캡처합니다.  
  
 [스택 이벤트](stack-etw-event.md)  
 이벤트가 발생한 이후 스택 추적을 생성하기 위해 다른 이벤트와 함께 사용되는 정보를 캡처합니다.  
  
## <a name="see-also"></a>참고자료

- [ETW를 사용한 디버깅 및 성능 조정 개선](https://go.microsoft.com/fwlink/?LinkId=179696)
- [Windows 성능 블로그](https://go.microsoft.com/fwlink/?LinkId=179509)
- [.NET Framework 로깅 제어](controlling-logging.md)
- [CLR ETW 공급자](clr-etw-providers.md)
- [CLR ETW 키워드 및 수준](clr-etw-keywords-and-levels.md)
- [공용 언어 런타임의 ETW 이벤트](etw-events-in-the-common-language-runtime.md)
