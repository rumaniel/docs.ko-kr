---
title: COR_PRF_HIGH_MONITOR 열거형
ms.date: 04/10/2018
ms.assetid: 3ba543d8-15e5-4322-b6e7-1ebfc92ed7dd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8cbc66ef1eb5048d2c708a615a99ea363d29540f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67752178"
---
# <a name="corprfhighmonitor-enumeration"></a>COR_PRF_HIGH_MONITOR 열거형
[.NET Framework 4.5.2 이상 버전에서 지원됨]  
  
 에 있는 것 외에도 플래그를 제공 합니다 [COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md) 프로파일러를 지정할 수 있는 열거형 합니다 [ICorProfilerInfo5::SetEventMask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md) 메서드 로드 될 때.  
  
## <a name="syntax"></a>구문  
  
```cpp
typedef enum {  
    COR_PRF_HIGH_MONITOR_NONE                     = 0x00000000,  
    COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES          = 0x00000001,  
    COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED        = 0x00000002,
    COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS = 0x00000004,
    COR_PRF_HIGH_DISABLE_TIERED_COMPILATION       = 0x00000008,
    COR_PRF_HIGH_BASIC_GC                         = 0x00000010,
    COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS         = 0x00000020,
    COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED    = 0x00000040,
    COR_PRF_HIGH_REQUIRE_PROFILE_IMAGE            = 0,  
    COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH           = COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED | 
                                                    COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS |
                                                    COR_PRF_HIGH_BASIC_GC |
                                                    COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS |
                                                    COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED,  
    COR_PRF_HIGH_MONITOR_IMMUTABLE                = COR_PRF_HIGH_DISABLE_TIERED_COMPILATION  
} COR_PRF_HIGH_MONITOR;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`COR_PRF_HIGH_MONITOR_NONE`|플래그가 설정되지 않았습니다.|  
|`COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES`|컨트롤의 [ICorProfilerCallback6::GetAssemblyReference](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md) CLR 어셈블리 참조 closure 워커 중에 어셈블리 참조를 추가 하는 것에 대 한 콜백입니다.|  
|`COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED`|컨트롤의 [ICorProfilerCallback7::ModuleInMemorySymbolsUpdated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback7-moduleinmemorysymbolsupdated-method.md) 메모리 내 모듈과 연관 된 기호 스트림이 업데이트에 대 한 콜백입니다.|  
|`COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS`|컨트롤의 [ICorProfilerCallback9::DynamicMethodUnloaded](icorprofilercallback9-dynamicmethodunloaded-method.md) 동적 메서드 가비지 된 시기를 나타내는 콜백 수집 되 고 언로드됩니다. <br/> [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]|
|`COR_PRF_HIGH_DISABLE_TIERED_COMPILATION`|.NET core 3.0 및 이후 버전의 경우에 해당: 사용 하지 않도록 설정 [컴파일 계층화](../../../core/whats-new/dotnet-core-3-0.md) 프로파일러에 대 한 합니다.|
|`COR_PRF_HIGH_BASIC_GC`|.NET core 3.0 및 이후 버전의 경우에 해당: GC 프로 파일링 옵션에 비해 간단한 제공 [ `COR_PRF_MONITOR_GC` ](cor-prf-monitor-enumeration.md)합니다. 만 제어 합니다 [GarbageCollectionStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionstarted-method.md)를 [GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md), 및 [GetGenerationBounds](icorprofilerinfo2-getgenerationbounds-method.md) 콜백 합니다. 와 달리 합니다 `COR_PRF_MONITOR_GC` 플래그를 `COR_PRF_HIGH_BASIC_GC` 동시 가비지 수집을 비활성화 하지 않습니다.|
|`COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS`|.NET core 3.0 및 이후 버전의 경우에 해당: 사용 하도록 설정 합니다 [MovedReferences](icorprofilercallback-movedreferences-method.md) 하 고 [MovedReferences2](icorprofilercallback4-movedreferences2-method.md) 만 압축 Gc에 대 한 콜백을 합니다.|
|`COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED`|.NET core 3.0 및 이후 버전의 경우에 해당: 비슷합니다 [ `COR_PRF_MONITOR_OBJECT_ALLOCATED` ](cor-prf-monitor-enumeration.md), 하지만 개체 할당에 대 한 큰 개체 힙 (LOH)만에 정보를 제공 합니다.|
|`COR_PRF_HIGH_REQUIRE_PROFILE_IMAGE`|프로필 향상 이미지가 필요한 모든 `COR_PRF_HIGH_MONITOR` 플래그를 나타냅니다. 에 해당 합니다 `COR_PRF_REQUIRE_PROFILE_IMAGE` 플래그를 [COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md) 열거형입니다.|  
|`COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH`|실행 중인 앱에 프로파일러를 연결한 후에 설정할 수 있는 모든 `COR_PRF_HIGH_MONITOR` 플래그를 나타냅니다.|  
|`COR_PRF_HIGH_MONITOR_IMMUTABLE`|초기화 중에만 설정할 수 있는 모든 `COR_PRF_HIGH_MONITOR` 플래그를 나타냅니다. 다른 위치에서 이러한 플래그를 변경하려고 하면 오류를 나타내는 `HRESULT` 값이 반환됩니다.|  
  
## <a name="remarks"></a>설명  
 `COR_PRF_HIGH_MONITOR` 플래그 사용 되는 `pdwEventsHigh` 의 매개 변수를 [ICorProfilerInfo5::GetEventMask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-geteventmask2-method.md) 및 [ICorProfilerInfo5::SetEventMask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md) 메서드.  
  
.NET Framework 4.6.1의 값을 사용 하 여 시작 합니다 `COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH` 0에서 변경 `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` (0x00000002). .NET Framework 4.7.2부터 해당 값을에서 변경할 `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` 에 `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED | COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS`입니다.   

`COR_PRF_HIGH_MONITOR_IMMUTABLE` 초기화 하는 동안만 설정할 수 있는 모든 플래그를 나타내는 비트 마스크를 것입니다. 다른 곳에서 실패 한 결과이 플래그를 변경 하 려 `HRESULT`합니다.

## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 열거형](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
- [COR_PRF_MONITOR 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md)
- [ICorProfilerInfo5 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-interface.md)
