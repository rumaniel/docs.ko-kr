---
title: '방법: 작업 및 해당 자식 취소'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to cancel
ms.assetid: 08574301-8331-4719-ad50-9cf7f6ff3048
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 08e5712db60fb09b48d6be9f35737c9a884d1ce8
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59324477"
---
# <a name="how-to-cancel-a-task-and-its-children"></a>방법: 작업 및 해당 자식 취소
이 예제는 다음 작업을 수행하는 방법을 보여줍니다.  
  
1. 취소 가능한 작업을 만들고 시작합니다.  
  
2. 사용자 대리자에 그리고 선택적으로 작업 인스턴스에 취소 토큰을 전달합니다.  
  
3. 사용자 대리자의 취소 요청을 확인하고 이에 응답합니다.  
  
4. 선택적으로 작업이 취소된 호출 스레드를 확인합니다.  
  
 호출 스레드가 작업을 강제로 종료하지 않으며, 취소가 요청되었다는 신호만 보냅니다. 작업이 이미 실행 중인 경우 사용자 대리자가 요청을 알리고 적절하게 응답해야 합니다. 작업 실행 전에 취소를 요청하면 사용자 대리자가 실행되지 않고 작업 개체가 Canceled 상태로 전환됩니다.  
  
## <a name="example"></a>예제  
 이 예제는 취소 요청에 대한 응답으로 <xref:System.Threading.Tasks.Task> 및 해당 자식을 종료하는 방법을 보여줍니다. 또한 <xref:System.Threading.Tasks.TaskCanceledException>을 throw하여 사용자 대리자가 종료될 때 호출 스레드에서 필요에 따라 <xref:System.Threading.Tasks.Task.Wait%2A> 메서드나 <xref:System.Threading.Tasks.Task.WaitAll%2A> 메서드를 사용하여 작업이 종료될 때까지 대기할 수 있음을 보여 줍니다. 이 경우 `try/catch` 블록을 사용하여 호출 스레드에서 예외를 처리해야 합니다.  
  
 [!code-csharp[TPL_Cancellation#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cancellation/cs/cancel1.cs#04)]
 [!code-vb[TPL_Cancellation#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cancellation/vb/cancel1.vb#04)]  
  
 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 클래스는 <xref:System.Threading.CancellationTokenSource?displayProperty=nameWithType> 및 <xref:System.Threading.CancellationToken?displayProperty=nameWithType> 유형을 기반으로 하는 취소 모델과 완전히 통합되었습니다. 자세한 내용은 [관리되는 스레드의 취소](../../../docs/standard/threading/cancellation-in-managed-threads.md) 및 [작업 취소](../../../docs/standard/parallel-programming/task-cancellation.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.CancellationTokenSource?displayProperty=nameWithType>
- <xref:System.Threading.CancellationToken?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>
- [작업 기반 비동기 프로그래밍](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)
- [연결된 자식 작업 및 분리된 자식 작업](../../../docs/standard/parallel-programming/attached-and-detached-child-tasks.md)
- [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)
