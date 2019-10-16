---
title: '방법: PLINQ 쿼리의 예외 처리'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to handle exceptions
ms.assetid: 8d56ff9b-a571-4d31-b41f-80c0b51b70a5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c9b5dce796e546bf041c28864c8bf66b5f51965e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046620"
---
# <a name="how-to-handle-exceptions-in-a-plinq-query"></a>방법: PLINQ 쿼리의 예외 처리

이 항목의 첫 번째 예제에서는 실행될 때 PLINQ 쿼리에서 throw될 수 있는 <xref:System.AggregateException?displayProperty=nameWithType>을 처리하는 방법을 보여줍니다. 두 번째 예제에서는 대리자 내에서 예외가 throw될 위치에 가능한 한 가깝게 try-catch 블록을 넣는 방법을 보여줍니다. 이 방법으로 예외가 발생한 즉시 예외를 catch하고 쿼리 실행을 계속할 수 있습니다. 예외가 가입된 스레드로 다시 버블 업될 수 있는 경우 예외가 발생한 후에도 쿼리에서 일부 항목을 계속 처리할 수 있습니다.

PLINQ가 순차적 실행으로 대체되고 예외가 발생하는 일부 경우에는 예외가 직접 전파되며 <xref:System.AggregateException>으로 래핑되지 않을 수 있습니다. <xref:System.Threading.ThreadAbortException>은 항상 직접 전파됩니다.

> [!NOTE]
> “내 코드만”이 사용하도록 설정된 경우 Visual Studio가 예외를 throw하는 줄에서 중단하고 “예외가 사용자 코드에서 처리되지 않았다”는 오류 메시지를 표시합니다. 이 오류는 심각하지는 않습니다. F5 키를 눌러 계속하고 아래 예제에 설명된 예외 처리 동작을 확인할 수 있습니다. 첫 번째 오류 지점에서 Visual Studio가 실행을 중단하지 않도록 하려면 **도구, 옵션, 디버깅, 일반**을 차례로 선택하고 “내 코드만” 확인란의 선택을 취소하기만 하면 됩니다.
>
> 이 예제는 사용법을 보여 주기 위한 것이며, 동일한 순차 LINQ to Objects 쿼리보다 빠르게 실행되지 않을 수도 있습니다. 속도 향상에 대한 자세한 내용은 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)를 참조하세요.

## <a name="example"></a>예

이 예제는 throw된 <xref:System.AggregateException?displayProperty=nameWithType>을 catch하는 쿼리를 실행하는 코드 주위에 try-catch 블록을 넣는 방법을 보여줍니다.

[!code-csharp[PLINQ#41](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#41)]
[!code-vb[PLINQ#41](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#41)]

이 예제에서는 예외가 throw된 후 쿼리를 계속할 수 없습니다. 애플리케이션 코드가 예외를 catch할 때까지 PLINQ가 모든 스레드에서 쿼리를 이미 중지했습니다.

## <a name="example"></a>예

다음 예제는 예외를 catch하고 쿼리 실행을 계속할 수 있도록 대리자에 try-catch 블록을 넣는 방법을 보여줍니다.

[!code-csharp[PLINQ#42](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#42)]
[!code-vb[PLINQ#42](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#42)]

## <a name="compiling-the-code"></a>코드 컴파일

- 이러한 예제를 컴파일하고 실행하려면 PLINQ 데이터 샘플 예제에 복사하고 Main에서 메서드를 호출합니다.

## <a name="robust-programming"></a>강력한 프로그래밍

프로그램 상태를 손상시키지 않도록 처리 방법을 아는 경우가 아니면 예외를 catch하지 마세요.

## <a name="see-also"></a>참고 항목

- <xref:System.Linq.ParallelEnumerable>
- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
