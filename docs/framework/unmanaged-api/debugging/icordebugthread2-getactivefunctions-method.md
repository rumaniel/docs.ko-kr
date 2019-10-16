---
title: ICorDebugThread2::GetActiveFunctions 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.GetActiveFunctions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::GetActiveFunctions
helpviewer_keywords:
- GetActiveFunctions method [.NET Framework debugging]
- ICorDebugThread2::GetActiveFunctions method [.NET Framework debugging]
ms.assetid: 27fae01a-ecec-423a-973e-24f8de55826c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fdf3998d7430348cb71af8e7dd75cf2203d380ce
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769038"
---
# <a name="icordebugthread2getactivefunctions-method"></a>ICorDebugThread2::GetActiveFunctions 메서드
이 스레드의 프레임의 각 활성 함수에 대 한 정보를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetActiveFunctions (  
    [in]   ULONG32             cFunctions,  
    [out]  ULONG32             *pcFunctions,  
    [in, out, size_is(cFunctions), length_is(*pcFunctions)]  
        COR_ACTIVE_FUNCTION    pFunctions[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cFunctions`  
 [in] `pFunctions` 배열의 크기입니다.  
  
 `pcFunctions`  
 [out] 반환 되는 개체의 수에 대 한 포인터를 `pFunctions` 배열입니다. 반환 된 개체의 수는 관리 되는 스택 프레임의 수와 같습니다.  
  
 `pFunctions`  
 [out에서] 이 스레드의 프레임의 현재 함수에 대 한 정보를 포함 하는 각 COR_ACTIVE_FUNCTION 개체의 배열입니다.  
  
 첫 번째 요소의 리프 프레임과 등 백 스택의의 루트에 대해 사용 됩니다.  
  
## <a name="remarks"></a>설명  
 하는 경우 `pFunctions` 가 입력 시 null `GetActiveFunctions` 스택에 있는 함수의 수만 반환 합니다. 즉, 하는 경우 `pFunctions` 가 입력 시 null `GetActiveFunctions` 값을 반환 에서만 `pcFunctions`합니다.  
  
 `GetActiveFunctions` 메서드는 최적화로 스택 추적의 프레임에서 동일한 정보를 가져오는 이며 했습니다 ICorDebugILFrame 개체에는 전체 스택 추적 프레임만 포함 되어 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
