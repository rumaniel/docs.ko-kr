---
title: ICorProfilerFunctionControl::SetCodegenFlags 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl.SetCodegenFlags
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl::SetCodegenFlags
helpviewer_keywords:
- ICorProfilerFunctionControl::SetCodegenFlags method [.NET Framework profiling]
- SetCodegenFlags method, ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: a2d5daa5-b990-4ae5-bf2a-c0862fe58bd7
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e4103925462732fa8ddc509a9538ef5b485266a6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67780370"
---
# <a name="icorprofilerfunctioncontrolsetcodegenflags-method"></a>ICorProfilerFunctionControl::SetCodegenFlags 메서드
하나 이상의 플래그를 설정 합니다 [COR_PRF_CODEGEN_FLAGS](../../../../docs/framework/unmanaged-api/profiling/cor-prf-codegen-flags-enumeration.md) 다시 컴파일된 함수는-just-in-time (JIT)에 대 한 코드 생성을 제어 하는 열거형입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetCodegenFlags(  
    [in] DWORD flags);  
```  
  
## <a name="parameters"></a>매개 변수  
 `flags`  
 [in] 하나 이상의 플래그를 [COR_PRF_CODEGEN_FLAGS](../../../../docs/framework/unmanaged-api/profiling/cor-prf-codegen-flags-enumeration.md) 열거형입니다.  
  
## <a name="remarks"></a>설명  
 프로파일러를 통해이 인터페이스의 인스턴스를 가져오고 합니다 [ICorProfilerCallback4::GetReJITParameters](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-getrejitparameters-method.md) 콜백 합니다. `SetCodegenFlags` 프로파일러가 다시 컴파일된 함수에 대 한 코드 생성을 제어할 수 있습니다. 다른 모든 JIT 다시 컴파일 매개 변수에서와 마찬가지로 코드 생성 플래그를 함수의 모든 인스턴스에 적용 됩니다.  
  
 JIT 컴파일러는 함수를 컴파일할 때 다른 원본에서 지정 된 다른 플래그와 함께 이러한 컴파일 플래그를 고려 합니다.  다른 원본 디버거, 전역 플래그를 사용 하 여 시작 하 여 프로파일러에 의해 설정 된 [icorprofilerinfo:: Seteventmask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md) 메서드 (값을 사용 하 여 `COR_PRF_DISABLE_INLINING` 및 `COR_PRF_DISABLE_OPTIMIZATIONS`), 및 프로파일러 [ Icorprofilercallback:: Jitinlining](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitinlining-method.md) 콜백 합니다.  JIT 컴파일러 최적화의 최소 크기를 요청 하는 원본에 대 한 우선 순위를 제공 합니다.  예를 들어, 프로파일러를 지정 하는 경우 `COR_PRF_DISABLE_INLINING` 시작 시 하지만 지정 하지 않습니다 `COR_PRF_CODEGEN_DISABLE_INLINING` 에 [icorprofilerfunctioncontrol:: Setcodegenflags](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-setcodegenflags-method.md) 콜백, 인라인 처리는 여전히 사용할 수 없습니다.  마찬가지로, 프로파일러를 지정 하지 않는 경우 `COR_PRF_CODEGEN_DISABLE_INLINING` 에서 `SetCodegenFlags`, 하지만 다음 비활성화를 사용 하 여 인라인 합니다 [icorprofilercallback:: Jitinlining](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitinlining-method.md) 콜백, 인라인을 사용할 수 없습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerFunctionControl 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-interface.md)
