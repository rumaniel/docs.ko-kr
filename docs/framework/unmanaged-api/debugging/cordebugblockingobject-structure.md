---
title: CorDebugBlockingObject 구조체
ms.date: 03/30/2017
api_name:
- CorDebugBlockingObject Structure
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugBlockingObject
helpviewer_keywords:
- CorDebugBlockingObject structure [.NET Framework debugging]
ms.assetid: 5944edd1-0914-4efa-aba0-d5a277c38b1a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 57de11c1c40c05befcf3c99c31c2e07e1ecaec5a
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71273966"
---
# <a name="cordebugblockingobject-structure"></a>CorDebugBlockingObject 구조체
스레드를 차단 하는 개체와 스레드가 차단 되는 특정 이유를 정의 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
Typedef struct CorDebugBlockingObject  
{  
ICorDebugValue pBlockingObject;  
DWORD dwTimeout;  
CorDebugBlockingReason blockingReason;  
}  CorDebugBlockingObject;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`pBlockingObject`|스레드가 차단 하 고 있는 개체입니다. 이 개체는 현재 동기화 된 상태의 기간 동안만 유효 합니다. 동일 하 게 동기화 된 상태에서 두 스레드가 동일한 개체에서 차단 하는 경우에는 [ICorDebugValue:: GetAddress](icordebugvalue-getaddress-method.md) 메서드가 같은 값을 반환할 것으로 예측할 수 있습니다. 그러나 인터페이스는 포인터가 될 수도 있고 그렇지 않을 수도 있습니다.|  
|`dwTimeout`|차단 작업의 제한 시간이 초과 될 때까지 걸리는 시간 (밀리초) 이거나, 제한 시간이 초과 되지 않음을 나타내는 무한 값입니다. 제한 시간 값은 계속 남아 있는 시간을 제외 하 고 차단 작업의 총 시간 길이를 지정 합니다.|  
|`blockingReason`|이 개체에서 스레드가 차단 된 이유입니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [디버깅 구조체](debugging-structures.md)
- [디버깅](index.md)
