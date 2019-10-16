---
title: ICorDebugThread3::GetActiveInternalFrames 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugThread3.GetActiveInternalFrames Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread3::GetActiveInternalFrames
helpviewer_keywords:
- ICorDebugThread3::GetActiveInternalFrames method [.NET Framework debugging]
- GetActiveInternalFrames method [.NET Framework debugging]
ms.assetid: d69796b4-5b6d-457c-85f6-2cf42e8a8773
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 58aaf0445fe42d083c12541056cb362f9a994944
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67765218"
---
# <a name="icordebugthread3getactiveinternalframes-method"></a>ICorDebugThread3::GetActiveInternalFrames 메서드
내부 프레임의 배열을 반환 합니다 ([ICorDebugInternalFrame2](../../../../docs/framework/unmanaged-api/debugging/icordebuginternalframe2-interface.md) 개체)를 스택에 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp 
HRESULT GetActiveInternalFrames  
      (  
      [in] ULONG32 cInternalFrames,  
      [out] ULONG32 *pcInternalFrames,  
      [in, out,size_is(cInternalFrames), length_is(*pcInternalFrames)]  
            ICorDebugInternalFrame2 * ppInternalFrames[]  
      );  
```  
  
## <a name="parameters"></a>매개 변수  
 `cInternalFrames`  
 [in] 예상 하는 내부 프레임 수가 `ppInternalFrames`합니다.  
  
 `pcInternalFrames`  
 [out] 에 대 한 포인터를 `ULONG32` 스택에 내부 프레임 수를 포함 하는 합니다.  
  
 `ppInternalFrames`  
 [out에서] 배열 스택에 내부 프레임의 주소에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|합니다 [ICorDebugInternalFrame2](../../../../docs/framework/unmanaged-api/debugging/icordebuginternalframe2-interface.md) 개체를 만들었습니다.|  
|E_INVALIDARG|`cInternalFrames` 0이 아닌 하 고 `ppInternalFrames` 됩니다 `null`, 또는 `pcInternalFrames` 는 `null`합니다.|  
|HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)|`ppInternalFrames` 내부 프레임의 수보다 작습니다.|  
  
## <a name="exceptions"></a>예외  
  
## <a name="remarks"></a>설명  
 내부 프레임은 임시 데이터를 저장 하는 런타임에서 스택에 밀어 넣은 데이터 구조입니다.  
  
 처음 호출할 때는 `GetActiveInternalFrames`를 설정 해야 합니다 `cInternalFrames` 매개 변수를 0 (영) 및 `ppInternalFrames` 매개 변수를 null. 때 `GetActiveInternalFrames` 먼저 반환 `pcInternalFrames` 스택에 내부 프레임 수를 포함 합니다.  
  
 `GetActiveInternalFrames` 다음 호출 해야 두 번째 시간입니다. 적절 한 개수를 전달 해야 합니다 (`pcInternalFrames`)에 `cInternalFrames` 매개 변수를 적절 한 크기의 배열에 대 한 포인터를 지정 하 고 `ppInternalFrames`합니다.  
  
 사용 된 [icordebugstackwalk:: Getframe](../../../../docs/framework/unmanaged-api/debugging/icordebugthread3-getactiveinternalframes-method.md) 실제 반환 방법 스택 프레임입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
