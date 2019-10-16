---
title: ICorDebugDataTarget::GetThreadContext 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget.GetThreadContext Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget::GetThreadContext
helpviewer_keywords:
- ICorDebugDataTarget::GetThreadContext method [.NET Framework debugging]
- GetThreadContext method, ICorDebugDataTarget interface [.NET Framework debugging]
ms.assetid: c8954268-1821-4b23-b665-dbb55f2af31b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2047929c52dbb7b0d780a4ea0f180bae48a3ce79
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67750388"
---
# <a name="icordebugdatatargetgetthreadcontext-method"></a>ICorDebugDataTarget::GetThreadContext 메서드
지정 된 스레드에 대 한 현재 스레드 컨텍스트를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetThreadContext(  
       [in] DWORD dwThreadID,  
       [in] ULONG32 contextFlags,  
       [in] ULONG32 contextSize,  
       [out, size_is(contextSize)] BYTE * pContext);  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwThreadID`  
 [in] 해당 컨텍스트를 검색할는 스레드의 식별자입니다. 식별자는 운영 체제에 의해 정의 됩니다.  
  
 `contextFlags`  
 [in] 컨텍스트의 부분 읽어들여야 함을 나타내는 플랫폼에 종속 된 플래그의 비트 조합입니다.  
  
 `contextSize`  
 [in] `pContext`의 크기입니다.  
  
 `pContext`  
 [out] 스레드 컨텍스트를 저장할 버퍼입니다.  
  
## <a name="remarks"></a>설명  
 Windows 플랫폼에서 `pContext` 이어야 합니다는 `CONTEXT` 구조 (WinNT.h에 정의 됨)으로 지정 된 컴퓨터 종류에 적합 합니다 [icordebugdatatarget:: Getplatform](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getplatform-method.md) 메서드. `contextFlags` 으로 동일한 값이 있어야 합니다 `ContextFlags` 필드는 `CONTEXT` 구조. `CONTEXT` 구조체가 프로세서별 대 한 자세한 내용은 WinNT.h 파일을 참조 하십시오.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugDataTarget 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
