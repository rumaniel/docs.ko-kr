---
title: ICorDebugManagedCallback2::FunctionRemapOpportunity 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.FunctionRemapOpportunity
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::FunctionRemapOpportunity
helpviewer_keywords:
- FunctionRemapOpportunity method [.NET Framework debugging]
- ICorDebugManagedCallback2::FunctionRemapOpportunity method [.NET Framework debugging]
ms.assetid: 0d6471bc-ad9b-4b1d-a307-c10443918863
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 24f058ff11a1155aa53a1d1f222ff1230c1c23e3
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67760988"
---
# <a name="icordebugmanagedcallback2functionremapopportunity-method"></a>ICorDebugManagedCallback2::FunctionRemapOpportunity 메서드
코드 실행 이전 버전의 편집된 된 함수에서 시퀀스 위치에 도달 했습니다 디버거에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT FunctionRemapOpportunity (  
    [in] ICorDebugAppDomain   *pAppDomain,  
    [in] ICorDebugThread      *pThread,  
    [in] ICorDebugFunction    *pOldFunction,  
    [in] ICorDebugFunction    *pNewFunction,  
    [in] ULONG32              oldILOffset  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pAppDomain`  
 [in] 편집된 된 함수를 포함 하는 응용 프로그램 도메인을 나타내는 ICorDebugAppDomain 개체에 대 한 포인터입니다.  
  
 `pThread`  
 [in] 다시 매핑 중단점이 발생 하는 스레드를 나타내는 ICorDebugThread 개체에 대 한 포인터입니다.  
  
 `pOldFunction`  
 [in] 현재 스레드에서 실행 중인 함수의 버전을 나타내는 ICorDebugFunction 개체에 대 한 포인터입니다.  
  
 `pNewFunction`  
 [in] 최신 버전의 함수를 나타내는 ICorDebugFunction 개체에 대 한 포인터입니다.  
  
 `oldILOffset`  
 [in] 이전 버전의 함수에 명령 포인터의 Microsoft MSIL (intermediate language) 오프셋입니다.  
  
## <a name="remarks"></a>설명  
 이 콜백은 디버거를 호출 하 여 명령에 대 한 포인터로 지정 된 함수의 새 버전에 적절 한 위치를 다시 매핑할 수 있는 기회를 제공 합니다 [ICorDebugILFrame2::RemapFunction](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe2-remapfunction-method.md) 메서드. 디버거를 호출 하지 않습니다 `RemapFunction` 호출 하기 전에 [icordebugcontroller:: Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) 메서드를 런타임에서 계속 이전 코드를 실행 하 고 다른 시기가 `FunctionRemapOpportunity` 다음 시퀀스 위치에서 콜백을 합니다.  
  
 이 콜백은 디버거 하면 S_OK가 반환 될 때까지 이전 버전의 지정된 된 함수를 실행 하는 프레임 마다 호출 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugManagedCallback2 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-interface.md)
- [ICorDebugManagedCallback 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)
