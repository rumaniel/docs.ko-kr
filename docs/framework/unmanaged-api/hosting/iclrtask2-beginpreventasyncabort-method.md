---
title: ICLRTask2::BeginPreventAsyncAbort 메서드
ms.date: 03/30/2017
api_name:
- ICLRTask2.BeginPreventAsyncAbort
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2::BeginPreventAsyncAbort
helpviewer_keywords:
- ICLRTask2::BeginPreventAsyncAbort method [.NET Framework hosting]
- BeginPreventAsyncAbort method [.NET Framework hosting]
ms.assetid: 75754c2f-38c7-4707-85fe-559db4542729
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 23ead080823ace1b091568108af8866dcbca14ec
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67770269"
---
# <a name="iclrtask2beginpreventasyncabort-method"></a>ICLRTask2::BeginPreventAsyncAbort 메서드
지연 새 스레드가 중단 요청을 현재 스레드의 스레드 중단이 발생 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT BeginPreventAsyncAbort();  
```  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|HOST_E_INVALIDOPERATION|메서드는 현재 스레드가 아닌 스레드에서 호출 되었습니다.|  
  
## <a name="remarks"></a>설명  
 이 메서드를 호출 현재 스레드의 스레드 중단 지연 카운터를 씩 증가 시킵니다.  
  
 에 대 한 호출 `BeginPreventAsyncAbort` 하 고 [ICLRTask2::EndPreventAsyncAbort](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-endpreventasyncabort-method.md) 중첩 될 수 있습니다. 카운터는 0 보다 큰,으로 현재 스레드의 스레드 중단이 지연 됩니다. 경우이 호출은 호출 하 여 연결 하지는 `EndPreventAsyncAbort` 스레드 중단을 현재 스레드에 배달할 수 없는 상태에 도달할 가능성이 메서드.  
  
 자체를 중단 하는 스레드에 대 한 지연 적용 되지 않습니다.  
  
 이 기능을 통해 노출 되는 기능을 가상 컴퓨터 (VM)에서 내부적으로 사용 됩니다. 이러한 메서드를 잘못 사용 하면 VM에 지정 되지 않은 동작이 발생할 수 있습니다. 예를 들어, 호출 `EndPreventAsyncAbort` 첫 번째 호출 하지 않고 `BeginPreventAsyncAbort` VM가 증가 이전 하는 경우 카운터를 0으로 설정할 수 있습니다. 마찬가지로, 오버플로 대 한 내부 카운터 확인 하지 않습니다. 호스트와 VM에서 증가 하기 때문에 정수 한계 초과, 하는 경우의 결과 동작은 지정 되지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [EndPreventAsyncAbort 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-endpreventasyncabort-method.md)
- [ICLRTask2 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-interface.md)
- [ICLRTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
