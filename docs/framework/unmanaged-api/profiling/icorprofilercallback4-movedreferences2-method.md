---
title: ICorProfilerCallback4::MovedReferences2 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.MovedReferences2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::MovedReferences2
helpviewer_keywords:
- MovedReferences2 method, ICorProfilerCallback4 interface [.NET Framework profiling]
- ICorProfilerCallback4::MovedReferences2 method [.NET Framework profiling]
ms.assetid: d17a065b-5bc6-4817-b3e1-1e413fcb33a8
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e676d03efc950ce911bce43e15322d1f9882d0fd
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67758222"
---
# <a name="icorprofilercallback4movedreferences2-method"></a>ICorProfilerCallback4::MovedReferences2 메서드
압축 가비지 수집의 결과로 힙에 있는 개체의 새 레이아웃을 보고하려고 호출됩니다. 이 메서드는 프로파일러 구현에 [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) 인터페이스입니다. 이 콜백은 대체 합니다 [icorprofilercallback:: Movedreferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md) 메서드를 더 큰 범위의 길이가 ulong에서으로 표현 될 수 있습니다 어떤 초과 하는 개체를 보고할 수 있어.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT MovedReferences2(  
    [in]  ULONG  cMovedObjectIDRanges,  
    [in, size_is(cMovedObjectIDRanges)] ObjectID oldObjectIDRangeStart[] ,  
    [in, size_is(cMovedObjectIDRanges)] ObjectID newObjectIDRangeStart[] ,  
    [in, size_is(cMovedObjectIDRanges)] SIZE_T    cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a>매개 변수  
 `cMovedObjectIDRanges`  
 [in] 압축 가비지 컬렉션 후에 이동된 연속 개체 블록 수입니다. 즉, `cMovedObjectIDRanges` 값은 `oldObjectIDRangeStart`, `newObjectIDRangeStart` 및 `cObjectIDRangeLength` 배열의 총 크기입니다.  
  
 `MovedReferences2`의 다음 세 인수는 병렬 배열입니다. 즉, `oldObjectIDRangeStart[i]`, `newObjectIDRangeStart[i]` 및 `cObjectIDRangeLength[i]`는 모두 단일 연속 개체 블록과 관련이 있습니다.  
  
 `oldObjectIDRangeStart`  
 [in] 메모리에서 연속 라이브 개체 블록의 이전(가비지 수집 전) 시작 주소를 각각 나타내는 `ObjectID` 값의 배열입니다.  
  
 `newObjectIDRangeStart`  
 [in] 메모리에서 연속 라이브 개체 블록의 새(가비지 컬렉션 후) 시작 주소를 각각 나타내는 `ObjectID` 값의 배열입니다.  
  
 `cObjectIDRangeLength`  
 [in] 메모리의 연속 개체 블록의 크기를 각각 나타내는 정수 배열입니다.  
  
 크기는 `oldObjectIDRangeStart` 및 `newObjectIDRangeStart` 배열에서 참조된 각 블록에 대해 지정됩니다.  
  
## <a name="remarks"></a>설명  
 압축 가비지 수집기는 데드 개체가 사용한 메모리를 회수하고 확보된 공간을 압축합니다. 따라서 라이브 개체가 힙 내에서 이동될 수 있고 이전 알림으로 분산된 `ObjectID` 값이 변경될 수 있습니다.  
  
 기존 `ObjectID` 값(`oldObjectID`)이 다음 범위 내에 있다고 가정합니다.  
  
 `oldObjectIDRangeStart[i]` <= `oldObjectID` < `oldObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 이 경우 범위 시작부터 개체 시작까지 오프셋은 다음과 같습니다.  
  
 `oldObjectID` - `oldObjectRangeStart[i]`  
  
 다음 범위에 있는 `i` 값에 대해  
  
 0 <= `i` < `cMovedObjectIDRanges`  
  
 새 `ObjectID`를 다음과 같이 계산할 수 있습니다.  
  
 `newObjectID` = `newObjectIDRangeStart[i]` + (`oldObjectID` – `oldObjectIDRangeStart[i]`)  
  
 콜백 자체가 진행되는 동안 `MovedReferences2`를 통해 전달된 `ObjectID` 값은 유효하지 않습니다. 가비지 수집기가 이전 위치에서 새 위치로 개체를 이동하는 중일 수 있기 때문입니다. 그러므로 프로파일러는 `MovedReferences2` 호출 중에 개체 검사를 시도하지 않아야 합니다. A [ICorProfilerCallback2::GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md) 콜백 나타내고 모든 개체가 새 위치로 이동 된 검사를 수행할 수 있습니다.  
  
 프로파일러 둘 다 구현 하는 경우는 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 하며 [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) 인터페이스는 `MovedReferences2` 메서드 전에 호출 됩니다는 [ICorProfilerCallback:: MovedReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md) 방법 이지만 경우에만 `MovedReferences2` 메서드가 성공적으로 반환 합니다. 프로파일러는 두 번째 메서드 호출을 방지하기 위해 `MovedReferences2` 메서드에서 실패를 나타내는 HRESULT를 반환할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [MovedReferences 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md)
- [ICorProfilerCallback4 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
