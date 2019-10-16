---
title: ICorDebugThread 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugThread
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread
helpviewer_keywords:
- ICorDebugThread interface [.NET Framework debugging]
ms.assetid: 3930fd9b-2bc3-4b72-80a0-b6eeb94d60c6
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1517d686c50923f5599e33436e0ad6126e8be140
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923151"
---
# <a name="icordebugthread-interface"></a>ICorDebugThread 인터페이스
프로세스의 스레드를 나타냅니다. `ICorDebugThread` 인스턴스의 수명은 이 인스턴스가 나타내는 스레드의 수명과 같습니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[ClearCurrentException 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-clearcurrentexception-method.md)|이 메서드가 구현되지 않았습니다. 이 메서드를 사용하지 마십시오.|  
|[CreateEval 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-createeval-method.md)|이 `ICorDebugThread`에 대해 작동 하는 ICorDebugEval 개체를 만듭니다.|  
|[CreateStepper 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-createstepper-method.md)|이 `ICorDebugThread`에서 활성 프레임을 단계별로 실행할 수 있도록 하는 ICorDebugStepper 개체를 만듭니다.|  
|[EnumerateChains 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-enumeratechains-method.md)|이 `ICorDebugThread`의 모든 스택 체인을 포함 하는 ICorDebugChainEnum 열거자에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetActiveChain 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getactivechain-method.md)|이 `ICorDebugThread`에 대 한 활성 ICorDebugChain 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetActiveFrame 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getactiveframe-method.md)|이 `ICorDebugThread`에 대 한 활성 ICorDebugFrame 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetAppDomain 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getappdomain-method.md)|현재 실행 중인 응용 프로그램 도메인 `ICorDebugThread` 에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetCurrentException 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getcurrentexception-method.md)|관리 코드에서 현재 throw 되는 예외를 나타내는 ICorDebugValue 개체에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetDebugState 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getdebugstate-method.md)|이 `ICorDebugThread`의 현재 디버그 상태를 설명 하는 CorDebugThreadState 값을 가져옵니다.|  
|[GetHandle 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-gethandle-method.md)|이 `ICorDebugThread`의 활성 부분에 대 한 현재 핸들을 가져옵니다.|  
|[GetID 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getid-method.md)|이 `ICorDebugThread`의 활성 부분에 대 한 현재 운영 체제 식별자를 가져옵니다.|  
|[GetObject 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getobject-method.md)|CLR (공용 언어 런타임) 스레드에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetProcess 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getprocess-method.md)|파트를 구성 하는 프로세스 `ICorDebugThread` 에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetRegisterSet 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getregisterset-method.md)|이 `ICorDebugThread`와 연결 된 레지스터 집합에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetUserState 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getuserstate-method.md)|이 `ICorDebugThread`의 현재 상태를 설명 하는 cordebuguserstate 값의 비트 조합을 가져옵니다.|  
|[SetDebugState 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-setdebugstate-method.md)|`CorDebugThreadState` 이`ICorDebugThread`의 디버깅 상태를 설명 하는 값의 비트 조합을 설정 합니다.|  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
