---
title: 동기화 기본 형식 개요
description: 공유 리소스에 대한 액세스를 동기화하거나 스레드 상호 작용을 제어하는 데 사용되는 .NET 스레드 동기화 기본 형식 알아보기
ms.date: 10/01/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- synchronization, threads
- threading [.NET],synchronizing threads
- managed threading
ms.assetid: b782bcb8-da6a-4c6a-805f-2eb46d504309
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 31d5df6521b7c420943a7d3d0efcf6e4bee2d3a2
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666286"
---
# <a name="overview-of-synchronization-primitives"></a>동기화 기본 형식 개요

.NET은 공유 리소스에 대한 액세스를 동기화하거나 스레드 상호 작용을 조정하는 데 사용할 수 있는 다양한 형식을 제공합니다.

> [!IMPORTANT]
> 동일한 동기화 기본 형식 인스턴스를 사용하여 공유 리소스에 대한 액세스를 보호합니다. 다른 동기화 기본 형식 인스턴스를 사용하여 동일한 리소스를 보호하는 경우 동기화 기본 형식에서 제공하는 보호를 사용할 수 없게 됩니다.

## <a name="waithandle-class-and-lightweight-synchronization-types"></a>WaitHandle 클래스 및 간단한 동기화 형식

여러 .NET 동기화 기본 형식이 <xref:System.Threading.WaitHandle?displayProperty=nameWithType> 클래스에서 파생됩니다. 이 클래스는 네이티브 운영 체제 동기화 핸들을 캡슐화하고 스레드 상호 작용의 신호 메커니즘을 사용합니다. 해당 클래스에는 다음이 포함됩니다.

- <xref:System.Threading.Mutex?displayProperty=nameWithType> - 공유 리소스에 대한 배타적 액세스 권한을 부여합니다. 뮤텍스의 상태는 스레드가 소유하지 않는 경우 신호를 받습니다.
- <xref:System.Threading.Semaphore?displayProperty=nameWithType> - 공유 리소스 또는 리소스 풀에 동시에 액세스할 수 있는 스레드 수를 제한합니다. 세마포 상태는 해당 개수가 0보다 크면 신호 알림으로 설정되고 해당 개수가 0이면 신호 알림 해제로 설정됩니다.
- <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType> - 스레드 동기화 이벤트를 나타내고 신호 알림 또는 신호 알림 해제 상태일 수 있습니다.
- <xref:System.Threading.AutoResetEvent?displayProperty=nameWithType> - <xref:System.Threading.EventWaitHandle>에서 파생되고 신호 알림을 받으면 단일 대기 스레드를 해제한 후 자동으로 신호 알림 해제 상태로 다시 설정됩니다.
- <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> - <xref:System.Threading.EventWaitHandle>에서 파생되고 신호 알림을 받을 경우 <xref:System.Threading.EventWaitHandle.Reset%2A> 메서드가 호출될 때까지 신호 알림 상태를 유지합니다.

.NET Framework에서 <xref:System.Threading.WaitHandle>은 <xref:System.MarshalByRefObject?displayProperty=nameWithType>에서 파생되므로 대기 핸들을 사용하여 애플리케이션 도메인 경계에 걸쳐 스레드 활동을 동기화할 수 있습니다.

.NET Framework 및 .NET Core에서 이러한 형식 중 일부는 운영 체제 전체에 표시되고 프로세스 간 동기화에 사용할 수 있는 명명된 시스템 동기화 핸들을 나타낼 수 있습니다.

- <xref:System.Threading.Mutex>(.NET Framework 및 .NET Core),
- <xref:System.Threading.Semaphore>(Windows의 .NET Framework 및 .NET Core),
- <xref:System.Threading.EventWaitHandle>(Windows의 .NET Framework 및 .NET Core).

자세한 내용은 <xref:System.Threading.WaitHandle> API 참조를 참조하세요.

간단한 동기화 형식은 기본 운영 체제 핸들을 사용하지 않고 일반적으로 향상된 성능을 제공합니다. 그러나 프로세스 간 동기화에는 사용할 수 없습니다. 한 애플리케이션 내에서 이러한 형식의 스레드 동기화를 사용합니다.

이러한 형식 중 일부는 <xref:System.Threading.WaitHandle>에서 파생된 형식의 대체 항목입니다. 예를 들어 <xref:System.Threading.SemaphoreSlim>은 <xref:System.Threading.Semaphore>의 간단한 대체 항목입니다.

## <a name="synchronization-of-access-to-a-shared-resource"></a>공유 리소스에 대한 액세스 동기화

.NET은 여러 스레드가 공유 리소스에 대한 액세스를 제어할 수 있는 다양한 동기화 기본 형식을 제공합니다.

### <a name="monitor-class"></a>Monitor 클래스

<xref:System.Threading.Monitor?displayProperty=nameWithType> 클래스는 리소스를 식별하는 개체에 대한 잠금을 획득하거나 해제하여 공유 리소스에 대한 상호 배타적 액세스 권한을 부여합니다. 잠금이 유지되는 동안 잠금을 보유하는 스레드는 잠금을 다시 획득하고 해제할 수 있습니다. 다른 스레드는 잠금을 획득할 수 없도록 차단되고 <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> 메서드는 잠금이 해제될 때까지 대기합니다. <xref:System.Threading.Monitor.Enter%2A> 메서드는 해제된 잠금을 획득합니다. 또한 <xref:System.Threading.Monitor.TryEnter%2A?displayProperty=nameWithType> 메서드를 사용하여 스레드가 잠금을 획득하려고 시도하는 시간을 지정할 수도 있습니다. <xref:System.Threading.Monitor> 클래스에 스레드 선호도가 있으므로 잠금을 획득한 스레드는 <xref:System.Threading.Monitor.Exit%2A?displayProperty=nameWithType> 메서드를 호출하여 잠금을 해제해야 합니다.

<xref:System.Threading.Monitor.Wait%2A?displayProperty=nameWithType>, <xref:System.Threading.Monitor.Pulse%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Monitor.PulseAll%2A?displayProperty=nameWithType> 메서드를 사용하여 동일한 개체에 대한 잠금을 획득하는 스레드의 상호 작용을 조정할 수 있습니다.

자세한 내용은 <xref:System.Threading.Monitor> API 참조를 참조하세요.

> [!NOTE]
> <xref:System.Threading.Monitor> 클래스를 직접 사용하는 대신 C#의 [lock](../../csharp/language-reference/keywords/lock-statement.md) 문 및 Visual Basic의 [SyncLock](../../visual-basic/language-reference/statements/synclock-statement.md) 문을 사용하여 공유 리소스에 대한 액세스를 동기화합니다. 이러한 문은 획득한 잠금이 항상 해제되도록 <xref:System.Threading.Monitor.Enter%2A> 및 <xref:System.Threading.Monitor.Exit%2A> 메서드와 `try…finally` 블록을 사용하여 구현됩니다.

### <a name="mutex-class"></a>Mutex 클래스

<xref:System.Threading.Monitor>와 같은 <xref:System.Threading.Mutex?displayProperty=nameWithType> 클래스는 공유 리소스에 대한 배타적 액세스 권한을 부여합니다. [Mutex.WaitOne](<xref:System.Threading.WaitHandle.WaitOne%2A?displayProperty=nameWithType>) 메서드 오버로드 중 하나를 사용하여 뮤텍스의 소유권을 요청합니다. <xref:System.Threading.Monitor>와 마찬가지로 <xref:System.Threading.Mutex>에는 스레드 선호도가 있고 뮤텍스를 획득한 스레드는 <xref:System.Threading.Mutex.ReleaseMutex%2A?displayProperty=nameWithType> 메서드를 호출하여 뮤텍스를 해제해야 합니다.

<xref:System.Threading.Monitor>와 달리 <xref:System.Threading.Mutex> 클래스는 프로세스 간 동기화에 사용할 수 있습니다. 이를 수행하려면 운영 체제 전체에 표시되는 명명된 뮤텍스를 사용합니다. 명명된 뮤텍스 인스턴스를 만들려면 이름을 지정하는 [뮤텍스 생성자](<xref:System.Threading.Mutex.%23ctor%2A>)를 사용합니다. <xref:System.Threading.Mutex.OpenExisting%2A?displayProperty=nameWithType> 메서드를 호출하여 기존 명명된 시스템 뮤텍스를 열 수도 있습니다.
  
자세한 내용은 [뮤텍스](mutexes.md) 문서 및 <xref:System.Threading.Mutex> API 참조를 참조하세요.

### <a name="spinlock-structure"></a>SpinLock 구조체

<xref:System.Threading.Monitor>와 같은 <xref:System.Threading.SpinLock?displayProperty=nameWithType> 구조체는 잠금의 가용성에 따라 공유 리소스에 대한 배타적 액세스 권한을 부여합니다. <xref:System.Threading.SpinLock>이 사용할 수 없는 잠금을 획득하려고 하면 잠금을 사용할 수 있을 때까지 루프에서 반복적으로 확인하면서 대기합니다.

회전 잠금을 사용하는 이점 및 결점에 대한 자세한 내용은 [SpinLock](spinlock.md) 문서 및 <xref:System.Threading.SpinLock> API 참조를 참조하세요.

### <a name="readerwriterlockslim-class"></a>ReaderWriterLockSlim 클래스

<xref:System.Threading.ReaderWriterLockSlim?displayProperty=nameWithType> 클래스는 쓰기 위해 공유 리소스에 대한 배타적 액세스 권한을 부여하고, 읽기 위해 여러 스레드가 동시에 리소스에 액세스하도록 허용합니다. <xref:System.Threading.ReaderWriterLockSlim>을 사용하여 스레드로부터 안전한 읽기 작업을 지원하지만 쓰기 작업을 수행할 배타적 액세스 권한이 필요한 공유 데이터 구조에 대한 액세스를 동기화할 수 있습니다. 스레드가 배타적 액세스를 요청하면(예: <xref:System.Threading.ReaderWriterLockSlim.EnterWriteLock%2A?displayProperty=nameWithType> 메서드 호출을 통해) 모든 기존 판독기가 잠금을 종료하고 작성기가 잠금을 시작 및 종료할 때까지 후속 판독기 및 작성기 요청이 차단됩니다.
  
자세한 내용은 <xref:System.Threading.ReaderWriterLockSlim> API 참조를 참조하세요.

### <a name="semaphore-and-semaphoreslim-classes"></a>세마포 및 SemaphoreSlim 클래스

<xref:System.Threading.Semaphore?displayProperty=nameWithType> 및 <xref:System.Threading.SemaphoreSlim?displayProperty=nameWithType> 클래스는 공유 리소스 또는 리소스 풀에 동시에 액세스할 수 있는 스레드 수를 제한합니다. 리소스를 요청하는 추가적인 스레드는 스레드가 세마포를 해제할 때까지 대기합니다. 세마포에는 스레드 선호도가 없으므로 한 스레드가 세마포를 획득할 수 있고 또 다른 스레드가 해당 세마포를 해제할 수 있습니다.

<xref:System.Threading.SemaphoreSlim>은 <xref:System.Threading.Semaphore>의 간단한 대체 항목이고 단일 프로세스 경계 내의 동기화에만 사용할 수 있습니다.

Windows에서는 프로세스 간 동기화에 <xref:System.Threading.Semaphore>를 사용할 수 있습니다. 이 작업을 수행하려면 이름을 지정하는 <xref:System.Threading.Semaphore>세마포 생성자[ 중 하나 또는 ](<xref:System.Threading.Semaphore.%23ctor%2A>) 메서드를 사용하여 명명된 시스템 세마포를 나타내는 <xref:System.Threading.Semaphore.OpenExisting%2A?displayProperty=nameWithType> 인스턴스를 만듭니다. <xref:System.Threading.SemaphoreSlim>은 명명된 시스템 세마포를 지원하지 않습니다.

자세한 내용은 [세마포 및 SemaphoreSlim](semaphore-and-semaphoreslim.md) 문서와 <xref:System.Threading.Semaphore> 또는 <xref:System.Threading.SemaphoreSlim> API 참조를 참조하세요.

## <a name="thread-interaction-or-signaling"></a>스레드 상호 작용 또는 신호

스레드 상호 작용(또는 스레드 신호)은 스레드가 계속 진행하기 위해 하나 이상의 스레드에서 알림이나 신호를 기다려야 함을 의미합니다. 예를 들어 스레드 A가 스레드 B의 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> 메서드를 호출하는 경우 스레드 B가 완료될 때까지 스레드 A가 차단됩니다. 이전 섹션에 설명된 동기화 기본 형식은 신호를 위한 다른 메커니즘을 제공합니다. 잠금을 해제함으로써 스레드는 또 다른 스레드에 잠금을 획득하면 계속 진행할 수 있음을 알립니다.

이 섹션에서는 .NET에서 제공하는 추가 신호 구문을 설명합니다.

### <a name="eventwaithandle-autoresetevent-manualresetevent-and-manualreseteventslim-classes"></a>EventWaitHandle, AutoResetEvent, ManualResetEvent 및 ManualResetEventSlim 클래스

<xref:System.Threading.EventWaitHandle?displayProperty=nameWithType> 클래스는 스레드 동기화 이벤트를 나타냅니다.

동기화 이벤트는 신호 알림 또는 신호 알림 해제 상태일 수 있습니다. 이벤트 상태가 신호 알림 해제인 경우 이벤트의 <xref:System.Threading.WaitHandle.WaitOne%2A?> 오버로드를 호출하는 스레드는 이벤트가 신호 알림을 받을 때까지 차단됩니다. <xref:System.Threading.EventWaitHandle.Set%2A?displayProperty=nameWithType> 메서드는 이벤트 상태를 신호 알림으로 설정합니다.

신호 알림을 받은 <xref:System.Threading.EventWaitHandle>의 동작은 재설정 모드에 따라 다릅니다.

- <xref:System.Threading.EventResetMode.AutoReset?displayProperty=nameWithType> 플래그를 사용하여 만들어진 <xref:System.Threading.EventWaitHandle>은 단일 대기 스레드를 해제한 후 자동으로 다시 설정됩니다. 신호 알림을 받을 때마다 스레드를 하나만 허용하는 턴스타일과 같습니다. <xref:System.Threading.EventWaitHandle>에서 파생되는 <xref:System.Threading.AutoResetEvent?displayProperty=nameWithType> 클래스는 해당 동작을 나타냅니다.
- <xref:System.Threading.EventResetMode.ManualReset?displayProperty=nameWithType> 플래그를 사용하여 만들어진 <xref:System.Threading.EventWaitHandle>은 <xref:System.Threading.EventWaitHandle.Reset%2A> 메서드가 호출될 때까지 신호 알림 상태를 유지합니다. 신호 알림을 받을 때까지 닫혀 있고 이후 누군가 닫을 때까지 열려 있는 게이트와 같습니다. <xref:System.Threading.EventWaitHandle>에서 파생되는 <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> 클래스는 해당 동작을 나타냅니다. <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType> 클래스는 <xref:System.Threading.ManualResetEvent>의 간단한 대체 항목입니다.

Windows에서는 프로세스 간 동기화에 <xref:System.Threading.EventWaitHandle>를 사용할 수 있습니다. 이 작업을 수행하려면 이름을 지정하는 <xref:System.Threading.EventWaitHandle>EventWaitHandle 생성자[ 중 하나 또는 ](<xref:System.Threading.EventWaitHandle.%23ctor%2A>) 메서드를 사용하여 명명된 시스템 동기화 이벤트를 나타내는 <xref:System.Threading.EventWaitHandle.OpenExisting%2A?displayProperty=nameWithType> 인스턴스를 만듭니다.

자세한 내용은 [EventWaitHandle](eventwaithandle.md) 문서를 참조하세요. API 참조에 대해서는 <xref:System.Threading.EventWaitHandle>, <xref:System.Threading.AutoResetEvent>, <xref:System.Threading.ManualResetEvent> 및 <xref:System.Threading.ManualResetEventSlim>을 참조하세요.

### <a name="countdownevent-class"></a>CountdownEvent 클래스

<xref:System.Threading.CountdownEvent?displayProperty=nameWithType> 클래스는 개수가 0일 때 설정되는 이벤트를 나타냅니다. <xref:System.Threading.CountdownEvent.CurrentCount?displayProperty=nameWithType>는 0보다 크지만 <xref:System.Threading.CountdownEvent.Wait%2A?displayProperty=nameWithType>를 호출하는 스레드가 차단됩니다. <xref:System.Threading.CountdownEvent.Signal%2A?displayProperty=nameWithType>을 호출하여 이벤트의 수를 감소시킵니다.

한 스레드의 신호로 다중 스레드를 차단 해제하는 데 사용할 수 있는 <xref:System.Threading.ManualResetEvent> 또는 <xref:System.Threading.ManualResetEventSlim>와 달리, <xref:System.Threading.CountdownEvent>를 사용하여 여러 스레드의 신호로 하나 이상의 스레드를 차단 해제할 수 있습니다.

자세한 내용은 [CountdownEvent](countdownevent.md) 문서 및 <xref:System.Threading.CountdownEvent> API 참조를 참조하세요.

### <a name="barrier-class"></a>Barrier 클래스

<xref:System.Threading.Barrier?displayProperty=nameWithType> 클래스는 스레드 실행 경계를 나타냅니다. <xref:System.Threading.Barrier.SignalAndWait%2A?displayProperty=nameWithType> 메서드를 호출하는 스레드는 장벽에 도달했다는 신호 알림을 보내고 다른 참가자 스레드가 경계에 도달할 때까지 대기합니다. 모든 참가자 스레드는 장벽에 도달하면 계속 진행하며 장벽이 다시 설정되고 다시 사용할 수 있습니다.

하나 이상의 스레드가 다음 계산 단계로 진행하기 전에 다른 스레드의 결과를 필요로 할 때 <xref:System.Threading.Barrier>를 사용할 수 있습니다.

자세한 내용은 [Barrier](barrier.md) 문서 및 <xref:System.Threading.Barrier> API 참조를 참조하세요.

## <a name="interlocked-class"></a>Interlocked 클래스

<xref:System.Threading.Interlocked?displayProperty=nameWithType> 클래스는 변수에서 단순 원자성 작업을 수행하는 정적 메서드를 제공합니다. 해당 원자성 작업에는 비교에 따른 추가, 증가 및 감소, 교환, 조건부 교환이 포함되고 64비트 정수 값을 읽는 작업이 포함됩니다.

자세한 내용은 <xref:System.Threading.Interlocked> API 참조를 참조하세요.

## <a name="spinwait-structure"></a>SpinWait 구조체

<xref:System.Threading.SpinWait?displayProperty=nameWithType> 구조체는 회전 기반 대기를 지원합니다. 이벤트가 신호를 받거나 조건이 충족될 때까지 스레드가 대기해야 하지만 대기 핸들을 사용하거나 현재 스레드를 차단하여 실제 대기 시간이 필요한 대기 시간보다 적을 것으로 예상할 때 이를 사용할 수 있습니다. <xref:System.Threading.SpinWait>를 사용하면 대기하는 동안 스핀하고 지정된 시간 안에 조건이 충족되지 않을 경우에만 대기 또는 중지를 통해 양보하는 짧은 기간을 지정할 수 있습니다.

자세한 내용은 [SpinWait](spinwait.md) 문서 및 <xref:System.Threading.SpinWait> API 참조를 참조하세요.

## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Concurrent?displayProperty=nameWithType>
- [스레드로부터 안전한 컬렉션](../collections/thread-safe/index.md)
- [스레딩 개체 및 기능](threading-objects-and-features.md)
