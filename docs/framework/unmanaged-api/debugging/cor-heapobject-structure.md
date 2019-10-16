---
title: COR_HEAPOBJECT 구조체
ms.date: 03/30/2017
api_name:
- COR_HEAPOBJECT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_HEAPOBJECT
helpviewer_keywords:
- COR_HEAPOBJECT structure [.NET Framework debugging]
ms.assetid: a92fdf95-492b-49ae-a741-2186e5c1d7c5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c59ddec655f3127e8dab8d8c41543f03a896cf63
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274029"
---
# <a name="cor_heapobject-structure"></a>COR_HEAPOBJECT 구조체
관리되는 힙의 개체에 대한 정보를 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct _COR_HEAPOBJECT {  
    CORDB_ADDRESS address;    
    ULONG64 size;             
    COR_TYPEID type;          
} COR_HEAPOBJECT;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`address`|메모리에 있는 개체의 주소입니다.|  
|`size`|개체의 총 크기 (바이트)입니다.|  
|`type`|개체의 유형을 나타내는 [COR_TYPEID](cor-typeid-structure.md) 토큰입니다.|  
  
## <a name="remarks"></a>설명  
 `COR_HEAPOBJECT`[ICorDebugProcess5:: EnumerateHeap](icordebugprocess5-enumerateheap-method.md) 메서드를 호출 하 여 채워지는 [ICorDebugHeapEnum](icordebugheapenum-interface.md) interface 개체를 열거 하 여 인스턴스를 검색할 수 있습니다.  
  
 인스턴스 `COR_HEAPOBJECT` 는 관리 되는 힙에서 라이브 개체에 대 한 정보를 제공 하 고, 개체가 루 팅 되지 않았지만 가비지 수집기에서 아직 수집 되지 않은 개체에 대 한 정보를 제공 합니다.  
  
 성능 향상을 `COR_HEAPOBJECT.address` 위해 대부분의 디버깅 API `CORDB_ADDRESS` 에서 사용 되는 ICorDebugValue 인터페이스 값이 아닌 값이 필드입니다. 지정 된 개체 주소에 대 한 ICorDebugValue 개체를 가져오려면 `CORDB_ADDRESS` [ICorDebugProcess5:: GetObject](icordebugprocess5-getobject-method.md) 메서드에 값을 전달 하면 됩니다.  
  
 성능 향상을 `COR_HEAPOBJECT.type` 위해 대부분의 디버깅 API `COR_TYPEID` 에서 사용 되는 ICorDebugType 인터페이스 값이 아닌 값이 필드입니다. 지정 된 형식 ID에 대 한 ICorDebugType 개체를 가져오려면 `COR_TYPEID` [ICorDebugProcess5:: gettypefortypeid](icordebugprocess5-gettypefortypeid-method.md) 메서드에 값을 전달 하면 됩니다.  
  
 구조체 `COR_HEAPOBJECT` 에는 참조 횟수가 계산 되는 COM 인터페이스가 포함 되어 있습니다. `COR_HEAPOBJECT` [ICorDebugHeapEnum:: Next](icordebugheapenum-next-method.md) 메서드를 호출 하 여 열거자에서 인스턴스를 검색 하는 경우 나중에 참조를 해제 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [디버깅 구조체](debugging-structures.md)
- [디버깅](index.md)
