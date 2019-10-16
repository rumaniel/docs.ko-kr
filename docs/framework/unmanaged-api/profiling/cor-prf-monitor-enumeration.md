---
title: COR_PRF_MONITOR 열거형
ms.date: 03/30/2017
api_name:
- COR_PRF_MONITOR
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_MONITOR
helpviewer_keywords:
- COR_PRF_MONITOR enumeration [.NET Framework profiling]
ms.assetid: 9294d702-b4e5-441c-a930-e63d27b86bfd
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b6916c223aee615fad0bb9e5a47691122db41c98
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67752059"
---
# <a name="corprfmonitor-enumeration"></a>COR_PRF_MONITOR 열거형
프로파일러가 구독하려는 동작, 기능 또는 이벤트를 지정하는 데 사용되는 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    COR_PRF_MONITOR_NONE                = 0x00000000,  
    COR_PRF_MONITOR_FUNCTION_UNLOADS    = 0x00000001,  
    COR_PRF_MONITOR_CLASS_LOADS         = 0x00000002,  
    COR_PRF_MONITOR_MODULE_LOADS        = 0x00000004,  
    COR_PRF_MONITOR_ASSEMBLY_LOADS      = 0x00000008,  
    COR_PRF_MONITOR_APPDOMAIN_LOADS     = 0x00000010,  
    COR_PRF_MONITOR_JIT_COMPILATION     = 0x00000020,  
    COR_PRF_MONITOR_EXCEPTIONS          = 0x00000040,  
    COR_PRF_MONITOR_GC                  = 0x00000080,  
    COR_PRF_MONITOR_OBJECT_ALLOCATED    = 0x00000100,  
    COR_PRF_MONITOR_THREADS             = 0x00000200,  
    COR_PRF_MONITOR_REMOTING            = 0x00000400,  
    COR_PRF_MONITOR_CODE_TRANSITIONS    = 0x00000800,  
    COR_PRF_MONITOR_ENTERLEAVE          = 0x00001000,  
    COR_PRF_MONITOR_CCW                 = 0x00002000,  
    COR_PRF_MONITOR_REMOTING_COOKIE     = 0x00004000 |   
                                          COR_PRF_MONITOR_REMOTING,  
    COR_PRF_MONITOR_REMOTING_ASYNC      = 0x00008000 |   
                                          COR_PRF_MONITOR_REMOTING,  
    COR_PRF_MONITOR_SUSPENDS            = 0x00010000,  
    COR_PRF_MONITOR_CACHE_SEARCHES      = 0x00020000,  
    COR_PRF_ENABLE_REJIT                = 0x00040000,  
    COR_PRF_ENABLE_INPROC_DEBUGGING     = 0x00080000,  
    COR_PRF_ENABLE_JIT_MAPS             = 0x00100000,  
    COR_PRF_DISABLE_INLINING            = 0x00200000,  
    COR_PRF_DISABLE_OPTIMIZATIONS       = 0x00400000,  
    COR_PRF_ENABLE_OBJECT_ALLOCATED     = 0x00800000,  
    COR_PRF_MONITOR_CLR_EXCEPTIONS      = 0x01000000,  
    COR_PRF_MONITOR_ALL                 = 0x0107FFFF,  
    COR_PRF_ENABLE_FUNCTION_ARGS        = 0X02000000,  
    COR_PRF_ENABLE_FUNCTION_RETVAL      = 0X04000000,  
    COR_PRF_ENABLE_FRAME_INFO           = 0X08000000,  
    COR_PRF_ENABLE_STACK_SNAPSHOT       = 0X10000000,  
    COR_PRF_USE_PROFILE_IMAGES          = 0x20000000,  
    COR_PRF_DISABLE_TRANSPARENCY_CHECKS_UNDER_FULL_TRUST  
                                        = 0x40000000,  
    COR_PRF_DISABLE_ALL_NGEN_IMAGES     = 0x80000000,  
    COR_PRF_ALL                         = 0x8FFFFFFF,  
    COR_PRF_REQUIRE_PROFILE_IMAGE       = COR_PRF_USE_PROFILE_IMAGES |   
                                          COR_PRF_MONITOR_CODE_TRANSITIONS |   
                                          COR_PRF_MONITOR_ENTERLEAVE,  
    COR_PRF_ALLOWABLE_AFTER_ATTACH      = COR_PRF_MONITOR_THREADS |  
                                          COR_PRF_MONITOR_MODULE_LOADS |  
                                          COR_PRF_MONITOR_ASSEMBLY_LOADS |  
                                          COR_PRF_MONITOR_APPDOMAIN_LOADS |  
                                          COR_PRF_ENABLE_STACK_SNAPSHOT |  
                                          COR_PRF_MONITOR_GC |  
                                          COR_PRF_MONITOR_SUSPENDS |  
                                          COR_PRF_MONITOR_CLASS_LOADS |  
                                          COR_PRF_MONITOR_JIT_COMPILATION,  
    COR_PRF_MONITOR_IMMUTABLE           = COR_PRF_MONITOR_CODE_TRANSITIONS |  
                                          COR_PRF_MONITOR_REMOTING |  
                                          COR_PRF_MONITOR_REMOTING_COOKIE |  
                                          COR_PRF_MONITOR_REMOTING_ASYNC |  
                                          COR_PRF_ENABLE_REJIT |  
                                          COR_PRF_ENABLE_INPROC_DEBUGGING |  
                                          COR_PRF_ENABLE_JIT_MAPS |  
                                          COR_PRF_DISABLE_OPTIMIZATIONS |  
                                          COR_PRF_DISABLE_INLINING |  
                                          COR_PRF_ENABLE_OBJECT_ALLOCATED |  
                                          COR_PRF_ENABLE_FUNCTION_ARGS |  
                                          COR_PRF_ENABLE_FUNCTION_RETVAL |  
                                          COR_PRF_ENABLE_FRAME_INFO |  
                                          COR_PRF_USE_PROFILE_IMAGES |  
                     COR_PRF_DISABLE_TRANSPARENCY_CHECKS_UNDER_FULL_TRUST |  
                                          COR_PRF_DISABLE_ALL_NGEN_IMAGES  
} COR_PRF_MONITOR;  
```  
  
## <a name="members"></a>멤버  
 다음 섹션은 `COR_PRF_MONITOR` 범주별 열거형 멤버입니다. 범주는 다음과 같습니다.  
  
- [플래그 설정 없음](#None)  
  
- [콜백 플래그](#Callback)  
  
- [기능 사용 플래그](#Feature)  
  
- [구성 플래그](#Config)  
  
- [복합 플래그](#Composite)  
  
<a name="None"></a>   
### <a name="no-flags-set"></a>플래그 설정 없음  
  
|멤버|Description|  
|------------|-----------------|  
|`COR_PRF_MONITOR_NONE`|플래그가 설정되지 않았습니다.|  
  
<a name="Callback"></a>   
### <a name="callback-flags"></a>콜백 플래그  
  
|멤버|Description|  
|------------|-----------------|  
|`COR_PRF_MONITOR_ALL`|모든 콜백 이벤트를 사용하도록 설정합니다.|  
|`COR_PRF_MONITOR_APPDOMAIN_LOADS`|컨트롤의 `AppDomainCreation*` 및 `AppDomainShutdown*` 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_ASSEMBLY_LOADS`|컨트롤의 `AssemblyLoad*` 및 `AssemblyUnload*` 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_CACHE_SEARCHES`|컨트롤의 `JITCachedFunctionSearch*` 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.<br /><br /> 이 플래그의 동작은 .NET Framework 버전 2.0에서 변경되었습니다.|  
|`COR_PRF_MONITOR_CCW`|컨트롤의 `COMClassicVTable*` 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_CLASS_LOADS`|컨트롤의 `ClassLoad*` 및 `ClassUnload*` 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_CLR_EXCEPTIONS`|컨트롤의 `ExceptionCLRCatcher*` 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_CODE_TRANSITIONS`|컨트롤의 [UnmanagedToManagedTransition](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-unmanagedtomanagedtransition-method.md) 하 고 [ManagedToUnmanagedTransition](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-managedtounmanagedtransition-method.md) 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스|  
|`COR_PRF_MONITOR_ENTERLEAVE`|컨트롤의 `FunctionEnter*`, `FunctionLeave*`, 및 `FunctionTailCall*` [프로 파일링 전역 정적 함수](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)합니다.|  
|`COR_PRF_MONITOR_EXCEPTIONS`|컨트롤의 [ExceptionThrown](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionthrown-method.md) 콜백 및 `ExceptionSearch*`, `ExceptionOSHandler*`, `ExceptionUnwind*`, 및 `ExceptionCatcher*` 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스.|  
|`COR_PRF_MONITOR_FUNCTION_UNLOADS`|컨트롤의 [FunctionUnloadStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-functionunloadstarted-method.md) 에서 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_GC`|컨트롤의 [GarbageCollectionStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionstarted-method.md)를 [GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md)를 [MovedReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md)를 [MovedReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-movedreferences2-method.md), [ SurvivingReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-survivingreferences-method.md), [SurvivingReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-survivingreferences2-method.md)를 [ObjectReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectreferences-method.md)하십시오 [ObjectsAllocatedByClass](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectsallocatedbyclass-method.md), [ RootReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-rootreferences-method.md), [RootReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-rootreferences2-method.md), [HandleCreated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-handlecreated-method.md)하십시오 [HandleDestroyed](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-handledestroyed-method.md), 및 [FinalizeableObjectQueued ](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-finalizeableobjectqueued-method.md) 콜백을 `ICorProfilerCallback*` 인터페이스입니다. 때 `COR_PRF_MONITOR_GC` 할당, 동시 가비지 컬렉션은 해제 합니다.|  
|`COR_PRF_MONITOR_JIT_COMPILATION`|컨트롤을 `JITCompilation*`, [JITFunctionPitched](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitfunctionpitched-method.md), 및 [JITInlining](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitinlining-method.md) 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_MODULE_LOADS`|컨트롤을 `ModuleLoad*`, `ModuleUnload*`, 및 [ModuleAttachedToAssembly](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleattachedtoassembly-method.md) 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_OBJECT_ALLOCATED`|컨트롤의 [ObjectAllocated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectallocated-method.md) 에서 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_REMOTING`|컨트롤의 `Remoting*` 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스입니다.|  
|`COR_PRF_MONITOR_REMOTING_ASYNC`|`Remoting*` 콜백이 비동기 이벤트를 모니터링하는지 여부를 제어합니다.|  
|`COR_PRF_MONITOR_REMOTING_COOKIE`|`Remoting*` 콜백으로 쿠키가 전달되는지 여부를 제어합니다.|  
|`COR_PRF_MONITOR_SUSPENDS`|컨트롤의 `RuntimeSuspend*`, `RuntimeResume*`, [RuntimeThreadSuspended](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimethreadsuspended-method.md), 및 [RuntimeThreadResumed](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimethreadresumed-method.md) 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스.|  
|`COR_PRF_MONITOR_THREADS`|컨트롤의 [ThreadCreated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threadcreated-method.md), [ThreadDestroyed](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threaddestroyed-method.md)를 [ThreadAssignedToOSThread](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threadassignedtoosthread-method.md), 및 [ThreadNameChanged](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-threadnamechanged-method.md) 콜백을 합니다 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 하 고 [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md) 인터페이스입니다.|  
  
<a name="Feature"></a>   
### <a name="feature-enabling-flags"></a>기능 사용 플래그  
  
|멤버|설명|  
|------------|-----------------|  
|`COR_PRF_ENABLE_FRAME_INFO`|정확한를 검색할 수 있도록 `ClassID` 호출 하 여 제네릭 함수에 대 한는 [GetFunctionInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md) 메서드를 `COR_PRF_FRAME_INFO` 에서 반환 된 값을 [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md) 콜백 합니다.|  
|`COR_PRF_ENABLE_FUNCTION_ARGS`|사용 하 여 사용 하도록 설정 인수 추적 합니다 [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md) 콜백 또는 [FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md) 콜백 하며 [GetFunctionEnter3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionenter3info-method.md) 메서드.|  
|`COR_PRF_ENABLE_FUNCTION_RETVAL`|사용 하 여 반환 값은 추적 하도록 설정 합니다 [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md) 콜백 또는 [FunctionLeave3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md) 콜백 및 [GetFunctionLeave3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md) 메서드.|  
|`COR_PRF_ENABLE_INPROC_DEBUGGING`|더 이상 사용되지 않습니다.<br /><br /> 프로세스 내 디버깅은 지원되지 않습니다. 이 플래그는 아무런 영향을 주지 않습니다.|  
|`COR_PRF_ENABLE_JIT_MAPS`|더 이상 사용되지 않습니다.<br /><br /> 프로파일러를 사용 하 여 IL-네이티브 맵을 가져올 수 있습니다 [GetILToNativeMapping](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getiltonativemapping-method.md)합니다. .NET Framework 2.0부터는 런타임이 항상 IL-네이티브 맵을 추적하므로 이 플래그는 항상 설정되어 있는 것으로 간주됩니다.|  
|`COR_PRF_ENABLE_OBJECT_ALLOCATED`|프로파일러가 개체 할당 알림을 받고자 할 수 있음을 런타임에 알립니다. 이 플래그는 초기화 중에 설정해야 합니다. 프로파일러를 사용 하 여 이후에 허용 합니다 `COR_PRF_MONITOR_OBJECT_ALLOCATED` 받으려면 플래그 [ObjectAllocated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectallocated-method.md) 콜백을 합니다.|  
|`COR_PRF_ENABLE_REJIT`|에 대 한 호출을 사용 하도록 설정 합니다 [RequestReJIT](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-requestrejit-method.md) 하 고 [RequestRevert](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-requestrevert-method.md) 메서드. 프로파일러는 시작 시 이 플래그를 설정해야 합니다.  프로파일러가 이 플래그를 지정하는 경우에는 `COR_PRF_DISABLE_ALL_NGEN_IMAGES`도 지정해야 합니다.|  
|`COR_PRF_ENABLE_STACK_SNAPSHOT`|에 대 한 호출을 사용 하도록 설정 합니다 [DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) 메서드.|  
  
<a name="Config"></a>   
### <a name="configuration-flags"></a>구성 플래그  
  
|멤버|설명|  
|------------|-----------------|  
|`COR_PRF_DISABLE_ALL_NGEN_IMAGES`|프로파일러 향상 이미지를 비롯한 모든 네이티브 이미지의 로드를 차단합니다.  이 플래그와 `COR_PRF_USE_PROFILE_IMAGES` 플래그가 모두 지정되어 있으면 `COR_PRF_DISABLE_ALL_NGEN_IMAGES`가 사용됩니다.|  
|`COR_PRF_DISABLE_INLINING`|모든 인라인 처리를 사용하지 않습니다.|  
|`COR_PRF_DISABLE_OPTIMIZATIONS`|모든 코드 최적화를 사용하지 않습니다.|  
|`COR_PRF_DISABLE_TRANSPARENCY_CHECKS_UNDER_FULL_TRUST`|일반적으로는 완전 신뢰 어셈블리에 대해 JIT(Just-In-Time) 컴파일 및 클래스 로드 중에 수행되는 보안 투명도 확인을 사용하지 않습니다. 이 경우 일부 계측을 보다 쉽게 수행할 수 있습니다.|  
|`COR_PRF_USE_PROFILE_IMAGES`|네이티브 이미지 검색에서 프로파일러 향상 이미지를 찾도록 지정합니다. 지정한 어셈블리의 프로파일러 향상 이미지가 없으면 공용 언어 런타임이 해당 어셈블리에 대해 JIT로 대체됩니다. 이 플래그와 `COR_PRF_DISABLE_ALL_NGEN_IMAGES` 플래그가 모두 지정되어 있으면 `COR_PRF_DISABLE_ALL_NGEN_IMAGES`가 사용됩니다.|  
  
<a name="Composite"></a>   
### <a name="composite-flags"></a>복합 플래그  
  
|멤버|설명|  
|------------|-----------------|  
|`COR_PRF_ALL`|모든 `COR_PRF_MONITOR` 플래그 값을 나타냅니다.|  
|`COR_PRF_ALLOWABLE_AFTER_ATTACH`|실행 중인 앱에 프로파일러를 연결한 후에 설정할 수 있는 모든 `COR_PRF_MONITOR` 플래그를 나타냅니다. 구문 섹션에는 이 비트 마스크에 있는 개별 플래그가 표시됩니다.|  
|`COR_PRF_MONITOR_ALL`|모든 콜백 이벤트를 사용하도록 설정합니다.|  
|`COR_PRF_MONITOR_IMMUTABLE`|초기화 중에만 설정할 수 있는 모든 `COR_PRF_MONITOR` 플래그를 나타냅니다. 초기화 후에 이러한 플래그를 변경하려고 하면 오류를 나타내는 `HRESULT` 값이 반환됩니다.|  
|`COR_PRF_REQUIRE_PROFILE_IMAGE`|프로필 향상 이미지가 필요한 모든 `COR_PRF_MONITOR` 플래그를 나타냅니다.|  
  
## <a name="remarks"></a>설명  
 `COR_PRF_MONITOR` 값을 사용 하 여이 기능을 사용 합니다 [icorprofilerinfo:: Geteventmask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-geteventmask-method.md) 및 [icorprofilerinfo:: Seteventmask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md) 에 공용 언어 런타임에서 이벤트 알림을 정의 하는 방법 프로파일러입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 열거형](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
- [GetEventMask 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-geteventmask-method.md)
- [SetEventMask 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)
