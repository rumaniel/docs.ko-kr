---
title: '방법: PLINQ에서 병합 옵션 지정'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to use merge options
ms.assetid: 0f33b527-e91a-4550-a39a-e63e396fd831
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 947f3cb15b7eb372d20884ece73374114c48f472
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988844"
---
# <a name="how-to-specify-merge-options-in-plinq"></a>방법: PLINQ에서 병합 옵션 지정
이 예제는 PLINQ 쿼리의 모든 후속 연산자에 적용할 병합 옵션을 지정하는 방법을 보여줍니다. 병합 옵션을 명시적으로 설정할 필요는 없지만 이를 수행하면 성능이 향상될 수 있습니다. 병합 옵션에 대한 자세한 내용은 [PLINQ의 병합 옵션](../../../docs/standard/parallel-programming/merge-options-in-plinq.md)을 참조하세요.  
  
> [!WARNING]
> 이 예제는 사용법을 보여 주기 위한 것이며, 동일한 순차 LINQ to Objects 쿼리보다 빠르게 실행되지 않을 수도 있습니다. 속도 향상에 대한 자세한 내용은 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)를 참조하세요.  
  
## <a name="example"></a>예  
 다음 예제에서는 정렬되지 않은 소스가 있는 기본 시나리오의 병합 옵션 동작을 보여주고 모든 요소에 비용이 많이 드는 함수를 적용합니다.  
  
 [!code-csharp[PLINQ#23](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#23)]
 [!code-vb[PLINQ#23](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#23)]  
  
 첫 번째 요소가 생성되기 전에 <xref:System.Linq.ParallelMergeOptions.AutoBuffered> 옵션이 바람직하지 않은 대기 시간을 발생시키는 경우, <xref:System.Linq.ParallelMergeOptions.NotBuffered> 옵션을 사용하여 결과 요소를 더욱 빠르고 원활하게 실행하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq.ParallelMergeOptions>
- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
