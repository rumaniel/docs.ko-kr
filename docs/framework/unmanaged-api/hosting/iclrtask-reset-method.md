---
title: ICLRTask::Reset 메서드
ms.date: 03/30/2017
api_name:
- ICLRTask.Reset
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask::Reset
helpviewer_keywords:
- ICLRTask::Reset method [.NET Framework hosting]
- Reset method, ICLRTask interface [.NET Framework hosting]
ms.assetid: 1bfb5d3a-0ffd-4bb4-9bf6-aec00cb675b7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3039855a58e6db6a403ab33c226b4b8b390668f7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67758598"
---
# <a name="iclrtaskreset-method"></a>ICLRTask::Reset 메서드
호스트 작업을 완료 하 고 현재 다시 사용 하려면 CLR을 사용 하도록 설정 된 CLR (공용 언어 런타임)에 게 알립니다 [ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) 인스턴스를 다른 작업을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Reset (  
    [in] BOOL fFull  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `fFull`  
 [in] `true`런타임은 현재와 관련 된 보안 및 로캘 정보 외에도 모든 스레드 관련 정적 값을 다시 설정 해야 하는 경우 `ICLRTask` 인스턴스이면이 고, 그렇지 `false`합니다.  
  
 값이 `true`, 런타임에서 사용 하 여 저장 된 데이터를 다시 설정 <xref:System.Threading.Thread.AllocateDataSlot%2A> 또는 <xref:System.Threading.Thread.AllocateNamedDataSlot%2A>합니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|`Reset` 성공적으로 반환 합니다.|  
|HOST_E_CLRNOTAVAILABLE|CLR이 로드 된 프로세스에 또는 CLR 상태인는 관리 코드를 실행 하거나 호출을 처리할 수 없습니다. successfully|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|이벤트가 차단 된 스레드가 취소 된 또는 파이버를 대기 하 고 있습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드 E_FAIL을 반환 하는 경우 CLR은 프로세스 내에서 사용할 수 없습니다. 메서드를 호스트 하는 데 대 한 후속 호출 HOST_E_CLRNOTAVAILABLE를 반환 합니다.|  
  
## <a name="remarks"></a>설명  
 이전에 만든 CLR 재활용할 수 `ICLRTask` 인스턴스를 반복적으로 새로 고침 작업이 필요할 때마다 새 인스턴스를 만드는 오버 헤드를 방지 합니다. 호스트를 호출 하 여이 기능을 활성화 `ICLRTask::Reset` of [iclrtask:: Exittask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-exittask-method.md) 때 작업을 완료 합니다. 다음은 요약의 일반적인 수명 주기는 `ICLRTask` 인스턴스:  
  
1. 런타임에서 새로 만들고 `ICLRTask` 인스턴스.  
  
2. 런타임 호출 [ihosttaskmanager:: Getcurrenttask](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-getcurrenttask-method.md) 현재 호스트 작업에 대 한 참조를 가져오려고 합니다.  
  
3. 런타임 호출 [ihosttask:: Setclrtask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-setclrtask-method.md) 호스트 작업을 사용 하 여 새 인스턴스를 연결 합니다.  
  
4. 태스크를 실행 하 고 완료 합니다.  
  
5. 호스트를 호출 하 여 작업을 소멸 시킵니다 `ICLRTask::ExitTask`합니다.  
  
 `Reset` 두 가지 방법으로이 시나리오를 변경합니다. 호스트를 호출 하 여 위의 5 단계에서 `Reset` 정리 된 상태로 작업을 다시 설정 하려면 다음을 `ICLRTask` 연결 된 인스턴스 [IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md) 인스턴스. 원하는 경우 호스트 캐시할 수도 있습니다는 `IHostTask` 인스턴스 다시 사용할 수 있도록 합니다. 위의 1 단계에서 공용 언어 런타임은 가져옵니다 재활용 된 `ICLRTask` 새 인스턴스를 만드는 대신 캐시에서.  
  
 이 방법은 호스트 역시 다시 사용할 수 있는 작업자 태스크의 풀 하는 경우에 작동 합니다. 호스트 중 하나을 제거 하면 해당 `IHostTask` 인스턴스를 해당 소멸 시킵니다 `ICLRTask` 호출 하 여 `ExitTask`합니다.  
  
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
