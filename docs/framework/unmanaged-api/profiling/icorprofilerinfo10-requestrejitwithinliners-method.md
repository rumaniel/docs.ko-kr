---
title: ICorProfilerInfo10::RequestReJITWithInliners
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo10.RequestReJITWithInliners
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 00bfc9fc21ed39226fd21c4096305c254d73ee11
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69665721"
---
# <a name="icorprofilerinfo10requestrejitwithinliners-method"></a>ICorProfilerInfo10:: RequestReJITWithInliners 메서드

요청 된 메서드 뿐 아니라 요청 된 메서드의 모든 inliners ReJITs 합니다.

## <a name="syntax"></a>구문

```cpp
HRESULT RequestReJITWithInliners( [in]                       DWORD       dwRejitFlags,
                                  [in]                       ULONG       cFunctions,
                                  [in, size_is(cFunctions)]  ModuleID    moduleIds[],
                                  [in, size_is(cFunctions)]  mdMethodDef methodIds[]);
```

#### <a name="parameters"></a>매개 변수

`dwRejitFlags` \
진행 [COR_PRF_REJIT_FLAGS](../../../../docs/framework/unmanaged-api/profiling/cor-prf-rejit-flags-enumeration.md)의 비트 마스크입니다.

`cFunctions` \
[in] 다시 컴파일할 함수 개수입니다.

`moduleIds` \
[in] 다시 컴파일할 함수를 식별하는 (`module`, `methodDef`) 쌍의 `moduleId` 부분을 지정합니다.

`methodIds` \
[in] 다시 컴파일할 함수를 식별하는 (`module`, `methodDef`) 쌍의 `methodId` 부분을 지정합니다.

## <a name="remarks"></a>설명

[RequestReJIT](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-requestrejit-method.md) 는 인라인 메서드를 추적 하지 않습니다. 프로파일러에서 인라인 된 메서드의 모든 인스턴스가 ReJITted 하는지 확인 하기 위해 인라인 처리 `RequestReJIT` 를 차단 하거나 인라이닝을 추적 하 고 모든 inliners에 대해를 호출 해야 합니다. 프로파일러가 인라인을 모니터링 하기 위해 제공 되지 않으므로 ReJIT on attach에 문제가 발생 합니다. 이 메서드를 호출 하 여 inliners의 전체 집합을 ReJITted 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [.Net Core 지원 운영 체제](../../../core/windows-prerequisites.md#net-core-supported-operating-systems)를 참조 하세요.

**헤더:** CorProf.idl, CorProf.h

**라이브러리** CorGuids.lib

**.Net 버전:** [!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]

## <a name="see-also"></a>참고자료

- [ICorProfilerInfo10 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-interface.md)
