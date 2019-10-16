---
title: ICorDebugHandleValue 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugHandleValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHandleValue
helpviewer_keywords:
- ICorDebugHandleValue interface [.NET Framework debugging]
ms.assetid: 66fcd2b8-ac66-414b-83a8-75a925e17772
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3219554cf953b8de31e236b2f484478172673f7b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69915001"
---
# <a name="icordebughandlevalue-interface"></a>ICorDebugHandleValue 인터페이스

디버거에서 가비지 수집에 대 한 핸들을 만든 참조 값을 나타내는 ICorDebugReferenceValue의 서브 클래스입니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[Dispose 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebughandlevalue-dispose-method.md)|인터페이스 포인터를 명시적으로 해제 `ICorDebugHandleValue` 하지 않고이 개체에서 참조 하는 핸들을 해제 합니다.|  
|[GetHandleType 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebughandlevalue-gethandletype-method.md)|이 `ICorDebugHandleValue`에서 참조 하는 핸들의 종류를 설명 하는 CorDebugHandleType 값을 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 디버깅 된 코드의 실행이 중단 되 면 개체가무효화됩니다.`ICorDebugReferenceValue` 는 `ICorDebugHandleValue` 명시적으로 해제 될 때까지 중단 및 연속을 통해 참조를 유지 관리 합니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
