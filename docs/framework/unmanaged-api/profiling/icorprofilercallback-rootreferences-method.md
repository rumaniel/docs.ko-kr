---
title: ICorProfilerCallback::RootReferences 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RootReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RootReferences
helpviewer_keywords:
- RootReferences method [.NET Framework profiling]
- ICorProfilerCallback::RootReferences method [.NET Framework profiling]
ms.assetid: dbdf853b-d1a4-4828-8ef7-53d121d8e6ae
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a68ea07c40c966422be6ebb663e62508032c2610
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67750440"
---
# <a name="icorprofilercallbackrootreferences-method"></a>ICorProfilerCallback::RootReferences 메서드
가비지 컬렉션 후 루트 참조에 대 한 정보를 사용 하 여 프로파일러를 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT RootReferences(  
    [in] ULONG    cRootRefs,  
    [in, size_is(cRootRefs)] ObjectID rootRefIds[] );  
```  
  
## <a name="parameters"></a>매개 변수  
 `cRootRefs`  
 [in] 에 대 한 참조 횟수를 `rootRefIds` 배열입니다.  
  
 `rootRefIds`  
 [in] 스택에 있는 개체 또는 정적 개체를 참조 하는 개체 Id의 배열입니다.  
  
## <a name="remarks"></a>설명  
 둘 다 `RootReferences` 하 고 [ICorProfilerCallback2::RootReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-rootreferences2-method.md) 프로파일러에 알리기 위해 호출 됩니다. 하나 또는 다른 프로파일러는 일반적으로 구현 됩니다 둘 모두가 아닌 정보를 전달 되므로 `RootReferences2` 전달의 상위 집합이 `RootReferences`합니다.  
  
 이기는 `rootRefIds` null 개체가 포함 될 배열입니다. 예를 들어 스택에 선언 된 모든 개체 참조는 가비지 수집기에서 루트로 처리 되 고 항상 보고 됩니다.  
  
 개체 Id가 반환한 `RootReferences` 가비지 컬렉션 이전 주소에서 개체를 새 주소로 이동 하는 중일 수 있으므로 자체를 콜백 하는 동안 유효 하지 않습니다. 따라서 프로파일러 시도 하지 않아야 하는 동안 개체를 검사 한 `RootReferences` 호출 합니다. 때 [ICorProfilerCallback2::GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md) 는 호출 개체를 모두 새 위치로 이동 되었습니다 및 안전 하 게 검사할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
