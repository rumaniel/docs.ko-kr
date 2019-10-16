---
title: 스레드 풀 ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- thread pool events [.NET Framework]
- ETW, thread pool events (CLR)
ms.assetid: f2a21e3a-3b6c-4433-97f3-47ff16855ecc
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9a96fd4c45113afd2ab918b714bd6e12a429917c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046183"
---
# <a name="thread-pool-etw-events"></a>스레드 풀 ETW 이벤트
<a name="top"></a> 이러한 이벤트는 작업자 스레드 및 I/O 스레드에 대한 정보를 수집합니다.  
  
 스레드 풀 이벤트에는 다음과 같은 두 그룹이 있습니다.  
  
- [작업자 스레드 풀 이벤트](#worker). 이러한 스레드 풀 이벤트는 응용 프로그램에서 스레드 풀을 사용하는 방식에 대한 정보 및 작업 부하가 동시성 제어에 미치는 영향에 대한 정보를 제공합니다.  
  
- [I/O 스레드 풀 이벤트](#io). 이러한 스레드 풀 이벤트는 스레드 풀에서 생성되거나, 만료되거나, 만료되지 않거나, 종료된 I/O 스레드에 대한 정보를 제공합니다.  
  
<a name="worker"></a>   
## <a name="worker-thread-pool-events"></a>작업자 스레드 풀 이벤트  
 이러한 이벤트는 런타임의 작업자 스레드 풀과 관련이 있으며, 스레드 이벤트에 대한 알림을 제공합니다(예: 스레드가 만들어지거나 중지될 때). 작업자 스레드 풀은 동시성 제어를 위해 측정된 처리량을 기준으로 스레드 수가 계산되는 자동 선택 알고리즘을 사용합니다. 작업자 스레드 풀 이벤트는 애플리케이션이 스레드 풀을 사용하는 방법 그리고 특정 작업 부하가 동시성 제어에 미칠 수 있는 영향을 이해하는 데 사용할 수 있습니다.  
  
### <a name="threadpoolworkerthreadstart-and-threadpoolworkerthreadstop"></a>ThreadPoolWorkerThreadStart 및 ThreadPoolWorkerThreadStop  
 다음 표에서는 이러한 이벤트의 키워드 및 수준을 보여 줍니다. 자세한 내용은 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)을 참조하세요.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`ThreadingKeyword` (0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-|-|-|  
|`ThreadPoolWorkerThreadStart`|50|작업자 스레드가 생성됩니다.|  
|`ThreadPoolWorkerThreadStop`|51|작업자 스레드가 중지됩니다.|  
|`ThreadPoolWorkerThreadRetirementStart`|52|작업자 스레드가 만료됩니다.|  
|`ThreadPoolWorkerThreadRetirementStop`|53|만료된 작업자 스레드가 다시 활성 상태가 됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|ActiveWorkerThreadCount|win:UInt32|이미 작업을 처리하고 있는 작업자 스레드를 포함하여 작업을 처리할 수 있는 작업자 스레드의 개수입니다.|  
|RetiredWorkerThreadCount|win:UInt32|작업을 처리할 수 없지만, 나중에 더 많은 스레드가 필요할 때를 대비하여 유지하고 있는 작업자 스레드의 개수입니다.|  
|ClrInstanceID|Win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
### <a name="threadpoolworkerthreadadjustment"></a>ThreadPoolWorkerThreadAdjustment  
 이러한 스레드 풀 이벤트는 스레드 삽입(동시성 제어) 알고리즘의 동작을 이해하고 디버깅하기 위한 정보를 제공합니다. 이 정보는 작업자 스레드 풀에서 내부적으로 사용합니다.  
  
#### <a name="threadpoolworkerthreadadjustmentsample"></a>ThreadPoolWorkerThreadAdjustmentSample  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`ThreadingKeyword` (0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|설명|  
|-----------|--------------|-----------------|  
|`ThreadPoolWorkerThreadAdjustmentSample`|54|한 샘플의 정보 컬렉션을 나타냅니다. 즉, 특정 시점에 특정 동시성 수준으로 처리량을 측정한 것입니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|처리량|win:Double|시간 단위당 완료 수입니다.|  
|ClrInstanceID|Win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
#### <a name="threadpoolworkerthreadadjustmentadjustment"></a>ThreadPoolWorkerThreadAdjustmentAdjustment  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`ThreadingKeyword` (0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|설명|  
|-----------|--------------|-----------------|  
|`ThreadPoolWorkerThreadAdjustmentAdjustment`|55|스레드 삽입(언덕 오르기) 알고리즘이 동시성 수준에서 변화를 감지할 때 제어의 변경을 기록합니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|AverageThroughput|win:Double|측정 샘플의 평균 처리량입니다.|  
|NewWorkerThreadCount|win:UInt32|새로운 활성 작업자 스레드의 수입니다.|  
|이유|win:UInt32|조정의 원인입니다.<br /><br /> 0x00 - 준비<br /><br /> 0x01 - 초기화 중<br /><br /> 0x02 - 무작위 이동<br /><br /> 0x03 - 오르기 이동<br /><br /> 0x04 - 포인트 변경<br /><br /> 0x05 - 안정화 중<br /><br /> 0x06 - 고갈<br /><br /> 0x07 - 스레드 시간 초과|  
|ClrInstanceID|Win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
#### <a name="threadpoolworkerthreadadjustmentstats"></a>ThreadPoolWorkerThreadAdjustmentStats  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`ThreadingKeyword` (0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|설명|  
|-----------|--------------|-----------------|  
|`ThreadPoolWorkerThreadAdjustmentStats`|56|스레드 풀의 데이터를 수집합니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|기간|win:Double|이러한 통계가 수집된 시간(초)입니다.|  
|처리량|win:Double|이 간격 동안의 초당 평균 완료 수입니다.|  
|ThreadWave|win:Double|내부용으로 예약됩니다.|  
|ThroughputWave|win:Double|내부용으로 예약됩니다.|  
|ThroughputErrorEstimate|win:Double|내부용으로 예약됩니다.|  
|AverageThroughputErrorEstimate|win:Double|내부용으로 예약됩니다.|  
|ThroughputRatio|win:Double|이 간격 동안 활성 작업자 스레드 수의 변화로 인해 발생한 처리량의 상대적인 증가량입니다.|  
|Confidence|win:Double|ThroughputRatio 필드의 유효성 측정값입니다.|  
|NewcontrolSetting|win:Double|활성 스레드 개수에서 미래의 변동에 대한 기준으로 사용될 활성 작업자 스레드 수입니다.|  
|NewThreadWaveMagnitude|Win:UInt16|활성 스레드 개수에서 미래 변동의 크기입니다.|  
|ClrInstanceID|Win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="io"></a>   
## <a name="io-thread-events"></a>I/O 스레드 이벤트  
 이러한 스레드 풀 이벤트는 비동기적인 I/O 스레드 풀(완료 포트)에서 스레드에 대해 발생합니다.  
  
### <a name="iothreadcreate_v1"></a>IOThreadCreate_V1  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`ThreadingKeyword` (0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-|-|-|  
|`IOThreadCreate_V1`|44|스레드 풀에서 I/O 스레드가 생성됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|개수|win:UInt64|새로 생성된 스레드를 포함한 I/O 스레드의 수입니다.|  
|NumRetired|win:UInt64|만료된 작업자 스레드의 수입니다.|  
|ClrInstanceID|Win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
### <a name="iothreadretire_v1"></a>IOThreadRetire_V1  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`ThreadingKeyword` (0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`IOThreadRetire_V1`|46|I/O 스레드가 만료 후보가 됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|개수|win:UInt64|스레드 풀에 남아 있는 I/O 스레드의 수입니다.|  
|NumRetired|win:UInt64|만료된 I/O 스레드의 수입니다.|  
|ClrInstanceID|Win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
### <a name="iothreadunretire_v1"></a>IOThreadUnretire_V1  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`ThreadingKeyword` (0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`IOThreadUnretire_V1`|47|스레드가 만료 후보가 된 후 대기 기간 내에 도착하는 I/O 때문에 I/O 스레드가 만료 취소됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|개수|win:UInt64|이 스레드를 포함하여 스레드 풀에 있는 I/O 스레드의 수입니다.|  
|NumRetired|win:UInt64|만료된 I/O 스레드의 수입니다.|  
|ClrInstanceID|Win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
### <a name="iothreadterminate"></a>IOThreadTerminate  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`ThreadingKeyword` (0x10000)|정보(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`IOThreadTerminate`|45|스레드 풀에서 I/O 스레드가 생성됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|개수|win:UInt64|스레드 풀에 남아 있는 I/O 스레드의 수입니다.|  
|NumRetired|win:UInt64|만료된 I/O 스레드의 수입니다.|  
|ClrInstanceID|Win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
## <a name="see-also"></a>참고자료

- [CLR ETW 이벤트](clr-etw-events.md)
