---
title: ICorProfilerCallback 인터페이스
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback
helpviewer_keywords:
- ICorProfilerCallback interface [.NET Framework profiling]
ms.assetid: 4bae06f7-94d7-4ba8-b250-648b2da78674
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3119818934df765a8bbd9c05caaee04f9476069f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963517"
---
# <a name="icorprofilercallback-interface"></a>ICorProfilerCallback 인터페이스
프로파일러가 구독할 이벤트를 발생 시킬 때 CLR (공용 언어 런타임)에서 코드 프로파일러에 알리는 데 사용 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[AppDomainCreationFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-appdomaincreationfinished-method.md)|응용 프로그램 도메인이 생성 되었음을 프로파일러에 알립니다.|  
|[AppDomainCreationStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-appdomaincreationstarted-method.md)|응용 프로그램 도메인이 생성 중임을 프로파일러에 알립니다.|  
|[AppDomainShutdownFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-appdomainshutdownfinished-method.md)|응용 프로그램 도메인이 프로세스에서 언로드 되었음을 프로파일러에 알립니다.|  
|[AppDomainShutdownStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-appdomainshutdownstarted-method.md)|응용 프로그램 도메인이 프로세스에서 언로드되고 있음을 프로파일러에 알립니다.|  
|[AssemblyLoadFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-assemblyloadfinished-method.md)|어셈블리의 로드가 완료 되었음을 프로파일러에 알립니다.|  
|[AssemblyLoadStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-assemblyloadstarted-method.md)|어셈블리가 로드 되 고 있음을 프로파일러에 알립니다.|  
|[AssemblyUnloadFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-assemblyunloadfinished-method.md)|어셈블리가 언로드 되었음을 프로파일러에 알립니다.|  
|[AssemblyUnloadStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-assemblyunloadstarted-method.md)|어셈블리가 언로드되고 있음을 프로파일러에 알립니다.|  
|[ClassLoadFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadfinished-method.md)|클래스의 로드가 완료 되었음을 프로파일러에 알립니다.|  
|[ClassLoadStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadstarted-method.md)|클래스를 로드 하는 중임을 프로파일러에 알립니다.|  
|[ClassUnloadFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classunloadfinished-method.md)|클래스의 언로드가 완료 되었음을 프로파일러에 알립니다.|  
|[ClassUnloadStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classunloadstarted-method.md)|클래스가 언로드되고 있음을 프로파일러에 알립니다.|  
|[COMClassicVTableCreated 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-comclassicvtablecreated-method.md)|지정 된 IID 및 클래스에 대 한 RCW (런타임 호출 가능 래퍼)가 생성 되었음을 프로파일러에 알립니다.|  
|[COMClassicVTableDestroyed 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-comclassicvtabledestroyed-method.md)|RCW가 소멸 중임을 프로파일러에 알립니다.|  
|[ExceptionCatcherEnter 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptioncatcherenter-method.md)|컨트롤이 적절 한 `catch` 블록에 전달 되 고 있음을 프로파일러에 알립니다.|  
|[ExceptionCatcherLeave 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptioncatcherleave-method.md)|컨트롤이 적절 한 `catch` 블록에서 전달 되 고 있음을 프로파일러에 알립니다.|  
|[ExceptionCLRCatcherExecute 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionclrcatcherexecute-method.md)|.NET Framework 버전 2.0에서 사용 되지 않습니다.|  
|[ExceptionCLRCatcherFound 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionclrcatcherfound-method.md)|.NET Framework 2.0에서 사용 되지 않습니다.|  
|[ExceptionOSHandlerEnter 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionoshandlerenter-method.md)|구현되지 않았습니다. 관리 되지 않는 예외 정보가 필요한 프로파일러는 다른 방법으로이 정보를 얻어야 합니다.|  
|[ExceptionOSHandlerLeave 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionoshandlerleave-method.md)|구현되지 않았습니다. 관리 되지 않는 예외 정보가 필요한 프로파일러는 다른 방법으로이 정보를 얻어야 합니다.|  
|[ExceptionSearchCatcherFound 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionsearchcatcherfound-method.md)|예외 처리의 검색 단계에서 throw 된 예외에 대 한 처리기를 찾을 때 프로파일러에 알립니다.|  
|[ExceptionSearchFilterEnter 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionsearchfilterenter-method.md)|사용자 필터가 실행 중임을 프로파일러에 알립니다.|  
|[ExceptionSearchFilterLeave 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionsearchfilterleave-method.md)|사용자 필터의 실행이 완료 되었음을 프로파일러에 알립니다.|  
|[ExceptionSearchFunctionEnter 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionsearchfunctionenter-method.md)|예외 처리의 검색 단계에서 함수를 입력 했음을 프로파일러에 알립니다.|  
|[ExceptionSearchFunctionLeave 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionsearchfunctionleave-method.md)|예외 처리의 검색 단계에서 함수 검색을 완료 했음을 프로파일러에 알립니다.|  
|[ExceptionThrown 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionthrown-method.md)|예외가 throw 되었음을 프로파일러에 알립니다.|  
|[ExceptionUnwindFinallyEnter 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfinallyenter-method.md)|예외 처리의 해제 단계가 지정 된 함수에 포함 된 절을 `finally` 입력 하 고 있음을 프로파일러에 알립니다.|  
|[ExceptionUnwindFinallyLeave 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfinallyleave-method.md)|예외 처리의 해제 단계에 `finally` 절이 남아 있음을 프로파일러에 알립니다.|  
|[ExceptionUnwindFunctionEnter 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfunctionenter-method.md)|예외 처리의 해제 단계에서 함수를 입력 했음을 프로파일러에 알립니다.|  
|[ExceptionUnwindFunctionLeave 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfunctionleave-method.md)|예외 처리의 해제 단계에서 함수 해제가 완료 되었음을 프로파일러에 알립니다.|  
|[FunctionUnloadStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-functionunloadstarted-method.md)|런타임이 함수 언로드를 시작 했음을 프로파일러에 알립니다.|  
|[Initialize 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)|새 CLR 응용 프로그램이 시작 될 때마다 프로파일러를 초기화 하기 위해 호출 됩니다.|  
|[JITCachedFunctionSearchFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcachedfunctionsearchfinished-method.md)|Ngen.exe를 사용 하 여 이전에 컴파일된 함수에 대해 검색이 완료 되었음을 프로파일러에 알립니다.|  
|[JITCachedFunctionSearchStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcachedfunctionsearchstarted-method.md)|Ngen.exe를 사용 하 여 이전에 컴파일된 함수에 대해 검색이 시작 되었음을 프로파일러에 알립니다.|  
|[JITCompilationFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md)|JIT 컴파일러가 함수 컴파일을 완료 했음을 프로파일러에 알립니다.|  
|[JITCompilationStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md)|JIT (just-in-time) 컴파일러가 함수 컴파일을 시작 했음을 프로파일러에 알립니다.|  
|[JITFunctionPitched 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitfunctionpitched-method.md)|JIT 컴파일된 함수가 메모리에서 제거 되었음을 프로파일러에 알립니다.|  
|[JITInlining 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitinlining-method.md)|JIT 컴파일러가 다른 함수를 사용 하 여 함수를 삽입 하려고 함을 프로파일러에 알립니다.|  
|[ManagedToUnmanagedTransition 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-managedtounmanagedtransition-method.md)|관리 코드에서 비관리 코드로의 전환이 발생 했음을 프로파일러에 알립니다.|  
|[ModuleAttachedToAssembly 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleattachedtoassembly-method.md)|모듈이 부모 어셈블리에 연결 되 고 있음을 프로파일러에 알립니다.|  
|[ModuleLoadFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md)|모듈의 로드가 완료 되었음을 프로파일러에 알립니다.|  
|[ModuleLoadStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadstarted-method.md)|모듈이 로드 되 고 있음을 프로파일러에 알립니다.|  
|[ModuleUnloadFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleunloadfinished-method.md)|모듈의 언로드가 완료 되었음을 프로파일러에 알립니다.|  
|[ModuleUnloadStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleunloadstarted-method.md)|모듈이 언로드되고 있음을 프로파일러에 알립니다.|  
|[MovedReferences 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md)|가비지 수집 중에 이동 된 개체 참조에 대해 프로파일러에 알립니다.|  
|[ObjectAllocated 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectallocated-method.md)|힙에 있는 메모리가 개체에 할당 되었음을 프로파일러에 알립니다.|  
|[ObjectReferences 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectreferences-method.md)|지정 된 개체에서 참조 하는 메모리의 개체에 대해 프로파일러에 알립니다.|  
|[ObjectsAllocatedByClass 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectsallocatedbyclass-method.md)|이전 가비지 수집 이후 만들어진 지정 된 각 클래스의 인스턴스 수에 대해 프로파일러에 알립니다.|  
|[RemotingClientInvocationFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingclientinvocationfinished-method.md)|클라이언트에서 원격 호출이 완료 될 때까지 실행 되었음을 프로파일러에 알립니다.|  
|[RemotingClientInvocationStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingclientinvocationstarted-method.md)|원격 호출이 시작 되었음을 프로파일러에 알립니다.|  
|[RemotingClientReceivingReply 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingclientreceivingreply-method.md)|원격 호출의 서버 쪽 부분이 완료 되었고 클라이언트에서 응답을 받고 있음을 프로파일러에 알립니다.|  
|[RemotingClientSendingMessage 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingclientsendingmessage-method.md)|클라이언트에서 서버로 요청을 보내고 있음을 프로파일러에 알립니다.|  
|[RemotingServerInvocationReturned 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingserverinvocationreturned-method.md)|프로세스가 원격 메서드 호출 요청에 대 한 응답으로 메서드 호출을 완료 했음을 프로파일러에 알립니다.|  
|[RemotingServerInvocationStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingserverinvocationstarted-method.md)|프로세스가 원격 메서드 호출 요청에 대 한 응답으로 메서드를 호출 하 고 있음을 프로파일러에 알립니다.|  
|[RemotingServerReceivingMessage 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingserverreceivingmessage-method.md)|프로세스에서 원격 메서드 호출 또는 활성화 요청을 수신 하 고 있음을 프로파일러에 알립니다.|  
|[RemotingServerSendingReply 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingserversendingreply-method.md)|프로세스가 원격 메서드 호출 요청 처리를 완료 했으며 채널을 통해 회신을 전송 하려고 함을 프로파일러에 알립니다.|  
|[RootReferences 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-rootreferences-method.md)|가비지 수집 후 루트 참조에 대 한 정보를 프로파일러에 알립니다.|  
|[RuntimeResumeFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimeresumefinished-method.md)|런타임이 모든 런타임 스레드를 다시 시작 하 고 정상 작업으로 반환 되었음을 프로파일러에 알립니다.|  
|[RuntimeResumeStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimeresumestarted-method.md)|런타임이 모든 런타임 스레드를 재개 함을 프로파일러에 알립니다.|  
|[RuntimeSuspendAborted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendaborted-method.md)|런타임에서 발생 한 런타임 일시 중단이 중단 되었음을 프로파일러에 알립니다.|  
|[RuntimeSuspendFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendfinished-method.md)|런타임이 모든 런타임 스레드의 일시 중단을 완료 했음을 프로파일러에 알립니다.|  
|[RuntimeSuspendStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendstarted-method.md)|런타임이 모든 런타임 스레드를 일시 중단 함을 프로파일러에 알립니다.|  
|[RuntimeThreadResumed 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimethreadresumed-method.md)|지정 된 스레드가 일시 중단 된 후 다시 시작 되었음을 프로파일러에 알립니다.|  
|[RuntimeThreadSuspended 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimethreadsuspended-method.md)|지정 된 스레드가 일시 중단 되었음을 프로파일러에 알립니다.|  
|[Shutdown 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-shutdown-method.md)|응용 프로그램이 종료 되었음을 프로파일러에 알립니다.|  
|[ThreadAssignedToOSThread 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threadassignedtoosthread-method.md)|특정 운영 체제 (OS) 스레드를 사용 하 여 관리 되는 스레드가 구현 중임을 프로파일러에 알립니다.|  
|[ThreadCreated 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threadcreated-method.md)|스레드가 생성 되었음을 프로파일러에 알립니다.|  
|[ThreadDestroyed 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threaddestroyed-method.md)|스레드가 소멸 되었음을 프로파일러에 알립니다.|  
|[UnmanagedToManagedTransition 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-unmanagedtomanagedtransition-method.md)|비관리 코드에서 관리 코드로의 전환이 발생 했음을 프로파일러에 알립니다.|  
  
## <a name="remarks"></a>설명  
 CLR은 `ICorProfilerCallback` (또는 [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)) 인터페이스의 메서드를 호출 하 여 프로파일러가 구독 한 이벤트가 발생할 때 프로파일러에 알립니다. 이 인터페이스는 CLR이 코드 프로파일러와 통신 하는 데 사용 하는 기본 콜백 인터페이스입니다.  
  
 코드 프로파일러는 `ICorProfilerCallback` 인터페이스의 메서드를 구현 해야 합니다. .NET Framework 버전 2.0 이상에서는 프로파일러가 `ICorProfilerCallback2` 메서드도 구현 해야 합니다. 각 메서드 구현에서는 success의 값이 S_OK이 고 실패 한 경우 E_FAIL 인 HRESULT를 반환 해야 합니다. 현재 CLR은 [ICorProfilerCallback:: ObjectReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectreferences-method.md)를 제외 하 고 각 콜백에서 반환 되는 HRESULT를 무시 합니다.  
  
 Microsoft Windows 레지스트리에서 코드 프로파일러는 `ICorProfilerCallback` 및 `ICorProfilerCallback2` 인터페이스를 구현 하는 COM (구성 요소 개체 모델) 개체를 등록 해야 합니다. 코드 프로파일러는 [ICorProfilerInfo:: SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)를 호출 하 여 알림을 수신 하려는 이벤트를 구독 합니다. 이는 일반적으로 프로파일러의 [ICorProfilerCallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)구현에서 수행 됩니다. 그러면 프로파일러가 실행 중인 런타임 프로세스에서 발생 하거나 이벤트를 발생 시킬 때 런타임에서 알림을 받을 수 있습니다.  
  
> [!NOTE]
> 프로파일러는 단일 COM 개체를 등록 합니다. 프로파일러가 .NET Framework 버전 1.0 또는 1.1를 대상으로 하는 경우 해당 COM 개체는의 `ICorProfilerCallback`메서드만 구현 해야 합니다. .NET Framework 버전 2.0 이상을 대상으로 하는 경우에는 COM 개체도의 `ICorProfilerCallback2`메서드를 구현 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerCallback2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
- [ICorProfilerCallback3 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-interface.md)
- [ICorProfilerCallback4 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)
