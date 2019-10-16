---
title: ICorProfilerCallback::Shutdown 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.Shutdown
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::Shutdown
helpviewer_keywords:
- ICorProfilerCallback::Shutdown method [.NET Framework profiling]
- Shutdown method [.NET Framework profiling]
ms.assetid: 1ea194f0-a331-4855-a2ce-37393b8e5f84
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9d63dd911a5f674a3ce0b02ec78de443c7aebf84
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747163"
---
# <a name="icorprofilercallbackshutdown-method"></a>ICorProfilerCallback::Shutdown 메서드
응용 프로그램이 종료 되는 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Shutdown();  
```  
  
## <a name="remarks"></a>설명  
 프로파일러 코드는의 메서드를 안전 하 게 호출할 수 없습니다는 [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md) 후 인터페이스를 `Shutdown` 메서드가 호출 됩니다. 에 대 한 모든 호출 `ICorProfilerInfo` 메서드 후 정의 되지 않은 동작이 발생할는 `Shutdown` 메서드 반환 합니다. 종료 후 변경할 수 없는 특정 이벤트가 발생할 수 있습니다. 이런 경우 즉시 반환할 프로파일러 주의 해야 합니다.  
  
 `Shutdown` 프로 파일링 되는 관리 되는 응용 프로그램 관리 코드로 시작 하는 경우에 메서드가 호출 됩니다 (즉, 프로세스 스택의 초기 프레임이 관리 됩니다). 응용 프로그램 관리 되지 않는 코드로 시작 하지만 나중에 관리 되는 코드로 이동 하 여 인스턴스를 만들 공용 언어 런타임 (CLR)의 다음 `Shutdown` 호출 되지 것입니다. 이러한 경우 프로파일러 해당 라이브러리를 포함 해야 합니다는 `DllMain` 루틴을 DLL_PROCESS_DETACH를 사용 하는 모든 리소스를 해제 하 고 해당 데이터를 추적 하 고 디스크에 플러시하는 등의 정리 프로세스를 수행할 값입니다.  
  
 일반적으로 프로파일러는 예기치 않은 종료를 사용 하 여 처리 해야 합니다. Win32의 의해 프로세스를 중단 예를 들어 `TerminateProcess` 메서드 (Winbase.h에 선언 됨). 다른 경우에 CLR에 소멸 순서 대로 메시지를 배달 하지 않고 (백그라운드 스레드)는 특정 관리 되는 스레드를 중단 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [Initialize 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)
