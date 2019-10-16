---
title: ICorDebugController 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugController
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController
helpviewer_keywords:
- ICorDebugController interface [.NET Framework debugging]
ms.assetid: dbb1c4dc-269a-459b-ab1d-6c70788782ce
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e2a083f46f24d6f3f24c63dd2415b85f975cfa29
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912858"
---
# <a name="icordebugcontroller-interface"></a>ICorDebugController 인터페이스

<xref:System.Diagnostics.Process>나 <xref:System.AppDomain> 같이 코드 실행 컨텍스트를 제어할 수 있는 범위를 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|`ICorDebugController::CanCommitChanges`|이 메서드는 사용되지 않습니다.|  
|`ICorDebugController::CommitChanges`|이 메서드는 사용되지 않습니다.|  
|[Continue 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md)|[ICorDebugController:: Stop](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-stop-method.md)호출 후 관리 되는 스레드의 실행을 다시 시작 합니다.|  
|[Detach 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-detach-method.md)|프로세스 또는 응용 프로그램 도메인에서 디버거를 분리 합니다.|  
|[EnumerateThreads 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-enumeratethreads-method.md)|프로세스의 활성 관리 되는 스레드에 대 한 열거자를 가져옵니다.|  
|[HasQueuedCallbacks 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-hasqueuedcallbacks-method.md)|지정 된 스레드에 대해 관리 되는 콜백이 현재 대기 중인지 여부를 나타내는 값을 가져옵니다.|  
|[IsRunning 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-isrunning-method.md)|프로세스의 스레드가 현재 자유롭게 실행 중인지 여부를 나타내는 값을 가져옵니다.|  
|[SetAllThreadsDebugState 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-setallthreadsdebugstate-method.md)|프로세스에 있는 모든 관리 되는 스레드의 디버그 상태를 설정 합니다.|  
|[Stop 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-stop-method.md)|프로세스에서 관리 코드를 실행 하는 모든 스레드에서 협조적 중지를 수행 합니다.|  
|[Terminate 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-terminate-method.md)|지정 된 종료 코드를 사용 하 여 프로세스를 종료 합니다.|  
  
## <a name="remarks"></a>설명  
 에서 `ICorDebugController` 프로세스를 제어 하는 경우 범위에 프로세스의 모든 스레드가 포함 됩니다. 가 `ICorDebugController` 응용 프로그램 도메인을 제어 하는 경우 해당 특정 응용 프로그램 도메인의 스레드만 범위에 포함 됩니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
