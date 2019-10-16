---
title: 210 - MessageThrottleExceeded
ms.date: 03/30/2017
ms.assetid: 24ca08ea-c11c-4753-946e-98aa820f8711
ms.openlocfilehash: 7ba5948b36642085ef44661b3d580e7f1c4102cb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61781887"
---
# <a name="210---messagethrottleexceeded"></a>210 - MessageThrottleExceeded
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|ID|210|  
|키워드|EndToEndMonitoring, HealthMonitoring, 문제 해결, ServiceModel|  
|수준|경고|  
|채널|Microsoft-Windows-애플리케이션 서버-애플리케이션/분석|  
  
## <a name="description"></a>설명  
 이 이벤트는 세 개의 기본 서비스 스로틀 중 하나가 초과되었을 때 내보내집니다. 이 이벤트는 스로틀 한계가 처음 초과되는 경우에만 내보내집니다. 예를 들어 동시 호출의 스로틀 한계가 10인 경우 11번째 동시 호출을 수행하면 `MessageThrottleExceeded` 이벤트가 내보내지지만 12번째 호출부터는 이 이벤트가 내보내지지 않습니다. 또한 불필요한 이벤트 스트림을 방지하기 위해 스로틀 한계를 넘나드는 작업을 수행하는 경우에도 이 이벤트가 내보내지지 않습니다. 이 예제에서는 두 개의 호출이 완료되면 동시 호출 수가 9가 됩니다. 나중에 두 개의 호출이 더 완료되면 현재 값은 다시 11이 됩니다. 이 경우 이 이벤트가 내보내지지 않습니다. 현재 값이 스로틀 한계의 70%에 도달하면 작업이 더디게 진행됨을 나타내는 다른 이벤트가 내보내집니다. 스로틀 한계를 초과하는 추가 작업을 수행하면 다른 `MessageThrottleExceeded` 이벤트가 내보내집니다. 이 예제에서는 동시 호출 수가 7에서 11이 되면 다른 `MessageThrottleExceeded` 이벤트가 내보내집니다.  
  
## <a name="message"></a>메시지  
 '%1'의 스로틀 한계 '%2'에 도달했습니다.  
  
## <a name="details"></a>설명  
  
|데이터 항목 이름|데이터 항목 형식|설명|  
|--------------------|--------------------|-----------------|  
|Throttle Name|`xs:string`|초과한 스로틀의 이름입니다. `MaxConcurrentCalls`, `MaxConcurrentInstances` 또는 `MaxConcurrentSessions` 중 하나입니다.|  
|Limit|`xs:long`|현재 구성된 스로틀 한계입니다.|  
|HostReference|`xs:string`|웹 호스팅 서비스의 경우 이 필드는 웹 계층의 서비스를 고유하게 식별합니다. 해당 형식으로 정의 됩니다 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'. 예제: 'Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|AppDomain.CurrentDomain.FriendlyName에서 반환되는 문자열입니다.|
