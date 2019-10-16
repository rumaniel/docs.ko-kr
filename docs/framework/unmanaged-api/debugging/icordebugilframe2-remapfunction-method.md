---
title: ICorDebugILFrame2::RemapFunction 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame2.RemapFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame2::RemapFunction
helpviewer_keywords:
- ICorDebugILFrame2::RemapFunction method [.NET Framework debugging]
- RemapFunction method [.NET Framework debugging]
ms.assetid: dd639ba0-f77b-426d-9ff6-f92706840348
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 75004f646c01897ef3e3016b073220ad33a0d925
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967573"
---
# <a name="icordebugilframe2remapfunction-method"></a>ICorDebugILFrame2::RemapFunction 메서드
새 MSIL (Microsoft 중간 언어) 오프셋을 지정 하 여 편집 된 함수를 다시 매핑합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT RemapFunction (  
    [in] ULONG32      newILOffset  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `newILOffset`  
 진행 명령 포인터가 배치 되어야 하는 스택 프레임의 새 MSIL 오프셋입니다. 이 값은 시퀀스 위치 여야 합니다.  
  
 이 값의 유효성을 확인 하는 것은 호출자의 책임입니다. 예를 들어 MSIL 오프셋은 함수 범위 밖에 있을 경우 유효 하지 않습니다.  
  
## <a name="remarks"></a>설명  
 프레임의 함수가 편집 된 경우 디버거는 메서드를 `RemapFunction` 호출 하 여 최신 버전의 프레임 함수를 교환 하 여 실행할 수 있습니다. 지정 된 MSIL 오프셋에서 코드 실행이 시작 됩니다.  
  
> [!NOTE]
> `RemapFunction` [ICorDebugILFrame:: SetIP](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe-setip-method.md)호출과 같이를 호출 하면 스레드의 스택 추적 생성과 관련 된 모든 디버깅 인터페이스가 즉시 무효화 됩니다. 이러한 인터페이스에는 [ICorDebugChain](../../../../docs/framework/unmanaged-api/debugging/icordebugchain-interface.md), ICorDebugILFrame, ICorDebugInternalFrame 및 ICorDebugNativeFrame가 포함 됩니다.  
  
 메서드 `RemapFunction` 는 현재 프레임의 컨텍스트에서만 호출할 수 있으며, 다음 중 한 가지 경우에만 호출할 수 있습니다.  
  
- [ICorDebugManagedCallback2:: FunctionRemapOpportunity](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-functionremapopportunity-method.md) 콜백이 아직 지속 되지 않은 것을 확인 한 후  
  
- 이 프레임에 대 한 [ICorDebugManagedCallback:: EditAndContinueRemap](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-editandcontinueremap-method.md) 이벤트로 인해 코드 실행이 중지 되었습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
