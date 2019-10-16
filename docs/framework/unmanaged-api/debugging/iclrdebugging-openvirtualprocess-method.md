---
title: ICLRDebugging::OpenVirtualProcess 메서드
ms.date: 03/30/2017
api_name:
- ICLRDebugging.OpenVirtualProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDebugging::OpenVirtualProcess
helpviewer_keywords:
- OpenVirtualProcess method [.NET Framework debugging]
- ICLRDebugging::OpenVirtualProcess method [.NET Framework debugging]
ms.assetid: e8ab7c41-d508-4ed9-8a31-ead072b5a314
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4c460bc644017f32fdb96d35e5f42981ac09f825
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67738375"
---
# <a name="iclrdebuggingopenvirtualprocess-method"></a>ICLRDebugging::OpenVirtualProcess 메서드
프로세스에 로드 된 공용 언어 런타임 (CLR) 모듈에 해당 하는 ICorDebugProcess 인터페이스를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT OpenVirtualProcess(  
    [in] ULONG64 moduleBaseAddress,  
    [in] IUnknown * pDataTarget,  
    [in] ICLRDebuggingLibraryProvider * pLibraryProvider,  
    [in] CLR_DEBUGGING_VERSION * pMaxDebuggerSupportedVersion,  
    [in] REFIID riidProcess,  
    [out, iid_is(riidProcess)] IUnknown ** ppProcess,  
    [in, out] CLR_DEBUGGING_VERSION * pVersion,  
    [out] CLR_DEBUGGING_PROCESS_FLAGS * pdwFlags);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleBaseAddress`  
 [in] 대상 프로세스에서 모듈의 기본 주소입니다. 지정된 된 모듈이 CLR 모듈이 없으면 COR_E_NOT_CLR 반환 됩니다.  
  
 `pDataTarget`  
 [in] 데이터 대상 추상화를 관리 되는 경우 디버거가 프로세스 상태를 검사할 수 있습니다. 디버거를 구현 해야 합니다 [ICorDebugDataTarget](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-interface.md) 인터페이스입니다. 구현 해야 합니다 [ICLRDebuggingLibraryProvider](../../../../docs/framework/unmanaged-api/debugging/iclrdebugginglibraryprovider-interface.md) 디버깅 중인 CLR 설치 되지 않은 로컬 컴퓨터의 시나리오를 지원 하도록 인터페이스입니다.  
  
 `pLibraryProvider`  
 [in] 버전별 디버깅 라이브러리 있고에 로드 된 요청 수를 허용 하는 라이브러리 공급자 콜백 인터페이스입니다. 경우에이 매개 변수는 필수 `ppProcess` 나 `pFlags` 아닙니다 `null`합니다.  
  
 `pMaxDebuggerSupportedVersion`  
 [in] 이 디버거를 디버깅할 수는 CLR의 가장 높은 버전입니다. 주, 부를 지정 하 고 및 빌드 버전을 디버거에서이 CLR 최신 하 고, 수정 번호 서비스 릴리스 이후 전체 CLR을 수용 하기 위해 65535로 설정 해야 합니다.  
  
 `riidProcess`  
 [in] 검색할 ICorDebugProcess 인터페이스의 ID입니다. 현재 허용 되는 유일한 값은 IID_CORDEBUGPROCESS3, IID_CORDEBUGPROCESS2, 및 IID_CORDEBUGPROCESS 합니다.  
  
 `ppProcess`  
 [out] 로 식별 되는 COM 인터페이스에 대 한 포인터 `riidProcess`합니다.  
  
 `pVersion`  
 [out에서] CLR의 버전입니다. 이 값은 입력에 대해 `null`합니다. 가리킬 수도 있습니다는 [CLR_DEBUGGING_VERSION](../../../../docs/framework/unmanaged-api/debugging/clr-debugging-version-structure.md) 구조체의 경우에서 구조체 `wStructVersion` 필드를 0 (영)으로 초기화 되어야 합니다.  
  
 반환된 된 출력에서 `CLR_DEBUGGING_VERSION` 구조 CLR의 버전 정보를 사용 하 여 채워집니다.  
  
 `pdwFlags`  
 [out] 지정 된 런타임에 대 한 정보 제공 용 이므로 플래그입니다. 참조 된 [CLR_DEBUGGING_PROCESS_FLAGS](../../../../docs/framework/unmanaged-api/debugging/clr-debugging-process-flags-enumeration.md) 플래그에 대 한 항목입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|E_POINTER|`pDataTarget`가 `null`인 경우|  
|CORDBG_E_LIBRARY_PROVIDER_ERROR|합니다 [ICLRDebuggingLibraryProvider](../../../../docs/framework/unmanaged-api/debugging/iclrdebugginglibraryprovider-interface.md) 콜백 오류를 반환 하거나 유효한 핸들을 제공 하지 않습니다.|  
|CORDBG_E_MISSING_DATA_TARGET_INTERFACE|`pDataTarget` 이 버전의 런타임이 필요한 데이터 대상 인터페이스를 구현 하지 않습니다.|  
|CORDBG_E_NOT_CLR|표시 된 모듈이 CLR 모듈이 아닙니다. 메모리가 손상, 모듈을 사용할 수 없는 CLR 버전은 shim 된 버전 보다 최신 때문에 CLR 모듈을 검색할 수 없는 경우에이 HRESULT 반환 됩니다.|  
|CORDBG_E_UNSUPPORTED_DEBUGGING_MODEL|이 런타임 버전에서이 디버깅 모델을 지원 하지 않습니다. 현재 디버깅 모델을.NET Framework 4 이전 버전의 CLR에서 지원 되지 않습니다. `pwszVersion` 출력 매개 변수는 여전히이 오류 후 올바른 값으로 설정 됩니다.|  
|CORDBG_E_UNSUPPORTED_FORWARD_COMPAT|버전의 CLR이 디버거에서 지원 해야 하는 버전 보다 큽니다. `pwszVersion` 출력 매개 변수는 여전히이 오류 후 올바른 값으로 설정 됩니다.|  
|E_NO_INTERFACE|`riidProcess` 인터페이스를 사용할 수 없습니다.|  
|CORDBG_E_UNSUPPORTED_VERSION_STRUCT|합니다 `CLR_DEBUGGING_VERSION` 구조에 대 한 인식 된 값이 없는 `wStructVersion`합니다. 이 이번에 허용 되는 유일한 값은 0입니다.|  
  
## <a name="exceptions"></a>예외  
  
## <a name="remarks"></a>설명  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
