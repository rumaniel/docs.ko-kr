---
title: ICorDebugStepper::Step 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.Step
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::Step
helpviewer_keywords:
- Step method, ICorDebugStepper interface [.NET Framework debugging]
- ICorDebugStepper::Step method [.NET Framework debugging]
ms.assetid: 38c1940b-ada1-40ba-8295-4c0833744e1e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9d0f601c4b454b55edc5fa25eb2ee33d491009b9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67760577"
---
# <a name="icordebugstepperstep-method"></a>ICorDebugStepper::Step 메서드
단일 단계로 포함 스레드를 통해를 필요에 따라이 ICorDebugStepper 하면 한 단계씩 스레드 내에서 호출 된 함수를 계속 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Step (  
    [in] BOOL   bStepIn  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `bStepIn`  
 [in] 로 `true` 스레드 내에서 호출 되는 함수를 한 단계씩 실행 합니다. 로 `false` 함수를 합니다.  
  
## <a name="remarks"></a>설명  
 공용 언어 런타임에서이 스텝 퍼이 프레임에서 다음 관리 되는 명령을 수행 단계 완료 됩니다. 경우 `Step` 는 관리 코드에 없는 스텝에서 호출 되 면, 단계는 다음 관리 되는 코드 명령이 스레드에 의해 실행 될 때 완료 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
