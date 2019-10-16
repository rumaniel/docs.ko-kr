---
title: IHostTaskManager 인터페이스
ms.date: 03/30/2017
api_name:
- IHostTaskManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager
helpviewer_keywords:
- IHostTaskManager interface [.NET Framework hosting]
ms.assetid: 4a0b05b9-3ef1-4607-b7c8-bd4dd43647a0
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: da30e75bf4a58e66bb0dd8210368b162cf14c3f7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61936476"
---
# <a name="ihosttaskmanager-interface"></a>IHostTaskManager 인터페이스
CLR (공용 언어 런타임)에서 표준 운영 체제 스레드 또는 파이버 함수를 사용 하는 대신 호스트를 통해 작업을 사용할 수 있는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[BeginDelayAbort 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-begindelayabort-method.md)|관리 코드는 호스트는 현재 작업 중단할 수 없는 기간이 시작 됨을 알립니다.|  
|[BeginThreadAffinity 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-beginthreadaffinity-method.md)|현재 작업 이동 하지 말아야 다른 운영 체제 스레드로 마침표를 입력 하는 관리 코드는 호스트에 알립니다.|  
|[CallNeedsHostHook 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-callneedshosthook-method.md)|호스트를에서 공용 언어 런타임에서 관리 되지 않는 함수에 지정된 된 호출을 인라인 할 수 있는지 여부를 지정할 수 있습니다.|  
|[CreateTask 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-createtask-method.md)|호스트에서 새 작업을 만들도록 요청 합니다.|  
|[EndDelayAbort 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-enddelayabort-method.md)|관리 코드는 호스트가 종료는 현재 작업을 중단 하지 말아야, 기간에 대 한 이전 호출을 다음 알립니다 `BeginDelayAbort`합니다.|  
|[EndThreadAffinity 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-endthreadaffinity-method.md)|관리 코드는 호스트는 기간이 종료 됨는 현재 작업 이동 하지 말아야 다른 운영 체제 스레드에 대 한 이전 호출 다음에 알립니다. `BeginThreadAffinity`합니다.|  
|[EnterRuntime 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-enterruntime-method.md)|관리 되지 않는 메서드를 호출 하는 플랫폼 호출 메서드를 같은 반환 되는지 실행 제어 clr 호스트에 알립니다.|  
|[GetCurrentTask 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-getcurrenttask-method.md)|이 호출이 수행 된 운영 체제 스레드에서 현재 실행 중인 작업에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetStackGuarantee 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-getstackguarantee-method.md)|프로세스의 닫기 전에 있지만 스택 작업이 완료 되 면 사용할 수 있도록 보장 되는 스택 공간의 크기를 가져옵니다.|  
|[LeaveRuntime 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-leaveruntime-method.md)|관리 코드는 호스트를 관리 되지 않는 함수를 호출 하려고에 알립니다.|  
|[ReverseEnterRuntime 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-reverseenterruntime-method.md)|비관리 코드에서 공용 언어 런타임 (CLR)에 호출이 수행 되는 호스트에 알립니다.|  
|[ReverseLeaveRuntime 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-reverseleaveruntime-method.md)|컨트롤의 입력을 차례로 호출 된 관리 코드에서 관리 되지 않는 함수를 clr에서 하는 호스트에 알립니다.|  
|[SetCLRTaskManager 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-setclrtaskmanager-method.md)|호스트에 대 한 인터페이스 포인터에 제공을 [ICLRTaskManager](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md) 인스턴스는 CLR에서 구현 합니다.|  
|[SetLocale 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-setlocale-method.md)|CLR이 현재 작업에서 로캘을 변경 되었음을 호스트에 알립니다.|  
|[SetStackGuarantee 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-setstackguarantee-method.md)|내부용으로 예약되어 있습니다.|  
|[SetUILocale 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-setuilocale-method.md)|현재 작업에서 사용자 인터페이스 로캘을 변경 되었음을 호스트에 알립니다.|  
|[Sleep 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-sleep-method.md)|현재 태스크 절전 모드로 전환 됨 호스트에 알립니다.|  
|[SwitchToTask 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-switchtotask-method.md)|현재 작업 전환 해야 함을 호스트에 알립니다.|  
  
## <a name="remarks"></a>설명  
 `IHostTaskManager` CLR 작업, 만들기 및 관리에 후크 그 반대의 경우와 비관리 코드를 관리 되는 컨트롤에서 전송 하는 경우 작업을 수행 하 고 특정 작업을 지정할 수는 호스트를 제공 하 호스트 수 있으며 코드 실행 하는 동안 사용할 수 없습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
