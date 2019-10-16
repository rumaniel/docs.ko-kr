---
title: ICorProfilerInfo8::GetFunctionFromIP3
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo8.GetFunctionFromIP3
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: df9ecc9bc355c12f993763820eb5065ba8bcc36b
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855922"
---
# <a name="icorprofilerinfo8getfunctionfromip3-method"></a>ICorProfilerInfo8:: GetFunctionFromIP3 메서드

관리 코드 명령 포인터를 FunctionID에 매핑합니다. 이 메서드는 동적 메서드와 비동적 메서드 모두에 대해 작동 합니다.

## <a name="syntax"></a>구문

```cpp
HRESULT GetFunctionFromIP3([in] LPCBYTE ip,
                           [out] FunctionID *functionId,
                           [out] ReJITID * pReJitId);
```

#### <a name="parameters"></a>매개 변수

`ip` \
진행 관리 코드의 명령 포인터입니다.

`pFunctionId` \
제한이 함수 ID입니다.

`pReJitId` \
제한이 함수의 JIT 다시 컴파일된 버전 id입니다.

## <a name="remarks"></a>설명

이 메서드는 동적 메서드와 비동적 메서드 모두에 대해 작동 합니다. 메타 데이터를 사용 하는 함수에만 작동 하는 [GetFunctionFromIP2](icorprofilerinfo4-getfunctionfromip2-method.md)의 상위 집합입니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

**헤더:** CorProf.idl, CorProf.h

**라이브러리** CorGuids.lib

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [ICorProfilerInfo8 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo8-interface.md)
