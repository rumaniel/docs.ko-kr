---
title: 동작 ID 전파
ms.date: 03/30/2017
ms.assetid: cd1c1ae5-cc8a-4f51-90c9-f7b476bcfe70
ms.openlocfilehash: 642d4da49f90d3fc6f2b0dfc9896d724acb075b5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651814"
---
# <a name="activity-id-propagation"></a>동작 ID 전파
ServiceModel 동작 추적을 사용하면 ServiceModel 동작을 통해 전파가 발생하고, ServiceModel 동작 추적을 사용하지 않으면 사용자 간에 전파가 발생합니다.  
  
## <a name="servicemodel-activity-tracing-is-enabled"></a>ServiceModel 동작 추적 사용  
 ServiceModel ActivityTracing을 사용하면 ProcessAction 동작 간에 전파가 발생합니다.  
  
### <a name="server"></a>서버  
 경우는 `propagateActivity` 특성이로 설정 된 `true` 클라이언트와 서버 ID입니다 합니다 `ProcessAction` 서버에서 작업 id는 전파에 동일 `ActivityId` 메시지 헤더입니다.  
  
 없는 경우 `ActivityId` 헤더를 메시지에 (즉, `propagateActivity` = `false` 클라이언트에서), 때나 `propagateActivity` = `false` 서버에서 서버 생성 하는 새 활동 id입니다.  
  
### <a name="client"></a>클라이언트  
 클라이언트가 동기 단일 스레드인 경우 클라이언트는 클라이언트나 서버의 `propagateActivity` 설정을 모두 무시합니다. 대신 요청 동작에서 응답이 처리됩니다. 클라이언트가 비동기 또는 동기 경우, 다중 스레드 `propagateActivity` = `true` 클라이언트에서 및 동작 ID 헤더를 서버에서 보낸 메시지에는 클라이언트에서 메시지에서 동작 ID를 검색 하 고 전송 합니다 전파 된 활동 ID를 포함 하는 Action 동작 처리 그렇지 않으면 클라이언트는 Process Message 동작에서 새 Process Action 동작으로 전송합니다. 새 Process Action 동작으로의 이 추가 전송은 일관성을 위해 수행됩니다. 이 동작 내에서 클라이언트는 응답 메시지 처리를 위해 스레드가 할당될 때 로컬 스레드 컨텍스트에서 BeginCall 동작의 동작 ID를 검색합니다. 그런 다음 초기 Process Action 동작으로 전송합니다.  
  
 클라이언트가 이중이면 메시지를 수신할 때 클라이언트가 서버 역할을 합니다.  
  
### <a name="propagation-in-fault-messages"></a>오류 메시지의 전파  
 올바른 메시지와 오류 메시지의 처리에는 차이가 없습니다. 하는 경우 `propagateActivity` = `true`, SOAP 오류 메시지 헤더에 추가 된 동작 ID가 앰비언트 동작과 동일 합니다.  
  
## <a name="servicemodel-activity-tracing-is-disabled"></a>ServiceModel 동작 추적 사용 안 함  
 ServiceModel ActivityTracing을 사용하지 않으면 ServiceModel 동작을 거치지 않고 직접 사용자 코드 동작 간에 전파가 발생합니다. 사용자 정의 동작 ID도 메시지 동작 ID 헤더를 통해 전파됩니다.  
  
 하는 경우 `propagateActivity` = `true` 하 고 `ActivityTracing` = `off` ServiceModel 추적 수신기 (에 관계 없이 여부 ServiceModel 추적을 활성화)에 대 한 다음 클라이언트 또는 서버에서 발생 합니다.  
  
- 작업 요청 또는 응답 전송 시 메시지가 구성될 때까지 TLS의 동작 ID가 사용자 코드에서 전파됩니다. 메시지가 전송되기 전에 동작 ID 헤더도 메시지에 삽입됩니다.  
  
- 요청이나 응답을 받을 때 수신된 메시지 개체를 만드는 즉시 메시지 헤더에서 동작 ID가 검색됩니다. TLS의 동작 ID는 사용자 코드에 도달할 때까지 메시지가 범위에서 사라지는 즉시 전파됩니다.  
  
 이러한 작업은 전파가 설정된 경우 사용자 추적이 동일한 동작에 나타나도록 합니다. 그러나 ServiceModel 추적의 경우는 다릅니다. ServiceModel 추적은 사용자 코드 동작이 설정된 스레드와 동일한 스레드에서 추적 처리가 실행되는 경우에만 사용자 코드 동작에서 발생합니다.  
  
 일반적으로 ServiceModel 추적은 다음 위치에서 확인할 수 있습니다.  
  
- ServiceModel 추적을 사용하지 않으면 내보낸 모든 추적이 사용자 동작에 나타납니다. 서버와 클라이언트에서 모두 전파를 사용하는 경우 이러한 추적이 동일한 동작에 있습니다.  
  
- ServiceModel 추적을 사용하지만 ActivityTracing을 사용하지 않으면 양쪽에서 모두 전파를 사용하는 경우 사용자 추적이 동일한 동작에 나타납니다. ServiceModel 추적은 동작이 처음에 설정된 사용자 코드 처리와 동일한 스레드에서 발생하지 않는 한 기본 0000 동작에 나타납니다.  
  
- ServiceModel 추적과 ActivityTracing을 모두 사용하면 사용자 추적이 사용자 정의 동작에 나타나고 ServiceModel 추적은 ServiceModel에서 정의된 동작에 나타납니다. 전파는 ServiceModel 수준에서 발생합니다.
