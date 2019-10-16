---
title: SpinWait
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- synchronization primitives, SpinWait
ms.assetid: 36012f42-34e5-4f86-adf4-973f433ed6c6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9b66ec913a6e8726710d90737f97c04335ae6e4f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54676434"
---
# <a name="spinwait"></a>SpinWait
<xref:System.Threading.SpinWait?displayProperty=nameWithType>는 커널 이벤트에 필요한 비용이 많이 드는 컨텍스트 스위치 및 커널 전환을 방지하기 위해 하위 수준 시나리오에서 사용할 수 있는 단순한 동기화 유형입니다. 멀티 코어 컴퓨터에서, 리소스를 장기간 보유하지 않아도 되는 경우 몇십 번 또는 몇백 번의 주기 동안 대기 스레드가 사용자 모드에서 회전한 다음, 리소스를 획득하려고 시도하는 것이 더 효율적일 수 있습니다. 회전 후에 리소스가 사용 가능해지면 몇천 번의 주기를 절약하는 것입니다. 리소스를 여전히 사용할 수 없는 경우에는 몇 번의 주기만 사용한 것이며 커널 기반의 대기를 계속 입력할 수 있습니다. 이 회전 후 대기 조합을 ‘2단계 대기 작업’이라고도 합니다.  
  
 <xref:System.Threading.SpinWait>는 <xref:System.Threading.ManualResetEvent>와 같은 커널 이벤트를 래핑하는 .NET Framework 유형과 함께 사용하도록 설계되었습니다. <xref:System.Threading.SpinWait>는 한 프로그램의 기본 회전 기능에 대해 자동으로 사용될 수도 있습니다.  
  
 <xref:System.Threading.SpinWait>는 빈 루프보다 큽니다. 일반적인 경우에는 올바른 회전 동작을 제공하도록 신중하게 구현되며, 충분히(대략 커널 전환에 필요한 시간 동안) 회전하는 경우 컨텍스트 스위치를 자동으로 시작합니다. 예를 들어 단일 코어 컴퓨터에서는, 회전 블록이 모든 스레드에서 진행되므로 <xref:System.Threading.SpinWait>가 스레드의 시간 조각을 즉시 생성합니다. 또한 <xref:System.Threading.SpinWait>은 대기 스레드가 우선 순위가 높은 스레드 또는 가비지 수집기를 차단하는 것을 방지하기 위해 멀티 코어 컴퓨터에서도 생성합니다. 따라서 2단계 대기 작업에서 <xref:System.Threading.SpinWait>를 사용하는 경우, <xref:System.Threading.SpinWait>가 자동으로 컨텍스트 스위치를 시작하기 전에 커널 대기를 호출하는 것이 좋습니다. <xref:System.Threading.SpinWait>는 <xref:System.Threading.SpinWait.NextSpinWillYield%2A> 속성을 제공합니다. 이 속성은 <xref:System.Threading.SpinWait.SpinOnce%2A>에 대한 모든 호출 전에 확인할 수 있습니다. 속성에서 `true`를 반환하면 고유한 대기 작업을 시작하세요. 예는 [방법: SpinWait을 사용하여 2단계 대기 작업 구현](../../../docs/standard/threading/how-to-use-spinwait-to-implement-a-two-phase-wait-operation.md)을 참조하세요.  
  
 2단계 대기 작업을 수행하지 않지만 일부 조건이 true가 될 때까지 회전하는 경우, Windows 운영 체제 환경에 적합하게 되도록 <xref:System.Threading.SpinWait>가 자신의 컨텍스트 스위치를 수행하도록 할 수 있습니다. 다음 기본 예제는 잠금 해제 스택의 <xref:System.Threading.SpinWait>를 보여줍니다. 스레드로부터 안전한 고성능 스택이 필요한 경우 <xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=nameWithType>을 사용하세요.  
  
 [!code-csharp[CDS_SpinWait#05](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinwait/cs/spinwait.cs#05)]
 [!code-vb[CDS_SpinWait#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinwait/vb/cds_spinwait1.vb#05)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Thread.SpinWait%2A>
- [스레딩 개체 및 기능](../../../docs/standard/threading/threading-objects-and-features.md)
