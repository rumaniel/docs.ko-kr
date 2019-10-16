---
title: ICorProfilerInfo4::RequestRevert 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.RequestRevert
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::RequestRevert
helpviewer_keywords:
- RequestRevert method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::RequestRevert method [.NET Framework profiling]
ms.assetid: 70261da5-5933-4e25-9de0-ddf51cba56cc
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5e74cb663f968cc9b1b04a912307e3b4a12e86d4
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67748667"
---
# <a name="icorprofilerinfo4requestrevert-method"></a>ICorProfilerInfo4::RequestRevert 메서드
지정된 함수의 모든 인스턴스를 원래 버전으로 되돌립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT RequestRevert (  
   [in] ULONG    cFunctions,  
   [in, size_is(cFunctions)]  ModuleID    moduleIds[],  
   [in, size_is(cFunctions)]  mdMethodDef methodIds[],  
   [out, size_is(cFunctions)]  HRESULT status[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cFunctions`  
 [in] 되돌릴 함수 개수입니다.  
  
 `moduleIds`  
 [in] 되돌릴 함수를 식별하는 (`module`, `methodDef`) 쌍의 `moduleId` 부분을 지정합니다.  
  
 `methodIds`  
 [in] 되돌릴 함수를 식별하는 (`module`, `methodDef`) 쌍의 `methodId` 부분을 지정합니다.  
  
 `status`  
 [out] 이 항목의 뒷부분에 있는 "상태 HRESULT" 섹션에 나열된 HRESULT 배열입니다. 각 HRESULT는 병렬 배열 `moduleIds` 및 `methodIds`에 지정된 각 함수의 되돌리기 성공 또는 실패를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|모든 요청을 되돌리려고 했습니다. 그러나 반환된 상태 배열을 검사하여 성공적으로 되돌려진 함수를 확인해야 합니다.|  
|CORPROF_E_CALLBACK4_REQUIRED|프로파일러를 구현 해야 합니다 [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) 지원 되는 데이 호출에 대 한 인터페이스입니다.|  
|CORPROF_E_REJIT_NOT_ENABLED|JIT 다시 컴파일이 사용하도록 설정되지 않았습니다. 초기화 하는 동안 JIT 다시 컴파일을 사용 하 여 설정 해야 합니다는 [icorprofilerinfo:: Seteventmask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md) 설정 하는 메서드를 `COR_PRF_ENABLE_REJIT` 플래그입니다.|  
|E_INVALIDARG|`cFunctions`가 0이거나 `moduleIds` 또는 `methodIds`가 `NULL`입니다.|  
|E_OUTOFMEMORY|메모리 부족 때문에 CLR에서 요청을 완료하지 못했습니다.|  
  
## <a name="status-hresults"></a>상태 HRESULTS  
  
|상태 배열 HRESULT|Description|  
|--------------------------|-----------------|  
|S_OK|해당 함수를 성공적으로 되돌렸습니다.|  
|E_INVALIDARG|`moduleID` 또는 `methodDef` 매개 변수가 `NULL`인 경우|  
|CORPROF_E_DATAINCOMPLETE|모듈은 아직 완전히 로드되지 않았거나 언로드되는 중입니다.|  
|CORPROF_E_MODULE_IS_DYNAMIC|지정한 모듈은 동적으로 생성되었습니다(예: `Reflection.Emit`에 의해). 따라서 이 메서드가 모듈을 지원하지 않습니다.|  
|CORPROF_E_ACTIVE_REJIT_REQUEST_NOT_FOUND|해당하는 활성 다시 컴파일 요청이 없기 때문에 CLR이 지정한 함수를 되돌리지 못했습니다. 다시 컴파일이 요청되지 않았거나 함수가 이미 되돌려졌습니다.|  
|기타|운영 체제가 CLR의 제어 범위를 벗어난 오류를 반환했습니다. 예를 들어 메모리 페이지의 액세스 보호를 변경하려는 시스템 호출이 실패하면 운영 체제 오류가 표시됩니다.|  
  
## <a name="remarks"></a>설명  
 되돌려진 함수 인스턴스 중 하나를 다음에 호출하면 함수의 원래 버전이 실행됩니다. 함수가 이미 실행되고 있으면 실행 중인 버전의 실행을 완료합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo4 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
