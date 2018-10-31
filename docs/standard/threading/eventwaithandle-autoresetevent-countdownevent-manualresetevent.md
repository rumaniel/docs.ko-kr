---
title: EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent
ms.date: 09/14/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- wait handles
- threading [.NET Framework], EventWaitHandle class
- event wait handles [.NET Framework]
ms.assetid: cd94fc34-ac15-427f-b723-a1240a4fab7d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: be9c858d7c76fdcc1b3e02485eb0b459f4e7555c
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48583154"
---
# <a name="eventwaithandle-autoresetevent-countdownevent-manualresetevent"></a>EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent

이벤트 대기 핸들을 통해 스레드가 서로 신호를 보내고 상대방의 신호를 대기하여 작업을 동기화할 수 있습니다. 이러한 동기화 이벤트는 운영 체제 대기 핸들을 기반으로 하며, 신호를 보낼 때 자동으로 다시 설정되는 이벤트 및 수동으로 다시 설정되는 이벤트라는 두 가지 유형으로 나눌 수 있습니다.  
  
이벤트 대기 핸들은 <xref:System.Threading.Monitor> 클래스와 동일한 여러 동기화 시나리오에서 유용합니다. 이벤트 대기 핸들은 대개 <xref:System.Threading.Monitor.Wait%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Monitor.Pulse%2A?displayProperty=nameWithType> 메서드보다 사용하기가 더 쉬우며 신호 보내기에 대해 더 많은 제어를 제공합니다. 명명된 이벤트 대기 핸들은 응용 프로그램 도메인 및 프로세스에 작업을 동기화하는 데 사용할 수 있습니다. 이 때 모니터는 응용 프로그램 도메인에 대해 로컬입니다.  
  
## <a name="in-this-section"></a>단원 내용

 [EventWaitHandle](eventwaithandle.md)  
 <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType> 클래스는 자동 또는 수동 재설정 이벤트를 나타내거나 로컬 이벤트 또는 명명된 시스템 이벤트를 나타낼 수 있습니다.  
  
 [AutoResetEvent](autoresetevent.md)  
 <xref:System.Threading.AutoResetEvent?displayProperty=nameWithType> 클래스는 <xref:System.Threading.EventWaitHandle>에서 파생되며 자동으로 다시 설정되는 로컬 이벤트를 나타냅니다.  
  
 [ManualResetEvent 및 ManualResetEventSlim](manualresetevent-and-manualreseteventslim.md)  
 <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> 클래스는 <xref:System.Threading.EventWaitHandle>에서 파생되며 수동으로 다시 설정해야 하는 로컬 이벤트를 나타냅니다. <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType> 클래스는 동일한 프로세스 내의 이벤트에 사용할 수 있는 간단하고 빠른 버전입니다.  
  
 [CountdownEvent](countdownevent.md)  
 <xref:System.Threading.CountdownEvent?displayProperty=nameWithType> 클래스는 대기 핸들을 사용하는 코드에서 포크/조인 병렬 처리 패턴을 구현하는 간단한 방법을 제공합니다.  

## <a name="see-also"></a>참고 항목

- <xref:System.Threading.WaitHandle?displayProperty=nameWithType>
- <xref:System.Threading.Barrier?displayProperty=nameWithType>
- [스레딩 개체 및 기능](threading-objects-and-features.md)
- [관리되는 스레딩 기본 사항](managed-threading-basics.md)
