---
title: IHostManualEvent 인터페이스
ms.date: 03/30/2017
api_name:
- IHostManualEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostManualEvent
helpviewer_keywords:
- IHostManualEvent interface [.NET Framework hosting]
ms.assetid: 300c2661-b7d1-4c39-b080-9ebdef0fd523
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ad580f7cab81323e09a24dc12db39f223be3aeb4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61973071"
---
# <a name="ihostmanualevent-interface"></a>IHostManualEvent 인터페이스
호스트에서 구현 하는 수동 재설정 이벤트의 표시를 제공합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[Reset 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmanualevent-reset-method.md)|현재 다시 설정 `IHostManualEvent` 신호 되지 않은 상태로 인스턴스.|  
|[Set 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmanualevent-set-method.md)|에서는 현재 `IHostManualEvent` 신호를 받은 상태 인스턴스입니다.|  
|[Wait 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostmanualevent-wait-method.md)|현재 `IHostManualEvent` 을 소유 하는 때까지 대기 하는 인스턴스 또는 지정된 된 시간 간격이 경과 시간입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRSyncManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md)
- [IHostAutoEvent 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostautoevent-interface.md)
- [IHostSemaphore 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostsemaphore-interface.md)
- [IHostSyncManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
