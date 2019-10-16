---
title: ICorDebugHeapValue3::GetMonitorEventWaitList 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue3.GetMonitorEventWaitList
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue3::GetMonitorEventWaitList
helpviewer_keywords:
- ICorDebugHeapValue3::GetMonitorEventWaitList method [.NET Framework debugging]
- GetMonitorEventWaitList method [.NET Framework debugging]
ms.assetid: 035a9035-ac66-4953-b48a-99652b42b7fe
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: db34d56fd4d074551ca4823681bc5d94e76df758
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67756624"
---
# <a name="icordebugheapvalue3getmonitoreventwaitlist-method"></a>ICorDebugHeapValue3::GetMonitorEventWaitList 메서드
모니터 잠금과 사용 하 여 연결 된 이벤트에 대 한 큐에 대기 중인 스레드는 정렬 된 목록을 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetMonitorEventWaitList (  
    [out] ICorDebugThreadEnum **ppThreadEnum  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppThreadEnum`  
 [out] 스레드 순서 있는 목록을 제공 하는 ICorDebugThreadEnum 열거자입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|The list is not empty.|  
|S_FALSE|목록이 비어 있습니다.|  
  
## <a name="exceptions"></a>예외  
  
## <a name="remarks"></a>설명  
 목록의 첫 번째 스레드는 다음 호출에 의해 제공 되는 첫 번째 스레드가 <xref:System.Threading.Monitor.Pulse%28System.Object%29?displayProperty=nameWithType>합니다. 목록에서 다음 스레드에서 다음 호출 등에 출시 됩니다.  
  
 목록에 비어 있지 않으면이 메서드는 S_OK를 반환 합니다. 목록이 비어 있으면 반환 S_FALSE; 이 경우는 열거형은 비어 있더라도 여전히 유효 합니다.  
  
 두 경우 모두 열거형 인터페이스는 현재 동기화 된 상태의 기간에만 사용할 수 있습니다. 그러나 스레드의 인터페이스에서 분배는 스레드가 종료 될 때까지 유효 합니다.  
  
 경우 `ppThreadEnum` 유효한 포인터가 아닙니다 결과가 정의 되지 않습니다.  
  
 확인할 수 없는 모니터에 대 한 대기 중인 스레드가 있으면 하는 것과 같은 오류가 발생 하는 경우 메서드는 오류를 나타내는 HRESULT를 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
