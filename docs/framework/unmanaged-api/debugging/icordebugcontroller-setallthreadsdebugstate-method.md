---
title: ICorDebugController::SetAllThreadsDebugState 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugController.SetAllThreadsDebugState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::SetAllThreadsDebugState
helpviewer_keywords:
- SetAllThreadsDebugState method [.NET Framework debugging]
- ICorDebugController::SetAllThreadsDebugState method [.NET Framework debugging]
ms.assetid: bdda4bd7-4743-4d58-a22b-8067e967db95
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9348652129a3357784654006dc16d822298f28f8
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67749954"
---
# <a name="icordebugcontrollersetallthreadsdebugstate-method"></a>ICorDebugController::SetAllThreadsDebugState 메서드
프로세스의 모든 관리 되는 스레드의 디버그 상태를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetAllThreadsDebugState (  
    [in] CorDebugThreadState  state,  
    [in] ICorDebugThread      *pExceptThisThread  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `state`  
 [in] 디버깅을 위한 스레드 상태를 지정 하는 "CorDebugThreadState" 열거형의 값입니다.  
  
 `pExceptThisThread`  
 [in] 디버그 상태 설정에서 제외 해야 하는 스레드를 나타내는 "ICorDebugThread" 개체에 대 한 포인터입니다. 이 값이 null 인 경우에 스레드가 없습니다 제외 됩니다.  
  
## <a name="remarks"></a>설명  
 `SetAllThreadsDebugState` 메서드를 통해 표시 되지 않는 스레드 영향을 줄 수 [EnumerateThreads 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-enumeratethreads-method.md)를 사용 하 여 일시 중단 된 하므로 스레드는 `SetAllThreadsDebugState` 메서드를 사용 하 여 다시 시작 해야 할를 `SetAllThreadsDebugState` 메서드.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료
