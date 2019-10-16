---
title: FunctionLeave2 함수
ms.date: 03/30/2017
api_name:
- FunctionLeave2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave2
helpviewer_keywords:
- FunctionLeave2 function [.NET Framework profiling]
ms.assetid: 8cdac941-8b94-4497-b874-4e571785f3fe
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 124921f2f99ca4d8da88cc3713624383e225a26f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781262"
---
# <a name="functionleave2-function"></a>FunctionLeave2 함수
함수에 대 한 호출자에 게 반환 하는 것을 스택 프레임 및 함수 반환 값에 대 한 정보를 제공 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
void __stdcall FunctionLeave2 (  
    [in]  FunctionID                        funcId,  
    [in]  UINT_PTR                          clientData,  
    [in]  COR_PRF_FRAME_INFO                func,  
    [in]  COR_PRF_FUNCTION_ARGUMENT_RANGE  *retvalRange  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `funcId`  
 [in] 식별자를 반환 하는 함수입니다.  
  
 `clientData`  
 [in] 프로파일러를 통해 이전에 지정 하는 매핑된 함수 식별자를 [FunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/functionidmapper-function.md) 함수입니다.  
  
 `func`  
 [in] `COR_PRF_FRAME_INFO` 스택 프레임에 대 한 정보를 가리키는 값입니다.  
  
 프로파일러에 실행 엔진으로 다시 전달할 수 있는 불투명 핸들로이 처리 해야 합니다 [ICorProfilerInfo2::GetFunctionInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md) 메서드.  
  
 `retvalRange`  
 [in] 에 대 한 포인터를 [COR_PRF_FUNCTION_ARGUMENT_RANGE](../../../../docs/framework/unmanaged-api/profiling/cor-prf-function-argument-range-structure.md) 함수의 반환 값의 메모리 위치를 지정 하는 구조입니다.  
  
 반환 값 정보에 액세스 하기 위해는 `COR_PRF_ENABLE_FUNCTION_RETVAL` 플래그를 설정 해야 합니다. 프로파일러를 사용 하 여 수를 [icorprofilerinfo:: Seteventmask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md) 이벤트 플래그를 설정 하는 방법입니다.  
  
## <a name="remarks"></a>설명  
 값을 `func` 및 `retvalRange` 매개 변수가 후 올바르면는 `FunctionLeave2` 함수 반환 값이 변경 될 수 있습니다 또는 제거 하기 때문에 합니다.  
  
 `FunctionLeave2` 함수 콜백을 구현 해야 합니다. 구현을 사용 해야 합니다 `__declspec`(`naked`) 저장소 클래스 특성입니다.  
  
 실행 엔진은이 함수를 호출 하기 전에 모든 레지스터를 저장 하지 않습니다.  
  
- 항목에는 부동 소수점 FPU (단위)에 포함 하 여 사용 하는 모든 레지스터를 저장 해야 합니다.  
  
- 종료 시 스택의 호출자에 의해 푸시된 모든 매개 변수에 팝 하 여 복원 해야 합니다.  
  
 구현의 `FunctionLeave2` 가비지 수집 지연 될 수 있으므로 차단 하지 않아야 합니다. 구현 해야 스택의 가비지 컬렉션에 게 친숙 한 상태의 수 없을 수도 가비지 수집을 시도 하지 않습니다. 런타임이 될 때까지 차단 됩니다 가비지 수집을 시도 하는 경우 `FunctionLeave2` 반환 합니다.  
  
 또한는 `FunctionLeave2` 함수를 호출 해서는 안 관리 코드로 또는는 관리 되는 메모리를 할당 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [FunctionEnter2 함수](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)
- [FunctionTailcall2 함수](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)
- [SetEnterLeaveFunctionHooks2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [프로파일링 전역 정적 함수](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
