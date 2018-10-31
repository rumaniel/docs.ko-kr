---
title: 스레드 일시 중지 및 중단
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- interrupting threads
- threading [.NET Framework], pausing
- pausing threads
ms.assetid: 9fce4859-a19d-4506-b082-7dd0792688ca
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b66881a8a42c0c34b5c2119f7404fe7787c8f3f2
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836260"
---
# <a name="pausing-and-interrupting-threads"></a>스레드 일시 중지 및 중단

스레드 작업을 동기화하는 가장 일반적인 방법은 스레드를 차단 및 해제하거나 개체 또는 코드 영역을 잠그는 것입니다. 이러한 잠금 및 차단 메커니즘에 대한 자세한 내용은 [동기화 기본 형식 개요](../../../docs/standard/threading/overview-of-synchronization-primitives.md)를 참조하세요.  
  
 스레드가 자동으로 중지되도록 할 수도 있습니다. 스레드가 차단 또는 중지된 경우 <xref:System.Threading.ThreadInterruptedException>을 사용하여 대기 상태에서 분리할 수 있습니다.  
  
## <a name="the-threadsleep-method"></a>Thread.Sleep 메서드

 <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> 메서드를 호출하면 현재 스레드가 메서드에 전달하는 시간(밀리초) 또는 시간 간격 동안 즉시 차단되고 해당 시간 조각의 나머지 부분을 다른 스레드에 양보합니다. 지정된 시간이 지나면 대기 중인 스레드가 다시 실행되기 시작합니다.  
  
 한 스레드가 다른 스레드에서 <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType>를 호출할 수는 없습니다.  <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType>은 현재 스레드를 항상 일시 중지하는 정적 메서드입니다.  
  
 <xref:System.Threading.Timeout.Infinite?displayProperty=nameWithType> 값을 사용하여 <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType>을 호출하면 일시 중지 스레드에서 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 메서드를 호출하는 다른 스레드에 의해 중단될 때까지 또는 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 메서드 호출에 의해 종료될 때까지 스레드가 일시 중지됩니다.  다음 예제에서는 대기 중인 스레드를 중단하는 두 가지 메서드를 보여 줍니다.  
  
 [!code-csharp[Conceptual.Threading.Resuming#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.Threading.Resuming/cs/Sleep1.cs#1)]
 [!code-vb[Conceptual.Threading.Resuming#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.Threading.Resuming/vb/Sleep1.vb#1)]  
  
## <a name="interrupting-threads"></a>스레드 중단

 차단된 스레드에서 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 메서드를 호출하여 <xref:System.Threading.ThreadInterruptedException>을 throw하면 스레드가 차단 호출에서 분리되어 대기 스레드를 중단할 수 있습니다. 스레드는 <xref:System.Threading.ThreadInterruptedException>을 catch하고 작업을 계속하는 데 필요한 동작을 수행해야 합니다. 스레드가 예외를 무시하는 경우 런타임은 예외를 catch하고 스레드를 중지합니다.  
  
> [!NOTE]
>  <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType>를 호출할 때 대상 스레드가 차단되지 않는 경우 스레드는 차단될 때까지 중단되지 않습니다. 스레드가 차단되지 않으면 중단 없이 완료될 수 있습니다.  
  
 대기가 관리되는 대기인 경우 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 둘 다 스레드를 즉시 깨웁니다. 대기가 관리되지 않는 대기인 경우(예: Win32 [WaitForSingleObject](/windows/desktop/api/synchapi/nf-synchapi-waitforsingleobject) 함수에 대한 플랫폼 호출) 스레드가 관리 코드로 반환되거나 호출할 때까지 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>는 스레드를 제어할 수 없습니다. 관리 코드에서 동작은 다음과 같습니다.  
  
-   <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType>는 대기 상태에서 스레드를 깨우고 대상 스레드에서 <xref:System.Threading.ThreadInterruptedException>이 발생하게 합니다.  
  
-   <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>는 대기 상태에서 스레드를 깨우고 스레드에서 <xref:System.Threading.ThreadAbortException>을 throw합니다. 자세한 내용은 [스레드 제거](../../../docs/standard/threading/destroying-threads.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Thread>  
- <xref:System.Threading.ThreadInterruptedException>  
- <xref:System.Threading.ThreadAbortException>  
- [스레딩](../../../docs/standard/threading/index.md)  
- [스레드 및 스레딩 사용](../../../docs/standard/threading/using-threads-and-threading.md)  
- [동기화 기본 형식 개요](../../../docs/standard/threading/overview-of-synchronization-primitives.md)
