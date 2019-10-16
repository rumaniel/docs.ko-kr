---
title: ICLRProfiling::AttachProfiler 메서드
ms.date: 03/30/2017
api_name:
- IClrProfiling.AttachProfiler Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- IClrProfiling::AttachProfiler
helpviewer_keywords:
- AttachProfiler method [.NET Framework profiling]
- IClrProfiling::AttachProfiler method [.NET Framework profiling]
ms.assetid: 535a6839-c443-405b-a6f4-e2af90725d5b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: efc097fd9b4da668aafce90ce601a3143ea57dc7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67763176"
---
# <a name="iclrprofilingattachprofiler-method"></a>ICLRProfiling::AttachProfiler 메서드
지정한 프로파일러를 지정된 프로세스에 연결합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT AttachProfiler(  
  [in] DWORD dwProfileeProcessID,  
  [in] DWORD dwMillisecondsMax,                     // optional  
  [in] const CLSID * pClsidProfiler,  
  [in] LPCWSTR wszProfilerPath,                     // optional  
  [in] size_is(cbClientData)] void * pvClientData,  // optional  
  [in] UINT cbClientData);                          // optional  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwProfileeProcessID`  
 [in] 프로파일러를 연결해야 하는 프로세스의 프로세스 ID입니다. 64비트 컴퓨터에서는 프로파일링된 프로세스의 비트가 `AttachProfiler`를 호출하는 트리거 프로세스의 비트와 일치해야 합니다. `AttachProfiler`가 호출되는 사용자 계정에 관리 권한이 있는 경우 대상 프로세스는 시스템의 모든 프로세스일 수 있습니다. 그러지 않으면 대상 프로세스가 동일한 사용자 계정에 의해 소유되어야 합니다.  
  
 `dwMillisecondsMax`  
 [in] `AttachProfiler`가 완료되는 기간(밀리초)입니다. 트리거 프로세스는 특정 프로파일러가 초기화를 완료하기에 충분한 것으로 알려진 시간 제한을 전달해야 합니다.  
  
 `pClsidProfiler`  
 [in] 로드할 프로파일러의 CLSID에 대한 포인터입니다. 트리거 프로세스는 `AttachProfiler`가 반환된 후 이 메모리를 다시 사용할 수 있습니다.  
  
 `wszProfilerPath`  
 [in] 로드할 프로파일러 DLL 파일의 전체 경로입니다. 이 문자열에는 null 종결자를 포함하여 260자 이하가 포함되어야 합니다. `wszProfilerPath`가 null 또는 빈 문자열인 경우 CLR(공용 언어 런타임)은 `pClsidProfiler`가 가리키는 CLSID를 레지스트리에서 찾아 프로파일러 DLL 파일의 위치를 찾으려고 합니다.  
  
 `pvClientData`  
 [in] 프로파일러에 전달할 데이터에 대 한 포인터를 [ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md) 메서드. 트리거 프로세스는 `AttachProfiler`가 반환된 후 이 메모리를 다시 사용할 수 있습니다. `pvClientData`가 null이면 `cbClientData`는 0이어야 합니다.  
  
 `cbClientData`  
 [in] `pvClientData`가 가리키는 데이터의 크기(바이트)입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 HRESULT를 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|지정된 프로파일러가 대상 프로세스에 성공적으로 연결했습니다.|  
|CORPROF_E_PROFILER_ALREADY_ACTIVE|활성 상태이거나 대상 프로세스에 연결하는 프로파일러가 이미 있습니다.|  
|CORPROF_E_PROFILER_NOT_ATTACHABLE|지정된 프로파일러가 연결을 지원하지 않습니다. 트리거 프로세스가 다른 프로파일러를 연결하려고 시도할 수 있습니다.|  
|CORPROF_E_PROFILEE_INCOMPATIBLE_WITH_TRIGGER|대상 프로세스 버전이 `AttachProfiler`를 호출하는 현재 프로세스와 호환되지 않으므로 프로파일러 연결을 요청할 수 없습니다.|  
|HRESULT_FROM_WIN32(ERROR_ACCESS_DENIED)|트리거 프로세스의 사용자에게 대상 프로세스에 액세스할 수 있는 권한이 없습니다.|  
|HRESULT_FROM_WIN32(ERROR_PRIVILEGE_NOT_HELD)|트리거 프로세스의 사용자에게 프로파일러를 지정된 대상 프로세스에 연결하는 데 필요한 권한이 없습니다. 애플리케이션 이벤트 로그에 자세한 정보가 포함될 수 있습니다.|  
|CORPROF_E_IPC_FAILED|대상 프로세스와 통신할 때 오류가 발생했습니다. 이 문제는 일반적으로 대상 프로세스를 종료하는 경우에 발생합니다.|  
|HRESULT_FROM_WIN32(ERROR_FILE_NOT_FOUND)|대상 프로세스가 없거나 연결을 지원하는 CLR을 실행하지 않습니다. 이는 런타임 열거형 메서드 호출 이후에 CLR가 언로드되었음을 나타낼 수 있습니다.|  
|HRESULT_FROM_WIN32(ERROR_TIMEOUT)|프로파일러 로드를 시작하지 않고 시간 제한이 만료되었습니다. 연결 작업을 다시 시도할 수 있습니다. 시간 초과는 대상 프로세스의 종료자가 시간 제한 값보다 오래 실행되는 경우에 발생합니다.|  
|E_INVALIDARG|하나 이상의 매개 변수에 잘못된 값이 있습니다.|  
|E_FAIL|지정되지 않은 다른 일부 오류가 발생했습니다.|  
|기타 오류 코드|경우 프로파일러의 [ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md) 실패를 나타내는 HRESULT를 반환 하는 메서드 `AttachProfiler` 반환 동일한 HRESULT입니다. 이 경우 E_NOTIMPL이 CORPROF_E_PROFILER_NOT_ATTACHABLE로 변환됩니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="memory-management"></a>메모리 관리  
 COM 규칙에 따라 `AttachProfiler` 호출자(예: 프로파일러 개발자가 작성한 트리거 코드)는 `pvClientData` 매개 변수가 가리키는 데이터에 대한 메모리를 할당 및 할당 취소해야 합니다. CLR은 `AttachProfiler` 호출을 실행할 때 `pvClientData`가 가리키는 메모리의 복사본을 만들고 대상 프로세스에 전송합니다. 대상 프로세스 내의 CLR이 고유한 `pvClientData` 블록 복사본을 받으면 `InitializeForAttach` 메서드를 통해 블록을 프로파일러에 전달한 다음 대상 프로세스에서 `pvClientData` 블록 복사본의 할당을 취소합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerInfo3 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
