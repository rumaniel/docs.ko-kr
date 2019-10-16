---
title: ICorProfilerInfo9::GetCodeInfo4
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo9.GetCodeInfo4
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: e6708971909c1035e41786f4d8dad1cf9afdffaf
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69665622"
---
# <a name="icorprofilerinfo9getcodeinfo4-method"></a>ICorProfilerInfo9:: GetCodeInfo4 메서드

네이티브 코드 시작 주소가 지정 된 경우이 코드를 저장 하는 가상 메모리 블록을 반환 합니다.

## <a name="syntax"></a>구문

```cpp
HRESULT GetCodeInfo4( [in]  UINT_PTR pNativeCodeStartAddress,
                      [in]  ULONG32 cCodeInfos,
                      [out] ULONG32* pcCodeInfos,
                      [out] COR_PRF_CODE_INFO codeInfos[]);
```

#### <a name="parameters"></a>매개 변수

`pNativeCodeStartAddress` \
진행 네이티브 함수의 시작 부분에 대 한 포인터입니다.

`cCodeInfos` \
[in] `codeInfos` 배열의 크기입니다.

`pcCodeInfos` \
제한이 사용할 수 있는 [COR_PRF_CODE_INFO](../../../../docs/framework/unmanaged-api/profiling/cor-prf-code-info-structure.md) 구조체의 총 수에 대 한 포인터입니다.

`codeInfos` \
[out] 호출자가 제공한 버퍼입니다. 메서드가 반환된 후에는 각각 네이티브 코드 블록을 설명하는 `COR_PRF_CODE_INFO` 구조체의 배열을 포함합니다.

## <a name="remarks"></a>설명

메서드 `GetCodeInfo4` 는 메서드의 다른 네이티브 버전에 대 한 코드 정보를 조회할 수 있다는 점을 제외 하 고 [GetCodeInfo3](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getcodeinfo3-method.md)와 비슷합니다.

> [!NOTE]
> `GetCodeInfo4`가비지 수집을 트리거할 수 있습니다.

범위는 CIL(Common Intermediate Language) 오프셋의 오름차순으로 정렬됩니다.

가 `GetCodeInfo4` 반환 된 후 `codeInfos` 버퍼가 모든 [COR_PRF_CODE_INFO](../../../../docs/framework/unmanaged-api/profiling/cor-prf-code-info-structure.md) 구조를 포함할 수 있을 만큼 충분히 큰지 확인 해야 합니다. 이렇게 하려면 `cCodeInfos` 값을 `cchName` 매개 변수의 값과 비교합니다. `pcCodeInfos` [COR_PRF_CODE_INFO 구조체](../../../../docs/framework/unmanaged-api/profiling/cor-prf-code-info-structure.md) 의 크기로 `codeInfos` `cCodeInfos` `GetCodeInfo4` 나눈 값이 보다 작으면 더 큰 버퍼를 할당 하 고를 더 큰 새 크기로 업데이트 한 다음를 다시 호출 합니다. `cCodeInfos`

또는 길이가 0인 `codeInfos` 버퍼로 `GetCodeInfo4`를 먼저 호출하여 올바른 버퍼 크기를 구합니다. 그런 다음 `codeInfos` 버퍼 크기를에서 `pcCodeInfos`반환 된 값으로 설정 하 고 [COR_PRF_CODE_INFO](../../../../docs/framework/unmanaged-api/profiling/cor-prf-code-info-structure.md) 구조체의 크기를 곱한 다음를 다시 호출할 `GetCodeInfo4` 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [.Net Core 지원 운영 체제](../../../core/windows-prerequisites.md#net-core-supported-operating-systems)를 참조 하세요.

**헤더:** CorProf.idl, CorProf.h

**라이브러리** CorGuids.lib

**.Net 버전:** [!INCLUDE[net_core_22](../../../../includes/net-core-22-md.md)]

## <a name="see-also"></a>참고자료

- [ICorProfilerInfo9 인터페이스](../../../../docs/framework/unmanaged-api/profiling/ICorProfilerInfo9-interface.md)
