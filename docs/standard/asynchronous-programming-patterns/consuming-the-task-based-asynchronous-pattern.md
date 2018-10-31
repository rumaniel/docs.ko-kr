---
title: 작업 기반 비동기 패턴 사용
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET Framework, and TAP
- asynchronous design patterns, .NET Framework
- TAP, .NET Framework support for
- Task-based Asynchronous Pattern, .NET Framework support for
- .NET Framework, asynchronous design patterns
ms.assetid: 033cf871-ae24-433d-8939-7a3793e547bf
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: eac5f9f6c8b47a6f14898eac2505ecc890015010
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50188122"
---
# <a name="consuming-the-task-based-asynchronous-pattern"></a>작업 기반 비동기 패턴 사용

TAP(작업 기반 비동기 패턴)을 사용하여 비동기 작업을 수행할 경우 콜백을 사용하면 차단 없이 대기를 진행할 수 있습니다.  작업의 경우 이는 <xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=nameWithType>와 같은 메서드를 통해 수행됩니다. 언어 기반 비동기 지원은 정상적인 제어 흐름 내에서 비동기 작업이 대기할 수 있도록 함으로써 콜백 숨김을 지원하고, 컴파일러에서 생성된 코드는 이와 동일한 API 수준 지원을 제공합니다.

## <a name="suspending-execution-with-await"></a>Await로 실행 일시 중지
 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]부터는 C#의 [await](~/docs/csharp/language-reference/keywords/await.md) 키워드 및 Visual Basic의 [Await 연산자](~/docs/visual-basic/language-reference/operators/await-operator.md)를 사용하여 <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 개체를 비동기적으로 대기할 수 있습니다. <xref:System.Threading.Tasks.Task> 개체를 대기하고 있을 때 `await` 식은 `void` 형식입니다. <xref:System.Threading.Tasks.Task%601> 개체를 대기하고 있을 때 `await` 식은 `TResult` 형식입니다. `await` 식은 비동기 메서드의 본문 내에서 발생해야 합니다. [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]의 C# 및 Visual Basic 언어 지원에 대한 자세한 내용은 C# 및 Visual Basic 언어 사양을 참조하세요.

 내부적으로 await 기능은 연속을 사용해서 작업에 콜백을 설치합니다.  이 콜백은 일시 중지 시점에서 비동기 메서드를 재개합니다. 비동기 메서드가 재개될 때 대기된 작업이 성공적으로 완료되고 <xref:System.Threading.Tasks.Task%601>인 경우 해당 `TResult`가 반환됩니다.  대기된 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체가 <xref:System.Threading.Tasks.TaskStatus.Canceled> 상태에서 종료된 경우 <xref:System.OperationCanceledException> 예외가 throw됩니다.  대기된 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체가 <xref:System.Threading.Tasks.TaskStatus.Faulted> 상태에서 종료된 경우 오류를 초래한 예외가 throw됩니다. `Task`에서는 여러 식의 결과로 오류가 발생할 수 있지만 이러한 예외 중 하나만 전파됩니다. 그러나 <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=nameWithType> 속성은 모든 오류가 포함된 <xref:System.AggregateException> 예외를 반환합니다.

 동기화 컨텍스트(<xref:System.Threading.SynchronizationContext> 개체)가 일시 중단될 때(예를 들어 <xref:System.Threading.SynchronizationContext.Current%2A?displayProperty=nameWithType> 속성이 `null`이 아닌 경우) 비동기 메서드를 실행하고 있던 스레드와 연결되어 있는 경우 비동기 메서드는 컨텍스트의 <xref:System.Threading.SynchronizationContext.Post%2A> 메서드를 사용하여 동일한 동기화 컨텍스트에서 다시 시작됩니다. 그러지 않으면 일시 중단될 때 최신 상태인 작업 스케줄러(<xref:System.Threading.Tasks.TaskScheduler> 개체)를 사용합니다. 일반적으로 이 개체는 스레드 풀을 대상으로 하는 기본 작업 스케줄러(<xref:System.Threading.Tasks.TaskScheduler.Default%2A?displayProperty=nameWithType>)입니다. 이 작업 스케줄러는 대기 중이던 비동기 작업이 완료된 위치에서 다시 시작되어야 하는지 또는 재개를 예약해야 하는지를 결정합니다. 기본 스케줄러는 일반적으로 대기 중이던 작업이 완료된 스레드에서 실행이 계속되도록 허용합니다.

 비동기 메서드가 호출되면 아직 완료되지 않은 대기 가능 인스턴스에 대한 첫 번째 대기 식이 나올 때까지, 즉 호출이 호출자에게 반환될 때까지 함수 본문을 동기적으로 실행합니다. 비동기 메서드가 `void`를 반환하지 않으면 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체가 반환되어 진행 중인 계산을 나타냅니다. void가 아닌 비동기 메서드에서, return 문이 나오거나 메서드 본문의 끝에 도달하는 경우 작업이 <xref:System.Threading.Tasks.TaskStatus.RanToCompletion> 최종 상태로 완료됩니다. 처리되지 않은 예외로 인해 제어 권한이 비동기 메서드의 본문을 벗어날 경우 작업이 <xref:System.Threading.Tasks.TaskStatus.Faulted> 상태로 종료됩니다. 해당 예외가 <xref:System.OperationCanceledException>인 경우 대신 작업이 <xref:System.Threading.Tasks.TaskStatus.Canceled> 상태로 종료됩니다. 이러한 방식으로 결과 또는 예외가 게시됩니다.

 이 동작은 몇 가지 중요한 형태로 변형되어 발생합니다.  성능상의 이유로 작업이 대기될 때 이미 거의 완료되었으면 제어가 일시 중단되지 않고 함수는 계속 실행됩니다.  또한 원래 컨텍스트로 돌아간다고 해서 항상 원하는 동작을 얻을 수 있는 것은 아니며 변경될 수 있습니다. 이 내용에 대해서는 다음 섹션에서 좀 더 자세히 설명합니다.

### <a name="configuring-suspension-and-resumption-with-yield-and-configureawait"></a>Yield 및 ConfigureAwait를 사용하여 일시 중단 및 재개 구성
 몇 가지 메서드는 비동기 메서드 실행을 좀 더 강력하게 제어합니다. 예를 들어 다음과 같이 <xref:System.Threading.Tasks.Task.Yield%2A?displayProperty=nameWithType> 메서드를 사용하여 비동기 메서드에 양보점(yield point)을 삽입할 수 있습니다.

```csharp
public class Task : …
{
    public static YieldAwaitable Yield();
    …
}
```

 이 작업은 비동기적으로 원래 컨텍스트에 다시 게시하거나 원래 컨텍스트를 예약하는 것과 같습니다.

```csharp
Task.Run(async delegate
{
    for(int i=0; i<1000000; i++)
    {
        await Task.Yield(); // fork the continuation into a separate work item
        ...
    }
});
```

 또한 비동기 메서드에서 일시 중단 및 다시 시작에 대한 제어를 개선하기 위해 <xref:System.Threading.Tasks.Task.ConfigureAwait%2A?displayProperty=nameWithType> 메서드를 사용할 수도 있습니다.  앞서 언급했듯이 기본적으로 비동기 메서드가 일시 중단되었던 당시의 현재 컨텍스트가 캡처되며 캡처된 해당 컨텍스트는 다시 시작할 때 비동기 메서드의 연속을 호출하는 데 사용합니다.  대부분의 경우에서 사용자가 원하는 정확한 행동이 바로 이것일 것입니다.  연속 컨텍스트를 별로 중요하게 생각하지 않을 수도 있고 원래 컨텍스트로의 다시 게시를 피함으로써 더 나은 성능을 얻을 수 있는 경우도 있습니다.  이 기능을 사용하도록 설정하려면 <xref:System.Threading.Tasks.Task.ConfigureAwait%2A?displayProperty=nameWithType> 메서드를 사용하여 대기 작업에 컨텍스트를 캡처하고 다시 시작하지 않고 대기 중인 비동기 작업이 완료될 때마다 실행을 계속하도록 지시합니다.

```csharp
await someTask.ConfigureAwait(continueOnCapturedContext:false);
```

## <a name="canceling-an-asynchronous-operation"></a>비동기 작업 취소
 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]부터는 취소를 지원하는 TAP 메서드가 취소 토큰(<xref:System.Threading.CancellationToken> 개체)을 수락하는 오버로드를 하나 이상 제공합니다.

 취소 토큰은 취소 토큰 소스(<xref:System.Threading.CancellationTokenSource> 개체)를 통해 생성됩니다.  소스의 <xref:System.Threading.CancellationTokenSource.Token%2A> 속성은 소스의 <xref:System.Threading.CancellationTokenSource.Cancel%2A> 메서드가 호출될 때 신호를 받을 취소 토큰을 반환합니다.  예를 들어 단일 웹 페이지를 다운로드하려고 하며 작업을 취소할 수 있게 하려는 경우 <xref:System.Threading.CancellationTokenSource> 개체를 만들고, 해당 토큰을 TAP 메서드에 전달한 후 작업을 취소할 준비가 되면 소스의 <xref:System.Threading.CancellationTokenSource.Cancel%2A> 메서드를 호출합니다.

```csharp
var cts = new CancellationTokenSource();
string result = await DownloadStringAsync(url, cts.Token);
… // at some point later, potentially on another thread
cts.Cancel();
```

 여러 비동기 호출을 취소하려면 모든 호출에 동일한 토큰을 전달할 수 있습니다.

```csharp
var cts = new CancellationTokenSource();
    IList<string> results = await Task.WhenAll(from url in urls select DownloadStringAsync(url, cts.Token));
    // at some point later, potentially on another thread
    …
    cts.Cancel();
```

 또는 작업의 선택적 하위 집합에 동일한 토큰을 전달할 수 있습니다.

```csharp
var cts = new CancellationTokenSource();
    byte [] data = await DownloadDataAsync(url, cts.Token);
    await SaveToDiskAsync(outputPath, data, CancellationToken.None);
    … // at some point later, potentially on another thread
    cts.Cancel();
```

 어떤 스레드에서도 취소 요청이 시작될 수 있습니다.

 취소 토큰을 수락하는 모든 메서드에 <xref:System.Threading.CancellationToken.None%2A?displayProperty=nameWithType> 값을 전달하여 취소가 절대 요청되지 않을 것을 나타낼 수 있습니다.  이렇게 하면 <xref:System.Threading.CancellationToken.CanBeCanceled%2A?displayProperty=nameWithType> 속성이 `false`를 반환하며, 호출된 메서드가 이에 따라 최적화될 수 있습니다.  테스트를 위해 토큰이 이미 취소된 상태 또는 취소 불가능 상태로 시작되어야 하는지를 나타내는 부울 값을 수락하는 생성자를 사용하여 인스턴스화된 미리 취소된 취소 토큰을 전달할 수도 있습니다.

 이러한 취소 방법에는 다음과 같은 여러 가지 이점이 있습니다.

-   제한 없는 수의 비동기 및 동기 작업에 동일한 취소 토큰을 전달할 수 있습니다.

-   동일한 취소 요청을 제한 없는 수의 수신기에 확산시킬 수 있습니다.

-   비동기 API의 개발자는 취소를 요청할 수 있는지 여부 및 적용되는 시기 등을 완전히 제어할 수 있습니다.

-   API를 사용하는 코드는 취소 요청이 전파되는 비동기 호출을 선택적으로 결정할 수 있습니다.

## <a name="monitoring-progress"></a>진행률 모니터링
 일부 비동기 메서드는 비동기 메서드에 전달된 진행률 인터페이스를 통해 진행 상황을 제공합니다.  예를 들어 텍스트 문자열을 비동기적으로 다운로드하고 지금까지 완료된 다운로드의 비율을 포함하는 진행률 업데이트를 야기하는 함수를 고려하세요.  이러한 메서드는 다음과 같이 WPF(Windows Presentation Foundation) 응용 프로그램에서 사용될 수 있습니다.

```csharp
private async void btnDownload_Click(object sender, RoutedEventArgs e)
{
    btnDownload.IsEnabled = false;
    try
    {
        txtResult.Text = await DownloadStringAsync(txtUrl.Text,
            new Progress<int>(p => pbDownloadProgress.Value = p));
    }
    finally { btnDownload.IsEnabled = true; }
}
```

<a name="combinators"></a>
## <a name="using-the-built-in-task-based-combinators"></a>기본 제공 작업 기반 조합기 사용
 <xref:System.Threading.Tasks> 네임스페이스에는 작업을 구성하고 사용하기 위한 몇 가지 메서드가 포함되어 있습니다.

### <a name="taskrun"></a>Task.Run
 <xref:System.Threading.Tasks.Task> 클래스에는 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체로 스레드 풀에 작업을 쉽게 오프로드할 수 있게 하는 몇 가지 <xref:System.Threading.Tasks.Task.Run%2A> 메서드가 포함되어 있습니다. 예를 들면 다음과 같습니다.

```csharp
public async void button1_Click(object sender, EventArgs e)
{
    textBox1.Text = await Task.Run(() =>
    {
        // … do compute-bound work here
        return answer;
    });
}
```

 <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=nameWithType> 오버로드와 같은 이러한 <xref:System.Threading.Tasks.Task.Run%2A> 메서드 중 일부는 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType> 메서드의 축약형으로 존재합니다.  <xref:System.Threading.Tasks.Task.Run%28System.Func%7BSystem.Threading.Tasks.Task%7D%29?displayProperty=nameWithType>과 같은 다른 오버로드를 사용하면 오프로드된 작업 내에서 await를 사용할 수 있습니다. 예를 들면 다음과 같습니다.

```csharp
public async void button1_Click(object sender, EventArgs e)
{
    pictureBox1.Image = await Task.Run(async() =>
    {
        using(Bitmap bmp1 = await DownloadFirstImageAsync())
        using(Bitmap bmp2 = await DownloadSecondImageAsync())
        return Mashup(bmp1, bmp2);
    });
}
```

 이러한 오버로드는 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType> 메서드를 작업 병렬 라이브러리의 <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> 확장 메서드와 함께 사용하는 것과 논리적으로 동일합니다.

### <a name="taskfromresult"></a>Task.FromResult
 데이터를 이미 사용할 수 있거나 <xref:System.Threading.Tasks.Task%601>에 리프트된 작업 반환 메서드에서 데이터를 반환하기만 하면 되는 시나리오에서는 <xref:System.Threading.Tasks.Task.FromResult%2A> 메서드를 사용합니다.

```csharp
public Task<int> GetValueAsync(string key)
{
    int cachedValue;
    return TryGetCachedValue(out cachedValue) ?
        Task.FromResult(cachedValue) :
        GetValueAsyncInternal();
}

private async Task<int> GetValueAsyncInternal(string key)
{
    …
}
```

### <a name="taskwhenall"></a>Task.WhenAll
 <xref:System.Threading.Tasks.Task.WhenAll%2A> 메서드를 사용하여 작업(task)으로 표현되는 여러 비동기 작업을 비동기적으로 대기합니다.  이 메서드에는 비일반 작업 집합 또는 균일하지 않은 일반 작업 집합을 지원하는 오버로드(예: 여러 void 반환 작업을 비동기적으로 대기하거나 각 값이 다른 형식을 가질 수 있는 여러 값 반환 메서드를 비동기적으로 대기) 및 균일한 일반 작업 집합을 지원하는 오버로드(여러 `TResult` 반환 메서드를 비동기적으로 대기)가 있습니다.

 여러 고객에게 전자 메일 메시지를 전송하려는 경우를 가정해 봅니다. 한 메시지가 완료될 때까지 기다렸다가 다음 메시지를 전송하지 않도록 메시지 전송을 겹칠 수 있습니다. 또한 보내기 작업이 완료될 때와 오류가 발생했는지 여부도 확인할 수 있습니다.또

```csharp
IEnumerable<Task> asyncOps = from addr in addrs select SendMailAsync(addr);
await Task.WhenAll(asyncOps);
```

 이 코드는 발생할 수 있는 예외를 명시적으로 처리하지 않지만 <xref:System.Threading.Tasks.Task.WhenAll%2A>의 결과 작업에 대한 `await`에서 예외가 전파되도록 합니다.  예외를 처리하려면 다음과 같은 코드를 사용할 수 있습니다.

```csharp
IEnumerable<Task> asyncOps = from addr in addrs select SendMailAsync(addr);
try
{
    await Task.WhenAll(asyncOps);
}
catch(Exception exc)
{
    ...
}
```

 이 경우 비동기 작업이 실패하면 모든 예외가 <xref:System.AggregateException> 예외에서 통합되어 <xref:System.Threading.Tasks.Task.WhenAll%2A> 메서드에서 반환되는 <xref:System.Threading.Tasks.Task>에 저장됩니다.  그러나 이러한 예외 중 하나만 `await` 키워드에 의해 전파됩니다.  모든 예외를 검사하려는 경우 앞의 코드를 다음과 같이 다시 작성할 수 있습니다.

```csharp
Task [] asyncOps = (from addr in addrs select SendMailAsync(addr)).ToArray();
try
{
    await Task.WhenAll(asyncOps);
}
catch(Exception exc)
{
    foreach(Task faulted in asyncOps.Where(t => t.IsFaulted))
    {
        … // work with faulted and faulted.Exception
    }
}
```

 웹에서 비동기적으로 여러 파일을 다운로드하는 예를 살펴보겠습니다.  이 경우 모든 비동기 작업이 동일한 결과 형식을 가지며 결과에 액세스하기 쉽습니다.

```csharp
string [] pages = await Task.WhenAll(
    from url in urls select DownloadStringAsync(url));
```

 이전의 void 반환 시나리오에서 설명한 것과 동일한 예외 처리 기술을 사용할 수 있습니다.

```csharp
Task [] asyncOps =
    (from url in urls select DownloadStringAsync(url)).ToArray();
try
{
    string [] pages = await Task.WhenAll(asyncOps);
    ...
}
catch(Exception exc)
{
    foreach(Task<string> faulted in asyncOps.Where(t => t.IsFaulted))
    {
        … // work with faulted and faulted.Exception
    }
}
```

### <a name="taskwhenany"></a>Task.WhenAny
 <xref:System.Threading.Tasks.Task.WhenAny%2A> 메서드를 사용하여 작업(task)으로 표현되는 여러 비동기 작업 중 하나가 완료될 때까지만 비동기적으로 대기할 수 있습니다.  이 메서드는 다음 네 가지 기본 사용 사례를 따릅니다.

-   중복: 작업을 여러 번 수행하고 먼저 완료되는 작업을 선택합니다(예를 들어, 단일의 결과를 생성하는 여러 주식 시세 웹 서비스에 연결하고 가장 빨리 완료되는 결과를 선택).

-   인터리브: 여러 작업을 시작하고 모두 완료해야 하지만 완료되었을 때 작업을 처리합니다.

-   스로틀: 다른 작업이 완료되면 추가 작업을 시작할 수 있습니다.  이것은 인터리브 시나리오의 확장입니다.

-   초기 재귀 한도: 예를 들어, 작업 t1으로 표시되는 작업은 다른 작업 t2를 사용하여 <xref:System.Threading.Tasks.Task.WhenAny%2A> 작업에서 그룹화할 수 있으며 <xref:System.Threading.Tasks.Task.WhenAny%2A> 작업에서 대기할 수 있습니다. 작업 t2는 시간 제한 또는 취소를 나타내거나 t1이 완료되기 전에 <xref:System.Threading.Tasks.Task.WhenAny%2A> 작업이 완료되도록 하는 일부 다른 신호를 나타낼 수 있습니다.

#### <a name="redundancy"></a>중복성
 주식 구매 여부를 결정하려는 경우를 고려해 봅니다.  신뢰할 수 있는 일부 주식 권장 웹 서비스가 있지만 매일의 부하에 따라 각 서비스가 서로 다른 시간에 느려질 수 있습니다.  다음과 같이 <xref:System.Threading.Tasks.Task.WhenAny%2A> 메서드를 사용하면 작업이 완료될 때 알림을 받을 수 있습니다.

```csharp
var recommendations = new List<Task<bool>>()
{
    GetBuyRecommendation1Async(symbol),
    GetBuyRecommendation2Async(symbol),
    GetBuyRecommendation3Async(symbol)
};
Task<bool> recommendation = await Task.WhenAny(recommendations);
if (await recommendation) BuyStock(symbol);
```

 성공적으로 완료된 모든 작업의 래핑되지 않은 결과를 반환하는 <xref:System.Threading.Tasks.Task.WhenAll%2A>과 달리, <xref:System.Threading.Tasks.Task.WhenAny%2A>는 완료된 작업을 반환합니다. 작업이 실패하면 해당 작업이 실패했다는 사실을 알아야 하고, 작업이 성공하면 해당 반환 값과 연결된 작업이 어떤 작업인지 알아야 합니다.  따라서 반환된 작업의 결과에 액세스하거나 이 예제에 나타난 대로 더 기다려야 합니다.

 <xref:System.Threading.Tasks.Task.WhenAll%2A>과 마찬가지로 예외를 수용할 수 있어야 합니다.  완료된 작업이 다시 수신되므로 반환된 작업이 오류를 전파하고 적절히 `try/catch`할 때까지 기다릴 수 있습니다.

```csharp
Task<bool> [] recommendations = …;
while(recommendations.Count > 0)
{
    Task<bool> recommendation = await Task.WhenAny(recommendations);
    try
    {
        if (await recommendation) BuyStock(symbol);
        break;
    }
    catch(WebException exc)
    {
        recommendations.Remove(recommendation);
    }
}
```

 또한 첫 번째 작업이 성공적으로 완료되더라도 후속 작업은 실패할 수 있습니다.  이 시점에서 예외를 처리할 수 있는 여러 옵션이 있습니다. <xref:System.Threading.Tasks.Task.WhenAll%2A> 메서드를 사용할 수 있는 경우 시작된 모든 작업이 완료될 때까지 기다릴 수도 있고 또는 모든 예외가 중요하며 로그온해야 한다고 결정할 수도 있습니다.  이를 위해 연속 작업을 사용하여 작업이 비동기적으로 완료되었을 때 알림을 받을 수 있습니다.

```csharp
foreach(Task recommendation in recommendations)
{
    var ignored = recommendation.ContinueWith(
        t => { if (t.IsFaulted) Log(t.Exception); });
}
```

 또는

```csharp
foreach(Task recommendation in recommendations)
{
    var ignored = recommendation.ContinueWith(
        t => Log(t.Exception), TaskContinuationOptions.OnlyOnFaulted);
}
```

 다음을 수행할 수도 있습니다.

```csharp
private static async void LogCompletionIfFailed(IEnumerable<Task> tasks)
{
    foreach(var task in tasks)
    {
        try { await task; }
        catch(Exception exc) { Log(exc); }
    }
}
…
LogCompletionIfFailed(recommendations);
```

 마지막으로 남은 모든 작업을 취소하려고 할 수도 있습니다.

```csharp
var cts = new CancellationTokenSource();
var recommendations = new List<Task<bool>>()
{
    GetBuyRecommendation1Async(symbol, cts.Token),
    GetBuyRecommendation2Async(symbol, cts.Token),
    GetBuyRecommendation3Async(symbol, cts.Token)
};

Task<bool> recommendation = await Task.WhenAny(recommendations);
cts.Cancel();
if (await recommendation) BuyStock(symbol);
```

#### <a name="interleaving"></a>인터리브
 웹에서 이미지를 다운로드하고 각 이미지를 처리하는 것을 고려해 봅니다(예: UI 컨트롤에 이미지 추가).  UI 스레드에서 순차적으로 처리를 수행해야 하지만 가능한 동시에 이미지를 다운로드하려고 할 것입니다. 또한 이미지가 모두 다운로드될 때까지 UI에 이미지를 추가하는 작업을 보류하지 않고 완료되는 대로 추가하려고 할 것입니다.

```csharp
List<Task<Bitmap>> imageTasks =
    (from imageUrl in urls select GetBitmapAsync(imageUrl)).ToList();
while(imageTasks.Count > 0)
{
    try
    {
        Task<Bitmap> imageTask = await Task.WhenAny(imageTasks);
        imageTasks.Remove(imageTask);

        Bitmap image = await imageTask;
        panel.AddImage(image);
    }
    catch{}
}
```

 다운로드한 이미지의 <xref:System.Threading.ThreadPool>에 대해 계산 집약적 처리를 발생시키는 시나리오에 인터리브를 적용할 수도 있습니다. 예를 들면 다음과 같습니다.

```csharp
List<Task<Bitmap>> imageTasks =
    (from imageUrl in urls select GetBitmapAsync(imageUrl)
         .ContinueWith(t => ConvertImage(t.Result)).ToList();
while(imageTasks.Count > 0)
{
    try
    {
        Task<Bitmap> imageTask = await Task.WhenAny(imageTasks);
        imageTasks.Remove(imageTask);

        Bitmap image = await imageTask;
        panel.AddImage(image);
    }
    catch{}
}
```

#### <a name="throttling"></a>스로틀
 사용자가 너무 많은 이미지를 다운로드하여 다운로드를 조절해야 하는 경우를 제외하고, 인터리브 예제를 고려해 보세요. 예를 들어 특정 횟수의 다운로드만 동시에 발생하도록 할 수 있습니다. 이를 위해 비동기 작업 일부를 시작할 수 있습니다.  작업이 완료되면 추가 작업을 추가해서 시작되도록 할 수 있습니다.

```csharp
const int CONCURRENCY_LEVEL = 15;
Uri [] urls = …;
int nextIndex = 0;
var imageTasks = new List<Task<Bitmap>>();
while(nextIndex < CONCURRENCY_LEVEL && nextIndex < urls.Length)
{
    imageTasks.Add(GetBitmapAsync(urls[nextIndex]));
    nextIndex++;
}

while(imageTasks.Count > 0)
{
    try
    {
        Task<Bitmap> imageTask = await Task.WhenAny(imageTasks);
        imageTasks.Remove(imageTask);

        Bitmap image = await imageTask;
        panel.AddImage(image);
    }
    catch(Exception exc) { Log(exc); }

    if (nextIndex < urls.Length)
    {
        imageTasks.Add(GetBitmapAsync(urls[nextIndex]));
        nextIndex++;
    }
}
```

#### <a name="early-bailout"></a>초기 재귀 한도 초과
 사용자의 취소 요청에 동시에 응답하면서 작업이 완료되기를 비동기적으로 기다리는 경우를 고려해 봅니다(예: 사용자가 취소 단추를 클릭한 경우). 다음 코드에서는 이 시나리오를 보여 줍니다.

```csharp
private CancellationTokenSource m_cts;

public void btnCancel_Click(object sender, EventArgs e)
{
    if (m_cts != null) m_cts.Cancel();
}

public async void btnRun_Click(object sender, EventArgs e)
{
    m_cts = new CancellationTokenSource();
    btnRun.Enabled = false;
    try
    {
        Task<Bitmap> imageDownload = GetBitmapAsync(txtUrl.Text);
        await UntilCompletionOrCancellation(imageDownload, m_cts.Token);
        if (imageDownload.IsCompleted)
        {
            Bitmap image = await imageDownload;
            panel.AddImage(image);
        }
        else imageDownload.ContinueWith(t => Log(t));
    }
    finally { btnRun.Enabled = true; }
}

private static async Task UntilCompletionOrCancellation(
    Task asyncOp, CancellationToken ct)
{
    var tcs = new TaskCompletionSource<bool>();
    using(ct.Register(() => tcs.TrySetResult(true)))
        await Task.WhenAny(asyncOp, tcs.Task);
    return asyncOp;
}
```

 이 구현은 재귀 한도가 초과되었다고 결정하는 즉시 사용자 인터페이스를 다시 사용하도록 설정하지만 기본 비동기 작업을 취소하지는 않습니다.  또 다른 방법은 재귀 한도가 초과되었다고 결정할 때 보류 중인 작업을 취소하지만, 취소 요청으로 인해 일찍 종료될 수 있으므로 작업이 실제로 완료될 때까지 사용자 인터페이스를 다시 설정하지 않는 것입니다.

```csharp
private CancellationTokenSource m_cts;

public async void btnRun_Click(object sender, EventArgs e)
{
    m_cts = new CancellationTokenSource();

    btnRun.Enabled = false;
    try
    {
        Task<Bitmap> imageDownload = GetBitmapAsync(txtUrl.Text, m_cts.Token);
        await UntilCompletionOrCancellation(imageDownload, m_cts.Token);
        Bitmap image = await imageDownload;
        panel.AddImage(image);
    }
    catch(OperationCanceledException) {}
    finally { btnRun.Enabled = true; }
}
```

 조기 종료의 또 다른 예제에는 <xref:System.Threading.Tasks.Task.WhenAny%2A> 메서드를 <xref:System.Threading.Tasks.Task.Delay%2A> 메서드와 함께 사용하는 방법(다음 섹션에서 논의함)이 포함됩니다.

### <a name="taskdelay"></a>Task.Delay
 <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> 메서드를 사용하여 비동기 메서드 실행에 일시 중지를 삽입할 수 있습니다.  이것은 폴링 루프 작성 및 미리 결정된 기간 동안 사용자 입력 처리 지연 등의 다양한 기능에 유용합니다.  또한 <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> 메서드를 <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType>와 함께 사용하면 대기 시간 제한을 구현하는 데 유용할 수 있습니다.

 더 큰 비동기 작업(예: ASP.NET 웹 서비스)에 속하는 작업(task)이 완료하는 데 너무 오래 걸리는 경우 전체 작업에 문제가 발생하며, 완료가 실패하는 경우에는 더 큰 문제가 됩니다.  이러한 이유로 비동기 작업을 대기하는 경우 시간이 초과되도록 할 수 있어야 합니다.  동기 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Task.WaitAll%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Task.WaitAny%2A?displayProperty=nameWithType> 메서드는 시간 제한 값을 허용하지만, 해당 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A?displayProperty=nameWithType>/<xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> 및 앞에서 언급한 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>/<xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> 메서드는 시간 제한 값을 허용하지 않습니다.  대신, <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType>를 함께 사용하여 시간 제한을 구현할 수 있습니다.

 예를 들어 UI 응용 프로그램에서 이미지를 다운로드하려고 하며 이미지를 다운로드하는 동안에 UI를 사용하지 않도록 설정하려고 합니다. 그러나 다운로드가 너무 오래 걸리는 경우 UI를 다시 사용하도록 설정하고 다운로드를 취소하려고 합니다.

```csharp
public async void btnDownload_Click(object sender, EventArgs e)
{
    btnDownload.Enabled = false;
    try
    {
        Task<Bitmap> download = GetBitmapAsync(url);
        if (download == await Task.WhenAny(download, Task.Delay(3000)))
        {
            Bitmap bmp = await download;
            pictureBox.Image = bmp;
            status.Text = "Downloaded";
        }
        else
        {
            pictureBox.Image = null;
            status.Text = "Timed out";
            var ignored = download.ContinueWith(
                t => Trace("Task finally completed"));
        }
    }
    finally { btnDownload.Enabled = true; }
}
```

 <xref:System.Threading.Tasks.Task.WhenAll%2A>이 작업을 반환하므로 동일한 사항이 여러 다운로드에 적용됩니다.

```csharp
public async void btnDownload_Click(object sender, RoutedEventArgs e)
{
    btnDownload.Enabled = false;
    try
    {
        Task<Bitmap[]> downloads =
            Task.WhenAll(from url in urls select GetBitmapAsync(url));
        if (downloads == await Task.WhenAny(downloads, Task.Delay(3000)))
        {
            foreach(var bmp in downloads) panel.AddImage(bmp);
            status.Text = "Downloaded";
        }
        else
        {
            status.Text = "Timed out";
            downloads.ContinueWith(t => Log(t));
        }
    }
    finally { btnDownload.Enabled = true; }
}
```

## <a name="building-task-based-combinators"></a>작업 기반 조합기 구축
 작업(task)이 완전히 비동기 작업을 나타내고 작업에 조인, 결과 가져오기 등을 위한 동기 및 비동기 기능을 제공할 수 있으므로 작업을 구성하여 더 큰 패턴을 구축하는 유용한 조합기 라이브러리를 빌드할 수 있습니다.  이전 섹션에서 설명한 것처럼 .NET Framework에는 몇 가지 기본 제공 조합기가 포함되어 있으나 직접 만들 수도 있습니다. 다음 섹션에서는 잠재적인 조합기 메서드 및 형식의 몇 가지 예를 제공합니다.

### <a name="retryonfault"></a>RetryOnFault
 대부분의 경우 이전 시도가 실패하면 작업을 다시 시도하려고 할 수 있습니다.  동기 코드의 경우 이를 위해 다음 예제의 `RetryOnFault`와 같은 도우미 메서드를 구축할 수 있습니다.

```csharp
public static T RetryOnFault<T>(
    Func<T> function, int maxTries)
{
    for(int i=0; i<maxTries; i++)
    {
        try { return function(); }
        catch { if (i == maxTries-1) throw; }
    }
    return default(T);
}
```

 TAP으로 구현되므로 작업(task)을 반환하는 비동기 작업에 대해서도 거의 동일한 도우미 메서드를 작성할 수 있습니다.

```csharp
public static async Task<T> RetryOnFault<T>(
    Func<Task<T>> function, int maxTries)
{
    for(int i=0; i<maxTries; i++)
    {
        try { return await function().ConfigureAwait(false); }
        catch { if (i == maxTries-1) throw; }
    }
    return default(T);
}
```

 이 조합기를 사용하여 응용 프로그램의 논리에 다시 시도를 인코딩할 수 있습니다. 예를 들면 다음과 같습니다.

```csharp
// Download the URL, trying up to three times in case of failure
string pageContents = await RetryOnFault(
    () => DownloadStringAsync(url), 3);
```

 `RetryOnFault` 함수를 추가로 확장할 수 있습니다. 예를 들어 이 함수는 다시 시도 중간에 호출되는 다른 `Func<Task>`를 수락하여 작업을 다시 시도해야 하는 시기를 결정할 수 있습니다. 예를 들면 다음과 같습니다.

```csharp
public static async Task<T> RetryOnFault<T>(
    Func<Task<T>> function, int maxTries, Func<Task> retryWhen)
{
    for(int i=0; i<maxTries; i++)
    {
        try { return await function().ConfigureAwait(false); }
        catch { if (i == maxTries-1) throw; }
        await retryWhen().ConfigureAwait(false);
    }
    return default(T);
}
```

 그런 후 다음과 같은 함수를 사용하여 작업을 다시 시도하기 전에 잠시 대기할 수 있습니다.

```csharp
// Download the URL, trying up to three times in case of failure,
// and delaying for a second between retries
string pageContents = await RetryOnFault(
    () => DownloadStringAsync(url), 3, () => Task.Delay(1000));
```

### <a name="needonlyone"></a>NeedOnlyOne
 경우에 따라 작업의 대기 시간 및 성공 가능성을 개선하기 위해 중복성을 이용할 수 있습니다.  주식 시세를 제공하는 여러 웹 서비스가 있으나 각 서비스는 하루 중 다른 시간에 다른 수준의 품질 및 응답 시간을 제공할 수 있습니다.  이러한 변동을 처리하려면 모든 웹 서비스로 요청을 보내고 응답을 받는 즉시 나머지 요청을 취소할 수 있습니다.  도우미 함수를 구현하면 여러 작업을 시작하고, 하나가 완료되기를 기다린 후 나머지는 취소하는 이러한 일반적인 패턴을 보다 쉽게 구현할 수 있습니다. 다음 예제의 `NeedOnlyOne` 함수는 이 시나리오를 보여 줍니다.

```csharp
public static async Task<T> NeedOnlyOne(
    params Func<CancellationToken,Task<T>> [] functions)
{
    var cts = new CancellationTokenSource();
    var tasks = (from function in functions
                 select function(cts.Token)).ToArray();
    var completed = await Task.WhenAny(tasks).ConfigureAwait(false);
    cts.Cancel();
    foreach(var task in tasks)
    {
        var ignored = task.ContinueWith(
            t => Log(t), TaskContinuationOptions.OnlyOnFaulted);
    }
    return completed;
}
```

 그런 후 이 함수를 다음과 같이 사용할 수 있습니다.

```csharp
double currentPrice = await NeedOnlyOne(
    ct => GetCurrentPriceFromServer1Async("msft", ct),
    ct => GetCurrentPriceFromServer2Async("msft", ct),
    ct => GetCurrentPriceFromServer3Async("msft", ct));
```

### <a name="interleaved-operations"></a>인터리브 작업
 매우 큰 작업 집합을 사용할 때 <xref:System.Threading.Tasks.Task.WhenAny%2A> 메서드를 사용하여 인터리브 시나리오를 지원할 경우 성능 문제가 발생할 수 있습니다.  <xref:System.Threading.Tasks.Task.WhenAny%2A>에 대한 모든 호출로 각 작업에 연속이 등록되게 됩니다. 작업 수가 N이면 인터리브 작업의 수명 동안 O(N2) 연속이 만들어집니다.  큰 작업을 하는 경우에는 성능 문제를 해결하기 위해 (다음 예의 `Interleaved`와 같은) 조합기를 사용할 수 있습니다.

```csharp
static IEnumerable<Task<T>> Interleaved<T>(IEnumerable<Task<T>> tasks)
{
    var inputTasks = tasks.ToList();
    var sources = (from _ in Enumerable.Range(0, inputTasks.Count)
                   select new TaskCompletionSource<T>()).ToList();
    int nextTaskIndex = -1;
    foreach (var inputTask in inputTasks)
    {
        inputTask.ContinueWith(completed =>
        {
            var source = sources[Interlocked.Increment(ref nextTaskIndex)];
            if (completed.IsFaulted)
                source.TrySetException(completed.Exception.InnerExceptions);
            else if (completed.IsCanceled)
                source.TrySetCanceled();
            else
                source.TrySetResult(completed.Result);
        }, CancellationToken.None,
           TaskContinuationOptions.ExecuteSynchronously,
           TaskScheduler.Default);
    }
    return from source in sources
           select source.Task;
}
```

 그런 다음 조합기를 사용하여 완료된 작업의 결과를 처리할 수 있습니다. 예를 들면 다음과 같습니다.

```csharp
IEnumerable<Task<int>> tasks = ...;
foreach(var task in Interleaved(tasks))
{
    int result = await task;
    …
}
```

### <a name="whenallorfirstexception"></a>WhenAllOrFirstException
 특정 분산/수집 시나리오에서 집합의 작업 하나가 실패하지 않는 한, 모든 작업이 완료되기를 기다리며, 실패하는 작업이 있으면 예외가 발생하는 즉시 대기를 중지할 수 있습니다.  다음 예제의 `WhenAllOrFirstException`과 같은 조합기 메서드로 이러한 작업을 수행할 수 있습니다.

```csharp
public static Task<T[]> WhenAllOrFirstException<T>(IEnumerable<Task<T>> tasks)
{
    var inputs = tasks.ToList();
    var ce = new CountdownEvent(inputs.Count);
    var tcs = new TaskCompletionSource<T[]>();

    Action<Task> onCompleted = (Task completed) =>
    {
        if (completed.IsFaulted)
            tcs.TrySetException(completed.Exception.InnerExceptions);
        if (ce.Signal() && !tcs.Task.IsCompleted)
            tcs.TrySetResult(inputs.Select(t => t.Result).ToArray());
    };

    foreach (var t in inputs) t.ContinueWith(onCompleted);
    return tcs.Task;
}
```

## <a name="building-task-based-data-structures"></a>작업 기반 데이터 구조 구축
 사용자 지정 작업 기반 조합기를 구축하는 기능 외에도, <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601>에서 비동기 작업의 결과와 조인을 위해 필요한 동기화를 모두 나타내는 데이터 구조를 유지하면 비동기 시나리오에서 사용할 사용자 지정 데이터 구조를 빌드할 수 있는 강력한 형식이 구현됩니다.

### <a name="asynccache"></a>AsyncCache
 작업의 한 가지 중요한 측면은 작업이 여러 소비자에게 전달될 수 있으며, 이들 모두가 작업을 대기하고, 작업에 연속을 등록하고, 해당 결과 또는 예외를 가져올(<xref:System.Threading.Tasks.Task%601>의 경우) 수 있다는 것입니다.  이로 인해 <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 개체가 비동기 캐싱 인프라에서 사용되는 데 완전히 적합하게 됩니다.  다음은 <xref:System.Threading.Tasks.Task%601> 개체를 기반으로 빌드한 작지만 강력한 비동기 캐시의 예입니다.

```csharp
public class AsyncCache<TKey, TValue>
{
    private readonly Func<TKey, Task<TValue>> _valueFactory;
    private readonly ConcurrentDictionary<TKey, Lazy<Task<TValue>>> _map;

    public AsyncCache(Func<TKey, Task<TValue>> valueFactory)
    {
        if (valueFactory == null) throw new ArgumentNullException("loader");
        _valueFactory = valueFactory;
        _map = new ConcurrentDictionary<TKey, Lazy<Task<TValue>>>();
    }

    public Task<TValue> this[TKey key]
    {
        get
        {
            if (key == null) throw new ArgumentNullException("key");
            return _map.GetOrAdd(key, toAdd =>
                new Lazy<Task<TValue>>(() => _valueFactory(toAdd))).Value;
        }
    }
}
```

 [AsyncCache\<TKey,TValue>](https://blogs.msdn.microsoft.com/pfxteam/2010/04/23/parallelextensionsextras-tour-12-asynccache/) 클래스는 `TKey`를 받고 <xref:System.Threading.Tasks.Task%601> 개체를 반환하는 함수를 해당 생성자에 대한 대리자로 허용합니다.  캐시에서 이전에 액세스했던 값은 내부 사전에 저장되며, 캐시에 동시에 액세스하더라도 `AsyncCache`는 키당 하나의 작업만 생성되도록 합니다.

 예를 들어 다운로드한 웹 페이지에 대한 캐시를 빌드할 수 있습니다.

```csharp
private AsyncCache<string,string> m_webPages =
    new AsyncCache<string,string>(DownloadStringAsync);
```

 그런 다음 웹 페이지의 콘텐츠가 필요할 때마다 비동기 메서드에서 이 캐시를 사용할 수 있습니다. `AsyncCache` 클래스는 가능한 작은 수의 페이지를 다운로드하도록 하고 결과를 캐시합니다.

```csharp
private async void btnDownload_Click(object sender, RoutedEventArgs e)
{
    btnDownload.IsEnabled = false;
    try
    {
        txtContents.Text = await m_webPages["https://www.microsoft.com"];
    }
    finally { btnDownload.IsEnabled = true; }
}
```

### <a name="asyncproducerconsumercollection"></a>AsyncProducerConsumerCollection
 또한 작업을 사용하여 비동기 활동을 조정하기 위한 데이터 구조를 구축할 수도 있습니다.  클래식 병렬 디자인인 생산자/소비자 중 하나를 고려하세요.  이 패턴에서 생산자는 소비자가 사용하는 데이터를 생성하고, 생산자와 소비자가 동시에 실행될 수 있습니다. 예를 들어, 소비자는 항목 2를 생성하고 있는 생산자가 이전에 생성한 항목 1을 처리합니다.  생산자/소비자 패턴의 경우 항상 소비자가 새 데이터에 대한 알림을 수신하고 사용 가능할 때 찾을 수 있도록 생산자가 만든 작업을 저장할 일부 데이터 구조가 필요합니다.

 비동기 메서드가 생산자 및 소비자로 사용할 수 있게 해 주는 작업 기반의 간단한 데이터 구조는 다음과 같습니다.

```csharp
public class AsyncProducerConsumerCollection<T>
{
    private readonly Queue<T> m_collection = new Queue<T>();
    private readonly Queue<TaskCompletionSource<T>> m_waiting =
        new Queue<TaskCompletionSource<T>>();

    public void Add(T item)
    {
        TaskCompletionSource<T> tcs = null;
        lock (m_collection)
        {
            if (m_waiting.Count > 0) tcs = m_waiting.Dequeue();
            else m_collection.Enqueue(item);
        }
        if (tcs != null) tcs.TrySetResult(item);
    }

    public Task<T> Take()
    {
        lock (m_collection)
        {
            if (m_collection.Count > 0)
            {
                return Task.FromResult(m_collection.Dequeue());
            }
            else
            {
                var tcs = new TaskCompletionSource<T>();
                m_waiting.Enqueue(tcs);
                return tcs.Task;
            }
        }
    }
}
```

 해당 데이터 구조가 준비되면 다음과 같이 코드를 작성할 수 있습니다.

```csharp
private static AsyncProducerConsumerCollection<int> m_data = …;
…
private static async Task ConsumerAsync()
{
    while(true)
    {
        int nextItem = await m_data.Take();
        ProcessNextItem(nextItem);
    }
}
…
private static void Produce(int data)
{
    m_data.Add(data);
}
```

<xref:System.Threading.Tasks.Dataflow> 네임스페이스에는 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 형식이 포함됩니다. 이 형식을 다음과 유사한 방식으로 사용할 수 있지만, 사용자 지정 컬렉션 형식을 빌드하지 않아도 됩니다.

```csharp
private static BufferBlock<int> m_data = …;
…
private static async Task ConsumerAsync()
{
    while(true)
    {
        int nextItem = await m_data.ReceiveAsync();
        ProcessNextItem(nextItem);
    }
}
…
private static void Produce(int data)
{
    m_data.Post(data);
}
```

> [!NOTE]
> <xref:System.Threading.Tasks.Dataflow> 네임스페이스는 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]에서 **NuGet**을 통해 사용할 수 있습니다. <xref:System.Threading.Tasks.Dataflow> 네임스페이스가 포함된 어셈블리를 설치하려면 Visual Studio에서 프로젝트를 열고 프로젝트 메뉴에서 **NuGet 패키지 관리**를 선택한 후 온라인으로 Microsoft.Tpl.Dataflow 패키지를 검색합니다.

## <a name="see-also"></a>참고 항목

- [TAP(작업 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)
- [작업 기반 비동기 패턴 구현](../../../docs/standard/asynchronous-programming-patterns/implementing-the-task-based-asynchronous-pattern.md)
- [다른 비동기 패턴 및 형식과의 Interop](../../../docs/standard/asynchronous-programming-patterns/interop-with-other-asynchronous-patterns-and-types.md)
