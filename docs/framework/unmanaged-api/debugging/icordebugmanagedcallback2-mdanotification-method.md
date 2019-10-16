---
title: ICorDebugManagedCallback2::MDANotification 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.MDANotification
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::MDANotification
helpviewer_keywords:
- MDANotification method [.NET Framework debugging]
- ICorDebugManagedCallback2::MDANotification method [.NET Framework debugging]
ms.assetid: 93f79627-bd31-4f4f-b95d-46a032a52fe4
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4011932af6f4b058906c19566e4c1abe96b409db
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67762090"
---
# <a name="icordebugmanagedcallback2mdanotification-method"></a>ICorDebugManagedCallback2::MDANotification 메서드
코드 실행을 MDA (관리 디버깅 도우미) 디버깅 중인 응용 프로그램에서 발생 하는 알림을 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT MDANotification(  
    [in] ICorDebugController  *pController,  
    [in] ICorDebugThread      *pThread,  
    [in] ICorDebugMDA         *pMDA  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pController`  
 [in] ICorDebugController 인터페이스 프로세스를 노출 하는 또는 mda가 발생 한 응용 프로그램 도메인에 대 한 포인터입니다.  
  
 디버거를 결정 하는 인터페이스 항상 쿼리할 수 있지만 프로세스 또는 응용 프로그램 도메인 컨트롤러 인지 하는 방법에 대 한 어떠한가 정도 해야 합니다.  
  
 `pThread`  
 [in] 디버그 이벤트가 발생 한 관리 되는 스레드를 노출 하는 ICorDebugThread 인터페이스 포인터입니다.  
  
 Mda는 관리 되지 않는 경우 스레드를 변수의 `pThread` null이 됩니다.  
  
 MDA 개체 자체에서 운영 체제 (OS) 스레드 ID를 가져와야 합니다.  
  
 `pMDA`  
 [in] 에 대 한 포인터를 [ICorDebugMDA](../../../../docs/framework/unmanaged-api/debugging/icordebugmda-interface.md) MDA 정보를 노출 하는 인터페이스입니다.  
  
## <a name="remarks"></a>설명  
 MDA는 추론 경고 및 호출 제외 하 고 명시적 디버거 조치가 필요 하지 않습니다 [icordebugcontroller:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) 디버깅 중인 응용 프로그램의 실행을 다시 시작 합니다.  
  
 된 mda 이며 데이터에 언제 든 지 특정된 MDA는 CLR (공용 언어 런타임) 확인할 수 있습니다. 따라서 디버거는 특정 MDA 패턴이 필요한 모든 기능을 구축 하지 해야 합니다.  
  
 Mda 큐에 대기 및 MDA 발생 직후 발생 될 수 있습니다. 이 MDA를 발견할 때 MDA를 실행 하는 대신 실행에 대 한 안전 지점에 도달할 때까지 대기 해야 하는 런타임 경우 발생할 수 있습니다. 즉, 런타임은 Mda의 숫자는 큐에 대기 중인된 콜백 ("연결" 이벤트 작업 유사) 단일 집합을 발생 시킬 수 있습니다.  
  
 디버거는에 대 한 참조를 해제 해야는 `ICorDebugMDA` 에서 반환 된 후 즉시 인스턴스는 `MDANotification` MDA가 사용 된 메모리를 CLR 수 있도록 콜백 합니다. 인스턴스가 해제 여러 개의 Mda가 실행 하는 경우 성능이 향상 될 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [관리 디버깅 도우미를 사용하여 오류 진단](../../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [ICorDebugManagedCallback2 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-interface.md)
- [ICorDebugManagedCallback 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)
