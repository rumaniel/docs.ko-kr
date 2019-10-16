---
title: ICorProfilerCallback2::GarbageCollectionStarted 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.GarbageCollectionStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::GarbageCollectionStarted
helpviewer_keywords:
- GarbageCollectionStarted method [.NET Framework profiling]
- ICorProfilerCallback2::GarbageCollectionStarted method [.NET Framework profiling]
ms.assetid: 44eef087-f21f-4fe2-b481-f8a0ee022e7d
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f4f639f9794002748e1019821514c546e4f4429f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67746876"
---
# <a name="icorprofilercallback2garbagecollectionstarted-method"></a>ICorProfilerCallback2::GarbageCollectionStarted 메서드
가비지 수집이 시작 되었습니다 코드 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GarbageCollectionStarted(  
    [in] int cGenerations,  
    [in, size_is(cGenerations), length_is(cGenerations)] BOOL generationCollected[],  
    [in] COR_PRF_GC_REASON reason);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cGenerations`  
 [in] 에 있는 항목의 총 수를 `generationCollected` 배열입니다.  
  
 `generationCollected`  
 [in] 부울 값의 배열을 `true` 고, 그렇지 않으면이 가비지 수집에 의해 수집 된 배열 인덱스에 해당 하는 생성 되 면 `false`합니다.  
  
 배열 값으로 인덱싱된 합니다 [COR_PRF_GC_GENERATION](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-generation-enumeration.md) 생성을 나타내는 열거형입니다.  
  
 `reason`  
 [in] 값을 [COR_PRF_GC_REASON](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-reason-enumeration.md) 가비지 수집 이유를 나타내는 열거형 도출 되었습니다.  
  
## <a name="remarks"></a>설명  
 이 가비지 컬렉션에 속하는 모든 콜백 간에 발생 합니다 `GarbageCollectionStarted` 콜백 및 해당 [ICorProfilerCallback2::GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md) 콜백 합니다. 이러한 콜백을 동일한 스레드에서 발생 하지 않아도 됩니다.  
  
 프로파일러를 검사 하는 동안 원래 위치에서 개체에 대 한 안전 합니다 `GarbageCollectionStarted` 콜백 합니다. 가비지 수집기에서 반환 된 후 개체를 이동할 예정 `GarbageCollectionStarted`합니다. 이 콜백에서 프로파일러가 반환 된 후 프로파일러 잘못 된 것을 받을 때까지 모든 개체 Id를 고려해 야는 `ICorProfilerCallback2::GarbageCollectionFinished` 콜백 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
