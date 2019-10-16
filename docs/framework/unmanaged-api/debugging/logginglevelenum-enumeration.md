---
title: LoggingLevelEnum 열거형
ms.date: 03/30/2017
api_name:
- LoggingLevelEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- LoggingLevelEnum
helpviewer_keywords:
- LoggingLevelEnum enumeration [.NET Framework debugging]
ms.assetid: 09daac08-005a-46b2-beab-408d0820c5e5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9659dd835bb60adf8471f73ed45b6588cf15126f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67752591"
---
# <a name="logginglevelenum-enumeration"></a>LoggingLevelEnum 열거형
관리되는 스레드가 이벤트를 기록할 때 이벤트 로그에 기록되는 설명 메시지의 보안 수준을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum LoggingLevelEnum {  
    LTraceLevel0 = 0,  
    LTraceLevel1,  
    LTraceLevel2,  
    LTraceLevel3,  
    LTraceLevel4,  
    LStatusLevel0 = 20,  
    LStatusLevel1,  
    LStatusLevel2,  
    LStatusLevel3,  
    LStatusLevel4,  
    LWarningLevel = 40,  
    LErrorLevel = 50,  
    LPanicLevel = 100  
} LoggingLevelEnum;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`LTraceLevel0`|메시지의 추적 수준이 0입니다.|  
|`LTraceLevel1`|메시지의 추적 수준이 1입니다.|  
|`LTraceLevel2`|메시지의 추적 수준이 2입니다.|  
|`LTraceLevel3`|메시지를 추적 수준 3입니다.|  
|`LTraceLevel4`|메시지의 추적 수준이 4입니다.|  
|`LStatusLevel0`|메시지의 상태 수준이 0입니다.|  
|`LStatusLevel1`|메시지의 상태 수준이 1입니다.|  
|`LStatusLevel2`|메시지의 상태 수준이 2입니다.|  
|`LStatusLevel3`|메시지의 상태 수준이 3입니다.|  
|`LStatusLevel4`|메시지의 상태 수준이 4입니다.|  
|`LWarningLevel`|메시지에는 경고 수준입니다.|  
|`LErrorLevel`|메시지 오류 수준입니다.|  
|`LPanicLevel`|메시지에는 심각한 오류 수준입니다.|  
  
## <a name="remarks"></a>설명  
 CLR (공용 언어 런타임)를 호출 합니다 [icordebugmanagedcallback:: Logmessage](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-logmessage-method.md) 메서드 알리도록 디버거 관리 되는 스레드는 이벤트를 기록 했습니다. CLR 값을 전달 합니다 `LoggingLevelEnum` 이벤트 로그에 작성 한 관리 되는 스레드는 메시지의 심각도 수준을 나타내는 열거형입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.EventLog>
- [디버깅 열거형](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
