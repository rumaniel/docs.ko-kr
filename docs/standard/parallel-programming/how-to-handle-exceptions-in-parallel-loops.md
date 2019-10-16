---
title: '방법: 병렬 루프의 예외 처리'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to handle exceptions
ms.assetid: 512f0d5a-4636-4875-b766-88f20044f143
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2ffc522b2ab13ae2098c01e6716e00aef5bef8e7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962491"
---
# <a name="how-to-handle-exceptions-in-parallel-loops"></a>방법: 병렬 루프의 예외 처리
<xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 오버로드에는 throw될 수 있는 예외를 처리하기 위한 특별한 메커니즘이 없습니다. 이런 점에서 일반 `for` 및 `foreach` 루프(Visual Basic의 `For` 및 `For Each`)와 비슷합니다. 처리되지 않은 예외로 인해 루프가 즉시 종료됩니다.  
  
 병렬 루프에 고유한 예외 처리 논리를 추가할 때 비슷한 예외가 여러 스레드에서 동시에 throw되는 경우와 한 스레드에서 throw된 예외로 인해 다른 스레드에서 다른 예외가 throw되는 경우를 처리합니다. <xref:System.AggregateException?displayProperty=nameWithType>에서 루프의 모든 예외를 래핑하여 두 경우 모두를 처리합니다. 다음 예제에서는 한 가지 가능한 접근 방법을 보여 줍니다.  
  
> [!NOTE]
> “내 코드만”이 사용하도록 설정된 경우 Visual Studio가 예외를 발생시키는 줄에서 중단하고 "예외가 사용자 코드에서 처리되지 않았다"는 오류 메시지를 표시합니다. 이 오류는 심각하지는 않습니다. F5 키를 눌러 계속하고 아래 예제에 설명된 예외 처리 동작을 확인할 수 있습니다. 첫 번째 오류 지점에서 Visual Studio가 실행을 중단하지 않도록 하려면 **도구, 옵션, 디버깅, 일반**을 차례로 선택하고 “내 코드만” 확인란의 선택을 취소하기만 하면 됩니다.  
  
## <a name="example"></a>예  
 이 예제에서는 모든 예외가 catch되고 나서 throw된 <xref:System.AggregateException?displayProperty=nameWithType>로 래핑됩니다. 호출자는 처리할 예외를 결정할 수 있습니다.  
  
 [!code-csharp[TPL_Exceptions#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptions.cs#08)]
 [!code-vb[TPL_Exceptions#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/exceptionsinloops.vb#08)]  
  
## <a name="see-also"></a>참고 항목

- [데이터 병렬 처리](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)
- [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)
