---
title: ICorDebugStepper 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugStepper
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper
helpviewer_keywords:
- ICorDebugStepper interface [.NET Framework debugging]
ms.assetid: ed8364eb-f01b-46f6-b5e3-5dda9cae2dfe
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c57b13b05522614ff066b93cb9f6a437cb340576
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962695"
---
# <a name="icordebugstepper-interface"></a>ICorDebugStepper 인터페이스
디버거에서 수행하는 코드 실행 단계를 나타내며, 명령의 실행/완료를 구분하는 식별자로 사용되고, 단계를 취소하는 방법을 제공합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[Deactivate 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-deactivate-method.md)|이 `ICorDebugStepper` 로 인해 마지막으로 수신한 단계 명령이 취소 됩니다.|  
|[IsActive 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-isactive-method.md)|이 `ICorDebugStepper` 가 현재 단계를 실행 하 고 있는지 여부를 나타내는 값을 가져옵니다.|  
|[SetInterceptMask 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setinterceptmask-method.md)|단계별 코드의 형식을 지정 하는 CorDebugIntercept 값을 설정 합니다.|  
|[SetRangeIL 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setrangeil-method.md)|[ICorDebugStepper:: StepRange](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-steprange-method.md) 에 대 한 호출이 네이티브 코드를 기준으로 인수 값을 전달 하는지 또는 단계별로 진행 중인 메서드의 MSIL (Microsoft 중간 언어) 코드를 기준으로 인수 값을 전달 하는지 여부를 나타내는 값을 설정 합니다.|  
|[SetUnmappedStopMask 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md)|실행이 중단 되는 매핑되지 않은 코드의 형식을 지정 하는 CorDebugUnmappedStop 값을 설정 합니다.|  
|[Step 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-step-method.md)|이 `ICorDebugStepper` 를 통해 포함 하는 스레드를 한 단계씩 실행 하 고 필요에 따라 스레드 내에서 호출 되는 함수를 한 단계씩 실행 합니다.|  
|[StepOut 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-stepout-method.md)|이 `ICorDebugStepper` 를 포함 하는 스레드를 한 단계씩 실행 하 고 현재 프레임에서 제어를 호출 프레임으로 반환할 때 완료 되도록 합니다.|  
|[StepRange 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-steprange-method.md)|이 `ICorDebugStepper` 를 통해 포함 하는 스레드를 한 단계씩 실행 하 고 지정 된 범위를 벗어난 코드에 도달 하면를 반환 합니다.|  
  
## <a name="remarks"></a>설명  
 인터페이스 `ICorDebugStepper` 는 다음과 같은 용도로 사용 됩니다.  
  
- 실행 되는 단계 명령과 해당 명령의 완료 사이에 식별자 역할을 합니다.  
  
- 수행할 수 있는 모든 단계를 캡슐화 하는 중앙 인터페이스를 제공 합니다.  
  
- 단계별 작업을 중간에 취소 하는 방법을 제공 합니다.  
  
 스레드 당 두 개 이상의 스텝 퍼가 있을 수 있습니다. 예를 들어 함수를 프로시저 단위로 실행 하는 동안 중단점이 적중 될 수 있으며 사용자가 해당 함수 내에서 새로운 단계별 작업을 시작할 수 있습니다. 이 상황을 처리 하는 방법을 결정 하는 것은 디버거를 통해 결정 됩니다. 디버거가 원래 단계별 작업을 취소 하거나 두 작업을 중첩할 수 있습니다. 인터페이스 `ICorDebugStepper` 는 두 옵션을 모두 지원 합니다.  
  
 CLR (공용 언어 런타임)이 크로스 스레드 마샬링된 호출을 수행 하는 경우 스텝 퍼는 스레드 간에 마이그레이션할 수 있습니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
