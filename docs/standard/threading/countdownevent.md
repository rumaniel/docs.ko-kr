---
title: CountdownEvent
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- synchronization primitives, CountdownEvent
ms.assetid: eec3812a-e20f-4ecd-bfef-6921d508b708
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ac1f2283ad30499748511e6fed6d5ce98da7fd14
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960103"
---
# <a name="countdownevent"></a>CountdownEvent
<xref:System.Threading.CountdownEvent?displayProperty=nameWithType>는 특정 횟수만큼 신호를 받은 후 대기 스레드를 차단 해제하는 동기화 기본 형식입니다. <xref:System.Threading.CountdownEvent>는 <xref:System.Threading.ManualResetEvent> 또는 <xref:System.Threading.ManualResetEventSlim>을 사용하여 이벤트에 신호를 보내기 전에 변수를 수동으로 감소시켜야 하는 시나리오를 위해 설계되었습니다. 예를 들어, 포크/조인 시나리오에서 신호 수가 5인 <xref:System.Threading.CountdownEvent>을 생성한 다음, 스레드 풀에서 5개의 작업 항목을 시작하고 완료될 때 각 작업 항목이 <xref:System.Threading.CountdownEvent.Signal%2A>을 호출하도록 할 수 있습니다. <xref:System.Threading.CountdownEvent.Signal%2A>을 호출할 때마다 신호 수가 1씩 감소됩니다. 주 스레드에서 <xref:System.Threading.CountdownEvent.Wait%2A>에 대한 호출은 신호 수가 0일 때까지 차단됩니다.  
  
> [!NOTE]
> 레거시 .NET Framework 동기화 API와 상호 작용할 필요가 없는 코드의 경우, 포크-조인 병렬 처리를 더 쉽게 표현할 수 있도록 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 개체 또는 <xref:System.Threading.Tasks.Parallel.Invoke%2A> 메서드를 사용하는 것이 좋습니다.  
  
 <xref:System.Threading.CountdownEvent>에는 다음과 같은 추가 기능이 있습니다.  
  
- 취소 토큰을 사용하여 대기 작업을 취소할 수 있습니다.  
  
- 인스턴스가 생성된 후에는 신호 수가 증가할 수 있습니다.  
  
- <xref:System.Threading.CountdownEvent.Wait%2A>가 <xref:System.Threading.CountdownEvent.Reset%2A> 메서드를 호출하여 반환한 후 인스턴스를 재사용할 수 있습니다.  
  
- 인스턴스는 <xref:System.Threading.WaitHandle.WaitAll%2A>와 같은 다른 .NET Framework 동기화 API와의 통합을 위해 <xref:System.Threading.WaitHandle>을 표시합니다.  
  
## <a name="basic-usage"></a>기본 사용  
 다음 예제는 <xref:System.Threading.ThreadPool> 작업 항목에 <xref:System.Threading.CountdownEvent>를 사용하는 방법을 보여줍니다.  
  
 [!code-csharp[CDS_CountdownEvent#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#01)]
 [!code-vb[CDS_CountdownEvent#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/module1.vb#01)]  
  
## <a name="countdownevent-with-cancellation"></a>취소를 사용하는 CountdownEvent  
 다음 예제는 취소 토큰을 사용하여 <xref:System.Threading.CountdownEvent>에서 대기 작업을 취소하는 방법을 보여줍니다. 기본 패턴은 .NET Framework 4에 도입된 통합 취소를 위한 모델을 따릅니다. 자세한 내용은 [관리되는 스레드의 취소](../../../docs/standard/threading/cancellation-in-managed-threads.md)를 참조하세요.  
  
 [!code-csharp[CDS_CountdownEvent#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#02)]
 [!code-vb[CDS_CountdownEvent#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/canceleventwait.vb#02)]  
  
 대기 작업은 해당 작업에 신호를 보내는 스레드를 취소하지 않습니다. 일반적으로 취소는 논리 연산에 적용되며, 이벤트에 대한 대기뿐만 아니라 대기가 동기화 중인 모든 작업 항목도 포함할 수 있습니다. 이 예제에서는 취소 요청에 응답할 수 있도록 작업 항목에 동일한 취소 토큰의 사본이 전달됩니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Semaphore?displayProperty=nameWithType>
