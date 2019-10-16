---
ms.openlocfilehash: 4529d8040fc08b5290ac46abd1ef752086ea3aeb
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774494"
---
### <a name="new-ambiguous-dispatcherinvoke-overloads-could-result-in-different-behavior"></a>(모호한) 새 Dispatcher.Invoke 오버로드는 다른 동작을 발생시킬 수 있습니다

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5는 <xref:System.Action> 형식의 매개 변수를 포함하는 새 오버로드를 <xref:System.Windows.Threading.Dispatcher.Invoke%2A?displayProperty=nameWithType>에 추가합니다. 기존 코드를 다시 컴파일하면 컴파일러는 <xref:System.Delegate> 매개 변수를 가진 Dispatcher.Invoke 메서드에 대한 호출로서 <xref:System.Action> 매개 변수를 갖는 Dispatcher.Invoke 메서드에 대한 호출을 해결할 수 있습니다. <xref:System.Delegate> 매개 변수를 가진 Dispatcher.Invoke 오버로드를 호출함으로써 해결된 <xref:System.Action> 매개 변수를 가진 Dispatcher.Invoke 오버로드를 호출하는 경우, 다음과 같은 동작 차이가 발생할 수 있습니다.<ul><li>예외가 발생하는 경우 <xref:System.Windows.Threading.Dispatcher.UnhandledExceptionFilter> 및 <xref:System.Windows.Threading.Dispatcher.UnhandledException> 이벤트가 발생하지 않습니다. 대신 예외는 <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException?displayProperty=name> 이벤트에 의해 처리됩니다.</li><li><xref:System.Windows.Threading.DispatcherOperation.Result>와 같은 일부 멤버에 대한 호출은 작업이 완료될 때까지 차단됩니다.</li></ul>|
|제안 해결 방법|모호성 (및 예외를 처리하거나 동작을 차단하는 잠재적인 문제)을 방지하려면 Dispatcher.Invoke를 호출하는 코드가 빈 개체를 두 번째 매개 변수로 Invoke 호출에 전달하여 .NET Framework 4.0 메서드 오버로드를 확인하도록 할 수 있습니다.|
|범위|부|
|버전|4.5|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.TimeSpan,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.TimeSpan,System.Windows.Threading.DispatcherPriority,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.Windows.Threading.DispatcherPriority,System.Object[])?displayProperty=nameWithType></li></ul>|
