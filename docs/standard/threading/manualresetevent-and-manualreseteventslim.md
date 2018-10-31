---
title: ManualResetEvent 및 ManualResetEventSlim
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], ManualResetEvent class
- ManualResetEvent class, about ManualResetEvent class
ms.assetid: 465fdcf9-ba24-4d8d-a43f-d983b7cb0cc6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c85d0c5c291743c6daac549e15d479fcf332235c
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49452825"
---
# <a name="manualresetevent-and-manualreseteventslim"></a>ManualResetEvent 및 ManualResetEventSlim
<xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> 클래스는 신호를 받은 후 수동으로 다시 설정해야 하는 로컬 대기 핸들 이벤트를 나타냅니다. 이 클래스는 기본 클래스인 <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType>의 특수한 경우를 나타냅니다. 수동 재설정 이벤트의 사용 및 기능은 [EventWaitHandle](../../../docs/standard/threading/eventwaithandle.md) 개념 설명서를 참조하세요.  
  
 <xref:System.Threading.ManualResetEvent> 개체는 <xref:System.Threading.EventWaitHandle.Reset%2A?displayProperty=nameWithType> 메서드가 호출될 때까지 신호를 받은 것으로 유지합니다. 대기 스레드 또는 신호를 받은 후 이벤트를 기다리는 스레드 수는 제한 없이 개체의 상태가 신호를 받는 동안 해제될 수 있습니다.
  
 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]에서는 대기 시간이 매우 짧을 것으로 예상되고 이벤트가 프로세스 경계를 넘어서지 않는 경우 <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType> 클래스를 사용하여 성능을 향상시킬 수 있습니다. <xref:System.Threading.ManualResetEventSlim>에서는 이벤트에 신호가 전달되기를 기다리는 짧은 시간 동안 고속 회전을 사용합니다. 대기 시간이 짧은 경우 대기 핸들을 사용하여 기다리는 것보다 회전하는 것이 비용이 적게 들 수 있습니다. 그러나 이벤트가 특정 기간 내에 신호를 받지 않는 경우 일반적인 이벤트 핸들 대기에 <xref:System.Threading.ManualResetEventSlim>을 사용합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.WaitHandle?displayProperty=nameWithType>
- [AutoResetEvent](autoresetevent.md)  
- [스핀 대기](spinwait.md)  
- [세마포 및 SemaphoreSlim](semaphore-and-semaphoreslim.md)
- [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)  
- [스레딩 개체 및 기능](threading-objects-and-features.md)  
- [스레딩](index.md)  
