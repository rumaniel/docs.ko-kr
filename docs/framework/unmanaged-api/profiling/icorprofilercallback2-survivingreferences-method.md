---
title: ICorProfilerCallback2::SurvivingReferences 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.SurvivingReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::SurvivingReferences
helpviewer_keywords:
- ICorProfilerCallback2::SurvivingReferences method [.NET Framework profiling]
- SurvivingReferences method [.NET Framework profiling]
ms.assetid: f165200e-3a91-47f7-88fc-13ff10c8babc
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fc3ec00f11582ede1dc4b3d481a4eb9dcc4dd1d9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963910"
---
# <a name="icorprofilercallback2survivingreferences-method"></a>ICorProfilerCallback2::SurvivingReferences 메서드
비압축 가비지 수집의 결과로 힙에 있는 개체의 레이아웃을 보고합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SurvivingReferences(  
    [in] ULONG  cSurvivingObjectIDRanges,  
    [in, size_is(cSurvivingObjectIDRanges)] ObjectID  
                objectIDRangeStart[] ,  
    [in, size_is(cSurvivingObjectIDRanges)] ULONG  
                cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a>매개 변수  
 `cSurvivingObjectIDRanges`  
 [in] 비압축 가비지 수집 후에 유지된 연속 개체 블록 수입니다. 즉, `cSurvivingObjectIDRanges` 값은 각 개체 블록의 `ObjectID` 및 길이를 각각 저장하는 `objectIDRangeStart` 및 `cObjectIDRangeLength` 배열의 크기입니다.  
  
 `SurvivingReferences`의 다음 두 인수는 병렬 배열입니다. 즉, `objectIDRangeStart` 및 `cObjectIDRangeLength`는 동일한 연속 개체 블록과 관련이 있습니다.  
  
 `objectIDRangeStart`  
 [in] 메모리에서 연속 라이브 개체 블록의 시작 주소를 각각 나타내는 `ObjectID` 값의 배열입니다.  
  
 `cObjectIDRangeLength`  
 [in] 메모리에 유지되는 연속 개체 블록의 크기를 각각 나타내는 정수 배열입니다.  
  
 크기는 `objectIDRangeStart` 배열에서 참조된 각 블록에 대해 지정됩니다.  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]
> 이 메서드는 64비트 플랫폼에서 4GB보다 큰 개체의 크기를 `MAX_ULONG`으로 보고합니다. 4gb 보다 큰 개체의 경우 [ICorProfilerCallback4:: SurvivingReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-survivingreferences2-method.md) 메서드를 대신 사용 합니다.  
  
 개체가 가비지 수집 후에 유지되었는지 여부를 확인하려면 `objectIDRangeStart` 및 `cObjectIDRangeLength` 배열의 요소를 다음과 같이 해석해야 합니다. `ObjectID` 값(`ObjectID`)이 다음 범위 내에 있다고 가정합니다.  
  
 `ObjectIDRangeStart[i]` <= `ObjectID` < `ObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 `i` 값이 다음 범위에 있는 경우 개체가 가비지 수집 후에 유지되었습니다.  
  
 0 <= `i` < `cSurvivingObjectIDRanges`  
  
 비압축 가비지 컬렉션은 "데드" 개체가 사용한 메모리를 회수하지만 확보된 공간을 압축하지는 않습니다. 따라서 메모리가 힙에 반환되지만 "라이브" 개체는 이동되지 않습니다.  
  
 CLR(공용 언어 런타임)은 비압축 가비지 수집을 위해 `SurvivingReferences`를 호출합니다. 압축 가비지 컬렉션의 경우 대신 [ICorProfilerCallback:: MovedReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md) 가 호출 됩니다. 한 세대는 단일 가비지 수집을 압축하고 다른 세대는 압축하지 않을 수 있습니다. 특정 세대의 가비지 컬렉션에 대해 프로파일러는 `SurvivingReferences` 콜백이나 `MovedReferences` 콜백 중 하나를 받게 되며 둘 다 받을 수는 없습니다.  
  
 제한된 내부 버퍼링, 서버 가비지 컬렉션 시 여러 스레드 보고 및 기타 이유로 인해 특정 가비지 컬렉션 중 `SurvivingReferences` 콜백을 여러 개 받을 수도 있습니다. 가비지 컬렉션 중 여러 콜백이 발생하는 경우 정보가 누적됩니다. `SurvivingReferences` 콜백에 보고된 모든 참조가 가비지 컬렉션 후에 유지됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
- [SurvivingReferences2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-survivingreferences2-method.md)
