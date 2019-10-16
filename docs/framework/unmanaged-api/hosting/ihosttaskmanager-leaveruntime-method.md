---
title: IHostTaskManager::LeaveRuntime 메서드
ms.date: 03/30/2017
api_name:
- IHostTaskManager.LeaveRuntime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::LeaveRuntime
helpviewer_keywords:
- IHostTaskManager::LeaveRuntime method [.NET Framework hosting]
- LeaveRuntime method [.NET Framework hosting]
ms.assetid: 43689cc4-e48e-46e5-a22d-bafd768b8759
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8b2e8e636915b3921fcd727fc78a3fb18fc69104
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959036"
---
# <a name="ihosttaskmanagerleaveruntime-method"></a>IHostTaskManager::LeaveRuntime 메서드
현재 실행 중인 태스크가 CLR (공용 언어 런타임)을 유지 하 고 비관리 코드를 입력 하려고 함을 호스트에 알립니다.  
  
> [!IMPORTANT]
> [IHostTaskManager:: EnterRuntime](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-enterruntime-method.md) 에 대 한 해당 호출에서는 현재 실행 중인 작업에서 관리 코드를 현재 실행 하 고 있음을 호스트에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT LeaveRuntime (  
    [in] SIZE_T target  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `target`  
 진행 호출할 관리 되지 않는 함수의 매핑된 이식 가능한 실행 파일 내 주소입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|`LeaveRuntime`성공적으로 반환 되었습니다.|  
|HOST_E_CLRNOTAVAILABLE|CLR이 프로세스에 로드 되지 않았거나 CLR이 관리 코드를 실행할 수 없거나 호출을 성공적으로 처리할 수 없는 상태에 있습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|차단 된 스레드나 파이버에서 대기 하는 동안 이벤트를 취소 했습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드가 E_FAIL을 반환 하는 경우 프로세스 내에서 더 이상 CLR을 사용할 수 없습니다. 호스팅 메서드에 대 한 후속 호출은 HOST_E_CLRNOTAVAILABLE을 반환 합니다.|  
|E_OUTOFMEMORY|메모리가 부족 하 여 요청 된 할당을 완료할 수 없습니다.|  
  
## <a name="remarks"></a>설명  
 비관리 코드와의 호출 시퀀스는 중첩 될 수 있습니다. 예를 들어 아래 `LeaveRuntime`목록에는, [IHostTaskManager:: ReverseEnterRuntime](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-reverseenterruntime-method.md), [IHostTaskManager:: ReverseLeaveRuntime](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-reverseleaveruntime-method.md)에 대 한 호출 시퀀스를 사용 하 고 `IHostTaskManager::EnterRuntime` 호스트에서 중첩 된 레이어를 식별 합니다.  
  
|동작|해당 메서드 호출|  
|------------|-------------------------------|  
|관리 되는 Visual Basic 실행 파일은 플랫폼 호출을 사용 하 여 C로 작성 된 관리 되지 않는 함수를 호출 합니다.|`IHostTaskManager::LeaveRuntime`|  
|관리 되지 않는 C 함수는로 C#작성 된 관리 DLL의 메서드를 호출 합니다.|`IHostTaskManager::ReverseEnterRuntime`|  
|관리 되 C# 는 함수는 C로 작성 된 다른 관리 되지 않는 함수를 호출 하 여 플랫폼 호출을 사용 하기도 합니다.|`IHostTaskManager::LeaveRuntime`|  
|두 번째 관리 되지 않는 함수는 C# 함수에 대 한 실행을 반환 합니다.|`IHostTaskManager::EnterRuntime`|  
|함수 C# 는 첫 번째 관리 되지 않는 함수에 대 한 실행을 반환 합니다.|`IHostTaskManager::ReverseLeaveRuntime`|  
|첫 번째 관리 되지 않는 함수는 Visual Basic 프로그램으로 실행을 반환 합니다.|`IHostTaskManager::EnterRuntime`|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
