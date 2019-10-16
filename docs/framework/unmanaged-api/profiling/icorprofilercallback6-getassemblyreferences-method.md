---
title: ICorProfilerCallback6::GetAssemblyReferences 메서드
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorProfilerCallback6.GetAssemblyReferences
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.assetid: 8b391afb-d79f-41bd-94ce-43ce62c6b5fc
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2c5296fbab71c67572718a58fedb9f89b064f816
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62041498"
---
# <a name="icorprofilercallback6getassemblyreferences-method"></a>ICorProfilerCallback6::GetAssemblyReferences 메서드
[.NET Framework 4.5.2 이상 버전에서 지원됨]  
  
 공용 언어 런타임이 어셈블리 참조 closure 워커를 수행할 때 어셈블리가 초기 로드 상태임을 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
HRESULT GetAssemblyReferences(        [in, string] const WCHAR* wszAssemblyPath,  
        [in] ICorProfilerAssemblyReferenceProvider* pAsmRefProvider  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `wszAssemblyPath`  
 [in] 메타데이터를 수정할 어셈블리의 경로와 이름입니다.  
  
 `pAsmRefProvider`  
 [in] 주소에 대 한 포인터를 [ICorProfilerAssemblyReferenceProvider](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-interface.md) 추가할 어셈블리를 지정 하는 인터페이스를 참조 합니다.  
  
## <a name="return-value"></a>반환 값  
 이 콜백의 반환 값은 무시됩니다.  
  
## <a name="remarks"></a>설명  
 이 콜백을 설정 하 여 제어 합니다 [COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES](../../../../docs/framework/unmanaged-api/profiling/cor-prf-high-monitor-enumeration.md) 이벤트 마스크 플래그를 호출할 때 합니다 [ICorProfilerCallback5::SetEventMask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md) 메서드. 프로파일러를 등록 하는 경우는 [ICorProfilerCallback6::GetAssemblyReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md) 콜백 메서드를 런타임에 전달에 대 한 포인터와 함께 로드할 어셈블리의 이름과 경로 [ ICorProfilerAssemblyReferenceProvider](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-interface.md) 인터페이스 개체를 메서드에 해당 합니다. 프로파일러를 호출할 수는 [icorprofilerassemblyreferenceprovider:: Addassemblyreference](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-addassemblyreference-method.md) 메서드를 `COR_PRF_ASSEMBLY_REFERENCE_INFO` 에 지정 된 어셈블리에서 참조 하려는 각 대상 어셈블리에 대 한 개체는 `GetAssemblyReferences` 콜백입니다.  
  
 프로파일러가 어셈블리 참조를 추가하기 위해 어셈블리 메타데이터를 수정해야 하는 경우에만 `GetAssemblyReferences` 콜백을 사용합니다. (하지만 실제 어셈블리의 메타 데이터 수정에서 수행 되는 참고 합니다 [icorprofilercallback:: Moduleloadfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md)콜백 메서드.) 프로파일러는 `GetAssemblyReferences` 콜백 메서드를 구현하여 모듈 로드 시 어셈블리 참조가 추가될 것임을 CLR(공용 언어 런타임)에 알려야 합니다.  그러면 프로파일러가 메타데이터 어셈블리 참조를 나중에 수정하더라도 이 초기 단계에서 CLR이 결정하는 어셈블리 공유 여부가 유효하게 유지됩니다.  따라서 프로파일러 메타데이터 수정으로 인해 발생하는 `SECURITY_E_INCOMPATIBLE_SHARE` 오류 중 일부를 방지할 수 있습니다.  
  
 프로파일러를 사용 합니다 [ICorProfilerAssemblyReferenceProvider](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-interface.md) CLR 어셈블리 참조 closure 워커에 어셈블리 참조를 추가 하려면이 메서드에서 제공 하는 개체입니다.  합니다 [ICorProfilerAssemblyReferenceProvider](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-interface.md) 개체를이 콜백 내 에서만 사용 해야 합니다. 에 대 한 호출을 [icorprofilerassemblyreferenceprovider:: Addassemblyreference](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-addassemblyreference-method.md) 메타 데이터가 수정 하지만 수정 된 어셈블리 참조 closure 워커에만이 콜백 메서드에서 이어지지는지 않습니다. 프로파일러를 사용 해야 합니다는 [IMetaDataAssemblyEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md) 내에서 어셈블리 참조를 명시적으로 추가할 개체를 [icorprofilercallback:: Moduleloadfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md) 참조에 대 한 콜백 어셈블리를 구현 하는 경우에는 `GetAssemblyReferences` 콜백 합니다.  
  
 프로파일러는 같은 어셈블리에 대 한이 콜백의 중복 호출을 받을 준비가 되어 있어야 하며 이러한 중복 호출에 대 한 동일 하 게 응답 해야 (동일한 집합을 만들어 [ICorProfilerAssemblyReferenceProvider:: AddAssemblyReference](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-addassemblyreference-method.md) 호출).  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerCallback6 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-interface.md)
- [ModuleLoadFinished 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md)
- [COR_PRF_ASSEMBLY_REFERENCE_INFO 구조체](../../../../docs/framework/unmanaged-api/profiling/cor-prf-assembly-reference-info-structure.md)
- [ICorProfilerAssemblyReferenceProvider 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-interface.md)
