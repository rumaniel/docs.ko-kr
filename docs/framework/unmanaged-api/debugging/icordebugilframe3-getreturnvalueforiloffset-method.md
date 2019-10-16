---
title: ICorDebugILFrame3::GetReturnValueForILOffset 메서드
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
api_name:
- ICorDebugILFrame3.GetReturnValueForILOffset
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 06522727-5f64-4391-9331-11386883c352
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5832ec095ea0e96327f6a9636193da9c0c8a5dd2
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988266"
---
# <a name="icordebugilframe3getreturnvalueforiloffset-method"></a>ICorDebugILFrame3::GetReturnValueForILOffset 메서드
함수의 반환 값을 캡슐화 하는 "ICorDebugValue" 개체를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
HRESULT GetReturnValueForILOffset(  
    ULONG32 ILoffset,   
    [out] ICorDebugValue **ppReturnValue  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ILOffset`  
 IL 오프셋입니다. 설명 부분을 참조하세요.  
  
 `ppReturnValue`  
 함수 호출의 반환 값에 대 한 정보를 제공 하는 "ICorDebugValue" 인터페이스 개체의 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 [ICorDebugCode3:: GetReturnValueLiveOffset](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md) 메서드와 함께 메서드의 반환 값을 가져오는 데 사용 됩니다. 다음 두 코드 예제와 같이 반환 값이 무시 되는 메서드의 경우 특히 유용 합니다. 첫 번째 예제에서는 <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> 메서드를 호출 하지만 메서드의 반환 값을 무시 합니다.  
  
 [!code-csharp[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv1.cs#1)]
 [!code-vb[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv1.vb#1)]  
  
 두 번째 예제에서는 디버깅에서 훨씬 일반적인 문제를 보여 줍니다. 메서드는 메서드 호출에서 인수로 사용 되므로 해당 반환 값은 디버거가 호출 된 메서드를 통해 단계를 수행 하는 경우에만 액세스할 수 있습니다. 대부분의 경우 호출 된 메서드가 외부 라이브러리에서 정의 된 경우에는 불가능 합니다.  
  
 [!code-csharp[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv2.cs#2)]
 [!code-vb[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv2.vb#2)]  
  
 [ICorDebugCode3:: GetReturnValueLiveOffset](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md) 메서드를 함수 호출 사이트에 대 한 IL 오프셋으로 전달 하는 경우 하나 이상의 네이티브 오프셋을 반환 합니다. 그런 다음 디버거는 함수에서 이러한 네이티브 오프셋에 중단점을 설정할 수 있습니다. 디버거가 중단점 중 하나에 적중 하면이 메서드에 전달 된 것과 동일한 IL 오프셋을 전달 하 여 반환 값을 가져올 수 있습니다. 그런 다음 디버거는 설정 된 모든 중단점을 지워야 합니다.  
  
> [!WARNING]
> [ICorDebugCode3:: GetReturnValueLiveOffset 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md) 및 `ICorDebugILFrame3::GetReturnValueForILOffset` 메서드를 사용 하 여 참조 형식에 대해서만 반환 값 정보를 가져올 수 있습니다. 값 형식에서 반환 값 정보를 검색 하는 경우 (즉,에서 <xref:System.ValueType>파생 되는 모든 형식)은 지원 되지 않습니다.  
  
 `ILOffset` 매개 변수로 지정 된 il 오프셋은 함수 호출 사이트에 있어야 하며, 디버기는 동일한 IL 오프셋에 대해 [ICorDebugCode3:: GetReturnValueLiveOffset](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md) 메서드에서 반환 되는 네이티브 오프셋에 설정 된 중단점에서 중지 되어야 합니다. 디버기가 지정 된 IL 오프셋의 올바른 위치에서 중지 되지 않은 경우 API가 실패 합니다.  
  
 함수 호출에서 값을 반환 하지 않는 경우 API가 실패 합니다.  
  
 메서드 `ICorDebugILFrame3::GetReturnValueForILOffset` 는 x86 기반 및 AMD64 시스템 에서만 사용할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v451plus](../../../../includes/net-current-v451plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [GetReturnValueLiveOffset 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-getreturnvalueliveoffset-method.md)
- [ICorDebugILFrame3 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe3-interface.md)
