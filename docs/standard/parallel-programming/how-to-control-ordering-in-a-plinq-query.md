---
title: '방법: PLINQ 쿼리의 순서 제어'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to control ordering
ms.assetid: c67eccc7-004d-4b2f-987e-919cbbd62ef7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7416f2f9c200d687d3f2c1f14b01cafdb48f85b1
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988193"
---
# <a name="how-to-control-ordering-in-a-plinq-query"></a>방법: PLINQ 쿼리의 순서 제어
다음 예제는 <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 확장 메서드를 사용하여 PLINQ 쿼리에서 순서를 제어하는 방법을 보여줍니다.  
  
> [!WARNING]
> 이 예제는 주로 사용법을 보여 주기 위해 제공되며 동일한 순차적 LINQ to Objects 쿼리보다 빠르게 실행되거나 실행되지 않을 수 있습니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 소스 시퀀스의 순서를 유지합니다. 때때로 이 작업이 필요합니다. 예를 들어 일부 쿼리 연산자에는 올바른 결과를 생성하려면 순서가 지정된 소스 시퀀스가 필요합니다.  
  
 [!code-csharp[PLINQ#12](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#12)]
 [!code-vb[PLINQ#12](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#12)]  
  
## <a name="example"></a>예  
 다음 예제는 소스 시퀀스의 순서가 지정되어야 할 수 있는 일부 쿼리 연산자를 보여줍니다. 이러한 연산자는 순서가 지정되지 않은 시퀀스에서 작동하지만 예기치 않은 결과를 생성할 수 있습니다.  
  
 [!code-csharp[PLINQ#14](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#14)]
 [!code-vb[PLINQ#14](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#14)]  
  
 이 메서드를 실행하려면 [PLINQ 데이터 샘플](../../../docs/standard/parallel-programming/plinq-data-sample.md) 프로젝트의 PLINQDataSample 클래스에 붙여넣고 F5 키를 누릅니다.  
  
## <a name="example"></a>예  
 다음 예제는 쿼리의 첫 번째 부분에 대한 순서를 유지하고, 순서를 제거하여 조인 절의 성능을 향상한 다음, 마지막 결과 시퀀스에 순서를 다시 적용하는 방법을 보여줍니다.  
  
 [!code-csharp[PLINQ#15](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#15)]
 [!code-vb[PLINQ#15](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#15)]  
  
 이 메서드를 실행하려면 [PLINQ 데이터 샘플](../../../docs/standard/parallel-programming/plinq-data-sample.md) 프로젝트의 PLINQDataSample 클래스에 붙여넣고 F5 키를 누릅니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq.ParallelEnumerable>
- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
