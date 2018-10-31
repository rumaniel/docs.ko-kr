---
title: ICorDebugBlockingObjectEnum::Next 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugBlockingObjectEnum.Next Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBlockingObjectEnum::Next
helpviewer_keywords:
- Next method, ICorDebugBlockingObjectEnum interface [.NET Framework debugging]
- ICorDebugBlockingObjectEnum::Next method [.NET Framework debugging]
ms.assetid: 0121753f-ebea-48d0-aeb2-ed7fda76dc60
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 04b28dec0f016d44692665fb0ce95a7e496f103c
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200524"
---
# <a name="icordebugblockingobjectenumnext-method"></a>ICorDebugBlockingObjectEnum::Next 메서드
지정 된 개수를 가져옵니다 [CorDebugBlockingObject](../../../../docs/framework/unmanaged-api/debugging/cordebugblockingobject-structure.md) 개체를 열거형에서 현재 위치에서 시작 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT Next([in] ULONG  celt,  
             [out, size_is(celt), length_is(*pceltFetched)]  
                           CorDebugBlockingObject values[],  
             [out] ULONG *pceltFetched;  
```  
  
#### <a name="parameters"></a>매개 변수  
 `celt`  
 [in] 검색할 개체의 수입니다.  
  
 `values`  
 [out] 에 대 한 포인터의 배열을 [CorDebugBlockingObject](../../../../docs/framework/unmanaged-api/debugging/cordebugblockingobject-structure.md) 개체입니다.  
  
 `pceltFetched`  
 [out] 검색 된 개체의 수에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT를 반환합니다.  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|S_FALSE|`pceltFetched`이 `celt`와 다릅니다.|  
  
## <a name="remarks"></a>설명  
 이 메서드가 함수는 일반적인 COM 열거자를 선호합니다.  
  
 입력된 배열 값 이상 이어야 합니다 크기인 `celt`합니다. 배열 채워집니다 중 하나를 사용 하 여 다음 `celt` 값을 열거형에 남아 있는 모든 값 보다 적으면 `celt` 유지 합니다. 이 메서드는 반환 될 때 `pceltFetched` 검색 된 값의 수로 채워집니다. 경우 `values` 잘못 된 포인터를 포함 하거나 보다 작은 버퍼를 가리키는 `celt`, 또는 경우 `pceltFetched` 는 잘못 된 포인터는 결과가 정의 되지 않습니다.  
  
> [!NOTE]
>  하지만 [CorDebugBlockingObject](../../../../docs/framework/unmanaged-api/debugging/cordebugblockingobject-structure.md) 구조를 해제할 필요가 없습니다, 내부 "ICorDebugValue" 인터페이스는 해제 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [ICorDebugDataTarget 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-interface.md)  
 [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
