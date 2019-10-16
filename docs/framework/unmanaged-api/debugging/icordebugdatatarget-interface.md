---
title: ICorDebugDataTarget 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget
helpviewer_keywords:
- ICorDebugDataTarget interface [.NET Framework debugging]
ms.assetid: df5f05be-bed7-4f3c-bc89-dbb435d79a0b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0c6a8ee1bcc65e640ef871e57acdeef21acd7896
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930831"
---
# <a name="icordebugdatatarget-interface"></a>ICorDebugDataTarget 인터페이스
특정 대상 프로세스에 대한 액세스를 제공하는 콜백 인터페이스를 제공합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetPlatform 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getplatform-method.md)|대상 프로세스가 실행 되는 프로세서 아키텍처 및 운영 체제를 포함 하 여 플랫폼에 대 한 정보를 제공 합니다.|  
|[ReadVirtual 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-readvirtual-method.md)|지정 된 주소에서 시작 하는 연속 메모리 블록을 가져와 제공 된 버퍼에 반환 합니다.|  
|[GetThreadContext 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getthreadcontext-method.md)|지정 된 스레드에 대 한 현재 스레드 컨텍스트를 요청 합니다.|  
  
## <a name="remarks"></a>설명  
 `ICorDebugDataTarget`및 해당 메서드의 특성은 다음과 같습니다.  
  
- 디버깅 서비스는이 인터페이스의 메서드를 호출 하 여 대상 프로세스의 메모리 및 기타 데이터에 액세스 합니다.  
  
- 디버거 클라이언트는 특정 대상에 적합 하 게이 인터페이스를 구현 해야 합니다 (예: 라이브 프로세스 또는 메모리 덤프).  
  
- 메서드 `ICorDebugDataTarget` 는 다른 `ICorDebug*` 인터페이스에 구현 된 메서드 내 에서만 호출할 수 있습니다. 이렇게 하면 디버거 클라이언트에서 호출 되는 스레드 및 시기를 제어할 수 있습니다.  
  
- `ICorDebugDataTarget` 구현은 항상 대상에 대 한 최신 정보를 반환 해야 합니다.  
  
 인터페이스 ( `ICorDebug*` `ICorDebugDataTarget` 및 메서드)를 호출 하는 동안에는 대상 프로세스를 중지 하 고 변경 하지 않아야 합니다. 대상이 라이브 프로세스이 고 상태가 변경 되 면 [ICLRDebugging:: OpenVirtualProcess](../../../../docs/framework/unmanaged-api/debugging/iclrdebugging-openvirtualprocess-method.md) 메서드를 다시 호출 하 여 대체 ICorDebugProcess 인스턴스를 제공 해야 합니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
