---
title: CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT
ms.date: 03/30/2017
f1_keywords:
- CORPROF_E_UNSUPPORTED_CALL_SEQUENCE
helpviewer_keywords:
- CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT [.NET Framework profiling]
ms.assetid: f2fc441f-d62e-4f72-a011-354ea13c8c59
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a8eb622b974de350f86a586a0f07b887bffdbd61
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66483059"
---
# <a name="corprofeunsupportedcallsequence-hresult"></a>CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT
CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT는.NET Framework 버전 2.0에서에서 도입 되었습니다. .NET Framework 4는 두 가지 시나리오에서이 HRESULT를 반환합니다.  
  
- 하이재킹 프로파일러 스레드를 강제로 다시 설정 하는 경우는 스레드가 일관성이 없는 상태에 있는 구조에 액세스 하려고 있도록 임의의 시간에 컨텍스트를 등록 합니다.  
  
- 프로파일러 콜백 메서드를 가비지 수집을 트리거하는 정보 제공 용 이므로 메서드를 호출 하려고 할 때 가비지 수집을 금지 하 합니다.  
  
 이러한 두 시나리오는 다음 섹션에서 설명 됩니다.  
  
## <a name="hijacking-profilers"></a>프로파일러를 하이재킹  
 (이 시나리오는 문제 비 하이재킹 프로파일러가이 HRESULT를 볼 수 있는 경우도 있지만 프로파일러를 하이재킹를 주로.)  
  
 이 시나리오에서는 하이재킹 프로파일러에서 강제로 컨텍스트를 다시 설정 스레드의 등록 임의의 시점에 스레드가 프로파일러 코드를 입력 하거나 다시는 CLR (공용 언어 런타임)을 입력 수 있도록 통해는 [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md) 메서드.  
  
 많은 Id 프로 파일링 API는 clr에서 데이터 구조를 가리킵니다. 많은 `ICorProfilerInfo` 호출에서 단순히 이러한 데이터 구조에서 정보를 읽어야 하 고 다시 전달 합니다. 그러나 CLR에서 실행 되 고 이렇게 하려면 잠금을 사용할 수 있습니다 이러한 구조를 변경할 수 있습니다. CLR가 이미 보유 (또는 획득 하려고) 잠금을 시 가정 프로파일러 스레드가 하이재킹입니다. 스레드가 CLR에 다시 들어가면을 더 많은 잠금을 또는 수정 중인 프로세스에 있는 구조를 검사 하려고 하는 경우 이러한 구조는 일관 되지 않은 상태의 수 있습니다. 교착 상태 및 액세스 위반 쉽게 이러한 상황에서 발생할 수 있습니다.  
  
 비 하이재킹 프로파일러 내의 코드를 실행 하는 경우에 일반적으로 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 메서드 및 호출에는 `ICorProfilerInfo` 메서드 올바른 매개 변수를 사용 하 여 해당 교착 상태 하거나 안 액세스 위반이 발생 합니다. 예를 들어, 내에서 실행 되는 프로파일러 코드를 [icorprofilercallback:: Classloadfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadfinished-method.md) 메서드를 호출 하 여 클래스에 대 한 정보를 요청할 수 있습니다 합니다 [ICorProfilerInfo2::GetClassIDInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassidinfo2-method.md) 메서드입니다. 코드 정보를 사용할 수 임을 나타내려면 CORPROF_E_DATAINCOMPLETE HRESULT 나타날 수 있습니다. 그러나 되거나 되지 않습니다 교착 상태 액세스 위반이 발생 합니다. 이 클래스에 대 한 호출 `ICorProfilerInfo` 에서 이루어지기 때문에 동기적으로 호출 되는 `ICorProfilerCallback` 메서드.  
  
 그러나 관리 되는 스레드는 실행 하지 않은 코드 내는 `ICorProfilerCallback` 메서드 비동기 호출을 만드는 것으로 간주 됩니다. .NET framework 버전 1에서 비동기 호출에서 발생할 수 있는 일을 결정 하기가 어려웠습니다. 호출 수 교착 상태 충돌 하거나 잘못 된 응답을 제공 합니다. .NET Framework 버전 2.0에는이 문제를 방지 하는 데 몇 가지 간단한 검사가 도입 되었습니다. 안전 하지 않은 호출 하는 경우.NET Framework 2.0에서는 `ICorProfilerInfo` 비동기적으로 함수를 CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT를 사용 하 여 실패 합니다.  
  
 일반적으로 비동기 호출은 안전 하지 않습니다. 그러나 다음 메서드는 안전 및 특히 비동기 호출을 지원 합니다.  
  
- [GetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-geteventmask-method.md)  
  
- [SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)  
  
- [GetCurrentThreadID](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcurrentthreadid-method.md)  
  
- [GetThreadContext](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadcontext-method.md)  
  
- [GetThreadAppDomain](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getthreadappdomain-method.md)  
  
- [GetFunctionFromIP](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromip-method.md)  
  
- [GetFunctionInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctioninfo-method.md)  
  
- [GetFunctionInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md)  
  
- [GetCodeInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcodeinfo-method.md)  
  
- [GetCodeInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcodeinfo2-method.md)  
  
- [GetModuleInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmoduleinfo-method.md)  
  
- [GetClassIDInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassidinfo-method.md)  
  
- [GetClassIDInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassidinfo2-method.md)  
  
- [IsArrayClass](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-isarrayclass-method.md)  
  
- [SetFunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)  
  
- [DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)  
  
 자세한 내용은 항목을 참조 하세요 [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE 있다고 이유](https://go.microsoft.com/fwlink/?LinkId=169156) CLR 프로 파일링 API 블로그에서.  
  
## <a name="triggering-garbage-collections"></a>가비지 수집 트리거  
 이 시나리오에서는 콜백 메서드 내에서 실행 되는 프로파일러 (예를 들어,이 중 하나는 `ICorProfilerCallback` 메서드) 가비지 수집을 금지 하 합니다. 프로파일러 정보 메서드를 호출 하려고 하는 경우 (예를 들어 메서드를는 `ICorProfilerInfo` 인터페이스)는 가비지 수집을 트리거할 수 있습니다, 정보 제공 용 이므로 메서드가 CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT를 사용 하 여 실패 합니다.  
  
 다음 표에서 가비지 수집을 금지 하는 콜백 메서드 및 가비지 컬렉션을 트리거할 수 있는 정보 메서드를 표시 합니다. 프로파일러 나열 된 콜백 메서드 중 하나 내에서 실행 나열된 하는 정보 제공 용 이므로 메서드 중 하나를 호출 하는 경우 해당 정보 제공 용 이므로 메서드가 CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT를 사용 하 여 실패 합니다.  
  
|가비지 컬렉션을 금지 하는 콜백 메서드|가비지 컬렉션을 트리거하는 정보 제공 용 이므로 메서드|  
|------------------------------------------------------|------------------------------------------------------------|  
|[ThreadAssignedToOSThread](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threadassignedtoosthread-method.md)<br /><br /> [ExceptionUnwindFunctionEnter](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfunctionenter-method.md)<br /><br /> [ExceptionUnwindFunctionLeave](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfunctionleave-method.md)<br /><br /> [ExceptionUnwindFinallyEnter](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfinallyenter-method.md)<br /><br /> [ExceptionUnwindFinallyLeave](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfinallyleave-method.md)<br /><br /> [ExceptionCatcherEnter](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptioncatcherenter-method.md)<br /><br /> [RuntimeSuspendStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendstarted-method.md)<br /><br /> [RuntimeSuspendFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendfinished-method.md)<br /><br /> [RuntimeSuspendAborted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendaborted-method.md)<br /><br /> [RuntimeThreadSuspended](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimethreadsuspended-method.md)<br /><br /> [RuntimeThreadResumed](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimethreadresumed-method.md)<br /><br /> [MovedReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md)<br /><br /> [ObjectReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectreferences-method.md)<br /><br /> [ObjectsAllocatedByClass](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectsallocatedbyclass-method.md)<br /><br /> [RootReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-rootreferences-method.md)<br /><br /> [HandleCreated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-handlecreated-method.md)<br /><br /> [HandleDestroyed](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-handledestroyed-method.md)<br /><br /> [GarbageCollectionStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionstarted-method.md)<br /><br /> [GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md)|[GetILFunctionBodyAllocator](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbodyallocator-method.md)<br /><br /> [SetILFunctionBody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md)<br /><br /> [SetILInstrumentedCodeMap](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md)<br /><br /> [ForceGC](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-forcegc-method.md)<br /><br /> [GetClassFromToken](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromtoken-method.md)<br /><br /> [GetClassFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassfromtokenandtypeargs-method.md)<br /><br /> [GetFunctionFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md)<br /><br /> [GetAppDomainInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getappdomaininfo-method.md)<br /><br /> [EnumModules](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enummodules-method.md)<br /><br /> [RequestProfilerDetach](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-requestprofilerdetach-method.md)<br /><br /> [GetAppDomainsContainingModule](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getappdomainscontainingmodule-method.md)|  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
- [ICorProfilerCallback3 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-interface.md)
- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
- [ICorProfilerInfo3 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
