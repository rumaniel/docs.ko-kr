---
title: ICorProfilerInfo2::GetFunctionInfo2 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetFunctionInfo2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetFunctionInfo2
helpviewer_keywords:
- GetFunctionInfo2 method [.NET Framework profiling]
- ICorProfilerInfo2::GetFunctionInfo2 method [.NET Framework profiling]
ms.assetid: 0aa60f24-8bbd-4c83-83c5-86ad191b1d82
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d6c45e44f68621708d05ca43857cf1e100113166
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67771080"
---
# <a name="icorprofilerinfo2getfunctioninfo2-method"></a>ICorProfilerInfo2::GetFunctionInfo2 메서드
함수의 부모 클래스, 메타데이터 토큰 및 각 형식 인수 `ClassID`(있는 경우)를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetFunctionInfo2(  
    [in]  FunctionID funcId,  
    [in]  COR_PRF_FRAME_INFO frameInfo,  
    [out] ClassID *pClassId,  
    [out] ModuleID *pModuleId,  
    [out] mdToken *pToken,  
    [in]  ULONG32 cTypeArgs,  
    [out] ULONG32 *pcTypeArgs,  
    [out] ClassID typeArgs[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `funcId`  
 [in] 부모 클래스 및 기타 정보를 가져올 함수의 ID입니다.  
  
 `frameInfo`  
 [in] 스택 프레임에 대한 정보를 가리키는 `COR_PRF_FRAME_INFO` 값입니다.  
  
 `pClassId`  
 [out] 함수의 부모 클래스에 대한 포인터입니다.  
  
 `pModuleId`  
 [out] 함수의 부모 클래스가 정의된 모듈에 대한 포인터입니다.  
  
 `pToken`  
 [out] 함수의 메타데이터 토큰에 대한 포인터입니다.  
  
 `cTypeArgs`  
 [in] `typeArgs` 배열의 크기입니다.  
  
 `pcTypeArgs`  
 [out] `ClassID` 값의 총수에 대한 포인터입니다.  
  
 `typeArgs`  
 [out] 각각 함수의 형식 인수 ID인 `ClassID` 값의 배열입니다. 메서드가 반환되면 `typeArgs`에 `ClassID` 값이 일부 또는 모두 포함됩니다.  
  
## <a name="remarks"></a>설명  
 프로파일러 코드를 호출할 수 있습니다 [icorprofilerinfo:: Getmodulemetadata](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmodulemetadata-method.md) 가져오려고를 [메타 데이터](../../../../docs/framework/unmanaged-api/metadata/index.md) 지정 된 모듈에 대 한 인터페이스입니다. `pToken`에서 참조하는 위치로 반환되는 메타데이터 토큰을 사용하여 함수에 대한 메타데이터에 액세스할 수 있습니다.  
  
 `pClassId` 및 `typeArgs` 매개 변수를 통해 반환되는 클래스 ID 및 형식 인수는 다음 표와 같이 `frameInfo` 매개 변수에 전달되는 값에 따라 달라집니다.  
  
|`frameInfo` 매개 변수의 값|결과|  
|----------------------------------------|------------|  
|`FunctionEnter2` 콜백에서 가져온 `COR_PRF_FRAME_INFO` 값|`pClassId`에서 참조된 위치에 반환된 `ClassID` 및 `typeArgs` 배열에 반환된 모든 형식 인수가 정확합니다.|  
|`FunctionEnter2` 콜백 이외의 소스에서 가져온 `COR_PRF_FRAME_INFO`|정확한 `ClassID` 및 형식 인수를 확인할 수 없습니다. 즉, `ClassID`가 null일 수도 있고 일부 형식 인수가 <xref:System.Object>로 반환될 수도 있습니다.|  
|0|정확한 `ClassID` 및 형식 인수를 확인할 수 없습니다. 즉, `ClassID`가 null일 수도 있고 일부 형식 인수가 <xref:System.Object>로 반환될 수도 있습니다.|  
  
 `GetFunctionInfo2`가 반환된 후 `typeArgs` 버퍼가 `ClassID` 값을 모두 포함할 수 있을 만큼 충분히 큰지 확인해야 합니다. 이렇게 하려면 `pcTypeArgs`가 가리키는 값을 `cTypeArgs` 매개 변수의 값과 비교합니다. `pcTypeArgs`가 `cTypeArgs`를 `ClassID` 값의 크기로 나눈 값보다 큰 값을 가리키는 경우 더 큰 `pcTypeArgs` 버퍼를 할당하고 `cTypeArgs`를 더 큰 새 크기로 업데이트한 다음 `GetFunctionInfo2`를 다시 호출합니다.  
  
 또는 길이가 0인 `pcTypeArgs` 버퍼로 `GetFunctionInfo2`를 먼저 호출하여 올바른 버퍼 크기를 구합니다. 그런 다음 버퍼 크기를 `pcTypeArgs`에서 반환된 값을 `ClassID` 값의 크기로 나눈 값으로 설정하고 `GetFunctionInfo2`를 다시 호출합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
