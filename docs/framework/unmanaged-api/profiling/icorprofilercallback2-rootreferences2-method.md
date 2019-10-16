---
title: ICorProfilerCallback2::RootReferences2 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.RootReferences2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::RootReferences2
helpviewer_keywords:
- RootReferences2 method [.NET Framework profiling]
- ICorProfilerCallback2::RootReferences2 method [.NET Framework profiling]
ms.assetid: 55a2f907-d216-42eb-8f2f-e5d59c2eebd6
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 563a2e19c9c254870b3e767253a276a201e631a6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779308"
---
# <a name="icorprofilercallback2rootreferences2-method"></a>ICorProfilerCallback2::RootReferences2 메서드
가비지 수집이 발생 한 후 루트 참조에 대 한 프로파일러를 알립니다. 이 메서드는 확장 합니다 [icorprofilercallback:: Rootreferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-rootreferences-method.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT RootReferences2(  
    [in] ULONG  cRootRefs,  
    [in, size_is(cRootRefs)] ObjectID rootRefIds[],  
    [in, size_is(cRootRefs)] COR_PRF_GC_ROOT_KIND rootKinds[],  
    [in, size_is(cRootRefs)] COR_PRF_GC_ROOT_FLAGS rootFlags[],  
    [in, size_is(cRootRefs)] UINT_PTR rootIds[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cRootRefs`  
 [in] 요소 수를 `rootRefIds`, `rootKinds`를 `rootFlags`, 및 `rootIds` 배열입니다.  
  
 `rootRefIds`  
 [in] 스택에 있는 개체 또는 정적 개체를 참조 하는 각 개체 Id의 배열입니다. 요소를 `rootKinds` 의 해당 요소를 분류 하는 정보를 제공 하는 배열은 `rootRefIds` 배열입니다.  
  
 `rootKinds`  
 [in] 배열을 [COR_PRF_GC_ROOT_KIND](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-root-kind-enumeration.md) 가비지 컬렉션 루트의 형식을 나타내는 값입니다.  
  
 `rootFlags`  
 [in] 배열을 [COR_PRF_GC_ROOT_FLAGS](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-root-flags-enumeration.md) 가비지 컬렉션 루트의 속성을 설명 하는 값입니다.  
  
 `rootIds`  
 [in] UINT_PTR 배열을 가리키는 값에 따라 가비지 컬렉션 루트에 대 한 추가 정보를 포함 하는 정수 값을 `rootKinds` 매개 변수입니다.  
  
 루트 형식의 스택을 인 경우 루트 ID 변수를 포함 하는 함수입니다. 해당 루트 ID 0 인 경우 함수는 내부 CLR에 있는 명명 되지 않은 함수입니다. 루트 형식의 대 한 핸들 인 경우 루트 ID 가비지 컬렉션 핸들입니다. 다른 루트 형식에 대 한 ID는 불투명 값을 무시 해야 합니다.  
  
## <a name="remarks"></a>설명  
 합니다 `rootRefIds`, `rootKinds`를 `rootFlags`, 및 `rootIds` 배열은 병렬 배열입니다. 즉, `rootRefIds[i]`, `rootKinds[i]`를 `rootFlags[i]`, 및 `rootIds[i]` 모두 동일한 루트를 다룹니다.  
  
 둘 다 `RootReferences` 고 `RootReferences2` 프로파일러에 알리기 위해 호출 됩니다. 프로파일러는 일반적으로 구현 하나 메서드 또는 다른 하지만 둘 다는 아님 정보 전달 되므로 `RootReferences2` 전달의 상위 집합이 `RootReferences`합니다.  
  
 항목에 대해 있기 `rootRefIds` 0는 해당 루트 참조를 null 이므로 관리 되는 힙에 있는 개체를 참조 하지 않습니다.  
  
 개체 Id가 반환한 `RootReferences2` 가비지 컬렉션 이전 주소에서 개체를 새 주소로 이동 하는 중일 수 있으므로 자체를 콜백 하는 동안 유효 하지 않습니다. 그러므로 프로파일러는 `RootReferences2` 호출 중에 개체 검사를 시도하지 않아야 합니다. 때 [ICorProfilerCallback2::GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md) 는 호출 개체를 모두 새 위치로 이동 되었습니다 및 안전 하 게 검사할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
