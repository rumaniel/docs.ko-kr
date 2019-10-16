---
title: ICorDebugRemote::DebugActiveProcessEx 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugRemote.DebugActiveProcessEx
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugRemoteTarget::DebugActiveProcessEx
helpviewer_keywords:
- ICorDebugRemote::DebugActiveProcessEx method [.NET Framework debugging]
- DebugActiveProcessEx method, ICorDebugRemote interface [.NET Framework debugging]
ms.assetid: b0df5c5d-9a2e-47bf-894c-6f8a9fe24a1f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 13371d15c8b29f9ef93cc4af87acf85029404644
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67744760"
---
# <a name="icordebugremotedebugactiveprocessex-method"></a>ICorDebugRemote::DebugActiveProcessEx 메서드
디버거에서 원격 컴퓨터의 프로세스를 시작합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DebugActiveProcessEx (  
    [in]  ICorDebugRemoteTarget *   pRemoteTarget,  
    [in]  DWORD                     dwProcessId,  
    [in]  BOOL                      fWin32Attach,  
    [out] ICorDebugProcess **       ppProcess  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pRemoteTarget`  
 [in] 에 대 한 포인터를 [ICorDebugRemoteTarget 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugremotetarget-interface.md)합니다. 이 매개 변수를 사용 하 여 프로세스가 실행 중인 컴퓨터를 확인 합니다.  
  
 `id`  
 [in] 디버거를 연결할를 프로세스의 ID입니다.  
  
 `win32Attach`  
 [in] `true` 디버거 프로세스에 대 한 Win32 디버거 처럼 동작 하며 관리 되지 않는 콜백을; 디스패치 하는 경우이 고, 그렇지 `false`합니다.  
  
 `ppProcess`  
 [out] 디버거가 연결 된 프로세스를 나타내는 "ICorDebugProcess" 개체의 주소에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 S_OK  
 원격 컴퓨터의 프로세스에 연결 했습니다.  
  
 E_FAIL(또는 다른 E_ 반환 코드)  
 원격 컴퓨터의 프로세스에 연결할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 Silverlight에는 혼합 모드 디버깅이 지원 되지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET framework 버전:** 4.5, 4, 3.5 SP1  
  
## <a name="see-also"></a>참고자료

- [ICorDebugRemote 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugremote-interface.md)
- [ICorDebug 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
