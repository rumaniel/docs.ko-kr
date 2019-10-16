---
title: ICorDebugCode3::GetReturnValueLiveOffset 메서드
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugCode3.GetReturnValueLiveOffset
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode3::GetReturnValueLiveOffset
helpviewer_keywords:
- ICorDebugCode3::GetReturnValueLiveOffset method [.NET Framework debugging]
- GetReturnValueLiveOffset method [.NET Framework debugging]
ms.assetid: 8c2ff5d8-8c04-4423-b1e1-e1c8764b36d3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5aa53d1c9d101544f532c51f43a8b47143117813
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988280"
---
# <a name="icordebugcode3getreturnvalueliveoffset-method"></a>ICorDebugCode3::GetReturnValueLiveOffset 메서드
지정 된 IL 오프셋의 경우 디버거가 함수에서 반환 값을 가져올 수 있도록 중단점이 배치 되어야 하는 네이티브 오프셋을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
HRESULT GetReturnValueLiveOffset(  
    [in] ULONG32 ILoffset,  
    [in] ULONG32 bufferSize,   
    [out] ULONG32 *pFetched,   
    [out, size_is(buffersize), length_is(*pFetched)] ULong32 pOffsets[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ILoffset`  
 IL 오프셋입니다. 함수 호출 사이트 여야 합니다. 그렇지 않으면 함수 호출이 실패 합니다.  
  
 `bufferSize`  
 저장 `pOffsets`하는 데 사용할 수 있는 바이트 수입니다.  
  
 `pFetched`  
 실제로 반환 된 오프셋 수에 대 한 포인터입니다. 일반적으로 해당 값은 1 이지만 단일 IL 명령은 여러 `CALL` 어셈블리 명령에 매핑할 수 있습니다.  
  
 `pOffsets`  
 네이티브 오프셋의 배열입니다. 일반적으로 `pOffsets` 에는 단일 오프셋이 포함 되지만 단일 IL 명령은 여러 `CALL` 어셈블리 명령에 매핑할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 [ICorDebugILFrame3:: GetReturnValueForILOffset](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe3-getreturnvalueforiloffset-method.md) 메서드와 함께 사용 되어 참조 형식을 반환 하는 메서드의 반환 값을 가져옵니다. 함수 호출 사이트에 대 한 IL 오프셋을이 메서드에 전달 하면 하나 이상의 네이티브 오프셋을 반환 합니다. 그런 다음 디버거는 함수에서 이러한 네이티브 오프셋에 중단점을 설정할 수 있습니다. 디버거가 중단점 중 하나에 적중 하면이 메서드에 전달 된 것과 동일한 IL 오프셋을 [ICorDebugILFrame3:: GetReturnValueForILOffset](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe3-getreturnvalueforiloffset-method.md) 메서드에 전달 하 여 반환 값을 가져올 수 있습니다. 그런 다음 디버거는 설정 된 모든 중단점을 지워야 합니다.  
  
> [!WARNING]
> 및 `ICorDebugCode3::GetReturnValueLiveOffset` [ICorDebugILFrame3:: getreturnvalueforiloffset](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe3-getreturnvalueforiloffset-method.md) 메서드를 사용 하 여 참조 형식에 대해서만 반환 값 정보를 가져올 수 있습니다. 값 형식에서 반환 값 정보를 검색 하는 경우 (즉,에서 <xref:System.ValueType>파생 되는 모든 형식)은 지원 되지 않습니다.  
  
 함수는 다음 표에 `HRESULT` 나와 있는 값을 반환 합니다.  
  
|`HRESULT` 값|Description|  
|---------------------|-----------------|  
|`S_OK`|명령 실행 성공|  
|`CORDBG_E_INVALID_OPCODE`|지정 된 IL 오프셋 사이트가 호출 명령이 아니거나 함수가를 반환 `void`합니다.|  
|`CORDBG_E_UNSUPPORTED`|지정 된 IL 오프셋은 적절 한 호출 이지만 반환 형식은 반환 값을 가져오는 데 지원 되지 않습니다.|  
  
 메서드 `ICorDebugCode3::GetReturnValueLiveOffset` 는 x86 기반 및 AMD64 시스템 에서만 사용할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v451plus](../../../../includes/net-current-v451plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [GetReturnValueForILOffset 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe3-getreturnvalueforiloffset-method.md)
- [ICorDebugCode3 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugcode3-interface.md)
