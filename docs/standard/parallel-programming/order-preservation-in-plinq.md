---
title: PLINQ에서 순서 유지
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, order preservation
ms.assetid: 10d202bc-19e1-4b5c-bbf1-9a977322a9ca
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1ddb6a5534eb7ef2dc823ac05e03d3b2d3d0cee7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623964"
---
# <a name="order-preservation-in-plinq"></a>PLINQ에서 순서 유지
PLINQ에서 목표는 정확성을 유지하면서 성능을 최대화하는 것입니다. 쿼리는 가능한 한 빠르게 실행되지만 올바른 결과를 생성해야 합니다. 경우에 따라 정확성을 위해 소스 시퀀스의 순서를 유지해야 하지만 순서 지정의 계산 비용이 높을 수 있습니다. 따라서 기본적으로 PLINQ는 소스 시퀀스의 순서를 유지하지 않습니다. 이와 관련하여 PLINQ는 [!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)]과 비슷하지만 순서를 유지하는 LINQ to Objects와는 다릅니다.  
  
 기본 동작을 재정의하려면 소스 시퀀스에서 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 연산자를 사용하여 순서 유지 기능을 켤 수 있습니다. 그런 다음, <xref:System.Linq.ParallelEnumerable.AsUnordered%2A> 메서드를 사용하여 쿼리에서 나중에 순서 유지 기능을 끌 수 있습니다. 두 메서드를 모두 사용하면 쿼리를 병렬로 실행할지 또는 순차적으로 실행할지 여부를 결정하는 추론을 기반으로 쿼리가 처리됩니다. 자세한 내용은 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)를 참조하세요.  
  
 다음 예제는 어떤 방식으로든 결과의 순서를 지정하지 않고 조건과 일치하는 모든 요소에 대해 필터링되는 순서가 지정되지 않은 병렬 쿼리를 보여줍니다.  
  
 [!code-csharp[PLINQ#8](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#8)]
 [!code-vb[PLINQ#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#8)]  
  
 이 쿼리는 조건을 충족하는 처음 1000개 도시를 소스 시퀀스에서 생성하기보다는 조건을 충족하는 1000개 도시 집합을 생성합니다. PLINQ 쿼리 연산자는 소스 시퀀스를 동시 작업으로 처리되는 여러 하위 시퀀스로 분할합니다. 순서 유지를 지정하지 않으면 각 파티션의 결과가 쿼리의 다음 단계에 임의 순서로 전달됩니다. 또한 파티션이 나머지 요소를 계속 처리하기 전에 결과 하위 집합을 생성할 수 있습니다. 결과 순서는 매번 다를 수 있습니다. 순서는 운영 체제가 스레드를 예약하는 방법에 따라 다르므로 애플리케이션이 순서를 제어할 수 없습니다.  
  
 다음 예제에서는 소스 시퀀스에서 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 연산자를 사용하여 기본 동작을 재정의합니다. 이렇게 하면 <xref:System.Linq.ParallelEnumerable.Take%2A> 메서드가 소스 시퀀스에서 조건을 충족하는 처음 1000개의 도시를 반환합니다.  
  
 [!code-csharp[PLINQ#9](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#9)]
 [!code-vb[PLINQ#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#9)]  
  
 그러나 이 쿼리는 전체 파티션에서 원래 순서를 추적하고 병합 시 순서가 일치하는지 확인해야 하므로 순서가 지정되지 않은 버전만큼 빠르게 실행되지 않을 수 있습니다. 따라서 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A>는 필요한 경우에만, 그리고 필요한 쿼리의 파트에만 사용하는 것이 좋습니다. 순서 유지가 더 이상 필요하지 않으면 <xref:System.Linq.ParallelEnumerable.AsUnordered%2A>를 사용하여 기능을 끕니다. 다음 예제에서는 두 개의 쿼리를 작성하여 이 작업을 수행합니다.  
  
 [!code-csharp[PLINQ#6](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#6)]
 [!code-vb[PLINQ#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#6)]  
  
 PLINQ는 나머지 쿼리에 대해 순서 포함 연산자에 의해 생성된 시퀀스의 순서를 유지합니다. 즉, <xref:System.Linq.ParallelEnumerable.OrderBy%2A> 및 <xref:System.Linq.ParallelEnumerable.ThenBy%2A> 같은 연산자는 뒤에 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A>에 대한 호출이 실행되는 것처럼 처리됩니다.  
  
## <a name="query-operators-and-ordering"></a>쿼리 연산자 및 순서 지정  
 다음 쿼리 연산자는 순서 유지를 쿼리의 모든 후속 작업에 포함하거나 <xref:System.Linq.ParallelEnumerable.AsUnordered%2A>가 호출될 때까지 포함합니다.  
  
- <xref:System.Linq.ParallelEnumerable.OrderBy%2A>  
  
- <xref:System.Linq.ParallelEnumerable.OrderByDescending%2A>  
  
- <xref:System.Linq.ParallelEnumerable.ThenBy%2A>  
  
- <xref:System.Linq.ParallelEnumerable.ThenByDescending%2A>  
  
 다음 PLINQ 쿼리 연산자는 올바른 결과를 생성하기 위해 경우에 따라 순서가 지정된 소스 시퀀스가 필요할 수 있습니다.  
  
- <xref:System.Linq.ParallelEnumerable.Reverse%2A>  
  
- <xref:System.Linq.ParallelEnumerable.SequenceEqual%2A>  
  
- <xref:System.Linq.ParallelEnumerable.TakeWhile%2A>  
  
- <xref:System.Linq.ParallelEnumerable.SkipWhile%2A>  
  
- <xref:System.Linq.ParallelEnumerable.Zip%2A>  
  
 일부 PLINQ 쿼리 연산자는 소스 시퀀스의 순서가 지정되거나 순서가 지정되지 않았는지에 따라 다르게 동작합니다. 다음 표에 이러한 연산자가 나와 있습니다.  
  
|연산자|소스 시퀀스의 순서가 지정된 경우의 결과|소스 시퀀스의 순서가 지정되지 않은 경우의 결과|  
|--------------|------------------------------------------------|--------------------------------------------------|  
|<xref:System.Linq.ParallelEnumerable.Aggregate%2A>|비연관 또는 비누적 작업에 대한 비결정적 출력|비연관 또는 비누적 작업에 대한 비결정적 출력|  
|<xref:System.Linq.ParallelEnumerable.All%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.Any%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.AsEnumerable%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.Average%2A>|비연관 또는 비누적 작업에 대한 비결정적 출력|비연관 또는 비누적 작업에 대한 비결정적 출력|  
|<xref:System.Linq.ParallelEnumerable.Cast%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Concat%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Count%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.DefaultIfEmpty%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.Distinct%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.ElementAt%2A>|지정된 요소 반환|임의 요소|  
|<xref:System.Linq.ParallelEnumerable.ElementAtOrDefault%2A>|지정된 요소 반환|임의 요소|  
|<xref:System.Linq.ParallelEnumerable.Except%2A>|순서가 지정되지 않은 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.First%2A>|지정된 요소 반환|임의 요소|  
|<xref:System.Linq.ParallelEnumerable.FirstOrDefault%2A>|지정된 요소 반환|임의 요소|  
|<xref:System.Linq.ParallelEnumerable.ForAll%2A>|병렬로 비결정적으로 실행|병렬로 비결정적으로 실행|  
|<xref:System.Linq.ParallelEnumerable.GroupBy%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.GroupJoin%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Intersect%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Join%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Last%2A>|지정된 요소 반환|임의 요소|  
|<xref:System.Linq.ParallelEnumerable.LastOrDefault%2A>|지정된 요소 반환|임의 요소|  
|<xref:System.Linq.ParallelEnumerable.LongCount%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.Min%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.OrderBy%2A>|시퀀스의 순서 변경|새 순서가 지정된 섹션 시작|  
|<xref:System.Linq.ParallelEnumerable.OrderByDescending%2A>|시퀀스의 순서 변경|새 순서가 지정된 섹션 시작|  
|<xref:System.Linq.ParallelEnumerable.Range%2A>|적용할 수 없음(<xref:System.Linq.ParallelEnumerable.AsParallel%2A>과 동일한 기본값)|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.Repeat%2A>|적용할 수 없음(<xref:System.Linq.ParallelEnumerable.AsParallel%2A>과 동일한 기본값)|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.Reverse%2A>|역방향 순서 지정|아무 작업도 수행하지 않습니다.|  
|<xref:System.Linq.ParallelEnumerable.Select%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Select%2A>(인덱싱됨)|순서가 지정된 결과|순서가 지정되지 않은 결과.|  
|<xref:System.Linq.ParallelEnumerable.SelectMany%2A>|순서가 지정된 결과.|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.SelectMany%2A>(인덱싱됨)|순서가 지정된 결과.|순서가 지정되지 않은 결과.|  
|<xref:System.Linq.ParallelEnumerable.SequenceEqual%2A>|순서가 지정된 비교|순서가 지정되지 않은 비교|  
|<xref:System.Linq.ParallelEnumerable.Single%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.SingleOrDefault%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.Skip%2A>|처음 *n*개 요소를 건너뜀|임의 *n*개 요소를 건너뜀|  
|<xref:System.Linq.ParallelEnumerable.SkipWhile%2A>|순서가 지정된 결과.|비결정적. 현재 임의 순서로 SkipWhile 수행|  
|<xref:System.Linq.ParallelEnumerable.Sum%2A>|비연관 또는 비누적 작업에 대한 비결정적 출력|비연관 또는 비누적 작업에 대한 비결정적 출력|  
|<xref:System.Linq.ParallelEnumerable.Take%2A>|처음 `n`개 요소 사용|임의 `n`개 요소 사용|  
|<xref:System.Linq.ParallelEnumerable.TakeWhile%2A>|순서가 지정된 결과|비결정적. 현재 임의 순서로 TakeWhile 수행|  
|<xref:System.Linq.ParallelEnumerable.ThenBy%2A>|`OrderBy` 보완|`OrderBy` 보완|  
|<xref:System.Linq.ParallelEnumerable.ThenByDescending%2A>|`OrderBy` 보완|`OrderBy` 보완|  
|<xref:System.Linq.ParallelEnumerable.ToArray%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.ToDictionary%2A>|적용할 수 없음|적용할 수 없음|  
|<xref:System.Linq.ParallelEnumerable.ToList%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.ToLookup%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Union%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Where%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Where%2A>(인덱싱됨)|순서가 지정된 결과|순서가 지정되지 않은 결과|  
|<xref:System.Linq.ParallelEnumerable.Zip%2A>|순서가 지정된 결과|순서가 지정되지 않은 결과|  
  
 순서가 지정되지 않은 결과는 순서가 활발히 바뀌지 않습니다. 특별한 순서 지정 논리가 적용되지 않습니다. 경우에 따라 순서가 지정되지 않은 쿼리가 소스 시퀀스의 순서를 유지할 수 있습니다. 인덱싱된 Select 연산자를 사용하는 쿼리의 경우 PLINQ는 출력 요소가 인덱스 증가 순서로 표시되도록 보장하지만 어떤 인덱스가 어떤 요소에 할당되는지에 대한 보장은 하지 않습니다.  
  
## <a name="see-also"></a>참고 항목

- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
