---
title: FunctionIDMapper 함수
ms.date: 03/30/2017
api_name:
- FunctionIDMapper
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionIDMapper
helpviewer_keywords:
- FunctionIDMapper function [.NET Framework profiling]
ms.assetid: b8205b60-1893-4303-8cff-7ac5a00892aa
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b9dee1404a8da63208bba7b7529b16eabbee3254
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67745769"
---
# <a name="functionidmapper-function"></a>FunctionIDMapper 함수
함수는 지정 된 식별자에 사용할 대체 ID를 다시 매핑할 수는 프로파일러에 알립니다. 합니다 [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)를 [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md), 및 [FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md) 함수에 대 한 콜백 합니다. `FunctionIDMapper`를 통해 프로파일러는 해당 함수에 대한 콜백을 받을지 여부를 나타낼 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
UINT_PTR __stdcall FunctionIDMapper (  
    [in]  FunctionID  funcId,   
    [out] BOOL       *pbHookFunction  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `funcId`  
 [in] 다시 매핑할 함수 식별자입니다.  
  
 `pbHookFunction`  
 [out] 프로파일러를 설정 하는 값에 대 한 포인터 `true` 수신 하려는 경우 `FunctionEnter2`를 `FunctionLeave2`, 및 `FunctionTailcall2` 콜백을;이 값을 설정 하는 고, 그렇지 `false`합니다.  
  
## <a name="return-value"></a>반환 값  
 프로파일러는 실행 엔진이 대체 함수 식별자로 사용하는 값을 반환합니다. `false`가 `pbHookFunction`에 반환되지 않는 한 반환 값은 null일 수 없습니다. 이 고, 그렇지 null 반환 값에는 프로세스 중지를 포함 한 예기치 않은 결과가 생성 됩니다.  
  
## <a name="remarks"></a>설명  
 `FunctionIDMapper` 는 콜백 함수입니다. 프로파일러에 대 한 더 유용한 다른 식별자 함수 ID를 매핑할 프로파일러에 의해 구현 됩니다. `FunctionIDMapper` 지정된 된 함수에 사용할 대체 ID를 반환 합니다. 다음 실행 엔진에서 프로파일러를 다시 기존 함수 ID 외에도이 대체 ID를 전달 하 여 프로파일러 요청을 적용 합니다 `clientData` 의 매개 변수를 `FunctionEnter2`를 `FunctionLeave2`, 및 `FunctionTailcall2` 후크를 식별 하 후크 호출 되는 함수입니다.  
  
 사용할 수는 [icorprofilerinfo:: Setfunctionidmapper](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md) 의 구현을 지정 하는 방법의 `FunctionIDMapper` 함수입니다. 호출할 수 있습니다 합니다 `ICorProfilerInfo::SetFunctionIDMapper` 에서 수행 하는 한 번만 메서드를 권장 합니다 [icorprofilercallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md) 콜백 합니다.  
  
 기본적으로 가정는 프로파일러는 COR_PRF_MONITOR_ENTERLEAVE 플래그를 사용 하 여 설정 [icorprofilerinfo:: Seteventmask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)를 통해 후크를 설정 하 고 [icorprofilerinfo:: Setenterleavefunctionhooks](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setenterleavefunctionhooks-method.md) 또는 [ICorProfilerInfo2::SetEnterLeaveFunctionHooks2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md)를 받아야 합니다 `FunctionEnter2`를 `FunctionLeave2`, 및 `FunctionTailcall2` 모든 함수에 대 한 콜백을 합니다. 그러나 프로파일러 구현할 수 있습니다 `FunctionIDMapper` 선택적으로 특정 이러한 콜백을 수신 하지 않도록 설정 하 여 함수 `pbHookFunction` 에 `false`입니다.  
  
 프로파일러는 프로 파일링 된 응용 프로그램의 여러 스레드가 동시에 동일한 메서드/함수를 호출 하는 경우 허용 해야 합니다. 이러한 경우 프로파일러 여러 나타날 `FunctionIDMapper` 동일에 대 한 콜백을 `FunctionID`합니다. 프로파일러 해야 동일한 여러 번 호출 될 때이 콜백에서 동일한 값을 반환 하려면 특정 `FunctionID`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [SetFunctionIDMapper 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)
- [FunctionIDMapper2 함수](../../../../docs/framework/unmanaged-api/profiling/functionidmapper2-function.md)
- [FunctionEnter2 함수](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)
- [FunctionLeave2 함수](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)
- [FunctionTailcall2 함수](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)
- [프로파일링 전역 정적 함수](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
