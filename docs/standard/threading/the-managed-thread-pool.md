---
title: 관리되는 스레드 풀
description: 백그라운드 작업자 스레드를 제공하는 .NET 스레드 풀에 대해 알아보기
ms.date: 08/02/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- thread pooling [.NET]
- thread pools [.NET]
- threading [.NET], thread pool
- threading [.NET], pooling
ms.assetid: 2be05b06-a42e-4c9d-a739-96c21d673927
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f921f40bbc5a7b72341c3fb778dd69fcc7b918c9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54665268"
---
# <a name="the-managed-thread-pool"></a>관리되는 스레드 풀

<xref:System.Threading.ThreadPool?displayProperty=nameWithType> 클래스는 시스템에서 관리하는 작업자 스레드 풀을 애플리케이션에 제공하여 스레드 관리 대신 애플리케이션 작업에 집중할 수 있게 해줍니다. 후순위 처리가 필요한 간단한 작업이 있는 경우 관리되는 스레드 풀을 통해 쉽게 여러 스레드를 활용할 수 있습니다. 스레드 풀 스레드에서 비동기 작업을 수행하는 <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 개체를 만들 수 있으므로 Framework 4 이상에서는 스레드 풀의 사용이 훨씬 쉬워집니다.  
  
.NET에서는 [TPL(작업 병렬 라이브러리)](../parallel-programming/task-parallel-library-tpl.md) 작업, 비동기 I/O 완료, [타이머](timers.md) 콜백, 등록된 대기 작업, 대리자를 사용한 비동기 메서드 호출 및 <xref:System.Net?displayProperty=nameWithType> 소켓 연결을 비롯한 다양한 용도로 스레드 풀 스레드를 사용합니다.  

## <a name="thread-pool-characteristics"></a>스레드 풀 특징

스레드 풀 스레드는 [백그라운드](foreground-and-background-threads.md) 스레드입니다. 각 스레드는 기본 스택 크기를 사용하고, 기본 우선 순위로 실행되며, 다중 스레드 아파트에 있습니다. 스레드 풀의 스레드가 해당 작업을 완료하면 대기 중인 스레드 큐로 반환됩니다. 이 시점에서 다시 사용할 수 있습니다. 이렇게 다시 사용하면 애플리케이션에서 각 작업에 대한 새 스레드를 만드는 비용을 방지할 수 있습니다.
  
프로세스당 하나의 스레드 풀만 있습니다.  
  
### <a name="exceptions-in-thread-pool-threads"></a>스레드 풀 스레드의 예외

스레드 풀 스레드에 처리되지 않은 예외가 있으면 프로세스가 종료됩니다. 이 규칙에는 다음 세 가지 예외 사항이 있습니다.  
  
- <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>가 호출되었으므로 스레드 풀 스레드에서 <xref:System.Threading.ThreadAbortException?displayProperty=nameWithType>이 throw됩니다.  
- 애플리케이션 도메인이 언로드되고 있으므로 스레드 풀 스레드에서 <xref:System.AppDomainUnloadedException?displayProperty=nameWithType>이 throw됩니다.  
- 공용 언어 런타임 또는 호스트 프로세스에서 스레드를 종료합니다.  
  
자세한 내용은 [관리되는 스레드의 예외](exceptions-in-managed-threads.md)를 참조하세요.  
  
### <a name="maximum-number-of-thread-pool-threads"></a>스레드 풀 스레드의 최대 개수

스레드 풀에 대기할 수 있는 작업 수가 사용 가능한 메모리에 의해 제한됩니다. 그러나 스레드 풀이 동시에 프로세스에서 활성화될 수 있는 스레드 수를 제한합니다. 모든 스레드 풀 스레드가 사용 중이면 스레드가 실행하는 데 사용 가능할 때까지 추가 작업 항목은 대기됩니다. .NET Framework 4부터 프로세스에 대한 스레드 풀의 기본 크기는 가상 주소 공간의 크기와 같은 여러 요인에 따라 달라집니다. 프로세스에서 <xref:System.Threading.ThreadPool.GetMaxThreads%2A?displayProperty=nameWithType> 메서드를 호출하여 스레드 수를 확인할 수 있습니다.  
  
<xref:System.Threading.ThreadPool.GetMaxThreads%2A?displayProperty=nameWithType> 및 <xref:System.Threading.ThreadPool.SetMaxThreads%2A?displayProperty=nameWithType> 메서드를 사용하여 최대 스레드 수를 제어할 수 있습니다.  

> [!NOTE]
> 공용 언어 런타임을 호스트하는 코드는 [`ICorThreadpool::CorSetMaxThreads`](../../framework/unmanaged-api/hosting/icorthreadpool-corsetmaxthreads-method.md) 메서드를 사용하여 크기를 설정할 수 있습니다.  
  
### <a name="thread-pool-minimums"></a>스레드 풀 최솟값

스레드 풀은 각 범주에 대해 지정된 최소값에 도달할 때까지 요청 시 새 작업자 스레드 또는 I/O 완료 스레드를 제공합니다. <xref:System.Threading.ThreadPool.GetMinThreads%2A?displayProperty=nameWithType> 메서드를 사용하여 이러한 최소값을 가져올 수 있습니다.  
  
> [!NOTE]
> 요구가 적을 때는 실제 스레드 풀 스레드 수가 최소값보다 작을 수 있습니다.  
  
최소값에 도달하면 스레드 풀이 추가 스레드를 만들거나 일부 작업이 완료될 때까지 기다릴 수 있습니다. .NET Framework 4부터는 스레드 풀이 시간 단위당 완료되는 작업 수로 정의된 처리량을 최적화하기 위해 작업자 스레드를 만들고 삭제합니다. 스레드가 너무 적으면 사용 가능한 리소스가 효율적으로 사용되지 않는 반면, 너무 많으면 리소스 경합이 증가할 수 있습니다.  
  
> [!CAUTION]
> <xref:System.Threading.ThreadPool.SetMinThreads%2A?displayProperty=nameWithType> 메서드를 사용하여 유휴 상태 스레드의 최소 개수를 늘릴 수 있습니다. 그러나 이러한 값을 불필요하게 늘리면 성능 문제가 발생할 수 있습니다. 너무 많은 작업이 동시에 시작되는 경우 모두 속도가 느린 것처럼 나타날 수 있습니다. 대부분의 경우 스레드 풀은 고유한 스레드 할당 알고리즘에서 성능이 향상됩니다.  

## <a name="using-the-thread-pool"></a>스레드 풀 사용

.NET Framework 4부터 스레드 풀을 사용하는 가장 쉬운 방법은 [TPL(작업 병렬 라이브러리)](../parallel-programming/task-parallel-library-tpl.md)을 사용하는 것입니다. 기본적으로 <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601>과 같은 TPL 형식은 스레드 풀 스레드를 사용하여 작업을 실행합니다.

관리 코드에서 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=nameWithType>(또는 비관리 코드에서 [`ICorThreadpool::CorQueueUserWorkItem`](../../framework/unmanaged-api/hosting/icorthreadpool-corqueueuserworkitem-method.md))을 호출하고 작업을 수행하는 메서드를 나타내는 <xref:System.Threading.WaitCallback?displayProperty=nameWithType> 대리자를 전달하여 스레드 풀을 사용할 수도 있습니다.

스레드 풀을 사용하는 또 다른 방법은 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=nameWithType> 메서드를 사용하고 신호를 받거나 시간 초과된 경우 <xref:System.Threading.WaitOrTimerCallback?displayProperty=nameWithType> 대리자가 나타내는 메서드를 호출하는 <xref:System.Threading.WaitHandle?displayProperty=nameWithType>을 전달하여 대기 작업과 관련된 작업 항목을 큐에 대기합니다. 스레드 풀 스레드는 콜백 메서드를 호출하는 데 사용됩니다.  

예제에서 참조된 API 페이지를 확인합니다.
  
## <a name="skipping-security-checks"></a>보안 검사 건너뛰기

스레드 풀은 <xref:System.Threading.ThreadPool.UnsafeQueueUserWorkItem%2A?displayProperty=nameWithType> 및 <xref:System.Threading.ThreadPool.UnsafeRegisterWaitForSingleObject%2A?displayProperty=nameWithType> 메서드도 제공합니다. 호출자 스택이 큐에 대기 중인 작업을 실행하는 동안 수행되는 보안 검사와 관련이 없는 경우에만 이러한 메서드를 사용합니다. <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=nameWithType> 및 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=nameWithType>는 둘 다 호출자 스택을 캡처합니다. 호출자 스택은 스레드가 작업 실행을 시작할 때 스레드 풀 스레드 스택에 병합됩니다. 보안 검사가 필요한 경우 전체 스택을 검사해야 합니다. 검사를 통해 안전성이 제공되지만 성능이 저하되는 단점도 있습니다.  

## <a name="when-not-to-use-thread-pool-threads"></a>스레드 풀 스레드를 사용하지 않아야 하는 경우

스레드 풀 스레드를 사용하는 대신 고유한 스레드를 만들고 관리하는 것이 적절한 여러 가지 시나리오가 있습니다.  
  
- 포그라운드 스레드가 필요합니다.  
- 스레드가 특정 우선 순위를 가져야 합니다.  
- 스레드가 오랜 시간 동안 차단되게 하는 작업이 있습니다. 스레드 풀에 최대 개수의 스레드가 있으므로 차단된 스레드 풀 스레드 수가 많으면 작업이 시작되지 않을 수 있습니다.  
- 단일 스레드 아파트에 스레드를 배치해야 합니다. 모든 <xref:System.Threading.ThreadPool> 스레드는 다중 스레드 아파트에 있습니다.  
- 스레드와 연결된 안정적인 ID가 있거나 스레드를 작업 전용으로 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.ThreadPool?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>
- [TPL(작업 병렬 라이브러리)](../parallel-programming/task-parallel-library-tpl.md)
- [방법: 작업에서 값 반환](../parallel-programming/how-to-return-a-value-from-a-task.md)
- [스레딩 개체 및 기능](threading-objects-and-features.md)
- [스레드 및 스레딩](threads-and-threading.md)
- [Asynchronous File I/O](../io/asynchronous-file-i-o.md)
- [타이머](timers.md)
