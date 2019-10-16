---
title: '방법: 사용자 지정 PLINQ 집계 함수 작성'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to create aggregate function
ms.assetid: 5a70dd49-ab2a-4798-b551-196ee7042b1a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 09e128c98b61ecc4ac673d8c9911f4bac476d521
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988437"
---
# <a name="how-to-write-a-custom-plinq-aggregate-function"></a>방법: 사용자 지정 PLINQ 집계 함수 작성
이 예제는 <xref:System.Linq.ParallelEnumerable.Aggregate%2A> 메서드를 사용하여 소스 시퀀스에 사용자 지정 집계 함수를 적용하는 방법을 보여줍니다.  
  
> [!WARNING]
> 이 예제는 사용법을 보여 주기 위한 것이며, 동일한 순차 LINQ to Objects 쿼리보다 빠르게 실행되지 않을 수도 있습니다. 속도 향상에 대한 자세한 내용은 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)를 참조하세요.  
  
## <a name="example"></a>예  
 다음 예제는 정수 시퀀스의 표준 편차를 계산합니다.  
  
 [!code-csharp[PLINQ#31](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#31)]
 [!code-vb[PLINQ#31](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#31)]  
  
 이 예제에서는 PLINQ에 고유한 집계 표준 쿼리 연산자의 오버로드를 사용합니다. 이 오버로드는 세 번째 입력 매개 변수로 추가 <xref:System.Func%603?displayProperty=nameWithType>를 사용합니다. 이 대리자는 집계 결과에 대한 최종 계산을 수행하기 전에 모든 스레드의 결과를 결합합니다. 이 예제에서는 모든 스레드의 합계를 함께 더합니다.  
  
 람다 식 본문이 단일식으로 구성된 경우 <xref:System.Func%602?displayProperty=nameWithType> 대리자의 반환 값은 식의 값입니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq.ParallelEnumerable>
- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
