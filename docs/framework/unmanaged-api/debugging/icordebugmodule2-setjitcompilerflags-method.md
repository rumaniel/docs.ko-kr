---
title: ICorDebugModule2::SetJITCompilerFlags 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.SetJITCompilerFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::SetJITCompilerFlags
helpviewer_keywords:
- ICorDebugModule2::SetJITCompilerFlags method [.NET Framework debugging]
- SetJITCompilerFlags method [.NET Framework debugging]
ms.assetid: ea574c84-c622-4589-9a14-b55771af5e06
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 114f4ff261d9612a81d17bf5b3df2f87323f77f2
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67764193"
---
# <a name="icordebugmodule2setjitcompilerflags-method"></a>ICorDebugModule2::SetJITCompilerFlags 메서드
이 ICorDebugModule2 컴파일하는 시간 (JIT)를 제어 하는 플래그를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetJITCompilerFlags (  
    [in] DWORD dwFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwFlags`  
 [in] 비트 조합 합니다 [CorDebugJITCompilerFlags](../../../../docs/framework/unmanaged-api/debugging/cordebugjitcompilerflags-enumeration.md) 열거형 값입니다.  
  
## <a name="remarks"></a>설명  
 경우는 `dwFlags` 값이 유효 하지는 `SetJITCompilerFlags` 메서드가 실패 합니다.  
  
 합니다 `SetJITCompilerFlags` 메서드 내 에서만 호출할 수 있습니다 합니다 [icordebugmanagedcallback:: Loadmodule](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-loadmodule-method.md) 이 모듈에 대 한 콜백입니다. 후에 메서드를 호출 하려고 합니다 `ICorDebugManagedCallback::LoadModule` 콜백이 전달 된 실패 합니다.  
  
 편집 하며 계속 하기 64 비트 또는 Win9x 플랫폼에서 지원 되지 않습니다. 따라서 호출 하는 경우는 `SetJITCompilerFlags` CORDEBUG_JIT_ENABLE_ENC 플래그가 설정 된이 두 플랫폼 중 하나에서 메서드 `dwFlags`의 `SetJITCompilerFlags` 메서드와 모든 메서드를 특정 편집 하며 계속 하기, 같은를 [ICorDebugModule2:: ApplyChanges](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule2-applychanges-method.md)에 실패 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
