---
title: ICorProfilerInfo4::GetILToNativeMapping2 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.GetILToNativeMapping2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::GetILToNativeMapping2
helpviewer_keywords:
- ICorProfilerInfo4::GetILToNativeMapping2 method [.NET Framework profiling]
- GetILToNativeMapping2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 756c1c25-08a7-4060-9798-dbeaa2f3bee5
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a8ffdb04bdf3fd2f605e2dffc5065a0d786bbaf7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967912"
---
# <a name="icorprofilerinfo4getiltonativemapping2-method"></a>ICorProfilerInfo4::GetILToNativeMapping2 메서드
지정된 함수의 JIT 다시 컴파일된 버전에 포함된 코드에 대한 MSIL(Microsoft Intermediate Language) 오프셋과 네이티브 오프셋 간의 맵을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetILToNativeMapping(  
    [in] FunctionID functionId,  
    [in] ReJITID reJitId,  
    [in] ULONG32 cMap,  
    [out] ULONG32 *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `functionId`  
 [in] 코드를 포함하는 함수의 ID입니다.  
  
 `pReJitId`  
 [in] JIT 다시 컴파일된 함수의 ID입니다. Id는 .NET Framework 4.5에서 0 이어야 합니다.  
  
 `cMap`  
 [in] `map` 배열의 최대 크기입니다.  
  
 `pcMap`  
 제한이 사용 가능한 COR_DEBUG_IL_TO_NATIVE_MAP 구조체의 총 수입니다.  
  
 `map`  
 [out] 각각 오프셋을 지정하는 `COR_DEBUG_IL_TO_NATIVE_MAP` 구조체의 배열입니다. `GetILToNativeMapping2` 메서드가 반환되면 `map`에 `COR_DEBUG_IL_TO_NATIVE_MAP` 구조체가 일부 또는 모두 포함됩니다.  
  
## <a name="remarks"></a>설명  
 `GetILToNativeMapping2`는 [ICorProfilerInfo:: GetILToNativeMapping](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getiltonativemapping-method.md) 메서드와 유사 합니다. 단, 프로파일러는 이후 릴리스에서 다시 컴파일된 함수의 ID를 지정할 수 있습니다.  
  
> [!NOTE]
> [ICorProfilerFunctionControl:: SetILInstrumentedCodeMap](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-setilinstrumentedcodemap-method.md) 메서드는 .NET Framework 4.5에서 구현 되지 않으므로 JIT 다시 컴파일된 함수는 원래 컴파일된 함수와 다른 IL-네이티브 매핑을 포함할 수 없습니다. 따라서 .NET Framework 4.5 `GetILToNativeMapping2` 에서 0이 아닌 JIT 다시 컴파일된 ID를 사용 하 여를 호출할 수 없습니다.  
  
 `GetILToNativeMapping2` 메서드는 `COR_DEBUG_IL_TO_NATIVE_MAP` 구조체의 배열을 반환합니다. 특정 범위의 네이티브 지침이 프롤로그와 같은 특정 코드 영역에 해당 하는 것을 전달 하기 위해 배열의 항목은 해당 `ilOffset` 필드를 [CorDebugIlToNativeMappingTypes](../../../../docs/framework/unmanaged-api/debugging/cordebugiltonativemappingtypes-enumeration.md) 열거형의 값으로 설정할 수 있습니다.  
  
 `GetILToNativeMapping2`가 반환된 후 `map` 버퍼가 모든 `COR_DEBUG_IL_TO_NATIVE_MAP` 구조체를 포함하기에 충분히 큰지 확인해야 합니다. 이렇게 하려면 `cMap` 값을 `pcMap` 매개 변수의 값과 비교합니다. `COR_DEBUG_IL_TO_NATIVE_MAP` 구조체의 크기를 곱한 `pcMap` 값이 `cMap`보다 크면 더 큰 `map` 버퍼를 할당하고 `cMap`를 더 큰 새 크기로 업데이트한 다음 `GetILToNativeMapping2`를 다시 호출합니다.  
  
 또는 길이가 0인 `map` 버퍼로 `GetILToNativeMapping2`를 먼저 호출하여 올바른 버퍼 크기를 구합니다. 그런 다음 버퍼 크기를 `pcMap`에 반환된 값으로 설정하고 `GetILToNativeMapping2`을 다시 호출합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [GetILToNativeMapping 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getiltonativemapping-method.md)
- [ICorProfilerInfo4 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
