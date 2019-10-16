---
title: ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetFunctionFromTokenAndTypeArgs
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs
helpviewer_keywords:
- ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs method [.NET Framework profiling]
- GetFunctionFromTokenAndTypeArgs method [.NET Framework profiling]
ms.assetid: ce8f6aa6-4ebf-4a86-b429-4bbc8af41a8f
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 31fad9e82d0b93360f92676f6357c136ae60634a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67771123"
---
# <a name="icorprofilerinfo2getfunctionfromtokenandtypeargs-method"></a>ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs 메서드
가져옵니다 합니다 `FunctionID` 클래스를 포함 하는 지정 된 메타 데이터 토큰을 사용 하 여 함수 및 `ClassID` 값의 형식 인수입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetFunctionFromTokenAndTypeArgs(  
    [in] ModuleID moduleID,  
    [in] mdMethodDef funcDef,  
    [in] ClassID classId,  
    [in] ULONG32 cTypeArgs,  
    [in, size_is(cTypeArgs)] ClassID typeArgs[],  
    [out] FunctionID* pFunctionID);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleID`  
 [in] 함수가 상주 하는 모듈의 ID입니다.  
  
 `funcDef`  
 [in] `mdMethodDef` 함수를 참조 하는 메타 데이터 토큰입니다.  
  
 `classId`  
 [in] 함수의 포함 하는 클래스의 ID입니다.  
  
 `cTypeArgs`  
 [in] 지정된 된 함수에 대 한 형식 매개 변수의 수입니다. 이 값에는 제네릭이 아닌 함수에 대 한 0 이어야 합니다.  
  
 `typeArgs`  
 [in] 배열을 `ClassID` 각각는 함수의 인수 값입니다. 변수의 `typeArgs` NULL 일 수 `cTypeArgs` 0으로 설정 됩니다.  
  
 `pFunctionID`  
 [out] 에 대 한 포인터를 `FunctionID` 지정 된 함수입니다.  
  
## <a name="remarks"></a>설명  
 호출 된 `GetFunctionFromTokenAndTypeArgs` 메서드는 `mdMethodRef` 대신 메타 데이터는 `mdMethodDef` 메타 데이터 토큰에 예기치 않은 결과가 있을 수 있습니다. 호출자가 해결 해야 합니다 `mdMethodRef` 에 `mdMethodDef` 전달 되는 경우.  
  
 함수가 이미 로드 되어 있지 않으면 호출 `GetFunctionFromTokenAndTypeArgs` 발생 하는 여러 상황에서 위험한 작업 인 로드 하면 됩니다. 예를 들어 모듈이 나 형식을 로드 하는 동안이 메서드를 호출 하면 런타임에 순환 로드를 시도할 때 무한 루프 발생할 수 있습니다.  
  
 일반적으로 사용 `GetFunctionFromTokenAndTypeArgs` 것이 좋습니다. 저장 해야 프로파일러 특정 함수에 대 한 이벤트에 관심이 있는 경우는 `ModuleID` 및 `mdMethodDef` 사용 하 여 해당 함수 [ICorProfilerInfo2::GetFunctionInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md) 검사할 여부를 지정 된 `FunctionID` 는 원하는 함수입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
