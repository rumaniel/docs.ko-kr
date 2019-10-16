---
title: ICorProfilerCallback2 인터페이스
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2
helpviewer_keywords:
- ICorProfilerCallback2 interface [.NET Framework profiling]
ms.assetid: 4a261dba-450d-4f1f-8d98-865b58bfc992
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d36d8ef3bfdbd6a1acf787a91003e2ff3139a4d9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963959"
---
# <a name="icorprofilercallback2-interface"></a>ICorProfilerCallback2 인터페이스
프로파일러가 구독할 이벤트를 발생 시킬 때 CLR (공용 언어 런타임)에서 코드 프로파일러에 알리는 데 사용 하는 메서드를 제공 합니다. 인터페이스 `ICorProfilerCallback2` 는 [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 인터페이스의 확장입니다. 즉, .NET Framework 버전 2.0에 도입 된 새 콜백을 제공 합니다.  
  
> [!NOTE]
> 각 메서드 구현은 success의 경우 S_OK 값을 가지는 HRESULT를 반환 하거나 실패 시 E_FAIL을 반환 해야 합니다. 현재 CLR은 [ICorProfilerCallback:: ObjectReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectreferences-method.md)를 제외 하 고 각 콜백에서 반환 되는 HRESULT를 무시 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[FinalizeableObjectQueued 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-finalizeableobjectqueued-method.md)|종료자를 사용 하는 개체가 해당 `Finalize` 메서드를 실행 하기 위해 종료자 스레드에 대기 되었음을 코드 프로파일러에 알립니다.|  
|[GarbageCollectionFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md)|가비지 수집이 완료 되었으며이에 대해 모든 가비지 수집 콜백이 실행 되었음을 프로파일러에 알립니다.|  
|[GarbageCollectionStarted 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionstarted-method.md)|가비지 수집이 시작 되었음을 코드 프로파일러에 알립니다.|  
|[HandleCreated 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-handlecreated-method.md)|가비지 수집 핸들이 생성 되었음을 코드 프로파일러에 알립니다.|  
|[HandleDestroyed 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-handledestroyed-method.md)|가비지 수집 핸들이 소멸 되었음을 코드 프로파일러에 알립니다.|  
|[RootReferences2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-rootreferences2-method.md)|가비지 수집이 발생 한 후 루트 참조에 대해 프로파일러에 알립니다. 이 메서드는 [ICorProfilerCallback:: RootReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-rootreferences-method.md) 메서드를 확장 한 것입니다.|  
|[SurvivingReferences 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-survivingreferences-method.md)|가비지 수집에서 남은 개체 참조에 대해 프로파일러에 알립니다.|  
|[ThreadNameChanged 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-threadnamechanged-method.md)|스레드의 이름이 변경 되었음을 코드 프로파일러에 알립니다.|  
  
## <a name="remarks"></a>설명  
 CLR은 `ICorProfilerCallback` (또는 `ICorProfilerCallback2`) 인터페이스의 메서드를 호출 하 여 프로파일러가 구독 한 이벤트가 발생할 때 프로파일러에 알립니다. 이 인터페이스는 CLR이 코드 프로파일러와 통신 하는 데 사용 하는 기본 콜백 인터페이스입니다.  
  
 코드 프로파일러는 `ICorProfilerCallback` 인터페이스의 메서드를 구현 해야 합니다. .NET Framework 2.0 이상 버전의 경우 프로파일러는 `ICorProfilerCallback2` 메서드도 구현 해야 합니다. 각 메서드 구현은 success의 경우 S_OK 값을 가지는 HRESULT를 반환 하거나 실패 시 E_FAIL을 반환 해야 합니다. 현재 CLR은 [ICorProfilerCallback:: ObjectReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectreferences-method.md)를 제외 하 고 각 콜백에서 반환 되는 HRESULT를 무시 합니다.  
  
 코드 프로파일러는 `ICorProfilerCallback` 및 `ICorProfilerCallback2` 인터페이스를 구현 하는 COM 개체, Microsoft Windows 레지스트리에 등록 해야 합니다. 코드 프로파일러는 [ICorProfilerInfo:: SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)를 호출 하 여 알림을 수신 하려는 이벤트를 구독 합니다. 이는 일반적으로 프로파일러의 [ICorProfilerCallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)구현에서 수행 됩니다. 그러면 프로파일러가 실행 중인 런타임 프로세스에서 발생 하거나 이벤트를 발생 시킬 때 런타임에서 알림을 받을 수 있습니다.  
  
> [!NOTE]
> 프로파일러는 단일 COM 개체를 등록 합니다. 프로파일러가 .NET Framework 버전 1.0 또는 1.1를 대상으로 하는 경우 해당 COM 개체는의 `ICorProfilerCallback`메서드만 구현 하면 됩니다. .NET Framework 버전 2.0 이상을 대상으로 하는 경우에는 COM 개체도의 `ICorProfilerCallback2`메서드를 구현 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback3 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-interface.md)
- [ICorProfilerCallback4 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)
