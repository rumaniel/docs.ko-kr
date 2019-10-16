---
title: '방법: PLINQ 쿼리 취소'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to cancel
- cancellation, PLINQ
ms.assetid: 80b14640-edfa-4153-be1b-3e003d3e9c1a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1a90a41b1dc2e5d0b24d3d72b870891238809d75
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046518"
---
# <a name="how-to-cancel-a-plinq-query"></a>방법: PLINQ 쿼리 취소
다음 예제는 PLINQ 쿼리를 취소하는 두 가지 방법을 보여줍니다. 첫 번째 예제에서는 주로 데이터 트래버스로 구성되는 쿼리를 취소하는 방법을 보여줍니다. 두 번째 예제에서는 계산을 많이 해야 하는 사용자 함수를 포함하는 쿼리를 취소하는 방법을 보여줍니다.

> [!NOTE]
> “내 코드만”이 사용하도록 설정된 경우 Visual Studio가 예외를 throw하는 줄에서 중단하고 “예외가 사용자 코드에서 처리되지 않았다”는 오류 메시지를 표시합니다. 이 오류는 심각하지는 않습니다. F5 키를 눌러 계속하고 아래 예제에 설명된 예외 처리 동작을 확인할 수 있습니다. 첫 번째 오류 지점에서 Visual Studio가 실행을 중단하지 않도록 하려면 **도구, 옵션, 디버깅, 일반**을 차례로 선택하고 “내 코드만” 확인란의 선택을 취소하기만 하면 됩니다.
>
> 이 예제는 사용법을 보여 주기 위한 것이며, 동일한 순차 LINQ to Objects 쿼리보다 빠르게 실행되지 않을 수도 있습니다. 속도 향상에 대한 자세한 내용은 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)를 참조하세요.

## <a name="example"></a>예

[!code-csharp[PLINQ#16](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#16)]
[!code-vb[PLINQ#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#16)]

PLINQ 프레임워크는 단일 <xref:System.OperationCanceledException>을 <xref:System.AggregateException?displayProperty=nameWithType>으로 롤링하지 않습니다. <xref:System.OperationCanceledException>은 별도의 catch 블록에서 처리되어야 합니다. 하나 이상의 사용자 대리자가 <xref:System.Threading.CancellationToken?displayProperty=nameWithType>을 사용하여 OperationCanceledException(externalCT)을 throw하지만 다른 예외를 throw하지 않고 쿼리가 `AsParallel().WithCancellation(externalCT)`로 정의된 경우 PLINQ는 <xref:System.AggregateException?displayProperty=nameWithType>이 아닌 단일 <xref:System.OperationCanceledException> (externalCT)을 throw합니다. 그러나 하나의 사용자 대리자가 <xref:System.OperationCanceledException>을 throw하고 다른 대리자가 다른 예외 형식을 throw할 경우에는 두 예외가 모두 <xref:System.AggregateException>으로 롤링됩니다.

취소에 대한 일반 지침은 다음과 같습니다.

1. 사용자 대리자 취소를 수행하는 경우 외부 <xref:System.Threading.CancellationToken>에 대해 PLINQ에 알리고 <xref:System.OperationCanceledException>(externalCT)을 throw해야 합니다.

2. 취소가 발생하고 다른 예외가 throw되지 않으면 <xref:System.AggregateException>이 아닌 <xref:System.OperationCanceledException>을 처리해야 합니다.

## <a name="example"></a>예

다음 예제는 사용자 코드에서 계산을 많이 해야 하는 경우 취소를 처리하는 방법을 보여줍니다.

[!code-csharp[PLINQ#17](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#17)]
[!code-vb[PLINQ#17](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#17)]

사용자 코드에서 취소를 처리하면 쿼리 정의에서 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A>을 사용할 필요가 없습니다. 그러나 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A>은 쿼리 성능에 영향을 주지 않고 이를 통해 쿼리 연산자 및 사용자 코드에서 취소를 처리할 수 있습니다.

시스템 응답성을 보장하기 위해 밀리초마다 한 번 정도 취소를 확인하는 것이 좋지만 최대 10밀리초의 기간이 허용되는 것으로 간주합니다. 이 빈도는 코드 성능에 부정적인 영향을 주면 안 됩니다.

쿼리 결과에 대해 반복 중인 foreach(Visual Basic의 For Each) 루프에서 코드가 중단되는 경우와 같이 열거자가 삭제되는 경우에는 쿼리가 취소되지만 예외가 throw되지 않습니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Linq.ParallelEnumerable>
- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
- [관리되는 스레드의 취소](../../../docs/standard/threading/cancellation-in-managed-threads.md)
