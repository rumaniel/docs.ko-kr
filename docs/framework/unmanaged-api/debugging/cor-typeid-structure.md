---
title: COR_TYPEID 구조체
ms.date: 03/30/2017
api_name:
- COR_TYPEID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_TYPEID
helpviewer_keywords:
- COR_TYPEID structure [.NET Framework debugging]
ms.assetid: 1e172b14-ee22-4943-b3b8-3740e7bdcd2e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5d76fa4b2352da18b5ef0e547ebc4e2e99d980b8
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71273991"
---
# <a name="cor_typeid-structure"></a>COR_TYPEID 구조체
유형 식별자를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct COR_TYPEID{  
    UINT64 token1;  
    UINT64 token2;  
} COR_TYPEID;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`token1`|첫 번째 토큰입니다.|  
|`token2`|두 번째 토큰입니다.|  
  
## <a name="remarks"></a>설명  
 구조체 `COR_TYPEID` 는 가비지 수집 될 개체에 대 한 정보를 제공 하는 다양 한 디버깅 메서드에서 반환 됩니다. 그런 다음 해당 항목에 대 한 추가 정보를 제공 하는 다른 디버깅 메서드에 인수로 전달 될 수 있습니다. 예를 들어, [ICorDebugHeapEnum](icordebugheapenum-interface.md) 개체를 열거 하 여 관리 되는 힙에서 개별 개체를 나타내는 개별 [COR_HEAPOBJECT](cor-heapobject-structure.md) 개체를 검색할 수 있습니다. 그런 다음 `COR_TYPEID` `COR_HEAPOBJECT.type` 필드의 값을 [ICorDebugProcess5:: gettypefortypeid](icordebugprocess5-gettypefortypeid-method.md) 메서드로 전달 하 여 개체에 대 한 형식 정보를 제공 하는 ICorDebugType 개체를 검색할 수 있습니다.  
  
 개체 `COR_TYPEID` 는 불투명 하기 위한 것입니다. 개별 필드에 액세스 하거나 조작할 수 없습니다. 유일한 용도는 메서드 호출에서 `out` 매개 변수로 제공 되는 식별자로 서, 추가 정보를 제공 하기 위해 다른 메서드에 전달할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [디버깅 구조체](debugging-structures.md)
- [디버깅](index.md)
