---
title: 장벽
ms.date: 09/14/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- synchronization primitives, Barrier
ms.assetid: 613a8bc7-6a28-4795-bd6c-1abd9050478f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 081a4e66462ab546bf4738b4a8b06a4a2ec91a1d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645029"
---
# <a name="barrier"></a>장벽

<xref:System.Threading.Barrier?displayProperty=nameWithType>은 여러 스레드(‘참가자’라고 함)가 단계별로 알고리즘에서 동시에 작동할 수 있게 해주는 동기화 기본 형식입니다. 각 참가자는 코드의 장벽 지점에 도달할 때까지 실행됩니다. 장벽은 한 작업 단계의 끝을 나타냅니다. 참가자가 장벽에 도달하면 모든 참가자가 동일한 장벽에 도달할 때까지 차단됩니다. 모든 참가자가 장벽에 도달한 후 사후 단계 작업을 필요에 따라 호출할 수 있습니다. 이 사후 단계 작업을 사용하여 다른 모든 스레드는 여전히 차단하는 동시에 단일 스레드에서 작업을 수행할 수 있습니다. 작업이 실행된 후 모든 참가자가 차단 취소됩니다.  
  
 다음 코드 조각에서는 기본 장벽 패턴을 보여 줍니다.  
  
 [!code-csharp[CDS_Barrier#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_barrier/cs/barrier.cs#02)]
 [!code-vb[CDS_Barrier#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_barrier/vb/barrier_vb.vb#02)]  
  
 전체 예제는 [방법: 동시 작업을 장벽과 동기화](how-to-synchronize-concurrent-operations-with-a-barrier.md)를 참조하세요.  
  
## <a name="adding-and-removing-participants"></a>참가자 추가 및 제거

 <xref:System.Threading.Barrier> 인스턴스를 만들 때 참가자 수를 지정합니다. 언제든지 참가자를 동적으로 추가 또는 제거할 수도 있습니다. 예를 들어 한 참가자가 문제의 해당 부분을 해결하는 경우 결과를 저장하고 해당 스레드에서 실행을 중지한 다음, <xref:System.Threading.Barrier.RemoveParticipant%2A?displayProperty=nameWithType>를 호출하여 장벽의 참가자 수를 줄일 수 있습니다. <xref:System.Threading.Barrier.AddParticipant%2A?displayProperty=nameWithType>를 호출하여 참가자를 추가하는 경우 반환 값은 새 참가자의 작업을 초기화하는 데 유용할 수 있는 현재 단계 번호를 지정합니다.  
  
## <a name="broken-barriers"></a>손상된 장벽

 한 참가자가 장벽에 도달하지 못할 경우 교착 상태가 발생할 수 있습니다. 이러한 교착 상태를 방지하려면 <xref:System.Threading.Barrier.SignalAndWait%2A?displayProperty=nameWithType> 메서드의 오버로드를 사용하여 시간 제한 기간 및 취소 토큰을 지정합니다. 이러한 오버로드는 다음 단계로 넘어가기 전에 각 참가자가 확인할 수 있는 부울 값을 반환합니다.  
  
## <a name="post-phase-exceptions"></a>사후 단계 예외

 사후 단계 대리자에서 예외가 발생하는 경우 <xref:System.Threading.BarrierPostPhaseException> 개체에 래핑된 다음 모든 참가자에게 전파됩니다.  
  
## <a name="barrier-versus-continuewhenall"></a>장벽과 ContinueWhenAll 비교

 장벽은 스레드가 루프로 여러 단계를 수행할 때 특히 유용합니다. 코드에 한두 개의 작업 단계만 필요한 경우 다음을 포함하여 임의 종류의 암시적 조인과 함께 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 개체를 사용할지 여부를 고려합니다.  
  
- <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A?displayProperty=nameWithType>  
  
- <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=nameWithType>  
  
- <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType>  
  
- <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType>  
  
 자세한 내용은 [연속 작업을 사용하여 작업 연결](../parallel-programming/chaining-tasks-by-using-continuation-tasks.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [스레딩 개체 및 기능](threading-objects-and-features.md)
- [방법: 동시 작업을 장벽과 동기화](how-to-synchronize-concurrent-operations-with-a-barrier.md)
