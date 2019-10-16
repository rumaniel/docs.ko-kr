---
title: ICorProfilerCallback::JITCachedFunctionSearchStarted 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCachedFunctionSearchStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCachedFunctionSearchStarted
helpviewer_keywords:
- JITCachedFunctionSearchStarted method [.NET Framework profiling]
- ICorProfilerCallback::JITCachedFunctionSearchStarted method [.NET Framework profiling]
ms.assetid: 5cba642c-0d80-48ee-889d-198c5044d821
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f4d35179b8ae35c03370cc3798609d6ed430cde3
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782848"
---
# <a name="icorprofilercallbackjitcachedfunctionsearchstarted-method"></a>ICorProfilerCallback::JITCachedFunctionSearchStarted 메서드
네이티브 이미지 생성기 (NGen.exe)를 사용 하 여 이전에 컴파일된 함수에 대 한 검색이 시작는 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT JITCachedFunctionSearchStarted(  
    [in]  FunctionID functionId,  
    [out] BOOL *pbUseCachedFunction);  
```  
  
## <a name="parameters"></a>매개 변수  
 `functionId`  
 [in] 검색이 수행 되는 함수의 ID입니다.  
  
 `pbUseCachedFunction`  
 [out] `true` (있는 경우) 실행 엔진에서 캐시 된 버전의 함수를 사용 해야 하는 경우이 고 그렇지 않으면 `false`합니다. 값이 `false`, 실행 엔진에서는 JIT 컴파일된 되지 않은 버전을 사용 하는 대신 함수 JIT 컴파일합니다.  
  
## <a name="remarks"></a>설명  
 .NET Framework 버전 2.0에에서는 `JITCachedFunctionSearchStarted` 및 [icorprofilercallback:: Jitcachedfunctionsearchfinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcachedfunctionsearchfinished-method.md) 콜백을 일반 NGen 이미지의 모든 함수에 대 한 걸 수 없습니다. 만 NGen 이미지의 프로필에 대 한 액세스에 최적화 된 이미지의 모든 함수에 대 한 콜백을 생성 됩니다. 그러나 추가 오버 헤드로 인해 프로파일러 요청 해야 프로파일러에 최적화 된 NGen 이미지를 컴파일된-just-in-time (JIT) 함수를 적용할 이러한 콜백을 사용 하려는 경우에 합니다. 그렇지 않은 경우 프로파일러 함수 정보를 수집 지연 전략을 사용 해야 합니다.  
  
 프로파일러는 프로 파일링 된 응용 프로그램의 여러 스레드가 동시에 동일한 메서드를 호출 되는 경우 지원 해야 합니다. 예를 들어 스레드는 호출 `JITCachedFunctionSearchStarted` 프로파일러를 설정 하 여 응답 *pbUseCachedFunction*JIT 컴파일을 FALSE로 합니다. 다음 호출 스레드가 [icorprofilercallback:: Jitcompilationstarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md) 하 고 [icorprofilercallback:: Jitcompilationfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md)합니다.  
  
 이제 B 호출 스레드 `JITCachedFunctionSearchStarted` 동일한 함수에 대 한 합니다. 프로파일러는 profiler가 스레드 A의 호출에 응답 하기 전에 스레드 B 콜백을 보내므로 두 번째 콜백 수신 프로파일러는 JIT 컴파일되나요 함수를 언급 하는 경우에 `JITCachedFunctionSearchStarted`합니다. 스레드 호출을 수행 하는 순서는 스레드의 예약 하는 방법에 따라 달라 집니다.  
  
 프로파일러 중복 콜백을 받으면에서 참조 값을 설정 해야이 `pbUseCachedFunction` 모든 중복 콜백에 대 한 동일한 값입니다. 즉, `JITCachedFunctionSearchStarted` 동일한 여러 번 호출 `functionId` 값 프로파일러 응답 해야 동일한 때마다 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
