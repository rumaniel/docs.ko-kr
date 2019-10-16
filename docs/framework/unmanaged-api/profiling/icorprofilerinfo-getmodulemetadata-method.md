---
title: ICorProfilerInfo::GetModuleMetaData 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetModuleMetaData
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetModuleMetaData
helpviewer_keywords:
- GetModuleMetaData method [.NET Framework profiling]
- ICorProfilerInfo::GetModuleMetaData method [.NET Framework profiling]
ms.assetid: 7a439d92-348a-44dd-b60f-cad7cba56379
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2e63cf698e41e70084c9b71bdf58d7ac60723d53
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782785"
---
# <a name="icorprofilerinfogetmodulemetadata-method"></a>ICorProfilerInfo::GetModuleMetaData 메서드
지정된 된 모듈에 매핑되는 메타 데이터 인터페이스 인스턴스를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetModuleMetaData(  
    [in]  ModuleID moduleId,  
    [in]  DWORD    dwOpenFlags,  
    [in]  REFIID   riid,  
    [out] IUnknown **ppOut);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleId`  
 [in] 인터페이스 인스턴스를 매핑할 수 있는 모듈의 ID입니다.  
  
 `dwOpenFlags`  
 [in] 값을 [CorOpenFlags](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md) 매니페스트 파일을 열기 위한 모드를 지정 하는 열거형입니다. 만 `ofRead`, `ofWrite` 및 `ofNoTransform` 비트 유효 합니다.  
  
 `riid`  
 [in] 참조 된 인스턴스를 검색할 수는 메타 데이터 인터페이스의 ID (GUID)입니다. 참조 [메타 데이터 인터페이스](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md) 인터페이스의 목록은 합니다.  
  
 `ppOut`  
 [out] 메타 데이터 인터페이스 인스턴스 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 메타 데이터 읽기/쓰기 모드에서 열 수를 요청할 수 있습니다 하지만 프로그램의 메타 데이터 실행 속도가 느려지게 됩니다 처럼 컴파일러에서 메타 데이터 변경 때문에 최적화 수 없습니다.  
  
 일부 모듈 (예: 리소스 모듈) 메타 데이터가 없는 경우 이러한 경우 `GetModuleMetaData` S_FALSE를 및 null HRESULT 값을 반환 합니다 *`ppOut`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
