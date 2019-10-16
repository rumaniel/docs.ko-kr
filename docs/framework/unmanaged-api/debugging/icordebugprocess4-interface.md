---
title: ICorDebugProcess4 인터페이스
ms.date: 02/07/2019
api_name:
- ICorDebugProcess4
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess4
helpviewer_keywords:
- ICorDebugProcess4 interface [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 1bdc958f2516bcd7c2eb74312fbf478e6d49535a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61948808"
---
# <a name="icordebugprocess4-interface"></a>ICorDebugProcess4 인터페이스

프로세스 실행 제어가 부족에 대 한 지원을 제공합니다.

## <a name="methods"></a>메서드

| 메서드                                                                 | 설명                                                                                             |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| [ProcessStateChanged](icordebugprocess4-processstatechanged-method.md) | 디버거 프로세스의 디버기의 실행을 계속 되는 ICorDebug 파이프라인에 알립니다. |

## <a name="remarks"></a>설명

이 인터페이스는 런타임 내에서 있으며 모든 헤더 또는 라이브러리 파일을 통해 노출 되지 않습니다. 그러나 COM 인터페이스에서 파생 되는 것 `IUnknown` GUID를 사용 하 여 `E930C679-78AF-4953-8AB7-B0AABF0F9F80` 일반적인 COM 메커니즘을 통해 얻을 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

**헤더:** 없음

**라이브러리:** 없음

**.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](debugging-interfaces.md)
- [디버깅](index.md)
