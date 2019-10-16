---
title: '방법: 간단한 PLINQ 쿼리 만들기 및 실행'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to create
ms.assetid: 983b4213-bddd-4a44-9262-cbe59186df4c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 472304dff23e92620dd461e8bc43c3093431ddc4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962524"
---
# <a name="how-to-create-and-execute-a-simple-plinq-query"></a>방법: 간단한 PLINQ 쿼리 만들기 및 실행
다음 예제에서는 소스 시퀀스에 대해 <xref:System.Linq.ParallelEnumerable.AsParallel%2A> 확장명 메서드를 사용하여 단순한 병렬 LINQ 쿼리를 만들고 <xref:System.Linq.ParallelEnumerable.ForAll%2A> 메서드를 사용하여 쿼리를 실행하는 방법을 보여 줍니다.  
  
> [!NOTE]
> 이 문서에서는 람다 식을 사용하여 PLINQ에 대리자를 정의합니다. C# 또는 Visual Basic의 람다 식을 잘 모르는 경우 [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)을 참조하세요.  
  
## <a name="example"></a>예  
 [!code-csharp[PLINQ#11](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/create1.cs#11)]
 [!code-vb[PLINQ#11](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/create1.vb#11)]  
  
 이 예제에서는 결과 시퀀스의 순서가 중요하지 않은 경우(일반적으로 순서가 지정되지 않은 쿼리가 순서가 지정된 쿼리보다 빠름)에 병렬 LINQ 쿼리를 만들고 실행하는 기본 패턴을 보여 줍니다. 쿼리에서는 소스를 여러 스레드에서 비동기적으로 실행되는 작업으로 분할합니다. 각 작업이 완료되는 순서는 파티션의 요소를 처리하는 데 관련된 작업의 양뿐만 아니라 운영 체제에서 각 스레드를 예약하는 방식과 같은 외부 요소에 따라 달라집니다. 이 예제는 사용법을 보여 주기 위한 것이며, 동일한 순차 LINQ to Objects 쿼리보다 빠르게 실행되지 않을 수도 있습니다. 속도 향상에 대한 자세한 내용은 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)를 참조하세요. 쿼리의 요소 순서를 유지하는 방법에 대한 자세한 내용은 [방법: PLINQ 쿼리의 순서 제어](../../../docs/standard/parallel-programming/how-to-control-ordering-in-a-plinq-query.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
