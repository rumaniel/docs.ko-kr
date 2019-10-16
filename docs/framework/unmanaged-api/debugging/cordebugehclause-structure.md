---
title: CorDebugEHClause 구조
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- CorDebugEHClause
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 0e350a1b-6997-46d0-bfc5-962a5011ef43
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 839e698c8921f916fad174bae4f4cc8bb4d02994
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61609076"
---
# <a name="cordebugehclause-structure"></a>CorDebugEHClause 구조
[.NET Framework 4.5.2 이상 버전에서 지원됨]  
  
 지정된 IL(중간 언어) 코드 부분에 대한 EH(예외 처리) 절을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
typedef struct _CorDebugEHClause {  
   ULONG32 Flags;  
   ULONG32 TryOffset;  
   ULONG32 TryLength;  
   ULONG32 HandlerOffset;  
   ULONG32 HandlerLength;  
   ULONG32 ClassToken;  
   ULONG32 FilterOffset;  
} CorDebugEHClause;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`Flags`|EH 절의 예외 정보를 설명하는 비트 필드입니다. 자세한 내용은 설명 섹션을 참조하세요.|  
|`TryOffset`|메서드 본문 시작 지점부터 `try` 블록의 오프셋(바이트)입니다.|  
|`TryLength`|`try` 블록의 길이(바이트)입니다.|  
|`HandlerOffset`|이 `try` 블록의 처리기 위치입니다.|  
|`HandlerLength`|처리기 코드의 크기(바이트)입니다.|  
|`ClassToken`|형식 기반 예외 처리기의 메타데이터 토큰입니다.|  
|`FilterOffset`|필터 기반 예외 처리기에 대한 메서드 본문 시작 지점부터의 오프셋(바이트)입니다.|  
  
## <a name="remarks"></a>설명  
 배열을 `CoreDebugEHClause` 에서 반환 하는 값을 [GetEHClauses](../../../../docs/framework/unmanaged-api/debugging/icordebugilcode-getehclauses-method.md) 메서드.  
  
 EH 절 정보는 CLI 사양을 통해 정의됩니다. 자세한 내용은 참조 하세요. [표준 ECMA-355: Common Language Infrastructure (CLI), 여섯 번째 Edition](https://www.ecma-international.org/publications/standards/Ecma-335.htm)합니다.  
  
 `flags` 필드는 다음 플래그를 포함할 수 있습니다. 이러한 플래그는 CorDebug.idl 또는 CorDebug.h에서 정의되지 않습니다.  
  
|플래그|값|설명|  
|----------|-----------|-----------------|  
|`COR_ILEXCEPTION_CLAUSE_EXCEPTION`|0x00000000|형식이 지정된 예외 절입니다.|  
|`COR_ILEXCEPTION_CLAUSE_FILTER`|0x00000001|예외 필터 및 처리기 절입니다.|  
|`COR_ILEXCEPTION_CLAUSE_FINALLY`|0x00000002|`finally` 절입니다.|  
|`COR_ILEXCEPTION_CLAUSE_FAULT`|0x00000004|fault 절, 즉 예외가 throw될 때만 호출되는 `finally` 절입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [GetEHClauses 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugilcode-getehclauses-method.md)
- [디버깅 구조체](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
