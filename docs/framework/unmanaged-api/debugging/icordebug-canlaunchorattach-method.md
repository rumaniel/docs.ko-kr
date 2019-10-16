---
title: ICorDebug::CanLaunchOrAttach 메서드
ms.date: 03/30/2017
api_name:
- ICorDebug.CanLaunchOrAttach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::CanLaunchOrAttach
helpviewer_keywords:
- ICorDebug::CanLaunchOrAttach method [.NET Framework debugging]
- CanLaunchOrAttach method [.NET Framework debugging]
ms.assetid: ca7723db-7c07-4cdd-bd92-fba34928b623
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: af933be9edc0d0fe7249f33800fe259ddc779aeb
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67738322"
---
# <a name="icordebugcanlaunchorattach-method"></a>ICorDebug::CanLaunchOrAttach 메서드
새 프로세스를 시작 하거나 지정한 기존 프로세스에 연결 하는 현재 컴퓨터 및 런타임 구성 컨텍스트 내에서 가능한 지 여부를 나타내는 HRESULT를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CanLaunchOrAttach (  
    [in] DWORD      dwProcessId,  
    [in] BOOL       win32DebuggingEnabled  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwProcessId`  
 [in] 기존 프로세스의 ID입니다.  
  
 `win32DebuggingEnabled`  
 [in] 전달 `true` Win32 디버깅 사용을 시작 하려고 하거나 Win32 디버깅, 그렇지 않으면 연결을 전달 하면 `false`합니다.  
  
## <a name="return-value"></a>반환 값  
 디버깅 서비스를 확인 하는 새 프로세스를 시작 하거나 지정된 된 프로세스에 연결 하는 경우 S_OK이 현재 컴퓨터 및 런타임 구성에 대 한 정보 지정 가능 합니다. 가능한 HRESULT 값은:  
  
- S_OK  
  
- CORDBG_E_DEBUGGING_NOT_POSSIBLE  
  
- CORDBG_E_KERNEL_DEBUGGER_PRESENT  
  
- CORDBG_E_KERNEL_DEBUGGER_ENABLED  
  
## <a name="remarks"></a>설명  
 이 메서드는 순수 알림입니다. 인터페이스는 중지 되지 것입니다 하에서 시작 또는에서 반환 된 값에 관계 없이 프로세스에 연결 `CanLaunchOrAttach`합니다.  
  
 Win32 디버깅이 설정 된 시작 또는 Win32 디버깅 하도록 설정한 연결을 전달 하려는 경우 `true` 에 대 한 `win32DebuggingEnabled`합니다. 반환 된 HRESULT `CanLaunchOrAttach` 이 옵션을 사용 하는 경우 다를 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebug 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)
