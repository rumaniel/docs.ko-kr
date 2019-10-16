---
title: 연결된 자식 작업 및 분리된 자식 작업
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, child tasks
ms.assetid: c95788bf-90a6-4e96-b7bc-58e36a228cc5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 29383d0b7f125111071ac131d8a822dba811032e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54603315"
---
# <a name="attached-and-detached-child-tasks"></a>연결된 자식 작업 및 분리된 자식 작업
‘자식 작업’(또는 ‘중첩 작업’)은 ‘부모 작업’이라는 다른 작업의 사용자 대리자에 만들어진 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 인스턴스입니다. 자식 작업을 분리하거나 연결할 수 있습니다. ‘분리된 자식 작업’은 부모와 독립적으로 실행되는 작업입니다. ‘연결된 자식 작업’은 부모가 명시적으로나 기본적으로 연결을 금지하지 않는 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent?displayProperty=nameWithType> 옵션으로 만들어진 중첩 작업입니다. 연결된 자식 작업 및 분리된 자식 작업은 작업에서 개수와 관계없이 만들 수 있고 시스템 자원에 의해서만 제한됩니다.  
  
 다음 표에는 두 가지 자식 작업의 기본적인 차이점이 나와 있습니다.  
  
|범주|분리된 자식 작업|연결된 자식 작업|  
|--------------|--------------------------|--------------------------|  
|부모는 자식 작업이 완료될 때까지 기다립니다.|아니요|예|  
|부모는 자식 작업에서 throw된 예외를 전파합니다.|아니요|예|  
|부모 상태는 자식 상태에 따라 달라집니다.|아니요|예|  
  
 분리된 자식 작업과 다른 작업과의 관계가 덜 복잡하므로 대부분 시나리오에서 해당 자식 작업을 사용하는 것이 좋습니다. 이는 부모 작업 내부에서 만들어진 작업은 기본적으로 분리되기 때문이고, 연결된 자식 작업을 만들려면 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent?displayProperty=nameWithType> 옵션을 명시적으로 지정해야 합니다.  
  
## <a name="detached-child-tasks"></a>분리된 자식 작업  
 자식 작업이 부모 작업에 의해 만들어지면 기본적으로 부모 작업과 독립적입니다. 다음 예제에서는 부모 작업에서 단순한 자식 작업 하나를 만듭니다. 예제 코드를 여러 번 실행하면 예제의 출력이 표시된 내용과 다르고 코드를 실행할 때마다 출력이 변경될 수 있음을 알 수 있습니다. 부모 작업과 자식 작업은 서로 독립적으로 실행되기 때문에 이 문제가 발생합니다. 자식은 분리된 작업입니다. 예제에서는 부모 작업이 완료될 때까지 대기하고 자식 작업은 콘솔 앱이 종료되기 전에 실행되거나 완료될 수 있습니다.  
  
 [!code-csharp[TPL_ChildTasks#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/nested1.cs#1)]
 [!code-vb[TPL_ChildTasks#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/nested1.vb#1)]  
  
 자식 작업을 <xref:System.Threading.Tasks.Task> 개체가 아닌 <xref:System.Threading.Tasks.Task%601> 개체로 표시하면 부모 작업은 자식이 분리된 자식 작업이더라도 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 속성에 액세스하여 자식이 완료될 때까지 대기합니다. <xref:System.Threading.Tasks.Task%601.Result%2A> 속성은 다음 예제와 같이 해당 작업이 완료될 때까지 차단됩니다.  
  
 [!code-csharp[TPL_ChildTasks#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/childtasks.cs#4)]
 [!code-vb[TPL_ChildTasks#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/tpl_childtasks.vb#4)]  
  
## <a name="attached-child-tasks"></a>연결된 자식 작업  
 분리된 자식 작업과 달리 연결된 자식 작업은 부모와 밀접하게 동기화됩니다. 다음 예제와 같이 작업 만들기 문에서 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent?displayProperty=nameWithType> 옵션을 사용하여 연결된 자식 작업에 대한 이전 예제에서 분리된 자식 작업을 변경할 수 있습니다. 이 코드에서는 연결된 자식 작업이 부모보다 먼저 완료됩니다. 따라서 예제의 출력은 코드를 실행할 때마다 같습니다.  
  
 [!code-csharp[TPL_ChildTasks#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/child1.cs#2)]
 [!code-vb[TPL_ChildTasks#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/child1.vb#2)]  
  
 연결된 자식 작업을 사용하여 비동기 작업의 밀접하게 동기화된 그래프를 만들 수 있습니다.  
  
 그러나 부모가 연결된 자식 작업을 금지하지 않는 경우에만 자식 작업이 부모에 연결될 수 있습니다. 부모 작업은 부모 작업의 클래스 생성자 또는 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType> 메서드에서 <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType> 옵션을 지정하여 명시적으로 자식 작업이 부모 작업에 연결되지 않도록 방지합니다. <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> 메서드 호출을 통해 만들어진 부모 작업은 명시적으로 자식 작업이 부모 작업에 연결되지 않도록 합니다. 다음은 이에 대한 예입니다. 부모 작업이 <xref:System.Threading.Tasks.TaskFactory.StartNew%28System.Action%29?displayProperty=nameWithType> 메서드가 아닌 <xref:System.Threading.Tasks.Task.Run%28System.Action%29?displayProperty=nameWithType> 메서드를 호출하여 만들어진다는 점을 제외하고 이전 예제와 동일합니다. 자식 작업이 부모에 연결할 수 없으므로 예제의 출력을 예측할 수 없습니다. <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> 오버로드에 대한 기본 작업 만들기 옵션에 <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType>가 포함되므로 이 예제는 “분리된 자식 작업" 섹션의 첫 번째 예제와 기능상으로 같습니다.  
  
 [!code-csharp[TPL_ChildTasks#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/child1a.cs#3)]
 [!code-vb[TPL_ChildTasks#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/child1a.vb#3)]  
  
## <a name="exceptions-in-child-tasks"></a>자식 작업의 예외  
 분리된 자식 작업에서 예외가 throw되면 중첩되지 않은 작업처럼 부모 작업에서 직접 해당 예외를 관찰하거나 처리해야 합니다. 연결된 자식 작업에서 예외가 throw되면 해당 예외는 자동으로 부모 작업에 전파되고 다시 작업의 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 속성을 기다리거나 속성에 액세스하는 스레드에 전파됩니다. 따라서 연결된 자식 작업을 사용하면 호출 스레드에서 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType>에 대한 호출의 한 지점에서만 모든 예외를 처리할 수 있습니다. 자세한 내용은 [예외 처리](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)를 참조하세요.  
  
## <a name="cancellation-and-child-tasks"></a>취소 및 자식 작업  
 작업 취소는 협조적입니다. 즉, 취소할 수 있으려면 모든 연결된 자식 작업과 분리된 자식 작업이 취소 토큰의 상태를 모니터링해야 합니다. 하나의 취소 요청을 사용하여 부모 및 모든 자식을 취소하려면 인수와 같은 토큰을 모든 작업에 전달하고 각 작업에서 논리를 제공하여 각 작업의 요청에 응답합니다. 자세한 내용은 [작업 취소](../../../docs/standard/parallel-programming/task-cancellation.md) 및 [방법: 작업 및 해당 자식 취소](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md)를 참조하세요.  
  
### <a name="when-the-parent-cancels"></a>부모가 취소되는 경우  
 자식 작업이 시작되기 전에 부모가 자신을 취소하면 자식이 시작되지 않습니다. 자식 작업이 시작되고 나서 부모가 자신을 취소하면 자체 취소 논리가 없을 경우 자식이 완료까지 실행됩니다. 자세한 내용은 [작업 취소](../../../docs/standard/parallel-programming/task-cancellation.md)를 참조하세요.  
  
### <a name="when-a-detached-child-task-cancels"></a>분리된 자식 작업이 취소되는 경우  
 분리된 자식 작업이 부모에 전달된 것과 같은 토큰을 사용하여 자신을 취소하고 부모가 하위 작업을 기다리지 않으면, 예외는 심각하지 않은 협력 취소로 처리되므로 전파되지 않습니다. 이 동작은 모든 최상위 작업의 동작과 같습니다.  
  
### <a name="when-an-attached-child-task-cancels"></a>연결된 자식 작업이 취소되는 경우  
 연결된 자식 작업이 부모 작업에 전달된 것과 같은 토큰을 사용하여 자신을 취소하면 <xref:System.Threading.Tasks.TaskCanceledException>은 <xref:System.AggregateException> 내부의 조인 스레드에 전파됩니다. 연결된 자식 작업의 그래프를 통해 전파되는 오류가 있는 모든 예외 이외에 심각하지 않은 예외를 모두 처리할 수 있습니다.  
  
 자세한 내용은 [예외 처리](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)를 참조하세요.  
  
## <a name="preventing-a-child-task-from-attaching-to-its-parent"></a>자식 작업을 해당 부모에 연결하는 것 방지  
 자식 작업에서 throw된 처리되지 않은 예외는 부모 작업에 전파됩니다. 이 동작을 사용하면 작업 트리에서 이동하는 대신 하나의 루트 작업에서 자식 작업 예외를 모두 관찰할 수 있습니다. 그러나 부모 작업에 다른 코드의 첨부 파일이 필요하지 않으면 예외 전파가 문제가 될 수 있습니다. 예를 들어 <xref:System.Threading.Tasks.Task> 개체에서 타사 라이브러리 구성 요소를 호출하는 앱을 고려해 보세요. 타사 라이브러리 구성 요소가 <xref:System.Threading.Tasks.Task> 개체를 만들고 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent?displayProperty=nameWithType>를 지정하여 부모 작업에 연결하면, 자식 작업에서 발생한 처리되지 않은 예외가 부모에 전파됩니다. 이로 인해 기본 앱에서 예기치 않은 동작이 발생할 수 있습니다.  
  
 자식 작업이 부모 작업에 연결되지 않도록 방지하려면 부모 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체를 만들 때 <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType> 옵션을 지정합니다. 작업이 부모에 연결되려고 하고 부모가 <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType> 옵션을 지정하면 자식 작업이 부모에 연결될 수 있고 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent?displayProperty=nameWithType> 옵션을 지정하지 않은 것처럼 실행됩니다.  
  
 자식 작업이 시기적절하게 완료되지 않으면 자식 작업이 부모에 연결되지 않도록 방지할 수도 있습니다. 부모 작업은 자식 작업이 모두 완료될 때까지 완료되지 않기 때문에 오래 실행되는 자식 작업은 전체적인 앱의 성능을 저하할 수 있습니다. 작업이 부모 작업에 연결되지 않도록 방지하여 앱 성능을 향상시키는 방법을 보여주는 예제는 [방법: 자식 작업이 부모 작업에 연결되지 않도록 방지](../../../docs/standard/parallel-programming/how-to-prevent-a-child-task-from-attaching-to-its-parent.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
- [데이터 병렬 처리](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)
