---
title: ICorDebugVariableHome::GetRegister 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHome.GetRegister
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome::GetRegister
helpviewer_keywords:
- ICorDebugVariableHome::GetRegister method [.NET Framework debugging]
- GetRegister method, ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: a5eecd7b-b04c-4266-bff2-7c8771d519a8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f4b3b80546095b79dc5b551a9c5e92ec15c0dddb
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67771792"
---
# <a name="icordebugvariablehomegetregister-method"></a>ICorDebugVariableHome::GetRegister 메서드
위치 형식의 변수를 포함 하는 레지스터를 가져옵니다 `VLT_REGISTER`, 및 위치 형식의 변수에 대 한 기본 등록 `VLT_REGISTER_RELATIVE`합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetRegister(  
    [out] CorDebugRegister *pRegister  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pRegister`  
 [out] 위치 형식의 변수에 대 한 등록을 나타내는 CorDebugRegister 열거형 값 `VLT_REGISTER`, 및 위치 형식의 변수에 대 한 기본 등록 `VLT_REGISTER_RELATIVE`합니다.  
  
## <a name="return-value"></a>반환 값  
 메서드는 다음 값을 반환 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|`S_OK`|변수가 가리키는 레지스터는 `pRegister` 인수입니다.|  
|`E_FAIL`|변수는 등록 또는 등록에 상대적인 위치에 없는 경우|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [VariableLocationType 열거형](../../../../docs/framework/unmanaged-api/debugging/variablelocationtype-enumeration.md)
- [ICorDebugVariableHome 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-interface.md)
