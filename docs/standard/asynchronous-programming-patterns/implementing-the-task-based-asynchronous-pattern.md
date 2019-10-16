---
title: 작업 기반 비동기 패턴 구현
ms.date: 06/14/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- .NET Framework, and TAP
- asynchronous design patterns, .NET Framework
- TAP, .NET Framework support for
- Task-based Asynchronous Pattern, .NET Framework support for
- .NET Framework, asynchronous design patterns
ms.assetid: fab6bd41-91bd-44ad-86f9-d8319988aa78
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 670cdb369920663ffa62e224bdd5aa495fc7e622
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66377693"
---
# <a name="implementing-the-task-based-asynchronous-pattern"></a>작업 기반 비동기 패턴 구현
TAP(작업 기반 비동기 패턴)는 세 가지 방식으로 구현할 수 있습니다. 즉 Visual Studio에서 C# 또는 Visual Basic 컴파일러를 사용하여 구현하거나, 수동으로 구현하거나, 컴파일러와 수동 방식을 함께 사용하여 구현할 수 있습니다. 다음 섹션에서는 각 방법에 대해 자세히 설명합니다. TAP 패턴을 사용하면 계산 바운드 및 I/O 바운드 비동기 작업을 모두 구현할 수 있습니다. 각 작업 유형에 대해서는 [워크로드](#workloads) 섹션에서 설명합니다.

## <a name="generating-tap-methods"></a>TAP 메서드 생성

### <a name="using-the-compilers"></a>컴파일러 사용
.NET Framework 4.5부터는 `async` 키워드(Visual Basic의 경우 `Async`)로 특성이 지정된 메서드가 비동기 메서드로 간주되며, C# 및 Visual Basic 컴파일러는 TAP를 사용해 비동기로 메서드를 구현하는 데 필요한 변환을 수행합니다. 비동기 메서드는 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 또는 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 개체를 반환해야 합니다. 두 번째 개체의 경우 함수 본문은 `TResult`를 반환해야 하며 컴파일러는 결과 작업 개체를 통해 이 결과가 제공되는지를 확인합니다. 마찬가지로 메서드 본문 내에서 처리되지 않는 모든 예외는 출력 작업으로 마샬링되므로 결과 작업이 <xref:System.Threading.Tasks.TaskStatus.Faulted?displayProperty=nameWithType> 상태로 종료됩니다. 단, <xref:System.OperationCanceledException> 또는 파생 형식이 처리되지 않는 경우에는 결과 작업이 <xref:System.Threading.Tasks.TaskStatus.Canceled?displayProperty=nameWithType> 상태로 종료됩니다.

### <a name="generating-tap-methods-manually"></a>수동으로 TAP 메서드 생성
구현을 보다 효율적으로 제어하기 위해 TAP 패턴을 수동으로 구현할 수 있습니다. 컴파일러는 <xref:System.Threading.Tasks?displayProperty=nameWithType> 네임스페이스의 지원 형식 및 <xref:System.Runtime.CompilerServices?displayProperty=nameWithType> 네임스페이스에서 노출되는 공개 노출 영역을 사용합니다. TAP를 직접 구현하려면 <xref:System.Threading.Tasks.TaskCompletionSource%601> 개체를 만들고 비동기 작업을 수행한 다음 작업이 완료되면 <xref:System.Threading.Tasks.TaskCompletionSource%601.SetResult%2A>, <xref:System.Threading.Tasks.TaskCompletionSource%601.SetException%2A> 또는 <xref:System.Threading.Tasks.TaskCompletionSource%601.SetCanceled%2A> 메서드나 이러한 메서드 중 하나의 `Try` 버전을 호출합니다. TAP 메서드를 수동으로 구현할 때는 표시된 비동기 작업이 완료되면 결과 작업을 완료해야 합니다. 예:

[!code-csharp[Conceptual.TAP_Patterns#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#1)]
[!code-vb[Conceptual.TAP_Patterns#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#1)]

### <a name="hybrid-approach"></a>혼합 방식
 TAP 패턴은 수동으로 구현하되 구현의 핵심 논리를 컴파일러에 위임하면 유용할 수 있습니다. 예를 들어 예외가 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 개체를 통해 노출되는 대신 메서드의 직접 호출자로 이스케이프될 수 있도록 컴파일러 생성 비동기 메서드 외부에서 인수를 확인하려는 경우 혼합 방식을 사용할 수 있습니다.

 [!code-csharp[Conceptual.TAP_Patterns#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#2)]
 [!code-vb[Conceptual.TAP_Patterns#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#2)]

 또한 빠른 경로 최적화를 구현하며 캐시된 작업을 반환하려는 경우에도 이러한 위임이 유용합니다.

## <a name="workloads"></a>작업
컴퓨트 바운드 및 I/O 바운드 비동기 작업을 모두 TAP 메서드로 구현할 수 있습니다. 그러나 TAP 메서드를 라이브러리에서 공개적으로 노출할 때는 I/O 바운드 연산이 포함된 작업에만 해당 메서드를 제공해야 합니다. 이러한 작업은 계산도 포함할 수 있지만 순수한 계산 작업이어서는 안 됩니다. 순수한 계산 바운드 메서드의 경우에는 동기 구현으로만 표시되어야 합니다. 그러면 해당 메서드를 사용하는 코드는 작업을 다른 스레드로 오프로드하거나 병렬 처리 기능을 제공하기 위해 해당 동기 메서드의 호출을 작업으로 래핑할지 여부를 선택할 수 있습니다. 그리고 메서드가 I/O 바운드인 경우에는 비동기 구현으로만 표시되어야 합니다.

### <a name="compute-bound-tasks"></a>계산 바운드 작업
<xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 클래스는 계산을 많이 수행하는 작업에 가장 적합합니다. 이 클래스는 기본적으로 <xref:System.Threading.ThreadPool> 클래스 내의 특수 지원을 활용하여 효율적 실행을 제공하며 비동기 계산 실행 시기, 위치 및 방법에 대한 상당한 제어 기능도 제공합니다.

다음과 같은 방법으로 컴퓨트 바인딩 작업을 생성할 수 있습니다.

- .NET Framework 4에서 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType> 메서드를 사용합니다. 이 메서드는 비동기식으로 실행할 대리자(일반적으로 <xref:System.Action%601> 또는 <xref:System.Func%601>)를 수락합니다. <xref:System.Action%601> 대리자를 제공하는 경우 메서드는 해당 대리자의 비동기 실행을 나타내는 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 개체를 반환합니다. <xref:System.Func%601> 대리자를 제공하는 경우 메서드는 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 개체를 반환합니다. <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> 메서드의 오버로드는 취소 토큰(<xref:System.Threading.CancellationToken>), 작업 만들기 옵션(<xref:System.Threading.Tasks.TaskCreationOptions>) 및 작업 스케줄러(<xref:System.Threading.Tasks.TaskScheduler>)를 수락합니다. 이러한 모든 항목은 작업 예약과 실행에 대한 세분화된 제어 기능을 제공합니다. 현재 작업 스케줄러를 대상으로 하는 팩터리 인스턴스는 <xref:System.Threading.Tasks.Task.Factory%2A> 클래스의 정적 속성(<xref:System.Threading.Tasks.Task>)으로 사용 가능합니다. 예를 들면 `Task.Factory.StartNew(…)`와 같습니다.

- .NET Framework 4.5 이상 버전(.NET Core 및 .NET Standard 포함)에서는 정적 <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> 메서드를 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType>의 바로 가기로 사용합니다. <xref:System.Threading.Tasks.Task.Run%2A>을 사용하여 스레드 풀을 대상으로 하는 컴퓨트 바운드 작업을 쉽게 시작할 수 있습니다. .NET Framework 4.5 이상 버전에서는 기본적으로 이 메커니즘을 통해 계산 바운드 작업을 시작합니다. 작업에 대해 더욱 세분화된 제어가 필요할 때만 `StartNew`를 직접 사용합니다.

- 작업을 개별적으로 생성하고 예약하려는 경우 `Task` 형식 또는 `Start` 메서드의 생성자를 사용합니다. 공용 메서드는 이미 시작된 작업만 반환해야 합니다.

- <xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=nameWithType> 메서드의 오버로드를 사용합니다. 이 메서드는 다른 작업이 완료되면 예약된 새 작업을 만듭니다. 일부 <xref:System.Threading.Tasks.Task.ContinueWith%2A> 오버로드는 연속 작업 예약과 실행을 효율적으로 제어할 수 있도록 취소 토큰, 연속 옵션 및 작업 스케줄러를 수락합니다.

- <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A?displayProperty=nameWithType> 메서드를 사용합니다. 이러한 메서드는 제공된 작업 집합이 모두 완료되거나 하나라도 완료되면 예약된 새 작업을 만듭니다. 이러한 메서드는 작업 예약과 실행을 제어하기 위한 오버로드도 제공합니다.

컴퓨트 바운드 작업에서 시스템은 작업 실행을 시작하기 전에 취소 요청을 받으면 예약된 작업 실행을 차단할 수 있습니다. 따라서 취소 토큰(<xref:System.Threading.CancellationToken> 개체)을 제공하는 경우 토큰을 모니터링하는 비동기 코드로 해당 토큰을 전달할 수 있습니다. 또한 `StartNew` 런타임도 토큰을 모니터링할 수 있도록 `Run` 또는 `Task`과 같은 앞에서 설명한 메서드 중 하나에 토큰을 제공할 수도 있습니다.

예를 들어 이미지를 렌더링하는 비동기 메서드의 경우를 고려해 보겠습니다. 작업 본문은 렌더링 중에 취소 요청이 도착하는 경우 코드를 일찍 종료할 수 있도록 취소 토큰을 폴링할 수 있습니다. 또한 렌더링을 시작하기 전에 취소 요청이 도착하면 렌더링 작업을 차단할 수 있습니다.

[!code-csharp[Conceptual.TAP_Patterns#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#3)]
[!code-vb[Conceptual.TAP_Patterns#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#3)]

컴퓨트 바운드 작업은 다음 조건 중 하나 이상에 해당하는 경우 <xref:System.Threading.Tasks.TaskStatus.Canceled>에서 종료됩니다.

- 작업이 <xref:System.Threading.CancellationToken> 상태로 전환되기 전에 `StartNew` 또는 `Run`과 같은 creation 메서드에 대한 인수로 제공되는 <xref:System.Threading.Tasks.TaskStatus.Running> 개체를 통해 취소 요청이 도착하는 경우

- <xref:System.OperationCanceledException> 예외가 작업의 본문 내에서 처리되지 않고, 작업으로 전달되는 것과 같은 <xref:System.Threading.CancellationToken>이 예외에 포함되어 있으며, 토큰에 취소가 요청되었음이 표시되는 경우

다른 예외가 작업의 본문 내에서 처리되지 않는 경우 작업은 <xref:System.Threading.Tasks.TaskStatus.Faulted> 상태로 종료되며 작업에서 대기하거나 결과에 액세스하려고 하면 예외가 throw됩니다.

### <a name="io-bound-tasks"></a>I/O 바운드 작업
스레드를 통해 전체 실행을 직접 지원해서는 안 되는 작업을 만들려면 <xref:System.Threading.Tasks.TaskCompletionSource%601> 형식을 사용합니다. 이 형식은 연결된 <xref:System.Threading.Tasks.TaskCompletionSource%601.Task%2A> 인스턴스를 반환하는 <xref:System.Threading.Tasks.Task%601> 속성을 노출합니다. 이 작업의 수명 주기는 <xref:System.Threading.Tasks.TaskCompletionSource%601>, <xref:System.Threading.Tasks.TaskCompletionSource%601.SetResult%2A>, <xref:System.Threading.Tasks.TaskCompletionSource%601.SetException%2A> 등의 <xref:System.Threading.Tasks.TaskCompletionSource%601.SetCanceled%2A> 메서드와 해당 `TrySet` 변형을 통해 제어됩니다.

지정된 시간이 지나면 완료되는 작업을 만든다고 가정해 보겠습니다. 예를 들어 사용자 인터페이스에서 작업을 지연시킬 수 있습니다. <xref:System.Threading.Timer?displayProperty=nameWithType> 클래스는 지정된 시간이 지나면 대리자를 비동기식으로 호출하는 기능을 이미 제공합니다. <xref:System.Threading.Tasks.TaskCompletionSource%601>를 사용하면 다음과 같이 타이머 앞에 <xref:System.Threading.Tasks.Task%601>를 배치할 수 있습니다.

[!code-csharp[Conceptual.TAP_Patterns#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#4)]
[!code-vb[Conceptual.TAP_Patterns#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#4)]

.NET Framework 4.5부터는 이러한 용도로 <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> 메서드가 제공되며, 예를 들어 다른 비동기 메서드 내에서 해당 메서드를 사용하여 비동기 폴링 루프를 구현할 수 있습니다.

[!code-csharp[Conceptual.TAP_Patterns#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#5)]
[!code-vb[Conceptual.TAP_Patterns#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#5)]

<xref:System.Threading.Tasks.TaskCompletionSource%601> 클래스에는 상응하는 제네릭이 아닌 클래스가 없습니다. 그러나 <xref:System.Threading.Tasks.Task%601>는 <xref:System.Threading.Tasks.Task>에서 파생되므로 작업만 반환하는 I/O 바운드 메서드에 대해 제네릭 <xref:System.Threading.Tasks.TaskCompletionSource%601> 개체를 사용할 수 있습니다. 이렇게 하려면 더미 `TResult`가 포함된 소스를 사용할 수 있습니다. (<xref:System.Boolean>을 사용하는 것이 좋기는 하지만, <xref:System.Threading.Tasks.Task> 사용자가 해당 항목을 <xref:System.Threading.Tasks.Task%601>로 다운캐스트할 수도 있는 경우에는 개인 `TResult` 형식을 대신 사용할 수 있습니다. 예를 들어 이전 예제의 `Delay` 메서드는 결과 오프셋(`Task<DateTimeOffset>`)과 함께 현재 시간을 반환합니다. 이러한 결과 값이 필요하지 않다면 대신 메서드를 다음과 같이 코딩할 수 있습니다. 이 경우 반환 값이 변경되며 인수는 <xref:System.Threading.Tasks.TaskCompletionSource%601.TrySetResult%2A>로 변경됩니다.

[!code-csharp[Conceptual.TAP_Patterns#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#6)]
[!code-vb[Conceptual.TAP_Patterns#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#6)]

### <a name="mixed-compute-bound-and-io-bound-tasks"></a>계산 바운드 및 I/O 바운드 혼합 작업
비동기 메서드에서는 컴퓨트 바운드 또는 I/O 바운드 작업 중 하나만 사용할 수 있는 것이 아니라 두 작업을 혼합하여 사용할 수도 있습니다. 실제로 여러 비동기 작업이 큰 혼합 작업으로 결합되는 경우가 많습니다. 예를 들어, 일부 입력 `RenderAsync`를 기반으로 이미지를 렌더링하기 위해 계산을 많이 하는 작업을 수행한 이전의 예에 있는 `imageData` 메서드를 고려합니다. 이 `imageData`는 비동기 방식으로 액세스하는 웹 서비스에서 제공된 것일 수 있습니다.

[!code-csharp[Conceptual.TAP_Patterns#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#7)]
[!code-vb[Conceptual.TAP_Patterns#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#7)]

또한 이 예제에서는 여러 비동기 작업을 통해 단일 취소 토큰 스레드를 만드는 방법도 보여 줍니다. 자세한 내용은 [작업 기반 비동기 패턴 사용](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)의 취소 사용 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [TAP(작업 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)
- [Consuming the Task-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)
- [다른 비동기 패턴 및 형식과의 Interop](../../../docs/standard/asynchronous-programming-patterns/interop-with-other-asynchronous-patterns-and-types.md)
