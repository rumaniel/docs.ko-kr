---
title: asynchronousThreadAbort MDA
ms.date: 03/30/2017
helpviewer_keywords:
- asynchronous thread aborts
- AsynchronousThreadAbort MDA
- managed debugging assistants (MDAs), asynchronous thread aborts
- threading [.NET Framework], managed debugging assistants
- MDAs (managed debugging assistants), asynchronous thread aborts
ms.assetid: 9ebe40b2-d703-421e-8660-984acc42bfe0
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9bde6f6e625476712c5af516491ab9dd29b7dea3
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052954"
---
# <a name="asynchronousthreadabort-mda"></a>asynchronousThreadAbort MDA
`asynchronousThreadAbort` MDA(관리 디버깅 도우미)는 스레드가 비동기 중단을 다른 스레드에 도입하려고 할 때 활성화됩니다. 동기 스레드 중단은 `asynchronousThreadAbort` MDA를 활성화하지 않습니다.

## <a name="symptoms"></a>증상
 주 애플리케이션 스레드가 중단되는 경우 애플리케이션이 처리되지 않은 <xref:System.Threading.ThreadAbortException>과 충돌합니다. 애플리케이션을 계속 실행하면 결과가 애플리케이션 충돌보다 더욱 악화되어 추가 데이터 손상이 발생할 수 있습니다.

 원자성으로 의도된 작업이 부분 완료 후 중단되어 애플리케이션 데이터가 예측할 수 없는 상태로 남겨졌을 가능성이 있습니다. 코드 실행의 임의 지점에서 <xref:System.Threading.ThreadAbortException>이 생성될 수 있으며, 예외가 발생할 것으로 예상되지 않는 지점에서 생성되는 경우도 많습니다. 코드에서 이러한 예외를 처리하지 못해 손상된 상태가 발생할 수도 있습니다.

 문제에 상속되는 임의성으로 인해 증상이 크게 달라질 수 있습니다.

## <a name="cause"></a>원인
 한 스레드의 코드에서 대상 스레드에 대해 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 메서드를 호출하여 비동기 스레드 중단을 도입했습니다. <xref:System.Threading.Thread.Abort%2A>를 호출하는 코드가 중단 작업의 대상이 아닌 다른 스레드에서 실행되고 있으므로 스레드 중단은 비동기입니다. <xref:System.Threading.Thread.Abort%2A>를 수행하는 스레드는 응용 프로그램 상태가 일치하는 안전한 검사점에서만 작업했기 때문에 동기 스레드 중단으로 인한 문제가 발생하지 않아야 합니다.

 비동기 스레드 중단은 대상 스레드 실행 중 예기치 않은 지점에서 처리되므로 문제를 일으킵니다. 이를 방지하려면 이런 방식으로 중단될 수 있는 스레드에서 실행되도록 작성된 코드는 거의 모든 코드 줄에서 <xref:System.Threading.ThreadAbortException>을 처리하고 애플리케이션 데이터를 다시 일치 상태로 만들어야 합니다. 이 문제를 염두에 두고 코드가 작성되기를 기대하거나 가능한 모든 상황으로부터 보호하는 코드를 작성하는 것은 어렵습니다.

 비관리 코드와 `finally` 블록 호출은 비동기적으로 중단되지 않고 이러한 범주 중 하나에서 종료 시 즉시 중단됩니다.

 문제에 내재된 임의성 때문에 원인을 확인하기 어려울 수 있습니다.

## <a name="resolution"></a>해결
 비동기 스레드 중단을 사용해야 하는 코드 디자인을 사용하지 마세요. <xref:System.Threading.Thread.Abort%2A> 호출이 필요 없고 대상 스레드 중단에 더 적합한 여러 가지 방법이 있습니다. 가장 안전한 방법은 대상 스레드에 중단을 요청하도록 알리는 일반 속성 등의 메커니즘을 도입하는 것입니다. 대상 스레드는 안전한 특정 검사점에서 신호를 확인합니다. 인터럽트가 요청된 것을 발견하면 정상적으로 종료할 수 있습니다.

## <a name="effect-on-the-runtime"></a>런타임에 대한 영향
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다. 비동기 스레드 중단에 대한 데이터를 보고만 합니다.

## <a name="output"></a>출력
 MDA는 중단을 수행하는 스레드의 ID 및 중단의 대상이 되는 스레드의 ID를 보고합니다. 비동기 중단으로 제한되므로 두 ID는 동일하지 않습니다.

## <a name="configuration"></a>구성

```xml
<mdaConfig>
  <assistants>
    <asynchronousThreadAbort />
  </assistants>
</mdaConfig>
```

## <a name="example"></a>예제
 `asynchronousThreadAbort` MDA를 활성화하려는 경우 실행 중인 별도 스레드에서 <xref:System.Threading.Thread.Abort%2A>를 호출하기만 하면 됩니다. 스레드 시작 함수의 내용이 임의 지점에서 중단에 의해 인터럽트될 수 있는 보다 복잡한 작업 집합인 경우의 결과를 고려해 보세요.

```csharp
using System.Threading;
void FireMda()
{
    Thread t = new Thread(delegate() { Thread.Sleep(1000); });
    t.Start();
    // The following line activates the MDA.
    t.Abort();
    t.Join();
}
```

## <a name="see-also"></a>참고자료

- <xref:System.Threading.Thread>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
