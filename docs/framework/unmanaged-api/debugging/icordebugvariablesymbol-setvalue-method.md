---
title: ICorDebugVariableSymbol::SetValue 메서드
ms.date: 03/30/2017
ms.assetid: 4609418d-71fa-44bc-9618-4d529d25cabb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5436f56d3dcad7de3df2296485b0a36e5b3cfd79
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967960"
---
# <a name="icordebugvariablesymbolsetvalue-method"></a>ICorDebugVariableSymbol::SetValue 메서드
바이트 배열의 값을 변수에 할당합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetValue(  
   [in] ULONG32 offset,  
   [in] DWORD threadID,  
   [in] ULONG32 cbContext,  
   [in, size_is(cbContext)] BYTE context[],  
   [in] ULONG32 cbValue,  
   [in, size_is(cbValue)] BYTE pValue[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `offset`  
 [in] 값을 설정할 변수의 시작 오프셋입니다. 이 매개 변수는 개체의 멤버 필드에 쓸 때 사용됩니다.  
  
 `threadID`  
 [in] 새 값을 반영하도록 컨텍스트를 업데이트해야 하는 스레드의 스레드 식별자입니다.  
  
 `cbContext`  
 [in] 스레드 컨텍스트의 크기(바이트)입니다.  
  
 `context`  
 [in] 값을 쓰는 데 사용되는 스레드 컨텍스트입니다.  
  
 `cbValue`  
 [in] `pValue` 버퍼의 크기(바이트)입니다.  
  
 `pValue`  
 [in] 설정할 값이 들어 있는 버퍼입니다.  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]
> 이 메서드는 .NET 네이티브에서만 사용할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugVariableSymbol 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablesymbol-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
