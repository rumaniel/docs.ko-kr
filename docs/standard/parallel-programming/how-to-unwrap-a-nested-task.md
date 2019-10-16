---
title: '방법: 중첩된 작업 래핑 취소'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to unwrap nested tasks
ms.assetid: a0769dd2-0f6d-48ca-8418-a9d39de7f450
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3cc468da70d3c62c139a98a6637e7a3c7990c378
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54602054"
---
# <a name="how-to-unwrap-a-nested-task"></a>방법: 중첩된 작업 래핑 취소
메서드에서 작업을 반환한 후 다음 예제와 같이 해당 작업을 대기하거나 계속할 수 있습니다.  
  
 [!code-csharp[TPL_Unwrap#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#01)]
 [!code-vb[TPL_Unwrap#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippets1-3.vb#01)]  
  
 이전 예제에서 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성은 `string`(Visual Basic의 경우 `String`) 형식입니다.  
  
 그러나 일부 시나리오에서는 다른 작업 내에 작업을 만들고 중첩된 작업을 반환할 수 있습니다. 이 경우 바깥쪽 작업의 `TResult` 자체가 작업입니다. 다음 예제에서 Result 속성은 C#의 경우 `Task(Of Task(Of String))` 또는 Visual Basic의 경우 `Task<Task<string>>`입니다.  
  
 [!code-csharp[TPL_Unwrap#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#02)]
 [!code-vb[TPL_Unwrap#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippets1-3.vb#02)]  
  
 외부 작업을 래핑 해제하고 원래 작업 및 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성을 검색하는 코드를 작성할 수 있지만, 예외 및 취소 요청을 처리해야 하므로 이러한 코드를 작성하기가 쉽지 않습니다. 이 경우 다음 예와 같이 <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> 확장 메서드 중 하나를 사용하는 것이 좋습니다.  
  
 [!code-csharp[TPL_UnWrap#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#03)]
 [!code-vb[TPL_UnWrap#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippets1-3.vb#03)]  
  
 <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> 메서드를 사용하면 `Task<Task>` 또는 `Task<Task<TResult>>`(Visual Basic의 경우 `Task(Of Task)` 또는 `Task(Of Task(Of TResult))`)를 `Task` 또는 `Task<TResult>`(Visual Basic의 경우 `Task(Of TResult)`)로 변환할 수 있습니다. 새 작업은 내부 중첩 작업을 완전히 나타내며 취소 상태 및 모든 예외를 포함합니다.  
  
## <a name="example"></a>예제  
 다음 예제는 <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> 확장 메서드를 사용하는 방법을 보여줍니다.  
  
 [!code-csharp[TPL_UnWrap#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#04)]
 [!code-vb[TPL_UnWrap#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippet04.vb#04)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Tasks.TaskExtensions?displayProperty=nameWithType>
- [작업 기반 비동기 프로그래밍](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)
