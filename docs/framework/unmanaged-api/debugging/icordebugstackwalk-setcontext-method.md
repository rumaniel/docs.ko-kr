---
title: ICorDebugStackWalk::SetContext 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugStackWalk.SetContext Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStackWalk::SetContext
helpviewer_keywords:
- SetContext method [.NET Framework debugging]
- ICorDebugStackWalk::SetContext method [.NET Framework debugging]
ms.assetid: bac0b156-31a3-4e7f-be4d-ab21789c81f1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d6eb97fc70fec25f4b225c3fd5bad1e780091f7c
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67771042"
---
# <a name="icordebugstackwalksetcontext-method"></a>ICorDebugStackWalk::SetContext 메서드
집합의 [ICorDebugStackWalk](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-interface.md) 스레드에 대 한 올바른 컨텍스트 개체의 현재 컨텍스트가 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetContext([in] CorDebugSetContextFlag flag,  
                   [in] ULONG32 contextSize,  
                   [in, size_is(contextSize)] BYTE context[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `flag`  
 [in] A [CorDebugSetContextFlag](../../../../docs/framework/unmanaged-api/debugging/cordebugsetcontextflag-enumeration.md) 컨텍스트가 스택의 활성 프레임에서 또는 컨텍스트 스택을 해제 하 여 얻은 여부를 나타내는 플래그입니다.  
  
 `contextSize`  
 [in] 할당 된 크기는 `CONTEXT` 버퍼입니다.  
  
 `context`  
 [in] `CONTEXT` 버퍼입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|`ICorDebugStackWalk` 개체의 컨텍스트를 설정 했습니다.|  
|E_FAIL|`ICorDebugStackWalk` 개체의 컨텍스트가 설정 되지 않았습니다.|  
|E_INVALIDARG|컨텍스트가 null입니다.|  
|HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)|상황에 맞는 버퍼가 너무 작습니다.|  
  
## <a name="exceptions"></a>예외  
  
## <a name="remarks"></a>설명  
 이 메서드는 스레드의 현재 컨텍스트를 변경 하지 않습니다.  
  
 잘못 된 컨텍스트에 현재 컨텍스트를 설정 합니다. 스택 워크에서 예기치 않은 결과가 발생할 수 있습니다.  
  
 이 컨텍스트에서의 정확한 비트 복사본을 즉시 호출 하 여 검색할 수 있습니다 합니다 [icordebugstackwalk:: Getcontext](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-getcontext-method.md) 메서드.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
