---
title: ICorProfilerCallback::ModuleAttachedToAssembly 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ModuleAttachedToAssembly
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ModuleAttachedToAssembly
helpviewer_keywords:
- ICorProfilerCallback::ModuleAttachedToAssembly method [.NET Framework profiling]
- ModuleAttachedToAssembly method [.NET Framework profiling]
ms.assetid: b595798a-5d40-4cac-ab4f-911c61d2c5d2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3345e2e87ba41f750031deed2d15e13dbe4f06c8
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769296"
---
# <a name="icorprofilercallbackmoduleattachedtoassembly-method"></a>ICorProfilerCallback::ModuleAttachedToAssembly 메서드
모듈 부모 어셈블리에 연결 되는 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ModuleAttachedToAssembly(  
    [in] ModuleID   moduleId,  
    [in] AssemblyID AssemblyId);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleId`  
 [in] ID는 연결 되는 모듈입니다.  
  
 `AssemblyId`  
 [in] 모듈을 연결할 부모 어셈블리의 ID입니다.  
  
## <a name="remarks"></a>설명  
 호출 하 여 가져오기 주소 테이블 (IAT)을 통해 모듈을 로드할 수 있습니다 `LoadLibrary`, 또는 메타 데이터 참조를 통해. 결과적으로, 공용 언어 런타임 (CLR) 로더 모듈 거주 하는 어셈블리를 확인 하기 위한 여러 코드 경로 있습니다. 따라서 것이 가능 후 [icorprofilercallback:: Moduleloadfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md) 가 호출 모듈에 어셈블리를 알 수 없습니다 것 이며 수 없는 부모 어셈블리 ID를 가져오는 중입니다. `ModuleAttachedToAssembly` 메서드 모듈은 부모 어셈블리 및 해당 부모 어셈블리 ID를 가져올 수 있습니다를 연결할 때 호출 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
