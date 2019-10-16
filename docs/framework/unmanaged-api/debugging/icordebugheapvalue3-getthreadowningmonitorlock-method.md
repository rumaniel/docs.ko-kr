---
title: ICorDebugHeapValue3::GetThreadOwningMonitorLock 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue3.GetThreadOwningMonitorLock
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue3::GetThreadOwningMonitorLock
helpviewer_keywords:
- GetThreadOwningMonitorLock method [.NET Framework debugging]
- ICorDebugHeapValue3::GetThreadOwningMonitorLock method [.NET Framework debugging]
ms.assetid: e06fc19d-2cf4-4cad-81a3-137a68af8969
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4322a7e23c7085dadb3b2df6c1f72125aa685cef
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67756609"
---
# <a name="icordebugheapvalue3getthreadowningmonitorlock-method"></a>ICorDebugHeapValue3::GetThreadOwningMonitorLock 메서드
이 개체의 모니터 잠금을 소유 하는 관리 되는 스레드를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetThreadOwningMonitorLock (  
    [out] ICorDebugThread   **ppThread,  
    [out] DWORD              *pAcquisitionCount  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppThread`  
 [out] 이 개체의 모니터 잠금을 소유 하는 관리 되는 스레드입니다.  
  
 `pAcquisitionCount`  
 [out] 이 스레드가 소유 중인를 반환 하기 전에 잠금을 해제 해야 하는 횟수입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|S_FALSE|이 개체에 대 한 모니터 잠금을 소유 하는 관리 되는 스레드가 없습니다.|  
  
## <a name="exceptions"></a>예외  
  
## <a name="remarks"></a>설명  
 이 개체의 모니터 잠금을 소유 하는 관리 되는 스레드:  
  
- 메서드는 S_OK를 반환합니다.  
  
- Thread 개체 스레드가 종료 될 때까지 유효 합니다.  
  
 이 개체에 대 한 모니터 잠금을 소유 하는 관리 되는 스레드가 없는 경우 `ppThread` 및 `pAcquisitionCount` 변경 되지 메서드에서 S_FALSE를 반환 합니다.  
  
 하는 경우 `ppThread` 또는 `pAcquisitionCount` 유효한 포인터가 아닙니다 결과가 정의 되지 않습니다.  
  
 확인할 수 있는 스레드가이 개체에 대 한 모니터 잠금을 소유 하 고 있는 경우 오류가 발생 하는 경우 메서드는 실패를 나타내는 HRESULT를 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
