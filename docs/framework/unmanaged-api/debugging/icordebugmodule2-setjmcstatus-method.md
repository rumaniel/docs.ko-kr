---
title: ICorDebugModule2::SetJMCStatus 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.SetJMCStatus
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::SetJMCStatus
helpviewer_keywords:
- SetJMCStatus method, ICorDebugModule2 interface [.NET Framework debugging]
- ICorDebugModule2::SetJMCStatus method [.NET Framework debugging]
ms.assetid: 8c6d2089-4dbb-4715-b9e9-2a4491c8c9ce
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d438123dcefb901098954845596c210e5b76cea6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67764111"
---
# <a name="icordebugmodule2setjmcstatus-method"></a>ICorDebugModule2::SetJMCStatus 메서드
이 ICorDebugModule2 제외한 지정 된 값의 모든 클래스의 모든 메서드의 코드 JMC (내) 상태를 설정 합니다 `pTokens` 반대 값으로 설정 하는 배열입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetJMCStatus (  
    [in] BOOL                        bIsJustMyCode,  
    [in] ULONG32                     cTokens,  
    [in, size_is(cTokens)] mdToken   pTokens[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `bIsJustMycode`  
 [in] 로 `true` 로 설정 하는 코드가 고 그렇지 않으면 디버깅 인 경우 `false`합니다.  
  
 `cTokens`  
 [in] `pTokens` 배열의 크기입니다.  
  
 `pTokens`  
 [in] 배열을 `mdToken` 로 설정 된 JMC 상태에 있는 메서드를 참조 하는 각 값!`bIsJustMycode`합니다.  
  
## <a name="remarks"></a>설명  
 에 지정 된 각 메서드의 JMC 상태를 `pTokens` 과 반대로 설정 되어 배열은 `bIsJustMycode` 값. 이 모듈의 다른 모든 메서드의 상태를로 `bIsJustMycode` 값입니다.  
  
 `SetJMCStatus` 메서드는이 모듈의 모든 이전 JMC 설정을 지웁니다.  
  
 `SetJMCStatus` 메서드는 모든 함수는 성공적으로 설정 된 경우 s_ok이 고, HRESULT를 반환 합니다. 표시 된 일부 함수는 경우 CORDBG_E_FUNCTION_NOT_DEBUGGABLE HRESULT를 반환 합니다 `true` 디버깅 가능 하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
