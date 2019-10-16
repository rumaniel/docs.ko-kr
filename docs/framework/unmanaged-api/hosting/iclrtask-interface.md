---
title: ICLRTask 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask
helpviewer_keywords:
- ICLRTask interface [.NET Framework hosting]
ms.assetid: b3a44df3-578a-4451-b55e-70c8e7695f5e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1baeac5db41aa64380d694ebab5419229d8adb4c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61763544"
---
# <a name="iclrtask-interface"></a>ICLRTask 인터페이스
호스트는 CLR (공용 언어 런타임)을 요청 하거나 알림 연결 된 작업에 대 한 CLR에 제공 하는 데 사용할 수 있는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[Abort 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-abort-method.md)|CLR 작업을 중단 하도록 요청 하는 현재 `ICLRTask` 인스턴스가 나타내는입니다.|  
|[ExitTask 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-exittask-method.md)|CLR 작업이 현재 연결에 알립니다 `ICLRTask` 인스턴스 종료 되 고 태스크를 종료 하려고 합니다.|  
|[GetMemStats 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-getmemstats-method.md)|현재 태스크에 의해 메모리 리소스 사용에 대 한 통계 정보를 가져옵니다 `ICLRTask` 인스턴스.|  
|[LocksHeld 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-locksheld-method.md)|작업에서 현재 보유 중인 잠금 수를 가져옵니다.|  
|[NeedsPriorityScheduling 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-needspriorityscheduling-method.md)|호스트에 높은 우선 순위를 나타내는 현재 작업을 재조정 하기 위해 할당 하는지 여부를 나타내는 값을 가져옵니다 `ICLRTask` 인스턴스.|  
|[Reset 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-reset-method.md)|호스트 작업을 완료 하 고 현재 다시 사용 하려면 CLR을 사용 하면 CLR에 알립니다 `ICLRTask` 인스턴스를 다른 작업을 나타냅니다.|  
|[RudeAbort 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-rudeabort-method.md)|사용 하면 현재 나타내는 작업을 중단 하려면 CLR `ICLRTask` 종료자를 실행할 수는 보증을 하지 않고 즉시 인스턴스.|  
|[SetTaskIdentifier 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-settaskidentifier-method.md)|현재 태스크에 대 한 고유 식별자를 설정 `ICLRTask` 디버깅 사용에 대 한 인스턴스.|  
|[SwitchIn 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-switchin-method.md)|현재 태스크를 나타내는 CLR 알립니다 `ICLRTask` 인스턴스가 작동 가능한 상태가 있습니다.|  
|[SwitchOut 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-switchout-method.md)|현재 태스크를 나타내는 CLR 알립니다 `ICLRTask` 인스턴스가 더 이상 작동 가능한 상태가 없습니다.|  
|[YieldTask 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask-yieldtask-method.md)|다른 태스크에서 사용할 CLR 확인 프로세서 시간 요청합니다. CLR은 처리 시간을 얻을 수 있습니다이 상태의 작업을 넣을 보장 되지 않습니다.|  
  
## <a name="remarks"></a>설명  
 `ICLRTask` CLR에 대 한 작업의 표현입니다. 언제 든 지 코드 실행 하는 동안 작업 실행 중이거나 실행 대기 중인으로 설명할 수 있습니다. 호스트 호출을 `ICLRTask::SwitchIn` CLR에 알려야 하는 방법은 태스크는 현재 `ICLRTask` 인스턴스가 나타내는 작동 가능한 상태가 됩니다. 호출한 후 `ICLRTask::SwitchIn`, 호스트 런타임에서 호출 하 여 지정 된 대로 스레드 선호도 필요로 하는 경우를 제외한 모든 운영 체제 스레드에서 작업을 예약할 수는 [ihosttaskmanager:: Beginthreadaffinity](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-beginthreadaffinity-method.md) 및 [Ihosttaskmanager:: Endthreadaffinity](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-endthreadaffinity-method.md) 메서드. 나중에 잠시 운영 체제 스레드에서 작업을 제거 하 고 실행 되지 않는 상태로 하기로 결정할 수 있습니다. 예를 들어이 항목은 작업 동기화 기본 형식에서 차단 되거나 I/O 작업이 완료 될 때까지 대기 될 때마다 발생할 수 있습니다. 호스트 호출 [SwitchOut](../../../../docs/framework/unmanaged-api/hosting/iclrtask-switchout-method.md) 태스크를 나타내는 현재 CLR에 알립니다 `ICLRTask` 인스턴스가 더 이상 작동 가능한 상태가 됩니다.  
  
 작업은 일반적으로 코드 실행의 끝에서 종료 합니다. 호스트를 호출 당시 `ICLRTask::ExitTask` 연결 된 제거할 `ICLRTask`합니다. 에 대 한 호출을 사용 하 여 작업도 재활용 수 있지만 `ICLRTask::Reset`를 허용 하는 `ICLRTask` 인스턴스를 다시 사용할 수 있습니다. 이 방법은 반복적으로 만들고 인스턴스 삭제는 오버 헤드를 방지 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [ICLRTask2 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-interface.md)
