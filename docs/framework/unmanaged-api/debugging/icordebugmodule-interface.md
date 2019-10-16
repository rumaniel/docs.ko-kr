---
title: ICorDebugModule 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugModule
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule
helpviewer_keywords:
- ICorDebugModule interface [.NET Framework debugging]
ms.assetid: 32e4d6fa-e5a3-413e-9166-d5e2871d3114
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5dce4f5859568c1288610e171286a5919dc8b19b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962425"
---
# <a name="icordebugmodule-interface"></a>ICorDebugModule 인터페이스

실행 파일 또는 DLL (동적 연결 라이브러리) 인 CLR (공용 언어 런타임) 모듈을 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[CreateBreakpoint 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-createbreakpoint-method.md)|구현되지 않았습니다.|  
|[EnableClassLoadCallbacks 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-enableclassloadcallbacks-method.md)|이 모듈에 대해 [ICorDebugManagedCallback:: LoadClass](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-loadclass-method.md) 및 [ICorDebugManagedCallback:: UnloadClass](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-unloadclass-method.md) 콜백이 호출 되었는지 여부를 확인 합니다.|  
|[EnableJITDebugging 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-enablejitdebugging-method.md)|JIT (just-in-time) 컴파일러에서이 모듈의 메서드에 대 한 디버깅 정보를 유지할지 여부를 결정 합니다.|  
|[GetAssembly 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getassembly-method.md)|이 모듈에 대 한 포함 어셈블리를 가져옵니다.|  
|[GetBaseAddress 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getbaseaddress-method.md)|모듈의 기본 주소를 가져옵니다.|  
|[GetClassFromToken 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getclassfromtoken-method.md)|메타 데이터에서 ICorDebugClass을 가져옵니다.|  
|[GetEditAndContinueSnapshot 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-geteditandcontinuesnapshot-method.md)|더 이상 사용되지 않습니다.|  
|[GetFunctionFromRVA 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getfunctionfromrva-method.md)|구현되지 않았습니다.|  
|[GetFunctionFromToken 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getfunctionfromtoken-method.md)|메타 데이터 토큰에 의해 지정 된 함수를 가져옵니다.|  
|[GetGlobalVariableValue 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getglobalvariablevalue-method.md)|지정 된 전역 변수에 대 한 값 개체를 가져옵니다.|  
|[GetMetaDataInterface 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getmetadatainterface-method.md)|모듈에 대 한 메타 데이터를 검사 하는 데 사용할 수 있는 메타 데이터 인터페이스 포인터를 가져옵니다.|  
|[GetName 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getname-method.md)|모듈의 파일 이름을 가져옵니다.|  
|[GetProcess 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getprocess-method.md)|이 모듈에 대 한 프로세스를 포함 하는을 가져옵니다.|  
|[GetSize 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-getsize-method.md)|모듈의 크기 (바이트)를 가져옵니다.|  
|[GetToken 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-gettoken-method.md)|이 모듈의 테이블 항목에 대 한 토큰을 가져옵니다.|  
|[IsDynamic 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-isdynamic-method.md)|모듈이 동적 인지 여부를 나타냅니다.|  
|[IsInMemory 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmodule-isinmemory-method.md)|이 모듈이 메모리에만 있는지 여부를 나타냅니다.|  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebug 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
