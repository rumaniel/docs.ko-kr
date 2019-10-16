---
title: ICorDebugProcess4::ProcessStateChanged 메서드
ms.date: 02/07/2019
api_name:
- ICorDebugProcess4::ProcessStateChanged
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess4::ProcessStateChanged
helpviewer_keywords:
- ICorDebugProcess4::ProcessStateChanged method [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: adfd563e19389642ac0ed0a3cef4aae8a32fa466
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67767192"
---
# <a name="icordebugprocess4processstatechanged-method"></a>ICorDebugProcess4::ProcessStateChanged 메서드

디버거 프로세스의 디버기의 실행을 계속 되는 ICorDebug 파이프라인에 알립니다.

## <a name="syntax"></a>구문

```cpp
HRESULT ProcessStateChanged(
    [in] CorDebugStateChange change
);
```

## <a name="parameters"></a>매개 변수

 `eChange`\
[in] 멤버는 [CorDebugStateChange 열거형](cordebugstatechange-enumeration.md) 프로세스의 실행 상태 변경을 설명 합니다.

## <a name="remarks"></a>설명

제공 된 메서드는의 일부는 `ICorDebugProcess4` 인터페이스 및 가상 메서드 테이블의 네 번째 슬롯에 해당 합니다.

## <a name="requirements"></a>요구 사항

 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

 **헤더:** 없음

 **라이브러리:** 없음
 
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>참고자료

- [ICorDebugProcess4 인터페이스](icordebugprocess4-interface.md)
- [디버깅 인터페이스](debugging-interfaces.md)
- [디버깅](index.md)
