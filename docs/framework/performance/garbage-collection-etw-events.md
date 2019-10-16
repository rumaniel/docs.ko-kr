---
title: 가비지 컬렉션 ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- GC events
- garbage collection events [.NET Framework]
- ETW, garbage collection events (CLR)
ms.assetid: f14b6fd7-0966-4d87-bc89-54ef3a44a94a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ec90d022a0c72782f413a84b6fbd2c1b8d663a73
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046502"
---
# <a name="garbage-collection-etw-events"></a>가비지 컬렉션 ETW 이벤트
<a name="top"></a> 이들 이벤트는 가비지 수집과 관련된 정보를 수집합니다. 가비지 수집 수행 횟수, 가비지 수집 중에 해제된 메모리 양 등을 판별하는 작업을 포함하여 진단과 디버깅에 도움이 됩니다.  
  
 이 범주는 다음 이벤트로 구성됩니다.  
  
- [GCStart_V1 Event](#gcstart_v1_event)  
  
- [GCEnd_V1 Event](#gcend_v1_event)  
  
- [GCHeapStats_V1 Event](#gcheapstats_v1_event)  
  
- [GCCreateSegment_V1 Event](#gccreatesegment_v1_event)  
  
- [GCFreeSegment_V1 Event](#gcfreesegment_v1_event)  
  
- [GCRestartEEBegin_V1 Event](#gcrestarteebegin_v1_event)  
  
- [GCRestartEEEnd_V1 Event](#gcrestarteeend_v1_event)  
  
- [GCSuspendEE_V1 Event](#gcsuspendee_v1_event)  
  
- [GCSuspendEEEnd_V1 Event](#gcsuspendeeend_v1_event)  
  
- [GCAllocationTick_V2 Event](#gcallocationtick_v2_event)  
  
- [GCFinalizersBegin_V1 Event](#gcfinalizersbegin_v1_event)  
  
- [GCFinalizersEnd_V1 Event](#gcfinalizersend_v1_event)  
  
- [GCCreateConcurrentThread_V1 Event](#gccreateconcurrentthread_v1_event)  
  
- [GCTerminateConcurrentThread_V1 Event](#gcterminateconcurrentthread_v1_event)  
  
<a name="gcstart_v1_event"></a>   
## <a name="gcstart_v1-event"></a>GCStart_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다. 자세한 내용은 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)을 참조하세요.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCStart_V1`|1|가비지 수집이 시작되었습니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|개수|win:UInt32|*n*번째 가비지 수집입니다.|  
|깊이|win:UInt32|수집되고 있는 세대입니다.|  
|이유|win:UInt32|가비지 수집이 트리거된 이유입니다.<br /><br /> 0x0 - 작은 개체 힙 할당.<br /><br /> 0x1 - 발생됨.<br /><br /> 0x2 - 메모리 부족.<br /><br /> 0x3 - 비어 있음.<br /><br /> 0x4 - 큰 개체 힙 할당.<br /><br /> 0x5 - 공간 부족(작은 개체 힙용).<br /><br /> 0x6 - 공간 부족(큰 개체 힙용).<br /><br /> 0x7 - 발생하지만 차단으로 강제 적용되지 않음.|  
|형식|win:UInt32|0x0 - 가비지 수집 차단이 백그라운드 가비지 수집 외부에서 발생함.<br /><br /> 0x1 - 백그라운드 가비지 수집.<br /><br /> 0x2 - 가비지 수집 차단이 백그라운드 가비지 수집 중에 발생함.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="gcend_v1_event"></a>   
## <a name="gcend_v1-event"></a>GCEnd_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCEnd_V1`|2|가비지 수집이 종료되었습니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|개수|win:UInt32|*n*번째 가비지 수집입니다.|  
|깊이|win:UInt32|수집된 세대입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="gcheapstats_v1_event"></a>   
## <a name="gcheapstats_v1-event"></a>GCHeapStats_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|설명|  
|-----------|--------------|-----------------|  
|`GCHeapStats_V1`|4|각 가비지 수집 종료 시 힙 통계를 표시합니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|GenerationSize0|win:UInt64|0세대 메모리의 크기(바이트)입니다.|  
|TotalPromotedSize0|win:UInt64|0세대에서 1세대로 수준이 올려진 바이트 수입니다.|  
|GenerationSize1|win:UInt64|1세대 메모리의 크기(바이트)입니다.|  
|TotalPromotedSize1|win:UInt64|1세대에서 2세대로 수준이 올려진 바이트 수입니다.|  
|GenerationSize2|win:UInt64|2세대 메모리의 크기(바이트)입니다.|  
|TotalPromotedSize2|win:UInt64|마지막 수집 후에 2세대에 남아 있는 바이트 수입니다.|  
|GenerationSize3|win:UInt64|큰 개체 힙의 크기(바이트)입니다.|  
|TotalPromotedSize3|win:UInt64|마지막 수집 후에 큰 개체 힙에 남아 있는 바이트 수입니다.|  
|FinalizationPromotedSize|win:UInt64|종료 준비가 된 개체의 전체 크기(바이트)입니다.|  
|FinalizationPromotedCount|win:UInt64|종료 준비가 된 개체 수입니다.|  
|PinnedObjectCount|win:UInt32|고정된(제거할 수 없는) 개체 수입니다.|  
|SinkBlockCount|win:UInt32|사용 중인 동기화 블록 수입니다.|  
|GCHandleCount|win:UInt32|사용 중인 가비지 수집 핸들 수입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="gccreatesegment_v1_event"></a>   
## <a name="gccreatesegment_v1-event"></a>GCCreateSegment_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCCreateSegment_V1`|5|새 가비지 수집 세그먼트가 만들어졌습니다. 또한 이미 실행 중인 프로세스에서 추적 기능이 사용되면 각 기존 세그먼트에 대해 이 이벤트가 발생합니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|주소|win:UInt64|세그먼트 주소입니다.|  
|크기|win:UInt64|세그먼트 크기입니다.|  
|형식|win:UInt32|0x0 - 작은 개체 힙.<br /><br /> 0x1 - 큰 개체 힙<br /><br /> 0x2 - 읽기 전용 힙.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 가비지 수집기에서 할당되는 세그먼트 크기는 구현에 따라 다르며 정기적인 업데이트를 포함하여 언제든지 변경될 수 있습니다. 앱에서 특정 세그먼트 크기를 가정하거나 의존해서는 안 되며, 세그먼트 할당에 사용할 수 있는 메모리 크기를 구성하려고 해서도 안 됩니다.  
  
 [맨 위로 이동](#top)  
  
<a name="gcfreesegment_v1_event"></a>   
## <a name="gcfreesegment_v1-event"></a>GCFreeSegment_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCFreeSegment_V1`|6|가비지 수집 세그먼트가 해제되었습니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|주소|win:UInt64|세그먼트 주소입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="gcrestarteebegin_v1_event"></a>   
## <a name="gcrestarteebegin_v1-event"></a>GCRestartEEBegin_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCRestartEEBegin_V1`|7|공용 언어 런타임 일시 중단에서 다시 시작이 시작되었습니다.|  
  
 이벤트 데이터가 없습니다.  
  
 [맨 위로 이동](#top)  
  
<a name="gcrestarteeend_v1_event"></a>   
## <a name="gcrestarteeend_v1-event"></a>GCRestartEEEnd_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCRestartEEEnd_V1`|3|공용 언어 런타임 일시 중단에서 다시 시작이 종료되었습니다.|  
  
 이벤트 데이터가 없습니다.  
  
 [맨 위로 이동](#top)  
  
<a name="gcsuspendee_v1_event"></a>   
## <a name="gcsuspendee_v1-event"></a>GCSuspendEE_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCSuspendEE_V1`|10|가비지 수집에 대한 실행 엔진의 일시 중단이 시작됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|이유|win:UInt16|0x0 - 기타.<br /><br /> 0x1 - 가비지 수집.<br /><br /> 0x2 - 애플리케이션 도메인 중지.<br /><br /> 0x3 - 코드 피칭.<br /><br /> 0x4 - 종료.<br /><br /> 0x5 - 디버거.<br /><br /> 0x6 - 가비지 수집 준비.|  
|개수|win:UInt32|해당 시점의 GC 개수입니다. 일반적으로 이 이벤트 뒤에 후속 GC 시작 이벤트가 확인되고 가비지 수집 중에 GC 인덱스를 늘리면 해당 개수는 이 개수 + 1이 됩니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="gcsuspendeeend_v1_event"></a>   
## <a name="gcsuspendeeend_v1-event"></a>GCSuspendEEEnd_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCSuspendEEEnd_V1`|8|가비지 수집에 대한 실행 엔진의 일시 중단이 종료됩니다.|  
  
 이벤트 데이터가 없습니다.  
  
 [맨 위로 이동](#top)  
  
<a name="gcallocationtick_v2_event"></a>   
## <a name="gcallocationtick_v2-event"></a>GCAllocationTick_V2 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCAllocationTick_V2`|10|매번 100KB 정도가 할당됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|AllocationAmount|win:UInt32|할당 크기(바이트)입니다. 이 값은 ULONG 길이(4,294,967,295바이트)보다 적은 할당에 대해 정확합니다. 할당이 더 크면 이 필드에 잘린 값이 포함됩니다. 매우 큰 할당에 대해서는 `AllocationAmount64` 를 사용하세요.|  
|AllocationKind|win:UInt32|0x0 - 작은 개체 할당(할당이 작은 개체 힙에 포함됨).<br /><br /> 0x1 - 큰 개체 할당(할당이 큰 개체 힙에 포함됨).|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
|AllocationAmount64|win:UInt64|할당 크기(바이트)입니다. 이 값은 매우 큰 할당에 대해 정확합니다.|  
|TypeId|win:Pointer|MethodTable 주소입니다. 이 이벤트 중에 여러 가지 개체 형식이 할당되었으면 이 항목은 할당된 마지막 개체(100KB 임계값을 초과한 개체)에 해당하는 MethodTable의 주소입니다.|  
|TypeName|win:UnicodeString|할당된 형식 이름입니다. 이 이벤트 중에 여러 가지 개체 형식이 할당되었으면 이 항목은 할당된 마지막 개체(100KB 임계값을 초과한 개체)의 형식입니다.|  
|HeapIndex|win:UInt32|개체가 할당된 힙입니다. 워크스테이션 가비지 수집에서 실행될 때 이 값은 0(영)입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="gcfinalizersbegin_v1_event"></a>   
## <a name="gcfinalizersbegin_v1-event"></a>GCFinalizersBegin_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCFinalizersBegin_V1`|14|종료자 실행이 시작됩니다.|  
  
 이벤트 데이터가 없습니다.  
  
 [맨 위로 이동](#top)  
  
<a name="gcfinalizersend_v1_event"></a>   
## <a name="gcfinalizersend_v1-event"></a>GCFinalizersEnd_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCFinalizersEnd_V1`|13|종료자 실행이 종료됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|개수|win:UInt32|실행된 종료자 수입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="gccreateconcurrentthread_v1_event"></a>   
## <a name="gccreateconcurrentthread_v1-event"></a>GCCreateConcurrentThread_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
|`ThreadingKeyword`(0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCCreateConcurrentThread_V1`|11|동시 가비지 수집 스레드가 만들어졌습니다.|  
  
 이벤트 데이터가 없습니다.  
  
 [맨 위로 이동](#top)  
  
<a name="gcterminateconcurrentthread_v1_event"></a>   
## <a name="gcterminateconcurrentthread_v1-event"></a>GCTerminateConcurrentThread_V1 Event  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|정보(4)|  
|`ThreadingKeyword`(0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`GCTerminateConcurrentThread_V1`|12|동시 가비지 수집 스레드가 종료되었습니다.|  
  
 이벤트 데이터가 없습니다.  
  
## <a name="see-also"></a>참고자료

- [CLR ETW 이벤트](clr-etw-events.md)
