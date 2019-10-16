---
title: ICorProfilerCallback4::ReJITCompilationStarted 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.ReJITCompilationStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::ReJITCompilationStarted
helpviewer_keywords:
- ReJITCompilationStarted method, ICorProfilerCallback4 interface [.NET Framework profiling]
- ICorProfilerCallback4::ReJITCompilationStarted method [.NET Framework profiling]
ms.assetid: 512fdd00-262a-4456-a075-365ef4133c4d
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 58293929b576493d3751f9ce30ba00cec92e180c
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67758171"
---
# <a name="icorprofilercallback4rejitcompilationstarted-method"></a>ICorProfilerCallback4::ReJITCompilationStarted 메서드
함수를 다시 컴파일 (JIT)-just-in-time 컴파일러가 시작 했음을 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ReJITCompilationStarted(   
    [in] FunctionID functionId,  
    [in] ReJITID    rejitId,  
    [in] BOOL       fIsSafeToBlock);  
```  
  
## <a name="parameters"></a>매개 변수  
 `functionId`  
 [in] JIT 컴파일러는 recompile을 시작 했음을 함수의 ID입니다.  
  
 `rejitId`  
 [in] 함수의 새 버전의 다시 컴파일 ID입니다.  
  
 `fIsSafeToBlock`  
 [in] `true` 차단 호출 스레드가이 콜백에서; 반환 될 때까지 대기할 런타임 시를 나타내려면 `false` 는 차단 영향을 주지 것입니다 런타임의 작업을 나타냅니다. 값 `true` 런타임에 영향을 주지 않으며 하지만 프로 파일링 결과 영향을 줄 수 있습니다.  
  
## <a name="remarks"></a>설명  
 둘 이상의 쌍을 받을 수 있기 `ReJITCompilationStarted` 하 고 [ReJITCompilationFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-rejitcompilationfinished-method.md) 메서드 호출 각 함수에 대 한 방식으로 인해 런타임 핸들 클래스 생성자입니다. 예를 들어 메서드는, 다시 컴파일 런타임이 시작 있지만 클래스 B에 대 한 클래스 생성자를 실행 해야 합니다. 따라서 런타임 클래스 B에 대 한 생성자를 다시 컴파일 및 실행 합니다. 생성자는 실행 되는 동안 메서드 A 다시 컴파일해야 하는 메서드를 호출을 하면 합니다. 이 시나리오에서는 첫 번째 메서드는 다시 중단 됩니다. 그러나 둘 다 JIT 다시 컴파일 이벤트를 사용 하 여이 보고 하는 메서드를 다시 컴파일할 하려고 합니다.  
  
 프로파일러는 두 스레드가 동시에 중인 콜백 하는 경우 JIT 다시 컴파일 콜백 시퀀스를 지원 해야 합니다. 그러나 예를 들어 스레드는 호출 `ReJITCompilationStarted`; 스레드는 호출 전에 [ReJITCompilationFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-rejitcompilationfinished-method.md), 스레드 B 호출 [icorprofilercallback:: Exceptionsearchfunctionenter](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionsearchfunctionenter-method.md) 함수 ID를 사용 하 여 `ReJITCompilationStarted` A. 스레드에 대 한 콜백 함수 ID는 아직 유효 하지 않은 것으로 보일 수 때문에 대 한 호출 [ReJITCompilationFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-rejitcompilationfinished-method.md) 프로파일러에 의해 아직 받지 했습니다. 그러나이 경우 함수 ID는 유효 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback4 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)
- [JITCompilationFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md)
- [ReJITCompilationFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-rejitcompilationfinished-method.md)
