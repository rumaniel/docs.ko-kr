---
title: Silverlight용 CreateDebuggingInterfaceFromVersion 함수
ms.date: 03/30/2017
f1_keywords:
- CreateDebuggingInterfaceFromVersion
helpviewer_keywords:
- CreateDebuggingInterfaceFromVersion function
- debugging API [Silverlight]
- Silverlight, debugging
ms.assetid: 35c7a18f-133a-4584-bd25-bb338568b0c6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 96968956b513e1ae80a25f5fb4afea48bf888876
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739271"
---
# <a name="createdebugginginterfacefromversion-function-for-silverlight"></a>Silverlight용 CreateDebuggingInterfaceFromVersion 함수
반환 되는 공용 언어 런타임 (CLR) 버전 문자열을 허용 합니다 [CreateVersionStringFromModule 함수](../../../../docs/framework/unmanaged-api/debugging/createversionstringfrommodule-function.md), 하 고 해당 디버거 인터페이스를 반환 합니다 (일반적으로 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)).  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateDebuggingInterfaceFromVersion (  
    [in]  LPCWSTR      szDebuggeeVersion,  
    [out] IUnknown**   ppCordb,  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `szDebuggeeVersion`  
 [in] 반환 하는 대상 디버기의 clr 버전 문자열을 [CreateVersionStringFromModule 함수](../../../../docs/framework/unmanaged-api/debugging/createversionstringfrommodule-function.md)합니다.  
  
 `ppCordb`  
 [out] COM 개체(`IUnknown`)에 대한 포인터의 포인터입니다. 이 개체를 캐스팅할 수는 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) 반환 되기 전에 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 S_OK  
 `ppCordb` 구현 하는 유효한 개체를 참조 합니다 [ICorDebug 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) 인터페이스입니다.  
  
 E_INVALIDARG  
 `szDebuggeeVersion` 또는 `ppCordb`가 null입니다.  
  
 CORDBG_E_DEBUG_COMPONENT_MISSING  
 CLR 디버깅에 필요한 구성 요소를 찾을 수 없습니다. 즉, mscordbi.dll 또는 mscordaccore.dll이 대상 CoreCLR.dll과 동일한 디렉터리에 없습니다.  
  
 CORDBG_E_INCOMPATIBLE_PROTOCOL  
 mscordbi.dll 또는 mscordaccore.dll이 대상 CoreCLR.dll과 동일한 버전이 아닙니다.  
  
 E_FAIL(또는 다른 E_ 반환 코드)  
 반환할 수 없습니다는 [ICorDebug 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)합니다.  
  
## <a name="remarks"></a>설명  
 반환된 인터페이스는 대상 프로세스의 CLR에 연결하고 CLR에서 실행 중인 관리 코드를 디버그하기 위한 기능을 제공합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** dbgshim.h  
  
 **라이브러리:** dbgshim.dll  
  
 **.NET framework 버전:** 3.5 SP1
