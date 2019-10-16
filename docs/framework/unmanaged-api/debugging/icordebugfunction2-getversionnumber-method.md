---
title: ICorDebugFunction2::GetVersionNumber 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugFunction2.GetVersionNumber
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction2::GetVersionNumber
helpviewer_keywords:
- ICorDebugFunction2::GetVersionNumber method [.NET Framework debugging]
- GetVersionNumber method, ICorDebugFunction2 interface [.NET Framework debugging]
ms.assetid: e3a1ce48-9bb9-4ed6-a5fe-5e1819a6333f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 89cf2a12b0a693bbed3e8a3c1134d0f2b2a72a30
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67754457"
---
# <a name="icordebugfunction2getversionnumber-method"></a>ICorDebugFunction2::GetVersionNumber 메서드
이 함수의 편집 하며 계속 하기 버전을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetVersionNumber (  
    [out] ULONG32   *pnVersion  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pnVersion`  
 [out] 이 ICorDebugFunction2 개체로 표현 되는 함수의 버전 번호를 나타내는 정수에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 런타임에서 수행 된 각 모듈에 디버그 세션 중 편집 횟수를 추적 합니다. 함수 버전 번호는 하나의 함수에 적용 된 편집 횟수 초과 합니다. 함수의 원래 버전은 1입니다. 수는 모듈에 대 한 될 때마다 증가 [ICorDebugModule2::ApplyChanges](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule2-applychanges-method.md) 해당 모듈에서 호출 됩니다. 따라서 첫 번째 및 세 번째 호출에서 함수 본문 바뀌었으면 `ICorDebugModule2::ApplyChanges`, `GetVersionNumber` 버전 1, 2 또는 4 해당 함수에 대 한 하지만 하지 버전 3 반환할 수 있습니다. (해당 함수가 없는 버전 3 해야 합니다.)  
  
 버전 번호는 각 모듈에 대해 개별적으로 추적 됩니다. 따라서 모듈 1 모듈 2 없음에 4 개의 편집을 수행한 다음 편집 모듈 1에서 6의 버전 번호를 모듈 1의 모든 편집된 함수에 할당 됩니다. 모듈 2를 편집 하는 동일한 모듈 2의 함수 2의 버전 번호를 받습니다.  
  
 하 여 버전 번호를 가져올는 `GetVersionNumber` 메서드를 여 가져온 보다 작을 수 있습니다 [icordebugfunction:: Getcurrentversionnumber](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction-getcurrentversionnumber-method.md)합니다.  
  
 합니다 [icordebugcode:: Getversionnumber](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getversionnumber-method.md) 와 동일한 작업을 수행 하는 메서드 `ICorDebugFunction2::GetVersionNumber`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
