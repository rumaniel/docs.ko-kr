---
title: ICorDebugFunction2::SetJMCStatus 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugFunction2.SetJMCStatus
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction2::SetJMCStatus
helpviewer_keywords:
- ICorDebugFunction2::SetJMCStatus method [.NET Framework debugging]
- SetJMCStatus method, ICorDebugFunction2 interface [.NET Framework debugging]
ms.assetid: 22c27b01-2869-4214-b840-5921f7c874fc
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 67959b2ebbfb62b47a1b2a770e278d043fc66d21
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67754921"
---
# <a name="icordebugfunction2setjmcstatus-method"></a>ICorDebugFunction2::SetJMCStatus 메서드
Just My Code에 대 한이 ICorDebugFunction2 함수가 표시 단계별로 실행 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetJMCStatus (  
    [in] BOOL   bIsJustMyCode  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `bIsJustMyCode`  
 [in] 로 `true` 사용자 코드로; 함수를 표시 하려면이 고, 그렇지로 `false`.  
  
## <a name="return-values"></a>반환 값  
  
|HRESULT|설명|  
|-------------|-----------------|  
|`S_OK`|함수를 표시 했습니다.|  
|`CORDBG_E_FUNCTION_NOT_DEBUGGABLE`|디버깅할 수 없습니다 때문에 사용자 코드로 함수를 표시할 수 없습니다.|  
  
## <a name="remarks"></a>설명  
 내 코드만 스텝 사용자 코드가 아닌 건너뜁니다. 사용자 코드에 디버깅 가능한 코드가의 하위 집합 이어야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
