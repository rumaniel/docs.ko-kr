---
title: ICorProfilerCallback3::ProfilerDetachSucceeded 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback3.ProfilerDetachSucceeded Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback3::ProfilerDetachSucceeded
helpviewer_keywords:
- ProfilerDetachSucceeded method [.NET Framework profiling]
- ICorProfilerCallback3::ProfilerDetachSucceeded method [.NET Framework profiling]
ms.assetid: 05164966-16ce-4cc9-a530-43a640c00711
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8cff277179be761bb0dc78b02702e7d35ad4b6a9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779255"
---
# <a name="icorprofilercallback3profilerdetachsucceeded-method"></a>ICorProfilerCallback3::ProfilerDetachSucceeded 메서드
CLR(공용 언어 런타임)이 프로파일러 DLL을 언로드한다고 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ProfilerDetachSucceeded();  
```  
  
## <a name="return-value"></a>반환 값  
 이 콜백의 반환 값은 무시됩니다.  
  
## <a name="remarks"></a>설명  
 `ProfilerDetachSucceeded` 콜백은 모든 스레드가 프로파일러의 코드를 종료한 후에 실행됩니다. 이 메서드가 호출되면 프로파일러는 UI 또는 로깅 구성 요소에 알림과 같은 소멸자에 적합하지 않은 마지막 작업을 모두 수행해야 합니다. 그러나 프로파일러 해야 함수를 호출 하지이 콜백 중 CLR에서 제공 하는 인터페이스에 (같은 합니다 [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md) 또는 `IMetaData*` 인터페이스).  
  
 CLR은 Windows 애플리케이션 이벤트 로그에 항목을 만들어 분리 작업에 성공했음을 나타냅니다.  
  
 프로파일러가 이 콜백에서 반환된 후 CLR은 프로파일러 개체를 해제하고 프로파일러 DLL을 언로드합니다. 따라서 프로파일러는 이 콜백에서 반환된 후 프로파일러 DLL 내에서 실행되는 작업을 수행하면 안 됩니다. 예를 들어 스레드를 만들거나 타이머 콜백을 등록하면 안 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 인터페이스](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
- [ICorProfilerInfo3 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
