---
title: ICorDebugStepper::StepOut 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.StepOut
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::StepOut
helpviewer_keywords:
- ICorDebugStepper::StepOut method [.NET Framework debugging]
- StepOut method [.NET Framework debugging]
ms.assetid: aae0f48c-4ede-4256-9251-a7fc85a229dc
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 36a33b74a692761d772a888ce918aa28a2d92678
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67760561"
---
# <a name="icordebugstepperstepout-method"></a>ICorDebugStepper::StepOut 메서드
현재 프레임 호출 프레임으로 컨트롤을 반환 하는 경우 완료 하 고 포함 스레드를 통해 단일 단계로이 ICorDebugStepper 발생 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT StepOut ();  
```  
  
## <a name="remarks"></a>설명  
 `StepOut` 호출 프레임에 현재 프레임에서 정상적으로 반환 된 후 작업이 완료 됩니다.  
  
 경우 `StepOut` 때 호출 된 경우 비관리 코드에서 호출 하는 관리 코드의 현재 프레임을 반환 하는 경우 단계 완료 됩니다.  
  
 .NET framework 버전 2.0에서 사용 하지 마십시오 `StepOut` 실패 하기 때문에 플래그가 설정 된 STOP_UNMANAGED를 사용 하 여 합니다. (사용 하 여 [icordebugstepper:: Setunmappedstopmask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md) 단계별 실행에 대 한 플래그를 설정 합니다.) Interop 디버거 나가야 합니다 네이티브 코드 자체입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
