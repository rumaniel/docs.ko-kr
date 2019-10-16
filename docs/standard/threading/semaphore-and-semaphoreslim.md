---
title: 세마포 및 SemaphoreSlim
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- counting semaphores
- semaphores
- threading [.NET Framework], cross-process synchronization
- Semaphore class, about Semaphore class
- SemaphoreSlim class, about SemaphoreSlim class
- threading [.NET Framework], Semaphore class
ms.assetid: 7722a333-b974-47a2-a7c0-f09097fb644e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 25121ea2b089df49efa77dcf363e2a0e400b3bff
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968431"
---
# <a name="semaphore-and-semaphoreslim"></a>세마포 및 SemaphoreSlim
로컬 또는 명명된(시스템 전체) 세마포를 나타내는 <xref:System.Threading.Semaphore?displayProperty=nameWithType> 클래스는 Win32 세마포 개체를 묶는 씬 래퍼입니다. Win32 세마포는 리소스 풀에 대한 액세스를 제어하는 데 사용할 수 있는 가산 세마포입니다.  
  
 <xref:System.Threading.SemaphoreSlim> 클래스는 대기 시간이 매우 짧을 것으로 예상될 때 단일 프로세스 내에서 대기하는 데 사용할 수 있는 간단하고 빠른 세마포를 나타냅니다. <xref:System.Threading.SemaphoreSlim>은 CLR(공용 언어 런타임)에서 제공하는 동기화 기본 형식을 최대한 활용합니다. 그러나 필요에 따라 여러 세마포에 대해 대기를 지원할 수 있도록 지연 초기화된 커널 기반 대기 핸들도 제공합니다. 또한 <xref:System.Threading.SemaphoreSlim>은 취소 토큰 사용도 지원하지만 명명된 세마포 또는 동기화용 대기 핸들 사용은 지원하지 않습니다.  
  
## <a name="managing-a-limited-resource"></a>제한된 리소스 관리  
 스레드는 <xref:System.Threading.WaitHandle.WaitOne%2A> 메서드를 호출하여 세마포를 입력합니다. 이 메서드는 <xref:System.Threading.WaitHandle> 개체의 경우 <xref:System.Threading.Semaphore?displayProperty=nameWithType> 클래스에서 상속되고 <xref:System.Threading.SemaphoreSlim> 개체의 경우에는 <xref:System.Threading.SemaphoreSlim.Wait%2A?displayProperty=nameWithType> 또는 <xref:System.Threading.SemaphoreSlim.WaitAsync%2A?displayProperty=nameWithType> 메서드에서 상속됩니다. 호출이 반환되면 세마포 수가 감소합니다. 스레드가 항목을 요청할 때 개수가 0이면 해당 스레드는 차단됩니다. 스레드가 <xref:System.Threading.Semaphore.Release%2A?displayProperty=nameWithType> 또는 <xref:System.Threading.SemaphoreSlim.Release%2A?displayProperty=nameWithType> 메서드를 호출하여 세마포를 해제하면 차단된 스레드를 입력할 수 있게 됩니다. FIFO(선입 선출) 또는 LIFO(후입 선출)와 같이 차단된 스레드가 세마포에 입력되는 보장된 순서는 없습니다.  
  
 스레드는 <xref:System.Threading.Semaphore?displayProperty=nameWithType> 개체의 <xref:System.Threading.WaitHandle.WaitOne%2A> 메서드 또는 <xref:System.Threading.SemaphoreSlim> 개체의 <xref:System.Threading.SemaphoreSlim.Wait%2A> 메서드를 반복적으로 호출하여 세마포를 여러 번 입력할 수 있습니다. 세마포를 해제하려는 경우 스레드는 <xref:System.Threading.Semaphore.Release?displayProperty=nameWithType> 또는 <xref:System.Threading.SemaphoreSlim.Release?displayProperty=nameWithType> 메서드 오버로드를 같은 횟수만큼 호출하거나 <xref:System.Threading.Semaphore.Release%28System.Int32%29?displayProperty=nameWithType> 또는 <xref:System.Threading.SemaphoreSlim.Release%28System.Int32%29?displayProperty=nameWithType> 메서드 오버로드를 호출하고 해제할 항목 수를 지정할 수 있습니다.  
  
### <a name="semaphores-and-thread-identity"></a>세마포 및 스레드 ID  
 두 세마포 형식은 <xref:System.Threading.WaitHandle.WaitOne%2A>, <xref:System.Threading.SemaphoreSlim.Wait%2A>, <xref:System.Threading.Semaphore.Release%2A> 및 <xref:System.Threading.SemaphoreSlim.Release%2A?displayProperty=nameWithType> 메서드 호출에 대해 스레드 ID를 적용하지 않습니다. 예를 들어 세마포의 일반적인 사용 시나리오에서는 생산자 스레드와 소비자 스레드가 사용되는데, 여기서 스레드 하나는 항상 세마포 수를 증가시키고 다른 하나는 항상 세마포 수를 감소시킵니다.  
  
 프로그래머는 스레드가 세마포를 너무 여러 번 해제하지 않는지 확인해야 합니다. 예를 들어 세마포의 최대 개수가 2개인데 스레드 A와 스레드 B가 모두 세마포를 입력한다고 가정해 보겠습니다. 스레드 B에서 프로그래밍 오류가 발생하여 `Release`가 두 번 호출되면 두 호출은 모두 성공합니다. 그러면 세마포 개수가 다 차서 스레드 A가 `Release`를 호출하면 <xref:System.Threading.SemaphoreFullException>이 throw됩니다.  
  
## <a name="named-semaphores"></a>명명된 세마포  
 Windows 운영 체제에서는 세마포에 이름을 지정할 수 있습니다. 명명된 세마포는 시스템 전체에 사용됩니다. 즉, 명명된 세마포는 작성되고 나면 모든 프로세스의 모든 프로세스에 표시됩니다. 따라서 명명된 세마포는 스레드뿐 아니라 프로세스의 활동을 동기화하는 데도 사용할 수 있습니다.  
  
 이름을 지정하는 생성자 중 하나를 사용하여 명명된 시스템 세마포를 나타내는 <xref:System.Threading.Semaphore> 개체를 만들 수 있습니다.  
  
> [!NOTE]
> 명명된 세마포는 시스템 전체 세마포이므로 같은 명명된 세마포를 나타내는 <xref:System.Threading.Semaphore> 개체를 여러 개 사용할 수 있습니다. 생성자 또는 <xref:System.Threading.Semaphore.OpenExisting%2A?displayProperty=nameWithType> 메서드를 호출할 때마다 새 <xref:System.Threading.Semaphore> 개체가 만들어집니다. 같은 이름을 반복적으로 지정하면 같은 명명된 세마포를 나타내는 개체가 여러 개 만들어집니다.  
  
 명명된 세마포를 사용할 때는 주의해야 합니다. 이러한 세마포는 시스템 전체 세마포이므로 같은 이름을 사용하는 다른 프로세스가 예기치 않게 세마포를 입력할 수 있습니다. 그러면 동일 컴퓨터에서 실행되는 악성 코드가 이를 악용해 서비스 거부 공격을 수행할 수 있습니다.  
  
 명명된 세마포를 나타내는 <xref:System.Threading.Semaphore> 개체를 보호하려면 액세스 제어 보안을 사용합니다. 이때 <xref:System.Security.AccessControl.SemaphoreSecurity?displayProperty=nameWithType> 개체를 지정하는 생성자를 사용하는 것이 좋습니다. <xref:System.Threading.Semaphore.SetAccessControl%2A?displayProperty=nameWithType> 메서드를 사용하여 액세스 제어 보안을 적용할 수도 있지만 이렇게 하면 세마포 작성 시간과 보호가 적용되는 시간 사이에 취약한 기간이 생기게 됩니다. 액세스 제어 보안을 통해 세마포를 보호하면 악의적인 공격을 방지할 수는 있지만 의도하지 않은 이름 충돌 문제는 해결되지 않습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Semaphore>
- <xref:System.Threading.SemaphoreSlim>
- [스레딩 개체 및 기능](../../../docs/standard/threading/threading-objects-and-features.md)
