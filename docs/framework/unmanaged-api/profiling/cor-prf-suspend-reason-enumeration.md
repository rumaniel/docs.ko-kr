---
title: COR_PRF_SUSPEND_REASON 열거형
ms.date: 03/30/2017
api_name:
- COR_PRF_SUSPEND_REASON
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_SUSPEND_REASON
helpviewer_keywords:
- COR_PRF_SUSPEND_REASON enumeration [.NET Framework profiling]
ms.assetid: 75594833-bed3-47b2-a426-b75c5fe6fbcf
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e084bc957eca9474078ed5ca3aef0276361dbe1b
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67745531"
---
# <a name="corprfsuspendreason-enumeration"></a>COR_PRF_SUSPEND_REASON 열거형
런타임이 일시 중단 되는 이유를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    COR_PRF_SUSPEND_OTHER                   = 0x00,  
    COR_PRF_SUSPEND_FOR_GC                  = 0x01,  
    COR_PRF_SUSPEND_FOR_APPDOMAIN_SHUTDOWN  = 0x02,  
    COR_PRF_SUSPEND_FOR_CODE_PITCHING       = 0x03,  
    COR_PRF_SUSPEND_FOR_SHUTDOWN            = 0x04,  
    COR_PRF_SUSPEND_FOR_INPROC_DEBUGGER     = 0x06,  
    COR_PRF_SUSPEND_FOR_GC_PREP             = 0x07,    COR_PRF_SUSPEND_FOR_REJIT               = 8  
} COR_PRF_SUSPEND_REASON;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`COR_PRF_FIELD_SUSPEND_OTHER`|런타임에 알 수 없는 이유로 일시 중단 됩니다.|  
|`COR_PRF_FIELD_SUSPEND_FOR_GC`|런타임은은 가비지 컬렉션 요청 서비스를 일시 중단 됩니다.<br /><br /> 가비지 컬렉션 관련 콜백이 사이 발생 합니다 [icorprofilercallback:: Runtimesuspendfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendfinished-method.md) 및 [icorprofilercallback:: Runtimeresumestarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimeresumestarted-method.md) 콜백 합니다.|  
|`COR_PRF_FIELD_SUSPEND_FOR_APPDOMAIN_SHUTDOWN`|런타임에서 일시 중단 됩니다 있도록는 `AppDomain` 종료할 수 있습니다.<br /><br /> 런타임에서 일시 중단 하는 동안를 확인 하는 스레드는에 `AppDomain` 즉 종료 되 고 다시 시작 될 때 중단 되도록 설정 합니다. 가지 없습니다 `AppDomain`-이 일시 중단 하는 동안 특정 콜백 합니다.|  
|`COR_PRF_FIELD_SUSPEND_FOR_CODE_PITCHING`|런타임 코드 피칭 발생할 수 있도록 일시 중단 됩니다.<br /><br /> 코드 피칭 근거가-just-in-time (JIT) 컴파일러가 활성화 되 면 코드 피칭 사용 하도록 설정 합니다. 코드 피칭 콜백 간에 발생 합니다 `ICorProfilerCallback::RuntimeSuspendFinished` 및 `ICorProfilerCallback::RuntimeResumeStarted` 콜백 합니다. **참고:**  CLR JIT는.NET Framework 버전 2.0의에서 함수 홍보 되므로 2.0에서이 값이 사용 되지 않습니다.|  
|`COR_PRF_FIELD_SUSPEND_FOR_SHUTDOWN`|종료할 수 있도록 런타임이 일시 중단 됩니다. 모든 스레드가 작업 완료를 일시 중단 해야 합니다.|  
|`COR_PRF_FIELD_SUSPEND_FOR_INPROC_DEBUGGER`|런타임은 프로세스의 디버깅에 대 한 일시 중단 됩니다.|  
|`COR_PRF_FIELD_SUSPEND_FOR_GC_PREP`|런타임은은 가비지 수집을 위해 준비 하려면 일시 중단 됩니다.|  
|`COR_PRF_SUSPEND_FOR_REJIT`|런타임은은 JIT 다시 컴파일을 위해 일시 중단 됩니다.|  
  
## <a name="remarks"></a>설명  
 비관리 코드에 있는 모든 런타임 스레드는이 시점에서 이러한도 일시 중단 됩니다 런타임을 다시 시작 될 때까지 런타임을 다시 입력 하려고 시도할 때까지 실행을 계속 허용 됩니다. 이 런타임에 입력 하는 새 스레드에도 적용 됩니다. 모든 스레드가 런타임 내에서 인터럽트 가능한 코드에 있는 경우 즉시 일시 중단 또는 인터럽트 가능한 코드에 도달할 때 일시 중지 하 라는 메시지가 표시 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 열거형](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
