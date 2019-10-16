---
title: ICorDebugProcess2::SetDesiredNGENCompilerFlags 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.SetDesiredNGENCompilerFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::SetDesiredNGENCompilerFlags
helpviewer_keywords:
- ICorDebugProcess2::SetDesiredNGENCompilerFlags method [.NET Framework debugging]
- SetDesiredNGENCompilerFlags method [.NET Framework debugging]
ms.assetid: 98320175-7c5e-4dbb-8683-86fa82e2641f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3582ebf2acee02d49aabafb03604c84249c4ce13
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747380"
---
# <a name="icordebugprocess2setdesiredngencompilerflags-method"></a>ICorDebugProcess2::SetDesiredNGENCompilerFlags 메서드
미리 컴파일된 이미지를 현재 프로세스에 해당 이미지를 로드 하려면 런타임에 대 한 순서 대로 포함 되어야 하는 플래그를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetDesiredNGENCompilerFlags (  
    [in] DWORD    pdwFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pdwFlags`  
 [in] 값을 [CorDebugJITCompilerFlags](../../../../docs/framework/unmanaged-api/debugging/cordebugjitcompilerflags-enumeration.md) 컴파일러 플래그를 지정 하는 열거형 올바른 미리 컴파일된 이미지를 선택 하는 데 사용 합니다.  
  
## <a name="remarks"></a>설명  
 `SetDesiredNGENCompilerFlags` 메서드는 런타임에서이 프로세스에 해당 이미지를 로드 하는 미리 컴파일된 이미지에 포함 되어야 하는 플래그를 지정 합니다. 이 메서드에 의해 설정 된 플래그는 올바른 미리 컴파일된 이미지 선택에 사용 됩니다. 이러한 이미지가 없는 경우 런타임에 로드 됩니다 Microsoft 중간 언어 (MSIL) 이미지 및 (JIT)-just-in-time 컴파일러 대신 합니다. 이 경우 디버거가 계속 사용 해야 합니다는 [ICorDebugModule2::SetJITCompilerFlags](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule2-setjitcompilerflags-method.md) JIT 컴파일에 대해 필요에 따라 플래그를 설정 하는 방법입니다.  
  
 이미지를 로드 하지만 약간의 JIT 컴파일을 수행 해야 합니다 (될 경우 이미지는 제네릭을 포함 하는 경우) 해당 이미지에 대 한 경우에 지정 된 컴파일러 플래그는 `SetDesiredNGENCompilerFlags` 메서드 추가 JIT 컴파일으로 적용 됩니다.  
  
 합니다 `SetDesiredNGENCompilerFlags` 메서드를 호출 하는 동안 합니다 [icordebugmanagedcallback:: Createprocess](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createprocess-method.md) 콜백 합니다. 호출 하려고 합니다 `SetDesiredNGENCompilerFlags` 나중에 메서드가 실패 합니다. 또한에 정의 된 잘못 된 플래그를 설정 하려고 시도 합니다 `CorDebugJITCompilerFlags` 열거형 또는 지정된 된 프로세스에 적합 하지 않은 실패 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebug 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)
- [ICorDebugManagedCallback 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)
