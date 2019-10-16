---
title: COR_PRF_GC_GENERATION 열거형
ms.date: 03/30/2017
api_name:
- COR_PRF_GC_GENERATION
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_GC_GENERATION
helpviewer_keywords:
- COR_GC_GENERATION_FLAGS enumeration [.NET Framework profiling]
ms.assetid: d6ece160-26ad-4d39-abd7-05acd6f78c48
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 74e70f58600205d44a9ba052981b2cc67b3a44ec
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67753813"
---
# <a name="corprfgcgeneration-enumeration"></a>COR_PRF_GC_GENERATION 열거형
가비지 수집 세대를 식별합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    COR_PRF_GC_GEN_0 = 0,  
    COR_PRF_GC_GEN_1 = 1,  
    COR_PRF_GC_GEN_2 = 2,  
    COR_PRF_GC_LARGE_OBJECT_HEAP = 3  
} COR_PRF_GC_GENERATION;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`COR_PRF_GC_GEN_0`|개체는 세대 0으로 저장 됩니다.|  
|`COR_PRF_GC_GEN_1`|개체는 1 세대도 저장 됩니다.|  
|`COR_PRF_GC_GEN_2`|개체는 2 세대도 저장 됩니다.|  
|`COR_PRF_GC_LARGE_OBJECT_HEAP`|개체는 대형 개체 힙에 저장 됩니다.|  
  
## <a name="remarks"></a>설명  
 가비지 수집기 기준 세대를 나눠 개체에서 메모리 관리 성능을 향상 시킵니다. 가비지 수집기는 현재 세 가지 세대와 0, 1, 2 및 큰 개체에 사용 되는 특수 힙 세그먼트를 번호 매기기를 사용 합니다. 특정 값 보다 큰 개체는 대형 개체 힙에 저장 됩니다. 0 세대에 속하는 다른 할당 된 개체를 시작 합니다. 가비지 컬렉션이 0 세대에서 발생 한 후에 있는 모든 개체는 1 세대로 승격 됩니다. 1 세대에서 가비지 수집이 수행 된 후 존재 하는 개체 세대 2로 이동 합니다.  
  
 사용 세대의 가비지 수집기는 한 번에 할당 된 개체의 하위 집합만 사용 하는 것을 의미 합니다.  
  
 합니다 `COR_PRF_GC_GENERATION` 열거형에서 사용 되는 [COR_PRF_GC_GENERATION_RANGE](../../../../docs/framework/unmanaged-api/profiling/cor-prf-gc-generation-range-structure.md) 구조입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 열거형](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
