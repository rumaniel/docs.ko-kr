---
title: ICorProfilerCallback::UnmanagedToManagedTransition 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.UnmanagedToManagedTransition
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::UnmanagedToManagedTransition
helpviewer_keywords:
- ICorProfilerCallback::UnmanagedToManagedTransition method [.NET Framework profiling]
- UnmanagedToManagedTransition method [.NET Framework profiling]
ms.assetid: ade2cc01-9b81-4e09-a5f9-b3b9dda27e96
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7fa7dfe101b07ae6eb8d58daad85954f0ce29b02
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747049"
---
# <a name="icorprofilercallbackunmanagedtomanagedtransition-method"></a>ICorProfilerCallback::UnmanagedToManagedTransition 메서드
비관리 코드에서 관리 코드로 전환 되었음을 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT UnmanagedToManagedTransition(  
    [in] FunctionID functionId,  
    [in] COR_PRF_TRANSITION_REASON reason);  
```  
  
## <a name="parameters"></a>매개 변수  
 `functionId`  
 [in] 호출 되는 함수의 ID입니다.  
  
 `reason`  
 [in] 값을 [COR_PRF_TRANSITION_REASON](../../../../docs/framework/unmanaged-api/profiling/cor-prf-transition-reason-enumeration.md) 전환으로 관리 되는 호출 하는 관리 되지 않는 함수에서 반환 된 또는 비관리 코드에서 관리 코드로 호출으로 인해 발생 했는지 여부를 나타내는 열거형입니다.  
  
## <a name="remarks"></a>설명  
 경우 값 `reason` COR_PRF_TRANSITION_RETURN 됩니다 및 `functionId` null이 아닌 ID는 관리 되지 않는 함수 및 됩니다 하지 컴파일되지 않은 시간 (JIT) 컴파일러를 사용 하는 함수입니다. 관리 되지 않는 함수는 그와 관련 된 이름 및 일부 메타 데이터와 같은 몇 가지 기본 정보를 갖고 있습니다.  
  
 경우 값 `reason` COR_PRF_TRANSITION_CALL는 (즉, 관리 되는 함수) 호출된 된 함수가 아직 JIT 컴파일 가능한 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ManagedToUnmanagedTransition 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-managedtounmanagedtransition-method.md)
- [C++에서 명시적 PInvoke 사용(DllImport 특성)](/cpp/dotnet/using-explicit-pinvoke-in-cpp-dllimport-attribute)
- [C++ Interop 사용(암시적 PInvoke)](/cpp/dotnet/using-cpp-interop-implicit-pinvoke)
