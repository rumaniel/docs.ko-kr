---
title: 스레딩 개체 및 기능
ms.date: 10/01/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], features
- managed threading
ms.assetid: 239b2e8d-581b-4ca3-992b-0e8525b9321c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f25609bc3c4dd829c66a1a4514b7f1121f9c0909
ms.sourcegitcommit: 01ea420eaa4bf76d5fc47673294c8881379b3369
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55759030"
---
# <a name="threading-objects-and-features"></a>스레딩 개체 및 기능

<xref:System.Threading.Thread?displayProperty=nameWithType> 클래스와 함께 .NET 다중 스레드 애플리케이션을 개발하는 데 도움이 되는 여러 클래스를 제공합니다. 다음 문서에서는 해당 클래스의 개요를 제공합니다.

|제목|설명|  
|-----------|-----------------|  
|[관리되는 스레드 풀](the-managed-thread-pool.md)|.NET에서 관리하는 작업자 스레드 풀을 제공하는 <xref:System.Threading.ThreadPool?displayProperty=nameWithType> 클래스를 설명합니다.|  
|[타이머](timers.md)|다중 스레드 환경에서 사용할 수 있는 .NET 타이머에 대해 설명합니다.|
|[동기화 기본 형식 개요](overview-of-synchronization-primitives.md)|공유 리소스에 대한 액세스를 동기화하거나 스레드 상호 작용을 제어하는 데 사용할 수 있는 형식을 설명합니다.|
|[EventWaitHandle](eventwaithandle.md)|스레드 동기화 이벤트를 나타내는 <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType> 클래스를 설명합니다.|
|[CountdownEvent](countdownevent.md)|해당 개수가 0일 때 설정되는 스레드 동기화 이벤트를 나타내는 <xref:System.Threading.CountdownEvent?displayProperty=nameWithType> 클래스를 설명합니다.|
|[뮤텍스](mutexes.md)|공유 리소스에 대한 배타적 액세스 권한을 부여하는 <xref:System.Threading.Mutex?displayProperty=nameWithType> 클래스를 설명합니다.|
|[세마포 및 SemaphoreSlim](semaphore-and-semaphoreslim.md)|공유 리소스 또는 리소스 풀에 동시에 액세스할 수 있는 스레드 수를 제한하는 <xref:System.Threading.Semaphore?displayProperty=nameWithType> 클래스를 설명합니다.|
|[장벽](barrier.md)|단계별 작업에서 스레드를 조정하기 위해 장벽 패턴을 구현하는 <xref:System.Threading.Barrier?displayProperty=nameWithType> 클래스를 설명합니다.|
|[스핀 잠금](spinlock.md)|특정 하위 수준 잠금 시나리오의 <xref:System.Threading.Monitor?displayProperty=nameWithType> 클래스에 대한 간단한 대체 항목인 <xref:System.Threading.SpinLock?displayProperty=nameWithType> 구조체를 설명합니다.|
|[스핀 대기](spinwait.md)|회전 기반 대기를 지원하는 <xref:System.Threading.SpinWait?displayProperty=nameWithType> 구조체를 설명합니다.|

## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.WaitHandle?displayProperty=nameWithType>
- <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- [스레드 및 스레딩 사용](using-threads-and-threading.md)
- [Asynchronous File I/O](../io/asynchronous-file-i-o.md)
- [병렬 프로그래밍](../parallel-programming/index.md)
- [TPL(작업 병렬 라이브러리)](../parallel-programming/task-parallel-library-tpl.md)
