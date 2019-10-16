---
title: ICorProfilerInfo::SetILInstrumentedCodeMap 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetILInstrumentedCodeMap
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetILInstrumentedCodeMap
helpviewer_keywords:
- ICorProfilerInfo::SetILInstrumentedCodeMap method [.NET Framework profiling]
- SetILInstrumentedCodeMap method [.NET Framework profiling]
ms.assetid: bce1dcf8-b4ec-4e73-a917-f2df1ad49c8a
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 65eee2e834251817b461f1cd1debf212696d5a5f
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855696"
---
# <a name="icorprofilerinfosetilinstrumentedcodemap-method"></a>ICorProfilerInfo::SetILInstrumentedCodeMap 메서드

지정 된 MSIL (Microsoft 중간 언어) 맵 항목을 사용 하 여 지정 된 함수에 대 한 코드 맵을 설정 합니다.

> [!NOTE]
> .NET Framework 버전 2.0에서 특정 응용 프로그램 `SetILInstrumentedCodeMap` 도메인의 `FunctionID` 제네릭 함수를 나타내는에 대해를 호출 하면 응용 프로그램 도메인에 있는 해당 함수의 모든 인스턴스에 영향을 줍니다.

## <a name="syntax"></a>구문

```cpp
HRESULT SetILInstrumentedCodeMap(
    [in]  FunctionID functionId,
    [in]  BOOL       fStartJit,
    [in]  ULONG      cILMapEntries,
    [in, size_is(cILMapEntries)] COR_IL_MAP rgILMapEntries[]);
```

## <a name="parameters"></a>매개 변수

`functionId`\
진행 코드 맵을 설정할 함수의 ID입니다.

`fStartJit`\
진행 `SetILInstrumentedCodeMap` 메서드에 대 한 호출이 특정 `FunctionID`에 대해 첫 번째 인지 여부를 나타내는 부울 값입니다. `SetILInstrumentedCodeMap` `false` `fStartJit` 지정`FunctionID`된에 대 한 첫 번째 호출 에서을로설정하고,그이후에를로설정합니다.`true`

`cILMapEntries`\
진행 `cILMapEntries` 배열의 요소 수입니다.

`rgILMapEntries`\
진행 각각 MSIL 오프셋을 지정 하는 COR_IL_MAP 구조체의 배열입니다.

## <a name="remarks"></a>설명

프로파일러는 메서드를 계측 하기 위해 메서드 소스 코드 내에 문을 삽입 하는 경우가 있습니다. 예를 들어 지정 된 소스 줄에 도달할 때 알림을 받을 수 있습니다. `SetILInstrumentedCodeMap`프로파일러가 원래 MSIL 명령을 새 위치에 매핑할 수 있도록 합니다. 프로파일러는 [ICorProfilerInfo:: GetILToNativeMapping](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getiltonativemapping-method.md) 메서드를 사용 하 여 지정 된 네이티브 오프셋의 원래 MSIL 오프셋을 가져올 수 있습니다.

디버거는 각각의 이전 오프셋이 원래 수정 되지 않은 MSIL 코드 내에서 MSIL 오프셋을 참조 하 고 각각의 새 오프셋이 새로운 계측 된 코드 내에서 MSIL 오프셋을 참조 한다고 가정 합니다. 맵은 오름차순으로 정렬 되어야 합니다. 단계별 실행이 제대로 작동 하려면 다음 지침을 따르세요.

- 계측 된 MSIL 코드를 다시 정렬 하지 않습니다.

- 원래 MSIL 코드를 제거 하지 마십시오.

- 맵의 PDB (프로그램 데이터베이스) 파일에서 모든 시퀀스 위치에 대 한 항목을 포함 합니다. 지도는 누락 된 항목을 보간 하지 않습니다. 따라서 다음 맵이 제공 됩니다.

  (0 이전, 0 개 새로 만들기)

  (5 이전, 10 개 새)

  (9 이전, 20 개 새로 만들기)

  - 0, 1, 2, 3 또는 4의 이전 오프셋은 새 오프셋 0에 매핑됩니다.

  - 5, 6, 7 또는 8의 이전 오프셋은 새 오프셋 10에 매핑됩니다.

  - 이전 오프셋 9 이상은 새 오프셋 20에 매핑됩니다.

  - 0, 1, 2, 3, 4, 5, 6, 7, 8 또는 9의 새 오프셋은 이전 오프셋 0에 매핑됩니다.

  - 새 오프셋 10, 11, 12, 13, 14, 15, 16, 17, 18 또는 19는 이전 오프셋 5에 매핑됩니다.

  - 새 오프셋 20 이상은 이전 오프셋 9에 매핑됩니다.

.NET Framework 3.5 및 이전 버전에서는 [CoTaskMemAlloc](/windows/desktop/api/combaseapi/nf-combaseapi-cotaskmemalloc) 메서드를 호출 하 `rgILMapEntries` 여 배열을 할당 합니다. 런타임에서는이 메모리의 소유권을 가지 므로 프로파일러를 해제 하려고 해서는 안 됩니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

**헤더:** CorProf.idl, CorProf.h

**라이브러리** CorGuids.lib

**.NET Framework 버전:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]

## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
