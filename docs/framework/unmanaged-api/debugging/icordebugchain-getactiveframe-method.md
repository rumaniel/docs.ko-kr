---
title: ICorDebugChain::GetActiveFrame 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetActiveFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetActiveFrame
helpviewer_keywords:
- ICorDebugChain::GetActiveFrame method [.NET Framework debugging]
- GetActiveFrame method, ICorDebugChain interface [.NET Framework debugging]
ms.assetid: 36887017-670b-4f21-b406-8fab956f84a3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c79f3b3b976b83eb99f8aa26d38a1fe316de471a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67744989"
---
# <a name="icordebugchaingetactiveframe-method"></a>ICorDebugChain::GetActiveFrame 메서드
활성 가져옵니다 (즉, 가장 최근) 체인에서 프레임입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetActiveFrame (  
    [out] ICorDebugFrame   **ppFrame  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppFrame`  
 [out] 활성 나타내는 ICorDebugFrame 개체의 주소에 대 한 포인터 (즉, 가장 최근) 체인에서 프레임입니다.  
  
## <a name="remarks"></a>설명  
 관리 되는 스택 프레임이 없기를 사용할 수 있으면 `ppFrame` 설정 되어 null로 합니다.  
  
 활성 프레임을 사용할 수 없는 경우 호출이 성공 한다는 및 `ppFrame` null이 됩니다. 활성 프레임 CHAIN_CLASS_INIT 인해 시작 하는 일부 체인 및 체인 CHAIN_ENTER_UNMANAGED,으로 인해 시작에 사용할 되지 않습니다. CorDebugChainReason 열거형을 참조 하세요.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
