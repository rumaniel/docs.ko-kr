---
title: ICorProfilerCallback4 인터페이스
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4
helpviewer_keywords:
- ICorProfilerCallback4 interface [.NET Framework profiling]
ms.assetid: 665f3cfc-cd6f-4880-906c-ea65ad384783
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3eb1f46900199db65be5d14c56bfc0b6f55bf269
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61598194"
---
# <a name="icorprofilercallback4-interface"></a>ICorProfilerCallback4 인터페이스
프로파일러에 대 한 정보를 전달 하는 CLR (공용 언어 런타임)를 사용 하는 콜백 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetReJITParameters 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-getrejitparameters-method.md)|코드 프로파일러를 새 다시 컴파일된 메서드 본문에 대 한 대체 코드 생성 플래그를 설정할 수 있습니다.|  
|[MovedReferences2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-movedreferences2-method.md)|압축 가비지 컬렉션의 결과로 힙에 있는 개체의 새 레이아웃을 보고합니다.|  
|[ReJITCompilationFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-rejitcompilationfinished-method.md)|Just-in-time (JIT) 컴파일러는 함수를 다시 컴파일하면 되었음을 프로파일러에 알립니다.|  
|[ReJITCompilationStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-rejitcompilationstarted-method.md)|함수를 다시 컴파일 (JIT)-just-in-time 컴파일러가 시작 했음을 프로파일러에 알립니다.|  
|[ReJITError 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-rejiterror-method.md)|다시 컴파일을 요청을 처리 하는 동안 발생 한 오류를 보고 합니다.|  
|[SurvivingReferences2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-survivingreferences2-method.md)|비압축 가비지 수집의 결과로 힙에 있는 개체의 레이아웃을 보고합니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
