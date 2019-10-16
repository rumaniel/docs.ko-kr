---
title: ICorProfilerInfo7::GetInMemorySymbolsLength Method
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo7.GetInMemorySymbolsLength
api_location:
- mscorwks.dll
- icorprof.idl
api_type:
- COM
ms.assetid: d62c4a4c-8a62-45aa-8f01-a8387cf36159
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 157b0e215f8afa58cccb3d54a65baa9c307ba966
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955420"
---
# <a name="icorprofilerinfo7getinmemorysymbolslength-method"></a>ICorProfilerInfo7::GetInMemorySymbolsLength Method
[.NET Framework 4.6.1 이상 버전에서 지원됨]  
  
 메모리 내 기호 스트림의 길이를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetInMemorySymbolsLength(  
        [in] ModuleID moduleId,  
        [out] DWORD* pCountSymbolBytes  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleId`  
 진행 메모리 내 스트림을 포함 하는 모듈의 식별자입니다.  
  
 pCountSymbolBytes  
 제한이 메서드가 반환 될 때 `DWORD` 스트림의 길이 (바이트)를 포함 하는 값에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 메모리 스트림의 길이가 `S_OK` 0 인 경우에도이 메서드는를 반환 합니다.  
  
 메서드는를 `CORPROF_E_MODULE_IS_DYNAMIC` 사용 하 여 <xref:System.Reflection.Emit?displayProperty=nameWithType>메서드를 만든 경우를 반환 합니다.  
  
## <a name="remarks"></a>설명  
 모듈에 메모리 내 기호가 있으면 스트림의 길이가에 `pCountSymbolBytes`배치 됩니다. 모듈에 메모리 내 기호 ( `*pCountSymbolBytes = 0`)가 없는 경우  
  
> [!NOTE]
> 현재 구현에서는 리플렉션 내보내기를 지원 하지 않습니다. 리플렉션을 사용 하 여 모듈을 만든 경우이 메서드는를 반환 `CORPROF_E_MODULE_IS_DYNAMIC`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo7 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md)
