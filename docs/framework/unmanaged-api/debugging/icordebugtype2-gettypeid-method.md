---
title: ICorDebugType2::GetTypeID 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugType2.GetTypeID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetTypeID
helpviewer_keywords:
- GetTypeID method, ICorDebugType2 interface [.NET Framework debugging]
- ICorDebugType2.GetTypeID method [.NET Framework debugging]
ms.assetid: 0b933686-226e-4373-92b7-fac579ee7b1a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3098911bab2878876b93ee1ce23d9794d7e6cdbd
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67772462"
---
# <a name="icordebugtype2gettypeid-method"></a>ICorDebugType2::GetTypeID 메서드
가져옵니다를 [COR_TYPEID](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md) 이 형식에 대 한 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetTypeID(  
    ([out] COR_TYPEID *id  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `id`  
 [out] 에 대 한 포인터를 [COR_TYPEID](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md) 이 icordebugtype 합니다.  
  
## <a name="return-value"></a>반환 값  
 반환 값은 성공 시 `S_OK`이고 실패 시에는 오류 `HRESULT` 코드입니다. `HRESULT` 코드는 다음과 같습니다.  
  
|반환 코드|설명|  
|-----------------|-----------------|  
|`S_OK`|메서드가 정상적으로 실행되었습니다. 메서드는 유효한 검색 했음을 [COR_TYPEID](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md)합니다.|  
|`CORDBG_E_CLASS_NOT_LOADED`|형식 로드 되지 않았습니다.|  
|`CORDBG_E_UNSUPPORTED`|형식이 지원 되지 않습니다.|  
  
## <a name="remarks"></a>설명  
 이 메서드는 ICorDebugType 수도 있습니다 하지에 로드 된 런타임을 있는 형식을 나타내는에서 매핑을 제공 된 [COR_TYPEID](../../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md), 런타임에 로드 형식을 식별 하는 불투명 역할 처리 합니다.  
  
 ICorDebugType 나타내는 형식이 아직이 메서드는 반환 된 로드 경우 `CORDBG_E_CLASS_NOT_LOADED`합니다.  반환 형식이 지원 되지 않는 경우 `CORDBG_E_UNSUPPORTED`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugType2 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugtype2-interface.md)
