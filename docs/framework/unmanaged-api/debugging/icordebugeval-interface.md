---
title: ICorDebugEval 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugEval
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval
helpviewer_keywords:
- ICorDebugEval interface [.NET Framework debugging]
ms.assetid: 3a5c9815-832d-47e1-b7f7-bbba135d7cf1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cfd29067f819ba69305f7ae8620729cd443915a0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931943"
---
# <a name="icordebugeval-interface"></a>ICorDebugEval 인터페이스

디버깅 중인 코드의 컨텍스트 내에서 디버거가 코드를 실행할 수 있도록 하는 메서드를 제공합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[Abort 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-abort-method.md)|이 `ICorDebugEval` 개체가 현재 수행 하 고 있는 계산을 중단 합니다.|  
|[CallFunction 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-callfunction-method.md)|지정 된 함수에 대 한 호출을 설정 합니다. .NET Framework 버전 2.0에서 사용 되지 않습니다. 대신 [ICorDebugEval2:: CallParameterizedFunction](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-callparameterizedfunction-method.md) 을 사용 합니다.|  
|[CreateValue 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-createvalue-method.md)|초기 값이 0 또는 null 인 지정 된 형식의 "ICorDebugValue" 개체에 대 한 인터페이스 포인터를 가져옵니다. .NET Framework 2.0에서 사용 되지 않습니다. 대신 [ICorDebugEval2:: CreateValueForType](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-createvaluefortype-method.md) 을 사용 하십시오.|  
|[GetResult 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-getresult-method.md)|계산 결과를 포함 `ICorDebugValue` 하는에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetThread 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-getthread-method.md)|이 평가가 실행 되거나 실행 되는 "ICorDebugThread"에 대 한 인터페이스 포인터를 가져옵니다.|  
|[IsActive 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-isactive-method.md)|이 `ICorDebugEval` 개체가 현재 실행 중인지 여부를 나타내는 값을 가져옵니다.|  
|[NewArray 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-newarray-method.md)|지정 된 요소 형식 및 차원의 새 배열을 할당 합니다. .NET Framework 2.0에서 사용 되지 않습니다. 대신 [ICorDebugEval2:: NewParameterizedArray](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedarray-method.md) 를 사용 하십시오.|  
|[NewObject 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-newobject-method.md)|새 개체 인스턴스를 할당 하 고 지정 된 생성자 메서드를 호출 합니다. .NET Framework 2.0에서 사용 되지 않습니다. 대신 [ICorDebugEval2:: NewParameterizedObject](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedobject-method.md) 를 사용 합니다.|  
|[NewObjectNoConstructor 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-newobjectnoconstructor-method.md)|생성자 메서드 호출을 시도 하지 않고 지정 된 형식의 새 개체 인스턴스를 할당 합니다. .NET Framework 2.0에서 사용 되지 않습니다. 대신 [ICorDebugEval2:: NewParameterizedObjectNoConstructor](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedobjectnoconstructor-method.md) 를 사용 합니다.|  
|[NewString 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-newstring-method.md)|지정 된 내용을 사용 하 여 새 문자열 개체를 할당 합니다.|  
  
## <a name="remarks"></a>설명  
 개체 `ICorDebugEval` 는 평가를 수행 하는 데 사용 되는 특정 스레드의 컨텍스트에서 만들어집니다. 지정 된 평가에 사용 되는 모든 개체와 유형은 동일한 응용 프로그램 도메인 내에 있어야 합니다. 해당 응용 프로그램 도메인은 스레드의 현재 응용 프로그램 도메인과 같을 필요가 없습니다. 평가는 중첩 될 수 있습니다.  
  
 디버거에서 [ICorDebugController:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md)를 호출 하 고 [ICorDebugManagedCallback:: EvalComplete](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-evalcomplete-method.md) callback을 받을 때까지 평가 작업이 완료 되지 않습니다. 다른 스레드를 실행 하도록 허용 하지 않고 평가 기능을 사용 해야 하는 경우 [ICorDebugController:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md)를 호출하기 전에 [ICorDebugController:: SetAllThreadsDebugState](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-setallthreadsdebugstate-method.md) 또는 [ICorDebugController:: Stop](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-stop-method.md)을 사용하여 스레드를 일시 중단합니다.  
  
 평가가 진행 중일 때 사용자 코드가 실행 되기 때문에 클래스 로드 및 중단점을 포함 하 여 모든 디버그 이벤트가 발생할 수 있습니다. 디버거에서는 이러한 이벤트에 대 한 콜백을 정상적으로 수신 합니다. 평가 상태는 일반적인 프로그램 상태 검사의 일부로 표시 됩니다. 스택 체인 `CHAIN_FUNC_EVAL` 은 체인이 됩니다 ("CorDebugStepReason" 열거 및 [ICorDebugChain:: getreason](../../../../docs/framework/unmanaged-api/debugging/icordebugchain-getreason-method.md) 메서드 참조). 전체 디버거 API는 정상적으로 계속 작동 합니다.  
  
 교착 상태 또는 무한 반복 상황이 발생 하면 사용자 코드가 완료 되지 않을 수 있습니다. 이러한 경우 프로그램을 다시 시작 하기 전에 [ICorDebugEval:: Abort](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-abort-method.md) 를 호출 해야 합니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
