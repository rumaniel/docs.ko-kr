---
title: ICorProfilerCallback::JITCompilationStarted 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCompilationStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCompilationStarted
helpviewer_keywords:
- JITCompilationStarted method [.NET Framework profiling]
- ICorProfilerCallback::JITCompilationStarted method [.NET Framework profiling]
ms.assetid: 31782b36-d311-4518-8f45-25f65385af5b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a5ba90ce4523fcc55fca3f84a78fa4cfeb6a93f0
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782823"
---
# <a name="icorprofilercallbackjitcompilationstarted-method"></a>ICorProfilerCallback::JITCompilationStarted 메서드
Just-in-time (JIT) 컴파일러에서 함수 컴파일을 시작 했다는 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT JITCompilationStarted(  
    [in] FunctionID functionId,  
    [in] BOOL       fIsSafeToBlock);  
```  
  
## <a name="parameters"></a>매개 변수  
 `functionId`  
 [in] 컴파일이 시작 되는 함수의 ID입니다.  
  
 `fIsSafeToBlock`  
 [in] 프로파일러 차단 여부를 나타내는 값을 런타임 작업에 영향을 줍니다. 값이 `true` 런타임에서이 콜백에서; 반환할 호출 스레드에 대 한 대기를 차단 않을 경우이 고, 그렇지 `false`합니다.  
  
 하지만 값 `true` 런타임 나쁜 영향을 주지, 프로 파일링 결과 기울일 수 있습니다.  
  
## <a name="remarks"></a>설명  
 둘 이상의 쌍을 받을 수 있기 `JITCompilationStarted` 하 고 [icorprofilercallback:: Jitcompilationfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md) 생성자를 호출 각 함수에 대 한 방식으로 인해 런타임 핸들 클래스입니다. 예를 들어, JIT 컴파일되나요 메서드 A는 런타임이 시작 하지만 클래스 B에 대 한 클래스 생성자를 실행 해야 합니다. 따라서 런타임에서 JIT 컴파일을 클래스 B에 대 한 생성자를 실행 합니다. 생성자는 실행 되는 동안 메서드 A 다시 JIT 컴파일할 수 하는 메서드를 호출을 하면 합니다. 이 시나리오에서는 첫 번째 메서드는 JIT 컴파일을 중단 됩니다. 그러나 두 하려고 JIT 컴파일되나요 메서드는 JIT 컴파일 이벤트를 사용 하 여 보고 됩니다. 프로파일러는 메서드에 대 한 Microsoft MSIL (intermediate language) 코드를 호출 하 여 대체 하려는 경우는 [icorprofilerinfo:: Setilfunctionbody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md) 메서드를 둘 다에 대해 이렇게 해야 `JITCompilationStarted` 이벤트 하지만 동일한 MSIL 블록을 사용할 수 있습니다 보십시오.  
  
 프로파일러는 두 스레드가 동시에 중인 콜백 하는 경우 JIT 콜백 시퀀스를 지원 해야 합니다. 예를 들어, 호출 스레드는 `JITCompilationStarted`합니다. 그러나 스레드는 호출 전에 `JITCompilationFinished`, 스레드 B 호출 [icorprofilercallback:: Exceptionsearchfunctionenter](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionsearchfunctionenter-method.md) 스레드 A의에서 함수 ID를 가진 `JITCompilationStarted` 콜백 합니다. 함수 ID는 아직 유효 하지 않은 것으로 보일 수 때문에 대 한 호출 `JITCompilationFinished` 프로파일러에 의해 아직 받지 했습니다. 그러나 이와 같은 경우 함수 ID가 잘못 되었습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [JITCompilationFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md)
