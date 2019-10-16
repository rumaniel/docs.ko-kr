---
title: PLINQ의 병합 옵션
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, merge options
ms.assetid: e8f7be3b-88de-4f33-ab14-dc008e76c1ba
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7255ef11bfdf74afa6ae2032b0c86c8c44dbfe7d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647735"
---
# <a name="merge-options-in-plinq"></a>PLINQ의 병합 옵션
쿼리가 병렬로 실행되는 경우 여러 스레드가 동시에 여러 파트에서(보통 개별 스레드에서) 작동할 수 있도록 PLINQ가 소스 시퀀스를 분할합니다. 결과를 `foreach`(Visual Basic의 `For Each`) 루프와 같은 한 스레드에서 사용할 경우 모든 스레드의 결과를 하나의 시퀀스로 다시 병합해야 합니다. PLINQ가 수행하는 병합의 종류는 쿼리에 있는 연산자에 따라 다릅니다. 예를 들어, 결과에 새 순서를 부과하는 연산자는 모든 스레드의 모든 요소를 버퍼링해야 합니다. 소비 스레드의 관점에서(또한 애플리케이션 사용자의 관점에서) 완전히 버퍼링된 쿼리는 첫 번째 결과를 생성하기 전에 한동안 실행될 수 있습니다. 다른 연산자는 기본적으로, 부분적으로 버퍼링되므로 일괄 처리로 결과가 생성됩니다. <xref:System.Linq.ParallelEnumerable.ForAll%2A> 연산자는 기본적으로 버퍼링되지 않습니다. 이 연산자는 모든 스레드에서 모든 요소를 즉시 생성합니다.  
  
 다음 예와 같이 <xref:System.Linq.ParallelEnumerable.WithMergeOptions%2A> 메서드를 사용하여 수행할 병합 종류를 나타내는 힌트를 PLINQ에 제공할 수 있습니다.  
  
 [!code-csharp[PLINQ#26](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#26)]
 [!code-vb[PLINQ#26](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#26)]  
  
 전체 예제는 [방법: PLINQ에서 병합 옵션 지정](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)을 참조하세요.  
  
 특정 쿼리가 요청된 옵션을 지원할 수 없는 경우에는 옵션이 무시됩니다. 대부분의 경우 PLINQ 쿼리의 병합 옵션을 지정할 필요가 없습니다. 그러나 어떤 경우에는 쿼리가 기본이 아닌 모드에서 가장 잘 실행한다는 것을 테스트 및 측정을 통해 확인할 수 있습니다. 이 옵션의 일반적인 용도는 응답성이 높은 사용자 인터페이스를 제공하기 위해 청크 병합 연산자가 결과를 스트리밍하도록 강제하는 것입니다.  
  
## <a name="parallelmergeoptions"></a>ParallelMergeOptions  
 <xref:System.Linq.ParallelMergeOptions> 열거에는 지원되는 쿼리 형태에 대해 결과가 한 스레드에서 사용될 때 쿼리의 최종 출력이 어떻게 생성되는지를 지정하는 다음 옵션이 포함됩니다.  
  
- `Not Buffered`  
  
     <xref:System.Linq.ParallelMergeOptions.NotBuffered> 옵션을 사용하면 처리된 각 요소가 생성되는 즉시 각 스레드에서 반환됩니다. 이 동작은 출력을 “스트리밍”하는 것과 유사합니다. 쿼리에 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 연산자가 있는 경우 `NotBuffered`는 소스 요소의 순서를 유지합니다. `NotBuffered`는 사용 가능하게 되는 즉시 결과를 생성하기 시작하지만 모든 결과를 생성하는 데 걸리는 총 시간이 다른 병합 옵션 중 하나를 사용하는 경우보다 오래 걸릴 수 있습니다.  
  
- `Auto Buffered`  
  
     <xref:System.Linq.ParallelMergeOptions.AutoBuffered> 옵션을 사용하면 쿼리에서는 요소를 버퍼에 수집한 다음 정기적으로 버퍼 내용을 모두 한꺼번에 소비 스레드로 내보냅니다. 이는 `NotBuffered`의 “스트리밍” 동작을 사용하는 대신 “청크”의 소스 데이터를 생성하는 것과 유사합니다. `AutoBuffered`는 소비 스레드에서 첫 번째 요소를 사용 가능하도록 설정하는 데 `NotBuffered`보다 오래 걸릴 수 있습니다. 버퍼 크기 및 정확한 생성 동작은 구성할 수 없으며 쿼리와 관련된 다양한 요소에 따라 다를 수 있습니다.  
  
- `FullyBuffered`  
  
     <xref:System.Linq.ParallelMergeOptions.FullyBuffered> 옵션을 사용하면 요소가 생성되기 전에 전체 쿼리 출력이 버퍼링됩니다. 이 옵션을 사용하면 첫 번째 요소가 소비 스레드에서 사용 가능하게 되기 전까지 오래 걸릴 수 있지만 전체 결과는 다른 옵션을 사용하여 더 빨리 생성될 수 있습니다.  
  
## <a name="query-operators-that-support-merge-options"></a>병합 옵션을 지원하는 쿼리 연산자  
 다음 표에서는 지정된 제한 사항에 따라 모든 병합 옵션 모드를 지원하는 연산자를 나열합니다.  
  
|연산자|제한|  
|--------------|------------------|  
|<xref:System.Linq.ParallelEnumerable.AsEnumerable%2A>|없음|  
|<xref:System.Linq.ParallelEnumerable.Cast%2A>|없음|  
|<xref:System.Linq.ParallelEnumerable.Concat%2A>|배열 또는 목록 소스만 있는 순서가 지정되지 않은 쿼리입니다.|  
|<xref:System.Linq.ParallelEnumerable.DefaultIfEmpty%2A>|없음|  
|<xref:System.Linq.ParallelEnumerable.OfType%2A>|없음|  
|<xref:System.Linq.ParallelEnumerable.Reverse%2A>|배열 또는 목록 소스만 있는 순서가 지정되지 않은 쿼리입니다.|  
|<xref:System.Linq.ParallelEnumerable.Select%2A>|없음|  
|<xref:System.Linq.ParallelEnumerable.SelectMany%2A>|없음|  
|<xref:System.Linq.ParallelEnumerable.Skip%2A>|없음|  
|<xref:System.Linq.ParallelEnumerable.Take%2A>|없음|  
|<xref:System.Linq.ParallelEnumerable.Where%2A>|없음|  
  
 다른 모든 PLINQ 쿼리 연산자는 사용자 제공 병합 옵션을 무시할 수 있습니다. 일부 쿼리 연산자(예: <xref:System.Linq.ParallelEnumerable.Reverse%2A> 및 <xref:System.Linq.ParallelEnumerable.OrderBy%2A>)는 모두 생성되어 다시 정렬될 때까지 요소를 생성할 수 없습니다. 따라서 <xref:System.Linq.ParallelEnumerable.Reverse%2A>와 같은 연산자도 포함된 쿼리에서 <xref:System.Linq.ParallelMergeOptions>를 사용하는 경우 해당 연산자가 결과를 생성할 때까지 병합 동작이 쿼리에 적용되지 않습니다.  
  
 병합 옵션을 처리하는 일부 연산자의 기능은 소스 시퀀스의 유형과 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 연산자가 쿼리에서 이전에 사용되었는지 여부에 따라 다릅니다. <xref:System.Linq.ParallelEnumerable.ForAll%2A>은 항상 <xref:System.Linq.ParallelMergeOptions.NotBuffered>이므로 해당 요소를 즉시 생성합니다. <xref:System.Linq.ParallelEnumerable.OrderBy%2A>는 항상 <xref:System.Linq.ParallelMergeOptions.FullyBuffered>입니다. 이 연산자는 생성하기 전에 전체 목록을 정렬해야 합니다.  
  
## <a name="see-also"></a>참고 항목

- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
- [방법: PLINQ에서 병합 옵션 지정](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)
