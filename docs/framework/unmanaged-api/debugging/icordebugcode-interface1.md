---
title: ICorDebugCode 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugCode
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode
helpviewer_keywords:
- ICorDebugCode interface [.NET Framework debugging]
ms.assetid: 7bd14fb6-8b54-4484-a891-e3c21859c019
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 75cc8ea9d88dda42362f50b519864b1a78e1a64b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960787"
---
# <a name="icordebugcode-interface"></a>ICorDebugCode 인터페이스

MSIL(Microsoft Intermediate Language) 코드나 네이티브 코드의 세그먼트를 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[CreateBreakpoint 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-createbreakpoint-method.md)|지정 된 오프셋에 중단점을 만듭니다.|  
|[GetAddress 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getaddress-method.md)|이 `ICorDebugCode` 가 나타내는 코드 세그먼트의 RVA (상대 가상 주소)를 가져옵니다.|  
|[GetCode 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getcode-method.md)|지정 된 함수에 대 한 코드를 모두 가져오고 디스어셈블리에 맞게 형식이 지정 됩니다. 이 메서드는 더 이상 사용 되지 않습니다. 대신 [ICorDebugCode2:: GetCodeChunks](../../../../docs/framework/unmanaged-api/debugging/icordebugcode2-getcodechunks-method.md) 를 사용 합니다.|  
|[GetEnCRemapSequencePoints 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getencremapsequencepoints-method.md)|구현되지 않았습니다.|  
|[GetFunction 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getfunction-method.md)|이 `ICorDebugCode`와 연결 된 "ICorDebugFunction"를 가져옵니다.|  
|[GetILToNativeMapping 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getiltonativemapping-method.md)|MSIL 오프셋과 네이티브 오프셋 간의 매핑을 나타내는 "COR_DEBUG_IL_TO_NATIVE_MAP" 인스턴스의 배열을 가져옵니다.|  
|[GetSize 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getsize-method.md)|이 `ICorDebugCode`가 나타내는 이진 코드의 크기 (바이트)를 가져옵니다.|  
|[GetVersionNumber 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getversionnumber-method.md)|이 `ICorDebugCode` 가 나타내는 코드의 버전을 식별 하는 1부터 사용 하는 번호를 가져옵니다.|  
|[IsIL 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-isil-method.md)|이이 `ICorDebugCode` MSIL로 컴파일 되었는지 여부를 나타내는 값을 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 `ICorDebugCode`MSIL 또는 네이티브 코드를 나타낼 수 있습니다. MSIL 코드를 나타내는 "ICorDebugFunction" 개체에는 0 개 또는 하나의 `ICorDebugCode` 개체가 연결 될 수 있습니다. 네이티브 코드를 나타내는 "ICorDebugFunction" 개체에는 연결 된 `ICorDebugCode` 개체가 여러 개 있을 수 있습니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugCode3 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
