---
title: TAP(작업 기반 비동기 패턴)
ms.date: 02/26/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- .NET Framework, and TAP
- asynchronous design patterns, .NET Framework
- TAP, .NET Framework support for
- Task-based Asynchronous Pattern, .NET Framework support for
- .NET Framework, asynchronous design patterns
ms.assetid: 8cef1fcf-6f9f-417c-b21f-3fd8bac75007
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 052f6a61fb1b03b060e22bbff2d8124ac3a1c0c0
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66377653"
---
# <a name="task-based-asynchronous-pattern-tap"></a>TAP(작업 기반 비동기 패턴)
TAP(작업 기반 비동기 패턴)은 임의 비동기 작업을 나타내는 데 사용되는 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 네임스페이스의 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks?displayProperty=nameWithType> 형식을 기준으로 합니다. TAP은 새로운 개발을 위해 비동기 디자인 패턴을 권장합니다.  
  
## <a name="naming-parameters-and-return-types"></a>이름 지정, 매개 변수 및 반환 형식

TAP은 단일 메서드를 사용하여 비동기 작업의 시작과 완료를 나타냅니다. 이는 APM(비동기 프로그래밍 모델 또는 `IAsyncResult`) 패턴 및 EAP(이벤트 기반 비동기 패턴)와 대조됩니다. APM에는 `Begin` 및 `End` 메서드가 필요합니다. EAP에는 `Async` 접미사가 있는 메서드가 필요하며 하나 이상의 이벤트, 이벤트 처리기 대리자 형식 및 `EventArg`에서 파생된 형식도 필요합니다. TAP의 비동기 메서드는 <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.ValueTask> 및 <xref:System.Threading.Tasks.ValueTask%601>와 같은 대기할 수 있는 형식을 반환하는 메서드의 작업 이름 뒤에 `Async` 접미사를 포함합니다. 예를 들어 `Task<String>`을 반환하는 비동기 `Get` 작업은 명명된 `GetAsync`일 수 있습니다. 접미사가 `Async`인 EAP 메서드 이름이 이미 포함되어 있는 클래스에 TAP 메서드를 추가하는 경우 대신 `TaskAsync` 접미사를 사용합니다. 예를 들어, 클래스에 `GetAsync` 메서드가 이미 있는 경우 이름으로 `GetTaskAsync`를 사용합니다. 메서드가 비동기 작업을 시작하지만 대기할 수 있는 형식을 반환하지 않는 경우 이 메서드가 작업 결과를 반환하거나 throw하지 않도록 제안하려면 해당 이름은 `Begin`, `Start` 또는 일부 다른 동사로 시작해야 합니다.  
  
 TAP 메서드는 해당 동기 메서드가 void를 반환하는지 또는 `TResult` 형식을 반환하는지에 따라 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 또는 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 개체를 반환합니다.  
  
 TAP 메서드의 매개 변수는 해당 동기 메서드의 매개 변수와 일치해야 하며 동일한 순서로 제공되어야 합니다.  그러나, `out` 및 `ref` 매개 변수는 이 규칙에서 제외되므로 사용하지 말아야 합니다. `out` 또는 `ref` 매개 변수를 통해 반환된 데이터는 `TResult`에 의해 반환되는 <xref:System.Threading.Tasks.Task%601>의 일부로 대신 반환되어야 하며, 여러 값을 수용하기 위해 튜플 또는 사용자 지정 데이터 구조를 사용해야 합니다. TAP 메서드의 동기 메서드가 매개 변수를 제공하지 않는 경우에도 <xref:System.Threading.CancellationToken> 매개 변수 추가를 고려해야 합니다.
 
 작업의 생성, 조작 또는 조합에만 사용되는 메서드(메서드의 비동기 의도는 메서드 이름 또는 메서드가 속해 있는 형식의 이름에 분명하게 나타나 있음)는 이 명명 패턴을 따를 필요가 없습니다. 이런 메서드를 흔히 조합기라고 합니다.  조합기의 예로는 <xref:System.Threading.Tasks.Task.WhenAll%2A> 및 <xref:System.Threading.Tasks.Task.WhenAny%2A>가 있으며, [작업 기반 비동기 패턴 사용](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md) 문서의 [기본 제공 작업 기반 조합기 사용](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md#combinators) 섹션에서 해당 설명을 확인할 수 있습니다.  
  
 TAP 구문이 APM(비동기 프로그래밍 모델) 및 EAP(이벤트 기반 비동기 패턴)와 같은 레거시 비동기 프로그래밍 패턴에 사용된 구문과 어떻게 다른지에 대한 예를 보려면 [비동기 프로그래밍 패턴](../../../docs/standard/asynchronous-programming-patterns/index.md)을 참조하세요.  
  
## <a name="initiating-an-asynchronous-operation"></a>비동기 작업 시작  
 TAP을 기반으로 하는 비동기 메서드는 인수 유효성 검사 및 결과 작업을 반환하기 전에 비동기 작업 시작 등 적은 양의 작업을 동기적으로 수행할 수 있습니다. 동기 작업은 비동기 메서드가 신속하게 반환할 수 있도록 최소한으로 유지해야 합니다. 빠르게 반환되는 이유는 다음과 같습니다.  
  
- 비동기 메서드는 사용자 인터페이스(UI) 스레드에서 호출할 수 있으며, 모든 장기 실행 동기 작업에서 애플리케이션의 응답에 문제가 발생할 수 있습니다  
  
- 여러 비동기 메서드를 동시에 실행할 수 있습니다. 따라서 비동기 메서드의 동기 부분에서 모든 장기 실행 작업은 다른 비동기 작업의 시작을 지연시켜 동시성의 이점을 감소시킬 수 있습니다.  
  
 경우에 따라 작업을 완료하는 데 필요한 작업 시간이 비동기적으로 작업을 실행하는 데 필요한 작업 시간보다 적을 수 있습니다. 이미 메모리에 버퍼링된 데이터로 읽기 작업을 충족할 수 있는 스트림에서 읽기는 이러한 시나리오의 예입니다. 경우에 따라 작업을 동기적으로 완료하고 이미 완료된 작업을 반환할 수 있습니다.  
  
## <a name="exceptions"></a>예외  
 비동기 메서드는 사용 오류에 응답에서만 비동기 메서드 호출에서 throw할 예외를 발생시켜야 합니다. 프로덕션 코드에서는 사용 오류가 절대 발생해서는 안 됩니다. 예를 들어, null 참조(Visual Basic에서 `Nothing`)를 오류 상태(일반적으로 <xref:System.ArgumentNullException>으로 표시되는 예외)를 유발하는 메서드 인수 중 하나로 전달하는 경우 null 참조가 전달되지 않도록 호출 코드를 수정할 수 있습니다. 기타 모든 오류에 대해 작업이 반환되기 전에 비동기 메서드가 완전하게 동기화되었다고 해도 비동기 메서드가 실행되는 동안 발생하는 예외를 반환된 작업에 할당해야 합니다. 일반적으로 작업에는 최대 하나의 예외가 포함됩니다. 그러나 <xref:System.Threading.Tasks.Task.WhenAll%2A>과 같이 작업이 여러 작업을 나타내는 경우 여러 예외가 단일 작업에 연결될 수 있습니다.  
  
## <a name="target-environment"></a>대상 환경  
 TAP 메서드를 구현하면 비동기 실행이 발생하는 위치를 확인할 수 있습니다. 스레드 풀에서 워크로드를 실행하는 방법, 대부분의 작업 실행을 위한 스레드에 바인딩하지 않고 비동기 I/O를 사용하여 구현하는 방법, UI 스레드와 같은 특정 스레드를 실행하는 방법 또는 원하는 수의 잠재 컨텍스트를 사용하는 방법 중 선택할 수 있습니다. TAP 메서드는 실행할 항목이 없을 수도 있으며 시스템 내 다른 위치에서의 조건 발생을 나타내는 <xref:System.Threading.Tasks.Task>만 반환할 수도 있습니다(예: 큐에 대기 중인 데이터 구조에 도착하는 데이터를 나타내는 작업).
 
 TAP 메서드의 호출자는 결과 작업을 동기적으로 대기함으로써 TAP 메서드의 완료 대기를 차단하거나 비동기 작업이 완료될 때 추가(연속) 코드를 실행할 수 있습니다. 연속 코드 작성자는 해당 코드가 실행되는 위치를 제어합니다. 연속 코드를 <xref:System.Threading.Tasks.Task> 클래스에서 메서드를 통해(예: <xref:System.Threading.Tasks.Task.ContinueWith%2A>) 명시적으로 만들거나 연속 작업을 기반으로 만들어진 언어 지원을 사용하여(예: C#의 `await`, Visual Basic의 `Await`, F#의 `AwaitValue`) 암시적으로 만들 수 있습니다.  
  
## <a name="task-status"></a>작업 상태  
 <xref:System.Threading.Tasks.Task> 클래스는 비동기 작업에 대한 수명 주기를 제공하며 해당 주기는 <xref:System.Threading.Tasks.TaskStatus> 열거형으로 표시됩니다. <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601>에서 파생되는 유형의 상황을 지원하거나 일정에 따라 구성을 구분할 수 있도록 지원하기 위해 <xref:System.Threading.Tasks.Task> 클래스가 <xref:System.Threading.Tasks.Task.Start%2A> 메서드를 노출합니다. 공용 <xref:System.Threading.Tasks.Task> 생성자에서 만든 작업은 예약되지 않은 <xref:System.Threading.Tasks.TaskStatus.Created> 상태에서 수명 주기를 시작하고 이러한 인스턴스에서 <xref:System.Threading.Tasks.Task.Start%2A>를 호출할 때만 예약되므로 콜드 작업이라고 합니다.  
 
 다른 모든 작업은 활성 상태로 수명 주기를 시작합니다. 즉, 작업이 나타내는 비동기 작업이 이미 시작되었고 작업 상태는 <xref:System.Threading.Tasks.TaskStatus.Created?displayProperty=nameWithType> 이외의 열거형 값임을 의미합니다. TAP 메서드에서 반환되는 모든 작업을 활성화해야 합니다. **TAP 메서드가 내부적으로 작업의 생성자를 사용하여 반환할 작업을 인스턴스화하는 경우 해당 TAP 메서드는 작업을 반환하기 전에 <xref:System.Threading.Tasks.Task> 개체에서 <xref:System.Threading.Tasks.Task.Start%2A>를 호출해야 합니다.** TAP 메서드의 소비자는 반환된 작업을 활성화했다가 안전하게 가정할 수 있으며 TAP 메서드에서 반환된 <xref:System.Threading.Tasks.Task.Start%2A>의 <xref:System.Threading.Tasks.Task>를 호출하려고 시도해서는 안 됩니다. 활성 작업에서 <xref:System.Threading.Tasks.Task.Start%2A>를 호출하면 <xref:System.InvalidOperationException> 예외가 나타납니다.  
  
## <a name="cancellation-optional"></a>취소(선택 사항)  
 TAP에서 취소는 비동기 메서드 구현자와 비동기 메서드 소비자 모두에 대한 선택 사항입니다. 작업에서 취소를 허용하는 경우에는 취소 토큰(<xref:System.Threading.CancellationToken> 인스턴스)을 수락하는 비동기 메서드의 오버로드가 표시됩니다. 관례적으로 매개 변수의 이름은 `cancellationToken`입니다.  
  
 [!code-csharp[Conceptual.TAP#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#1)]
 [!code-vb[Conceptual.TAP#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#1)]  
  
 비동기 작업은 취소 요청에 대해 이 토큰을 모니터링합니다. 취소 요청을 받으면 작업을 요청하고 취소하도록 선택할 수 있습니다. 작업이 완료되지 않은 상태로 취소되었다면, TAP 메서드는 <xref:System.Threading.Tasks.TaskStatus.Canceled> 상태에서 종료된 작업을 반환합니다. 이 때, 사용 가능한 결과는 없으며 예외도 throw되지 않습니다.  <xref:System.Threading.Tasks.TaskStatus.Canceled> 상태는 <xref:System.Threading.Tasks.TaskStatus.Faulted> 및 <xref:System.Threading.Tasks.TaskStatus.RanToCompletion> 상태와 함께 작업에 대한 최종(완료) 상태로 간주됩니다. 따라서 작업이 <xref:System.Threading.Tasks.TaskStatus.Canceled> 상태에 있을 경우 <xref:System.Threading.Tasks.Task.IsCompleted%2A> 속성은 `true`를 반환합니다. <xref:System.Threading.Tasks.TaskStatus.Canceled> 상태에서 작업이 완료되면 <xref:System.Threading.Tasks.TaskContinuationOptions.NotOnCanceled>와 같은 연속 옵션이 연속을 취소하기 위해 지정되지 않는 한 작업이 등록된 모든 연속은 예정되거나 실행됩니다. 언어 기능의 사용을 통해 취소된 작업을 비동기적으로 대기하고 있는 코드는 실행을 계속하고 여기에서 파생되는 <xref:System.OperationCanceledException> 또는 예외를 받습니다. 또한 <xref:System.Threading.Tasks.Task.Wait%2A> 및 <xref:System.Threading.Tasks.Task.WaitAll%2A>과 같은 메서드를 통해 작업에서 대기 중인 동기적으로 차단된 코드도 예외적으로 계속해서 실행합니다.  
  
 토큰을 허용하는 TAP 메서드가 호출되기 전에 취소 토큰이 취소를 요청한 경우 TAP 메서드가 <xref:System.Threading.Tasks.TaskStatus.Canceled> 작업을 반환해야 합니다.  그러나 비동기 작업을 실행하는 동안 취소가 요청된 경우 비동기 작업에서 취소 요청을 허용해서는 안됩니다.  반환된 작업은 작업이 취소 요청의 결과로 종료될 경우에만 <xref:System.Threading.Tasks.TaskStatus.Canceled> 상태에서 종료되어야 합니다. 취소가 요청되었지만 결과나 예외가 계속해서 발생하면 <xref:System.Threading.Tasks.TaskStatus.RanToCompletion> 또는 <xref:System.Threading.Tasks.TaskStatus.Faulted> 상태에서 작업을 종료해야 합니다. 
 
 무엇보다도 먼저 취소할 기능을 표시하려는 비동기 메서드의 경우 취소 토큰을 수락하지 않은 오버로드를 제공하지 않아도 됩니다. 취소할 수 없는 메서드의 경우 취소 토큰을 수락하는 오버로드를 제공하지 마세요. 이렇게 하면 대상 메서드가 실제로 취소 가능한지 여부를 호출자에게 알려줍니다.  취소를 원하지 않는 소비자 코드는 <xref:System.Threading.CancellationToken>을 허용하는 메서드를 호출하고 인수 값으로 <xref:System.Threading.CancellationToken.None%2A>을 제공할 수도 있습니다. <xref:System.Threading.CancellationToken.None%2A>은 기본 <xref:System.Threading.CancellationToken>과 기능적으로 동일합니다.  
  
## <a name="progress-reporting-optional"></a>진행률 보고(선택 사항)  
 일부 비동기 작업은 진행률 알림을 제공하여 이점을 얻습니다. 이는 일반적으로 비동기 작업의 진행률에 대한 정보로 사용자 인터페이스를 업데이트하는 데 사용됩니다. 
 
 TAP에서 일반적으로 <xref:System.IProgress%601>라고 이름이 지정된 매개 변수로 비동기 메서드에 전달되는 `progress` 인터페이스를 통해 진행이 처리됩니다.  비동기 메서드를 호출할 때 진행률 인터페이스를 제공하면 작업을 시작한 후 잘못 등록된 이벤트 처리기가 업데이트를 누락시킬 수 있는 경우 잘못된 사용으로 인해 발생하는 경합 상태를 없앨 수 있습니다.  더욱 중요한 것은 진행률 인터페이스에서 사용하는 코드에 따라 결정된 대로 다양한 진행률 구현을 지원한다는 점입니다.  예를 들어, 현재 사용하고 있는 코드는 가장 최신 진행 상황 업데이트에만 관여하거나 모든 업데이트를 버퍼링하거나, 각 업데이트에 대한 작업을 호출하거나, 특정 스레드 호출이 마샬링되었는지 제어할 수 있습니다. 특정 소비자의 요구에 따라 맞춘 다양한 인터페이스의 구현을 통해 이러한 옵션을 모두 수행할 수 있습니다.  취소와 마찬가지로 API가 진행률 알림을 지원할 경우에만 TAP 구현에서 <xref:System.IProgress%601> 매개 변수를 제공해야 합니다. 
 
 예를 들어, 지금까지는 이 문서 앞부분에서 설명한 `ReadAsync` 메서드가 바이트 리드 수의 형태로 중간 진행률을 보고할 수 있는 경우 진행률 콜백이 <xref:System.IProgress%601> 인터페이스일 수 있었습니다.  
  
 [!code-csharp[Conceptual.TAP#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#2)]
 [!code-vb[Conceptual.TAP#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#2)]  
  
 `FindFilesAsync` 메서드가 특정 검색 패턴을 충족하는 모든 파일의 목록을 반환하는 경우 진행률 콜백은 완료된 작업 비율과 부분 결과의 현재 집합에 관한 예측을 제공할 수 있습니다.  튜플을 사용하여 이를 수행할 수 있습니다.  
  
 [!code-csharp[Conceptual.TAP#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#3)]
 [!code-vb[Conceptual.TAP#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#3)]  
  
 또는 API에 따라 달라지는 데이터 형식을 사용합니다.  
  
 [!code-csharp[Conceptual.TAP#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#4)]
 [!code-vb[Conceptual.TAP#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#4)]  
  
 후자의 경우 일반적으로 특수 데이터 형식에 `ProgressInfo` 접미사가 붙습니다.  
  
 TAP 구현이 `progress` 매개 변수를 허용하는 오버로드를 제공하는 경우 진행률이 보고되지 않으면 `null`인 인수를 허용해야 합니다. TAP 구현에서는 비동기 메서드에서 신속하게 진행률을 제공하고 진행률의 소비자가 해당 정보를 다루는 방법과 가장 잘 처리할 수 있는 상황을 결정할 수 있는 <xref:System.Progress%601> 개체에 진행률을 동기적으로 보고해야 합니다. 예를 들어, 진행률 인스턴스에서 콜백 마샬링을 선택할 수 있으며, 캡처된 동기화 컨텍스트에 이벤트를 발생시킬 수 있습니다.  
  
## <a name="iprogresst-implementations"></a>IProgress\<T> 구현  
 .NET Framework 4.5는 단일 <xref:System.IProgress%601> 구현인 <xref:System.Progress%601>를 제공합니다. <xref:System.Progress%601> 클래스는 다음과 같이 선언됩니다.  
  
```csharp  
public class Progress<T> : IProgress<T>  
{  
    public Progress();  
    public Progress(Action<T> handler);  
    protected virtual void OnReport(T value);  
    public event EventHandler<T> ProgressChanged;  
}  
```  
  
```vb  
Public Class Progress(Of T) : Inherits IProgress(Of T)  
    Public Sub New()  
    Public Sub New(handler As Action(Of T))  
    Protected Overridable Sub OnReport(value As T)  
    Public Event ProgressChanged As EventHandler(Of T>  
End Class  
```  
  
 <xref:System.Progress%601>의 인스턴스는 비동기 작업이 진행률 업데이트를 보고할 때마다 발생하는 <xref:System.Progress%601.ProgressChanged> 이벤트를 노출합니다. <xref:System.Progress%601.ProgressChanged> 이벤트는 <xref:System.Threading.SynchronizationContext> 인스턴스를 인스턴스화할 때 캡처된 <xref:System.Progress%601> 개체에서 발생합니다. 동기화 컨텍스트를 사용할 수 없는 경우 스레드 풀을 대상으로 하는 기본 컨텍스트가 사용됩니다. 처리기가 이 이벤트에 등록될 수 있습니다. 또한 편의를 위해 단일 처리기가 <xref:System.Progress%601> 생성자에 제공될 수 있으며 <xref:System.Progress%601.ProgressChanged> 이벤트의 이벤트 처리기와 같이 동작합니다. 진행률 업데이트는 이벤트 처리기를 실행하는 동안 비동기 작업이 지연되지 않도록 비동기적으로 발생합니다. 다른 <xref:System.IProgress%601> 구현에서 다른 의미 체계를 적용하도록 선택할 수 있습니다.  
  
## <a name="choosing-the-overloads-to-provide"></a>제공할 오버로드 선택  
 TAP 구현에서 선택적 <xref:System.Threading.Tasks.TaskFactory.CancellationToken%2A>과 선택적 <xref:System.IProgress%601> 매개 변수를 모두 사용하는 경우 잠재적으로 최대 4개의 오버로드가 필요할 수 있습니다.  
  
```csharp  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…, CancellationToken cancellationToken);  
public Task MethodNameAsync(…, IProgress<T> progress);   
public Task MethodNameAsync(…,   
    CancellationToken cancellationToken, IProgress<T> progress);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, cancellationToken As CancellationToken cancellationToken) As Task  
Public MethodNameAsync(…, progress As IProgress(Of T)) As Task   
Public MethodNameAsync(…, cancellationToken As CancellationToken,   
                       progress As IProgress(Of T)) As Task  
```  
  
 그러나 많은 TAP 구현에서 취소 또는 진행률 기능을 제공하지 않으므로 단일 방법이 필요합니다.  
  
```csharp  
public Task MethodNameAsync(…);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
```  
  
 TAP 구현에서 취소 또는 진행률을 지원하지만 둘 모두 지원하지 않는 경우 두 가지 오버로드를 제공할 수 있습니다.  
  
```csharp  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…, CancellationToken cancellationToken);  
  
// … or …  
  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…, IProgress<T> progress);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, cancellationToken As CancellationToken) As Task  
  
' … or …  
  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, progress As IProgress(Of T)) As Task  
```  
  
 TAP 구현에서 취소와 진행률을 모두 지원하는 경우 4가지 오버로드를 모두 노출할 수 있습니다. 그러나 다음 두 가지만 제공할 수 있습니다.  
  
```csharp  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…,   
    CancellationToken cancellationToken, IProgress<T> progress);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, cancellationToken As CancellationToken,   
                       progress As IProgress(Of T)) As Task  
```  
  
 누락된 두 개의 중간 조합을 조정하기 위해 개발자가 <xref:System.Threading.CancellationToken.None%2A> 매개 변수에 대해 <xref:System.Threading.CancellationToken> 또는 기본값인 `cancellationToken`을 전달하고 `null` 매개 변수에 대해 `progress`을 전달할 수 있습니다.  
  
 TAP 메서드를 사용할 때마다 취소 또는 진행률을 이용해야 하는 경우 관련 매개 변수를 허용하지 않는 오버로드는 생략할 수 있습니다.  
  
 여러 오버로드가 취소 또는 진행률을 선택하도록 노출되는 경우 취소 또는 진행률을 지원하지 않는 오버로드는 이를 지원하는 오버로드에 대해 취소의 경우 <xref:System.Threading.CancellationToken.None%2A> 및 진행률의 경우 `null`이 전달된 것처럼 동작해야 합니다.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[비동기 프로그래밍 패턴](../../../docs/standard/asynchronous-programming-patterns/index.md)|작업 기반 비동기 패턴(TAP), 비동기 프로그래밍 모델(APM) 및 이벤트 기반 비동기 패턴(EAP)과 같이 비동기 작업을 수행하는 세 가지 패턴이 도입됩니다.|  
|[작업 기반 비동기 패턴 구현](../../../docs/standard/asynchronous-programming-patterns/implementing-the-task-based-asynchronous-pattern.md)|Visual Studio의 C#와 Visual Basic 컴파일러를 수동으로 사용하거나 컴파일러 및 수동적인 방법의 조합을 사용하는 이 세 가지 방법으로 작업 기반 비동기 패턴(TAP)을 구현하는 방법에 대해 설명합니다.|  
|[Consuming the Task-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)|작업과 콜백을 사용하여 차단되지 않고 대기하는 방법에 대해 설명합니다.|  
|[다른 비동기 패턴 및 형식과의 Interop](../../../docs/standard/asynchronous-programming-patterns/interop-with-other-asynchronous-patterns-and-types.md)|비동기 프로그래밍 모델(APM) 및 이벤트 기반 비동기 패턴(EAP)을 구현하기 위해 작업 기반 비동기 패턴(TAP)을 사용하는 방법에 대해 설명합니다.|
