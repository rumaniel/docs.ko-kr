---
title: DacpReJitData 구조체
ms.date: 02/01/2019
api.name:
- DacpReJitData Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpReJitData Structure
helpviewer.keywords:
- DacpReJitData Structure [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 77ef2c65157df4a033700bb8d0295875ede46554
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739105"
---
# <a name="dacprejitdata-structure"></a>DacpReJitData 구조체

지정 된 프로파일러가 계측 메서드에 대 한 기본 정보를 정의 합니다.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>구문

```cpp
struct MSLAYOUT DacpReJitData
{
    enum Flags
    {
        kUnknown,
        kRequested,
        kActive,
        kReverted,
    };

    CLRDATA_ADDRESS                 rejitID;
    Flags                           flags;
    CLRDATA_ADDRESS                 NativeCodeAddr;
};
```

## <a name="members"></a>멤버

| 멤버           | 설명                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------------------ |
| `rejitID`        | 메서드에 대 한 ReJit 수정 번호입니다.                                                          |
| `flags`          | 지정된 된 버전에 대 한 메서드의 ReJit 계측의 현재 상태를 나타내는 플래그입니다. |
| `NativeCodeAddr` | 메서드의 rejitted 구현의 기본 주소입니다.                                         |

## <a name="remarks"></a>설명

이 구조는 런타임 내에서 있으며 모든 헤더 또는 라이브러리 파일을 통해 노출 되지 않습니다. 를 사용 하려면 위에서 지정한 대로 구조를 정의 합니다. 사용 하 여 구조 정의 해야 `ms_struct` 압축 사용 하지 않는 경우 Microsoft 컴파일러.

## <a name="requirements"></a>요구 사항
**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
**헤더:** 없음  
**라이브러리:** 없음  
**.NET Framework 버전:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>참고자료

- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [디버깅 구조체](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
