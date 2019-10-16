---
title: '방법: PLINQ에 실행 모드 지정'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to use execution mode
ms.assetid: e52ff26c-c5d3-4fab-9fec-c937fb387963
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 705b6bc364e2ecf00c3629814228157c90017a8b
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988448"
---
# <a name="how-to-specify-the-execution-mode-in-plinq"></a>방법: PLINQ에 실행 모드 지정
이 예제에서는 PLINQ가 해당 기본 추론을 강제로 바이패스하게 하여 쿼리 모양에 관계없이 쿼리를 병렬 처리하는 방법을 보여줍니다.  
  
> [!WARNING]
> 이 예제는 사용법을 보여 주기 위한 것이며, 동일한 순차 LINQ to Objects 쿼리보다 빠르게 실행되지 않을 수도 있습니다. 속도 향상에 대한 자세한 내용은 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)를 참조하세요.  
  
## <a name="example"></a>예  
 [!code-csharp[PLINQ#22](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#22)]
 [!code-vb[PLINQ#22](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#22)]  
  
 PLINQ는 병렬 처리 기회를 활용하도록 설계됩니다. 그러나 일부 쿼리는 병렬 실행을 활용하지 않습니다. 예를 들어 작업이 거의 없는 단일 사용자 대리자가 쿼리에 포함될 경우 해당 쿼리는 대개 더 빠르게 순차적으로 실행됩니다. 이는 병렬 실행을 구현하는 데 관련된 오버헤드는 확보된 속도 향상보다 비용이 더 큽니다. 따라서 PLINQ가 모든 쿼리를 자동으로 병렬 처리하는 것은 아닙니다. 먼저 쿼리 모양을 확인하고 쿼리를 구성하는 다양한 연산자를 확인합니다. 이 분석에 따라 기본 실행 모드의 PLINQ는 쿼리의 일부 또는 전체를 순차적으로 실행하도록 결정할 수 있습니다. 그러나 일부 경우에는 PLINQ가 분석에서 확인할 수 있는 것보다 더 많은 쿼리 정보를 사용자가 알고 있을 수 있습니다. 예를 들어 대리자의 비용이 매우 많이 들고 쿼리가 분명히 병렬 처리를 활용할 것이라는 점을 알고 있을 수 있습니다. 이러한 경우에는 <xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A> 메서드를 사용하고 <xref:System.Linq.ParallelExecutionMode.ForceParallelism>을 지정하여 PLINQ가 항상 쿼리를 병렬로 실행하도록 지시할 수 있습니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 코드를 잘라내어 [PLINQ 데이터 샘플](../../../docs/standard/parallel-programming/plinq-data-sample.md)에 붙여넣고 `Main`에서 메서드를 호출합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq.ParallelEnumerable.AsSequential%2A>
- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
