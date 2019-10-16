---
title: 데이터 병렬 처리(작업 병렬 라이브러리)
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallelism, data
ms.assetid: 3f05f33f-f1da-4b16-81c2-9ceff1bef449
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 19e518db75fe3e45f57cbb6fab8c5281cceb4d34
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939335"
---
# <a name="data-parallelism-task-parallel-library"></a>데이터 병렬 처리(작업 병렬 라이브러리)
*데이터 병렬 처리*는 소스 컬렉션 또는 배열의 요소에서 동일한 작업이 동시에(즉, 병렬로) 수행되는 시나리오를 가리킵니다. 데이터 병렬 작업에서 소스 컬렉션은 여러 스레드가 서로 다른 세그먼트에서 동시에 작동할 수 있도록 분할됩니다.  
  
 TPL(작업 병렬 라이브러리)은 <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType> 클래스를 통해 데이터 병렬 처리를 지원합니다. 이 클래스는 [for](../../csharp/language-reference/keywords/for.md) 및 [foreach](../../csharp/language-reference/keywords/foreach-in.md) 루프(Visual Basic에서는 `For` 및 `For Each`)의 메서드 기반 병렬 구현을 제공합니다. 순차 루프를 작성하는 것과 마찬가지로 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 또는 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 루프에 대한 루프 논리를 작성합니다. 스레드나 큐 작업 항목을 만들 필요가 없습니다. 기본 루프에서는 잠금을 수행할 필요가 없습니다. TPL에서 모든 하위 수준 작업을 자동으로 처리합니다. <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType>의 용도에 대한 심층 내용은 [병렬 프로그래밍의 패턴: .NET Framework 4의 병렬 패턴 이해 및 적용](https://www.microsoft.com/download/details.aspx?id=19222) 문서를 다운로드하세요. 다음 코드 예제에서는 간단한 `foreach` 루프 및 해당 병렬 루프를 보여 줍니다.  
  
> [!NOTE]
> 이 문서에서는 람다 식을 사용하여 TPL에 대리자를 정의합니다. C# 또는 Visual Basic의 람다 식을 잘 모르는 경우 [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)을 참조하세요.  
  
 [!code-csharp[TPL#20](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#20)]
 [!code-vb[TPL#20](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/tpl_vb.vb#20)]  
  
 병렬 루프가 실행되는 경우 TPL은 루프가 동시에 여러 부분에서 작동할 수 있도록 데이터 소스를 분할합니다. 내부적으로 작업 스케줄러는 시스템 리소스 및 작업에 따라 작업을 분할합니다. 가능한 경우 스케줄러는 작업 불균형이 발생할 때 여러 스레드 및 프로세서 간에 작업을 재배포합니다.  
  
> [!NOTE]
> 고유한 사용자 지정 파티셔너 또는 스케줄러를 제공할 수도 있습니다. 자세한 내용은 [PLINQ 및 TPL에 대한 사용자 지정 파티셔너](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md) 및 [작업 스케줄러](xref:System.Threading.Tasks.TaskScheduler)를 참조하세요.  
  
 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 메서드 둘 다에는 루프 실행을 중지 또는 중단하고, 다른 스레드의 루프 상태를 모니터링하고, 스레드 로컬 상태를 유지 관리하고, 스레드 로컬 개체를 종료하고, 동시성 수준을 제어할 수 있도록 하는 여러 오버로드가 있습니다. 이 기능을 사용할 수 있도록 하는 도우미 형식에는 <xref:System.Threading.Tasks.ParallelLoopState>, <xref:System.Threading.Tasks.ParallelOptions>, <xref:System.Threading.Tasks.ParallelLoopResult>, <xref:System.Threading.CancellationToken> 및 <xref:System.Threading.CancellationTokenSource>가 있습니다.  
  
 자세한 내용은 [병렬 프로그래밍의 패턴: .NET Framework 4의 병렬 패턴 이해 및 적용](https://www.microsoft.com/download/details.aspx?id=19222)을 참조하세요.  
  
 선언적 또는 쿼리와 유사한 구문을 사용한 데이터 병렬 처리는 PLINQ에서 지원됩니다. 자세한 내용은 [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)를 참조하세요.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[방법: 간단한 Parallel.For 루프 작성](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md)|배열 또는 인덱싱 가능한 <xref:System.Collections.Generic.IEnumerable%601> 소스 컬렉션에 대한 <xref:System.Threading.Tasks.Parallel.For%2A> 루프를 작성하는 방법을 설명합니다.|  
|[방법: 간단한 Parallel.ForEach 루프 작성](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-foreach-loop.md)|<xref:System.Collections.Generic.IEnumerable%601> 소스 컬렉션에 대한 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 루프를 작성하는 방법을 설명합니다.|  
|[방법: Parallel.For 루프 중지 또는 중단](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd460721(v=vs.100))|모든 스레드가 작업 알림을 받도록 병렬 루프에서 중지 또는 중단하는 방법을 설명합니다.|  
|[방법: 스레드 로컬 변수를 사용하는 Parallel.For 루프 작성](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md)|각 스레드가 다른 스레드에 표시되지 않는 전용 변수를 유지 관리하는 <xref:System.Threading.Tasks.Parallel.For%2A> 루프를 작성하는 방법 및 루프 완료 시 모든 스레드의 결과를 동기화하는 방법을 설명합니다.|  
|[방법: 파티션 로컬 변수를 사용하는 Parallel.ForEach 루프 작성](../../../docs/standard/parallel-programming/how-to-write-a-parallel-foreach-loop-with-partition-local-variables.md)|각 스레드가 다른 스레드에 표시되지 않는 전용 변수를 유지 관리하는 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 루프를 작성하는 방법 및 루프 완료 시 모든 스레드의 결과를 동기화하는 방법을 설명합니다.|  
|[방법: Parallel.For 또는 ForEach 루프 취소](../../../docs/standard/parallel-programming/how-to-cancel-a-parallel-for-or-foreach-loop.md)|<xref:System.Threading.CancellationToken?displayProperty=nameWithType>을 사용하여 병렬 루프를 취소하는 방법을 설명합니다.|  
|[방법: 작은 루프 본문 속도 개선](../../../docs/standard/parallel-programming/how-to-speed-up-small-loop-bodies.md)|루프 본문이 매우 작을 때 실행을 가속화하는 한 가지 방법을 설명합니다.|  
|[TPL(작업 병렬 라이브러리)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)|작업 병렬 라이브러리에 대해 간략하게 설명합니다.|  
|[병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)|.NET Framework의 병렬 프로그래밍을 소개합니다.|  
  
## <a name="see-also"></a>참고 항목

- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
