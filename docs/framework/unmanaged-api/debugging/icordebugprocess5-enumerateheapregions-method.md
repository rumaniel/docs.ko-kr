---
title: ICorDebugProcess5::EnumerateHeapRegions 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHeapRegions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHeapRegions
helpviewer_keywords:
- EnumerateHeapRegions method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHeapRegions method [.NET Framework debugging]
ms.assetid: b1edba68-9c36-4f69-be9f-678ce0b33480
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cf9340977c55c54b9a4683115000293d1c98dfcf
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67767466"
---
# <a name="icordebugprocess5enumerateheapregions-method"></a>ICorDebugProcess5::EnumerateHeapRegions 메서드
관리 되는 힙의 메모리 범위에 대 한 열거자를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnumerateHeapRegions(  
   [out] ICorDebugHeapSegmentEnum **ppRegions  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppRegions`  
 [out] 주소에 대 한 포인터를 [ICorDebugHeapSegmentEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapsegmentenum-interface.md) 인터페이스 개체는 개체에 관리 되는 힙 메모리의 범위에 대 한 열거자입니다.  
  
## <a name="remarks"></a>설명  
 호출 하기 전에 합니다 `ICorDebugProcess5::EnumerateHeapRegions` 호출 해야 합니다는 [ICorDebugProcess5::GetGCHeapInformation](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-getgcheapinformation-method.md) 메서드의 값을 검사 합니다 `areGCStructuresValid` 반환 된 필드 [COR_HEAPINFO](../../../../docs/framework/unmanaged-api/debugging/cor-heapinfo-structure.md) 가비지 수집 힙의 현재 상태에서 열거 가능한 지 확인 하는 개체입니다. 또한 합니다 `ICorDebugProcess5::EnumerateHeapRegions` 메서드가 반환 되는 `E_FAIL` 너무 일찍 프로세스의 수명에에서 연결 하는 경우 메모리 전에 지역 만들어집니다.  
  
 이 메서드는 항상 관리 되는 개체를 포함할 수 있는 모든 메모리 영역을 열거 하지만 해당 지역에서 관리 되는 개체 실제로 있는 보장 하지 않습니다. 합니다 [ICorDebugHeapSegmentEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapsegmentenum-interface.md) 컬렉션 개체는 비어 있거나 예약 된 메모리 영역을 포함 될 수 있습니다.  
  
 합니다 [ICorDebugHeapSegmentEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapsegmentenum-interface.md) 인터페이스 개체는 열거할 수 있도록 ICorDebugEnum 인터페이스에서 파생 하는 표준 열거자 [COR_SEGMENT](../../../../docs/framework/unmanaged-api/debugging/cor-segment-structure.md) 개체입니다. 각 [COR_SEGMENT](../../../../docs/framework/unmanaged-api/debugging/cor-segment-structure.md) 개체의 해당 세그먼트에서 개체의 세대와 함께 특정 세그먼트를 하는 메모리 범위에 대 한 정보를 제공 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugProcess5 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
