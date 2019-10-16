---
title: COR_SEGMENT 구조체
ms.date: 03/30/2017
api_name:
- COR_SEGMENT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_SEGMENT
helpviewer_keywords:
- COR_SEGMENT structure [.NET Framework debugging]
ms.assetid: 93aeecb9-7fef-4545-8daf-f566dfc47084
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: aabf3ac4e51280bd847d145e15ad804d514ede2c
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274003"
---
# <a name="cor_segment-structure"></a>COR_SEGMENT 구조체
관리되는 힙의 메모리 영역에 대한 정보를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct _COR_SEGMENT {  
    CORDB_ADDRESS start;            
    CORDB_ADDRESS end;              
    CorDebugGenerationTypes gen;    
    ULONG heap;                     
} COR_SEGMENT;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`start`|메모리 영역의 시작 주소입니다.|  
|`end`|메모리 영역의 끝 주소입니다.|  
|`gen`|메모리 영역의 생성을 나타내는 [CorDebugGenerationTypes](cordebuggenerationtypes-enumeration.md) 열거형 멤버입니다.|  
|`heap`|메모리 영역이 있는 힙 번호입니다. 자세한 내용은 설명 부분을 참조하세요.|  
  
## <a name="remarks"></a>설명  
 `COR_SEGMENTS` 구조는 관리되는 힙의 메모리 영역을 나타냅니다.  `COR_SEGMENTS` 개체는 [ICorDebugHeapRegionEnum](icordebugheapsegmentenum-interface.md) 컬렉션 개체의 멤버이며, [ICorDebugProcess5::EnumerateHeapRegions](icordebugprocess5-enumerateheapregions-method.md) 메서드를 호출하여 채웁니다.  
  
 `heap` 필드는 보고되는 힙에 해당하는 프로세서 번호입니다. 워크스테이션 가비지 수집기의 경우 워크스테이션에 가비지 수집 힙이 하나만 있으므로, 해당 값은 항상 0입니다. 서버 가비지 수집기의 값은 힙이 연결된 프로세서에 해당합니다. 가비지 수집기의 구현 세부 정보로 인해 실제 프로세서보다 가비지 수집 힙이 더 많거나 적을 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [디버깅 구조체](debugging-structures.md)
- [디버깅](index.md)
