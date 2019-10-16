---
title: ICorDebugController::HasQueuedCallbacks 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugController.HasQueuedCallbacks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::HasQueuedCallbacks
helpviewer_keywords:
- HasQueuedCallbacks method [.NET Framework debugging]
- ICorDebugController::HasQueuedCallbacks method [.NET Framework debugging]
ms.assetid: 0d6a1cd9-370b-4462-adbf-e3980e897ea7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0d17f51867b64780fca9b21c5f48c88db36343af
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67748777"
---
# <a name="icordebugcontrollerhasqueuedcallbacks-method"></a>ICorDebugController::HasQueuedCallbacks 메서드
모든 관리 되는 콜백을 지정 된 스레드에 대 한 현재 대기 중인 여부를 나타내는 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT HasQueuedCallbacks (  
    [in] ICorDebugThread *pThread,  
    [out] BOOL           *pbQueued  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pThread`  
 [in] 스레드를 나타내는 "ICorDebugThread" 개체에 대 한 포인터입니다.  
  
 `pbQueued`  
 [out] 값에 대 한 포인터 `true` 모든 관리 되는 콜백을 고, 그렇지 않으면 지정 된 스레드에 대 한 큐에 대기 중인 현재 경우 `false`합니다.  
  
 에 대 한 null을 지정 하는 경우는 `pThread` 매개 변수를 `HasQueuedCallbacks` 돌아갑니다 `true` 현재 관리 되는 콜백을 모든 스레드에 대 한 대기 합니다.  
  
## <a name="remarks"></a>설명  
 콜백이 발송된 한 번, 때마다 됩니다 [icordebugcontroller:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) 라고 합니다. 디버거는 동시에 발생 하는 여러 디버깅 이벤트를 보고 하려는 경우이 플래그를 확인할 수 있습니다.  
  
 디버깅 이벤트 큐에 대기 하는 경우는 이미 발생 하므로 디버거가 디버기의 상태의 되도록 전체 큐를 제거 해야 합니다. (호출 `ICorDebugController::Continue` 큐를 비울.) 예를 들어, 큐 스레드에서 두 디버깅 이벤트를 포함 하는 경우 *X*, 디버거 스레드를 일시 중단 *X* 그 다음으로 첫 번째 디버깅 이벤트 호출 후 `ICorDebugController::Continue`에 대 한 두 번째 디버깅 이벤트 스레드 *X* 는 스레드가 일시 중단 된 있지만 발송 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료
