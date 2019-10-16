---
title: ICorDebugRemote::CreateProcessEx 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugRemote.CreateProcessEx
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugRemoteTarget::CreateProcessEx
helpviewer_keywords:
- CreateProcessEx method, ICorDebugRemote interface [.NET Framework debugging]
- ICorDebugRemote::CreateProcessEx method [.NET Framework debugging]
ms.assetid: 41af93c7-e448-4251-8d4d-413d38c635f2
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d05384af8201fae8cf81650d38c99a5c44e6bd16
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67744779"
---
# <a name="icordebugremotecreateprocessex-method"></a>ICorDebugRemote::CreateProcessEx 메서드
디버거에서 원격 컴퓨터의 프로세스를 시작합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateProcessEx (  
    [in]  ICorDebugRemoteTarget*      pRemoteTarget,  
    [in]  LPCWSTR                     lpApplicationName,  
    [in]  LPWSTR                      lpCommandLine,  
    [in]  LPSECURITY_ATTRIBUTES       lpProcessAttributes,  
    [in]  LPSECURITY_ATTRIBUTES       lpThreadAttributes,  
    [in]  BOOL                        bInheritHandles,  
    [in]  DWORD                       dwCreationFlags,  
    [in]  PVOID                       lpEnvironment,  
    [in]  LPCWSTR                     lpCurrentDirectory,  
    [in]  LPSTARTUPINFOW              lpStartupInfo,  
    [in]  LPPROCESS_INFORMATION       lpProcessInformation,  
    [in]  CorDebugCreateProcessFlags  debuggingFlags,  
    [out] ICorDebugProcess**          ppProcess  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pRemoteTarget`  
 [in] 에 대 한 포인터를 [ICorDebugRemoteTarget 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugremotetarget-interface.md)합니다. 프로세스를 시작할 수는 원격 컴퓨터를 확인 하는 데 사용 합니다.  
  
 `lpApplicationName`  
 [in] 시작된 프로세스에서 실행 될 모듈을 지정 하는 null로 끝나는 문자열에 대 한 포인터입니다. 모듈 호출 프로세스의 보안 컨텍스트에서 실행 됩니다.  
  
 `lpCommandLine`  
 [in] 시작된 프로세스에서 실행할 명령줄을 지정 하는 null로 끝나는 문자열에 대 한 포인터입니다.  
  
 `lpProcessAttributes`  
 [in] 원격 디버깅을 위해 사용 되지 않습니다.  
  
 `lpThreadAttributes`  
 [in] 원격 디버깅을 위해 사용 되지 않습니다.  
  
 `bInheritHandles`  
 [in] 원격 디버깅을 위해 사용 되지 않습니다.  
  
 `dwCreationFlags`  
 [in] 원격 디버깅을 위해 사용 되지 않습니다.  
  
 `lpEnvironment`  
 [in] 새 프로세스에 대 한 환경 블록에 대 한 포인터입니다.  
  
 `lpCurrentDirectory`  
 [in] 프로세스에 대 한 현재 디렉터리에 전체 경로 지정 하는 null로 끝나는 문자열에 대 한 포인터입니다. 이 매개 변수가 null 이면 새 프로세스 호출 프로세스와 같은 현재 드라이브 및 디렉터리 포함 됩니다.  
  
 `lpStartupInfo`  
 [in] 원격 디버깅을 위해 사용 되지 않습니다.  
  
 `lpProcessInformation`  
 [in] 원격 디버깅을 위해 사용 되지 않습니다.  
  
 `debuggingFlags`  
 [in] 원격 디버깅을 위해 사용 되지 않습니다.  
  
 `ppProcess`  
 [out] 프로세스를 나타내는 "ICorDebugProcess 인터페이스" 개체의 주소에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 S_OK  
 디버깅에 대 한 원격 컴퓨터에 반환 된 "ICorDebugProcess 인터페이스" 프로세스를 시작 했습니다.  
  
 E_FAIL(또는 다른 E_ 반환 코드)  
 원격 컴퓨터의 프로세스를 시작 하 고 디버깅에 대 한 "ICorDebugProcess 인터페이스"를 반환할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 Silverlight에는 혼합 모드 디버깅이 지원 되지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET framework 버전:** 4.5, 4, 3.5 SP1  
  
## <a name="see-also"></a>참고자료

- [ICorDebugRemote 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugremote-interface.md)
- [ICorDebug 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
