---
title: dangerousThreadingAPI MDA
ms.date: 03/30/2017
helpviewer_keywords:
- suspending threads
- DangerousThreadingAPI MDA
- managed debugging assistants (MDAs), dangerous threading operations
- threading [.NET Framework], suspending
- MDAs (managed debugging assistants), dangerous threading operations
- Suspend method
- threading [.NET Framework], managed debugging assistants
ms.assetid: 3e5efbc5-92e4-4229-b31f-ce368a1adb96
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 860f524820e6b92e58f4a593e2ddf651a5e7094d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052903"
---
# <a name="dangerousthreadingapi-mda"></a>dangerousThreadingAPI MDA
`dangerousThreadingAPI` MDA(관리 디버깅 도우미)는 <xref:System.Threading.Thread.Suspend%2A?displayProperty=nameWithType> 메서드가 현재 스레드 이외의 스레드에서 호출될 때 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 애플리케이션이 응답하지 않거나 무기한으로 중단됩니다. 시스템 또는 애플리케이션 데이터가 일시적으로 또는 애플리케이션이 종료된 후에도 예측 가능한 상태로 남아 있을 수 있습니다. 일부 작업이 예상대로 완료되지 않습니다.  
  
 문제에 상속되는 임의성으로 인해 증상이 크게 달라질 수 있습니다.  
  
## <a name="cause"></a>원인  
 스레드는 <xref:System.Threading.Thread.Suspend%2A> 메서드를 사용하는 다른 스레드에 의해 비동기적으로 일시 중단됩니다. 작업 중간에 있을 수 있는 다른 스레드를 언제 안전하게 일시 중단할 수 있는지 확인할 방법이 없습니다. 스레드를 일시 중단하면 데이터가 손상되거나 고정이 중단될 수 있습니다. 스레드가 일시 중단 상태로 전환되고 <xref:System.Threading.Thread.Resume%2A> 메서드를 통해 다시 시작되지 않으면 애플리케이션이 무기한 중단되고 애플리케이션 데이터가 손상될 수 있습니다. 이러한 메서드는 사용되지 않는 것으로 표시되었습니다.  
  
 동기화 기본 형식이 대상 스레드에서 보류되는 경우 일시 중단 중에 계속 보류됩니다. 기본 형식에 대한 잠금을 획득하려는 시도인 <xref:System.Threading.Thread.Suspend%2A>를 수행하는 스레드 같은 또 다른 스레드인 경우 이로 인해 교착 상태가 발생할 수 있습니다. 이 상황에서는 문제가 교착 상태로 나타납니다.  
  
## <a name="resolution"></a>해결  
 <xref:System.Threading.Thread.Suspend%2A> 및 <xref:System.Threading.Thread.Resume%2A>을 사용해야 하는 디자인을 피합니다. 스레드 간 상호 작용의 경우 <xref:System.Threading.Monitor>, <xref:System.Threading.ReaderWriterLock>, <xref:System.Threading.Mutex> 또는 C# `lock` 문과 같은 동기화 기본 형식을 사용합니다. 이러한 메서드를 사용해야 할 경우 스레드가 일시 중단 상태인 동안 실행되는 기간을 단축하거나 코드 양을 최소화합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다. 위험한 스레딩 작업에 대한 데이터만 보고합니다.  
  
## <a name="output"></a>출력  
 MDA는 MDA를 활성화시키는 위험한 스레딩 메서드를 식별합니다.  
  
## <a name="configuration"></a>구성하기  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dangerousThreadingAPI />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 `dangerousThreadingAPI`를 활성화시키는 <xref:System.Threading.Thread.Suspend%2A> 메서드에 대한 호출을 보여 줍니다.  
  
```csharp
using System.Threading;  
void FireMda()  
{  
Thread t = new Thread(delegate() { Thread.Sleep(1000); });  
    t.Start();  
    // The following line activates the MDA.  
    t.Suspend();   
    t.Resume();  
    t.Join();  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Threading.Thread>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [lock 문](../../csharp/language-reference/keywords/lock-statement.md)
