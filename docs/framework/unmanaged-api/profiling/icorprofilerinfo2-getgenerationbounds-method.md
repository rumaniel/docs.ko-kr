---
title: ICorProfilerInfo2::GetGenerationBounds 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetGenerationBounds
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetGenerationBounds
helpviewer_keywords:
- ICorProfilerInfo2::GetGenerationBounds method [.NET Framework profiling]
- GetGenerationBounds method [.NET Framework profiling]
ms.assetid: 9c37185f-d1e0-4a6e-8b99-707f7df61d88
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: eee04315e18a6e0442271858b75783a081468f90
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776720"
---
# <a name="icorprofilerinfo2getgenerationbounds-method"></a>ICorProfilerInfo2::GetGenerationBounds 메서드
다양한 가비지 컬렉션 세대를 구성하는 힙 세그먼트인 메모리 영역을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetGenerationBounds(  
    [in]  ULONG cObjectRanges,  
    [out] ULONG *pcObjectRanges,  
    [out, size_is(cObjectRanges), length_is(*pcObjectRanges)] COR_PRF_GC_GENERATION_RANGE ranges[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cObjectRanges`  
 [in] `ranges` 배열에 대해 호출자가 할당한 요소 수입니다.  
  
 `pcObjectRanges`  
 [out] 일부 또는 전체가 `ranges` 배열로 반환되는 총 범위 수를 지정하는 정수에 대한 포인터입니다.  
  
 `ranges`  
 [out] 배열을 [COR_PRF_GC_GENERATION_RANGE](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-generation-range-structure.md) 가비지 컬렉션 중인 세대 내의 메모리 범위 (즉, 블록)를 설명 하는 각 구조입니다.  
  
## <a name="remarks"></a>설명  
 가비지 컬렉션이 진행되고 있지 않으면 모든 프로파일러 콜백에서 `GetGenerationBounds` 메서드를 호출할 수 있습니다.

 대부분의 세대 이동은 가비지 수집 중에 발생합니다. 컬렉션 간에 세대가 증가할 수 있지만 일반적으로 이동하지는 않습니다. 따라서 가장 흥미로운 `GetGenerationBounds` 호출 위치는 `ICorProfilerCallback2::GarbageCollectionStarted` 및 `ICorProfilerCallback2::GarbageCollectionFinished`입니다.  
  
 프로그램 시작 중에 일부 개체는 CLR(공용 언어 런타임)에 의해 일반적으로 3세대 및 0세대에서 할당됩니다. 따라서 관리 코드 실행이 시작되는 시간에는 이러한 세대에 이미 개체가 포함되어 있습니다. 1세대와 2세대는 가비지 수집기에서 생성되는 더미 개체를 제외하고 일반적으로 비어 있습니다. 더미 개체의 크기는 32비트 CLR 구현에서 12바이트이고 64비트 구현에서는 크기가 더 큽니다. 네이티브 이미지 생성기(NGen.exe)에 의해 생성된, 모듈 내에 있는 2세대 범위가 표시될 수도 있습니다. 이 경우에 2 세대의 개체는 *개체를 고정*, NGen.exe가 실행 하는 경우 보다는 가비지 수집기에 의해 할당 되는 합니다.  
  
 이 함수는 호출자 할당 버퍼를 사용합니다.  
  
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
