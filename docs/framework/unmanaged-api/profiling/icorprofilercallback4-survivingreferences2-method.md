---
title: ICorProfilerCallback4::SurvivingReferences2 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.SurvivingReferences2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::SurvivingReferences2
helpviewer_keywords:
- ICorProfilerCallback4::SurvivingReferences2 method [.NET Framework profiling]
- SurvivingReferences2 method, ICorProfilerCallback4 interface [.NET Framework profiling]
ms.assetid: 02b51888-5d89-4e50-a915-45b7e329aad9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: beb260030914de211d227342e497daa3db287c9e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67758080"
---
# <a name="icorprofilercallback4survivingreferences2-method"></a>ICorProfilerCallback4::SurvivingReferences2 메서드
비압축 가비지 수집의 결과로 힙에 있는 개체의 레이아웃을 보고합니다. 이 메서드는 프로파일러 구현에 [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) 인터페이스입니다. 이 콜백은 대체 합니다 [ICorProfilerCallback2::SurvivingReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-survivingreferences-method.md) 메서드를 더 큰 범위의 길이가 ulong에서으로 표현 될 수 있습니다 어떤 초과 하는 개체를 보고할 수 있어.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SurvivingReferences2(  
    [in] ULONG  cSurvivingObjectIDRanges,  
    [in, size_is(cSurvivingObjectIDRanges)] ObjectID  
                objectIDRangeStart[] ,  
    [in, size_is(cSurvivingObjectIDRanges)] SIZE_T  
                cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a>매개 변수  
 `cSurvivingObjectIDRanges`  
 [in] 비압축 가비지 수집 후에 유지된 연속 개체 블록 수입니다. 즉, `cSurvivingObjectIDRanges` 값은 각 개체 블록의 `ObjectID` 및 길이를 각각 저장하는 `objectIDRangeStart` 및 `cObjectIDRangeLength` 배열의 크기입니다.  
  
 `SurvivingReferences2`의 다음 두 인수는 병렬 배열입니다. 즉, `objectIDRangeStart` 및 `cObjectIDRangeLength`는 동일한 연속 개체 블록과 관련이 있습니다.  
  
 `objectIDRangeStart`  
 [in] 메모리에서 연속 라이브 개체 블록의 시작 주소를 각각 나타내는 `ObjectID` 값의 배열입니다.  
  
 `cObjectIDRangeLength`  
 [in] 메모리에 유지되는 연속 개체 블록의 크기를 각각 나타내는 정수 배열입니다.  
  
 크기는 `objectIDRangeStart` 배열에서 참조된 각 블록에 대해 지정됩니다.  
  
## <a name="remarks"></a>설명  
 개체가 가비지 수집 후에 유지되었는지 여부를 확인하려면 `objectIDRangeStart` 및 `cObjectIDRangeLength` 배열의 요소를 다음과 같이 해석해야 합니다. `ObjectID` 값(`ObjectID`)이 다음 범위 내에 있다고 가정합니다.  
  
 `ObjectIDRangeStart[i]` <= `ObjectID` < `ObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 `i` 값이 다음 범위에 있는 경우 개체가 가비지 수집 후에 유지되었습니다.  
  
 0 <= `i` < `cSurvivingObjectIDRanges`  
  
 비압축 가비지 컬렉션은 "데드" 개체가 사용한 메모리를 회수하지만 확보된 공간을 압축하지는 않습니다. 따라서 메모리가 힙에 반환되지만 "라이브" 개체는 이동되지 않습니다.  
  
 CLR(공용 언어 런타임)은 비압축 가비지 수집을 위해 `SurvivingReferences2`를 호출합니다. 압축 가비지 컬렉션 [MovedReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-movedreferences2-method.md) 대신 호출 됩니다. 한 세대는 단일 가비지 수집을 압축하고 다른 세대는 압축하지 않을 수 있습니다. 특정 세대의 가비지 컬렉션에 대 한 프로파일러 중 하나를 받게를 `SurvivingReferences2` 콜백 또는 [MovedReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-movedreferences2-method.md) 콜백, 하지만 둘 다.  
  
 제한된 내부 버퍼링, 서버 가비지 컬렉션 중 여러 콜백 발생 및 기타 이유로 인해 특정 가비지 컬렉션 중 `SurvivingReferences2` 콜백을 여러 개 받을 수도 있습니다. 가비지 수집 중 여러 콜백이 발생하는 경우 정보가 누적됩니다. `SurvivingReferences2` 콜백에 보고된 모든 참조가 가비지 수집 후에 유지됩니다.  
  
 프로파일러 둘 다 구현 하는 경우는 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 하며 [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) 인터페이스는 `SurvivingReferences2` 메서드 전에 호출 됩니다는 [ICorProfilerCallback2:: SurvivingReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-survivingreferences-method.md) 방법 이지만 경우에만 `SurvivingReferences2` 성공적으로 반환 합니다. 프로파일러는 두 번째 메서드 호출을 방지하기 위해 `SurvivingReferences2` 메서드에서 실패를 나타내는 HRESULT를 반환할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
- [ICorProfilerCallback4 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)
