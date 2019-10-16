---
title: ICorDebugCode::GetILToNativeMapping 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetILToNativeMapping
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetILToNativeMapping
helpviewer_keywords:
- GetILToNativeMapping method, ICorDebugCode interface [.NET Framework debugging]
- ICorDebugCode::GetILToNativeMapping method [.NET Framework debugging]
ms.assetid: a8ecd8c8-9627-4356-9c6f-bd05e24637c0
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7c9e2bb9ef97326c3d11553b6cabd0de0fd6e495
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747511"
---
# <a name="icordebugcodegetiltonativemapping-method"></a>ICorDebugCode::GetILToNativeMapping 메서드
Microsoft MSIL (intermediate language) 오프셋과 네이티브 오프셋 간의 매핑을 나타내는 "COR_DEBUG_IL_TO_NATIVE_MAP" 인스턴스의 배열을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetILToNativeMapping (  
    [in]  ULONG32    cMap,  
    [out] ULONG32    *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cMap`  
 [in] `map` 배열의 크기입니다.  
  
 `pcMap`  
 [out] 반환 되는 요소의 실제 수에 대 한 포인터를 `map` 배열입니다.  
  
 `map`  
 [out] 배열을 `COR_DEBUG_IL_TO_NATIVE_MAP` 각각 MSIL 오프셋에서 네이티브 오프셋에 대 한 매핑을 나타내는 구조입니다.  
  
 반환 되는 요소의 배열에 순서가 있지 않습니다.  
  
## <a name="remarks"></a>설명  
 `GetILToNativeMapping` 메서드가이 "ICorDebugCode" 인스턴스에 just-in-time (JIT) MSIL 코드에서 컴파일된 네이티브 코드를 나타내는 경우에 의미 있는 결과 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugCode 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-interface1.md)
