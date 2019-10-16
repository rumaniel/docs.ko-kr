---
title: ICorProfilerInfo2::GetClassFromTokenAndTypeArgs 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetClassFromTokenAndTypeArgs
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetClassFromTokenAndTypeArgs
helpviewer_keywords:
- GetClassFromTokenAndTypeArgs method [.NET Framework profiling]
- ICorProfilerInfo2::GetClassFromTokenAndTypeArgs method [.NET Framework profiling]
ms.assetid: b25c88f0-71b9-443b-8eea-1c94db0a44b9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a88a6c19a5c8b45576dd6f632adf70f7ec2eed55
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67751880"
---
# <a name="icorprofilerinfo2getclassfromtokenandtypeargs-method"></a>ICorProfilerInfo2::GetClassFromTokenAndTypeArgs 메서드
가져옵니다 합니다 `ClassID` 지정 된 메타 데이터 토큰을 사용 하 여 형식 및 `ClassID` 값의 형식 인수입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetClassFromTokenAndTypeArgs(  
    [in] ModuleID moduleID,  
    [in] mdTypeDef typeDef,  
    [in] ULONG32 cTypeArgs,  
    [in, size_is(cTypeArgs)] ClassID typeArgs[],  
    [out] ClassID* pClassID);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleID`  
 [in] ID 형식 상주 하는 모듈입니다.  
  
 `typeDef`  
 [in] `mdTypeDef` 유형을 참조 하는 메타 데이터 토큰입니다.  
  
 `cTypeArgs`  
 [in] 지정 된 형식의 형식 매개 변수의 수입니다. 이 값은 제네릭이 아닌 형식에는 0 이어야 합니다.  
  
 `typeArgs`  
 [in] 배열을 `ClassID` 값에는 각각 인수 형식입니다. 변수의 `typeArgs` NULL 일 수 `cTypeArgs` 0으로 설정 됩니다.  
  
 `pClassID`  
 [out] 에 대 한 포인터를 `ClassID` 지정된 된 형식입니다.  
  
## <a name="remarks"></a>설명  
 호출를 `GetClassFromTokenAndTypeArgs` 메서드는 `mdTypeRef` 대신는 `mdTypeDef` 메타 데이터 토큰이 예기치 않은 결과 가질 수 있으며 호출자가 해결 해야 합니다는 `mdTypeRef` 에 `mdTypeDef` 전달 되는 경우.  
  
 형식을 아직 로드 되지 않은, 경우 호출 `GetClassFromTokenAndTypeArgs` 로드는 여러 상황에서 위험한 작업이 트리거됩니다. 예를 들어 모듈이 나 다른 형식을 로드 하는 동안이 메서드를 호출 하면 런타임에 순환 로드를 시도할 때 무한 루프 발생할 수 있습니다.  
  
 일반적으로 사용 `GetClassFromTokenAndTypeArgs` 것이 좋습니다. 저장 해야 프로파일러 특정 형식에 대 한 이벤트에 관심이 있는 경우는 `ModuleID` 및 `mdTypeDef` 해당 형식 및 사용 하 여 [ICorProfilerInfo2::GetClassIDInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassidinfo2-method.md) 검사할 여부를 지정 `ClassID` 은 합니다 필요한 형식입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
