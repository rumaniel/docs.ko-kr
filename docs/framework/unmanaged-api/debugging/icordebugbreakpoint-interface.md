---
title: ICorDebugBreakpoint 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBreakpoint
helpviewer_keywords:
- ICorDebugBreakpoint interface [.NET Framework debugging]
ms.assetid: aa5ad3d7-e1bb-42af-99bc-471224e3bcaa
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 608c2cea79c20a43d65fcbf37ba13242fa465100
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969319"
---
# <a name="icordebugbreakpoint-interface"></a>ICorDebugBreakpoint 인터페이스

함수의 중단점 또는 값에 대 한 조사식을 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[Activate 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugbreakpoint-activate-method.md)|이 `ICorDebugBreakpoint`의 활성 상태를 설정 합니다.|  
|[IsActive 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugbreakpoint-isactive-method.md)|이 `ICorDebugBreakpoint` 가 활성 상태 인지 여부를 나타내는 값을 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 중단점은 조건식을 직접 지원 하지 않습니다. 이러한 기능이 필요한 경우 디버거는 위에서 `ICorDebugBreakpoint`이 기능을 구현 해야 합니다.  
  
 ICorDebugFunctionBreakpoint 인터페이스는 함수 `ICorDebugBreakpoint` 내에서 중단점을 지원 하도록 확장 됩니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
