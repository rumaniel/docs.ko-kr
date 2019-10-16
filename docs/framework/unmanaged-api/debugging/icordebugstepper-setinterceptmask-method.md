---
title: ICorDebugStepper::SetInterceptMask 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.SetInterceptMask
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::SetInterceptMask
helpviewer_keywords:
- SetInterceptMask method [.NET Framework debugging]
- ICorDebugStepper::SetInterceptMask method [.NET Framework debugging]
ms.assetid: 6245e2ae-5cc2-43ff-8cc1-71953d12113a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 37b644227a6085352bed682f0ddd7c3455b54895
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67760696"
---
# <a name="icordebugsteppersetinterceptmask-method"></a>ICorDebugStepper::SetInterceptMask 메서드
한 단계씩 코드 형식을 지정 하는 값을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetInterceptMask (  
    [in] CorDebugIntercept    mask  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `mask`  
 [in] 코드의 형식을 지정 하는 CorDebugIntercept 열거형 값의 조합입니다.  
  
## <a name="remarks"></a>설명  
 인터셉터에 대 한 비트가 설정 된 경우 스텝 퍼는 코드를 차단 하는 지정 된 형식이 발견 될 때 완료 됩니다. 비트가 지워지면 가로채 코드를 건너뜁니다.  
  
 합니다 `SetInterceptMask` 메서드에 있을 수 있습니다 사용 하 여 예측할 수 없는 상호 작용 [icordebugstepper:: Setunmappedstopmask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md) (사용자의 관점에서). 예를 들어 경우만 표시 됨 (즉, 비-내부) 클래스 초기화 코드의 부분 매핑 정보가 없으며 STOP_NO_MAPPING_INFO 설정 되어 있지 않습니다 (참조를 [icordebugstepper:: Setunmappedstopmask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md) 메서드 및 CorDebugUnmappedStop 열거형) 스텝 퍼 클래스 초기화 건너뛰기 됩니다. 기본적으로 INTERCEPT_NONE 값만을 `CorDebugIntercept` 열거 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
