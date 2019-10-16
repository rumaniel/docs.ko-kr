---
title: ICorDebugStepper::StepRange 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.StepRange
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::StepRange
helpviewer_keywords:
- StepRange method [.NET Framework debugging]
- ICorDebugStepper::StepRange method [.NET Framework debugging]
ms.assetid: b9776112-6e6d-4708-892a-8873db02e16f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7e1ace501bf5de741ea110fe4d3bb4bc44843bf8
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67760530"
---
# <a name="icordebugsteppersteprange-method"></a>ICorDebugStepper::StepRange 메서드
이 ICorDebugStepper 단일 단계로 포함 스레드를 통해 반환 하는 마지막 지정 된 범위를 벗어난 코드에 도달 하면 발생 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT StepRange (  
    [in] BOOL     bStepIn,  
    [in, size_is(cRangeCount)] COR_DEBUG_STEP_RANGE ranges[],  
    [in] ULONG32  cRangeCount  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `bStepIn`  
 [in] 로 `true` 스레드 내에서 호출 되는 함수를 한 단계씩 실행 합니다. 로 `false` 함수를 합니다.  
  
 `ranges`  
 [in] 범위를 지정 하는 각 COR_DEBUG_STEP_RANGE 구조체의 배열입니다.  
  
 `cRangeCount`  
 [in] `ranges` 배열의 크기입니다.  
  
## <a name="remarks"></a>설명  
 `StepRange` 메서드처럼 작동 합니다 [icordebugstepper:: Step](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-step-method.md) 메서드를 제외 하 고 지정 된 범위를 벗어난 코드까지 완료 되지 않으면에 도달 합니다.  
  
 이 한 번에 하나의 명령을 단계별로 실행 하는 보다 더 효율적일 수 있습니다. 스텝 퍼의 프레임의 시작 부분에서 오프셋된 쌍의 목록으로 범위가 지정 됩니다.  
  
 범위는 메서드의 Microsoft MSIL (intermediate language) 코드 기준입니다. 호출 [icordebugstepper:: Setrangeil](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setrangeil-method.md) 사용 하 여 `false` 메서드의 네이티브 코드를 기준으로 범위를 확인 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
