---
title: ICorProfilerInfo7::ReadInMemorySymbols
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo7.ReadInMemorySymbols
api_location:
- CorProf.idl
- CorProf.h
- CorGuids.lib
api_type:
- COM
ms.assetid: 1745a0b9-8332-4777-a670-b549bff3b901
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 95b463b23c230d620d746e48da49d75238ef2cb7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955367"
---
# <a name="icorprofilerinfo7readinmemorysymbols"></a>ICorProfilerInfo7::ReadInMemorySymbols
[.NET Framework 4.6.1 이상 버전에서 지원됨]  
  
 메모리 내 기호 스트림에서 바이트를 읽습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ReadInMemorySymbols(  
        [in] ModuleID moduleId,  
        [in] DWORD symbolsReadOffset,  
        [out] BYTE* pSymbolBytes,  
        [in] DWORD countSymbolBytes,  
        [out] DWORD* pCountSymbolBytesRead  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleId`  
 진행 메모리 내 스트림을 포함 하는 모듈의 식별자입니다.  
  
 `symbolsReadOffset`  
 진행 바이트 읽기를 시작할 메모리 내 스트림 내의 오프셋입니다.  
  
 `pSymbolBytes`  
 제한이 데이터가 복사 될 버퍼에 대 한 포인터입니다. 버퍼 `countSymbolBytes` 에 사용 가능한 공간이 있어야 합니다.  
  
 `countSymbolBytes`  
 진행 복사할 바이트 수입니다.  
  
 `pCountSymbolBytesRead`  
 제한이 메서드가 반환 될 때 읽은 실제 바이트 수를 포함 합니다.  
  
## <a name="return-value"></a>반환 값  
 `S_OK`0이 아닌 바이트 수를 읽은 경우입니다.  
  
 `CORPROF_E_MODULE_IS_DYNAMIC`를 사용 하 여 <xref:System.Reflection.Emit>모듈을 만든 경우입니다.  
  
## <a name="remarks"></a>설명  
 메서드 `ReadInMemorySymbols` 는 메모리 내 스트림 `countSymbolBytes` 내의 오프셋 `symbolsReadOffset` 에서 시작 하는 데이터를 읽으려고 시도 합니다. 데이터가에 `pSymbolBytes`복사 됩니다 .이는 사용 가능한 공간이 있어야 `countSymbolBytes` 합니다.     `pCountSymbolsBytesRead`읽은 실제 바이트 수를 포함 합니다. 스트림의 끝에 도달 하 `countSymbolBytes` 는 경우 보다 적을 수 있습니다.  
  
> [!NOTE]
> 현재 구현에서는 리플렉션 내보내기를 지원 하지 않습니다. 리플렉션을 사용 하 여 모듈을 만든 경우이 메서드는를 반환 `CORPROF_E_MODULE_IS_DYNAMIC`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo7 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md)
