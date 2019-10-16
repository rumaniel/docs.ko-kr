---
title: ICorProfilerInfo::GetModuleInfo 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetModuleInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetModuleInfo
helpviewer_keywords:
- GetModuleInfo method [.NET Framework profiling]
- ICorProfilerInfo::GetModuleInfo method [.NET Framework profiling]
ms.assetid: 5a90d16f-7929-4987-8f83-a631becf564d
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ceca2133068d3ed011b9499024d127a3dd9279ed
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782779"
---
# <a name="icorprofilerinfogetmoduleinfo-method"></a>ICorProfilerInfo::GetModuleInfo 메서드
모듈 ID가 지정된 경우 모듈의 파일 이름 및 모듈의 부모 어셈블리 ID를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetModuleInfo(  
    [in]  ModuleID   moduleId,  
    [out] LPCBYTE    *ppBaseLoadAddress,  
    [in]  ULONG      cchName,  
    [out] ULONG      *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
          WCHAR      szName[] ,  
    [out] AssemblyID *pAssemblyId);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleId`  
 [in] 정보가 검색되는 모듈의 ID입니다.  
  
 `ppBaseLoadAddress`  
 [out] 모듈이 로드되는 기본 주소입니다.  
  
 `cchName`  
 [in] `szName` 반환 버퍼의 길이(문자)입니다.  
  
 `pcchName`  
 [out] 반환되는 모듈 파일 이름의 총 문자 길이에 대한 포인터입니다.  
  
 `szName`  
 [out] 호출자가 제공한 와이드 문자 버퍼입니다. 메서드가 반환되면 이 버퍼에 모듈의 파일 이름이 포함됩니다.  
  
 `pAssemblyId`  
 [out] 모듈의 부모 어셈블리 ID에 대한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 동적 모듈의 경우 `szName` 매개 변수는 빈 문자열이고 기본 주소는 0입니다.  
  
 하지만 합니다 `GetModuleInfo` 모듈의 ID가 즉시 메서드를 호출할 수 있습니다, 프로파일러를 받을 때까지 부모 어셈블리의 ID를 사용할 수 없습니다 합니다 [icorprofilercallback:: Moduleattachedtoassembly](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleattachedtoassembly-method.md) 콜백 합니다.  
  
 `GetModuleInfo`가 반환된 후 `szName` 버퍼가 모듈의 전체 파일 이름을 포함하기에 충분히 큰지 확인해야 합니다. 이렇게 하려면 `pcchName`가 가리키는 값을 `cchName` 매개 변수의 값과 비교합니다. `pcchName`이 `cchName`보다 큰 값을 가리키는 경우 더 큰 `szName` 버퍼를 할당하고 `cchName`을 더 큰 새 크기로 업데이트한 후 `GetModuleInfo`를 다시 호출합니다.  
  
 또는 길이가 0인 `szName` 버퍼로 `GetModuleInfo`를 먼저 호출하여 올바른 버퍼 크기를 구합니다. 그런 다음 버퍼 크기를 `pcchName`에 반환된 값으로 설정하고 `GetModuleInfo`을 다시 호출합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
- [GetModuleInfo2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getmoduleinfo2-method.md)
