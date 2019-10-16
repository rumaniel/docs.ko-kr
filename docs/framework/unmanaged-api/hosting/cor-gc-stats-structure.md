---
title: COR_GC_STATS 구조체
ms.date: 03/30/2017
api_name:
- COR_GC_STATS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_STATS
helpviewer_keywords:
- COR_GC_STATS structure [.NET Framework hosting]
ms.assetid: 8d4ff73e-739b-40f6-9349-359fbc99c2f9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1085bec812d797d3fbe4ea63ef447d4c466149f2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965051"
---
# <a name="cor_gc_stats-structure"></a>COR_GC_STATS 구조체
CLR (공용 언어 런타임)의 가비지 수집 메커니즘에 대 한 통계를 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct _COR_GC_STATS {  
    ULONG   Flags;   
    SIZE_T  ExplicitGCCount;  
    SIZE_T  GenCollectionsTaken[3];  
    SIZE_T  CommittedKBytes;   
    SIZE_T  ReservedKBytes;  
    SIZE_T  Gen0HeapSizeKBytes;  
    SIZE_T  Gen1HeapSizeKBytes;  
    SIZE_T  Gen2HeapSizeKBytes;  
    SIZE_T  LargeObjectHeapSizeKBytes;  
    SIZE_T  KBytesPromotedFromGen0;  
    SIZE_T  KBytesPromotedFromGen1;  
} COR_GC_STATS;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`Flags`|계산 되 고 반환 되어야 하는 필드 값을 나타냅니다.|  
|`ExplicitGCCount`|외부 요청에 의해 강제 적용 된 가비지 수집 수를 나타냅니다.|  
|`GenCollectionsTaken`|각 세대에 대해 수행 되는 가비지 컬렉션 수를 나타냅니다.|  
|`CommittedKBytes`|모든 힙에서 커밋된 총 kb 수입니다.|  
|`ReservedKBytes`|모든 힙에서 예약 된 총 kb 수입니다.|  
|`Gen0HeapSizeKBytes`|0 세대 힙의 크기 (kb)입니다.|  
|`Gen1HeapSizeKBytes`|1 세대 힙의 크기 (kb)입니다.|  
|`Gen2HeapSizeKBytes`|2 세대 힙의 크기 (kb)입니다.|  
|`LargeObjectHeapSizeKBytes`|큰 개체 힙의 크기 (kb)입니다.|  
|`KBytesPromotedFromGen0`|0 세대에서 1 세대로 수준이 올려진 개체의 크기 (kb)입니다.|  
|`KBytesPromotedFromGen1`|1 세대에서 2 세대로 수준이 올려진 개체의 크기 (kb)입니다.|  
  
## <a name="remarks"></a>설명  
 [ICLRGCManager:: getstats](../../../../docs/framework/unmanaged-api/hosting/iclrgcmanager-getstats-method.md) 메서드를 사용 하려면 `Flags` `COR_GC_STATS` 구조체의 필드를 [COR_GC_STAT_TYPES](../../../../docs/framework/unmanaged-api/hosting/cor-gc-stat-types-enumeration.md) 열거형의 하나 이상의 값으로 설정 하 여 설정할 통계를 지정 해야 합니다.  
  
 다음 표에서는이 구조체에 의해 제공 되는 통계를 두 [COR_GC_STAT_TYPES](../../../../docs/framework/unmanaged-api/hosting/cor-gc-stat-types-enumeration.md) 열거형 값 `COR_GC_COUNTS` `COR_GC_MEMORYUSAGE`에 매핑합니다.  
  
|COR_GC_COUNTS에서 지정|COR_GC_MEMORYUSAGE에서 지정|  
|----------------------------------|---------------------------------------|  
|`ExplicitGCCount`<br /><br /> `GenCollectionsTaken`|`CommittedKBytes`<br /><br /> `ReservedKBytes`<br /><br /> `Gen0HeapSizeKBytes`<br /><br /> `Gen1HeapSizeKBytes`<br /><br /> `Gen2HeapSizeKBytes`<br /><br /> `LargeObjectHeapSizeKBytes`<br /><br /> `KBytesPromotedFromGen0`<br /><br /> `KBytesPromotedFromGen1`|  
  
 사용 예는 다음과 같습니다.  
  
```cpp  
COR_GC_STATS GCStats;  
GCStats.Flags = COR_GC_COUNTS | COR_GC_MEMORYUSAGE;  
pCLRGCManager->GetStats(&GCStats);  
```  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** GCHost.idl  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 구조체](../../../../docs/framework/unmanaged-api/hosting/hosting-structures.md)
- [자동 메모리 관리](../../../standard/automatic-memory-management.md)
- [가비지 수집](../../../standard/garbage-collection/index.md)
