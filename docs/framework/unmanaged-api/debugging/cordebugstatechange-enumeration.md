---
title: CorDebugStateChange 열거형
ms.date: 02/07/2019
api_name:
- CorDebugStateChange
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 1d4424ab-5143-4e50-a84a-ceeb4ddf3bba
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 676489880cb30ca540cb78d70797dbf4eedf7395
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739591"
---
# <a name="cordebugstatechange-enumeration"></a>CorDebugStateChange 열거형

프로세스에 대한 변경 내용을 기반으로 삭제해야 하는 캐시된 데이터의 양을 설명합니다.

## <a name="syntax"></a>구문

```cpp
typedef enum CorDebugStateChange
{
    PROCESS_RUNNING = 0x0000001,
    FLUSH_ALL       = 0x0000002,
} CorDebugStateChange;
```

## <a name="members"></a>멤버

| 멤버            | Description                                                              |
| ----------------- | ------------------------------------------------------------------------ |
| `PROCESS_RUNNING` | 프로세스가 정방향 실행을 통해 새로운 메모리 상태에 도달했습니다.            |
| `FLUSH_ALL`       | 프로세스의 메모리가 이전과 임의적으로 달라질 수 있습니다. |

## <a name="remarks"></a>설명

 멤버는 `CorDebugStateChange` 디버거를 호출 하는 경우 열거를 인수로 제공 되는 `ProcessStateChanged` 메서드 사용 하 여 [ICorDebugProcess4::ProcessStateChanged](icordebugprocess4-processstatechanged-method.md) 또는 [ICorDebugProcess6:: ProcessStateChanged](icordebugprocess6-processstatechanged-method.md)

## <a name="requirements"></a>요구 사항

 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

 **헤더:** CorDebug.idl, CorDebug.h

 **라이브러리:** CorGuids.lib

 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>참고자료

- [디버깅 열거형](debugging-enumerations.md)
- [디버깅](index.md)
