---
title: 프로파일링 열거형
ms.date: 03/30/2017
helpviewer_keywords:
- profiling enumerations [.NET Framework]
- enumerations [.NET Framework profiling]
- unmanaged enumerations [.NET Framework], profiling
ms.assetid: 8d5f9570-9853-4ce8-8101-df235d5b258e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 996352637f34b0b6c0d12e611a6d9e70ab85230e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757575"
---
# <a name="profiling-enumerations"></a>프로파일링 열거형
이 섹션에서는 프로파일링 API에서 사용하는 관리되지 않는 열거형에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [COR_PRF_CLAUSE_TYPE 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-clause-type-enumeration.md)  
 코드에서 방금 시작되거나 끝난 예외 절 형식을 나타냅니다.  
  
 [COR_PRF_CODEGEN_FLAGS 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-codegen-flags-enumeration.md)  
 사용 하 여 설정할 수 있는 코드 생성 플래그를 정의 합니다 [icorprofilerfunctioncontrol:: Setcodegenflags](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-setcodegenflags-method.md) 메서드.  
  
 [COR_PRF_FINALIZER_FLAGS 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-finalizer-flags-enumeration.md)  
 개체에 대한 종료자를 설명합니다.  
  
 [COR_PRF_GC_GENERATION 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-generation-enumeration.md)  
 가비지 수집 생성을 식별합니다.  
  
 [COR_PRF_GC_REASON 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-reason-enumeration.md)  
 가비지 컬렉션이 수행되는 이유를 나타냅니다.  
  
 [COR_PRF_GC_ROOT_FLAGS 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-root-flags-enumeration.md)  
 가비지 수집기 루트의 속성을 나타냅니다.  
  
 [COR_PRF_GC_ROOT_KIND 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-root-kind-enumeration.md)  
 에 의해 노출 되는 가비지 수집기 루트의 종류를 나타내는 합니다 [ICorProfilerCallback2::RootReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-rootreferences2-method.md) 콜백 합니다.  
  
 [COR_PRF_HIGH_MONITOR 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-high-monitor-enumeration.md)  
 에 있는 것 외에도 플래그를 제공 합니다 [COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md) 프로파일러를 지정할 수 있는 열거형 합니다 [ICorProfilerInfo5::SetEventMask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md) 메서드 로드 될 때.  
  
 [COR_PRF_JIT_CACHE 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-jit-cache-enumeration.md)  
 캐시된 함수 검색의 결과를 나타냅니다.  
  
 [COR_PRF_MISC 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-misc-enumeration.md)  
 특수 식별자를 지정하는 상수 값을 포함합니다.  
  
 [COR_PRF_MODULE_FLAGS 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-module-flags-enumeration.md)  
 모듈의 속성을 지정합니다.  
  
 [COR_PRF_MONITOR 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md)  
 프로파일러가 구독하려는 동작, 기능 또는 이벤트를 지정하는 데 사용되는 값을 포함합니다.  
  
 [COR_PRF_RUNTIME_TYPE 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-runtime-type-enumeration.md)  
 공용 언어 런타임의 버전을 나타내는 값을 포함합니다.  
  
 [COR_PRF_SNAPSHOT_INFO 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-snapshot-info-enumeration.md)  
 프로파일러 `StackSnapshotCallback` 함수에 대한 각 호출에서 스택 스냅샷과 함께 다시 전달할 데이터의 양을 지정합니다.  
  
 [COR_PRF_STATIC_TYPE 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-static-type-enumeration.md)  
 필드가 정적인지 여부와 정적인 경우 필드에 적용될 정적 품질을 나타냅니다.  
  
 [COR_PRF_SUSPEND_REASON 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-suspend-reason-enumeration.md)  
 런타임이 일시 중단된 이유를 나타냅니다.  
  
 [COR_PRF_TRANSITION_REASON 열거형](../../../../docs/framework/unmanaged-api/profiling/cor-prf-transition-reason-enumeration.md)  
 관리 코드에서 비관리 코드로 전환 또는 그 반대의 경우로 전환하는 이유를 나타냅니다.  
  
## <a name="related-sections"></a>관련 단원  
 [프로파일링 개요](../../../../docs/framework/unmanaged-api/profiling/profiling-overview.md)  
  
 [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
  
 [프로파일링 전역 정적 함수](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)  
  
 [프로파일링 구조체](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)
