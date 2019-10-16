---
title: ICorProfilerCallback::ManagedToUnmanagedTransition 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ManagedToUnmanagedTransition
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ManagedToUnmanagedTransition
helpviewer_keywords:
- ManagedToUnmanagedTransition method [.NET Framework profiling]
- ICorProfilerCallback::ManagedToUnmanagedTransition method [.NET Framework profiling]
ms.assetid: ef3cd619-912d-40c5-a449-03ba02a39ee7
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 277e035ab542f895ca700ecd5f3205cc757c9ddd
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769302"
---
# <a name="icorprofilercallbackmanagedtounmanagedtransition-method"></a>ICorProfilerCallback::ManagedToUnmanagedTransition 메서드
관리 코드에서 비관리 코드로 전환 되었음을 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ManagedToUnmanagedTransition(  
    [in] FunctionID functionId,  
    [in] COR_PRF_TRANSITION_REASON reason);  
```  
  
## <a name="parameters"></a>매개 변수  
 `functionId`  
 [in] 호출 되는 함수의 ID입니다.  
  
 `reason`  
 [in] 값을 [COR_PRF_TRANSITION_REASON](../../../../docs/framework/unmanaged-api/profiling/cor-prf-transition-reason-enumeration.md) 전환 또는 관리 되는 함수에 의해 관리 되지 않는 호출에서 반환 된 관리 코드에서 비관리 코드 호출으로 인해 발생 했는지 여부를 나타내는 열거형입니다.  
  
## <a name="remarks"></a>설명  
 경우 변수의 `reason` COR_PRF_TRANSITION_CALL, 함수는 관리 되지 않는 함수는 되지 컴파일된-just-in-time 컴파일러를 사용 하 여 ID가 됩니다. 이름, 일부 메타 데이터 등, 관련 기본 정보를 포함 하는 관리 되지 않는 함수입니다. 암시적 플랫폼을 사용 하 여 관리 되지 않는 함수를 호출한 경우 호출 (PInvoke), 런타임에서 호출의 대상 및의 값을 확인할 수 없습니다 `functionId` null이 됩니다. 암시적 PInvoke에 대 한 자세한 내용은 참조 하세요. [사용 C++ (암시적 PInvoke) Interop](/cpp/dotnet/using-cpp-interop-implicit-pinvoke)합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [UnmanagedToManagedTransition 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-unmanagedtomanagedtransition-method.md)
- [C++에서 명시적 PInvoke 사용(DllImport 특성)](/cpp/dotnet/using-explicit-pinvoke-in-cpp-dllimport-attribute)
