---
title: ICorDebugProcess::GetHelperThreadID 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetHelperThreadID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetHelperThreadID
helpviewer_keywords:
- GetHelperThreadID method [.NET Framework debugging]
- ICorDebugProcess::GetHelperThreadID method [.NET Framework debugging]
ms.assetid: 84e1e605-37c1-49a5-8e12-35db85654622
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ad62b267eb0c49ff8fbefeb45b523c21edc705fe
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67766045"
---
# <a name="icordebugprocessgethelperthreadid-method"></a>ICorDebugProcess::GetHelperThreadID 메서드
디버거의 내부 도우미 스레드의 운영 체제 (OS) 스레드 ID를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetHelperThreadID (  
    [out] DWORD *pThreadID  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pThreadID`  
 [out] OS에 대 한 포인터 스레드 디버거의 내부 도우미 스레드의 ID입니다.  
  
## <a name="remarks"></a>설명  
 관리 및 관리 되지 않는 디버그 하는 동안는 디버거의 디버거에 의해 배치 중단점이 적중 될 경우 지정된 된 ID 사용 하 여 스레드가 계속 실행 되도록 합니다. 디버거는 사용자 로부터이 스레드를 숨길 수도 있습니다. 도우미 스레드가 아직 프로세스에 있는 경우는 `GetHelperThreadID` 에서 0을 반환 하는 메서드 *`pThreadID`합니다.  
  
 시간이 지남에 따라 변경 될 수 있으므로 도우미 스레드의 스레드 ID를 캐시할 수 없습니다. 다시 중지 이벤트가 발생할 때마다 스레드 ID를 쿼리해야 합니다.  
  
 스레드 ID의 디버거 도우미 스레드에서 수정 될 모든 관리 되지 않는 [icordebugmanagedcallback:: Createthread](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createthread-method.md) 디버거 도우미 스레드 스레드 ID를 확인 하 고 사용자 로부터 숨길 있으므로 이벤트입니다. 관리 되지 않는 동안 도우미 스레드로 식별 되는 스레드 `ICorDebugManagedCallback::CreateThread` 이벤트는 관리 되는 사용자 코드를 실행 되지 것입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl. CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
