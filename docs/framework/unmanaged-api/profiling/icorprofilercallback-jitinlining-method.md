---
title: ICorProfilerCallback::JITInlining 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITInlining
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITInlining
helpviewer_keywords:
- JITInlining method [.NET Framework profiling]
- ICorProfilerCallback::JITInlining method [.NET Framework profiling]
ms.assetid: c2f45801-dd38-4b78-b6b7-64397dc73f83
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 82af06837ead9a00923c23d4ce145015308fbbf7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782797"
---
# <a name="icorprofilercallbackjitinlining-method"></a>ICorProfilerCallback::JITInlining 메서드
다른 함수에 따라 함수를 삽입할 시간 (JIT) 컴파일러는 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT JITInlining(  
    [in]  FunctionID callerId,  
    [in]  FunctionID calleeId,  
    [out] BOOL      *pfShouldInline);  
```  
  
## <a name="parameters"></a>매개 변수  
 `callerId`  
 [in] 함수의 ID는 `calleeId` 함수 삽입 됩니다.  
  
 `calleeId`  
 [in] 삽입할 함수의 ID입니다.  
  
 `pfShouldInline`  
 [out] `true` ; 발생을 삽입할 수 있도록이 고, 그렇지 `false`합니다.  
  
## <a name="remarks"></a>설명  
 프로파일러 설정할 수 있습니다 `pfShouldInline` 를 `false` 방지 하기 위해 합니다 `calleeId` 함수를 삽입 하는 `callerId` 함수. 또한 프로파일러 전역적으로 해제할 수 인라인 삽입 COR_PRF_DISABLE_INLINING 값을 사용 하 여 합니다 [COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md) 열거형입니다.  
  
 삽입 함수를 인라인으로 출입에 대 한 이벤트를 발생 하지 않습니다. 따라서 프로파일러 설정 해야 합니다 `pfShouldInline` 에 `false` 정확한 호출 그래프를 생성 하기 위해. 설정 `pfShouldInline` 에 `false` 인라인 삽입에서 일반적으로 속도 증가 하 고 삽입 된 메서드에 대 한 별도 JIT 컴파일 이벤트 수가 감소 하기 때문에 성능이 저하 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
