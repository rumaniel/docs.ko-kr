---
title: ICLRTask2::EndPreventAsyncAbort 메서드
ms.date: 03/30/2017
api_name:
- ICLRTask2.EndPreventAsyncAbort
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2::EndPreventAsyncAbort
helpviewer_keywords:
- EndPreventAsyncAbort method [.NET Framework hosting]
- ICLRTask2::EndPreventAsyncAbort method [.NET Framework hosting]
ms.assetid: d8013659-e3df-44b3-814f-a6b534ce62f8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 36947eb33460fe3f15cf4ade1cad55cb5e77f1cc
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67770233"
---
# <a name="iclrtask2endpreventasyncabort-method"></a>ICLRTask2::EndPreventAsyncAbort 메서드
새 또는 현재 스레드에서 보류 중인 스레드가 될 스레드 중단 요청을 중단 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EndPreventAsyncAbort();  
```  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|HOST_E_INVALIDOPERATION|메서드는 현재 스레드가 아닌 스레드에서 호출 되었습니다.|  
  
## <a name="remarks"></a>설명  
 현재 스레드에 대 한 하나에서이 메서드는 지연 스레드 중단 감소 카운터를 호출합니다.  
  
 에 대 한 호출 [ICLRTask2::BeginPreventAsyncAbort](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-beginpreventasyncabort-method.md) 고 `EndPreventAsyncAbort` 중첩 될 수 있습니다. 카운터는 0 보다 큰,으로 현재 스레드의 스레드 중단이 지연 됩니다.  
  
 이 기능을 통해 노출 되는 기능을 가상 컴퓨터 (VM)에서 내부적으로 사용 됩니다. 이러한 메서드를 잘못 사용 하면 VM에 지정 되지 않은 동작이 발생할 수 있습니다. 예를 들어, 호출 `EndPreventAsyncAbort` 첫 번째 호출 하지 않고 `BeginPreventAsyncAbort` VM가 증가 이전 하는 경우 카운터를 0으로 설정할 수 있습니다. 마찬가지로, 오버플로 대 한 내부 카운터 확인 하지 않습니다. 호스트와 VM에서 증가 하기 때문에 정수 한계 초과, 하는 경우의 결과 동작은 지정 되지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [BeginPreventAsyncAbort 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-beginpreventasyncabort-method.md)
- [ICLRTask2 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-interface.md)
- [ICLRTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
