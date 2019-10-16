---
title: ICorDebugThread::SetDebugState 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugThread.SetDebugState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::SetDebugState
helpviewer_keywords:
- ICorDebugThread::SetDebugState method [.NET Framework debugging]
- SetDebugState method [.NET Framework debugging]
ms.assetid: 6382bdf6-d488-4952-b653-cb09b6e1c6c2
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 15e18888e307a14c4396966afc0a623e1acba104
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332805"
---
# <a name="icordebugthreadsetdebugstate-method"></a>ICorDebugThread::SetDebugState 메서드
이 ICorDebugThread의 디버깅 상태를 설명 하는 플래그를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetDebugState (  
    [in] CorDebugThreadState state  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `state`  
 진행 이 스레드의 디버깅 상태를 지정 하는 CorDebugThreadState 열거형 값의 비트 조합입니다.  
  
## <a name="remarks"></a>설명  
 `SetDebugState`은 스레드의 현재 디버그 상태를 설정 합니다. "현재 디버그 상태"는 실제 현재 상태가 아닌 프로세스를 계속 해야 하는 경우 디버그 상태를 나타냅니다. 이에 대 한 일반 값은 THREAD_RUN입니다. 디버거만 스레드의 디버그 상태에 영향을 줄 수 있습니다. 디버그 상태는 계속 해 서 진행 되므로 여러 스레드를 계속 해 서 THREAD_SUSPENDed 유지 하려는 경우에는 한 번만 설정할 수 있으며, 그 후에는 걱정할 필요가 없습니다. 스레드를 일시 중단 하 고 프로세스를 다시 시작 하면 교착 상태가 발생할 수 있습니다. 이는 스레드와 프로세스의 내장 품질 이며 디자인 방식입니다. 디버거는 스레드를 비동기적으로 중단 하 고 다시 시작 하 여 교착 상태를 중단할 수 있습니다. 스레드의 사용자 상태에 USER_UNSAFE_POINT가 포함 된 경우 스레드는 GC (가비지 수집)를 차단할 수 있습니다. 즉, 일시 중단 된 스레드는 교착 상태를 일으킬 가능성이 훨씬 높습니다. 이미 큐에 대기 된 디버그 이벤트에는 영향을 주지 않습니다. 따라서 디버거는 스레드를 일시 중단 하거나 다시 시작 하기 전에 [ICorDebugController:: HasQueuedCallbacks](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-hasqueuedcallbacks-method.md)를 호출 하 여 전체 이벤트 큐를 드레이닝 해야 합니다. 그렇지 않으면 스레드가 이미 일시 중단 된 것으로 판단 되는 이벤트를 가져올 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
