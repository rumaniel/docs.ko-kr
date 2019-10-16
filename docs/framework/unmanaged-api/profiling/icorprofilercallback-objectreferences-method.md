---
title: ICorProfilerCallback::ObjectReferences 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ObjectReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectReferences
helpviewer_keywords:
- ObjectReferences method [.NET Framework profiling]
- ICorProfilerCallback::ObjectReferences method [.NET Framework profiling]
ms.assetid: dd5e9b64-b4a3-4ba6-9be6-ddb540f4ffcf
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4141c79502dae89ec228e4e39da121615f292786
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782968"
---
# <a name="icorprofilercallbackobjectreferences-method"></a>ICorProfilerCallback::ObjectReferences 메서드
지정된 된 개체에서 참조 되지 않는 메모리에서 개체에 대 한 프로파일러를 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ObjectReferences(  
    [in]  ObjectID objectId,  
    [in]  ClassID  classId,  
    [in]  ULONG    cObjectRefs,  
    [in, size_is(cObjectRefs)] ObjectID objectRefIds[] );  
```  
  
## <a name="parameters"></a>매개 변수  
 `objectId`  
 [in] 개체를 참조 하는 개체의 ID입니다.  
  
 `classId`  
 [in] 지정된 된 개체의 인스턴스가 있는 클래스의 ID입니다.  
  
 `cObjectRefs`  
 [in] 지정된 된 개체에서 참조 하는 개체 수 (의 요소 수를 `objectRefIds` 배열)입니다.  
  
 `objectRefIds`  
 [in] 참조 되지 않는 개체의 Id 배열을 `objectId`합니다.  
  
## <a name="remarks"></a>설명  
 `ObjectReferences` 힙에 남아 있는 가비지 수집이 완료 된 후 각 개체에 대해 호출 됩니다. 프로파일러가이 콜백에서 오류를 반환 하는 경우 다음 가비지 수집 될 때까지이 콜백을 호출 하면 프로 파일링 서비스는 중단 됩니다.  
  
 합니다 `ObjectReferences` 콜백와 함께에서 사용할 수는 [icorprofilercallback:: Rootreferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-rootreferences-method.md) 런타임에 대 한 완전 한 개체 참조 그래프를 만들 콜백입니다. CLR (공용 언어 런타임) 하면 각 개체 참조 하 여 한 번만 보고 되는 `ObjectReferences` 메서드.  
  
 개체 Id가 반환한 `ObjectReferences` 가비지 컬렉션 개체를 이동 하는 중일 수 있으므로 자체를 콜백 하는 동안 유효 하지 않습니다. 따라서 프로파일러 시도 하지 않아야 하는 동안 개체 검사는 `ObjectReferences` 호출 합니다. 때 [ICorProfilerCallback2::GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md) 호출 되는 가비지 수집이 완료 되 고 검사를 안전 하 게 수행할 수 있습니다.  
  
 Null `ClassId` 나타내는 `objectId` 형식이 언로드하는 중입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
