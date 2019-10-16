---
title: ICorProfilerInfo2::GetClassIDInfo2 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetClassIDInfo2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetClassIDInfo2
helpviewer_keywords:
- GetClassIDInfo2 method [.NET Framework profiling]
- ICorProfilerInfo2::GetClassIDInfo2 method [.NET Framework profiling]
ms.assetid: 0141d582-d066-4d49-8d1f-ae82129a1960
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 892379d3281a98821b7feb5250973fac74f1f4f6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67751849"
---
# <a name="icorprofilerinfo2getclassidinfo2-method"></a>ICorProfilerInfo2::GetClassIDInfo2 메서드
부모 모듈 및 메타 데이터를 지정된 된 클래스의 제네릭 정의 열기에 대 한 토큰 가져옵니다 합니다 `ClassID` , 부모 클래스의 및 `ClassID` 있는 클래스의 경우 각 형식 인수에 대 한 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetClassIDInfo2(  
    [in]  ClassID classId,  
    [out] ModuleID *pModuleId,  
    [out] mdTypeDef *pTypeDefToken,  
    [out] ClassID *pParentClassId,  
    [in]  ULONG32 cNumTypeArgs,  
    [out] ULONG32 *pcNumTypeArgs,  
    [out] ClassID typeArgs[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `classId`  
 [in] 정보가 검색되는 클래스의 ID입니다.  
  
 `pModuleId`  
 [out] 지정된 된 클래스의 제네릭 정의 열기에 대 한 부모 모듈의 ID에 대 한 포인터입니다.  
  
 `pTypeDefToken`  
 [out] 지정된 된 클래스의 제네릭 정의 열기에 대 한 메타 데이터 토큰에 대 한 포인터입니다.  
  
 `pParentClassId`  
 [out] 부모 클래스의 ID에 대한 포인터입니다.  
  
 `cNumTypeArgs`  
 [in] `typeArgs` 배열의 크기입니다.  
  
 `pcNumTypeArgs`  
 [out] 사용 가능한 요소의 총수에 대한 포인터입니다.  
  
 `typeArgs`  
 [out] 각각 클래스의 형식 인수 ID를 나타내는 `ClassID` 값의 배열입니다. 메서드가 반환되면 `typeArgs`에 사용 가능한 `ClassID` 값이 일부 또는 모두 포함됩니다.  
  
## <a name="remarks"></a>설명  
 합니다 `GetClassIDInfo2` 메서드는 비슷합니다는 [icorprofilerinfo:: Getclassidinfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassidinfo-method.md) 메서드를 하지만 `GetClassIDInfo2` 제네릭 형식에 대 한 추가 정보를 가져옵니다.  
  
 프로파일러 코드를 호출할 수 있습니다 [icorprofilerinfo:: Getmodulemetadata](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmodulemetadata-method.md) 가져오려고를 [메타 데이터](../../../../docs/framework/unmanaged-api/metadata/index.md) 지정 된 모듈에 대 한 인터페이스입니다. 그런 다음 `pTypeDefToken`에서 참조된 위치로 반환되는 메타데이터 토큰을 사용하여 클래스에 대한 메타데이터에 액세스할 수 있습니다.  
  
 `GetClassIDInfo2`가 반환된 후 `typeArgs` 버퍼가 `ClassID` 값을 모두 포함할 수 있을 만큼 충분히 큰지 확인해야 합니다. 이렇게 하려면 `pcNumTypeArgs`가 가리키는 값을 `cNumTypeArgs` 매개 변수의 값과 비교합니다. `pcNumTypeArgs`이 `cNumTypeArgs`보다 큰 값을 가리키는 경우 더 큰 `typeArgs` 버퍼를 할당하고 `cNumTypeArgs`을 더 큰 새 크기로 업데이트한 후 `GetClassIDInfo2`를 다시 호출합니다.  
  
 또는 길이가 0인 `typeArgs` 버퍼로 `GetClassIDInfo2`를 먼저 호출하여 올바른 버퍼 크기를 구합니다. 그런 다음 `typeArgs` 버퍼 크기를 `pcNumTypeArgs`에 반환된 값으로 설정하고 `GetClassIDInfo2`를 다시 호출합니다.  
  
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
