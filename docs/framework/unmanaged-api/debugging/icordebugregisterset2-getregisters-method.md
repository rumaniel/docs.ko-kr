---
title: ICorDebugRegisterSet2::GetRegisters 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet2.GetRegisters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet2::GetRegisters
helpviewer_keywords:
- GetRegisters method, ICorDebugRegisterSet2 interface [.NET Framework debugging]
- ICorDebugRegisterSet2::GetRegisters method [.NET Framework debugging]
ms.assetid: dbc498a8-ba3f-42f2-bdd9-b623c77a1019
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3c1b90390689e709ee131935bd6417fa6b273eb2
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769988"
---
# <a name="icordebugregisterset2getregisters-method"></a>ICorDebugRegisterSet2::GetRegisters 메서드
(코드를 현재 실행 중인 플랫폼)에 대 한 각 레지스터의 값을 가져옵니다 지정 된 비트 마스크에 의해 지정 된 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetRegisters (  
    [in] ULONG32 maskCount,  
    [in, size_is(maskCount)] BYTE mask[],  
    [in] ULONG32 regCount,  
    [out, size_is(regCount)] CORDB_REGISTER regBuffer[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `maskCount`  
 [in] 크기 (바이트)의는 `mask` 배열입니다.  
  
 `mask`  
 [in] 바이트 배열에는 각 비트 레지스터에 해당합니다. 이 비트가 1 인 경우 해당 레지스터의 값이 검색 됩니다.  
  
 `regCount`  
 [in] 레지스터 값을 검색할 수 있습니다.  
  
 `regBuffer`  
 [out] 배열을 `CORDB_REGISTER` 레지스터의 값을 받습니다. 각 개체입니다.  
  
## <a name="remarks"></a>설명  
 `GetRegisters` 메서드 마스크에 의해 지정 된 레지스터에서 값의 배열을 반환 합니다. 배열에 마스크 비트가 설정 되지 않은 레지스터의 값을 없습니다. 따라서 크기는 `regBuffer` 배열 마스크의 1의 수가 동일 해야 합니다. 경우 변수의 `regCount` 마스크를 레지스터의 값에 의해 지정 된 레지스터 수 집합에서 잘립니다에 너무 작습니다. 하는 경우 `regCount` 너무 커서를 사용 하지 않는 `regBuffer` 요소를 수정 되지 것입니다.  
  
 마스크에 의해를 사용할 수 없는 레지스터를 지정 하는 경우 해당 등록에 대 한 비활성화 상태 값을 반환 됩니다.  
  
 `ICorDebugRegisterSet2::GetRegisters` 메서드는 64 개 등록 하는 플랫폼에 대 한 필요 합니다. 예를 들어, IA64 있으므로 128 일반 용도 레지스터와 부동 소수점 레지스터 128 비트 마스크에 64 비트 이상이 필요 합니다.  
  
 X86와 같은 플랫폼의 경우에는 64 개 이상의 레지스터가 없는 경우는 `GetRegisters` 메서드 실제로 변환 하는 바이트를 `mask` 바이트 배열에는 `ULONG64` 를 호출 하는 [ICorDebugRegisterSet:: GetRegisters](../../../../docs/framework/unmanaged-api/debugging/icordebugregisterset-getregisters-method.md) 를 사용 하는 메서드는 `ULONG64` 마스크입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugRegisterSet2 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugregisterset2-interface.md)
- [ICorDebugRegisterSet 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugregisterset-interface.md)
