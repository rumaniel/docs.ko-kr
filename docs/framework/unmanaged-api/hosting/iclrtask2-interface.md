---
title: ICLRTask2 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRTask2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2
helpviewer_keywords:
- ICLRTask2 interface [.NET Framework hosting]
ms.assetid: b5a22ebc-0582-49de-91f9-97a3d9789290
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 518248651de6d8afdf25692c5f48da52b11eb0f7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61763401"
---
# <a name="iclrtask2-interface"></a>ICLRTask2 인터페이스
모든 기능을 제공 합니다 [ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) 인터페이스; 또한 스레드 중단을 현재 스레드에서 지연 될 수 있는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[BeginPreventAsyncAbort 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-beginpreventasyncabort-method.md)|지연 새 스레드는 현재 스레드에 대 한 요청을 중단 합니다.|  
|[EndPreventAsyncAbort 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-endpreventasyncabort-method.md)|새 또는 현재 스레드에서 보류 중인 스레드가 될 스레드 중단 요청을 중단 합니다.|  
  
## <a name="remarks"></a>설명  
 `ICLRTask2` 인터페이스가 상속 된 `ICLRTask` 인터페이스 및 호스트가 실패 해서는 안 되는 코드 영역을 보호 하기 위해 스레드 중단을 지연 하는 데 사용할 수 있는 메서드를 추가 합니다. 호출 `BeginPreventAsyncAbort` 현재 스레드 및 호출에 대 한 스레드 중단 지연 카운터를 증가 시킵니다 `EndPreventAsyncAbort` 감소 것입니다. 에 대 한 호출 `BeginPreventAsyncAbort` 고 `EndPreventAsyncAbort` 중첩 될 수 있습니다. 카운터는 0 보다 큰,으로 현재 스레드의 스레드 중단이 지연 됩니다.  
  
 경우에 대 한 호출 `BeginPreventAsyncAbort` 및 `EndPreventAsyncAbort` 는 이루지 않는 것이 스레드 중단을 현재 스레드에 배달할 수 없는 상태에 도달할 수 있습니다.  
  
 자체를 중단 하는 스레드에 대 한 지연 적용 되지 않습니다.  
  
 이 기능을 통해 노출 되는 기능을 가상 컴퓨터 (VM)에서 내부적으로 사용 됩니다. 이러한 메서드를 잘못 사용 하면 VM에 지정 되지 않은 동작이 발생할 수 있습니다. 예를 들어, 호출 `EndPreventAsyncAbort` 첫 번째 호출 하지 않고 `BeginPreventAsyncAbort` VM가 증가 이전 하는 경우 카운터를 0으로 설정할 수 있습니다. 마찬가지로, 오버플로 대 한 내부 카운터 확인 하지 않습니다. 호스트와 VM에서 증가 하기 때문에 정수 한계 초과, 하는 경우의 결과 동작은 지정 되지 않습니다.  
  
 상속 된 멤버에 대 한 정보에 대 한 `ICLRTask` 이 인터페이스의 다른 용도 확인 합니다 [ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) 인터페이스입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
