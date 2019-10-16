---
title: ICorDebugRegisterSet2::GetRegistersAvailable 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet2.GetRegistersAvailable
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet2::GetRegistersAvailable
helpviewer_keywords:
- GetRegistersAvailable method, ICorDebugRegisterSet2 interface [.NET Framework debugging]
- ICorDebugRegisterSet2::GetRegistersAvailable method [.NET Framework debugging]
ms.assetid: f3ed344b-0d3a-44e8-8000-2a97e0805a2c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5d4ab49aaccd77fac497bd86413915e82c99ed3e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67744912"
---
# <a name="icordebugregisterset2getregistersavailable-method"></a>ICorDebugRegisterSet2::GetRegistersAvailable 메서드
사용 가능한 레지스터의 비트맵을 제공 하는 바이트 배열을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetRegistersAvailable (  
    [in] ULONG32 numChunks,  
    [out, size_is(numChunks)] BYTE availableRegChunks[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `numChunks`  
 [in] `availableRegChunks` 배열의 크기입니다.  
  
 `availableRegChunks`  
 [out] 바이트 배열에는 각 비트 레지스터에 해당합니다. 레지스터 사용 가능한 경우 레지스터의 해당 비트가 설정 됩니다.  
  
## <a name="remarks"></a>설명  
 CorDebugRegister 열거형의 값을 다른 마이크로프로세서의 레지스터를 지정합니다. 각 값의 상위 5 비트는 인덱스를 `availableRegChunks` 바이트 배열입니다. 각 값의 세 가지 하위 비트는 인덱싱된 바이트에서 비트 위치를 식별 합니다. 지정 된 `CorDebugRegister` 특정 레지스터를 마스크의 레지스터의 위치를 지정 하는 값은 다음과 같이 결정 됩니다.  
  
1. 정확한 바이트에 액세스 하는 데 필요한 인덱스를 추출 합니다 `availableRegChunks` 배열:  
  
     `CorDebugRegister` 값 >> 3  
  
2. 여기서 0 비트는 최하위 비트에서 인덱싱된 바이트 비트 위치를 추출 합니다.  
  
     `CorDebugRegister` 값 및 7  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugRegisterSet2 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugregisterset2-interface.md)
- [ICorDebugRegisterSet 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugregisterset-interface.md)
