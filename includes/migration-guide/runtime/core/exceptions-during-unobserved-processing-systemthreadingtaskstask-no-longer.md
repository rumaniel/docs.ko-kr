---
ms.openlocfilehash: b0e6d6f228647148083d3df64e65f817dc3455d5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "66379702"
---
### <a name="exceptions-during-unobserved-processing-in-systemthreadingtaskstask-no-longer-propagate-on-finalizer-thread"></a>System.Threading.Tasks.Task의 관찰되지 않은 처리 중에 예외는 더 이상 종료자 스레드를 전파하지 않습니다

|   |   |
|---|---|
|세부 정보|<xref:System.Threading.Tasks.Task?displayProperty=name> 클래스는 비동기 작업을 나타내기 때문에 비동기 처리를 하는 동안 발생하는 심각하지 않은 예외를 모두 catch합니다. .NET Framework 4.5에서는 예외가 관찰되지 않고 코드가 작업에서 대기하지 않으면 예외는 더 이상 종료자 스레드에서 전파되지 않고 가비지 수집 도중 프로세스와 충돌합니다. 이러한 변경으로 인해 관찰되지 않은 비동기 처리를 수행하기 위해 Task 클래스를 사용하는 애플리케이션의 안정성이 향상됩니다.|
|제안 해결 방법|응용 프로그램이 종료자 스레드를 전파하는 관찰되지 않은 비동기 예외에 종속되는 경우 이전의 동작을 <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException> 이벤트에 대한 적절한 처리기를 제공하거나 [런타임 구성 요소](~/docs/framework/configure-apps/file-schema/runtime/throwunobservedtaskexceptions-element.md)를 설정하여 복원할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Threading.Tasks.Task.Run(System.Action)?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.Run(System.Action,System.Threading.CancellationToken)?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.Run(System.Func{System.Threading.Tasks.Task})?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.Run(System.Func{System.Threading.Tasks.Task},System.Threading.CancellationToken)?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.Run%60%601(System.Func{%60%600})?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.Run%60%601(System.Func{%60%600},System.Threading.CancellationToken)?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.Run%60%601(System.Func{System.Threading.Tasks.Task{%60%600}})?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.Run%60%601(System.Func{System.Threading.Tasks.Task{%60%600}},System.Threading.CancellationToken)?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.Start?displayProperty=nameWithType></li><li><xref:System.Threading.Tasks.Task.Start(System.Threading.Tasks.TaskScheduler)?displayProperty=nameWithType></li></ul>|
