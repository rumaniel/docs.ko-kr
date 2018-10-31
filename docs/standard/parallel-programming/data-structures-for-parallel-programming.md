---
title: 병렬 프로그래밍을 위한 데이터 구조
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- data structures, multi-threading
ms.assetid: bdc82f2f-4754-45a1-a81e-fe2e9c30cef9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6453e9983086dcb5b97ec134db9d74160d7a47cf
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836475"
---
# <a name="data-structures-for-parallel-programming"></a>병렬 프로그래밍을 위한 데이터 구조
.NET Framework 버전 4에서는 동시 컬렉션 클래스, 간단한 동기화 기본 요소 및 초기화 지연 관련 형식을 포함하여 병렬 프로그래밍에서 유용한 여러 가지 새로운 형식을 소개합니다. 이러한 형식을 작업 병렬 라이브러리 및 PLINQ를 포함한 다중 스레드 응용 프로그램 코드와 함께 사용할 수 있습니다.  
  
## <a name="concurrent-collection-classes"></a>동시 컬렉션 클래스  
 <xref:System.Collections.Concurrent?displayProperty=nameWithType> 네임스페이스의 컬렉션 클래스는 가능한 경우 항상 잠금을 방지하고 잠금이 필요한 경우 세분화된 잠금을 사용하는 스레드로부터 안전한 추가 및 제거 작업을 제공합니다. .NET Framework 버전 1.0 및 2.0에 도입된 컬렉션과 달리 동시 컬렉션 클래스에는 항목에 액세스할 때 잠금을 획득하기 위한 사용자 코드가 필요하지 않습니다. 동시 컬렉션 클래스는 여러 스레드가 컬렉션에서 항목을 추가하고 제거하는 시나리오에서 <xref:System.Collections.ArrayList?displayProperty=nameWithType> 및 <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>(사용자가 구현한 잠금 사용)와 같은 형식보다 성능을 크게 개선할 수 있습니다.  
  
 다음 표에는 새로운 동시 컬렉션 클래스가 나와 있습니다.  
  
|형식|설명|  
|----------|-----------------|  
|<xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType>|<xref:System.Collections.Concurrent.IProducerConsumerCollection%601?displayProperty=nameWithType>을 구현하는 스레드로부터 안전한 컬렉션에 대한 차단 및 경계 기능을 제공합니다. 슬롯을 사용할 수 없거나 컬렉션이 가득 차면 생산자 스레드가 차단됩니다. 컬렉션이 비어 있으면 소비자 스레드가 차단됩니다. 이 형식은 소비자 및 생산자가 비차단 액세스도 지원합니다. <xref:System.Collections.Concurrent.BlockingCollection%601>은 <xref:System.Collections.Generic.IEnumerable%601>을 지원하는 모든 컬렉션 클래스에 대한 차단 및 결합을 제공하기 위한 기본 클래스 또는 백업 저장소로 사용할 수 있습니다.|  
|<xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=nameWithType>|확장 가능한 추가 및 가져오기 작업을 제공하는 스레드로부터 안전한 모음 구현.|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=nameWithType>|동시 및 확장 가능한 사전 형식.|  
|<xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType>|동시 및 확장 가능한 FIFO 큐.|  
|<xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=nameWithType>|동시 및 확장 가능한 LIFO 스택.|  
  
 자세한 내용은 [스레드로부터 안전한 컬렉션](../../../docs/standard/collections/thread-safe/index.md)을 참조하세요.  
  
## <a name="synchronization-primitives"></a>동기화 기본 형식  
 <xref:System.Threading?displayProperty=nameWithType> 네임스페이스의 새 동기화 기본 형식은 레거시 다중 스레딩 코드에 있는 비용이 많이 드는 잠금 메커니즘을 방지하여 세분화된 동시성과 더 빠른 성능을 제공할 수 있습니다. <xref:System.Threading.Barrier?displayProperty=nameWithType> 및 <xref:System.Threading.CountdownEvent?displayProperty=nameWithType>와 같은 일부 새로운 형식은 이전 릴리스의 .NET Framework에는 해당하는 항목이 없습니다.  
  
 다음 표에는 새 동기화 형식이 나와 있습니다.  
  
|형식|설명|  
|----------|-----------------|  
|<xref:System.Threading.Barrier?displayProperty=nameWithType>|각 작업이 도착에 대한 신호를 보낸 다음, 일부 또는 모든 작업이 도착할 때까지 차단될 수 있는 지점을 제공하여 여러 스레드가 하나의 알고리즘에서 병렬로 작동하도록 합니다. 자세한 내용은 [Barrier](../../../docs/standard/threading/barrier.md)를 참조하세요.|  
|<xref:System.Threading.CountdownEvent?displayProperty=nameWithType>|쉽게 랑데부 메커니즘을 제공하여 포크 및 조인 시나리오를 간소화합니다. 자세한 내용은 [CountdownEvent](../../../docs/standard/threading/countdownevent.md)를 참조하세요.|  
|<xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType>|<xref:System.Threading.ManualResetEvent?displayProperty=nameWithType>와 유사한 동기화 기본 형식입니다. <xref:System.Threading.ManualResetEventSlim>은 더 간단하지만 프로세스 간 통신에만 사용할 수 있습니다. 자세한 내용은 [ManualResetEvent 및 ManualResetEventSlim](../../../docs/standard/threading/manualresetevent-and-manualreseteventslim.md)을 참조하세요.|  
|<xref:System.Threading.SemaphoreSlim?displayProperty=nameWithType>|리소스 또는 리소스 풀에 동시에 액세스할 수 있는 스레드 수를 제한하는 동기화 기본 형식입니다. 자세한 내용은 [세마포 및 SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md)을 참조하세요.|  
|<xref:System.Threading.SpinLock?displayProperty=nameWithType>|퀀텀을 일시 중단하기 전에 일정 시간 동안 잠금을 획득하려고 시도 중인 스레드가 루프 또는 ‘스핀’에서 대기하도록 하는 상호 배제 잠금 기본 형식입니다. 잠금 대기가 짧아야 하는 시나리오에서 <xref:System.Threading.SpinLock>은 다른 형태의 잠금보다 향상된 성능을 제공합니다. 자세한 내용은 [SpinLock](../../../docs/standard/threading/spinlock.md)을 참조하세요.|  
|<xref:System.Threading.SpinWait?displayProperty=nameWithType>|지정된 시간 동안 스핀하고 스핀 수를 초과하는 경우 결국 스레드를 대기 상태로 전환하는 작고 간단한 형식입니다.  자세한 내용은 [SpinWait](../../../docs/standard/threading/spinwait.md)을 참조하세요.|  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [방법: 낮은 수준의 동기화에 SpinLock 사용](../../../docs/standard/threading/how-to-use-spinlock-for-low-level-synchronization.md)  
  
-   [방법: 동시 작업을 배리어와 동기화](../../../docs/standard/threading/how-to-synchronize-concurrent-operations-with-a-barrier.md).  
  
## <a name="lazy-initialization-classes"></a>초기화 지연 클래스  
 초기화 지연을 사용하면 필요할 때까지 개체용 메모리가 할당되지 않습니다. 초기화 지연을 통해 개체 할당을 프로그램 수명에 균등하게 분산하여 성능을 향상시킬 수 있습니다. <xref:System.Lazy%601> 형식을 래핑하여 모든 사용자 지정 형식에 대한 초기화 지연을 사용하도록 설정할 수 있습니다.  
  
 다음 표에는 초기화 지연 형식이 나와 있습니다.  
  
|형식|설명|  
|----------|-----------------|  
|<xref:System.Lazy%601?displayProperty=nameWithType>|간단하고 스레드로부터 안전한 초기화 지연을 제공합니다.|  
|<xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType>|각 스레드가 초기화 함수 호출을 지연시켜 스레드별 기준으로 초기화가 지연된 값을 제공합니다.|  
|<xref:System.Threading.LazyInitializer?displayProperty=nameWithType>|전용 초기화 지연 인스턴스를 할당할 필요가 없도록 하는 정적 메서드를 제공합니다. 대신 참조를 사용하여 대상이 액세스될 때 초기화되었는지 확인합니다.|  
  
 자세한 내용은 [초기화 지연](../../../docs/framework/performance/lazy-initialization.md)을 참조하세요.  
  
## <a name="aggregate-exceptions"></a>집계 예외  
 <xref:System.AggregateException?displayProperty=nameWithType> 형식은 개별 스레드에서 동시에 throw되는 여러 예외를 캡처하고 조인 스레드에 단일 예외로 반환하는 데 사용할 수 있습니다. <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType> 형식과 PLINQ는 이 용도로 <xref:System.AggregateException>을 광범위하게 사용합니다. 자세한 내용은 [예외 처리](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md) 및 [방법: PLINQ 쿼리의 예외 처리](../../../docs/standard/parallel-programming/how-to-handle-exceptions-in-a-plinq-query.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Concurrent?displayProperty=nameWithType>  
- <xref:System.Threading?displayProperty=nameWithType>  
- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
