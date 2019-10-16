---
title: ICorDebugThread::GetCurrentException 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetCurrentException
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetCurrentException
helpviewer_keywords:
- ICorDebugThread::GetCurrentException method [.NET Framework debugging]
- GetCurrentException method [.NET Framework debugging]
ms.assetid: 331ed465-a195-4359-8584-b82c6098b29b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2a6d53ebfebb8c883065ce119c2338a2225f0472
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67762488"
---
# <a name="icordebugthreadgetcurrentexception-method"></a>ICorDebugThread::GetCurrentException 메서드
현재 관리 코드에 의해 throw 되는 예외를 나타내는 ICorDebugValue 개체에 대 한 인터페이스 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetCurrentException (  
    [out] ICorDebugValue **ppExceptionObject  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppExceptionObject`  
 [out] 주소에 대 한 포인터는 `ICorDebugValue` 관리 코드에서 throw 되는 예외를 나타내는 개체입니다.  
  
## <a name="remarks"></a>설명  
 예외 개체는 끝날 때까지 예외가 throw 된 시점부터 존재는 `catch` 블록입니다. ICorDebugEval 메서드에서 수행 하는 함수 평가 설정에 예외 개체를 지우고 완료 되 면 복원 됩니다.  
  
 예외 (예를 들어, 예외가 throw 되 면 필터 또는 함수 실행) 중첩 될 수 있도록 단일 스레드에서 여러 처리 되지 않은 예외가 있을 수 있습니다. `GetCurrentException` 가장 최근 예외를 반환합니다.  
  
 예외 개체 및 형식 예외의 수명 동안 변경 될 수 있습니다. 예를 들어, x 형식의 예외가 throw 되 면 공용 언어 런타임 (CLR) 고 수 있습니다 메모리 부족의 메모리 부족 예외가 수준을 올립니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
