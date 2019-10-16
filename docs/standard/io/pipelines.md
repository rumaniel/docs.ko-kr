---
title: I/O 파이프라인 - .NET
description: .NET에서 I/O 파이프라인을 효율적으로 사용하고 코드에서 문제를 방지하는 방법에 대해 알아봅니다.
ms.date: 10/01/2019
ms.technology: dotnet-standard
helpviewer_keywords:
- Pipelines
- Pipelines I/O
- I/O [.NET], Pipelines
author: rick-anderson
ms.author: riande
ms.openlocfilehash: 9e26fb36b77e38c81273ccda370a203dd3388e5c
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291694"
---
# <a name="systemiopipelines-in-net"></a>.NET의 System.IO.Pipelines

<xref:System.IO.Pipelines>는 .NET에서 고성능 I/O를 더 쉽게 수행할 수 있도록 설계된 새 라이브러리입니다. 모든 .NET 구현에서 작동하는 .NET Standard를 대상으로 하는 라이브러리입니다.

<a name="solve"></a>

## <a name="what-problem-does-systemiopipelines-solve"></a>System.IO.Pipelines이 해결하는 문제
<!-- corner case doesn't MT (machine translate)   -->
스트리밍 데이터를 구문 분석하는 앱은 특수하고 비정상적인 코드 흐름이 많은 상용구 코드로 구성됩니다. 상용구와 특수 사례 코드는 복잡하고 유지관리가 어렵습니다.

`System.IO.Pipelines`는 다음을 위해 설계되었습니다.

* 고성능 스트리밍 데이터 구문 분석 수행
* 코드 복잡성 감소

다음 코드는 클라이언트에서 줄로 구분된 메시지를 수신하는 TCP 서버(`'\n'`으로 구분됨)에서 일반적입니다.

```csharp
async Task ProcessLinesAsync(NetworkStream stream)
{
    var buffer = new byte[1024];
    await stream.ReadAsync(buffer, 0, buffer.Length);
    
    // Process a single line from the buffer
    ProcessLine(buffer);
}
```

위의 코드에는 몇 가지 문제가 있습니다.

* `ReadAsync`에 대한 단일 호출에서 전체 메시지(줄의 끝)를 수신하지 못할 수 있습니다.
* `stream.ReadAsync`의 결과를 무시합니다. `stream.ReadAsync`가 읽은 데이터의 양을 반환합니다.
* 단일 `ReadAsync` 호출에서 여러 줄을 읽는 경우를 처리하지 않습니다.
* 각 읽기에 `byte` 배열을 할당합니다.

위의 문제를 해결하려면 다음과 같이 변경해야 합니다.

* 새 줄을 찾을 때까지 들어오는 데이터를 버퍼링합니다.
* 버퍼에 반환된 모든 줄을 구문 분석합니다.
* 줄이 1KB(1024바이트)보다 클 수 있습니다. 코드는 버퍼 안의 전체 줄에 맞추기 위해 구분 기호를 찾을 때까지 입력 버퍼의 크기를 조정해야 합니다.

  * 버퍼 크기를 조정하는 경우 입력에 더 긴 줄이 표시되면 더 많은 버퍼 복사본이 생성됩니다.
  * 불필요한 공간을 줄이려면 줄 읽기에 사용되는 버퍼를 압축합니다.

* 메모리를 반복해서 할당하지 않도록 버퍼 풀링을 사용하는 것이 좋습니다.
* 다음 코드는 이러한 문제 중 일부를 해결합니다.

[!code-csharp[](~/samples/snippets/csharp/pipelines/ProcessLinesAsync.cs?name=snippet)]

이전 코드는 복잡하며, 식별된 모든 문제를 해결하지는 않습니다. 고성능 네트워킹은 일반적으로 성능을 최대화하는 매우 복잡한 코드를 작성하는 것을 의미합니다. `System.IO.Pipelines`는 이러한 종류의 코드 작성을 더 쉽게 만들기 위해 설계되었습니다.

## <a name="pipe"></a>파이프

<xref:System.IO.Pipelines.Pipe> 클래스를 사용하여 `PipeWriter/PipeReader` 쌍을 만들 수 있습니다. `PipeWriter`에 작성된 모든 데이터는 `PipeReader`에서 사용할 수 있습니다.

[!code-csharp[](~/samples/snippets/csharp/pipelines/Pipe.cs?name=snippet2)]

<a name="pbu"></a>

### <a name="pipe-basic-usage"></a>파이프 기본 사용 방법

[!code-csharp[](~/samples/snippets/csharp/pipelines/Pipe.cs?name=snippet)]

두 가지 루프가 있습니다.

* `FillPipeAsync`는 `Socket`에서 읽고 `PipeWriter`에 씁니다.
* `ReadPipeAsync`는 `PipeReader`에서 읽고 들어오는 줄을 구문 분석합니다.

할당된 명시적 버퍼가 없습니다. 모든 버퍼 관리는 `PipeReader` 및 `PipeWriter` 구현에 위임됩니다. 버퍼 관리를 위임하면 더 쉽게 코드 사용을 비즈니스 논리에만 집중할 수 있습니다.

첫 번째 루프에서 다음을 수행합니다.

* <xref:System.IO.Pipelines.PipeWriter.GetMemory(System.Int32)?displayProperty=nameWithType>는 기본 작성기에서 메모리를 가져오기 위해 호출됩니다.
* <xref:System.IO.Pipelines.PipeWriter.Advance(System.Int32)?displayProperty=nameWithType>는 버퍼에 기록된 데이터의 양을 `PipeWriter`에 알리기 위해 호출됩니다.
* <xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A?displayProperty=nameWithType>는 `PipeReader`에서 데이터를 사용할 수 있도록 호출됩니다.

두 번째 루프에서 `PipeReader`는 `PipeWriter`로 작성된 버퍼를 사용합니다. 버퍼는 소켓에서 나옵니다. `PipeReader.ReadAsync`에 대한 호출:

* 두 가지 중요 한 정보를 포함하는 <xref:System.IO.Pipelines.ReadResult>를 반환합니다.

  * `ReadOnlySequence<byte>` 형식으로 읽은 데이터입니다.
  * EOF(데이터의 끝)에 도달했는지 여부를 나타내는 부울 `IsCompleted`입니다. 

EOL(줄의 끝) 구분 기호를 찾은 후 줄을 구문 분석합니다.

* 논리는 버퍼를 처리하여 이미 처리된 작업을 건너뜁니다.
* `PipeReader.AdvanceTo`를 호출하여 사용되고 검사된 데이터의 양을 `PipeReader`에 알려줍니다.

판독기 및 작성기 루프는 `Complete`를 호출하여 종료됩니다. `Complete`는 기본 파이프가 할당된 메모리를 해제하도록 합니다.

### <a name="backpressure-and-flow-control"></a>역 압력 및 흐름 제어

다음과 같이 읽기와 구문 분석이 함께 작동하는 것이 가장 좋습니다.

* 쓰기 스레드는 네트워크의 데이터를 사용하며 이를 버퍼에 저장합니다.
* 구문 분석 스레드는 적절한 데이터 구조를 생성합니다.

일반적으로 다음과 같은 이유로 인해 구문 분석에는 네트워크에서 데이터 블록을 복사하는 것보다 시간이 더 걸립니다.

* 읽기 스레드가 구문 분석 스레드 앞에 있습니다.
* 읽기 스레드의 속도가 느려야 하거나 구문 분석 스레드에 대한 데이터를 저장하기 위해 더 많은 메모리를 할당해야 합니다.

성능을 최적화하기 위해 잦은 일시 중지와 더 많은 메모리 할당 사이에서 균형을 유지합니다.

위의 문제를 해결하기 위해 `Pipe`에는 데이터 흐름을 제어하는 두 가지 설정이 있습니다.

* <xref:System.IO.Pipelines.PipeOptions.PauseWriterThreshold>: <xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A> 일시 중지를 호출하기 전에 버퍼링되어야 하는 데이터의 양을 결정합니다.
* <xref:System.IO.Pipelines.PipeOptions.ResumeWriterThreshold>: `PipeWriter.FlushAsync` 호출을 다시 시작하기 전에 판독기가 관찰해야 하는 데이터의 양을 결정합니다.

![ResumeWriterThreshold 및PauseWriterThreshold의 다이어그램](./media/pipelines/resume-pause.png)

<xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A?displayProperty=nameWithType>:

* `Pipe`의 데이터 크기가 `PauseWriterThreshold`를 넘으면 불완전한 `ValueTask<FlushResult>`를 반환합니다.
* `ResumeWriterThreshold`보다 작으면 `ValueTask<FlushResult>`가 완료됩니다.

하나의 값이 사용될 경우 발생할 수 있는 빠른 순환을 방지하기 위해 두 값이 사용됩니다.

### <a name="examples"></a>예

```csharp
// The Pipe will start returning incomplete tasks from FlushAsync until
// the reader examines at least 5 bytes.
var options = new PipeOptions(pauseWriterThreshold: 10, resumeWriterThreshold: 5);
var pipe = new Pipe(options);
```

### <a name="pipescheduler"></a>PipeScheduler

일반적으로 `async` 및 `await`를 사용하는 경우 비동기 코드는 <xref:System.Threading.Tasks.TaskScheduler> 또는 현재 <xref:System.Threading.SynchronizationContext>에서 다시 시작됩니다.

I/O를 수행하는 경우 I/O가 수행되는 위치를 세부적으로 제어하는 것이 중요합니다. 이 컨트롤을 사용하면 CPU 캐시를 효과적으로 활용할 수 있습니다. 효율적인 캐싱은 웹 서버와 같은 고성능 앱에 매우 중요합니다. <xref:System.IO.Pipelines.PipeScheduler>는 비동기 콜백이 실행되는 위치에 대한 제어를 제공합니다. 기본적으로 다음과 같습니다.

* 현재 <xref:System.Threading.SynchronizationContext>가 사용됩니다.
* `SynchronizationContext`가 없으면 스레드 풀을 사용하여 콜백을 실행합니다.

[!code-csharp[](~/samples/snippets/csharp/pipelines/Program.cs?name=snippet)]

[PipeScheduler.ThreadPool](xref:System.IO.Pipelines.PipeScheduler.ThreadPool)은 스레드 풀에 대한 콜백을 큐에 대기시키는 <xref:System.IO.Pipelines.PipeScheduler> 구현입니다. `PipeScheduler.ThreadPool`은 기본값이며 일반적으로 최상의 선택입니다. [PipeScheduler.Inline](xref:System.IO.Pipelines.PipeScheduler.Inline)은 교착 상태와 같은 의도하지 않은 결과를 발생시킬 수 있습니다.

### <a name="pipe-reset"></a>파이프 다시 설정

`Pipe` 개체를 다시 사용하는 것이 효율적인 경우가 많습니다. 파이프를 다시 설정하려면 `PipeReader`와 `PipeWriter`가 모두 완료될 때 <xref:System.IO.Pipelines.PipeReader> <xref:System.IO.Pipelines.Pipe.Reset%2A>을 호출합니다.

## <a name="pipereader"></a>PipeReader

<xref:System.IO.Pipelines.PipeReader>는 호출자를 대신하여 메모리를 관리합니다. **항상** <xref:System.IO.Pipelines.PipeReader.ReadAsync%2A?displayProperty=nameWithType>를 호출한 후 <xref:System.IO.Pipelines.PipeReader.AdvanceTo%2A?displayProperty=nameWithType>를 호출합니다. 이를 통해 `PipeReader`는 호출자가 메모리를 작업을 완료하는 시기를 알 수 있어서 메모리를 추적할 수 있습니다. `PipeReader.ReadAsync`에서 반환된 `ReadOnlySequence<byte>`는 `PipeReader.AdvanceTo`를 호출할 때까지만 유효합니다. `PipeReader.AdvanceTo`를 호출한 후에는 `ReadOnlySequence<byte>`를 사용할 수 없습니다.

`PipeReader.AdvanceTo`는 두 개의 <xref:System.SequencePosition> 인수를 사용합니다.

* 첫 번째 인수는 사용된 메모리의 양을 결정합니다.
* 두 번째 인수는 관찰된 버퍼의 양을 결정합니다.

데이터를 사용됨으로 표시하면 파이프가 메모리를 기본 버퍼 풀로 반환할 수 있다는 의미입니다. 데이터를 관찰됨으로 표시하면 `PipeReader.ReadAsync`에 대한 다음 호출의 수행 내용을 제어합니다. 모든 항목을 관찰됨으로 표시하면 파이프에 더 많은 데이터를 쓸 때까지 `PipeReader.ReadAsync`에 대한 다음 호출이 반환되지 않는다는 의미입니다. 다른 모든 값을 사용하면 `PipeReader.ReadAsync`에 대한 다음 호출이 관찰된 데이터 *및* 관찰되지 않은 데이터이지만 이미 사용된 데이터를 사용하여 즉시 반환합니다.

### <a name="read-streaming-data-scenarios"></a>스트리밍 데이터 읽기 시나리오

스트리밍 데이터를 읽으려고 할 때 나타나는 몇 가지 일반적인 패턴은 다음과 같습니다.

* 데이터 스트림이 지정된 경우 단일 메시지를 구문 분석합니다.
* 데이터 스트림이 지정된 경우 사용 가능한 모든 메시지를 구문 분석합니다.

다음 예에서는 `ReadOnlySequence<byte>`의 메시지를 구문 분석하는 데 `TryParseMessage` 메서드를 사용합니다. `TryParseMessage`는 단일 메시지를 구문 분석하고 입력 버퍼를 업데이트하여 버퍼에서 구문 분석된 메시지를 자릅니다. `TryParseMessage`는 .NET의 일부가 아니므로 다음 섹션에서 사용되는 사용자 작성 방법입니다.

```csharp
bool TryParseMessage(ref ReadOnlySequence<byte> buffer, out Message message);
```

### <a name="read-a-single-message"></a>단일 메시지 읽기

다음 코드는 `PipeReader`에서 단일 메시지를 읽고 호출자에게 반환합니다.

[!code-csharp[ReadSingleMsg](~/samples/snippets/csharp/pipelines/ReadSingleMsg.cs?name=snippet)]

위의 코드는:

* 단일 메시지를 구문 분석합니다.
* 사용된 `SequencePosition`을 업데이트하고 `SequencePosition`을 검사하여 잘린 입력 버퍼의 시작을 가리킵니다.

`TryParseMessage`는 입력 버퍼에서 구문 분석된 메시지를 제거하므로 두 개의 `SequencePosition` 인수가 업데이트됩니다. 일반적으로 버퍼에서 단일 메시지를 구문 분석할 때 검사된 위치는 다음 중 하나여야 합니다.

* 메시지 끝
* 메시지를 찾을 수 없는 경우 받은 버퍼의 끝

단일 메시지 사례에서 오류가 발생할 가능성이 가장 높습니다. *검사됨*으로 잘못된 값을 전달하면 메모리 부족 예외 또는 무한 루프가 발생할 수 있습니다. 자세한 내용은 이 문서의 [PipeReader의 일반적인 문제](#gotchas) 섹션을 참조하세요.

### <a name="reading-multiple-messages"></a>여러 메시지 읽기

다음 코드는 `PipeReader`에서 모든 메시지를 읽고 각각에 대해 `ProcessMessageAsync`를 호출합니다.

[!code-csharp[MyConnection1](~/samples/snippets/csharp/pipelines/MyConnection1.cs?name=snippet)]

### <a name="cancellation"></a>취소

`PipeReader.ReadAsync`:

* <xref:System.Threading.CancellationToken> 전달을 지원합니다.
* 읽기 보류 중에 `CancellationToken`이 취소되는 경우 <xref:System.OperationCanceledException>이 throw됩니다.
* <xref:System.IO.Pipelines.PipeReader.CancelPendingRead%2A?displayProperty=nameWithType>을 통해 현재 읽기 작업을 취소하는 방법을 지원하여 예외 증가를 방지합니다. `PipeReader.CancelPendingRead`를 호출하면 `PipeReader.ReadAsync`에 대한 현재 또는 다음 호출이 `IsCanceled`가 `true`로 설정된 <xref:System.IO.Pipelines.ReadResult>를 반환합니다. 이는 기존 읽기 루프를 비파괴적이고 예외 없는 방식으로 중지하는 데 유용할 수 있습니다.

[!code-csharp[MyConnection](~/samples/snippets/csharp/pipelines/MyConnection.cs?name=snippet)]

<a name="gotchas"></a>

### <a name="pipereader-common-problems"></a>PipeReader의 일반적인 문제

* `consumed` 또는 `examined`에 잘못된 값을 전달하면 이미 읽은 데이터를 읽을 수 있습니다.
* `buffer.End`를 검사됨으로 전달하면 다음과 같은 결과를 초래할 수 있습니다.

  * 중단된 데이터
  * 데이터가 사용되지 않는 경우 OOM(메모리 부족) 예외 발생 (예: 버퍼에서 한 번에 하나의 메시지를 처리하는 경우 `PipeReader.AdvanceTo(position, buffer.End)`)

* `consumed` 또는 `examined`에 잘못된 값을 전달하면 무한 루프가 발생할 수 있습니다. 예를 들어 `PipeReader.AdvanceTo(buffer.Start)`는 `buffer.Start`이 변경되지 않은 경우 `PipeReader.ReadAsync`에 대한 다음 호출이 새 데이터가 도착하기 전에 즉시 반환되도록 합니다.
* `consumed` 또는 `examined`에 잘못된 값을 전달하면 무한 버퍼링(최종 OOM)이 발생할 수 있습니다.
* `PipeReader.AdvanceTo`를 호출한 후 `ReadOnlySequence<byte>`를 사용하면 메모리가 손상될 수 있습니다(사용 가능해진 이후 사용).
* `PipeReader.Complete/CompleteAsync`를 호출하지 못하면 메모리 누수가 발생할 수 있습니다.
* 버퍼를 처리하기 전에 <xref:System.IO.Pipelines.ReadResult.IsCompleted?displayProperty=nameWithType>를 확인하고 읽기 논리를 종료하면 데이터 손실이 발생합니다. 루프 종료 조건은 `ReadResult.Buffer.IsEmpty` 및 `ReadResult.IsCompleted`를 기반으로 해야 합니다. 이렇게 하면 무한 루프가 잘못 발생할 수 있습니다.

#### <a name="problematic-code"></a>문제 코드

❌ **데이터 손실**

`IsCompleted`가 `true`로 설정된 경우 `ReadResult`는 최종 데이터 세그먼트를 반환할 수 있습니다. 읽기 루프를 종료하기 전에 해당 데이터를 읽지 않으면 데이터가 손실됩니다.

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

[!code-csharp[DoNotUse#1](~/samples/snippets/csharp/pipelines/DoNotUse.cs?name=snippet)]

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

❌ **무한 루프**

`Result.IsCompleted`가 `true`이지만 버퍼에 완전한 메시지가 없는 경우 다음 논리로 인해 무한 루프가 발생할 수 있습니다.

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

[!code-csharp[DoNotUse#2](~/samples/snippets/csharp/pipelines/DoNotUse.cs?name=snippet2)]

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

동일한 문제가 있는 또 다른 코드는 다음과 같습니다. `ReadResult.IsCompleted`를 확인하기 전에 비어 있지 않은 버퍼를 확인하는 것입니다. `else if`이기 때문에 버퍼에 완전한 메시지가 없는 경우 무한 반복됩니다.

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

[!code-csharp[DoNotUse#3](~/samples/snippets/csharp/pipelines/DoNotUse.cs?name=snippet3)]

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

❌ **예기치 않은 중단**

`examined` 위치에서 `buffer.End`를 사용하여 `PipeReader.AdvanceTo`를 무조건 호출하면 단일 메시지를 구문 분석할 때 작동이 중지될 수 있습니다. `PipeReader.AdvanceTo`에 대한 다음 호출은 다음까지 반환되지 않습니다.

* 파이프에 기록된 데이터가 더 있음
* 새 데이터는 이전에 검사되지 않았음

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

[!code-csharp[DoNotUse#4](~/samples/snippets/csharp/pipelines/DoNotUse.cs?name=snippet4)]

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

❌ **OOM(메모리 부족)**

다음 조건에서 다음 코드는 <xref:System.OutOfMemoryException>이 발생할 때까지 버퍼링을 유지합니다.

* 최대 메시지 크기가 없습니다.
* `PipeReader`에서 반환된 데이터는 완전한 메시지를 생성하지 않습니다. 예를 들어, 다른 쪽에서 매우 용량이 큰 메시지(예: 4GB 메시지)를 작성하기 때문에 완전한 메시지를 생성하지 않습니다.

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

[!code-csharp[DoNotUse#5](~/samples/snippets/csharp/pipelines/DoNotUse.cs?name=snippet5)]

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

❌ **메모리 손상**

버퍼를 읽는 도우미를 작성하는 경우 `Advance`를 호출하기 전에 반환된 모든 페이로드를 복사해야 합니다. 다음 예제에서는 `Pipe`가 버렸고 다음 작업(읽기/쓰기)에 다시 사용할 수도 있는 메모리를 반환합니다.

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

[!code-csharp[DoNotUse#Message](~/samples/snippets/csharp/pipelines/DoNotUse.cs?name=snippetMessage)]

[!code-csharp[DoNotUse#6](~/samples/snippets/csharp/pipelines/DoNotUse.cs?name=snippet6)]

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

## <a name="pipewriter"></a>PipeWriter

<xref:System.IO.Pipelines.PipeWriter>는 호출자를 대신해 쓰기 위한 버퍼를 관리합니다. `PipeWriter`는 [`IBufferWriter<byte>`](xref:System.Buffers.IBufferWriter`1)를 구현합니다. `IBufferWriter<byte>`는 추가 버퍼 복사본 없이 쓰기를 수행하기 위해 버퍼에 액세스할 수 있습니다.

[!code-csharp[MyPipeWriter](~/samples/snippets/csharp/pipelines/MyPipeWriter.cs?name=snippet)]

이전 코드는 다음과 같습니다.

* <xref:System.IO.Pipelines.PipeWriter.GetSpan%2A>을 사용하여 `PipeWriter`에서 최소 5바이트의 버퍼를 요청합니다.
* 반환된 `Span<byte>`에 ASCII 문자열 `"Hello"`를 위한 바이트를 씁니다.
* <xref:System.IO.Pipelines.PipeWriter.Advance%2A>를 호출하여 버퍼에 쓴 바이트 수를 표시합니다.
* 기본 디바이스로 바이트를 전송하는 `PipeWriter`를 플러시합니다.

이전 작성 메서드에서는 `PipeWriter`에서 제공하는 버퍼를 사용합니다. 또는, <xref:System.IO.Pipelines.PipeWriter.WriteAsync%2A?displayProperty=nameWithType>:

* 기존 버퍼를 `PipeWriter`에 복사합니다.
* `GetSpan`, `Advance`를 적절하게 호출하고 <xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A>를 호출합니다.

[!code-csharp[MyPipeWriter#2](~/samples/snippets/csharp/pipelines/MyPipeWriter.cs?name=snippet2)]

### <a name="cancellation"></a>취소

<xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A>에서는 <xref:System.Threading.CancellationToken> 전달을 지원합니다. `CancellationToken`을 전달하면 플러시가 보류 중인 동안 토큰이 취소되는 경우 `OperationCanceledException`을 반환됩니다. `PipeWriter.FlushAsync`는 예외를 발생시키지 않고 <xref:System.IO.Pipelines.PipeWriter.CancelPendingFlush%2A?displayProperty=nameWithType>을 통해 현재 플러시 작업을 취소하는 메서드를 지원합니다. `PipeWriter.CancelPendingFlush`를 호출하면 `PipeWriter.FlushAsync` 또는 `PipeWriter.WriteAsync`에 대한 현재 또는 다음 호출이 `IsCanceled`가 `true`로 설정된 <xref:System.IO.Pipelines.FlushResult>를 반환합니다. 이는 생성 플러시를 비파괴적이고 예외 없는 방식으로 중지하는 데 유용할 수 있습니다.

<a name="pwcp"></a>

### <a name="pipewriter-common-problems"></a>PipeWriter의 일반적인 문제

* <xref:System.IO.Pipelines.PipeWriter.GetSpan%2A> 및 <xref:System.IO.Pipelines.PipeWriter.GetMemory%2A>는 적어도 요청된 양의 메모리를 포함하는 버퍼를 반환합니다. 정확한 버퍼 크기를 가정하지 **마세요**.
* 연속 호출이 동일한 버퍼 또는 동일한 크기의 버퍼를 반환한다는 보장은 없습니다.
* 추가 데이터를 계속 작성하려면 <xref:System.IO.Pipelines.PipeWriter.Advance%2A>를 호출한 후 새 버퍼를 요청해야 합니다. 이전에 획득한 버퍼에 쓸 수 없습니다.
* `GetMemory` 또는 `GetSpan`을 호출하면 `FlushAsync`에 대한 불완전한 호출이 안전하지 않습니다.
* 플러시된 데이터가 없는 상태에서 `Complete` 또는 `CompleteAsync`를 호출하면 메모리가 손상될 수 있습니다.

## <a name="iduplexpipe"></a>IDuplexPipe

<xref:System.IO.Pipelines.IDuplexPipe>는 읽기와 쓰기를 모두 지원하는 형식에 대한 계약입니다. 예를 들어 네트워크 연결은 `IDuplexPipe`로 표시됩니다.

 `PipeReader` 및 `PipeWriter`를 포함하는 `Pipe`와 달리 `IDuplexPipe`는 전체 이중 연결의 단일한 측면을 나타냅니다. 이는 `PipeWriter`로 쓴 내용이 `PipeReader`에서 읽히지 않는다는 의미입니다.

## <a name="streams"></a>스트림

스트림 데이터를 읽거나 쓸 때는 일반적으로 역직렬 변환기를 사용하여 데이터를 읽고 직렬 변환기를 사용하여 데이터를 씁니다. 대부분의 읽기 및 쓰기 스트림 API에는 `Stream` 매개 변수가 있습니다. 기존 API와 쉽게 통합할 수 있도록 `PipeReader` 및 `PipeWriter`는 <xref:System.IO.Pipelines.PipeReader.AsStream%2A>를 제공합니다.  <xref:System.IO.Pipelines.PipeWriter.AsStream%2A>은 `PipeReader` 또는 `PipeWriter` 주위에 `Stream` 구현을 반환합니다.
