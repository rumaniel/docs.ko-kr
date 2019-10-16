---
title: CreateDebuggingInterfaceFromVersion 함수
ms.date: 03/30/2017
api_name:
- CreateDebuggingInterfaceFromVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- CreateDebuggingInterfaceFromVersion
helpviewer_keywords:
- CreateDebuggingInterfaceFromVersion function [.NET Framework hosting]
ms.assetid: a746a849-463c-44f5-a2f0-9e812ed8bcc3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fe34ffded73e8305e4ade3bb9b402b1d8e1bcc49
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67764685"
---
# <a name="createdebugginginterfacefromversion-function"></a>CreateDebuggingInterfaceFromVersion 함수
만듭니다는 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) 개체 정보를 기반으로 지정 된 버전입니다.  
  
 이 함수는.NET Framework 4에서 사용 되지 않습니다. CLR (공용 언어 런타임) 2.0에 대 한 인터페이스를 가져오려면 대신 합니다 [iclrruntimeinfo:: Getinterface](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getinterface-method.md) 메서드 인터페이스 식별자 IID_ICorDebug CLSID_CLRDebuggingLegacy 클래스 식별자를 지정 합니다. CLR 4에 대 한 인터페이스를 가져오거나 나중에 호출 하 여 [CLRCreateInstance](../../../../docs/framework/unmanaged-api/hosting/clrcreateinstance-function.md) 함수 및 클래스 식별자 CLSID_CLRDebugging 및 IID_ICLRDebugging 인터페이스 식별자를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateDebuggingInterfaceFromVersion (  
    [in]  int      iDebuggerVersion,   
    [in]  LPCWSTR  szDebuggeeVersion,   
    [out] IUnknown **ppCordb  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `iDebuggerVersion`  
 [in] 버전 `ICorDebug` 디버거에 의해 예상 됩니다. 참조 된 [CorDebugInterfaceVersion](../../../../docs/framework/unmanaged-api/debugging/cordebuginterfaceversion-enumeration.md) 유효한 값에 대 한 열거형입니다.  
  
 `szDebuggeeVersion`  
 [in] 응용 프로그램 또는 프로세스를 디버깅할 수와 연결 된 공용 언어 런타임 버전입니다. 참조를 [GetVersionFromProcess](../../../../docs/framework/unmanaged-api/hosting/getversionfromprocess-function.md) 하거나 [GetRequestedRuntimeVersion](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md) 이 값을 검색 하는 방법은 메서드.  
  
 `ppCordb`  
 [out] 에 대 한 포인터를 받는 위치를 `ICorDebug` 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음 값 외에도 WinError.h 파일에 정의 된 대로 표준 COM 오류 코드를 반환 합니다.  
  
|반환 코드|Description|  
|-----------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|E_INVALIDARG|`szDebuggeeVersion` 또는 `ppCordb` 는 null 또는 버전 문자열이 잘못 되었습니다.|  
  
## <a name="remarks"></a>설명  
 `szDebuggeeVersion` 매개 변수 MSCorDbi.dll의 해당 버전에 매핑됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [사용되지 않는 CLR 호스팅 함수](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
