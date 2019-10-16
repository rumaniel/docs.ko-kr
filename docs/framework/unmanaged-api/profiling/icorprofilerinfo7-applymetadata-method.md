---
title: ICorProfilerInfo7::ApplyMetaData 메서드
ms.date: 02/15/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo7.ApplyMetaData
api_location:
- mscorwks.dll
api_type:
- COM
ms.assetid: a1bfb649-4584-4d35-b3e6-8fe59b53992a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8f261b02dd19ead0d6803cae543f39a06c99f033
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64586696"
---
# <a name="icorprofilerinfo7applymetadata-method"></a>ICorProfilerInfo7::ApplyMetaData 메서드
[.NET Framework 4.6.1 이상 버전에서 지원됨]  
  
 새로 정의한 메타 데이터를 적용 합니다 `IMetadataEmit::Define*` 지정된 된 모듈에는 메서드.  
  
## <a name="syntax"></a>구문  
  
```cpp
HRESULT ApplyMetaData(  
        [in] ModuleID moduleID  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleID`  
 [in] 해당 메타 데이터가 변경 된 모듈의 식별자입니다.  
  
## <a name="remarks"></a>설명  
 후 메타 데이터를 변경 하는 경우는 [ModuleLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md) 콜백 새 메타 데이터를 사용 하기 전에이 메서드를 호출 해야 합니다.  
  
 `ApplyMetaData` 다음과 같은 유형의 메타 데이터를 추가 지원 합니다.  
  
- `AssemblyRef` 호출 하 여 만든 레코드를 [imetadataassemblyemit:: Defineassemblyref](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-defineassemblyref-method.md)합니다. 메서드를 재정의합니다.  
  
- `TypeRef` 호출 하 여 만든 레코드를 [imetadataemit:: Definetyperefbyname](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetyperefbyname-method.md) 메서드.  
  
- `TypeSpec` 호출 하 여 만든 레코드를 [imetadataemit:: Gettokenfromtypespec](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-gettokenfromtypespec-method.md) 메서드.  
  
- `MemberRef` 호출 하 여 만든 레코드를 [imetadataemit:: Definememberref](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definememberref-method.md) 메서드.  
  
- `MemberSpec` 호출 하 여 만든 레코드를 [IMetaDataEmit2::DefineMethodSpec](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-definemethodspec-method.md) 메서드.  
  
- `UserString` 호출 하 여 만든 레코드를 [imetadataemit:: Defineuserstring](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineuserstring-method.md) 메서드.  

.NET Core 3.0부터 `ApplyMetaData` 도 지원 합니다.

- `TypeDef` 호출 하 여 만든 레코드를 [imetadataemit:: Definetypedef](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetypedef-method.md) 메서드.

- `MethodDef` 호출 하 여 만든 레코드를 [imetadataemit:: Definemethod](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definemethod-method.md) 메서드. 그러나 가상 메서드를 기존 형식에 추가 지원 되지 않습니다. 하기 전에 가상 메서드를 추가 해야 합니다 [ModuleLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md) 콜백 합니다.

## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo7 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md)
