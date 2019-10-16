---
title: 연속 작업을 사용하여 작업 연결
ms.date: 02/11/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, continuations
ms.assetid: 0b45e9a2-de28-46ce-8212-1817280ed42d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1f88308dcea250c02d9c6cd7f326570f8bc0133c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64630113"
---
# <a name="chaining-tasks-by-using-continuation-tasks"></a>연속 작업을 사용하여 작업 연결
비동기 프로그래밍에서는 한 비동기 작업이 완료 시 두 번째 작업을 호출하고 해당 작업에 데이터를 전달하는 것이 일반적입니다. 일반적으로 연속 작업은 콜백 메서드를 통해 수행되었습니다. 작업 병렬 라이브러리에서는 *연속 작업*이 동일한 기능을 제공합니다. 연속 작업(연속이라고도 함)은 선행 작업이 완료될 때 다른 작업( *선행*이라고 함)이 호출하는 비동기 작업입니다.  
  
 연속은 비교적 사용이 용이하지만 강력하고 유연합니다. 예를 들어 다음 작업을 할 수 있습니다.  
  
- 선행 작업의 데이터를 연속 작업에 전달합니다.  
  
- 연속 작업이 호출되거나 호출되지 않는 정확한 조건을 지정합니다.  
  
- 시작되기 전이나 실행 중일 때 함께 연속 작업을 취소합니다.  
  
- 연속 작업을 예약하는 방법에 대한 힌트를 제공합니다.  
  
- 동일한 선행 작업에서 여러 개의 연속 작업을 호출합니다.  
  
- 여러 선행 작업 중 하나 또는 모두가 완료되면 하나의 연속 작업을 호출합니다.  
  
- 연속 작업을 임의 길이까지 차례로 연결합니다.  
  
- 연속 작업을 사용하여 선행 작업에서 발생한 예외를 처리합니다.  
  
## <a name="about-continuations"></a>연속 작업 정보  
 연속 작업은 <xref:System.Threading.Tasks.TaskStatus.WaitingForActivation> 상태로 만들어지는 작업입니다. 선행 작업이 완료되면 자동으로 활성화됩니다. 사용자 코드에서 연속 작업에 대해 <xref:System.Threading.Tasks.Task.Start%2A?displayProperty=nameWithType> 를 호출하면 <xref:System.InvalidOperationException?displayProperty=nameWithType> 예외가 발생합니다.  
  
 연속 작업 자체는 <xref:System.Threading.Tasks.Task> 이며 작업이 시작된 스레드를 차단하지 않습니다. 연속 작업이 완료될 때까지 차단하려면 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 메서드를 호출합니다.  
  
## <a name="creating-a-continuation-for-a-single-antecedent"></a>단일 선행 작업에 대한 연속 작업 만들기  
 <xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=nameWithType> 메서드를 호출하여 선행 작업이 완료되었을 때 실행되는 연속 작업을 만듭니다. 다음 예제에서는 기본 패턴을 보여줍니다(이해하기 쉽도록 예외 처리는 생략됨). 현재 요일의 이름을 나타내는 `taskA`개체를 반환하는 선행 작업 <xref:System.DayOfWeek> 를 실행합니다. 선행 작업이 완료되면 연속 작업 `continuation`에 선행 작업이 전달되고 해당 결과를 포함하는 문자열을 표시합니다. 

> [!NOTE]
> 이 문서의 C# 샘플은 `Main` 메서드에서 `async` 한정자를 사용합니다. 해당 기능은 C# 7.1 이상에서 사용할 수 있습니다. 이전 버전은 이 샘플 코드를 컴파일하는 경우 [`CS5001`](../../csharp/misc/cs5001.md)을 생성합니다. 언어 버전을 C# 7.1 이상으로 설정해야 합니다. [언어 버전 구성](../../csharp/language-reference/configure-language-version.md)에 관한 문서에서 언어 버전을 구성하는 방법을 알아볼 수 있습니다.
  
 [!code-csharp[TPL_Continuations#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/simple1.cs#1)]
 [!code-vb[TPL_Continuations#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/simple1.vb#1)]  
  
## <a name="creating-a-continuation-for-multiple-antecedents"></a>여러 선행 작업에 대한 연속 작업 만들기  
 작업 그룹 중 하나 또는 모두가 완료되었을 때 실행되는 연속 작업을 만들 수도 있습니다. 모든 선행 작업이 완료되었을 때 연속 작업을 실행하려면 static(Visual Basic에서는`Shared` ) <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 메서드 또는 인스턴스 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A?displayProperty=nameWithType> 메서드를 호출합니다. 선행 작업 중 하나가 완료되었을 때 연속 작업을 실행하려면 static(Visual Basic에서는`Shared` ) <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> 메서드 또는 인스턴스 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A?displayProperty=nameWithType> 메서드를 호출합니다.  
  
 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> 오버로드 호출은 호출 스레드를 차단하지 않습니다.  그러나 일반적으로는 <xref:System.Threading.Tasks.Task.WhenAll%28System.Collections.Generic.IEnumerable%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Task.WhenAll%28System.Threading.Tasks.Task%5B%5D%29?displayProperty=nameWithType> 메서드를 제외하고 모두 호출하여 반환된 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 속성을 검색하므로, 호출 스레드가 차단됩니다.  
  
 다음 예제에서는 <xref:System.Threading.Tasks.Task.WhenAll%28System.Collections.Generic.IEnumerable%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=nameWithType> 메서드를 호출하여 10개 선행 작업의 결과를 반영하는 연속 작업을 만듭니다. 각 선행 작업은 1에서 10까지의 인덱스 값을 제곱합니다. 선행 작업이 성공적으로 완료될 경우( <xref:System.Threading.Tasks.Task.Status%2A?displayProperty=nameWithType> 속성이 <xref:System.Threading.Tasks.TaskStatus.RanToCompletion?displayProperty=nameWithType>임) 연속 작업의 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 속성은 각 선행 작업에서 반환된 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 값의 배열입니다. 예제에서는 값을 더하여 1과 10 사이의 모든 숫자의 제곱 합계를 컴퓨팅합니다.  
  
 [!code-csharp[TPL_Continuations#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/whenall1.cs#5)]
 [!code-vb[TPL_Continuations#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/whenall1.vb#5)]  
  
## <a name="continuation-options"></a>연속 옵션  
 단일 작업 연속을 만드는 경우 <xref:System.Threading.Tasks.Task.ContinueWith%2A> 열거형 값을 받는 <xref:System.Threading.Tasks.TaskContinuationOptions?displayProperty=nameWithType> 오버로드를 사용하여 연속 작업이 시작되는 조건을 지정할 수 있습니다. 예를 들어 선행 작업이 성공적으로 완료되거나 오류 상태로 완료되는 경우에만 연속 작업이 실행되도록 지정할 수 있습니다. 선행 작업이 연속 작업을 호출할 준비가 되었을 때 조건이 true가 아니면 연속 작업이 <xref:System.Threading.Tasks.TaskStatus.Canceled?displayProperty=nameWithType> 상태로 바로 전환되며 그 후에 시작할 수 없습니다.  
  
 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A?displayProperty=nameWithType> 메서드 오버로드와 같은 많은 다중 작업 연속 메서드에는 <xref:System.Threading.Tasks.TaskContinuationOptions?displayProperty=nameWithType> 매개 변수도 포함됩니다. 그러나 모든 <xref:System.Threading.Tasks.TaskContinuationOptions?displayProperty=nameWithType> 열거형 멤버의 하위 집합만 유효합니다. <xref:System.Threading.Tasks.TaskContinuationOptions?displayProperty=nameWithType> 열거형에 해당 항목이 있는 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=nameWithType> 값(예: <xref:System.Threading.Tasks.TaskContinuationOptions.AttachedToParent?displayProperty=nameWithType>, <xref:System.Threading.Tasks.TaskContinuationOptions.LongRunning?displayProperty=nameWithType>및 <xref:System.Threading.Tasks.TaskContinuationOptions.PreferFairness?displayProperty=nameWithType>)을 지정할 수 있습니다. 다중 작업 연속에 `NotOn` 또는 `OnlyOn` 옵션을 지정하는 경우 런타임에 <xref:System.ArgumentOutOfRangeException> 예외가 발생합니다.  
  
 작업 연속 옵션에 대한 자세한 내용은 <xref:System.Threading.Tasks.TaskContinuationOptions> 항목을 참조하세요.  
  
## <a name="passing-data-to-a-continuation"></a>연속 작업에 데이터 전달  
 <xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=nameWithType> 메서드는 연속 작업의 사용자 대리자에게 선행 작업에 대한 참조를 인수로 전달합니다. 선행 작업이 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 개체이고 작업이 완료될 때까지 실행된 경우 연속 작업이 해당 작업의 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 속성에 액세스할 수 있습니다.  
  
 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 속성은 작업이 완료될 때까지 차단됩니다. 그러나 작업이 취소되거나 오류가 발생한 경우 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성에 액세스하려고 하면 <xref:System.AggregateException> 예외가 발생합니다. 다음 예제와 같이 <xref:System.Threading.Tasks.TaskContinuationOptions.OnlyOnRanToCompletion> 옵션을 사용하여 이 문제를 방지할 수 있습니다.  
  
 [!code-csharp[TPL_Continuations#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/result1.cs#2)]
 [!code-vb[TPL_Continuations#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/result1.vb#2)]  
  
 선행 작업이 성공적으로 완료될 때까지 실행되지 않은 경우에도 연속 작업을 실행하려면 예외로부터 보호해야 합니다. 한 가지 방법은 선행 작업의 <xref:System.Threading.Tasks.Task.Status%2A?displayProperty=nameWithType> 속성을 테스트하고 상태가 <xref:System.Threading.Tasks.Task%601.Result%2A> 또는 <xref:System.Threading.Tasks.TaskStatus.Faulted> 가 아닌 경우에만 <xref:System.Threading.Tasks.TaskStatus.Canceled>속성에 액세스하는 것입니다. 선행 작업의 <xref:System.Threading.Tasks.Task.Exception%2A> 속성을 검사할 수도 있습니다. 자세한 내용은 [예외 처리](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)를 참조하세요. 다음 예제에서는 상태가 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 인 경우에만 선행 작업의 <xref:System.Threading.Tasks.TaskStatus.RanToCompletion?displayProperty=nameWithType>속성에 액세스하도록 이전 예제를 수정합니다.  
  
 [!code-csharp[TPL_Continuations#7](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/result2.cs#7)]
 [!code-vb[TPL_Continuations#7](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/result2.vb#7)]  
  
## <a name="canceling-a-continuation"></a>연속 작업 취소  
 다음과 같은 경우 연속 작업의 <xref:System.Threading.Tasks.Task.Status%2A?displayProperty=nameWithType> 속성이 <xref:System.Threading.Tasks.TaskStatus.Canceled?displayProperty=nameWithType> 로 설정됩니다.  
  
- 취소 요청에 대한 응답으로 <xref:System.OperationCanceledException> 예외를 발생시키는 경우. 모든 작업과 마찬가지로 연속 작업에 전달된 것과 동일한 토큰이 예외에 포함되어 있으면 협조적 취소의 인정으로 처리됩니다.  
  
- 연속 작업에 <xref:System.Threading.CancellationToken?displayProperty=nameWithType> 속성이 <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> 인 `true`이 전달된 경우. 이 경우에는 연속 작업이 시작되지 않고 <xref:System.Threading.Tasks.TaskStatus.Canceled?displayProperty=nameWithType> 상태로 전환됩니다.  
  
- <xref:System.Threading.Tasks.TaskContinuationOptions> 인수로 설정된 조건이 충족되지 않았으므로 연속 작업이 실행되지 않습니다. 예를 들어 선행 작업이 <xref:System.Threading.Tasks.TaskStatus.Faulted?displayProperty=nameWithType> 상태로 전환되는 경우 <xref:System.Threading.Tasks.TaskContinuationOptions.NotOnFaulted?displayProperty=nameWithType> 옵션이 전달된 연속 작업이 실행되지 않고 <xref:System.Threading.Tasks.TaskStatus.Canceled> 상태로 전환됩니다.  
  
 작업과 해당 연속 작업이 동일한 논리 작업의 두 부분을 나타내는 경우 다음 예제와 같이 두 작업에 모두 동일한 취소 토큰을 전달할 수 있습니다. 취소 토큰은 33으로 나눌 수 있는 정수 목록을 생성하는 선행 작업으로 구성되며 연속 작업에 전달됩니다. 그런 다음 연속 작업이 목록을 표시합니다. 선행 작업과 연속 작업은 모두 임의 간격 동안 정기적으로 일시 중지됩니다. 또한 <xref:System.Threading.Timer?displayProperty=nameWithType> 개체는 5초 시간 제한 간격 후에 `Elapsed` 메서드를 실행하는 데 사용됩니다. 이 예제에서는 현재 실행 중인 작업이 <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A?displayProperty=nameWithType> 메서드를 호출하게 하는 <xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=nameWithType> 메서드를 호출합니다. 선행 작업이나 해당 연속 작업이 실행 중일 때 <xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=nameWithType> 메서드를 호출할지 여부는 임의로 생성된 일시 중지 기간에 따라 달라집니다. 선행 작업이 취소되면 연속 작업은 시작되지 않습니다. 선행 작업이 취소되지 않은 경우에도 토큰을 사용하여 연속 작업을 취소할 수 있습니다.  
  
 [!code-csharp[TPL_Continuations#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/cancellation1.cs#3)]
 [!code-vb[TPL_Continuations#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/cancellation1.vb#3)]  
  
 연속 작업을 만들 때 <xref:System.Threading.Tasks.TaskContinuationOptions.NotOnCanceled?displayProperty=nameWithType> 옵션을 지정하면 연속 작업에 취소 토큰을 제공하지 않고 선행 작업이 취소된 경우에도 연속 작업이 실행되지 않도록 할 수 있습니다. 다음은 간단한 예제입니다.  
  
 [!code-csharp[TPL_Continuations#8](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/cancellation2.cs#8)]
 [!code-vb[TPL_Continuations#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/cancellation2.vb#8)]  
  
 연속 작업이 <xref:System.Threading.Tasks.TaskStatus.Canceled> 상태로 전환된 후 연속 작업에 대해 지정된 <xref:System.Threading.Tasks.TaskContinuationOptions> 에 따라 이후의 연속 작업에 영향을 줄 수 있습니다.  
  
 삭제된 연속 작업은 시작되지 않습니다.  
  
## <a name="continuations-and-child-tasks"></a>연속 작업 및 자식 작업  
 연속 작업은 선행 작업 및 연결된 모든 자식 작업이 완료될 때까지 실행되지 않습니다. 연속 작업은 분리된 자식 작업이 완료되기를 기다리지 않습니다. 다음 두 예제에서는 연속 작업을 만드는 선행 작업에 연결된 자식 작업과 분리된 자식 작업을 보여 줍니다. 다음 예제에서는 모든 자식 작업이 완료된 후에만 연속 작업이 실행되며 예제를 여러 번 실행해도 매번 동일한 출력이 생성됩니다. 기본적으로 <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> 메서드는 기본 작업 생성 옵션이 <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType>인 부모 작업을 만들기 때문에 예제에서는 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType> 메서드를 호출하여 선행 작업을 시작합니다.  
  
 [!code-csharp[TPL_Continuations#9](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/attached1.cs#9)]
 [!code-vb[TPL_Continuations#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/attached1.vb#9)]  
  
 그러나 자식 작업이 선행 작업에서 분리된 경우 자식 작업의 상태에 관계없이 선행 작업이 종료된 즉시 연속 작업이 실행됩니다. 따라서 다음 예제를 여러 번 실행하면 작업 스케줄러가 각 자식 작업을 처리한 방식에 따라 다른 출력이 생성될 수 있습니다.  
  
 [!code-csharp[TPL_Continuations#10](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/detached1.cs#10)]
 [!code-vb[TPL_Continuations#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/detached1.vb#10)]  
  
 선행 작업의 최종 상태는 연결된 자식 작업의 최종 상태에 따라 달라집니다. 분리된 자식 작업의 상태는 부모에 영향을 주지 않습니다. 자세한 내용은 [연결된 자식 작업과 분리된 자식 작업](../../../docs/standard/parallel-programming/attached-and-detached-child-tasks.md)을 참조하세요.  
  
## <a name="associating-state-with-continuations"></a>연속 작업에 상태 연결  
 연속 작업에 임의 상태를 연결할 수 있습니다. <xref:System.Threading.Tasks.Task.ContinueWith%2A> 메서드는 각각 연속 상태를 나타내는 <xref:System.Object> 값을 받는 오버로드된 버전을 제공합니다. 나중에 <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=nameWithType> 속성을 사용하여 이 상태 개체에 액세스할 수 있습니다. 값을 제공하지 않을 경우 이 상태 개체는 `null` 입니다.  
  
 연속 상태는 [APM(비동기 프로그래밍 모델)](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md) 을 사용하는 기존 코드를 TPL을 사용하도록 변환하는 경우에 유용합니다. APM에서는 일반적으로 **Begin**_Method_ 메서드에 개체 상태를 제공하고 나중에 <xref:System.IAsyncResult.AsyncState%2A?displayProperty=nameWithType> 속성을 통해 해당 상태에 액세스합니다. <xref:System.Threading.Tasks.Task.ContinueWith%2A> 메서드를 사용하면 APM을 사용하는 코드를 TPL을 사용하도록 변환할 때 이 상태를 보존할 수 있습니다.  
  
 Visual Studio 디버거에서 <xref:System.Threading.Tasks.Task> 개체로 작업하는 경우에도 연속 상태가 유용할 수 있습니다. 예를 들어 **병렬 작업** 창의 **작업** 열에는 각 작업에 대한 상태 개체의 문자열 표현이 표시됩니다. **병렬 작업** 창에 대한 자세한 내용은 [작업 창 사용](/visualstudio/debugger/using-the-tasks-window)을 참조하세요.  
  
 다음 예제에서는 연속 상태를 사용하는 방법을 보여 줍니다. 연속 작업 체인을 만듭니다. 각 작업은 <xref:System.DateTime> 메서드의 `state` 매개 변수에 대해 현재 시간인 <xref:System.Threading.Tasks.Task.ContinueWith%2A> 개체를 제공합니다. 각 <xref:System.DateTime> 개체는 연속 작업이 만들어진 시간을 나타냅니다. 각 작업은 작업 완료 시간을 나타내는 두 번째 <xref:System.DateTime> 개체를 결과로 생성합니다. 이 예제에서는 모든 작업이 완료된 후 만든 시간과 각 연속 작업의 완료 시간이 표시됩니다.  
  
 [!code-csharp[TPL_ContinuationState#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuationstate/cs/continuationstate.cs#1)]
 [!code-vb[TPL_ContinuationState#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuationstate/vb/continuationstate.vb#1)]  
  
## <a name="handling-exceptions-thrown-from-continuations"></a>연속 작업에서 발생한 예외 처리  
 선행-연속 관계는 부모-자식 관계가 아닙니다. 연속 작업에서 발생한 예외는 선행 작업으로 전파되지 않습니다. 따라서 다른 작업에서 처리하는 것처럼 연속 작업에서 발생한 예외를 다음과 같이 처리합니다.  
  
- <xref:System.Threading.Tasks.Task.Wait%2A>, <xref:System.Threading.Tasks.Task.WaitAll%2A>또는 <xref:System.Threading.Tasks.Task.WaitAny%2A> 메서드나 해당하는 제네릭 항목을 사용하여 연속 작업을 기다릴 수 있습니다. 다음 예제와 같이 동일한 `try` 문에서 선행 작업과 해당 연속 작업을 기다릴 수 있습니다.  
  
     [!code-csharp[TPL_Continuations#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/exception1.cs#6)]
     [!code-vb[TPL_Continuations#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/exception1.vb#6)]  
  
- 두 번째 연속 작업을 사용하여 첫 번째 연속 작업의 <xref:System.Threading.Tasks.Task.Exception%2A> 속성을 관찰할 수 있습니다. 다음 예제에서는 작업이 존재하지 않는 파일을 읽으려고 합니다. 그런 다음 연속 작업이 선행 작업의 예외 정보를 표시합니다.  
  
     [!code-csharp[TPL_Continuations#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/exception2.cs#4)]
     [!code-vb[TPL_Continuations#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/exception2.vb#4)]  
  
     <xref:System.Threading.Tasks.TaskContinuationOptions.OnlyOnFaulted?displayProperty=nameWithType> 옵션으로 실행되었기 때문에 연속 작업은 선행 작업에서 예외가 발생한 경우에만 실행되므로 선행 작업의 <xref:System.Threading.Tasks.Task.Exception%2A> 속성이 `null`이 아니라고 가정할 수 있습니다. 선행 작업에 예외가 발생했는지 여부에 관계없이 연속 작업이 실행되는 경우 다음 코드 조각과 같이 예외를 처리하기 전에 선행 작업의 <xref:System.Threading.Tasks.Task.Exception%2A> 속성이 `null` 이 아닌지 여부를 확인해야 합니다.  
  
     [!code-csharp[TPL_Continuations#11](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_continuations/cs/exception2.cs#11)]
     [!code-vb[TPL_Continuations#11](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_continuations/vb/exception2.vb#11)]  
  
     자세한 내용은 [예외 처리](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)를 참조하세요.  
  
- 연속 작업이 <xref:System.Threading.Tasks.TaskContinuationOptions.AttachedToParent?displayProperty=nameWithType> 옵션으로 만든 연결된 자식 작업인 경우 다른 연결된 자식과 마찬가지로 부모가 해당 예외를 호출 스레드로 다시 전파합니다. 자세한 내용은 [연결된 자식 작업과 분리된 자식 작업](../../../docs/standard/parallel-programming/attached-and-detached-child-tasks.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [TPL(작업 병렬 라이브러리)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)
