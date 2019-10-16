---
title: ICorDebugUnmanagedCallback::DebugEvent 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugUnmanagedCallback.DebugEvent
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugUnmanagedCallback::DebugEvent
helpviewer_keywords:
- DebugEvent method [.NET Framework debugging]
- ICorDebugUnmanagedCallback::DebugEvent method [.NET Framework debugging]
ms.assetid: be9cab04-65ec-44d5-a39a-f90709fdd043
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c1c75e1844fca4e592faa924a55432dd42fa7355
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67772625"
---
# <a name="icordebugunmanagedcallbackdebugevent-method"></a>ICorDebugUnmanagedCallback::DebugEvent 메서드
네이티브 이벤트가 발생 했음을 디버거에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DebugEvent (  
    [in] LPDEBUG_EVENT  pDebugEvent,  
    [in] BOOL           fOutOfBand  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pDebugEvent`  
 [in] 네이티브 이벤트에 대 한 포인터입니다.  
  
 `fOutOfBand`  
 [in] `true`디버거 호출 될 때까지 관리 되지 않는 이벤트가 발생 한 후 관리 되는 프로세스 상태를 사용 하 여 상호 작용 수 없는 경우 [icordebugcontroller:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md)이 고, 그렇지 않으면 `false`합니다.  
  
## <a name="remarks"></a>설명  
 디버깅 중인 스레드의 Win32 스레드 인 경우에 디버깅 인터페이스는 Win32의 모든 멤버를 사용 하지 마십시오. 호출할 수 있습니다 `ICorDebugController::Continue` Win32 스레드에서만 및 지난 대역의 이벤트를 계속 하는 경우에 합니다.  
  
 `DebugEvent` 콜백 콜백에 대 한 표준 규칙을 따르지 않습니다. 호출 하는 경우 `DebugEvent`프로세스에 원시 됩니다, OS 디버그 상태를 중지 합니다. 프로세스 동기화 되지 않습니다. 중첩 된 다른 따를 수 있는 관리 코드에 대 한 정보에 대 한 요청을 충족 하기 위해 필요한 경우 동기화 된 상태로 자동으로 입력 됩니다 `DebugEvent` 콜백 합니다.  
  
 호출 [icordebugprocess:: Clearcurrentexception](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess-clearcurrentexception-method.md) 프로세스를 계속 하기 전에 예외 이벤트를 무시 하는 프로세스에 있습니다. 이 메서드를 호출 DBG_EXCEPTION_NOT_HANDLED 대신 DBG_CONTINUE 계속 요청을 전송 하 고 자동으로 대역의 중단점 및 단일 단계 예외를 지웁니다. 대역의 이벤트는 시간과 처리 중인 대역 내 이벤트는 이미 디버깅 중인 응용 프로그램 중지 표시 하는 경우에 언제 든 지 가져올 수 있습니다.  
  
 .NET framework 버전 2.0에서 디버거 대역의 중단점 이벤트 지난 즉시 계속 해야 합니다. 디버거를 사용 해야 합니다 [ICorDebugProcess2::SetUnmanagedBreakpoint](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess2-setunmanagedbreakpoint-method.md) 및 [ICorDebugProcess2::ClearUnmanagedBreakpoint](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess2-clearunmanagedbreakpoint-method.md) 메서드를 추가 하 고 중단점을 제거 합니다. 이러한 메서드는 자동으로 대역의 중단점을 통해 건너뜁니다. 따라서 발송 된 밴드를만 중단점을 원시 중단점은 명령 스트림을 win32 호출과 같은 이미 있어야 `DebugBreak` 함수입니다. 사용 하지 마세요 `ICorDebugProcess::ClearCurrentException`, [icordebugprocess:: Getthreadcontext](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess-getthreadcontext-method.md)를 [icordebugprocess:: Setthreadcontext](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess-setthreadcontext-method.md), 또는 다른 어떤 멤버도 합니다 [디버깅 API](../../../../docs/framework/unmanaged-api/debugging/index.md)합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugUnmanagedCallback 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugunmanagedcallback-interface.md)
