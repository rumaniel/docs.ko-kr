---
title: IHostTaskManager::CreateTask 메서드
ms.date: 03/30/2017
api_name:
- IHostTaskManager.CreateTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::CreateTask
helpviewer_keywords:
- CreateTask method, IHostTaskManager interface [.NET Framework hosting]
- IHostTaskManager::CreateTask method [.NET Framework hosting]
ms.assetid: a6f8ad36-61e1-42b0-9db2-add575646d18
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0a154aeafed9bc4de63dea3fe7fc32e2daee7b96
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67749731"
---
# <a name="ihosttaskmanagercreatetask-method"></a>IHostTaskManager::CreateTask 메서드
호스트에서 새 작업을 만들도록 요청 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateTask (  
    [in]  DWORD stacksize,   
    [in]  LPTHREAD_START_ROUTINE pStartAddress,  
    [in]  PVOID pParameter,  
    [out] IHostTask **ppTask  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `stacksize`  
 [in] 요청 된 크기 (바이트) 요청 된 스택을의 기본 크기에 대 한 0 (영)입니다.  
  
 `pStartAddress`  
 [in] 함수에 대 한 포인터는 태스크를 실행 합니다.  
  
 `pParameter`  
 [in] 매개 변수를 사용 하는 함수, 함수 또는 null 전달 될 사용자 데이터에 대 한 포인터입니다.  
  
 `ppTask`  
 [out] 주소에 대 한 포인터를 [IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md) 태스크를 만들 수 없는 경우 호스트 또는 null가 만든 인스턴스입니다. 작업은 명시적으로 호출 하 여 시작 될 때까지 일시 중단 된 상태를 유지 [ihosttask:: Start](../../../../docs/framework/unmanaged-api/hosting/ihosttask-start-method.md)합니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|`CreateTask` 성공적으로 반환 합니다.|  
|HOST_E_CLRNOTAVAILABLE|프로세스에는 CLR (공용 언어 런타임)에 로드 되지 또는 CLR 상태인는 관리 코드를 실행 하거나 호출을 처리할 수 없습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|이벤트가 차단 된 스레드가 취소 된 또는 파이버를 대기 하 고 있습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드 E_FAIL을 반환 하는 경우 CLR은 프로세스 내에서 사용할 수 없습니다. 메서드를 호스트 하는 데 대 한 후속 호출 HOST_E_CLRNOTAVAILABLE를 반환 합니다.|  
|E_OUTOFMEMORY|메모리가 부족 하 여 요청된 작업을 만들 수 있습니다.|  
  
## <a name="remarks"></a>설명  
 CLR에서는 `CreateTask` 호스트에서 새 작업을 만들도록 요청 합니다. 호스트에 대 한 인터페이스 포인터를 반환 합니다.는 `IHostTask` 인스턴스. 반환된 된 작업은 명시적으로 호출 하 여 시작 될 때까지 일시 중지 해야 `IHostTask::Start`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
