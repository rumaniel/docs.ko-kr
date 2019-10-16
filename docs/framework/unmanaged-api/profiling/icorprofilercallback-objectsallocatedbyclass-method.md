---
title: ICorProfilerCallback::ObjectsAllocatedByClass 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ObjectsAllocatedByClass
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectsAllocatedByClass
helpviewer_keywords:
- ObjectsAllocatedByClass method [.NET Framework profiling]
- ICorProfilerCallback::ObjectsAllocatedByClass method [.NET Framework profiling]
ms.assetid: 91d688f3-a80e-419d-9755-ff94bc04188a
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4229332ef3a079a5a294e27b624dde0e1fb46691
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782959"
---
# <a name="icorprofilercallbackobjectsallocatedbyclass-method"></a>ICorProfilerCallback::ObjectsAllocatedByClass 메서드
가장 최근의 가비지 수집 이후 생성 된 각 지정 된 클래스의 인스턴스 수에 대 한 프로파일러를 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ObjectsAllocatedByClass(  
    [in] ULONG   cClassCount,  
    [in, size_is(cClassCount)] ClassID classIds[] ,  
    [in, size_is(cClassCount)] ULONG   cObjects[] );  
```  
  
## <a name="parameters"></a>매개 변수  
 `cClassCount`  
 [in] 크기를 `classIds` 고 `cObjects` 배열입니다.  
  
 `classIds`  
 [in] 배열 클래스 Id 각 ID 하나 이상의 인스턴스를 사용 하 여 클래스를 지정 하는 위치입니다.  
  
 `cObjects`  
 [in] 각 정수에 해당 클래스의 인스턴스 수를 지정 하는 위치, 정수의 배열을 `classIds` 배열입니다.  
  
## <a name="remarks"></a>설명  
 합니다 `classIds` 고 `cObjects` 배열은 병렬 배열입니다. 예를 들어 `classIds[i]` 고 `cObjects[i]` 동일한 클래스를 참조 합니다. 이전 가비지 수집 이후 클래스의 인스턴스를 만든 경우 클래스는 생략 됩니다. `ObjectsAllocatedByClass` 콜백 대형 개체 힙에 할당 된 개체를 보고 하지 것입니다.  
  
 숫자에서 보고 `ObjectsAllocatedByClass` 만 예상 됩니다. 정확한 개수에 대 한 사용 [icorprofilercallback:: Objectallocated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectallocated-method.md)합니다.  
  
 합니다 `classIds` 배열의 경우 하나 이상의 null 항목을 포함할 수 있습니다 해당 `cObjects` 언로드하는 배열 형식이 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
