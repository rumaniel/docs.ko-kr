---
title: StackSnapshotCallback 함수
ms.date: 03/30/2017
api_name:
- StackSnapshotCallback
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- StackSnapshotCallback
helpviewer_keywords:
- StackSnapshotCallback function [.NET Framework profiling]
ms.assetid: d0f235b2-91fe-4f82-b7d5-e5c64186eea8
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6140ecda1d12c26e1936daee4eaad11cbd9b6ba4
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781232"
---
# <a name="stacksnapshotcallback-function"></a>StackSnapshotCallback 함수
프로파일러가 시작 되는 스택 워크 중 스택의 각 관리 되는 프레임 및 관리 되지 않는 프레임의 각 실행에 대 한 정보를 제공 합니다 [ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT __stdcall StackSnapshotCallback (  
    [in] FunctionID funcId,  
    [in] UINT_PTR ip,  
    [in] COR_PRF_FRAME_INFO frameInfo,  
    [in] ULONG32 contextSize,  
    [in] BYTE context[],  
    [in] void *clientData  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `funcId`  
 [in] 이 콜백을 실행 하는 관리 되지 않는 프레임입니다이 값이 0 인 경우 이 고, 그렇지 관리 되는 함수의 식별자 이며이 콜백은 관리 되는 프레임입니다.  
  
 `ip`  
 [in] 프레임에서 네이티브 코드 명령 포인터의 값입니다.  
  
 `frameInfo`  
 [in] `COR_PRF_FRAME_INFO` 스택 프레임에 대 한 정보를 참조 하는 값입니다. 이 값은이 콜백 중에 사용 하기에 적합 합니다.  
  
 `contextSize`  
 [in] 크기를 `CONTEXT` 에서 참조 하는 구조는 `context` 매개 변수입니다.  
  
 `context`  
 [in] Win32에 대 한 포인터 `CONTEXT` 이 프레임에 대 한 CPU의 상태를 나타내는 구조체입니다.  
  
 합니다 `context` 매개 변수는 COR_PRF_SNAPSHOT_CONTEXT 플래그에 전달 된 경우에 유효 `ICorProfilerInfo2::DoStackSnapshot`합니다.  
  
 `clientData`  
 [in] 직접 전달 되는 클라이언트 데이터에 대 한 포인터 `ICorProfilerInfo2::DoStackSnapshot`합니다.  
  
## <a name="remarks"></a>설명  
 `StackSnapshotCallback` 프로파일러 작성기에서 함수를 구현 합니다. 수행 된 작업의 복잡성을 제한 해야 `StackSnapshotCallback`합니다. 예를 들어, 사용 하는 경우 `ICorProfilerInfo2::DoStackSnapshot` 비동기 방식으로, 대상 스레드가 있습니다 잠금을 유지 합니다. 경우 내 코드 `StackSnapshotCallback` 같은 잠금이 필요 교착 상태 충돌 수 없습니다.  
  
 합니다 `ICorProfilerInfo2::DoStackSnapshot` 메서드 호출을 `StackSnapshotCallback` 함수 관리 되는 프레임 마다 한 번씩 또는 관리 되지 않는 프레임 실행 당 한 번입니다. 경우 `StackSnapshotCallback` 라고 관리 되지 않는 프레임의 실행에 대 한 프로파일러 레지스터 컨텍스트로 사용할 수 있습니다 (에서 참조 하는 `context` 매개 변수)는 자체 관리 되지 않는 스택 워크가 수행 하 합니다. 이 경우 Win32 `CONTEXT` 구조 관리 되지 않는 프레임이 실행 되는 가장 최근에 푸시된 프레임에 대 한 CPU 상태를 나타냅니다. 하지만 Win32 `CONTEXT` 모든 등록에 대 한 값을 포함 하는 구조, 스택 포인터 레지스터와 프레임 포인터 레지스터, 명령 포인터 레지스터 (보존)이 표시 되는 비휘발성의 값에만 의존 하는 정수 레지스터입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [DoStackSnapshot 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)
- [프로파일링 전역 정적 함수](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
